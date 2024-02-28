# Authenticated XSS via Media Files

### Severity: Medium

## Issue Description

WordPress versions prior to 5.4.2 were vulnerable to an authenticated Cross-Site Scripting (XSS) attack via media files. This vulnerability allowed authenticated users, with specific privileges such as Contributor or Author, to upload malicious media files containing JavaScript code. When these files were viewed in the media library, or embedded in posts or pages, the JavaScript code would execute in the context of the user viewing the file, potentially leading to unauthorized actions or data theft.


## Risk Rating

- Severity: Medium

- Difficulty to Exploit: Easy

- Authentication: No


## Affected URLs/Area

http://43.205.237.12:31337/wp-admin/upload.php


## Steps to Reproduce/PoC

1. Log in to WordPress dashboard.
2.  Go to Media > Add New.
<a href="https://ibb.co/sW5W4Yy"><img src="https://i.ibb.co/g4v48Kz/image.png" alt="image" border="0"></a>

3. Create a new media file  by uploading an image or video. 
4. Insert malicious JavaScript into the Title or Description field
5. Click View attachment page
<a href="https://ibb.co/vm54fMR"><img src="https://i.ibb.co/hH5FrTw/image.png" alt="image" border="0"></a>

6. View the media file in a web browser. 
7. Notice the XSS alert triggered when the file is loaded, such as an alert box displaying the user's cookie

    <a href="https://ibb.co/rs8KXTG"><img src="https://i.ibb.co/QdS7xzF/image.png" alt="image" border="0"></a>




## Affected Demograpic


The CVE-2020-4047 vulnerability affects users of WordPress versions prior to 5.4.2. Specifically, it impacts authenticated users who have the ability to upload media files to the WordPress site, such as Contributors, Authors, Editors, or Administrators. In other words, it affects users who have been granted permission to upload media content to the WordPress media library.

Notably, this vulnerability requires authentication, meaning that an attacker must have valid credentials to access the WordPress site. Therefore, it doesn't affect anonymous or unauthenticated users who do not have login credentials for the WordPress site.

The issue occurs due to a lack of proper validation and sanitization of media files uploaded to the WordPress media library. Attackers could exploit this vulnerability by uploading specially crafted media files containing malicious JavaScript code. When these files are viewed in the media library or embedded in posts or pages by other users (including administrators), the JavaScript code would execute within the context of the user viewing the file, potentially leading to unauthorized actions or data theft.

  
## Recommended Fix

 **Update the WordPress  to version 5.4.2 or later**.
 

 

## References


- [1] https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-4047/
