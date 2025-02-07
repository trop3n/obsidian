---
title: Server-Side Vulnerabilities
source: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/path-traversal-apprentice/file-path-traversal/what-is-path-traversal
tags:
  - webappsecurity
  - portswigger
created: 2025-01-07
---

![](https://i.imgur.com/A3Xfxdh.png)
# What is Path Traversal?

Path traversal is also known as **directory traversal**. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. This might include:

- Application code and data.
- Credentials for back-end systems.
- Sensitive operating system files.

In some cases, an attacker might be able to *write arbitrary files on the server*, allowing them to *modify application data or behavior*, and ultimately take control of the server.
## Reading Arbitrary Files Via Path Traversal

Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML:

```
<img src="/loadImage?filename=218.png">
```

The `loadImage` URL takes a `filename` parameter and returns the contents of the specified file. The image files are stored on disk in the location `/var/www/images/`. To return an image, the application appends the requested filename to this base directory and uses a filesystem API to read the contents of the file. In other words, the application reads from the following file path:

```
/var/www/images/218.png
```

This application implements no defenses against path traversal attacks. As a result, an attacker can request the following URL to retrieve the `/etc/passwd` file from the server's filesystem:

```
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```

This causes the application to read from the following path:

```
/var/www/images/../../../etc/passwd
```

The sequence `../` is **valid** within a file path, and means to step up one level in the directory structure. The three consecutive `../` sequences step up from `/var/www/images/` to the filesystem root, and so the file that is actually read is:

```
/etc/passwd
```

On Unix-based operating systems, this is a standard file *containing details* of the **users** that are registered on the server, but an attacker could retrieve other arbitrary files using the same technique. 

On Windows, both `../` and `..\` are valid directory traversal sequences. The following is an example of an equivalent attack against a Windows-based server:

```
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```
# Access Control
## What is Access Control?

Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management.

- **Authentication** confirms that the user is who they say they are.
- **Session Management** identifies which subsequent HTTP requests are being made by that same user.
- **Access Control** determines whether the user is allowed to carry out actions that they are attempting to perform.

![](https://i.imgur.com/7aPQ8C9.png)
## Vertical Privilege Escalation

If a user gains access to functionality that they are *not permitted to access*, then is is **vertical**
**privilege escalation**. For example, if a non-admin user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.
## Unprotected Functionality

At its most basic, vertical privilege escalation arises where an application does **not enforce**
**any protection for sensitive functionality**. 
	For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:

```
https://insecure-website.com/admin
```

This might be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the `robots.txt` file:

```
https://insecure-website.com/robots.txt
```

Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of sensitive functionality. 

In some cases, sensitive information is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity". However, hiding sensitive functionality does not provide effective access control because users might discover the obfuscated URL in a number of ways. 

Imagine an application that hosts administrative functions at the following URL:

```
https://insecure-website.com/administrator-panel-yb556
```

This might not be directly guessable by an attacker. However, an application might still leak the URL to users. The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:

```js
<script> 
	var isAdmin = false; 
	if (isAdmin) { 
		... 
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556'); 
		adminPanelTag.innerText = 'Admin panel'; 
		... 
	} 
</script>
```

This script adds a link to the user's UI if they are an admin user. However, the script containing the URL is visible to all users regardless of their role. 


