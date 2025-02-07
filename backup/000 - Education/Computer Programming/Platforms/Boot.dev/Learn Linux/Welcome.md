---
up: "[[Learn Linux]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/linux/welcome"
prev: "[[Filesystems]]"
---


This course will be a bit different that what you've done so far on Boot.dev. Instead of writing code in the browser, we're going to be interacting with the command line interface (CLI) on your local machine.

You'll pass off most of the lessons in this course by copying and pasting text from your terminal into an input form here on the site, or by answering multiple-choice questions about the things that are happening on your machine as you run various commands. 

In previous Boot.dev courses you're likely used to running your code by clicking a "run" button. As a developer, you'll most likely run your code using a command line interface (CLI) instead. For example, in Python, you will probably run code on your own machine by typing this into a terminal:

```bash
python main.py
```

This course will get you feeling comfortable working on a command line, which is a skill that's going to be critical for the rest of your career as a programmer, especially as a backend developer.
# Command Line vs. GUI
## What's a CLI?

We often hear terms like "terminal", "shell", "command line", "CLI" and "command prompt" used interchangeably, but often they all refer to the same thing: a program that allows you to interact with your computer in a text-based way. 
## What's a GUI?

If you don't have a technical background, you're probably used to interacting with your phone or computer using a [graphical user interface](https://en.wikipedia.org/wiki/Graphical_user_interface) (GUI). When you use a mouse to click on fancy icons, buttons, and menus, you're using a GUI.

To be fair, it's usually easier to teach someone how to use a GUI than a CLI. You can simply point to things and say "click here" or "drag this there". But GUIs do have some drawbacks:

- **They're weak.** You are given much more control over your computer through a CLI. With a GUI you're limited to the options that the developer of the GUI has given you.
- **They're slow**: Once you know the commands to type, it's much faster to type them than to click through endless menus with a mouse.
- **They're not as reproducible**. If you want to share a set of instructions, you can just copy and paste commands without worrying about screen sizes and user preferences. 
- **They're not automatable**. It's easy to write code that manipulates text (as you've seen in Python), but it's much harder to write code that manipulates GUIs.
- **They're not as cool**. You will be invited to 90% fewer romantic outings if you are a GUI user.
# What is a Terminal?

As we talked about, the terms "shell", "CLI" and "terminal" are often used to refer to the same thing: the program that lets you issue text-based commands. 

However, to get pedantic, the "terminal" is just one *specific* part of that program. Historically, the word "terminal" meant a physical device that you could type commands into, essentially a keyboard and a screen.

These days, when we say "terminal", we really mean "terminal emulator". A terminal emulator is a program the emulates a physical terminal. It's a program that lets you type commands into a window on your computer. *Which* commands you're able to use isn't determined by the terminal emulator that you happen to be using. It's determined by the shell, which we will talk about later. 

_Your terminal emulator is just responsible for drawing text on the screen and processing your keystrokes._
# What is a Shell?

So if your terminal is just a program that lets you issue text-based commands and renders the output of those commands...

...What is the program that _runs_ those commands???

That's a shell.

Shells do a lot of things, but their main job is to interpret the commands you type and execute them.
## REPL

Shells are often referred to as "REPL"s. REPL stands for

- Read
- Eval (evaluate)
- Print
- Loop

This is a fancy way of saying that shells are programs that:

1. Read the commands you type
2. Evaluate those commands, usually by running other programs on your computer
3. Print the output of those commands
4. Give you a new prompt to type another command and repeat
# Variables

- If you're using Ubuntu on WSL, you're probably running a [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) shell.
- If you're using macOS, you're probably running a [Zsh](https://en.wikipedia.org/wiki/Z_shell) shell.
- If you're running full Linux, I pray you already know what you're using.

The point is that you're probably using Bash or Zsh, and for this course they're basically the same. Both Bash and Zsh are shells, and they also happen to be powerful programming languages. They have variables, functions, loops, and more. Thay said, only crazy people write large programs in shell languages... shells are optimized for running other programs and writing small scripts, not for writing programs. 

```bash
name="Jason"
```

```bash
echo $name
"Jason"
```

Unlike in Python where you can just use a variable's name, in your shell you need to prefix the variable name with a `$` when you want to use it. 
# Navigate History

## Arrows

You'll often want to re-run a command that you've run before. You could just type it out again, but assuming you don't have the [WPM](https://en.wikipedia.org/wiki/Words_per_minute) of ThePrimeagen, that's going to be a pain.

Instead, you can use the up and down arrows to cycle through your command history.

Focus your terminal window and use the "up" arrow key to start cycling through your command history. If you recently restarted your terminal type a few commands first, like:

```bash
echo hello
echo world
```

Once you've cycled back through your history with the "up" arrow, you can use the "down" arrow to cycle back to the most recent command.
# Terminal Alternatives

So far you've been likely working in the default terminal that came with your operating system, and that's fine. However, there are a number of other options, I want to highlight a couple of them just in case you want to check them out (but you don't have to).
## Editor/IDE built-in terminals

Most text editors for developers have a built-in terminal.

VS Code is a popular text editor that also has a built-in terminal. I use VS Code for all of my development work, and I use the built-in terminal.

However, in this course, I do _not_ recommend using VS Code. It's overkill for what we're doing.
## iTerm2

[iTerm2](https://iterm2.com/) is a popular terminal for Mac OS. It's a bit more powerful than the default terminal, and it has some nice features like split panes.
## Alacritty

[Alacritty](https://github.com/alacritty/alacritty) is a popular terminal for Linux with a focus on flexibility and extensive configuration. GPU-accelerated, it's great if you're doing a lot of heavy lifting in the terminal.
## Windows Terminal

[Windows Terminal](https://apps.microsoft.com/detail/9N0DX20HK701?rtc=1&hl=en-us&gl=US) is Microsoft's substitute for the Linux terminal. Use the "cmd.exe" program settings to change the default terminal. Be sure to start WSL whenever you open a new terminal window.