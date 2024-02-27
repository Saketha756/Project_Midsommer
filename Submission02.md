# Contributor+ Stored Cross-Site Scripting via Malicious SVG

### Severity: Medium

## Issue Description

The plugin allows users with a role as low as Contributor to configure the upload form in a way that allows uploading of SVG files, which could be then be used for Cross-Site Scripting attacks


## Risk Rating

- Severity: Medium

- Difficulty to Exploit: Medium

- Authentication: No


## Affected URLs/Area

http://43.205.237.12:31337/wp-admin/post.php


## Steps to Reproduce/PoC

1. Create a new post or edit an existing one. This post will be used to demonstrate the file upload functionality.Within the post editor, add the following shortcode

> `[wordpress_file_upload uploadpatterns="*.svg"]`

This shortcode allows users with Contributor privileges or higher to upload SVG files

<a href="https://ibb.co/f1hSnwm"><img src="https://i.ibb.co/1vDndWH/image.png" alt="image" border="0"></a>

2. Preview or update the post to apply the changes

  <a href="https://ibb.co/GxrW5w7"><img src="https://i.ibb.co/6nqHWhY/image.png" alt="image" border="0"></a> 
  


    
    <svg xmlns:svg="http://www.w3.org/2000/svg"><svg:script>alert(/XSS/)</svg:script></svg>
    

> (XSS payload)

3. In the post editor or preview, you should see an option to upload files. Upload the SVG file with XSS payload named `xss.svg` provided in the PoC.


4. After uploading the SVG file, it will be stored in the server's `wp-content/uploads/` directory. 
You can then access the uploaded SVG file directly via its URL, which typically follows the format

  http://43.205.237.12:31337/wp-content/uploads/xss.svg 

5. Visiting this URL will execute the XSS payload contained within the SVG file, triggering the alert box with the message "XSS"

<a href="https://ibb.co/3WhVxd4"><img src="https://i.ibb.co/hH8rG9L/image.png" alt="image" border="0"></a>


## Affected Demograpic

Stored Cross-Site Scripting (XSS) via malicious SVG affects users who interact with web applications or websites that allow user-generated content to be stored and displayed to other users. This issue primarily impacts applications that accept SVG \files uploaded by users, which are subsequently stored and rendered for other users to view.

It doesn't necessarily affect every user on the internet but rather those who visit or use websites or applications susceptible to this vulnerability. The severity of the impact can vary depending on the popularity and usage of the affected website or application. 

This vulnerability can occur when a malicious user uploads an SVG file containing JavaScript code disguised as harmless graphics or animations. Since SVG files can contain executable code, if the application does not properly sanitize and validate user-uploaded SVG files, the malicious code can be stored on the server-side database. When other users view the affected page where the SVG is displayed, their browsers will execute the injected JavaScript code, leading to potential security exploits such as session hijacking, data theft, or further compromise of the affected website or application.

  

## Recommended Fix

 - **Update the WordPress File Upload plugin to version 4.16.4 or later**.
 
 - **Implement File Validation and Sanitization**

## Also This vulnerability can exploit as Content Injection vulnerability
https://wpscan.com/vulnerability/1527ebdb-18bc-4f9d-9c20-8d729a628670/

 

## References


- [1] https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-24960
