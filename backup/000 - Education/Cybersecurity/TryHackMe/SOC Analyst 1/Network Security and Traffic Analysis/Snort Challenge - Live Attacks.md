
# Answer the questions below

## First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

If we remember back from the Snort room how to run in sniffer mode, we want to use the `-v` for Verbose.

![](https://miro.medium.com/v2/resize:fit:700/1*RnnFDZzhvYVeIhMmdFEl8Q.png)

So knowing what tack we want to use, let’s start to run Snort in sniffer mode. We will use the command `sudo snort -v -l .`, we use the `-l` to log and the `.` to log it in our current directory.

![](https://miro.medium.com/v2/resize:fit:651/1*SWL6EP4XKpZU1MGWoQAD9A.png)

Let that run for 10–15 seconds, then press the keyboard ctrl + c to stop Snort. Let snort finish, when it is done, the terminal will be waiting to accept another command.

![](https://miro.medium.com/v2/resize:fit:700/1*4pEXZV1nKxmg275Yim3aHQ.png)

To be able to make our rule we first need to look at the log file to see what we have captured. Since we know that Snort names it’s log files snort.log{set of numbers}, we can use Tab complete. With Tab complete, you only have to press Tab after starting to type, and if it only has one entry that matches, it will auto complete it. Using Tab complete, use the command `sudo snort -r snort.log.1672414629 -X`, then press enter to run.

![](https://miro.medium.com/v2/resize:fit:541/1*HYHwFig7Quw6qhB1TKQF2A.png)

After Snort is done reading the file, and outputting it to the screen. We need to scroll up to the last packet.

![](https://miro.medium.com/v2/resize:fit:699/1*oIOM_lmwDx4IC9qBEj2i2w.png)

After inspecting the packets, I kept seeing port 22 coming up. Not just in the Destination side either but in the source.

![](https://miro.medium.com/v2/resize:fit:700/1*h3z4TtncXDfLuSunlw_Npw.png)

So using grep, I ran the same command and added grep to the end of it. That command being `sudo snort -r snort.log.1672414629 -X | grep :22`, see way I can see if it is a thread I should follow.

![](https://miro.medium.com/v2/resize:fit:654/1*B2MTgbrYGNW02Wj-QFTMig.png)

Sure enough, it does come up quite a lot.

![](https://miro.medium.com/v2/resize:fit:482/1*RYX8Z0u5coSpcqYY45QtAA.png)

So, knowing that SSH runs on port 22, I then used grep to search for ssh in the packets with the command `sudo snort -r snort.log.1672414629 -X | grep "ssh"`.

![](https://miro.medium.com/v2/resize:fit:651/1*tMM4Yk7zf1rMGndUFnskiQ.png)

When Snort is done, scroll up to the top of the output. I am sure you will see as you scroll up that we have found some ssh results. When you make it to the top, start to scroll down through, and not too far down you will find a hit.

![](https://miro.medium.com/v2/resize:fit:677/1*CaQ5jCiD8BQaK0r4CsNvMw.png)

So let’s narrow it down and take a look at that packet. To do this I used the command `sudo snort -r snort.log.1672414629 -X -n 30`, this will only output the first 30 packets to the terminal.

![](https://miro.medium.com/v2/resize:fit:659/1*ctkUrAXhGtryDK7qs_iJWg.png)

When Snort is done, scroll up, you should spot the packet right away. It stands out amongst the others.

![](https://miro.medium.com/v2/resize:fit:700/1*X9Ob8NyiaXJRWp_iKyyzog.png)

Looking at the top of the packet, we can see the source is matches what we saw before. So we should have enough information to write our rule.

![](https://miro.medium.com/v2/resize:fit:700/1*bZKeRvvm4RuLQ9hxgbyigA.png)

## Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

- Create the rule and test it with “-A console” mode.
- Use **“-A full”** mode and the **default log path** to stop the attack.
- Write the correct rule and run the Snort in IPS “-A full” mode.
- **Block the traffic at least for a minute** and then the flag file will appear on your desktop.

First, we need to open the local.rules file in a text editor. Using the command `sudo gedit /etc/snort/rules/local.rules`, and press enter

![](https://miro.medium.com/v2/resize:fit:628/1*QkhUytGPN2tGuPoP8r67kg.png)

Looking back at Task 9 of the Snort room, and we can see what Action must be taken.

![](https://miro.medium.com/v2/resize:fit:700/1*KsQMztdiAqU-LPzkBL8d0A.png)

Time to write our rule, to start it off we won’t be writing alert as we usually have. No, this time we will write `drop`. Then from the packet we know it’s a `tcp`protocol. The next section is source IP address, we will put `any 22`, as we want to specify the port. Followed by the `<>` directional arrows. For the destination IP address, we are going to put `any any`. The reasoning behind using any on both parts is what if the attacker changes IP addresses, you are now ahead of the game. Now the second half of the rule, for the msg: section I put `"SSH Connection attempted"`. To finish off the rule since we only have one, the sid: should be `100001`, and the rev: will stay at `1`. It should look as such so far `drop tcp any 22 <> any any (msg:"SSH Connection attempted"; sid:100001; rev:1;)`.

![](https://miro.medium.com/v2/resize:fit:660/1*R3z92i9pj7nBCh7LrxEE-Q.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/v2/resize:fit:700/1*7sDcTkuaxQPmcsr9zLncNw.png)

## Stop the attack and get the flag (which will appear on your Desktop)

Almost time to run our rule against the live traffic, but first we need to know how we are to run the Snort. If we look back at Task 7 of the Snort room, we can see how we need to run the rule.

![](https://miro.medium.com/v2/resize:fit:700/1*U94yRJcOMd3j4YhL1zeVxg.png)

After seeing the command we have to use to run the rule, the only change that needs to be made is instead of console on the end we put full. so the command it `sudo snort -c /ect/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full`, the press enter and let it run till you see the flag.txt file pop-up on the desktop.

![](https://miro.medium.com/v2/resize:fit:700/1*7ZV1DcfcPqgseeLEAtVUTg.png)

Once the flag.txt file appears, you can stop snort with ctrl +c. Then double-click on the flag.txt icon to open it.

![](https://miro.medium.com/v2/resize:fit:210/1*gJLFtY7t8K_maw_D4OIq9A.png)

After opening it you will be greeted with the flag.

# Scenario 2 | Reverse-Shell

## Answer the questions below

### First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

If we remember back from the Snort room how to run in sniffer mode, we want to use the `-v` for Verbose.

![](https://miro.medium.com/v2/resize:fit:700/1*RnnFDZzhvYVeIhMmdFEl8Q.png)

So knowing what tack we want to use, let’s start to run Snort in sniffer mode. We will use the command `sudo snort -v -l .`, we use the `-l` to log and the `.` to log it in our current directory.

![](https://miro.medium.com/v2/resize:fit:647/1*LU82yNdTI3O9ieie_q1y5w.png)

Let that run for 10–15 seconds, then press the keyboard ctrl + c to stop Snort. Let snort finish, when it is done, the terminal will be waiting to accept another command.

![](https://miro.medium.com/v2/resize:fit:417/1*DAeUPg0W_MUwliOFEPD_ZQ.png)

To be able to make our rule we first need to look at the log file to see what we have captured. Since we know that Snort names it’s log files snort.log{set of numbers}, we can use Tab complete. With Tab complete, you only have to press Tab after starting to type, and if it only has one entry that matches, it will auto complete it. Using Tab complete, use the command `sudo snort -r snort.log.1672697486 -X`, then press enter to run.

![](https://miro.medium.com/v2/resize:fit:539/1*c1JVnlwVZGxqIgYItj98_A.png)

After Snort is done reading the file, and outputting it to the screen. We need to scroll up to the last packet.

![](https://miro.medium.com/v2/resize:fit:508/1*5iWACnO6K5u5_A4I3X5Cpw.png)

As we can see from inspecting some of the packets, the port in the source and destination of some of the packets is 4444. This could indcate the possibilty of a reverse shell.

![](https://miro.medium.com/v2/resize:fit:650/1*TzeEKw9vZuvlk2VRXHKYfQ.png)

Time to use grep to search the log file for port 4444, and see if we get any results. The command we are going to use is `sudo snort -r snort.log.1672697486 -X | grep ":4444"`, then press enter to run Snort.

![](https://miro.medium.com/v2/resize:fit:647/1*SkRWkSL5w--GlSDeFWwuSg.png)

Look at the results shows us that we are looking in the right direction.

![](https://miro.medium.com/v2/resize:fit:660/1*OMBCxPfmipK82sHeb91wAg.png)

Let’s run snort again only getting 10 results back from the 5,000+ we have. To do this we use the command `sudo snort -r snort.log.1672697486 -X -n 10`, press enter to run Snort.

![](https://miro.medium.com/v2/resize:fit:647/1*A8qYblF56UQpc4P7zEalWw.png)

We should have enough information now to write a rule for snort!

![](https://miro.medium.com/v2/resize:fit:647/1*S6nNo_dy2j-bRPk5PcI9_g.png)

## Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

- Create the rule and test it with “-A console” mode.
- Use **“-A full”** mode and the **default log path** to stop the attack.
- Write the correct rule and run the Snort in IPS “-A full” mode.
- **Block the traffic at least for a minute** and then the flag file will appear on your desktop.

First, we need to open the local.rules file in a text editor. Using the command `sudo gedit /etc/snort/rules/local.rules`, and press enter

![](https://miro.medium.com/v2/resize:fit:628/1*QkhUytGPN2tGuPoP8r67kg.png)

Looking back at Task 9 of the Snort room, and we can see what Action must be taken.

![](https://miro.medium.com/v2/resize:fit:700/1*KsQMztdiAqU-LPzkBL8d0A.png)

Time to write our rule, to start it off we won’t be writing alert as we usually have. No, this time we will write `drop`. Then from the packet we know it’s a `tcp`protocol. The next section is source IP address, we will put `any 4444`, as we want to specify the port. Followed by the `<>` directional arrows. For the destination IP address, we are going to put `any any`. The reasoning behind using any on both parts is what if the attacker changes IP addresses, you are now ahead of the game. Now the second half of the rule, for the msg: section I put `"Reverse Shell Detected"`. To finish off the rule since we only have one, the sid: should be `100001`, and the rev: will stay at `1`. It should look as such so far `drop tcp any 4444 <> any any (msg:"Reverse Shell Detected"; sid:100001; rev:1;)`.

![](https://miro.medium.com/v2/resize:fit:664/1*VNgEv0UgiedGGb5KhBRmAQ.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/v2/resize:fit:653/1*4aC8clHSNw0DZQtduzZfkw.png)

## Stop the attack and get the flag (which will appear on your Desktop)

Almost time to run our rule against the live traffic, but first we need to know how we are to run the Snort. If we look back at Task 7 of the Snort room, we can see how we need to run the rule.

![](https://miro.medium.com/v2/resize:fit:700/1*U94yRJcOMd3j4YhL1zeVxg.png)

After seeing the command we have to use to run the rule, the only change that needs to be made is instead of console on the end we put full. so the command it `sudo snort -c /ect/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full`, the press enter and let it run till you see the flag.txt file pop-up on the desktop.

![](https://miro.medium.com/v2/resize:fit:700/1*7ZV1DcfcPqgseeLEAtVUTg.png)

Once the flag.txt file appears, you can stop snort with ctrl +c. Then double-click on the flag.txt icon to open it.

![](https://miro.medium.com/v2/resize:fit:210/1*gJLFtY7t8K_maw_D4OIq9A.png)

After opening it you will be greeted with the flag.