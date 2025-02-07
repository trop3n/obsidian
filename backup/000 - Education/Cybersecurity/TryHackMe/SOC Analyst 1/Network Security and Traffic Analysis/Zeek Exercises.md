# Anomalous DNS

**An alert triggered: "Anomalous DNS Activity".**

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive.

A terminal window will pop-up, time to move to the Exercise-Files directory. To do this we will use the `cd` command, which stands for change directory. We will use this command in combination with Tab completion. With Tab complete, you only have to press Tab after starting to type, and if it only has one entry that matches, it will auto-complete it. So let’s type out the command `cd Desktop/Exercise-Files/`, then press enter to run the command. Follow up with the `ls` command to see the contents of the directory.

## Task 2 Anomalous DNS[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#task-2-anomalous-dns)

**An alert triggered:** “Anomalous DNS Activity”.

The case was assigned to you. Inspect the PCAP and retrieve the artifacts to confirm this alert is a true positive.

## Answer the questions below[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#answer-the-questions-below)

First, move into the anomalous-dns directory with the `cd` command. So the command we are doing is `cd anomalous-dns/`, then press enter to move into the directory. Then use `ls` to see the contents of the directory.

### Investigate the **dns-tunneling.pcap** file. Investigate the **dns.log** file. What is the number of DNS records linked to the IPv6 address?[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#investigate-the--dns-tunnelingpcap--file-investigate-the--dnslog--file-what-is-the-number-of-dns-records-linked-to-the-ipv6-address)

So we want to use run Zeek against the pcap file. To do this we will use the command `zeek -r dns-tunneling.pcap`, then press enter to run Zeek. Using `ls`, will show the content and log files in the current directory.

Now let’s cat the dns log file and pipe it through less to see if we can figure out the name of the field we want to see it. Also, the question here wasn’t very clear so at first I was searching the IP addresses for an IPv6 address, and found one. But what they are asking for here is, a certain DNS record associated with the IPv6 address, and what is the number of occurrences of this DNS record are. So knowing this and looking at the hint that TryHackMe gives, we are looking for the quad A record (AAAA). Know all this let’s run the command `cat dns.log | less`, then press enter to run. When you get in the dns log file through less press the right arrow key till reaching the quad A record.

After looking at the fields and counting, I determined that the name of the field we are looking for is qtype_name. Press `q` to exit out of less.

Knowing the field we need to zeek-cut, time to do a little Command-Line Kung-Fu! The command being `cat dns.log | zeek-cut qtype_name | grep "AAAA" | uniq -c`, then press enter to run. After we zeek-cut the field out, we then pipe that into grep which we then pull out only quad A results. Then take the results from grep and pipe that into uniq and get rid of the duplicates and count the number of times it occurred. After this command runs we are left with the answer in the output, type it into the TryHackMe answer field, then click submit.

**Answer: 320**

### Investigate the **conn.log** file. What is the longest connection duration?[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#investigate-the--connlog--file-what-is-the-longest-connection-duration)

Now let’s cat the conn log file and pipe it through less to see if we can figure out the name of the field we want to see it. So the command we want to use is `cat conn.log | less`, and press enter to run.

At a quick glance at the different fields, we see that one of the field names is duration. This seems to be the field we want to use, time to use some zeek-cut.

Time to use zeek-cut, sort, and tail with some pipes. The command that we want to use is `cat conn.log | zeek-cut duration | sort -n | tail -1`, and press enter to run the code. We take the field and run it through zeek-cut, and pipe the results through sort. Sort has the dash/tick n for sorting numerically, then we pipe the results of sort through tail. Tail gives the last 10 results unless told otherwise, which we are telling it to with the dash/tick 1. After running the command, you are left with the result in the output of the terminal, type the answer into the TryHackMe answer field, then click submit.

**Answer: 9.420791**

### Investigate the **dns.log** file. Filter all unique DNS queries. What is the number of unique domain queries?[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#investigate-the--dnslog--file-filter-all-unique-dns-queries-what-is-the-number-of-unique-domain-queries)

To start we will pipe the DNS log file into less to find the field we want to look at, to do this use the command `cat dns.log | less`, press enter to run.

At a quick glance at the different fields, we see that one of the field names is query. This seems to be the field we want to use, time to use some zeek-cut.

Let’s use zeek-cut along with some new commands to find the answer. After trying multiple combinations, and finally looking at the hint the full command I used was `cat dns.log | zeek-cut query | rev | cut -d '.' -f 1-2 | rev | sort | uniq`, and press enter to run. We take and zeek cut the query field out, then pipe the results through to rev. Rev then reverses the string of characters, which then get’s piped to cut. Cut will then work like zeek-cut and with the parameters of -d for the delimiter and we chose the period, the -f stands for field, and 1–2 is for the first and second field. Now the results of cut are piped back into rev to reverse the string of characters once more, aka they are now in the proper order. The results from rev are piped into sort, to sort them alphabetically. Finally, the results from sort are piped into uniq to remove any duplicates. After the command has run, you are left with a single output of each unique domain query. Count them to get your answer, once you have counted them type it into the TryHackMe answer field, then click submit.

**Answer: 6**

### There are a massive amount of DNS queries sent to the same domain. This is abnormal. Let’s find out which hosts are involved in this activity. Investigate the **conn.log** file. What is the IP address of the source host?[](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/#there-are-a-massive-amount-of-dns-queries-sent-to-the-same-domain-this-is-abnormal-lets-find-out-which-hosts-are-involved-in-this-activity-investigate-the--connlog--file-what-is-the-ip-address-of-the-source-host)

To start we will pipe the conn log file into less to find the field we want to look at, to do this use the command `cat conn.log | less`, press enter to run.

At a quick glance at the different fields, we see that two of the field names are id.orig_h and id.resp_h. This seems to be the field we want to use, time to use some zeek-cut.

Time to use zeek-cut, sort, and uniq with some pipes. The command that we want to use is `cat conn.log | zeek-cut id.orig_h id.resp_h | sort -n | uniq -c`, then press enter. We take the field and run it through zeek-cut, and pipe the results through sort. Sort has the dash/tick n for sorting numerically. Finally, the results from sort are piped into uniq to remove any duplicates. After you run the command you are left with the results, one of those results is over two thousand times. The answer is the source IP address from this row. Once you find it type it into the TryHackMe answer field, then click submit.

**Answer: 10.20.57.3**

You have finished these tasks, and can now move on to Task 3 Phishing, Task 4 Log4J, & Task 5 Conclusion.

# Task 3 - Phishing

**An alert triggered:** “Phishing Attempt”.

The case was assigned to you. Inspect the PCAP and retrieve the artifacts to confirm this alert is a true positive.

## Answer the questions below[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#answer-the-questions-below)

First, we need to move into the correct directory, to do this we need to use the command `cd phishing/`, then press enter. Using `ls` will list out the directories contents.

[![](https://miro.medium.com/max/562/1*Ffq2-F9syTEIqGW5f3lJsA.png)](https://miro.medium.com/max/562/1*Ffq2-F9syTEIqGW5f3lJsA.png)

Next, let’s run Zeek against the phishing pcap file. To do this we use the command `zeek -r phishing.pcap`, and press enter. Then use `ls` to see the contents of the current directory.

[![](https://miro.medium.com/max/528/1*v0eiRxpsy2ct-y4UxXI7sw.png)](https://miro.medium.com/max/528/1*v0eiRxpsy2ct-y4UxXI7sw.png)
### Investigate the logs. What is the suspicious source address? Enter your answer in **defanged format**.[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the-logs-what-is-the-suspicious-source-address-enter-your-answer-in--defanged-format)

After doing some investigating myself, I came to the realization that they want to know what the infected local machine is. So I went to the dhcp.log file and looked at it with `cat dhcp.log | less`, pressing enter to open it.

[![](https://miro.medium.com/max/519/1*1g8mNsmOpn-l_7nMJWbvCg.png)](https://miro.medium.com/max/519/1*1g8mNsmOpn-l_7nMJWbvCg.png)
At a quick glance at the different fields, we see that one of the field names is client_addr. This seems to be the field we want to use, time to use some zeek-cut.

[![](https://miro.medium.com/max/630/1*Zz46_emeHHIg4wI0d3UTeA.png)](https://miro.medium.com/max/630/1*Zz46_emeHHIg4wI0d3UTeA.png)

To keep with using the command line, I asked ChatGPT what is the command line script to defang an IP address. It gave me a bin/bash script to do this, I then asked it for one that doesn’t require bin/bash. ChatGPT gave me this script `echo "IP address" | sed -e 's/\./[.]/g'`.

[![](https://miro.medium.com/max/630/1*RbVQdCMnpyCZ6m7YccjMmg.png)](https://miro.medium.com/max/630/1*RbVQdCMnpyCZ6m7YccjMmg.png)
So with our newly learned code from ChatGPT, and the command line kung-fu we already know let us get the answer. So the command we use is `cat dhcp.log | zeek-cut client_addr | uniq | sed -e 's/\./[.]/g'`, and press enter to run. We take the field and run it through zeek-cut, and pipe the results through uniq. Uniq is used to remove any duplicates, then we pipe the results into sed to defang the IP address. After running the command we are left with a defanged IP address in the output of the terminal, and the answer to the question. Type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/630/1*_d4yRlcLxvbQgL4q43s8Pg.png)](https://miro.medium.com/max/630/1*_d4yRlcLxvbQgL4q43s8Pg.png)

**Answer: 10[.]6[.]27[.]102**

### Investigate the **http.log** file. Which domain address were the malicious files downloaded from? Enter your answer in **defanged format**.[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--httplog--file-which-domain-address-were-the-malicious-files-downloaded-from-enter-your-answer-in--defanged-format)

Now let’s cat the HTTP log file and pipe it through less to see if we can figure out the name of the field we need to use.

[![](https://miro.medium.com/max/630/1*-OwMfwIcCrNJIqMWCugP-g.png)](https://miro.medium.com/max/630/1*-OwMfwIcCrNJIqMWCugP-g.png)
Once less opens the HTTP log file, press the right arrow key once.
[![](https://miro.medium.com/max/630/1*eL7uHCuSpmRgNab108t64Q.png)](https://miro.medium.com/max/630/1*eL7uHCuSpmRgNab108t64Q.png)

We can see the name of the field we are looking for is host, and if we remember the malicious file from task 2. We can see it here, along with the domain that it was downloaded from. Time to use some zeek-cut, so press `q` to exit less.

[![](https://miro.medium.com/max/630/1*xuJ7H9biguhlvcfpu0NZkw.png)](https://miro.medium.com/max/630/1*xuJ7H9biguhlvcfpu0NZkw.png)

With the name of the field, and some command line kung-fu let’s get the answer. The command we are going to run is `cat http.log | zeek-cut host | grep "smart-fax" | uniq | sed -e 's/\./[.]/g'`, press enter to run the command. We take the field and run it through zeek-cut, and pipe the results through grep. Using grep we pull out only the host that matches our string, we then pipe those results into uniq. With uniq we get rid of the duplicates, and we then pipe those results into sed. Finally with sed to defang the domain. After running the command we are left with a defanged domain in the output of the terminal, and the answer to the question. Type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/630/1*cEETe7jsYGEhDKctl1cauw.png)](https://miro.medium.com/max/630/1*cEETe7jsYGEhDKctl1cauw.png)

**Answer: smart-fax[.]com**

### Investigate the malicious document in VirusTotal. What kind of file is associated with the malicious document?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the-malicious-document-in-virustotal-what-kind-of-file-is-associated-with-the-malicious-document)

To start off, we need to run Zeek again, this time with the script hash-demo.zeek. The command we are going to run is `zeek -C -r phishing.pcap hash-demo.zeek`, and press enter to run. After Zeek is done, us the command `ls` to show the contents of the current directory.

[![](https://miro.medium.com/max/630/1*aIV2ShtdGuCgo2ExbEzXEQ.png)](https://miro.medium.com/max/630/1*aIV2ShtdGuCgo2ExbEzXEQ.png)

Now let’s cat the files log file and pipe it through less to see if we can figure out the name of the field we need to use

[![](https://miro.medium.com/max/630/1*OWKoTIfCs1kdAkEQE_W8Xw.png)](https://miro.medium.com/max/630/1*OWKoTIfCs1kdAkEQE_W8Xw.png)

Once less opens the files log file, press the right arrow key once.

[![](https://miro.medium.com/max/630/1*07JiXs5YK8QgSiEL4tdigw.png)](https://miro.medium.com/max/630/1*07JiXs5YK8QgSiEL4tdigw.png)

From the Zeek room, we know that we want to look at the mime_type field. We can see this by the fact that the application/msword is in this field.

[![](https://miro.medium.com/max/630/1*PkwhAEkvK_n3KCAIdvMEHA.png)](https://miro.medium.com/max/630/1*PkwhAEkvK_n3KCAIdvMEHA.png)

Next, we need to look at the hash field, use the right arrow key to move to the right till you reached the hashes. Once there, you will see the name of the md5 hash field. Now we have all the info we need for now, press `q` to exit less.

[![](https://miro.medium.com/max/630/1*5ZCVPoPY6EBr1dt2ZMkAOQ.png)](https://miro.medium.com/max/630/1*5ZCVPoPY6EBr1dt2ZMkAOQ.png)

So to get the hash that we need we can use some command line kung-fu. The command we are using is `cat files.log | zeek-cut mime_type md5 | grep "word"` , then press enter to run. You will have the hash will be in the output of the terminal.

[![](https://miro.medium.com/max/630/1*yqAROCrNJ3n2LWSJHmborQ.png)](https://miro.medium.com/max/630/1*yqAROCrNJ3n2LWSJHmborQ.png)

Highlight the hash, right-click on the highlighted hash, then click Copy on the drop-down menu.

[![](https://miro.medium.com/max/411/1*Rqe7WouyeKwI7q6Ob0CbyA.png)](https://miro.medium.com/max/411/1*Rqe7WouyeKwI7q6Ob0CbyA.png)

Open a browser, go to the [VirusTotal](https://www.virustotal.com/) website (I provided the link to the site). Once the site loads, click the SEARCH tab in the middle of the screen.

[![](https://miro.medium.com/max/630/1*ESRY4cRzb2PYcqCbQvRuog.png)](https://miro.medium.com/max/630/1*ESRY4cRzb2PYcqCbQvRuog.png)

A search field will be in the middle of the page, using the keyboard shortcut ctrl + v to paste the hash in search field and press enter to search the hash.

[![](https://miro.medium.com/max/630/1*zgsj5yx6yyvgzKrQoPPDzQ.png)](https://miro.medium.com/max/630/1*zgsj5yx6yyvgzKrQoPPDzQ.png)

Once the DETECTION page loads, click the RELATIONS tab.

[![](https://miro.medium.com/max/630/1*xttkQ0u0YZCNxGe9w3ud8A.png)](https://miro.medium.com/max/630/1*xttkQ0u0YZCNxGe9w3ud8A.png)

Once the RELATIONS page loads, scroll down till you see Bundled Files section.

[![](https://miro.medium.com/max/630/1*WXfURGkLPk0sQDjCET4y_g.png)](https://miro.medium.com/max/630/1*WXfURGkLPk0sQDjCET4y_g.png)

Once you reach the Bundled Files section, you will see a column labeled File type. The three-letter file abbreviation is the answer, type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/583/1*2_SqDc_fX-glNcO_BsxWHw.png)](https://miro.medium.com/max/583/1*2_SqDc_fX-glNcO_BsxWHw.png)

**Answer: VBA**

### Investigate the extracted malicious **.exe** file. What is the given file name in Virustotal?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the-extracted-malicious--exe--file-what-is-the-given-file-name-in-virustotal)

Head back to the terminal and leave VirusTotal open. Since we know the field to look at from the previous question, let’s use zeek-cut and grep to get hash for the exe file. The command being `cat files.log | zeek-cut mime_type md5 | grep "exe"`, press enter to run the command.

[![](https://miro.medium.com/max/630/1*_93Adl-__kmDwXzbloxjdw.png)](https://miro.medium.com/max/630/1*_93Adl-__kmDwXzbloxjdw.png)

Highlight the hash, right-click on the highlighted hash, then click Copy on the drop-down menu.

[![](https://miro.medium.com/max/422/1*Qt0qlzjs54nsiet2J0ETmg.png)](https://miro.medium.com/max/422/1*Qt0qlzjs54nsiet2J0ETmg.png)

Back at VirusTotal highlight the hash at the top of the page, and press the delete key to remove it from the search field.

[![](https://miro.medium.com/max/630/1*XcAWXoPhJc6sSPOx8H6x6g.png)](https://miro.medium.com/max/630/1*XcAWXoPhJc6sSPOx8H6x6g.png)

Use the keyboard shortcut ctrl + v to paste the new hash into the search field, then press enter to search it.

[![](https://miro.medium.com/max/630/1*-vWcH9SZPS1w8crD51krGQ.png)](https://miro.medium.com/max/630/1*-vWcH9SZPS1w8crD51krGQ.png)

Once the DETECTION tab loads, you can see this is malicious. At the top is a box that has some general information about the file. Inside this box, under the hash, you will see the name of the file, and thus the answer to the question. Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer field, then click submit.

[![](https://miro.medium.com/max/630/1*GRbeWeBrjkEmVEXB66Eg1g.png)](https://miro.medium.com/max/630/1*GRbeWeBrjkEmVEXB66Eg1g.png)

**Answer: PleaseWaitWindow.exe**

### Investigate the malicious **.exe** file in VirusTotal. What is the contacted domain name? Enter your answer in **defanged format**.[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the-malicious--exe--file-in-virustotal-what-is-the-contacted-domain-name-enter-your-answer-in--defanged-format)

Go back to VirusTotal, you already have the exe file hash searched in VirusTotal so we just need to do a little looking for the answer to this question. Once back on VirusTotal, click the RELATIONS tab.

[![](https://miro.medium.com/max/630/1*WX6Rjev11i75HNp7GGNCzA.png)](https://miro.medium.com/max/630/1*WX6Rjev11i75HNp7GGNCzA.png)

The first section is Contacted Domains, there is one that has a detection. You don’t need the full domain for the answer, just every after dunlop.. You can type the answer in and defange it yourself or use the command `echo hopto.org | sed -e 's/\./[.]/g'`, and press enter to run. Highlight copy (ctrl + c) and paste (ctrl + v) from the VM or type, the answer into the TryHackMe answer field, then click submit.

[![](https://miro.medium.com/max/630/1*OAzTU6Eg4gHjFA5Xl1GOag.png)](https://miro.medium.com/max/630/1*OAzTU6Eg4gHjFA5Xl1GOag.png)

**Answer:hopto[.]org**

### Investigate the **http.log** file. What is the request name of the downloaded malicious **.exe** file?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--httplog--file-what-is-the-request-name-of-the-downloaded-malicious--exe--file)

Head back to your terminal in the VM, use the command `cat http.log | grep "exe"`, you will see the name of the malicious file. Type the answer into the TryHackMe answer field, then click submit.

[![](https://miro.medium.com/max/630/1*72WJ18j5LJiqqtYt_Fmq4A.png)](https://miro.medium.com/max/630/1*72WJ18j5LJiqqtYt_Fmq4A.png)

**Answer: knr.exe**

## Task 4 Log4J[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#task-4-log4j)

**An alert triggered:** “Log4J Exploitation Attempt”.

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive.

## Answer the questions below[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#answer-the-questions-below-1)

First we need to move from the phishing directory to the log4j directory. Use the command `cd ..`, to back out of the current directory. Then using the command `cd log4j/`, to move forward into the log4j directory. Finally, use the command `ls` to list the content of the current directory.

[![](https://miro.medium.com/max/517/1*B645dZT2RU8I5jGk0MnDfw.png)](https://miro.medium.com/max/517/1*B645dZT2RU8I5jGk0MnDfw.png)

### Investigate the **log4shell.pcapng file** with **detection-log4j.zeek** script. Investigate the **signature.log** file. What is the number of signature hits?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--log4shellpcapng-file-with-detection-log4jzeek--script-investigate-the--signaturelog--file-what-is-the-number-of-signature-hits)

Start by using the command `zeek -C -r log4shell.pcapng detection-log4j.zeek`, press enter to run. Then use the command `ls`to see the contents of the current directory.

[![](https://miro.medium.com/max/630/1*hM3EGlv2e41yNQwAcELLRA.png)](https://miro.medium.com/max/630/1*hM3EGlv2e41yNQwAcELLRA.png)

Now let’s cat the signatures log file and pipe it through less to see if we can find the answer.

[![](https://miro.medium.com/max/630/1*Ok8C-2FUkQoItNSo55TCSg.png)](https://miro.medium.com/max/630/1*Ok8C-2FUkQoItNSo55TCSg.png)

Once less opens the signatures log file, press the right arrow key once.

[![](https://miro.medium.com/max/630/1*DS91l9joDwKY_I3vjQy9QQ.png)](https://miro.medium.com/max/630/1*DS91l9joDwKY_I3vjQy9QQ.png)

If you count the number of Signatures here in the note field you will get your answer. But I will show you the command line way of finding it. Press `q` to exit less.

[![](https://miro.medium.com/max/630/1*iOgtivm1-DiaFqI7A_s1vA.png)](https://miro.medium.com/max/630/1*iOgtivm1-DiaFqI7A_s1vA.png)

Back in the terminal, we want to use the command `cat signatures.log | zeek-cut note | uniq -c`, press enter after you were done typing the command. After you have run the command you will have the answer in the output of the terminal, type it into the TryHackMe answer field, then click submit.

[![](https://miro.medium.com/max/630/1*f_vdy3eRZ4rDXhgKO9R6nw.png)](https://miro.medium.com/max/630/1*f_vdy3eRZ4rDXhgKO9R6nw.png)

**Answer: 3**

### Investigate the **http.log** file. Which tool is used for scanning?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--httplog-file-which-tool-is-used-for-scanning)

Now let’s cat the http log file and pipe it through less to see if we can find the answer.

[![](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)

Once less opens the http log file, press the right arrow key once.

[![](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)

As we look through the user_agent field we can see some interesting information, so the field we are looking for is user_agent. Time to use some zeek-cut, so press `q` to exit less

[![](https://miro.medium.com/max/630/1*m1meI6lkscdrr2XDTp10Lw.png)](https://miro.medium.com/max/630/1*m1meI6lkscdrr2XDTp10Lw.png)

Knowing the field we want to look at let’s run zeek-cut, sort, and uniq. The command being `cat http.log | zeek-cut user_agent | sort | uniq`, after you have finished typing out the command press enter. We use zeek-cut to “cut” that field out to look at, taking the results for zeek-cut we pipe it through sort. With sort, the results are sorted alphabetically, those results are then piped through uniq. Finally uniq will remove any dupilcates. After the command is finished running, look through the output you should be able to notice a famous network mapping program (wink wink). Once you find it, type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/630/1*QuJ712VKjXaFMjzeHanJCg.png)](https://miro.medium.com/max/630/1*QuJ712VKjXaFMjzeHanJCg.png)

**Answer: Nmap**

### Investigate the **http.log** file. What is the extension of the exploit file?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--httplog--file-what-is-the-extension-of-the-exploit-file)

Now let’s cat the http log file and pipe it through less to see if we can find the answer.

[![](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)

Once less opens the http log file, press the right arrow key once.

[![](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)

As we look through the user_agent field we can see some interesting information, so the field we are looking for is uri. Time to use some zeek-cut, so press `q` to exit less

[![](https://miro.medium.com/max/630/1*jtT9mjEtVYBdnAK5TQFMeQ.png)](https://miro.medium.com/max/630/1*jtT9mjEtVYBdnAK5TQFMeQ.png)

Knowing the field we want to look at let’s run zeek-cut, sort, and uniq. The command being `cat http.log | zeek-cut uri | sort | uniq`, after you have finished typing out the command press enter. We use zeek-cut to “cut” that field out to look at, taking the results for zeek-cut we pipe it through sort. With sort, the results are sorted alphabetically, those results are then piped through uniq. Finally uniq will remove any dupilcates. After the command is finished running, look through the output you should be able to see only one file extension, this is the answer. Once you find it, type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/630/1*CHUjbXZ_wCPwctuKCKhRzQ.png)](https://miro.medium.com/max/630/1*CHUjbXZ_wCPwctuKCKhRzQ.png)

**Answer: .class**

### Investigate the **log4j.log** file. Decode the base64 commands. What is the name of the created file?[](https://haircutfish.com/posts/Zeek-Exercises-Task3-Phishing-Task4-Log4J-and-Task5-Conclusion/#investigate-the--log4jlog--file-decode-the-base64-commands-what-is-the-name-of-the-created-file)

Now let’s cat the log4j log file and pipe it through less to see if we can find the answer. Once the log4j file opens in less, looking through the fields along with the field contents we can see some of the base64 we need to decode. Time to use some command line kung-fu to help slim down the results.

[![](https://miro.medium.com/max/630/1*NEBgt7pQAoSNDVxtU5_xhQ.png)](https://miro.medium.com/max/630/1*NEBgt7pQAoSNDVxtU5_xhQ.png)

Time for the command line kung-fu, the command we want to run is `cat log4j.log | zeek-cut uri | sort -nr | uniq`, after you have done typing the command out press enter to run it. You will see three base64 codes in the output. Next we will be decoding them.

[![](https://miro.medium.com/max/630/1*btXF3MEovOXEuqOyxRgDUg.png)](https://miro.medium.com/max/630/1*btXF3MEovOXEuqOyxRgDUg.png)

To decode all three the take the same steps to reach. First step is to highlight the base64 code, then right-click on it. On the drop-down menu click copy.

[![](https://miro.medium.com/max/406/1*ZPhbsrZQWKS9zhT7oi4WWg.png)](https://miro.medium.com/max/406/1*ZPhbsrZQWKS9zhT7oi4WWg.png)

Then type `echo` into the terminal, using the paste shortcut for linux terminal, ctrl + shift + v, paste the base64 code into the terminal. Then pipe it to `base64 -d`, this command will take a base64 code and decode it. So the command is `echo {base64 code} | base64 -d`, press enter to run the code.

[![](https://miro.medium.com/max/630/1*IUPqoRraVRpHn0UNLo9VoQ.png)](https://miro.medium.com/max/630/1*IUPqoRraVRpHn0UNLo9VoQ.png)

Repeat these steps for the other two base64 codes. Now that you have them all decoded, you should see the name of the file created at the end of the first line. Touch is used to create, and with the name on the end this says that this is the name of the file. Once you have found it, type the answer into the TryHackMe answer field, and click submit.

[![](https://miro.medium.com/max/630/1*92zMUCSShyIALwJa-tIV8Q.png)](https://miro.medium.com/max/630/1*92zMUCSShyIALwJa-tIV8Q.png)

**Answer: pwned**