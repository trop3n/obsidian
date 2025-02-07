### All About YARA

*"The pattern matching swiss knife for malware researchers (and everyone else)" [Virustotal., 2020](https://virustotal.github.io/yara/)*
> With such a fitting quote, Yara can identify information based on both binary and textual patterns, such as hexadecimal and strings contained within a file.

Rules are used to label these patterns.

For example, Yara rules are frequently written to determine if a file is malicious or not, based upon the features - or patterns - it presents.

Strings are fundamental components of programming languages. Applications use strings to store data as text.

For example, the code snippet below prints "Hello World" in Python. The text "Hello World" would be stored a string.

`print("Hello World")`

We could write a Yara rule to search for "hello world" in every program on our operating system if we would like.
### Why Does Malware Use Strings?

Malware, just like our "Hello World" application, uses strings to store textual data. Here are a few examples of the data that various malware types store within strings:

|   |   |   |
|---|---|---|
|**Type**|**Data**|**Description**|
|Ransomware|[12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw](https://www.blockchain.com/btc/address/12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw)|Bitcoin Wallet for ransom payments|
|Botnet|12.34.56.7|The IP address of the Command and Control (C&C) server|
### Caveat: Malware Analysis

> Explaining the functionality of malware is vastly out of the scope of this room due to the sheer size of the topic. 
> 
> 	I have covered strings in much more detail in "Task 12 - Strings" of my [MAL: Introductory room](https://tryhackme.com/room/malmalintroductory). In fact, I am creating a whole Learning Path for it. If you'd like to get a taster whilst learning the fundamentals, I'd recommend my room.

# Introduction to Yara Rules

> The proprietary language that Yara uses is fairly trivial to pick up, but hard to master. This is because your rule is only as effective as your understanding of the patterns you want to search for.

Using a Yara rule is simple. Every `yara` command requires two arguments to be valid, these are:
1. The rule file we create
2. Name of the file, directory or process ID to use the rule for.

Every rule must have a name and condition.

For example, if we wanted to use "myrule.yar" on directory "some directory", we would use the following command:
`yara myrule.yar somedirectory`

Note that `.yar` is the standard file extension for all Yara rules. We'll make one of the most basic rules you can make below:

1. Make a file named "somefile" via `touch somefile`
2. Create a new file and name it "myfirstrule.yar" like below:

```shell
cmnatic@thm:~$ touch somefile
```

```shell
cmnatic@thm touch myfirstrule.yar
```

The **name** of the rule in this snippet is `examplerule`, where we have one condition, in this case, the **condition** is `condition`. As previously discussed, every rule requires both a name and a condition to be valid. This rule has satisfied those two requirements.

Simply, the rule we have made checks to see if the file/directory/PID that we specify exists via `condition: true`. If the file does exist, we are given the output of `examplerule`

Let's give this a try on the file **"somefile"** that we made in step one:  
`yara myfirstrule.yar somefile`  
  
If "somefile" exists, Yara will say `examplerule` because the pattern has been met - as we can see below:

           `cmnatic@thm:~$ yara myfirstrule.yar somefile  examplerule somefile`  

If the file does not exist, Yara will output an error such as that below:  
  

Yara complaining that the file does not exist

           `cmnatic@thm:~$ yara myfirstrule.yar sometextfile error scanning sometextfile: could not open file`
# Yara Conditions Continued

> Checking whether or not a file exists isn't all that helpful. After all, we can figure that our for ourselves...using much better tools for the job.

Yara has a few conditions, which I encourage you to read [here](https://yara.readthedocs.io/en/stable/writingrules.html) at your own leisure. However, I'll detail a few below and explain their purpose.

| Keyword    |
| ---------- |
| Desc       |
| Meta       |
| Strings    |
| Conditions |
| Weight     |
### Meta

> This section of a Yara rule is reserved for descriptive information by the author of the rule. For example, you can use `desc`, short for description, to summarize what your rule checks for. 
> 
> 	Anything within this section doesn't influence the rule itself. Similar to commenting code, it is useful to summarize your rule.

### String

> Remember our discussion about string in Task 2? Well, here we go. You can use strings to search for specific text or hexadecimal in files or programs. 
> 
> 	For example, say we wanted to search for a directory for all files containing "Hello World!", we would create a rule such as below:

```yara
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
}
```

> We define the keyword `Strings` where the string that we want to search, i.e., "Hello World!" is stored within the variable `$hello_world`

Of course, we need a condition here to make the rule valid. In this example, to make this string the condition, we need to use the variable's name. In this case: `$hello_world`:

```
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
		$hello_world
}
```

> Essentially, if any file has the string "Hello World!" then the rule will match. However, this is literally saying that it will only match "Hello World!" is found and will not match if "*hello world*" or "*HELLO WORLD.*"

To solve this, the condition `any of them` allows multiple strings to be searched for, like below:

```
rule helloword_checker{
	strings:
		$hello_world = "Hello World!"
		$hello_world_lowercase = "hello world"
		$hello_world_uppercase = "HELLO WORLD"

	condition:
		any of them
}
```

Now, any file with the strings of:
1. Hello World!
2. hello world
3. HELLO WORLD

Will now trigger the rule.
### Conditions

> We have already used the `true` and `any of them` condition. Much like regular programming, you can use operators such as:

>`<= less than or equal to`
>`= more than or equal to`
 `!= not equal to`

For example, the rule below would do the following:

```Yara
rule helloworld_checked{
	strings:
		$hello_world = "Hello World!"
	condition:
		#hello world <= 10
}
```

The rule will now:
1. Look for the "Hello World!" string.
2. Only say the rule matches if there are less than or equal to ten occurrences of the "Hello World!" string.
### Combining Keywords

> Moreover, you can use keywords such as:

`and`
`not`
`or`

To combine multiple conditions. Say if you wanted to check if a file has a string and is of a certain size In this example, the sample file we are checking is **less than** <10kb and has "Hello World!" you can use a rule like below:

```
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

		condition:
			$hello_world and filesize < 10KB
}
```

> The rule will only match if both conditions are true. 
> 
> To illustrate: below, the rule we created, in this case, did not match because although the file has "Hello World!", it has a file size larger than 10KB:

Yara failing to match the file mytextfile because it is larger than 10kb

           `cmnatic@thm:~$ <output intentionally left blank>`

> However, the rule matched this time because the file has both "Hello World!" and a file size of less than 10KB:

Yara successfully matching the file mytextfile because it has "Hello World" and a file size of less than 10KB

`cmnatic@thm:~$ yara myfirstrule.yar mytextfile.txt 
`helloworld_textfile_checker mytextfile.txt`

> Remembering that the text within the red box is the name of our rule, and the text within the green is the matched file.
### Anatomy of a Yara Rule

# Yara Modules

### Integrating with Other Libraries

> Frameworks such as the [Cuckoo Sandbox](https://cuckoosandbox.org/) or [Python's PE Module](https://pypi.org/project/pefile/) allow you to improve the technicality of your Yara rules ten-fold.
### Cuckoo

> Cuckoo Sandbox is an automated malware analysis environment. This module allows you to generate Yara rules based upon the behaviors discovered from Cuckoo Sandbox.

As the environment executes malware, you can create rules on specific behaviors such as runtime strings and the like.
### Python PE

> Python's PE module allows you to create Yara rules from the various sections and elements of the **Windows Portable Executable (PE)** structure.

Explaining this structure is out of scope as it is covered in the [malware introductory room](https://tryhackme.com/room/malmalintroductory). However, this *structure is the standard formatting of all executables and DLL files on Windows.* 

- Including the programming libraries that are used.

Examining a PE file's contents is an essential technique in malware analysis; this is because behaviors such as cryptography or worming can be largely identified without reverse engineering or execution of the sample.
# Other Tools and Yara

> Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. 

There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements.
### LOKI

> LOKI is a free open-source IOC scanner written/created by Florian Roth.

Based on the GitHub page, detection is based on 4 methods:

1. File Name IOC Check
2. Yara Rule Check
3. Hash Check
4. C2 Back Connect Check

There are additional checks that LOKI can be used for. For a full rundown, please reference the [GitHub readme](https://github.com/Neo23x0/Loki/blob/master/README.md).

LOKI can be used on both Windows and Linux systems and can be downloaded [here](https://github.com/Neo23x0/Loki/releases).
### THOR

> THOR *Lite* is Florian's newest multi-platform IOC AND YARA scanner. 

There are precompiled versions for Windows, Linux and macOS. 

A nice feature with THOR Lite is its scan throttling to limit exhausting CPU resources. For more information and/or to download the binary, start [here](https://www.nextron-systems.com/thor-lite/). 

> THOR Lite is the free version, with the main one being geared towards corporate customers.
### FENRIR

> This is the 3rd tool created by Neo23x0 (Florian Roth). You guessed it, the previous 2 are named above.

The updated version was created to address the issues from it's predecessors, where requirements must be mete for them to function.

*Fenrir is a bash script; it will run on any system capable of running Bash (nowadays, even Windows.)*
### YAYA

> YAYA was created by the EFF (Electronic Frontier Foundation) and released in September 2020. Based on their website, *"YAYA is a new open-source tool to help researchers manage multiple YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules and then lets researchers add their own rules, disable specific rules, and run scans of files."*
# Using LOKI

> As a security analyst, you may need to research various threat intelligence reports, blog postings, etc. and gather information based on the latest tactics and techniques seen in the wild, past or present.

Typically in these readings, IOCs (hashes, IP addresses, domain names, etc.) will be shared so rules can be created to detect these threats in your environment, along with Yara rules. 

On the flip side, you might find yourself in a situation where you've encountered something unknown, that your security stack of tools can't or didn't detect. 

- Using tools such as LOKI, you will need to add your own rules based on your threat intelligence gatherings or findings from an incident response engagement.
---

Loki is located in the `tools`. 

```
cmnatic@thm-yara:~/tools$ ls 
Loki  yarGen
```

> Navigate to the Loki directory. Run `python loki.py -h` to see what options are available.

If you are running Loki on your own system, the first command you should run is `--update`. This will add teh `signature-base` directory, which Loki uses to scan for known evil. 

- This command was already executed in the attached VM.
# Creating Yara Rules with yarGen

> From the previous section, we realized that we have file that Loki didn't flag on. At this point, we are unable to run Loki on other web servers because if **file2** exists in any of the other web servers, it will go undetected. 

We need to create a new Yara rule to detect this specific web shell in our environment. 

Typically this is what is done in the case of an incident, which is an event that affects/impacts the organization in a negative fashion. 

We can manually open the file and attempt to sift through lines upon lines of code to find possible strings that can be used in our newly created Yara rule. 

Let's check how many lines this particular file has. You can run the following: `strings <file name> | wc -l`

> If we were to try to go through this file string by string, line by line manually, you should quickly realize that this can be a daunting task.
---
> Luckily, we can use [yarGen](https://github.com/Neo23x0/yarGen) (yes, another tool created by Florian Roth) to aid us with this task.

What is yarGen? yarGen is a generator for Yara rules.

From the README - "*The main principle is the creation of Yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use.*"

To use yarGen to generate a Yara rule for file 2, you can run the following command:

`python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar`

> A brief explanation of the parameters above:

- `-m` is the path to the files you want to generate rules for
- `--excludegood` force to exclude all goodware strings (*these are strings found in legitmate software and can increase false positives*)
- `-o` location and name you want to output the Yara rule

> Generally, you would examine the Yara rule and remove any strings that you feel might generate false positives. 

For this exercise, we will leave the generated Yara rule as is and test to see if Yara will flag file2 or no.

**Note**: Another tool created to assist with this is called [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/) (you guessed it - created by Florian Roth). We will not examine that tool in this room, but you should read up on it, especially if you decide to start creating your own Yara rules.

**Further Reading on creating Yara rules and using yarGen**:

- [https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/](https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/)  
- [https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/](https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/)
- [https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/](https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/)
# Valhalla

> **Valhalla** is an online Yara feed created and hosted by [Nextron-Systems](https://www.nextron-systems.com/valhalla/). By now, you should be aware of the ridiculous amount of time and energy Florian has dedicated to creating these tools for the community. 

Per the website, "*Valhalla boosts your detection capabilities with the power of thousands of hand-crafted high-quality YARA rules.*"
We are provided with the name of the rule, a brief description, a reference link for more information about the rule, along with the rule date.

Picking up from our scenario, at this point, you know that the 2 files are related. Even though Loki classified the file are suspicious, you know in your gut that they are malicious. 

Hence the reason you created a Yara rule using yarGen to detect it on other web servers. But let's further pretend that you are not code-savvy (FYI, not all security professionals know how to code/script or read it).

You need to conduct further research regarding these files to receive approval to eradicate these files from the network.



