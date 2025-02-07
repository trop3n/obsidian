---
title: "Unsafe Archive Unpacking: Labs and Semgrep Rules · Doyensec's Blog"
source: "https://blog.doyensec.com/2024/12/16/unsafe-unpacking.html?utm_source=tldrsec.com&utm_medium=newsletter&utm_campaign=tl-dr-sec-262-red-teaming-ai-aws-org-policies-deep-dive-anti-edr-compendium"
author:
published:
created: 2025-01-17
description: "Unsafe Archive Unpacking: Labs and Semgrep Rules"
tags:
  - "clippings"
---
## Unsafe Archive Unpacking: Labs and Semgrep Rules

16 Dec 2024 - Posted by Michael Pastor

## Introduction

During my recent internship with Doyensec, I had the opportunity to research **decompression attacks** across different programming languages. As the use of archive file formats is widespread in software development, it is crucial for developers to understand the potential security risks involved in handling these files.

The objective of my research was to identify, analyze, and detect vulnerable implementations in several popular programming languages used for web and app development, including Python, Ruby, Swift, Java, PHP, and JavaScript. These languages have libraries for archive decompression that, when used improperly, may potentially lead to vulnerabilities.

To demonstrate the risk of unsafe unpacking, I created proof-of-concept (PoC) code with different vulnerable implementations for each method and each language. My work also focused on safe alternatives for each one of the vulnerable implementations. Additionally, I created a web application to upload and test whether the code used in a specific implementation is safe or not.

To efficiently search for vulnerabilities on larger codebases, I used a popular SAST (Static Application Security Testing) tool - [Semgrep](https://semgrep.dev/index.html). Specifically, I wrote a set of rules to automatically detect those vulnerable implementations which it will make it easier to identify vulnerabilities.

**Secure and insecure code, labs and Semgrep rules for all programming languages have been published on** [https://github.com/doyensec/Unsafe-Unpacking](https://github.com/doyensec/Unsafe-Unpacking).

## Understanding Archive Path Traversal

Extracting an archive (e.g., a ZIP file) usually involves reading all its contents and writing them to the specified extraction path. An archive path traversal aims to extract files to directories that are outside the intended extraction path.

This can occur when archive extraction is improperly handled, as archives may contain files with filenames referencing parent directories (e.g., using `../`). If not properly checked, these sequences may cause the extraction to occur outside the intended directory.

For example, consider a ZIP file with the following structure:

```js
/malicious
    /foo.txt
    /foo.py
    /../imbad.txt
```

When unzipping the archive to `/home/output`, if the extraction method does not validate or sanitize the file paths, the contents may be written to the following locations:

```plaintext
/home/output/foo.txt
/home/output/foo.py
/home/imbad.txt
```

As a result, `imbad.txt` would be written outside the intended directory. If the vulnerable program runs with high privileges, this could also allow the attacker to overwrite sensitive files, such as `/etc/passwd` – where Unix-based systems store user account information.

## Proving the Concept: Code Examples

To demonstrate the vulnerability, I created several proof-of-concept examples in various programming languages. These code snippets showcase vulnerable implementations where the archive extraction is improperly handled.

### Python

The combination of the `ZipFile` library as reader and `shutil.copyfileobj()` as writer makes the programmer responsible for handling the extraction correctly.

The usage of `shutil.copyfileobj()` is straightforward: as the first argument, we pass the file descriptor of the file whose contents we want to extract, and as the second argument, we pass the file descriptor to the destination file. Since the method receives file descriptors instead of paths, it doesn’t know if the path is out of the output directory, making the following implementation vulnerable.

```py
def unzip(file_name, output):
    # bad
    with zipfile.ZipFile(file_name, 'r') as zf:
        for filename in zf.namelist():
            # Output
            output_path = os.path.join(output, filename)
            with zf.open(filename) as source:
                with open(output_path, 'wb') as destination:
                    shutil.copyfileobj(source, destination)
                    
unzip1(./payloads/payload.zip", "./test_case")
```

If we run the previous code, we’ll realize that instead of extracting the zip content (`poc.txt`) to the `test_case` folder, it will be extracted to the parent folder:

```bash
$ python3 zipfile_shutil.py

$ ls test_case
# No output, empty folder

$ ls
payloads  poc.txt  test_case  zipfile_shutil.py
```

### Ruby

```rb
Zip::File.open(file_name).extract(entry, file_path)
```

The `extract()` method in Ruby’s `zip` library is used to extract an entry from the archive to the `file_path` directory. This method is unsafe since it doesn’t remove redundant dots and path separators. It’s the caller’s responsibility to make sure that `file_path` is safe:

```rb
require 'zip'
 
def unzip1(file_name, file_path)
  # bad
  Zip::File.open(file_name) do |zip_file|
    zip_file.each do |entry|
      extraction_path = File.join(file_path, entry.name)
      FileUtils.mkdir_p(File.dirname(extraction_path))
      zip_file.extract(entry, extraction_path) 
    end
  end
end

unzip1('./payloads/payload.zip', './test_case/')
```

```bash
$ ruby zip_unsafe.rb

$ ls test_case
# No output, empty folder

$ ls
payloads  poc.txt  test_case  zip_unsafe.rb
```

### PHP, Swift, JS and Java

All the other cases are documented in Doyensec’s [repository](https://github.com/doyensec/unsafe-Unpacking), along with the Semgrep rules and the labs.

## Unsafe Unpacking Labs

As part of the research, I developed a few web applications that allow users to test whether specific archive extraction implementations are vulnerable to decompression attacks.

![Class Pollution Gadgets](https://blog.doyensec.com/public/images/unsafe-unpacking-lab-1.png)

- **RUN**: without uploading an archive, the application will extract one of the prebuilt malicious archives. If the user uploads an archive, that archive will be unpacked instead.
- **Clear TXT Files**: the application will remove all the extracted files from the previous archives.
- **Fetch Directory Contents**: the web application will show you both the `archive directory` (where files are supposed to be extracted) and the `current directory` (where files are NOT supposed to be extracted).

![Class Pollution Gadgets](https://blog.doyensec.com/public/images/unsafe-unpacking-lab-2.png)

These web application labs are available for every language except Swift, for which a desktop application is provided instead.

## Developing Semgrep Rules for Vulnerability Detection

One of the most efficient ways to detect vulnerabilities in open-source projects is by using static application analysis tools. Semgrep is a fast, open-source, static analysis tool that searches code, finds bugs, and enforces secure guardrails and coding standards.

Semgrep works by scanning source code for specific syntax patterns. Since it supports various programming languages and makes it simple to write custom rules, it was ideal for my research purposes.

In the following example I’m using the `Unsafe-Unpacking/Python/PoC/src` folder from the GitHub repository, which contains 5 unzipping vulnerabilities. You can run the Semgrep rule by using the following command:

```sh
semgrep scan --config=../../rules/zip_shutil_python.yaml

...

┌─────────────────┐
│ 5 Code Findings │
└─────────────────┘

    zipfile_shutil.py
   ❯❯❱ rules.unsafe_unpacking
          Unsafe Zip Unpacking

           13┆ shutil.copyfileobj(source, destination)
            ⋮┆----------------------------------------
           21┆ shutil.copyfileobj(source, destination)
            ⋮┆----------------------------------------
           31┆ shutil.copyfileobj(source, destination)
            ⋮┆----------------------------------------
           41┆ shutil.copyfileobj(source, destination)
            ⋮┆----------------------------------------
           57┆ shutil.copyfileobj(source_file, target_file)
```

A set of **15 rules** can be found in the GitHub repository.

## Mitigation

Since in most of the vulnerable implementations the programmer is responsible for sanitizing or validating the output path, they can take two approaches to mitigate the problem.

### 1\. Path Sanitization

To sanitize the path, the filename should be normalized. In the case of Ruby, the method `Path.basename` can be used, which removes redundant dots and converts a path like `../../../../bad.txt` to `bad.txt`.

In the following code, when using `File.join` to compute the output path, `File.basename` is called to sanitize the entry filename from the archive, mitigating the vulnerability:

```rb
def safe_unzip(file_name, output)
  # good
  Zip::File.open(file_name) do |zip_file|
    zip_file.each do |entry|
      # sanitize the entry path
      file_path = File.join(output, File.basename(entry.name))
      FileUtils.mkdir_p(File.dirname(file_path))
      zip_file.extract(entry, file_path) 
    end
  end
end
```

The side effect of this mitigation is that the archive’s folder structure is flattened, and all files are extracted to a single folder. Due to this, the solution may not be ideal for many applications.

Another solution would be using `Pathname.new().cleanpath`, `pathname` (a built-in Ruby class). It can normalize paths and remove any `../` sequences:

```rb
require 'pathname'

def safe_unzip(file_name, output)
  output += File::SEPARATOR unless output.end_with?(File::SEPARATOR)

  Zip::File.open(file_name) do |zip_file|
    zip_file.each do |entry|
      # Remove any relative path components like "../"
      sanitized_name = Pathname.new(entry.name).cleanpath.to_s
      sanitized_path = File.join(output, sanitized_name)

      FileUtils.mkdir_p(File.dirname(sanitized_path))
      zip_file.extract(entry, sanitized_path)
    end
  end
end
```

However, if the developer wants to sanitize the path themselves by removing `../` using any kind of replacement, they should make sure that the sanitization is applied repeatedly until there are no `../` sequences left. Otherwise, cases like the following can occur, leading to a bypass:

```rb
entry = "..././bad.txt"
sanitized_name = entry.gsub(/(\.\.\/)/, '') # ../bad.txt
```

### 2\. Path Validation

Before writing the contents of the entry to the destination path, you should ensure that the write path is within the intended destination directory. This can be done by using `start_with?` to check if the write path starts with the destination path, which prevents directory traversal attacks.

```rb
def safe_unzip(file_name, output)
  output += File::SEPARATOR unless output.end_with?(File::SEPARATOR)
  # good
  Zip::File.open(file_name) do |zip_file|
    zip_file.each do |entry|
      safe_path = File.expand_path(entry.name, output)

      unless safe_path.start_with?(File.expand_path(output))
        raise "Attempted Path Traversal Detected: #{entry.name}"
      end

      FileUtils.mkdir_p(File.dirname(safe_path))
      zip_file.extract(entry, safe_path) 
    end
  end
end
```

It’s important to note that `File.expand_path` should be used instead of `File.join`. Using `File.expand_path()` is crucial because it converts a relative file path into an absolute file path, ensuring proper validation and preventing path traversal attacks.

For example, consider the following secure approach using `File.expand_path`:

```rb
# output = Ruby/PoC/test_case

# path = Ruby/PoC/secret.txt
path = File.expand_path(entry_var, output)

# Check for path traversal
unless path.start_with?(File.expand_path(output))
    raise "Attempted Path Traversal Detected: #{entry_var}"
end
```

In this case `File.expand_path` converts `path` to an absolute path, and the check with `start_with` correctly verifies whether the extracted file path is within the intended output directory.

On the other hand, if you use `File.join` to build the output path, it may result in vulnerabilities:

```rb
# output = Ruby/PoC/test_case

# path = Ruby/PoC/test_case/../secret.txt
path = File.join(output, entry_var)

# Incorrect check
unless path.start_with?(File.expand_path(output))
    raise "Attempted Path Traversal Detected: #{entry_var}"
end
```

The check would incorrectly return *true* even though the path actually leads outside the intended directory (`test_case/../secret.txt`), allowing an attacker to bypass the validation and perform a path traversal. The takeaway is to always **normalize** the path before verifying.

One detail I missed, which my mentor (Savio Sisco) pointed out, is that in the original `safe_method`, I didn’t include the following line:

```rb
output += File::SEPARATOR unless output.end_with?(File::SEPARATOR)
```

Without this line, it was still possible to bypass the `start_with` check. Although path traversal is not possible in this case, it could still lead to writing outside of the intended directory:

```rb
output = "/home/user/output"
entry.name = "../output_bypass/bad.txt"
safe_path = File.expand_path(entry.name, output) # /home/user/output_bypass/bad.txt
safe_path.start_with?(File.expand_path(output))# true
```

## Conclusions

This research delves into the issue of unsafe archive extraction across various programming languages. The post shows how giving developers more freedom also places the responsibility on them. While manual implementations are important, they can also introduce serious security risks.

Additionally, as security researchers, it is important to understand the root cause of the vulnerability. By developing Semgrep rules and labs, we hope it will help others to identify, test and mitigate these vulnerabilities. All these resources are available in the Doyensec [repository](https://github.com/doyensec/unsafe-Unpacking).

Decompression attacks are a broad field of research. While this blog covers some cases related to file extraction, there are still many other attacks, such as zip bombs and symlink attacks, that need to be considered.

### A Few Thoughts On My Internship

Although this blog post is not about the internship, I would like to use this opportunity to discuss my experience too.

Two years ago, during my OSWE preparation, I came across a Doyensec blog post, and I used them as study resource . Months later, I found out they here hiring for an internship which I thought was an incredible opportunity.

The first time I applied, I received my very first technical challenge — a set of vulnerable code that was a lot of fun to work with if you enjoy reading code. However, I wasn’t able to pass the challenge that year. This year, after two interview rounds with Luca and John, I was finally accepted. The interviews were 360 degree, covering various aspects like how to fix a vulnerability, how computers work, how to make a secure snippet vulnerable, and how to approach threat modeling.

In my first few weeks, I was assigned to some projects with a lot of guidance from other security engineers. I had the chance to talk to them about their work at Doyensec and even chat with one former intern about his internship experience. I learned a lot about the company’s methodology, not only in terms of bug hunting but also in how to be more organized — both in work and in life. Just like many CTF players, I was used to working late into the night, but since I wasn’t working alone on these projects, this habit started to interfere with communication. Initially, it felt strange to open Burp when the sun was still up, but over time, I got used to it. I didn’t realize how much this simple change could improve my productivity until I fully adjusted.

Working on projects with large codebases or complex audits really pushed me to keep searching for bugs, even when it seemed like a dead end. There were times when I got really nervous after days without finding anything of interest. However, Savio was a great help during these moments, advising me to stay calm and stick to a clear methodology instead of letting my nerves drive me hunt without thinking. Eventually, I was able to find some cool bugs on those projects.

Even though I had very high expectations, this experience definitely lived up to them. A huge thanks to the team, especially Luca and Savio, who took great care of me throughout the entire process.