# Author+ Stored Cross-Site Scripting

### Severity: Medium

## Issue Description

The plugin does not sanitise and escape some of its settings, which could allow high privilege users such as authors to perform Stored Cross-Site Scripting attacks.


## Risk Rating

- Severity: Medium

- Difficulty to Exploit: Medium

- Authentication: No


## Affected URLs/Area

http://43.205.237.12:31337/wp-admin/post.php


## Steps to Reproduce/PoC

1.  Go to the Posts section and either create a new post or edit an existing one.
    
2.  **Add the Shortcode:** In the post editor, switch to the Text or Code view. Then, add the following shortcode

> [wordpress_file_upload redirect="true"
> redirectlink="javascript:alert(1)"]
<a href="https://ibb.co/fM27ZsZ"><img src="https://i.ibb.co/K6XHBJB/image.png" alt="image" border="0"></a>

3. After adding the shortcode, save or update the post. This will apply the shortcode to the post.

<a href="https://ibb.co/tHSTKDF"><img src="https://i.ibb.co/Fh9L3zC/image.png" alt="image" border="0"></a>


5. Choose any file from your local system to upload. This could be any type of file, as the focus here is on triggering the XSS vulnerability

6. Once the upload completes, if the XSS vulnerability is successfully triggered, you should see a JavaScript alert pop up with the message "1" or any other message you specified in the alert

<a href="https://ibb.co/Yj1Ntjn"><img src="https://i.ibb.co/x5B2M59/image.png" alt="image" border="0"></a>
  
## Affected Demograpic
Stored XSS can potentially affect all users of a vulnerable web application. Any user who accesses the page where the injected script is stored and rendered can be impacted. This includes regular users, administrators, and anyone else interacting with the application

The impact of stored XSS largely depends on the specific vulnerability and how the application is used. In some cases, it might affect only a small subset of users if the malicious script is injected into a less frequently visited page or section of the application. However, in other cases where the script is injected into commonly accessed and critical pages, the impact could be widespread, affecting a large number of users.

Stored XSS vulnerabilities typically arise due to inadequate input validation and output encoding practices in web applications. Here's how it can occur:

1.  **Lack of Input Validation**: If the application allows users to submit arbitrary content (such as comments, messages, or profile information) without properly validating and sanitizing it, attackers can inject malicious scripts.
    
2.  **Failure to Encode Output**: Even if the input is properly validated, if the application fails to encode special characters (such as `<`, `>`, `&`, etc.) when displaying user-generated content, an attacker can inject scripts that will be executed in the browsers of other users.
    
3.  **Insecure Storage**: If the application stores user-generated content in a database or another storage location without proper precautions, an attacker might directly manipulate this storage to insert malicious scripts.
    
4.  **Unsanitized Data Retrieval**: When the application retrieves and displays stored content, if it fails to properly sanitize or escape the content, the injected scripts will be executed.
  

## Recommended Fix

**Update the WordPress File Upload plugin to version 4.23.3 or later**. This update includes a patch that addresses the vulnerability and prevents it from being exploited.

  

## References


- [1] [https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-4811/]()
