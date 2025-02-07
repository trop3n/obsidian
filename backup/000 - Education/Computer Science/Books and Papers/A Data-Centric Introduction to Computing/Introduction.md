#computerscience #programming #datastructures #databases 
# 1.1 What This Book is About

This book is an introduction to computer science. It will teach you how to program, and do so in ways that are of practical value and importance. 

However, it was also go beyond programming to computer science, a rich, deep fascinating and beautiful intellectual discipline. You will learn many useful things that you can apply right away, but we will also show you some of what lies beneath and beyond.

Most of all, we want to give you *ways of thinking about solving problems using computation*. Some of these ways are technical methods, such as working from data and examples to construct solutions to problems. Others are scientific methods, such as ways of making sure that programs are reliable and do what they claim. Finally, some are social, thinking about the impacts that programs have on people.
# 1.2 The Values that Drive This Book

Our perspective is guided by our decades of experience as software developers, researchers and educators. This has instilled in us the following beliefs:

- Software is not written only to be run. It must also be written to be read and maintained by others. Often that "other" person is you, six months later, who has forgotten what they did and why.

- Programmers are responsible for their software meeting its desired goal and being reliable. This is reflected in a variety of disciplines inside computer science, such as testing and verification.

- Programs ought to be amenable to prediction. We need to know, as much as possible, before a program runs, how it will behave. This behavior includes not only technical characteristics such as running twice, space, power, and so on, but also social impacts, benefits, and harms. Programmers have been *notoriously poor at thinking* about the latter.
# 1.3 Our Perspective on Data

At a computational level, data have had a profound effect. Traditionally, the only way to make a program better was to improve the program directly, which often meant making it more complicated and impacting the values we discuss above. 

There are classes of programs for which there is another method: simply give the *same* program more or better data, and the program can improve. These data-driven programs lie at the heart of many innovations we see around us.

In addition to this technical effect, data can have a profound pedagogic impact, too. Most introductory programming is plagued by artificial data that have no real meaning, interest, or consequence (and often artificial problems to accompany them). With real data, learned can personalize their education, focusing on problems they find meaningful, enriching, or just plain fun -- asking and answering questions they find worthwhile. Indeed, from this perspective, programs interrogate data: that is, *programs are tools for answering questions*. In turn, the emphasis on real data and real questions enables us to discuss the social impacts of computing.

The structure of data serve as apoint of departure for thinking about and achieving some of the values above - performance, reliability, and predictability - using the many tools of computer science. 
# 1.4 What Makes this Book Unique

First, we propose a new perspective on structuring computing curricula, which we call `data centricity`. We view a data centric curriculum as 

	data centric = data science + data structures

in that order. We being with ideas from data science, before shifting to classical ideas from data structures and the rest of computer science. This book lays out this vision concretely and in detail.

Second, computing education talks a great deail about *notional machines* -- abstractions of program behavior meant to help students understand how programs work - but few curricula actually use one. We take notional machines seriously, developing a sequence of them and weaving them through the curriculum. This ties our belief that programs are not only objects to run, but also objects that we reason about.

Third, we weave content on socially-responsible computing into the text. Unlike other efforts that focus on exposing students to ethics or the pitfalls of technology in general, we aim to show students how the constructs and concepts that they are turning into code *right now* can lead to adverse impacts unless used **with care**. In keeping with our focus on testing and concrete examples, we introduce several topics by getting students to think about assumptions at the level of concrete data. This material is called out explicitly throughout the book.

Finally, this book is deeply informed by recent and ongoing research results. Our choices of material, order of presentation, programming methods, and more are driven by what we know from the research literature. In many cases, we ourselves are the ones doing the research, so the curriculum and research live in a **symbiotic relationship**. 

You can find our papers (some with each other, others not) [on](https://cs.brown.edu/~kfisler/Pubs/index.html) [our](https://cs.brown.edu/~sk/Publications/Papers/Published/) [respective](https://www.ccs.neu.edu/home/blerner/papers.html) [pages](https://jpolitz.github.io).
# 1.5 Who this Book is For

This book is written for students primarily who are in the early stages of computing education at the tertiary level.
# 1.6 The Structure of this Book

Unlike some other textbooks, this one does not follow a top-down narrative. Rather is has the flow of a conversation, with backtracking. We will often build up programs incrementally, just as a pair of programmers would. We will include mistakes, not because we don't know better, but because *this is the best way for you to learn*. Including mistakes makes it impossible for you to read passively, you must engage with the material, because you can never be sure of the veracity of what you're reading. 
# 1.7 Organization of the Material

Because this book covers what would be considered multiple semesters worth of material at the tertiary level in the USA, we have divided it into seven main booklets. Later booklets depend on some earlier ones, but the earlier ones can be treated as a stand-alone book that arrives at a satisfying ending for a student or course that does not proceed further.

1. [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html): An introduction to programming for beginners that teaches programming and rudimentary data analysis. It introduces core programming concepts through composing images and processing tables, before covering lists and trees. The notional machine throughout this section is based on substitution.
    
    Dependencies: None!
    
2. [From Pyret to Python](https://dcic-world.org/2024-09-03/booklet_pyret-to-python.html): Students learn to transfer their knowledge from Pyret to Python, highlighting similarities and differences between the languages and their traditional programming styles (“paradigms”). Students are also introduced to Pandas, as a real-world table-processing system.
    
    Dependencies: [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html).

3. [Programming With State](https://dcic-world.org/2024-09-03/booklet_programming-with-state.html): Students learn the subtleties of state and aliasing. Much of the coverage is in both Python and Pyret. This contrast lets students understand how multiple languages can approach the same topic; the ways in which the underlying ideas are actually the same; but also some key differences that provide insight. The notional machine grows to cover state and aliasing by separating the naming environment (here called the directory) from a heap of structured data values.
    
    Dependencies: [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html) is essential. [From Pyret to Python](https://dcic-world.org/2024-09-03/booklet_pyret-to-python.html) is helpful to follow the Python portions of this booklet, but a student can do the Pyret parts without having seen Python.

4. [Algorithm Analysis](https://dcic-world.org/2024-09-03/booklet_algo-analysis.html): Students are introduced to multiple techniques for analyzing algorithms.
    
    Dependencies: [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html). There is no dependency on state.
    
5. [Data Structures with Analysis](https://dcic-world.org/2024-09-03/booklet_data-with-analysis.html): Students are introduced to more advanced data structures through a lens of algorithm analysis, which motivates their revision and variation.
    
    Dependencies: [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html) and [Algorithm Analysis](https://dcic-world.org/2024-09-03/booklet_algo-analysis.html) are essential everywhere. [Programming With State](https://dcic-world.org/2024-09-03/booklet_programming-with-state.html) is necessary for some material.
    
6. [Advanced Topics](https://dcic-world.org/2024-09-03/booklet_advanced.html): Students cover a grab-bag of interesting computer science topics in program design and algorithmic programming. Relative to the other material, this content is either more subtle, more advanced, or less essential in a mainstream course.
    
    Dependencies: All the material depends on [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html). Some material depends on [Algorithm Analysis](https://dcic-world.org/2024-09-03/booklet_algo-analysis.html) and/or [Programming With State](https://dcic-world.org/2024-09-03/booklet_programming-with-state.html).
    
7. [Interactive Programs](https://dcic-world.org/2024-09-03/booklet_interaction.html): Students can write interactive programs with relatively few dependencies!
    
    Dependencies: [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html).
    

This decomposition into booklets allows flexibility in offering several different kinds of courses at very different levels of sophistication. For instance, we already offer two very different courses by remixing this material, which others could follow:

- An introductory course can use [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html), [From Pyret to Python](https://dcic-world.org/2024-09-03/booklet_pyret-to-python.html), and [Programming With State](https://dcic-world.org/2024-09-03/booklet_programming-with-state.html) to cover the data-centric view of computer science and leaving students with basic skills in Python. This corresponds to [CSCI 0111](https://cs.brown.edu/courses/csci0111/) at Brown University.
    
- A more advanced course can start with [Introduction to Programming](https://dcic-world.org/2024-09-03/booklet_intro-to-programming.html), then do [Algorithm Analysis](https://dcic-world.org/2024-09-03/booklet_algo-analysis.html) (perhaps in increments), followed by [Data Structures with Analysis](https://dcic-world.org/2024-09-03/booklet_data-with-analysis.html), before returning to [Programming With State](https://dcic-world.org/2024-09-03/booklet_programming-with-state.html), while interspersing content from [Advanced Topics](https://dcic-world.org/2024-09-03/booklet_advanced.html). This corresponds to [CSCI 0190](https://cs.brown.edu/courses/csci0190/) at Brown University.
    

The course pages archive all prior instances of the courses, which include all the assignments and related materials. Readers are welcome to use these in their own courses.

Many of these courses will have entering students who have programmed with state before (in Python, Java, Scratch, or other languages). In our experience, most of these students have been given either vastly incomplete, or outright misleading, explanations of and metaphors for state (e.g., “a variable is a box”). Thus, they have a poor understanding of it beyond the absolute basics, especially when they get to important topics like aliasing. As a result, many of these students have found it both novel and insightful to properly understand how state really works through our notional machine. For that reason, we recommend going through that material slowly and carefully.

We of course invite readers to create their own mashups of the chapters within the sections. We would love to hear about others’ designs.
# Our Programming Language of Choice

If we wanted to get rich, we’d have written this book entirely in Python. As of this writing, Python is enjoying its instructional-use heyday (just like Java before it, C++ before that, C before that, Pascal earlier, and so on). And there are, indeed, many attractive aspects of Python, not least its presence next to bullet points on job listings. However, we’ve been [repeatedly frustrated by Python](https://dcic-world.org/2024-09-03/pyret-vs-python.html) as an entrypoint into learning programming.

As a result, this book features two programming languages. It starts with a language, called [Pyret](https://www.pyret.org/), that we designed to address our needs and frustrations. It has been expressly designed for the style of programming in this book, so the two can grow in harmony. It draws on Python, but also on many other excellent programming languages. Beginning programmers can therefore rest in the knowledge they are being cared for, while programmers with past acquaintance of the language menagerie, from serpents to dromedaries, should find Pyret familiar and comfortable.

Then, recognizing the value of Python both as a standard language of communication and for its extensive libraries, the [Programming with State (in Both Pyret and Python)](https://dcic-world.org/2024-09-03/part_state.html) part of this book explicitly covers Python. Rather than starting from scratch in Python, we present a systematic and gradual transition to it from the earlier material. We believe this will make you learn general programming better than if you had seen only one programming language. However, we believe this will help you understand Python better, too: just like you learn to appreciate your own language, country, or culture better once you’ve stepped outside and been exposed to other ones.

Programming Tools: The programming environment for Pyret is called [CPO](https://code.pyret.org/) (an abbreviation of code.pyret.org). It runs entirely in the browser and uses Google Drive for authentication and file storage. We do not recommend any particular Python environment. Any Python editor that allows you to use pytest and load external data files should work fine.


