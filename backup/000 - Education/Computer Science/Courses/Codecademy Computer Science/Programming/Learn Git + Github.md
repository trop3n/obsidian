# Basic Git Workflow

### Generalizations

You have now been introducted to the fundamental Git workflow. 

- Git is the industry-standard version control system for web developers.
- Use Git commands to help keep track of changes made to a project.
	- `git init` creates a new Git repository
	- `git status` inspects the contents of the working directory and staging area
	- `git add` adds files from the working directory to the staging area
	- `git diff` shows the difference between the working directory and the staging area
	- `git commit` permanently stores file changes from the staging area in the repository
	- `git log` shows a list of all previous commands
# Git Cheat Sheet

## GitHub
(https://education.github.com/git-cheat-sheet-education.pdf)

(https://education.github.com/git-cheat-sheet-education.pdf)

In this resource, you will learn important and commonly used Git commands. This is helpful if you would like a resource that you can keep referring to as you get more used to Git commands.
# What is Markdown?

### Introduction

> If you are looking for a simple way to create visually appealing text documents without using an fancy editors, check out [Markdown](https://en.wikipedia.org/wiki/Markdown). Invented by John Gruber and Aaron Swartz in 2004, Markdown provides a lightweight syntax to style any text document so that it can be converted to [HTML](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics) for viewing and publishing.
### Differences between HTML and Markdown

> Markdown translates to HTML, but Markdown is not a replacement for HTML. 

Markdown's syntax can be converted to a small subset of HTML tags to do things like format text, add links, display images, and more. 

You can incorporate HTML elements inside a markdown document. To render Markdown  in HTML, though, you would need a tool called a Markdown parser.
### Benefits of Using Markdown

> Compared to HMTL, writing text in Markdown is much faster because the syntax is simpler. 

The [authors of Markdown](https://daringfireball.net/projects/markdown/) intended Markdown to be a language for writing styled text with syntax that is just as easy to read as it is to write.

Imagine that we are writing down some important text on a sheet of paper. If we wanted to emphasize the text we might underline it, twice even! Similarly, in Markdown, we could write:

```markdown
Title of My Document
====================
```

> Notice that we have plaintext that has a row of equal signs (`=`) to produce a first-level header, also known as <`h1`>. 

The amount of `=`s don’t matter so long as there’s at least one and it goes under the text.

For text that’s important, but not as important as a first-level heading, we might just underline it once. In code, we could use a row of hyphens (`-`), like so:

```md
Sub-Title of My Document
------------------------
```

To produce a second-level header, also known as `<h2>`:
# Sub Title of My Document

Both examples are valid Markdown syntax. It is intuitive and normal for headings to be in either format. Alternatively, you can format headings using the `#` character. We’ll show more examples of different headings, but for now, here’s an example of valid syntax for a `<h1>` heading:

```Markdown
# Title of My Document
```

> Furthermore, a Markdown document without any HTML tags can be published as is because its syntax is already made for easy viewing. For example, the following Markdown document has:

- Styled a heading underlined with equal signs (`=`)
- Emphasized `week` in bold with double asterisks (`**`)
- Bulleted a list by prefacing each item with a number and a period
- And marked several lines as separate quotes with an angle bracket (`>`) per quote.

```
My Todo List
============
At the end of this **week**, I plan to:
1. Learn Markdown
2. Write Markdown
3. Share a Markdown note

My favorite quote is:
> If you didn't get it the first time
> Do not despair
> Try and try again
> ~ Anonymous
```

> The HTML equivalent to the above would be:

```HTML
<h1>My Todo List</h1>
<p>At the end of this <strong>week</strong>, I plan to:</p>
<ol>  
  <li>Learn Markdown</li>  
  <li>Write Markdown</li>  
  <li>Share a Markdown note</li>
</ol><p>My favorite quote is:</p>
<blockquote>  
  <p>    
    If you didn't get it the first time<br>    
    Do not despair<br>    
    Try and try again<br>    
    ~ Anonymous  
  </p>
</blockquote>
```

> When viewed on a Markdown parser such as [Stackedit.io](https://stackedit.io/app#), you will see this:
### When to Use Markdown

> After knowing the many benefits of Markdown input, you might want to consider using Markdown if you ever find yourself in any of these scenarios:

- The only editor available to you only supports plain text.
- Time is of the essence and you can't afford to learn how to use an unfamiliar rich-text editor.
- You need to quickly outline your ideas in a structured but presentable manner.
- You want your document to be portable so that it can be converted to HTML, PDF, EPUB, and/or MOBI.
### Markdown Document Extension

> Contrary to popular belief, Markdown is not a document format. Therefore, it doesn't require a strict file extension naming convention, such as `.md`. 

As the official Markdown mailing list explains, Markdown isn't meant to take over the format or file.

Any file extension that you would normally use to name your text document such as `.txt` or `.text` is appropriate. 

- However, organizations such as GitHub have a preference to expect Markdown documents to appear with an `.md` or `.markdown` extension.
### Markdown Applications

> Since Markdown has gained a lot of popularity, you will find Markdown content being accepted in many applications.

- Website publishers that accept Markdown content include [Wordpress.com](https://wordpress.com/support/can-i-use-markdown-on-wordpress-com), [Ghost](https://www.markdownguide.org/tools/ghost/) and [BeakerBrowser](https://beakerbrowser.com/docs/guides/create-a-markdown-site). Tools such as [Jekyll](https://www.markdownguide.org/tools/jekyll/), [Docusaurus](https://www.markdownguide.org/tools/docusaurus/) and [MkDocs](https://www.markdownguide.org/tools/mkdocs/) can convert Markdown documents into a static website geared for technical documentation. Take a look at this [page](https://daringfireball.net/projects/markdown/basics) rendered in HTML, and its text [source](https://daringfireball.net/projects/markdown/basics.text) styled in Markdown.
- Book publishers such as [LeanHub](http://help.leanpub.com/en/articles/2941344-leanpub-flavoured-markdown-vs-markua-for-writing-in-plain-text) accepts Markdown manuscripts and convert them to books for publication.
- Slide-show presentations such as [Remark](https://remarkjs.com/) and [Cleaver](https://jdan.github.io/cleaver/#2) can convert Markdown slides into HTML for web viewing.
### The Markdown Parser

> A **Markdown Parser** is software written to parse the Markdown syntax in a text document and convert it to HTML syntax. The original Markdown parser was written in Perl, but you can find parser [implementations](https://github.com/markdown/markdown.github.com/wiki/Implementations) today in almost any programming language. 

- Regardless, a basic Markdown parser should support the [core Markdown syntax](https://daringfireball.net/projects/markdown/basics): paragraphs, headers, blockquotes, phrase emphasis, lists, code, images, and links.

There are Markdown parsers that are freely available on the Web: [StackEdit.io](https://stackedit.io/app#), [Dillinger](http://dillinger.io), [Parse](https://parsedown.org/demo) and [Markdown to HTML Converter](https://markdowntohtml.com/). In addition to parsing and rendering, both Parse and Markdown to HTML Converter also convert the Markdown document to raw HTML so that you can copy and paste the HTML to be used elsewhere.
### Markdown Tutorial

> Let's learn a little more about the Markdown syntax. As mentioned above, you can simulate a `<h1>` HTML tag with a `#` Markdown symbol. Since then there are six heading tags for HTML, from `<h1>` through `<h6>`, you can simulate this with `#` through `######` in Markdown. For example this markdown syntax:

```Markdown
# This is a H1 heading
## This is a H2 heading
### This is a H3 heading
#### This is a H4 heading
##### This is a H5 heading
###### This is a H6 heading
```

> Will render this:

# This is a H1 heading

## This is a H2 heading

### This is a H3 heading

#### This is a H4 heading

##### This is a H5 heading

###### This is a H6 heading

> In addition to numbered lists, you can style a bulleted list too. There are three different symbols you can use to mark a line item as a bullet:

- The `*`
- The `+`
- The `-`

For example:

```
* Markdown
+ HTML
- XML
```

Produces this:

- Markdown
- HTML
- XML

> For best practice, ***it is recommended to use the same marker throughout your list*** instead of mixing them like above. 

The core Markdown syntax does not include nested lists (list within another list), but it allows adding paragraphs between list items. To do so, you need to add a blank line after a list item or indent 4 spaces or 1 tab before starting a paragraph.

-  Some parsers are lenient and do not enforce 4 spaces but there should be some spacing.

```
* Markdown   
	 Markdown is a lightweight markup language for styling text.
* HTML   
	 HTML stands for HyperText Markup Language.
```

> For more examples of basic syntax, check out [CommonMark’s reference guide](https://commonmark.org/help/).
### The Markdown Flavors

> Because the core Markdown language supports only a subset of HTML features, many independent developers have extended the Markdown syntax to incorporate more HTML compatabilities and customize it for their own organizations. Here are a few popular flavors of Markdown:

- [CommonMark](https://commonmark.org/) is a body of special-interest developers who work side-by-side on a proposal to standardize the Markdown syntax and offer extensive test suites to validate Markdown implementations against this specification.
	- This standard has been used by other developers to base their code upon.
- GitHub Flavored Markup, or [GFM](https://github.github.com/gfm/) is GitHub’s expanded dialect of Markdown based on CommonMark and is used throughout the GitHub platform by its active community.
- [Trello](https://help.trello.com/article/821-using-markdown-in-trello), a popular collaborative tool that organizes and tracks information through virtual boards and cards, implements a custom version of Markdown as well.
### Conclusion

You’ve learned a lot about Markdown, specifically:

- What Markdown is and how it differs from HTML
- How you can benefit from Markdown
- Where and when to apply Markdown in various scenarios
- How to write Markdown to style your text and make it presentable
- What a Markdown parser is and where to locate one
- Where to find other flavors of Markdown that are used in industry

Amazing job getting this far! Don’t be shy in applying Markdown in your next document. In fact, this article and many others like this on Codecademy were prepared using Markdown! See? We practice what we preach.
# Mastering Markdown

### External article for learning Markdown.

→ **[Mastering Markdown](https://guides.github.com/features/mastering-markdown/)**

**With regard to GitHub, why is it important to learn Markdown?**

> Markdown styles text to make it easier to present lists, images, code and other content in GitHub gists and comments within issues and pull requests.

**What is Markdown not used for?**

> Creating code edits to fix issues raised in pull requests in GitHub.

**Fill in the blanks to assign the Markdown symbols to the correct style desired:**
# Markdown Cheatsheet

## Markdown

](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)[

](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

In this resource, you will find a summary of all the basic Markdown syntax. This is helpful if you want a quick reference guide for writing in Markdown.
# How to Write a Good README for Your Project

> The purpose, conventional structure, proper formatting of a README file, and best practices to follow when writing one.
### What is a README file?

> You may have noticed that when a GitHub repo is initialized, you see a prompt to create a README.md file immediately. As implied within it's name, a README file is a text file that contains text to introduce, explain and share the information required to understand what the project is about. 

Since a README file is often the first thing a visitor sees, it should tell the view how to install and use the project. 

There is not one good way to structure a README but there is only one bad way: to not include a README at all. 
### Conventions of a Good README File

> Your README should be as good as your project itself.

Make your project stand out and look professional by at least including the following elements in your README:

- **Project Title**: the name of your project
- **Description**: This is an extremely important component of the README. You should describe the main purpose of your project. Answer questions like "why did you build this project?" and "what problem(s) does it solve?" It also helps to include your motivations for the project and what you learned from it.
- **Features**: If your project has multiple features, list them here. Don't be afraid to brag if your project has unique features that make it stand out. You can even add screenshots and gifs to show off features.
- **How to Use**: Here, you should write step-by-step instructions on how to install and use your project. Any software or package requirements should also be listed here.
- **Collaborators**: If others have contributed yo your project in any way, it is important to give them credit for their work. Write your team member's or collaborators' names here along with a link to their GitHub profile.
- **License**: It's also important to list a license on your README so other developers can understand what they can and can't do with your project. You can use [this guide](https://choosealicense.com/) to help you choose a license.

> Keep READMEs brief but detailed. README should always be up-to-date and self-explanatory.

If you have spent a lot of time on your project, you should also spend a good chunk of time on your readme. 

- It can help your future self as well when your step away for a while and need to get reacquainted with your project.
- Not to mention it'll leave a positive impression on future interviewers who look at your GitHub profile.
### Using Markdown to Format READMEs

> Keep in mind that nobody wants to read a long block of unformatted text bloated with information. 

That is why a README file has the `.md` extension. 
### Use Headers

Every title or section (usage, license, etc.) in a README.md should be formatted as a header. Using headers and adding some HTML, we can achieve stuff like this:
### Level Up READMEs With Media

Documentation doesn’t have to be boring. Go for images or videos to make a project more understandable and appealing! We can add the project’s logo, diagrams, screenshots, or even GIFs!

For Markdown files living in a repository, the path to the image can either be to an URL or to an image file in the repository. For example, if we had an image named `diagram.png` inside the `images` folder of the repository, we could reference it like so `![Use Case Diagram](./images/diagram.png)` in the **README.md**.
# Git Branching

> Up to this point, you've practiced in a single Git branch. 

**Note: GitHub has changed the anming convention of the main branch from `master` to `main`. The course will be updated to reflect that, but until then, `master` refers to main.**

Git allows us to create *branches* to experiment with versions of a project. 

Imagine you want to create a version of a story with a happy ending. You can create a new branch and make the happy ending changes to that branch only. 

- It will have no effect
