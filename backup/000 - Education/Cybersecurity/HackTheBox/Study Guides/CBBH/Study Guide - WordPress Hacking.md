# Study Guide: Hacking WordPress

## Section 1: Intro

### Practice Questions:

1. What is WordPress primarily used for?
2. Name three examples of popular WordPress plugins.
3. Why is WordPress considered customizable and extensible?
4. What are the main components of a CMS?
5. What is the difference between a CMA and a CDA in a CMS?
6. What makes WordPress vulnerable to attacks?
7. What technologies does WordPress typically run on?
8. What is the purpose of themes and plugins in WordPress?
9. How can hosting companies assist with WordPress security?
10. What will this module teach you about WordPress?

### Practical Exercises:

1. Install WordPress on your local machine using XAMPP or Docker.
2. Explore the WordPress admin dashboard and identify key features.
3. Install and activate a free plugin from the WordPress repository.
4. Customize the appearance of your WordPress site using a theme.
5. Create a new page and post in WordPress.
6. Export your WordPress site's database using phpMyAdmin.
7. Research and list three vulnerabilities associated with WordPress plugins.
8. Write a short report on why WordPress is a popular target for attackers.
9. Set up a local development environment for WordPress.
10. Experiment with different themes and observe how they change the site's layout.

---

## Section 2: WordPress Structure

### Practice Questions:

1. What is the default file structure of a WordPress installation?
2. What is the purpose of the `index.php` file in WordPress?
3. Where is the WordPress configuration file located?
4. What information does the `wp-config.php` file contain?
5. What is the role of the `wp-content` directory?
6. What types of files are stored in the `wp-includes` directory?
7. How can you identify the WordPress version from the source code?
8. What is the significance of the `readme.html` file in older WordPress versions?
9. What is the purpose of the `wp-admin` folder?
10. How can renaming the login page improve security?

### Practical Exercises:

1. Locate and review the `wp-config.php` file in a WordPress installation.
2. Modify the `wp-config.php` file to enable debugging mode.
3. Enumerate all installed plugins by inspecting the `wp-content/plugins` directory.
4. Identify the active theme by reviewing the `wp-content/themes` directory.
5. Use `cURL` to retrieve the WordPress version from the source code.
6. Rename the `wp-login.php` file and test access to the login page.
7. Disable directory indexing in Apache and verify the change.
8. Inspect the `wp-includes` directory and list core files stored there.
9. Manually edit the `index.php` file to display a custom message.
10. Remove unused themes and plugins from a WordPress installation.

---

## Section 3: WordPress User Roles

### Practice Questions:

1. What are the five default user roles in WordPress?
2. Which user role has the highest level of access?
3. What can an editor do that an author cannot?
4. Can a contributor publish their own posts? Why or why not?
5. What is the primary function of a subscriber?
6. Why is gaining administrator access critical for attackers?
7. How can user roles be exploited during an attack?
8. What permissions does an author have?
9. Can a subscriber edit other users' profiles? Why or why not?
10. How can user roles be managed in WordPress?

### Practical Exercises:

1. Create users with different roles (admin, editor, author, contributor, subscriber).
2. Log in as each user role and document the differences in permissions.
3. Assign a user the "Editor" role and test their ability to manage posts.
4. Attempt to publish a post as a contributor and observe the limitations.
5. Promote a subscriber to an administrator and verify the change.
6. Use WPScan to enumerate users on a WordPress site.
7. Test password brute-forcing against a low-privileged user account.
8. Restrict user roles using a WordPress security plugin.
9. Audit user roles and remove unnecessary accounts.
10. Implement two-factor authentication for all user roles.

---

## Section 4: WordPress Core Version Enumeration

### Practice Questions:

1. Why is identifying the WordPress version important during enumeration?
2. How can you find the WordPress version using the page source code?
3. What is the `meta generator` tag, and where is it located?
4. How can CSS and JS files reveal version information?
5. What is the significance of the `readme.html` file in older versions?
6. How can you use `cURL` to extract version information?
7. What are passive and active enumeration methods?
8. How can outdated versions of WordPress be exploited?
9. What tools can automate version enumeration?
10. Why is version enumeration a critical step in penetration testing?

### Practical Exercises:

1. Use `cURL` to extract the WordPress version from a live site.
2. Inspect the page source code of a WordPress site to locate the `meta generator` tag.
3. Review CSS and JS files to identify version-related clues.
4. Access the `readme.html` file on an older WordPress site.
5. Use WPScan to enumerate the WordPress version.
6. Write a script to automate version enumeration using `cURL`.
7. Compare the results of passive and active enumeration methods.
8. Research known vulnerabilities for a specific WordPress version.
9. Enumerate the WordPress version using the JSON API endpoint.
10. Test version enumeration on a local WordPress installation.

---

## Section 5: Plugins and Themes Enumeration

### Practice Questions:

1. How can you identify installed plugins manually?
2. What is the purpose of the `wp-content/plugins` directory?
3. How can you use `cURL` to enumerate plugins?
4. What is directory indexing, and why is it a security risk?
5. How can deactivated plugins still pose a risk?
6. What is the best practice for managing unused plugins?
7. How can themes be enumerated using the JSON API?
8. What tools can automate plugin and theme enumeration?
9. Why is it important to keep plugins and themes updated?
10. How can outdated plugins be exploited?

### Practical Exercises:

1. Enumerate installed plugins by inspecting the page source code.
2. Use `cURL` to enumerate plugins via directory listing.
3. Test directory indexing on a WordPress site and disable it.
4. Enumerate themes using the JSON API endpoint.
5. Use WPScan to enumerate plugins and themes.
6. Identify outdated plugins and research their vulnerabilities.
7. Remove unused plugins and themes from a WordPress site.
8. Test for Local File Inclusion (LFI) in a vulnerable plugin.
9. Exploit a known vulnerability in an outdated plugin.
10. Automate plugin enumeration using a custom script.

---

## Section 6: User Enumeration

### Practice Questions:

1. Why is user enumeration important in WordPress security assessments?
2. How can you enumerate users using the `author` parameter?
3. What is the JSON API endpoint used for user enumeration?
4. How can you confirm the existence of a user using `cURL`?
5. What response indicates a non-existent user?
6. How can user enumeration aid in brute-force attacks?
7. What changes were made to the JSON API after WordPress 4.7.1?
8. How can you prevent user enumeration on a WordPress site?
9. What tools can automate user enumeration?
10. Why is disabling user enumeration a best practice?

### Practical Exercises:

1. Enumerate users using the `author` parameter in the URL.
2. Use `cURL` to confirm the existence of a user.
3. Enumerate users using the JSON API endpoint.
4. Test for user enumeration on a local WordPress installation.
5. Use WPScan to enumerate users.
6. Implement a plugin to disable user enumeration.
7. Test brute-force attacks using enumerated usernames.
8. Audit user accounts and remove unused ones.
9. Research and exploit a vulnerability related to user enumeration.
10. Write a script to automate user enumeration.

---

## Section 7: Login and Brute Force Attacks

### Practice Questions:

1. How can you perform a brute-force attack on WordPress?
2. What is the difference between `wp-login` and `xmlrpc` methods?
3. What response indicates successful login credentials?
4. What is the purpose of the `xmlrpc.php` file?
5. How can you prevent brute-force attacks on WordPress?
6. What tools can automate brute-force attacks?
7. Why is limiting login attempts important?
8. How can two-factor authentication enhance security?
9. What is the impact of weak passwords on WordPress security?
10. How can you detect brute-force attacks?

### Practical Exercises:

1. Perform a brute-force attack using WPScan.
2. Test the `xmlrpc.php` file for vulnerabilities.
3. Limit login attempts using a WordPress plugin.
4. Implement two-factor authentication for all users.
5. Test the effectiveness of strong passwords against brute-force attacks.
6. Monitor login attempts using a security plugin.
7. Block malicious IPs using a firewall.
8. Audit user passwords and enforce strong password policies.
9. Detect and log brute-force attempts.
10. Simulate a brute-force attack and analyze the logs.

---

## Section 8: Exploiting Vulnerable Plugins

### Practice Questions:

1. What is Local File Inclusion (LFI), and how can it be exploited?
2. How can you verify an LFI vulnerability using `cURL`?
3. What is the impact of an LFI vulnerability?
4. How can you exploit SQL Injection in a WordPress plugin?
5. What tools can automate vulnerability exploitation?
6. How can you mitigate plugin vulnerabilities?
7. Why is keeping plugins updated important?
8. What is the role of the WPVulnDB database?
9. How can you use WPScan to identify vulnerable plugins?
10. What is the impact of exploiting a vulnerable plugin?

### Practical Exercises:

1. Exploit an LFI vulnerability using `cURL`.
2. Verify an LFI vulnerability in a lab environment.
3. Exploit SQL Injection in a vulnerable plugin.
4. Use WPScan to identify vulnerable plugins.
5. Research and exploit a known plugin vulnerability.
6. Update all plugins to their latest versions.
7. Remove unused and outdated plugins.
8. Use WPVulnDB to check for plugin vulnerabilities.
9. Test for vulnerabilities in a custom plugin.
10. Write a report on mitigating plugin vulnerabilities.

---

## Section 9: Remote Code Execution (RCE) via the Theme Editor

### Practice Questions:

1. How can you achieve RCE through the WordPress Theme Editor?
2. What is the purpose of the `system()` function in PHP?
3. Why should you modify an inactive theme?
4. How can you upload a web shell to WordPress?
5. What is the impact of RCE on a WordPress site?
6. How can you prevent unauthorized access to the Theme Editor?
7. What tools can automate RCE exploitation?
8. Why is restricting file editing important?
9. How can you detect unauthorized code changes?
10. What is the role of least privilege in preventing RCE?

### Practical Exercises:

1. Upload a web shell using the Theme Editor.
2. Test RCE by executing system commands via a web shell.
3. Modify an inactive theme to avoid corrupting the main theme.
4. Restrict file editing in the WordPress admin panel.
5. Use a security plugin to detect unauthorized code changes.
6. Audit theme files for suspicious code.
7. Implement least privilege for WordPress users.
8. Test RCE in a lab environment.
9. Write a script to detect unauthorized file modifications.
10. Analyze logs for signs of RCE exploitation.

---

## Section 10: WordPress Hardening

### Practice Questions:

1. What are the best practices for securing a WordPress site?
2. Why is regular updating important?
3. How can you enable automatic updates in WordPress?
4. What is the role of security plugins in WordPress?
5. How can you prevent user enumeration?
6. Why is renaming the login page beneficial?
7. What is the impact of strong password enforcement?
8. How can two-factor authentication enhance security?
9. What is the role of a Web Application Firewall (WAF)?
10. How can you audit user rights and access?

### Practical Exercises:

1. Enable automatic updates in WordPress.
2. Install and configure a security plugin.
3. Prevent user enumeration using a plugin.
4. Rename the `wp-login.php` file and test access.
5. Enforce strong password policies for all users.
6. Implement two-factor authentication.
7. Configure a WAF to block malicious traffic.
8. Audit user rights and revoke unnecessary access.
9. Test the effectiveness of hardening measures.
10. Write a report on WordPress hardening best practices.