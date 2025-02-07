---
up: "[[000 - Education/Computer Programming/General/General|General]]"
tags:
  - "#education/computerprogramming/general/thinklikeaprogrammer"
---

# Introduction

Do you struggle to write programs, even though you think you understand programming languages? Are you able to read through a chapter in a programming book, nodding along the whole way, but unable to apply what you've read to your own programs? Are you able to comprehend a program example you've read online, even to a point where you could explain it to someone else what each line of code is doing, yet you feel your brain seize up when faced with a programming task and a blank screen in your text editor?

You're not alone. I have taught programming for over 15 years, and most of my students would have fit this description at some point in their instruction. We will call the missing skill *problem solving*, the ability to take a given problem description and write and original program to solve it. Not all programming requires extensive problem solving. If you're just making minor modifications to an existing program, debugging or adding testing code, programming may be so mechanical in nature that your creativity is never tested. But all programs require problem solving at some point, and **all good programmers can solve problems**. 

Problem solving is **hard**. It's true that a few people make it look easy -- the "naturals", the programming world's equivalent of a gifted athlete, like Michael Jordan. For these select few, high-level ideas are effortlessly translated into source code. To make a Java metaphor, it's as if their brains execute Java natively, while the rest of us have to run a virtual machine, interpreting as we go. 

Not being a natural isn't fatal to being a good programmer -- if it were, the world would have few programmers. Yet I've seen too many worthy learners struggle too long in frustration. In the worst cases, they give up programming entirely, convinced that they can never be programmers, that the only good programmers are born with the innate gift. 

In part, it's because problem solving is a *different activity* from learning programming syntax and therefore uses a different set of mental "muscles". Learning programming syntax, reading programs, memorizing elements of an application programming interface -- these are mostly analytical "left brain" activities. Writing an original program using previously learned tools and skills is a creative "right brain" activity. 

Suppose you need to remove a branch that has fallen into one of the rain gutters on your house, but your ladder isn't quite long enough to allow you to reach the branch. You head into the garage and look for something, or a combination of things, that will enable you to remove the branch from the gutter. Is there some way to extend the ladder? Is there something you can hold at the top of the ladder to grab or dislodge the branch? Maybe you could just get on the roof from another place and get the branch from above. That's problem solving, and it's a **creative activity**. Believe it or not, when you design an original program, your mental process is quite similar to that of the person figuring out how to remove the branch from the gutter and quite different from that of a person debugging an existing `for` loop. 

Most programming books, though, focus their attention on syntax and semantics. Learning the syntax and semantics of a programming language is essential, but it's only the first step in learning *how to program* in that language. In essence, most programming books for beginners teach how to read a program, not how to write one. Books that do focus on writing are often effectively "cookbooks" in that they teach specific recipes for use in particular situations. Such books can be quite valuable timesavers, but not as a path toward learning to write original code. Think about cookbooks in the original sense. Although great cooks own cookbooks, no one who relies upon cookbooks can be great cook. A great cook understands ingredients, preparation methods, and cooking methods and knows how they can be combined to make great meals. All a great cook needs to produce a tasty meal is a fully stocked kitchen. 

In the same way, a great programmer understands language syntax, application frameworks, algorithms, and software engineering principles and knows how they can be combined to make great programs. Give a great programmer a list of specifications, turn him loose with a fully stocked programming environment, and great things will happen.

In general, current programming education doesn’t offer much guidance in the area of problem solving. Instead, it’s assumed that if programmers are given access to all of the tools of programming and requested to write enough programs, eventually they will learn to write such programs and write them well. There is truth in this, but “eventually” can be a long time. The journey from initiation to enlightenment can be filled with frustration, and too many who start the journey never reach the destination.In general, current programming education doesn’t offer much guidance in the area of problem solving. Instead, it’s assumed that if programmers are given access to all of the tools of programming and requested to write enough programs, eventually they will learn to write such programs and write them well. There is truth in this, but “eventually” can be a long time. The journey from initiation to enlightenment can be filled with frustration, and too many who start the journey never reach the destination.

Instead of learning by trial and error, you can learn problem solving in a systematic way. That's what this book is all about. You can learn techniques to organize your thoughts, procedures to discover solutions, and strategies to apply to certain classes of problems. By studying these approaches, you can unlock your creativity. Make no mistake: Programming, and especially problem solving, is a **creative activity**. Creativity is mysterious, and no one can say exactly how the creative mind functions. Yet, if we can learn music composition, take advice on creative writing, or be shown how to paint, then we can learn to creatively solve programming problems, too. 

My goal is for you and every other reader of this book to learn to system- atically approach every programming task and to have the confidence that you will ultimately solve a given problem. When you complete this book, *I want you to think like a programmer and to believe that you are a programmer.*
# Chapter 1: Strategies for Problem Solving

What is problem solving, exactly? 

Trading in an old car that isn't working correctly isn't a *solution*, it is *avoidance*. A mechanical problem is a problem that can be solved with automotive knowledge, diagnosis, replacement equipment, and common shop tools. 

Problems include constraints, unbreakable rules about the problem or the way in which the problem must be solved. 

In the car analogy, the constraint is that we want to fix the current car, not buy a new one. Other constraints would include the cost of the repairs, how long the repair will take, or that no new tools can be purchased just for this single repair.

Computer programs also come with restraints:

- Programming language
- Platform
- Performance
- Memory footprint

Sometimes a constraint is the other code that can be referenced. Maybe the program can't include certain open-source code, or maybe the opposite, maybe it can use only open source.

For programmers, we can define ***problem solving*** as **writing an original program that performs a particular set of tasks and meets all stated constraints.**

New programmers often become too eager to accomplish the first part that they fail on the second -- creating a program that performs the certain task, but doesn't meet any of the constraints. This can be referred to as a ***Kobayashi Maru***.

Kobayashi Maru is from Star Trek II: The Wrath of Khan. The film contains a subplot about an exercise for aspiring Starfleet Academy officers. The cadets are put aboard a simulated starship bridge and made to act as captain on a mission that involves an impossible choice. Innocent people will die on a wounded ship, the *Kobayashi Maru*, but to reach them requires starting a battle with the Klingons, a battle that can only end in the destruction of the captain's ship. 

The exercise is intended to test a cadet's courage under fire. There's no way to win, and all choices lead to bad outcomes. Toward the end of the film, we discover that Captain Kirk modified the simulation to make actually winnable. Kirk was clever, but he did not solve the dilemma of the *Kobayashi Maru*, he avoided it. 

Fortunately, the problems you will face as a programmer are solvable, but many programmers still resort to Kirk’s approach. In some cases, they do so accidentally. (“Oh, shoot! My solution only works if there are a hundred data items or fewer. It’s supposed to work for an unlimited data set. I’ll have to rethink this.”) In other cases, the removal of constraints is deliberate, a ploy to meet a deadline imposed by a boss or an instructor. In still other cases, the programmer just doesn’t know how to meet all of the constraints. In the worst cases I have seen, the programming student has paid someone else to write the program. Regardless of the motivations, we must always be diligent to avoid the Kobayashi Maru.
## Classic Puzzles

Expert problem solvers are quick to recognize an *analogy*, an exploitable similarity between a solved problem and an unsolved problem. If we recognize that a feature of problem A is analogous to a feature of problem B and we have already solved problem B, we have a **valuable insight** into solving problem A. 

In this section, we will discuss classic problems from outside the world of programming that have lessons we can apply to programming problems. 
### The Fox, The Goose and The Corn

This first classic problem we will discuss is a riddle about a farmer who needs to cross a rive. You have probably encountered it previously in one form or another. 
#### Problem: How to Cross the River?

A farmer with a fox, a goose, and a sack of corn needs to cross a river. The farmer has a rowboat, but there is only room for the farmer and one of his three items. Unfortunately, both the fox and the goose are hungry. The fox cannot be left alone with the goose, or the fox will eat the goose. Likewise, the goose cannot be left alone with the sack of corn, or the goose will eat the corn. How does the farmer get everything across the river?

> [!Important] Solution
> Few people are able to solve this riddle, at least without a hint. I know I wasn’t. Here’s how the reasoning usually goes. Since the farmer can take only one thing at a time, he’ll need multiple trips to take everything to the far shore. On the first trip, if the farmer takes the fox, the goose would be left with the sack of corn, and the goose would eat the corn. Likewise, if the farmer took the sack of corn on the first trip, the fox would be left with the goose, and the fox would eat the goose. Therefore, the farmer must take the goose on the first trip.
> 
> So far, so good. But on the second trip, the farmer must take the fox or the corn. Whatever the farmer takes, however, must be left on the far shore with the goose while the farmer returns to the near shore for the remaining item. This means that either the fox and goose will be left together or the goose and corn will be left together. Because neither of these situations is acceptable, the problem appears unsolvable. Again, if you have seen this problem before, you probably remember the key element of the solution. The farmer has to take the goose on the first trip, as explained before. On the second trip, let’s suppose the farmer takes the fox. Instead of leaving the fox with the goose, though, the farmer takes the goose back to the near shore. Then the farmer takes the sack of corn across, leaving the fox and the corn on the far shore, while returning for a fourth trip with the goose. The complete solution is shown in Figure 1-3. This puzzle is difficult because most people never consider taking one of the items back from the far shore to the near shore. Some people will even suggest that the problem is unfair, saying something like, “You didn’t say I could take something back!” This is true, but it’s also true that nothing in the problem description suggests that taking something back is prohibited.
> 
> 

This puzzle would have been much easier to solve if the possibility of taking one of the items back was made explicitly clear: *The farmer has a rowboat that **can be used to transfer items in both directions**, but there is room only for the farmer and one of this three items.*

With that suggestion in plain sight, more people would figure out the problem. This illustrates an important principle of problem solving: **If you are unaware of all possible actions you could take, you may be unable to solve the problem.** We can refer to these actions as *operations*. By enumerating all the possible operations, we can solve many problems by testing every combination of operations until we find one that works. More generally, by restarting the problem in more formal terms, we can often uncover solutions that would have otherwise eluded us.

A useful method is to break the problem down more formally:

List the constraints:
1. The farmer can take only one item at a time in the boat.
2. The fox and goose cannot be left alone on the same shore.
3. The goose and corn cannot be left alone on the same shore.

This problem is a good example of the importance of constraints. If we remove any of these constraints, the puzzle is easy. 

Next, list the operations:
1. Operation: Carry the fox to the far side of the river.
2. Operation: Carry the goose to the far side of the river.
3. Operation: Carry the corn to the far side of the river.

Remember, though, that the goal of formally restating the problem is to gain insight for a solution. 

Lets list the operations more generically, or paramaterized:
1. Operation: Row the boat from one shore to the other.
2. Operation: If the boat is empty, load an item from the shore. 
3. Operation: If the boat is not empty, unload the item to the shore.

If we generate all possible sequences of moves, ending each sequence once it violates one of our constraints or reaches a configuration we've seen before, we will eventually hit upon the sequence of the final solution. 
#### Lessons Learned

Restating the problem in a more formal manner is a great technique for gaining insight into a problem. Many programmers seek out other programmers to discuss a problem, not just because other programmers may have the answer but also because articulating the problem out loud often triggers new and useful thoughts. Restating a problem is like having a discussion with another programmer, except that you are playing both parts. 

The broader lesson is that thinking about the problem may be as productive, or in some cases more productive, than thinking about the solution. In many cases, the correct approach to the solution *is* the solution.
### Sliding Tile Puzzles






