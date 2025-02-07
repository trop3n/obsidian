---
up: "[[Real Python]]"
tags:
  - "#education/computerprogramming/languages/python/realpython/venv"
source: https://realpython.com/python-virtual-environments-a-primer/
---

# Intro

In this tutorial, you’ll learn how to work with [Python’s `venv` module](https://docs.python.org/3/library/venv.html) to create and manage separate [virtual environments](https://docs.python.org/3/library/venv.html#venv-def) for your Python projects. Each environment can use different versions of package dependencies and different versions of Python.

Once you’ve learned to work with virtual environments, you’ll be able to help other programmers reproduce your development setup and make sure that your projects never create dependency conflicts.

**By the end of this tutorial, you’ll know how to:**

- **Create** and **activate** a **Python virtual environment**
- Explain **why** you want to **isolate external dependencies**
- **Visualize what Python does** when you create a virtual environment
- **Customize** your virtual environments using **optional arguments** to `venv`
- **Deactivate** and **remove** virtual environments
- Choose **additional tools for managing** your Python versions and virtual environments

Working with virtual environments is a common and effective technique used in Python development. Gaining a better understanding of how they work, why you need them, and what you can do with them will help you master your Python programming workflow.

Throughout the tutorial, you can select code examples for either Windows, Ubuntu Linux, or macOS. Pick your platform at the top right of the relevant code blocks to get the commands that you need, and feel free to switch between them if you want to learn how to work with virtual environments on other operating systems.
# How Can You Work with a Python Virtual Environment?

If you just need to get a virtual environment up and running to continue working on your project, this section is for you.

This tutorial uses [Python’s `venv` module](https://docs.python.org/3/library/venv.html) to create virtual environments. This mode is part of Python's standard library, and it's been the [officially recommended](https://docs.python.org/3/library/venv.html#creating-virtual-environments) way to create virtual environments since Python 3.5.

> [!NOTE]
> **Note:** There are other great third-party tools for creating virtual environments, such as [conda](https://realpython.com/python-virtual-environments-a-primer/#the-conda-package-and-environment-manager) and [virtualenv](https://realpython.com/python-virtual-environments-a-primer/#the-virtualenv-project), that you’ll learn more about later in this tutorial. Either of these tools can help you set up a virtual environment and also go beyond just that.

For basic usage, `venv` is an excellent choice because it already comes packaged with your Python installation. With that in mind, you're ready to create your first virtual environment.
## Create It

Any time you're working on a Python project that uses external dependencies you're installing with `pip`, it's best to first create a virtual environment. 

```
python3 -m venv venv/
```

Many Linux operating systems ship with a version of Python3. If `python3` doesn't work, then you'll first have to install Python and you may need to se the specific name of the executable version that was installed, for example, `python3.12` for Python 3.12. If that's the case for you, remember to replace mention of `python3` in the code blocks with the specific version number. 

> [!NOTE]
> **Note:** You don’t need to include the slash (`/`) at the end of the name of your virtual environment, but it’s a helpful reminder that you’re creating a folder.

This command creates a new virtual environment named `venv` using Python's built-in `venv` module. The first `venv` that you use in the command specifies the module, and the second `venv/` sets the name for your virtual environment. You could name it differently, bu calling it *venv* is good practice for consistency. 
## Activate It

Great! Our project now has its own virtual environment. Generally, before we start to use it, we **activate it** by executing a script that comes with the installation. 

```bash
source venv/bin/activate
(venv) $
```

Before you run this command, make sure that you’re in the folder containing the virtual environment you just created. If you’ve named your virtual environment something other than _venv_, then you’ll have to use that name in the path instead of _venv_ when you source the activation script.

> [!NOTE]
> **Note:** You can also work with your virtual environment without activating it. To do this, you [provide the full path](https://realpython.com/python-virtual-environments-a-primer/#it-runs-from-anywhere-with-absolute-paths) to its Python interpreter when executing a command. However, you’ll likely want to activate the virtual environment after you create it to save yourself the effort of having to repeatedly type long pathnames.
## Install Packages Into It

After you've created and activated your virtual environment, you can install any external dependencies that you need for your project:

```bash
(venv) $ python -m pip install <package-name>
```

This command is the default command that you should use to install external Python packages with `pip`. Because you first created and activated the virtual environment, `pip` will install the packages in an isolated location.

**Note**: Since you created your virtual environment using a version of Python 3, you don't need to call `python3` or `pip3` explicitly. As long as your virtual environment is active, `python` and `pip` link to the same executable files that `python3` and `pip3` do. 

You can now install your packages to your virtual environment. To get to this point, you created a virtual environment named `venv` and then activated it in your current shell session. 

As long as you don't close your terminal, every Python package that you install will end up in this isolated environment instead of your global Python site-packages. This means that you can now work on your Python project without worrying about dependency conflicts. 
## Deactivate It

Once you're done working with this virtual environment, you can deactivate it:

```
(venv) $ deactivate
```

After executing the `deactivate` command, you command prompt returns to normal. This change means that you've exited your virtual environment. If you interact with Python or `pip` now, you'll interact with your globally configured Python environment. 

If you want to go back into a virtual environment that you've created before, then you'll need to [run the activate script](https://realpython.com/python-virtual-environments-a-primer/#activate-it) for that virtual environment once again.  

> [!NOTE]
> **Note**: Before you install a package, look for the name of your virtual environment within parenthesis just before your command prompt. In the example above, the name of the environment is `venv`. 
> 
> If the name appears, then you know that your virtual environment is active and you can install your external dependencies. If you don't see the name in your command line, remember to activate your Python virtual environment before installing any packages.

At this point, you've covered the essentials of working with Python virtual environments. 

However, if you want to learn the nuts and bolts of what exactly just happened, why so many tutorials ask you to create a venv in the first place, and what a virtual environment really is, then keep on reading. 
# Why do we Need Virtual Environments

Nearly everyone in the Python community suggests that you use virtual environments for all your projects. But why? If you want to find out why you need to set up a virtual environment in the first place, then this is the right section for you. 

The short answer is that **Python isn't great at dependency management**. If you're not specific, then `pip` will place all the external packages that you install in a folder called `site-packages/` in your base Python installation.

> [!Important] ## Deep Dive: Site Packages
> Technically, Python comes with *two* site packages folders:
> 
> 1. `purelib/` should contain only modules written in pure Python code.
> 2. `platlib/` should contain binaries that aren't written in pure Python, for example, `.dll`, `.so` or `.pydist` libraries.
> 
> You can find these folders in different locations if you're working on Fedora or Redhat Linux distributions. 
> 
> However, most operating systems implement Python's site-packages so that both locations point to the same path, effectively create a single site-packages folder. You can check the paths using `sysconfig`: 
> 
> ```sh
> import sysconfig
> sysconfig.get_path("purelib")
> '/usr/local/lib/python3.12/site-packages'
> sysconfig.get_path("platlib")
> '/usr/local/lib/python3.12/site-packages'
> ```
> 
> Most likely, both outputs will show you the same path. If both outputs are the same, then your operating system doesn't put `purelib` modules into a different folder than `platlib` modules. If two different paths show up, then your OS makes this distinction. 
> 
> Even if your operating system distiniguishes between the two, dependency conflicts will still arise because all `purelib` modules will go into a signle location for `purelib` modules, and the same will happen with the `platlib` modules.
> 
> 
> To work with virtual environments, you don't need to worry about the implementation details of a single site-packages folder or two separate ones. In fact, you probably won't ever need to think about it again. You can, however, keep in mind that when someone mentions Python's site packages directory, they *could* be talking about two different directories. 

Several issues can come up if all of your external packages land in the same folder. Next up, you'll learn more about these issues and other problems that virtual environments mitigate.
## Avoid System Pollution

Linux and macOS come preinstalled with a version of Python that the operating system uses for internal tasks. 

If you install packages to your operating system's global Python, these packages will mix with the system-relevant packages. This mix-up could have unexpected side effects on tasks crucial to your operating system's normal behavior. 

Additionally, if you update your operating system, then the packages you installed might get overwritten and lost, and you don't want either of those headaches to happen. 
## Sidestep Dependency Conflicts

One of your projects might require a different version of an external library compared to another project. If you only have one place to install packages, then you won't be able to work with two different versions of the same library. This is a common reason why it's recommended to use a Python virtual environment instead. 

To better understand why this is important, imagine you're building [Django websites](https://realpython.com/get-started-with-django-1/) for two different clients:

- One client is comfortable with their existing web app, which you initially built using [Django 2.2.26](https://pypi.org/project/Django/2.2.26/), and this client refuses to update their project to a modern Django version.
- Another client wants you to include async functionality in their website, which is only available [starting with Django 3.1](https://docs.djangoproject.com/en/5.1/releases/3.1/#what-s-new-in-django-3-1). You’ll want to use a modern Django version for this client!

If you install Django globally, you can only have one version installed:

```shell
$ python -m pip install django==2.2.26
$ python -m pip list
Package   Version
-------   -------
Django    2.2.26
pip       24.2
pytz      2024.1
sqlparse  0.5.1

$ python -m pip install django==5.1
$ python -m pip list
Package   Version
-------   -------
asgiref   3.8.1
Django    5.1
pip       24.2
pytz      2024.1
sqlparse  0.5.1
```

If you install two different versions of the same package into your global Python environment, the second installation overwrites the first one. For the same reason, having a single virtual environment for both clients won't work either. You can't have two different versions of the same package in a single Python environment.

Looks like you won't be able to work on one of the two projects with this setup! However, if you create a virtual environment for each of your client's projects, then you can install a different version of Django into each of them:

```sh
$ python3 -m venv client-old/
$ source client-old/bin/activate
(client-old) $ python -m pip install django==2.2.26
(client-old) $ python -m pip list
Package  Version
-------- -------
Django   2.2.26
pip      24.2
pytz     2024.1
sqlparse 0.5.1
(client-old) $ deactivate

$ python3 -m venv client-new/
$ source client-new/bin/activate
(client-new) $ python -m pip install django==5.1
(client-new) $ python -m pip list
Package  Version
-------- -------
asgiref  3.8.1
Django   5.1
pip      24.2
sqlparse 0.5.1
(client-new) $ deactivate
```

If you now activate either of the two virtual environments, then you'll notice that it still holds its own specific version of of Django. The two environments also have different dependencies, and each only contains dependencies necessary for that version of Django. 

With this setup, you can activate one environment when you work on one project and another when you work on the other. Now you can keep any number of clients happy at the same time.
## Minimize Reproducibility Issues

If all your packages are in one location, then it'll be difficult to only [pin dependencies](https://realpython.com/python-virtual-environments-a-primer/#pin-your-dependencies) that are relevant for a single project.

If you've worked with Python for a while, then your global Python environment might already include all sorts of third-party packages. If that's not the case, then pat yourself on the back. You've probably installed a new version of Python recently, or you already know how to handle virtual environments to [avoid system pollution](https://realpython.com/python-virtual-environments-a-primer/#avoid-system-pollution).

To clarify what reproducibility issues you can encounter when sharing a Python environment across multiple projects, you'll look at an example next. Imagine you've worked on two independent projects over the past month:

1. [A web scraping project with Beautiful Soup](https://realpython.com/beautiful-soup-web-scraper-python/)
2. [A Flask application](https://realpython.com/python-web-applications-with-flask-part-i/)

Unaware of virtual environments, you installed all necessary packages into your global Python environment:

```
$ python3 -m pip install beautifulsoup4 requests
$ python3 -m pip install flask
```

Your Flask app has turned out to be quite helpful, so other developers want to work on it as well. They need to reproduce the environment that you used for working on it. You want to go ahead and [pin your dependencies](https://realpython.com/python-virtual-environments-a-primer/#pin-your-dependencies) so that you can share your project online:

```sh
$ python3 -m pip freeze
beautifulsoup4==4.12.3
blinker==1.8.2
certifi==2024.8.30
charset-normalizer==3.3.2
click==8.1.7
Flask==3.0.3
idna==3.8
itsdangerous==2.2.0
Jinja2==3.1.4
MarkupSafe==2.1.5
requests==2.32.3
soupsieve==2.6
urllib3==2.2.2
Werkzeug==3.0.4
```

Which of these packages are relevant to your Flask app, and which ones are here because of your web scraping project? It's hard to tell when all external dependencies are in a single bucket. 

With a single environment like this, you'd have to manually go through the dependencies and know which are necessary for your project and which aren't. At best, this approach is tedious, but even more so, it's error-prone.

If you use a separate virtual environment for each of your projects, then it'll be more straightforward to read the project requirements from your pinned dependencies. That means you can more easily share your code when you develop a great app, making it possible for others to collaborate.
## Dodge Installation Privilege Lockouts

Finally, you may need admin privileges on a computer to install packages into the host Python's site-packages directory. In a corporate network, you most likely won't have that level of access to the machine that you're working on.

If you use virtual environments, then you create a new installation location within the scope of your user privileges, which allows you to install and work with external packages.

Whether you're coding as a hobby on your own machine, developing websites for clients or working in a corporate environment, using a virtual environment will save you lots of grief in the long run.
# What is a Python Virtual Environment?

At this point, you're convinced you want to work with virtual environments. Great, but *what* are you working with you use one? If you want to understand what virtual environments are, then this is the right section for you.

The short answer is that a Python virtual environment is a folder structure that gives you everything you need to run a lightweight yet isolated Python environment.
## A Folder Structure

When you create a new virtual environment using the `venv` module, Python creates a self-contained folder structure and or copies [symlinks](https://en.wikipedia.org/wiki/Symbolic_link) the Python [executable files](https://en.wikipedia.org/wiki/Executable) into that folder structure.

You don't need to dig deeply into this folder structure to learn more about what virtual environments are made of. In just a bit, you'll carefully scrape off the topsoil and investigate the high-level structures that you uncover. 

However, if you already have your shovel out and are itching to dig, then look at the section below:

> [!NOTE]
> Welcome, brave one. You’ve accepted the challenge to venture deeper into your virtual environment’s folder structure! In this collapsible section, you’ll find instructions on how to take a look into that dark abyss.
> 
> On your command line, navigate to the folder that contains your virtual environment. Take a deep breath and brace yourself, then execute the `tree` command to display the contents of the directory:
> 
> ```
>  tree venv/
> ```
> 
> **Note**: Alternatively, you could hone your skills by creating a new virtual environment, install the `rptree` package into it, and use that to display the folder's tree structure. You could even take a bigger detour and [build that directory tree generator](https://realpython.com/directory-tree-generator-python/) yourself!
> 
> However you end up displaying the contents of the `venv/` folder, you might be surprised by what you find. Many developers experience a slight shock when they first take a peek. There are _a lot_ of files in there!
> 
> If this was your first time and you felt that way, then welcome to the group of people who have taken a look and been a bit overwhelmed !

A virtual environment folder contains a lot of files and folders, but you might notice that most of what makes this tree structure so long rests inside the `site-packages/` folder. If you trim down the subfolders and files in there, you end up with a tree structure that isn't too overwhelming:

```
venv/
│
├── bin/
│   ├── Activate.ps1
│   ├── activate
│   ├── activate.csh
│   ├── activate.fish
│   ├── pip
│   ├── pip3
│   ├── pip3.12
│   ├── python
│   ├── python3
│   └── python3.12
│
├── include/
│   │
│   └── python3.12/
│
├── lib/
│   │
│   └── python3.12/
│       │
│       └── site-packages/
│           │
│           ├── pip/
│           │
│           └── pip-24.2.dist-info/
│
├── lib64/
│   │
│   └── python3.12/
│       │
│       └── site-packages/
│           │
│           ├── pip/
│           │
│           └── pip-24.2.dist-info/
│
└── pyvenv.cfg
```

This reduced tree structure gives you a better overview of what's going on in your virtual environment folder:

- `bin/` contains the executable files for your virtual environment. Most notable are the Python interpreter (`python`) and the `pip` executable (`pip`) as well as their respective symlinks (`python3`. `python3.12`, `pip3`, `pip3.12`). The folder also contains activation scripts for the virtual environment. Your specific activation script depends on what shell you use. For example, in this tutorial, you can `activate`, which works for the Bash and Zsh shells. 

- `include/` is an initially empty repository that Python uses to [include C header files](https://docs.python.org/3/c-api/intro.html#include-files) for packages you might install that depend on C extensions.

- `lib/` contains the `site-packages` directory nested in a folder the designates the Python version (`python3.12`/). `site-packages/` is one of the main reasons for creating your virtual environment. This folder is where you'll install the external packages that you want to use with your virtual environment. [Starting with Python 3.12](https://github.com/python/cpython/issues/95299), your virtual environment comes preinstalled with only one dependency, `pip`. You’ll learn more about it in a bit.

- `lib64/` in many Linux systems comes as a symlink to `lib/` [for compatibility reasons](https://stackoverflow.com/a/11370995/5717580). Some Linux systems may use the distinction between `lib/` and `lib64/` to install different versions of libraries depending on their architecture.

- A `{name}--{version}.dist-info/` **directory**, which you get by default for `pip`, contains [package distribution](https://realpython.com/pypi-publish-python-package/) information that exists to [record information about installed packages](https://packaging.python.org/en/latest/specifications/recording-installed-packages/#the-dist-info-directory).

- `pyvenv.cfg` is a crucial file for your virtual environment. It contains only a couple of key-value pairs that Python uses to set variables in the `sys` module that determine which Python interpreter and site-packages directory the current Python session will use. You'll learn more about the settings in this file when your read about how a virtual environment works.

From this bird's eye view of the contents of your virtual environments folder, you can zoom out even further to discover that there are three essential parts to a virtual environment:

1. A copy of a symlink of the **Python Binary**
2. A `pyvenv.cfg` file.
3. A **site-packages directory**

The installed package inside `site-packages/` is optional but comes as a reasonable default. 
However, your virtual environment  would still be a valid virtual environment if this directory were empty, and there are ways to create it [without installing any dependencies](https://realpython.com/python-virtual-environments-a-primer/#avoid-installing-pip).

With the default settings, `venv` will install only `pip`, which is the recommended tool to install packages in Python. Because installing other packages is the most common use case for virtual environments, you'll want to have access to `pip`. 

You can double-check that Python has installed `pip` to your virtual environment by using `pip` when you created the virtual environment with its default settings.

> [!NOTE]
> **Note**: Below that output, `pip` might also display a warning that you're not using the latest version of the module. Don't worry about this yet. Later, you'll learn more about why this happens and how to [automatically update `pip`](https://realpython.com/python-virtual-environments-a-primer/#update-the-core-dependencies) when you create your virtual environment.

The files that make up `pip` constitute most of the content of your new virtual environment. If you avoid looking at the packages contents, then the structure is already a lot less daunting.

If you're working with a Python version that's older than 3.12, then you'll notice that there are a couple of additional folders in the `site-packages` directory. Expand the collapsible section to learn more about them:

> [!NOTE]
> - **The `setuptools` module** has been a fundamental tool in the Python packaging ecosystem for many years. `setuptools` extended the `distutils` module with features like package discovery and distribution, and dependency management. Including `setuptools` by default ensured that users had immediate access to these features without having to install additional tools. Before the adoption of [PEP 517](https://peps.python.org/pep-0517/) and [PEP 518](https://peps.python.org/pep-0518/), many packages relied on `setuptools` for installation.
> - **The `_distutils_hack/` module**, [in a manner true to its name](https://github.com/pypa/setuptools/blob/main/_distutils_hack/), ensures that when performing package installations, Python picks the local `._distutils` submodule of `setuptools` over the standard library’s `distutils` module.
> - **The `pkg_resources/` module** helps applications discover plugins automatically and allows Python packages to access their resource files. It’s [distributed together with `setuptools`](https://setuptools.pypa.io/en/latest/pkg_resources.html).
> 
> Finally, there’s also a file named **`distutils-precedence.pth`**. This file helps set the path precedence for `distutils` imports and works together with `_distutils_hack` to ensure that Python prefers the version of `distutils` that comes bundled with `setuptools` over the built-in one.
> 
> You’re learning about these additional files and folders for the sake of completeness. If you’re on Python 3.12 or later, then they won’t come preinstalled in your virtual environment. Even if you’re working with an older version of Python, you won’t need to remember them to effectively work with your virtual environments.
> 
> It’s enough to keep in mind that any preinstalled packages in your `site-packages/` directory are standard tools that make installing _other_ packages more user-friendly.

At this point, you've seen all the files and folders that make up a virtual environment if you've installed it using the built-in `venv` module.

Remember that your virtual environment is just a folder structure, which means that you can delete and re-create it anytime you want. But why *this specific* folder structure, and what does this structure make possible?
# An Isolated Python Environment

Python virtual environments aim to provide a lightweight, isolated Python environment that you can quickly create and then discard when you don't need it anymore. The folder structure that you just explored makes that possible by providing three key pieces:

1. A copy or symlink of the **Python Binary**
2. a `pyvenv.cfg` file
3. a **site-packages directory**

You want to achieve and isolated environment so that any external packages you install wn't conflict with global-site packages. To make this possible, `venv` reproduces the folder structure that a standard Python installation creates. 

This structure accounts for the location of the copy or symlink of the Python binary and the site-packages directory, where Python installs external site packages. 

> [!NOTE]
> **Note:** Whether or not the Python executable in your virtual environment is a copy or a symlink of the Python executable that you’ve based the environment on depends primarily on your operating system.
> 
> Windows and Linux may create symlinks instead of copies, while macOS always creates a copy. You can try to [influence the default behavior](https://realpython.com/python-virtual-environments-a-primer/#copy-or-link-your-executables) with optional arguments when you create the virtual environment. However, this is something you won’t have to worry about in most cases.

In addition to the Python binary and site-packages directory, you also get the `pyvenv.cfg` file. It's a small file that contains only a couple of key-value pairs. However, these settings are crucial for making your virtual environment work:

```
home = /usr/local/bin
include-system-site-packages = false
version = 3.12.5
executable = /usr/local/bin/python3.12
command = /usr/local/bin/python3.12 -m venv /home/name/path/to/project/venv
```

We will learn more about this file later when reading about [how a virtual environment works](https://realpython.com/python-virtual-environments-a-primer/#how-does-a-virtual-environment-work).

Suppose you closely inspect your newly minted virtual environment's folder structure. You might notice that this lightweight installation doesn't contain any of the trusted [standard library](https://docs.python.org/3/library/) modules. Some might say that Python without its standard library is like a toy car without batteries!

However, if you start the Python interpreter from within your virtual environment, then you can still access all the goodies from the standard library.

```
>>> import urllib
>>> from pprint import pp
>>> pp(dir(urllib))
['__builtins__',
 '__cached__',
 '__doc__',
 '__file__',
 '__loader__',
 '__name__',
 '__package__',
 '__path__',
 '__spec__']
```

In this example code snipper, you've successfully [imported](https://realpython.com/python-import/) both the [`urllib` module](https://realpython.com/urllib-request/) and the `pp()` shortcut from the [pretty print module](https://realpython.com/python-pretty-print/). Then you used `dir()` to inspect the `urllib` module.

Both modules are part of the standard library, so how come you have to access to them even though they're not in the folder structure of our Python venv?

You can access Python's standard library modules because your virtual environment reuses Python's built in library and standard library modules from the Python installation we used to create our virtual environment. In a later section, you'll learn *how* the virtual environment achieves [linking to your base Python’s standard library](https://realpython.com/python-virtual-environments-a-primer/#it-links-back-to-your-standard-library).

> [!NOTE]
> **Note:** Because you always need an existing Python installation to create your virtual environment, `venv` opts to reuse the existing standard-library modules to avoid the overhead of copying them into your new virtual environment. This intentional behavior speeds up the creation of virtual environments and makes them more lightweight, as described in the [motivation for PEP 405](https://www.python.org/dev/peps/pep-0405/#motivation).

In addition to the standard-library modules, you can optionally [give your virtual environment access to the base installation’s site-packages](https://realpython.com/python-virtual-environments-a-primer/#include-the-system-site-packages) through an argument when you create the environment:

```
$ python3 -m venv venv/ --system-site-packages
```

If you add `--system-site-packages` when you call `venv`, Python will set the value to `include-system-site-packages` in `pyvenv.cfg` to `true`. This setting means that you can use any external packages that you installed to your base Python as if you'd installed them into your virtual environment. 

This connection works in only one direction. Even if you give your virtual env access to the source Python's site-package folder, any new packages you install into your virtual environment won't mingle with the packages there. Python will respect the isolated nature of installations to your virtual environment and place them into the separate side-packages directory within the virtual environment. 

You now understand that a virtual environment is basically a folder structure with a settings file. It may or may not come with `pip` preinstalled, and it has access to the source Python’s standard-library modules while remaining isolated. However, you might still be wondering how all of this works, and you’ll delve into that next.
# How Does a Virtual Environment Work?

If you know what a virtual environment is but wonder how it manages to create the lightweight isolation that it provides, then you're in the right section. Here you’ll [peek under the hood](https://realpython.com/podcasts/rpp/156/) and learn how the folder structure and the settings in your `pyvenv.cfg` file interact with Python to provide a reproducible and isolated space for installing external dependencies.

If you like the [Real Python Podcast](https://realpython.com/real-python-podcast-launch/), then you can listen to the episodes [Launching Python, Virtual Environments, and Locking Dependencies](https://realpython.com/podcasts/rpp/93/) and [Virtual Environment Structure & Surveying the Packaging Ecosystem](https://realpython.com/podcasts/rpp/156/), both with Brett Cannon, for an audio-guided tour on [how virtual environments work](https://snarky.ca/how-virtual-environments-work/).
## It Copies Structure and Files

When you create a virtual environment using `venv`, the module re-creates the file and [folder structure](https://realpython.com/python-virtual-environments-a-primer/#a-folder-structure) of a standard Python installation on your operating system. Python also copies or symlinks to that folder structure the Python executable with which you've called `venv`. 

```
venv/
│
├── bin/
│   ├── Activate.ps1
│   ├── activate
│   ├── activate.csh
│   ├── activate.fish
│   ├── pip
│   ├── pip3
│   ├── pip3.12
│   ├── python
│   ├── python3
│   └── python3.12
│
├── include/
│
├── lib/
│   │
│   └── python3.12/
│       │
│       └── site-packages/
│
├── lib64/
│   │
│   └── python3.12/
│       │
│       └── site-packages/
│
└── pyvenv.cfg
```

If you locate your system-wide Python installation on your operating system and inspects the folder structure there, then you'll see that your virtual environment resembles that structure. 

You can find the base Python installation is based on by navigating to the path you can find under the `home` key in `pyvenv.cfg`.

> [!NOTE]
> **Note:** On Windows, you may notice that `python.exe` in your base Python installation isn’t in `Scripts\` but is one folder level up. In your virtual environment, the executable is intentionally located in the `Scripts\` folder.
> 
> This small change to the folder structure means that you only need to add a single directory to your shell [`PATH`](https://realpython.com/add-python-to-path/) variable to activate the virtual environment.

While you might find some additional files and folders in your base Python installation, you'll notice that the standard folder strucutre is the same as in your virtual environment. `venv` creates this folder structure to ensure that Python will work as expected in isolation, without needing to apply additional changes. 
## It Adapts the Prefix-Finding Process

