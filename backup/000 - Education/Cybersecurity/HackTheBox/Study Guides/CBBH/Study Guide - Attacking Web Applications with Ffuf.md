# Study Guide: Attacking Web Applications with Ffuf

## Introduction

### Practice Questions:

1. What is web fuzzing, and why is it important in web application security?
2. Name three common tools used for web fuzzing.
3. What is the primary purpose of using `ffuf` in web fuzzing?
4. How does automated fuzzing differ from manual fuzzing?
5. What are some common HTTP response codes that indicate a successful page discovery during fuzzing?
6. Why is it important to use wordlists in web fuzzing?
7. What is the difference between fuzzing for directories and fuzzing for files?
8. How can fuzzing help identify hidden vhosts?
9. What are some potential risks of using high thread counts in `ffuf`?
10. Why is it important to filter out certain HTTP response codes during fuzzing?

### Example Scenarios:

1. You are tasked with identifying all accessible directories on a web server. Describe the steps you would take using `ffuf`.
2. A colleague mentions that they found a directory but received an HTTP 403 response. What does this mean, and how should you proceed?
3. You need to fuzz a website for hidden files. Which wordlist would you use, and why?
4. Explain how you would determine if a web server is running PHP or ASP.NET using `ffuf`.
5. A scan returns multiple 404 responses. What does this indicate, and how would you refine your scan?
6. You want to fuzz for subdomains on a local development server. How would you configure `ffuf` for this task?
7. Describe how you would verify the existence of a discovered subdomain.
8. You notice that your fuzzing tool is sending too many requests and causing network issues. What adjustments would you make?
9. How would you use `ffuf` to identify hidden parameters in a web application?
10. A scan reveals a page with an HTTP 200 response but no visible content. What could this mean, and what would be your next steps?

---

## Web Fuzzing

### Practice Questions:

1. What is the basic concept behind web fuzzing for pages and directories?
2. Why is it impractical to manually fuzz web applications?
3. What is the role of wordlists in web fuzzing?
4. How do HTTP status codes help in determining the success of a fuzzing attempt?
5. What is the difference between a 404 and a 403 HTTP response code in the context of fuzzing?
6. Why is it important to use tools like `ffuf` for web fuzzing?
7. What are some common wordlists used for directory and file fuzzing?
8. How can you optimize the speed of a fuzzing scan without causing disruptions?
9. What is the significance of the `-w` flag in `ffuf`?
10. How does `ffuf` handle large wordlists efficiently?

### Example Scenarios:

1. You are given a target URL and asked to fuzz for directories. Write the `ffuf` command you would use.
2. A scan returns several 301 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for files with a `.php` extension. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both directories and files simultaneously.
5. You want to fuzz a website for hidden pages under a specific directory. Write the appropriate `ffuf` command.
6. A scan reveals a directory with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all `.html` files on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subdirectories under a known directory.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain pages. What could be the issue, and how would you resolve it?

---

## Directory Fuzzing

### Practice Questions:

1. What is the primary goal of directory fuzzing?
2. How do you specify the wordlist in `ffuf` for directory fuzzing?
3. What is the significance of the `FUZZ` keyword in `ffuf` commands?
4. How do you place the `FUZZ` keyword in a URL for directory fuzzing?
5. What are some common HTTP response codes that indicate a successful directory discovery?
6. Why is it important to filter out certain response sizes during directory fuzzing?
7. How can you increase the speed of a directory fuzzing scan?
8. What is the role of recursion in directory fuzzing?
9. How do you specify the depth of recursion in `ffuf`?
10. What is the difference between `-recursion` and `-recursion-depth` flags in `ffuf`?

### Example Scenarios:

1. You are tasked with fuzzing for directories on a web server. Write the `ffuf` command you would use.
2. A scan returns several 301 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for directories under a specific path. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both directories and files simultaneously.
5. You want to fuzz a website for hidden directories under `/admin`. Write the appropriate `ffuf` command.
6. A scan reveals a directory with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all directories on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subdirectories under a known directory.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain directories. What could be the issue, and how would you resolve it?

---

## Page Fuzzing

### Practice Questions:

1. What is the primary goal of page fuzzing?
2. How do you specify the wordlist in `ffuf` for page fuzzing?
3. What is the significance of the `FUZZ` keyword in `ffuf` commands for page fuzzing?
4. How do you place the `FUZZ` keyword in a URL for page fuzzing?
5. What are some common HTTP response codes that indicate a successful page discovery?
6. Why is it important to filter out certain response sizes during page fuzzing?
7. How can you increase the speed of a page fuzzing scan?
8. What is the role of extensions in page fuzzing?
9. How do you specify the extension in `ffuf` for page fuzzing?
10. What is the difference between fuzzing for directories and fuzzing for pages?

### Example Scenarios:

1. You are tasked with fuzzing for pages on a web server. Write the `ffuf` command you would use.
2. A scan returns several 200 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for pages with a `.php` extension. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both directories and pages simultaneously.
5. You want to fuzz a website for hidden pages under `/blog`. Write the appropriate `ffuf` command.
6. A scan reveals a page with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all `.html` files on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subpages under a known directory.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain pages. What could be the issue, and how would you resolve it?

---

## Recursive Fuzzing

### Practice Questions:

1. What is recursive fuzzing, and why is it useful?
2. How do you enable recursive scanning in `ffuf`?
3. What is the significance of the `-recursion` flag in `ffuf`?
4. How do you specify the depth of recursion in `ffuf`?
5. What are some potential risks of using deep recursion in fuzzing?
6. Why is it important to limit the depth of recursion in `ffuf`?
7. How can you optimize the speed of a recursive fuzzing scan?
8. What is the role of extensions in recursive fuzzing?
9. How do you specify the extension in `ffuf` for recursive fuzzing?
10. What is the difference between `-recursion` and `-recursion-depth` flags in `ffuf`?

### Example Scenarios:

1. You are tasked with performing a recursive fuzzing scan on a web server. Write the `ffuf` command you would use.
2. A scan returns several 301 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for directories and pages recursively under `/admin`. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both directories and pages recursively.
5. You want to fuzz a website for hidden directories and pages under `/blog`. Write the appropriate `ffuf` command.
6. A scan reveals a directory with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all directories and pages on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subdirectories and subpages under a known directory.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain directories and pages. What could be the issue, and how would you resolve it?

---

## DNS Records

### Practice Questions:

1. What is the purpose of DNS records in web fuzzing?
2. How do you add a custom domain to your `/etc/hosts` file?
3. What is the difference between public and private DNS records?
4. Why is it important to add custom domains to your `/etc/hosts` file during fuzzing?
5. What happens if a domain is not found in `/etc/hosts` or public DNS?
6. How do you verify that a custom domain has been added correctly to `/etc/hosts`?
7. What is the role of DNS in resolving domain names to IP addresses?
8. How do you troubleshoot DNS resolution issues during fuzzing?
9. What is the significance of the `Host` header in HTTP requests?
10. How do you use `ffuf` to fuzz for subdomains?

### Example Scenarios:

1. You are tasked with adding a custom domain to your `/etc/hosts` file. Write the command you would use.
2. A scan returns several 200 responses for subdomains. What does this indicate, and how would you proceed?
3. You need to fuzz for subdomains on a local development server. How would you configure `ffuf`?
4. Describe how you would verify the existence of a discovered subdomain.
5. You want to fuzz a website for hidden subdomains under `*.academy.htb`. Write the appropriate `ffuf` command.
6. A scan reveals a subdomain with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all subdomains on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subdomains under a known domain.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain subdomains. What could be the issue, and how would you resolve it?

---

## Sub-Domain Fuzzing

### Practice Questions:

1. What is the primary goal of sub-domain fuzzing?
2. How do you specify the wordlist in `ffuf` for sub-domain fuzzing?
3. What is the significance of the `FUZZ` keyword in `ffuf` commands for sub-domain fuzzing?
4. How do you place the `FUZZ` keyword in a URL for sub-domain fuzzing?
5. What are some common HTTP response codes that indicate a successful sub-domain discovery?
6. Why is it important to filter out certain response sizes during sub-domain fuzzing?
7. How can you increase the speed of a sub-domain fuzzing scan?
8. What is the role of recursion in sub-domain fuzzing?
9. How do you specify the depth of recursion in `ffuf` for sub-domain fuzzing?
10. What is the difference between `-recursion` and `-recursion-depth` flags in `ffuf` for sub-domain fuzzing?

### Example Scenarios:

1. You are tasked with fuzzing for sub-domains on a web server. Write the `ffuf` command you would use.
2. A scan returns several 301 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for sub-domains under a specific domain. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both sub-domains and directories simultaneously.
5. You want to fuzz a website for hidden sub-domains under `*.academy.htb`. Write the appropriate `ffuf` command.
6. A scan reveals a sub-domain with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all sub-domains on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for sub-sub-domains under a known sub-domain.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain sub-domains. What could be the issue, and how would you resolve it?

---

## Vhost Fuzzing

### Practice Questions:

1. What is the primary goal of vhost fuzzing?
2. How do you specify the wordlist in `ffuf` for vhost fuzzing?
3. What is the significance of the `FUZZ` keyword in `ffuf` commands for vhost fuzzing?
4. How do you place the `FUZZ` keyword in the `Host` header for vhost fuzzing?
5. What are some common HTTP response codes that indicate a successful vhost discovery?
6. Why is it important to filter out certain response sizes during vhost fuzzing?
7. How can you increase the speed of a vhost fuzzing scan?
8. What is the role of recursion in vhost fuzzing?
9. How do you specify the depth of recursion in `ffuf` for vhost fuzzing?
10. What is the difference between `-recursion` and `-recursion-depth` flags in `ffuf` for vhost fuzzing?

### Example Scenarios:

1. You are tasked with fuzzing for vhosts on a web server. Write the `ffuf` command you would use.
2. A scan returns several 200 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for vhosts under a specific domain. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both vhosts and directories simultaneously.
5. You want to fuzz a website for hidden vhosts under `*.academy.htb`. Write the appropriate `ffuf` command.
6. A scan reveals a vhost with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all vhosts on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for sub-vhosts under a known vhost.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain vhosts. What could be the issue, and how would you resolve it?

---

## Filtering Results

### Practice Questions:

1. What is the purpose of filtering results in `ffuf`?
2. How do you filter out specific HTTP response codes in `ffuf`?
3. What is the significance of the `-fs` flag in `ffuf`?
4. How do you filter out specific response sizes in `ffuf`?
5. What are some common HTTP response codes that should be filtered out during fuzzing?
6. Why is it important to filter out certain response sizes during fuzzing?
7. How can you increase the accuracy of your fuzzing results by filtering?
8. What is the role of the `-fc` flag in `ffuf`?
9. How do you filter out specific words in the response using `ffuf`?
10. What is the difference between `-fs` and `-fc` flags in `ffuf`?

### Example Scenarios:

1. You are tasked with filtering out 404 responses during a fuzzing scan. Write the `ffuf` command you would use.
2. A scan returns several 200 responses with a size of 900 bytes. How would you filter these out?
3. You need to filter out responses with a size of 0 bytes. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to filter out both 404 and 403 responses.
5. You want to fuzz a website for hidden pages while filtering out 404 responses. Write the appropriate `ffuf` command.
6. A scan reveals a page with an empty page. How would you filter out these results?
7. You are tasked with identifying all pages on a web server while filtering out 403 responses. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to filter out responses with a specific word count.
9. A scan returns multiple 403 responses. How would you refine your scan to filter these out?
10. You notice that your fuzzing tool is returning too many false positives. How would you adjust your filtering options?

---

## Parameter Fuzzing

### Practice Questions:

1. What is the primary goal of parameter fuzzing?
2. How do you specify the wordlist in `ffuf` for parameter fuzzing?
3. What is the significance of the `FUZZ` keyword in `ffuf` commands for parameter fuzzing?
4. How do you place the `FUZZ` keyword in a URL for parameter fuzzing?
5. What are some common HTTP response codes that indicate a successful parameter discovery?
6. Why is it important to filter out certain response sizes during parameter fuzzing?
7. How can you increase the speed of a parameter fuzzing scan?
8. What is the role of recursion in parameter fuzzing?
9. How do you specify the depth of recursion in `ffuf` for parameter fuzzing?
10. What is the difference between `-recursion` and `-recursion-depth` flags in `ffuf` for parameter fuzzing?

### Example Scenarios:

1. You are tasked with fuzzing for parameters on a web server. Write the `ffuf` command you would use.
2. A scan returns several 200 responses. What does this indicate, and how would you proceed?
3. You need to fuzz for parameters with a `.php` extension. How would you modify your `ffuf` command?
4. Describe how you would use `ffuf` to fuzz for both parameters and directories simultaneously.
5. You want to fuzz a website for hidden parameters under `/admin`. Write the appropriate `ffuf` command.
6. A scan reveals a parameter with an empty page. What could this mean, and what would be your next steps?
7. You are tasked with identifying all parameters on a web server. How would you configure `ffuf`?
8. Explain how you would use `ffuf` to fuzz for subparameters under a known parameter.
9. A scan returns multiple 403 responses. What does this indicate, and how would you refine your scan?
10. You notice that your fuzzing tool is not detecting certain parameters. What could be the issue, and how would you resolve it?