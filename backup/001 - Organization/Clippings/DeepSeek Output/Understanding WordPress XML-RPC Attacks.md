---
title: "DeepSeek"
source: "https://chat.deepseek.com/a/chat/s/c6d42efb-4a48-4468-83ba-27a6eac9c94b"
author:
published:
created: 2025-01-18
description: "Chat with DeepSeek AI – your intelligent assistant for coding, content creation, file reading, and more. Upload documents, engage in long-context conversations, and get expert help in AI, natural language processing, and beyond. | 深度求索（DeepSeek）助力编程代码开发、创意写作、文件处理等任务，支持文件上传及长文本对话，随时为您提供高效的AI支持。"
tags:
  - "clippings"
---
WordPress XML-RPC attacks refer to exploitation attempts targeting the XML-RPC functionality in WordPress. XML-RPC is a remote procedure call (RPC) protocol that enables external applications to interact with WordPress. While it can be useful for legitimate purposes, such as enabling remote publishing or mobile app integration, it can also be abused by attackers to carry out malicious activities.

### Common XML-RPC Attacks

1. **Brute Force Attacks**: Attackers use the `system.multicall` method to attempt multiple login attempts in a single request, making it easier to brute force credentials.
2. **DDoS Amplification**: Attackers can use the `pingback.ping` method to initiate Distributed Denial of Service (DDoS) attacks by spoofing the source IP and targeting other websites.
3. **Remote Code Execution**: Vulnerabilities in XML-RPC implementations can sometimes allow attackers to execute arbitrary code on the server.
4. **Spam and Content Injection**: Attackers may use XML-RPC to inject spam content or malicious links into posts or comments.

### Executing All Method Calls

To execute all available XML-RPC method calls, you would typically need to interact with the XML-RPC endpoint (`/xmlrpc.php`) programmatically. However, doing so without proper authorization is illegal and unethical. Below is an explanation of how XML-RPC works and how you can interact with it **legitimately** for testing or development purposes.

#### Legitimate Use of XML-RPC

If you have permission to test or interact with a WordPress site, you can use tools like `curl` or libraries in programming languages (e.g., Python, PHP) to send XML-RPC requests.

1. **Discover Available Methods**:  
You can retrieve a list of available methods by sending a request to the XML-RPC endpoint:

```
<methodCall>
    <methodName>system.listMethods</methodName>
    <params></params>
</methodCall>
```
2. **Execute Specific Methods**:  
Once you know the available methods, you can execute them by sending the appropriate XML-RPC request. For example, to publish a post:

```
<methodCall>
    <methodName>wp.newPost</methodName>
    <params>
        <param><value><int>1</int></value></param> 
        <param><value><string>username</string></value></param> 
        <param><value><string>password</string></value></param> 
        <param>
            <value>
                <struct>
                    <member>
                        <name>post_title</name>
                        <value><string>Test Post</string></value>
                    </member>
                    <member>
                        <name>post_content</name>
                        <value><string>This is a test post.</string></value>
                    </member>
                    <member>
                        <name>post_status</name>
                        <value><string>publish</string></value>
                    </member>
                </struct>
            </value>
        </param>
    </params>
</methodCall>
```
3. **Using a Library**:  
In Python, you can use the `xmlrpc.client` library to interact with XML-RPC:

```
import xmlrpc.client

url = 'https://example.com/xmlrpc.php'
username = 'your_username'
password = 'your_password'

server = xmlrpc.client.ServerProxy(url)
methods = server.system.listMethods()
print(methods)

post = {
    'post_title': 'Test Post',
    'post_content': 'This is a test post.',
    'post_status': 'publish'
}
post_id = server.wp.newPost(1, username, password, post)
print(f'Post created with ID: {post_id}')
```

### Protecting Against XML-RPC Attacks

If you don't need XML-RPC functionality, it's best to disable it to reduce the attack surface. You can do this by adding the following code to your theme's `functions.php` file or using a security plugin:

```
add_filter('xmlrpc_enabled', '__return_false');
```

Alternatively, you can block access to `xmlrpc.php` via your `.htaccess` file (for Apache servers):

```
<Files xmlrpc.php>
    Order Allow,Deny
    Deny from all
</Files>
```

For Nginx servers, you can add the following to your server configuration:

```
location = /xmlrpc.php {
    deny all;
}
```

### Conclusion

XML-RPC attacks are a serious security concern for WordPress sites. While it’s possible to interact with XML-RPC programmatically, doing so without authorization is illegal. Always ensure you have permission before testing or interacting with a site's XML-RPC interface, and take steps to secure your site if XML-RPC is not needed.

The number of XML-RPC methods available in WordPress depends on the version of WordPress, the plugins installed, and the theme being used. By default, WordPress core provides a set of XML-RPC methods, but plugins and themes can add their own methods. Here's a breakdown:

---

### **Default WordPress XML-RPC Methods**

WordPress core provides a variety of XML-RPC methods for managing content, users, comments, and more. These methods are grouped into different APIs, such as:

1. **System Methods**:
    
    - `system.listMethods`: Lists all available methods.
        
    - `system.methodHelp`: Provides documentation for a specific method.
        
    - `system.methodSignature`: Describes the parameters and return type of a method.
        
    - `system.multicall`: Allows multiple method calls in a single request.
        
2. **Post Methods**:
    
    - `wp.getPosts`: Retrieves a list of posts.
        
    - `wp.getPost`: Retrieves a specific post.
        
    - `wp.newPost`: Creates a new post.
        
    - `wp.editPost`: Edits an existing post.
        
    - `wp.deletePost`: Deletes a post.
        
3. **Taxonomy Methods**:
    
    - `wp.getTaxonomies`: Retrieves a list of taxonomies.
        
    - `wp.getTerms`: Retrieves terms for a taxonomy.
        
    - `wp.getTerm`: Retrieves a specific term.
        
    - `wp.newTerm`: Creates a new term.
        
    - `wp.editTerm`: Edits an existing term.
        
    - `wp.deleteTerm`: Deletes a term.
        
4. **Media Methods**:
    
    - `wp.uploadFile`: Uploads a file to the media library.
        
5. **Comment Methods**:
    
    - `wp.getComments`: Retrieves a list of comments.
        
    - `wp.getComment`: Retrieves a specific comment.
        
    - `wp.newComment`: Creates a new comment.
        
    - `wp.editComment`: Edits an existing comment.
        
    - `wp.deleteComment`: Deletes a comment.
        
6. **User Methods**:
    
    - `wp.getUsers`: Retrieves a list of users.
        
    - `wp.getUser`: Retrieves a specific user.
        
    - `wp.getProfile`: Retrieves the current user's profile.
        
    - `wp.editProfile`: Edits the current user's profile.
        
7. **Options Methods**:
    
    - `wp.getOptions`: Retrieves site options.
        
    - `wp.setOptions`: Updates site options.
        
8. **Pingback Methods**:
    
    - `pingback.ping`: Notifies a site that it has been linked to.
        
    - `pingback.extensions.getPingbacks`: Retrieves pingbacks for a post.
        

---
### **Total Number of Default Methods**

In a default WordPress installation, there are approximately **40-50 XML-RPC methods** available. However, this number can vary slightly depending on the WordPress version.

---
### **Additional Methods from Plugins and Themes**

Plugins and themes can extend the XML-RPC API by adding their own methods. For example:

- **WooCommerce**: Adds methods for managing products, orders, and customers.
- **Jetpack**: Adds methods for remote management and synchronization.
- **Custom Plugins/Themes**: Developers can register custom XML-RPC methods using the `xmlrpc_methods` filters

The total number of methods can increase significantly depending on the plugins and themes installed. For example, a site with WooCommerce and Jetpack might have **100+ XML-RPC methods**.

---
### **How to List All Methods**

To get a complete list of all available XML-RPC methods for a specific WordPress site, you can use the `system.listMethods` method. Here’s an example using Python:

```
url = 'https://example.com/xmlrpc.php'
server = xmlrpc.client.ServerProxy(url)
```

# List all available methods
```python
methods = server.system.listMethods()
print(f"Total methods: {len(methods)}")
print(methods)
```

This will return an array of all available methods, including those added by plugins and themes.

---
### **Summary**

- **Default WordPress**: ~40-50 methods.
- **With Plugins/Themes**: Can exceed 100+ methods.
- Use `system.listMethods` to get the exact count and list of methods for a specific site.

If you’re working with XML-RPC, always ensure you have proper authorization and understand the implications of each method call.