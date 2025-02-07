#computerscience #computerarchitecture #nostarchpress #books 
# Introduction

Are you curious about how computers work? Gaining a broad understanding of computing is often a long and winding path. The problem isn’t a lack of documentation. A quick search online shows that there are many, many books and websites devoted to explaining computing. Programming, computer science, electronics, operat- ing systems . . . a wealth of information is out there. This is a good thing, but it can be daunting. Where should you begin? How does one topic connect to another? This book was written to give you an entry point for learning about key concepts of computing and how these concepts fit together.

Many programmers know how to make a computer do their bidding, but they don't understand what is really happening under the hood. The goal of this book is to present the fundamentals of computing in an accessible, hands on way that makes abstract concepts more real. It presents the foundational concepts of computer and connects the dots between them. The book should enable you to construct a mental picture of how computers work, which allows you to dive deeper on the topics that interest you. 
## About this Book

This book looks at computing as a **technology stack**. A modern computing device, such as a smartphone, is composed of *layers of technology*. At the bottom of the stack we have hardware, and at the top of the stack we have apps, with multiple technology layers in between. The beauty of the layered model is that each layer benefits from all the capabilities of the lower levels, but any given layer only needs to build upon the layer directly below it. 

As you read through this book, you’ll come across circuit diagrams and source code used to illustrate concepts. These are intended as teach- ing tools, favoring clarity over performance, security, and other factors that engineers consider when designing hardware or software. In other words, the circuits and code in this book can help you learn how computers work, but they aren’t necessarily examples of the best way to do things. Similarly, the book’s technical explanations favor simplicity over completeness. I sometimes gloss over certain details to avoid getting mired in complexity.
## About Exercises and Projects

Throughout the chapters you’ll find exercises and hands-on projects. The exercises are problems for you to work out mentally or with pencil and paper. The projects go beyond mental exercises and often involve building a circuit or programming a computer. You’ll need to acquire some hardware to perform the projects (you can find a list of needed components in Appendix B). I’ve included these projects because I believe that the best way to learn is to try things yourself, and I encourage you to complete the projects if you want to get the most out of xxii Introduction this book. That said, I’ve presented the chapter material in a way that allows you to still follow along, even if you don’t build a single circuit or enter one line of code. You can find the answers to exercises in Appendix A, and the details for each project are found at the end of the corresponding chapter. Appendix B contains information to help you get started with projects, and the project text points you there when needed. A copy of the source code used in the projects is available at https:// www.howcomputersreallywork.com/code/. You can also visit this book’s page at https://nostarch.com/how-computers-really-work/ where we will provide updates.
## My Computing Journey

My fascination with computers probably began with the video games I played as a kid. When I visited my grandparents, I’d spend hours playing Frogger, Pac-Man, and Donkey Kong on my aunt’s Atari 2600. Later, when I was in fifth grade, my parents gave me a Nintendo Entertainment System for Christmas, and I was thrilled! While I loved playing Super Mario Bros. and Double Dragon, somewhere along the way, I began to wonder how video games and computers worked. Unfortunately, my Nintendo game console didn’t provide me with many clues as to what was going on inside it. Around the same time, my family bought our first “real” computer, an Apple IIGS, opening new doors for me to explore exactly how these machines functioned. Fortunately, my middle school offered a class on BASIC programming of Apple II computers, and I soon learned that I couldn’t get enough of coding! I would write code at school, bring home a copy of my work on floppy disk, and continue working at home. Throughout middle school and high school, I learned more about programming, and I greatly enjoyed it. I also began to realize that although BASIC and other similar programming languages make it relatively easy to tell a computer what to do, they also hide many details of how computers work. I wanted to go deeper. In college I studied electrical engineering, and I began to understand electronics and digital circuits. I took classes on C programming and assembly language, and I finally got glimpses of how computers execute instruc- tions. The low-level details of how computers work were beginning to make sense. While in college, I also started learning about this new thing called the World Wide Web; I even crafted my very own web page (this seemed like a big deal at the time)! I began programming Windows applications, and I was introduced to Unix and Linux. These topics sometimes seemed far removed from the hardware- specific details of digital circuits and assembly language, and I was curious to understand how it all fit together. After college I was fortunate to get a job at Microsoft. In my 17 years there, I worked in various software engineering roles, from debugging the Windows kernel to developing web applications. These experiences helped me gain a broader and deeper understanding of computers. I worked with many incredibly smart and knowledgeable people, and I learned that there’s always more to learn about computing. Understanding how computers work has been a lifelong journey for me, and I hope to pass on some of what I’ve learned to you through this book.
# Ch. 1: Computing Concepts

In this chapter we'll begin by discussing the definition of a computer. From there, we'll cover the differences between analog and digital data and then explore number systems and the terminology used to describe digital data. 
## Defining a Computer

What is a computer?

A *computer* is any electronic device that can be programmed to carry out a set of logical instructions. 

By that definition, it becomes clear that many modern devices are in fact computers.
## Analog and Digital

You've probably heard of a computer being described as a digital device. This is in contrast to an analog device, such as a mechanical clock. Understanding the difference between analog and digital is foundational to understanding computing. 
### The Analog Approach

Locating a device and describing it, the color, the weight, the size, this is all the ***data*** for that particular device. For a given property of an object, the variations found across all of the objects available in the world is potentially *infinite*.

Think about a scale. To measure the weight of an object, you place it onto a scale. The weight of the object moves a needle that corresponds to a number on a dial. The position of the needle determines the weight of the object. 

This kind of measurement is common, but let's think a little more deeply about it. The position of the needle on the scale isn't actually the weight; it's a *representation* of the weight. Although the weight is an attribute of an object, here we can understand that attribute through something else: the position of the needle along the line. The needle's position changes proportionally in response to the weight being placed on the scale. Thus, the scale is working as an *analogy* where we understand the weight of the object through the needle's position on the line. This is why we call this method of measuring the ***analog*** approach.

Another example of an analog measuring tool is a mercury thermom- eter. Mercury’s volume increases with temperature. Thermometer manufac- turers utilize this property by placing mercury in a glass tube with markings that correspond to the expected volume of the mercury at various tem- peratures. Thus, the position of mercury in the tube serves as a representa- tion of temperature. Notice that for both of these examples (a scale and a thermometer), when we make a measurement, we can use markings on the instrument to convert a position to a specific numeric value. But the value we read from the instrument is just an approximation. The true position of the needle or mercury can be anywhere within the range of the instrument, and we round up or down to the nearest marked value. So although it may seem that these tools can produce only a finite set of measurements, that’s a limitation imposed by the conversion to a number, not by the analogy itself.

Throughout most of human history, humans have measured things with an analog approach. There's also clever ways to store data in an analog fashion. 

A phonograph record used a modulated groove as an analog representation of audio that was recorded. The groove's shape changes along its path in a way that corresponds to changes in the shape of the audio waveform over time. The groove isn't the audio itself, but it's an analogy of the original sounds' waveform. 

Film-based cameras do something similar by briefly exposing film to light from a camera lens, leading to a chemical change in the film. The chemical properties of film are not the image itself, but a representation of the captured image, an *analogy of the image*.
### Going Digital

It turns out that all those analog representations of data are hard for computers to deal with. The types of analog systems used are so different and variable that creating a common computing device that can understand all of them is nearly impossible.

Computers require highly reliable and accurate representations of certain types of data, such as numeric data sets and software programs. Analog representations of data can be difficult to measure precisely, tend to decay over time, and lost fidelity when copied. Computers need a way to represent all types of data in a format that can be accurately process, stored and copied. 

Alas, the **digital system**. A **digital system** represents data as a sequence of symbols, where each symbol is one of a limited set of values. 

In almost all of today's comptuers, data is represented with combinations of two symbols: 0 and 1. That's it. Although a digital system could use more than two symbols, adding more symbols allows would increase the complexity and cost of the system. A set of only two symbols *allows for simplified hardware and improved reliability*. All data in most modern computing devices is represented as a sequence of 0s and 1s. 

It's a point worth repeating: **everything on your computer is stored as 0s and 1s**. 

Many find it counter intuitive that such a limited "vocabulary" can be used to express complex ideas. The key here is that digital systems use a **sequence** of 0s and 1s. A digital photograph, for example, usually consists of millions of 0s and 1s. 

You may see other terms used to describe these 0s and 1s: false and true, off and on, low and high, and so forth. This is because the computer doesn't literally store the number `0` or `1`. It stores a sequence of entries where each entry in the sequence can have only two possible states. Each entry is like a light switch that is either on or off. 

In practice, these sequences of 1s and 0s are stored in various ways. On a CD or DVD, the 0s and 1s are stored on the disc as bumps (0) and flat spaces (1). On a flash drive, the 1s and 0s are stored as *electrical charges*. A hard disk drive stores the 0s and 1s using magnetization. 

Before we move on, one final note on the term *analog*—it’s often used to simply mean “not digital.” For example, engineers may speak of an “ana- log signal,” meaning a signal that varies continuously and doesn’t align to digital values. In other words, it’s a non- digital signal but doesn’t necessarily represent an analogy of something else. So, when you see the term *analog*, consider that it might not always mean what you think.
## Number Systems

So far, we’ve established that computers are digital machines that deal with 0s and 1s. For many people, this concept seems strange; they’re used to having 0 through 9 at their disposal when representing numbers. If we constrain ourselves to only two symbols, rather than ten, how should we represent large numbers? To answer that question, let’s back up and review an elementary school math topic: number systems.
### Decimal Numbers

We typically write down numbers using something called *decimal place-value notation*. Let's break that down.

- *Place-value notation* means that each position in a written number represents a different order of magnitude: *decimal* or *base 10*, means that the orders of magnitude are factors of 10, and each place can have one of ten different symbols, 0 through 9. Look at the example of place-value notation below:

| 2              | 7          | 5          |
| -------------- | ---------- | ---------- |
| Hundreds place | Tens place | Ones place |
In Figure 1-1, the number two hundred seventy-five is written in decimal notation as 275. The 5 is in the ones place, meaning its value is $5 × 1 = 5$. The 7 is in the tens place, meaning its value is $7 × 10 = 70$. The 2 is in the hundreds place, meaning its value is $2 × 100 = 200$. The total value is the sum of all the places: $5 + 70 + 200 = 275$

Why is the rightmost number the ones place? And why is the next place the tens place, and so on? It's because we are working in decimal, or base 10, and therefore each place is a power of ten -- in other words, 10 multiplied by itself a certain number of times. 

As seen in Figure 1-2, the rightmost place is 10 raised to 0, which is 1, because any number raised to 0 is 1. The next place is 10 raised to 1, which is 10, and the next place is 10 raised to $2 (10 × 10)$, which is 100.

| 2      | 7      | 5      |
| ------ | ------ | ------ |
| $10^2$ | $10^1$ | $10^0$ |
If we needed to represent a number larger than 999 in decimal, we'd add another place to the left, the *thousands place*, and it's weight would be equal to 10 raised to 3 ($10 x 10 x 10$), which is 1,000. The pattern continues so that we can represent any large whole number by adding more places as needed. 

We’ve established why the various places have certain weights, but let’s keep digging. Why does each place use the symbols 0 through 9? When working in decimal, we can only have ten symbols, because by definition each place can only represent ten different values. 0 through 9 are the symbols that are currently used, but really any set of ten unique symbols could be used, with each symbol corresponding to a certain numeric value. 

Most humans prefer decimal, base 10, as a number system. Some say this is because we have ten fingers and ten toes, but whatever the reason, in the modern world most people read, write, and think of numbers in decimal. Of course, that’s just a convention we’ve collectively chosen to represent numbers. As we covered earlier, that convention doesn’t apply to computers, which instead use only two symbols. Let’s see how we can apply the principles of the place-value system while constraining ourselves to only two symbols.
### Binary Numbers

The number system consisting of only two symbols is *base 2*, or *binary*. Binary is still a place-value system, so the fundamental mechanics are the same as decimal, but there are a couple of changes. 

First, each place represents a power of 2, rather than a power of 10. Second, each place can only have one of two symbols, rather than 10. Those two symbols are 0 and 1. 

| 1           | 0          | 1          |
| ----------- | ---------- | ---------- |
| Fours Place | Twos Place | Ones Place |
| $2^2$       | $2^1$      | $2^0$      |
| $2 x 2 = 4$ | $2$        | $1$        |
In the table above, we have a binary number: 101. That may look like one hundred and one, but when dealing with binary, this is actually a representation of **five**. If you wish to verbally say it, "one zero one binary" would be a good way to communicate what is written.

Just like in decimal, each place has a weight equal to the base raised to the various powers. Since we are in base 2, the rightmost place is 2 raised to 0, which is 1. The next place is two raised to 1, which is 2, and the third place is 2 raised to 2, which is 4. Also, just like in decimal, to get the total value, we multiply the symbol in each place by the place-value weight and sum the results. 

So, starting from the right, we have $(1 x 1) + (0 x 2) + (1 x 4) = 5$. 

Now, we can try converting from binary to decimal yourself. 
#### Exercise 1-2: Binary to Decimal

Convert these numbers, represented in binary, to their decimal equivalents. 


