# Study Guide: Web Requests

This study guide is designed to help you review and practice the key concepts from the markdown file. Each section corresponds to a `#` header in the original document, with 10 questions and practical exercises for each section.

---

## HyperText Transfer Protocol

### Questions
1. What is HTTP, and how does it facilitate communication on the web?
2. Describe the structure of a URL and its components.
3. What are the default ports for HTTP and HTTPS?
4. How does DNS resolution work in the context of HTTP requests?
5. What is the purpose of the `/etc/hosts` file?
6. How can cURL be used to send HTTP requests?
7. What are the differences between HTTP and HTTPS?
8. How does HTTPS ensure secure communication?
9. What is the role of SSL certificates in HTTPS?
10. How can you bypass SSL certificate checks in cURL?

### Practical Exercises
1. Use cURL to send a basic HTTP GET request to a website.
2. Download a webpage using cURL and save it to a file.
3. Use cURL to send a request to an HTTPS site with an invalid SSL certificate.
4. Analyze the headers of an HTTP response using cURL's verbose mode.
5. Modify the User-Agent header in a cURL request.
6. Set up a local `/etc/hosts` entry to map a domain to an IP address.
7. Use browser DevTools to inspect network requests made by a webpage.
8. Capture and analyze an HTTPS request using a proxy tool like Burp Suite.
9. Compare the headers of HTTP and HTTPS responses.
10. Use cURL to send a HEAD request and analyze the response.


---

## HTTP Requests and Responses

### Questions
1. What are the main components of an HTTP request?
2. Describe the structure of an HTTP response.
3. What is the purpose of HTTP headers?
4. How do general headers differ from entity headers?
5. What are some common request headers?
6. What are some common response headers?
7. How do security headers enhance web security?
8. What is the purpose of the `Content-Type` header?
9. How can you view HTTP headers using cURL?
10. What is the difference between the `-I` and `-i` flags in cURL?

### Practical Exercises
1. Use cURL to send a request with custom headers.
2. Analyze the headers of an HTTP response using browser DevTools.
3. Modify the `Referer` header in a cURL request.
4. Set a custom `User-Agent` header in a cURL request.
5. Use cURL to view both the headers and body of an HTTP response.
6. Inspect cookies set by a website using browser DevTools.
7. Add a custom `Authorization` header to a cURL request.
8. Use cURL to send a request with multiple headers.
9. Analyze the `Set-Cookie` header in an HTTP response.
10. Use cURL to send a request with a `Content-Length` header.

---

## HTTP Methods and Codes

### Questions
1. What are the most commonly used HTTP methods?
2. Describe the purpose of the GET and POST methods.
3. What is the difference between PUT and DELETE methods?
4. How do response codes indicate the status of an HTTP request?
5. What are some common 2xx, 3xx, 4xx, and 5xx response codes?
6. How can you use cURL to send different types of HTTP requests?
7. What is HTTP Basic Authentication?
8. How can you authenticate using HTTP Basic Auth with cURL?
9. What is the purpose of the `Authorization` header?
10. How can you manually set the `Authorization` header in a cURL request?

### Practical Exercises
1. Use cURL to send a GET request with query parameters.
2. Authenticate to a web page using HTTP Basic Auth with cURL.
3. Send a POST request with form data using cURL.
4. Use cURL to send a PUT request to update a resource.
5. Delete a resource using a DELETE request with cURL.
6. Analyze the response codes of different HTTP requests.
7. Use browser DevTools to inspect the request and response of a login form.
8. Craft a cURL command to send JSON data in a POST request.
9. Use cURL to follow redirects with the `-L` flag.
10. Inspect the `Set-Cookie` header after a successful login.

---

## CRUD API

### Questions
1. What are the four main operations in a CRUD API?
2. How do HTTP methods map to CRUD operations?
3. What is the purpose of the `Content-Type` header in API requests?
4. How can you use cURL to read data from an API?
5. What is the difference between POST and PUT methods in API usage?
6. How can you update an entry in an API using cURL?
7. What is the purpose of the DELETE method in API requests?
8. How can you format JSON output using tools like `jq`?
9. What are some common security considerations when using APIs?
10. How can you authenticate API requests using cookies or tokens?

### Practical Exercises
1. Use cURL to read data from a CRUD API endpoint.
2. Add a new entry to an API using a POST request.
3. Update an existing entry in an API using a PUT request.
4. Delete an entry from an API using a DELETE request.
5. Format the JSON output of an API response using `jq`.
6. Use cURL to send a PATCH request to partially update an entry.
7. Inspect the headers of an API response using cURL.
8. Authenticate an API request using a session cookie.
9. Use browser DevTools to inspect API requests made by a webpage.
10. Compare the results of GET, POST, PUT, and DELETE requests on an API.

---

## Web Applications vs. Websites

### Questions
1. What are the key differences between Web 1.0 and Web 2.0?
2. How do web applications provide more functionality than traditional websites?
3. What does it mean for a web application to be modular?
4. How do web applications handle different display sizes and platforms?
5. What are the advantages of web applications over native OS applications?
6. What are the limitations of web applications compared to native OS applications?
7. How do hybrid and progressive web applications bridge the gap between web and native applications?
8. What are some common open-source web applications?
9. Name three proprietary web applications and their primary uses.
10. How does version unity benefit web applications?

### Practical Exercises
1. Compare the source code of a static website with that of a dynamic web application.
2. Modify a static website to include dynamic content using JavaScript.
3. Test the responsiveness of a web application on different devices and screen sizes.
4. Set up a local instance of Joomla and explore its features.
5. Install and configure a Wix or Shopify account to create a simple online store.
6. Explore the differences between a native OS application and a web application by comparing similar functionalities.
7. Develop a simple hybrid web application using a modern framework like React Native.
8. Analyze the performance of a web application on different browsers.
9. Document the process of setting up a local development environment for a web application.
10. Evaluate the pros and cons of using open-source vs. proprietary web applications.

---

## Security Risks of Web Applications

### Questions
1. What are some common security risks associated with web applications?
2. How do automated tools contribute to web application vulnerabilities?
3. What is the impact of a successful web application attack?
4. How can web applications be secured against common vulnerabilities?
5. What role does secure coding play in web application security?
6. How can organizations mitigate the risks of web application attacks?
7. What are some real-world examples of web application attacks?
8. How does the complexity of web applications affect their security?
9. What are the implications of hosting sensitive data on web servers?
10. How can regular security audits improve web application security?

### Practical Exercises
1. Perform a vulnerability scan on a test web application using a tool like Nikto.
2. Exploit a known vulnerability in a test environment to understand its impact.
3. Implement input validation on a simple web form to prevent SQL injection.
4. Use a web application firewall (WAF) to protect a test application.
5. Analyze the logs of a web server to identify potential security threats.
6. Conduct a code review of a web application to identify security flaws.
7. Simulate a password spraying attack on a test web application.
8. Document the process of securing a web application against common vulnerabilities.
9. Evaluate the effectiveness of different security measures in a test environment.
10. Develop a security policy for a web application and implement it.