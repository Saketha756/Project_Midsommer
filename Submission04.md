# SQL Injection via WP_Query

### Severity: High

## Issue Description

Due to improper sanitization in WP_Query, there can be cases where SQL injection is possible through plugins or themes that use it in a certain way.


## Risk Rating

- Severity: High

- Difficulty to Exploit: Medium

- Authentication: No


## Affected URLs/Area

http://43.205.237.12:31337/wp-admin/theme-editor.php?file=functions.php&theme=twentytwenty


## Steps to Reproduce/PoC

1. Create a new WordPress theme and add the following PHP code to its `functions.php` file

   

>  phpfunction vulnerable_wp_query() {
>            $query_args = array('post_type' => $_GET['post_type']);
>            $wp_query = new WP_Query($query_args);
>        }
>        add_action('init', 'vulnerable_wp_query');


<a href="https://ibb.co/xJbhgBv"><img src="https://i.ibb.co/WgXnzM9/image.png" alt="image" border="0"></a><br /><a target='_blank' href='https://usefulwebtool.com/convert-lower-upper-case'></a><br />


2.  Activate the newly created theme on WordPress website.

3.  Open a web browser and navigate to the following URL

  
> `http://43.205.237.12:31337/?post_type=%27+or+1=1+--+`
> 
> This payload leverages an SQL injection technique to bypass the
> sanitization of the `post_type` parameter.

4. When you visit the URL, the vulnerable `WP_Query` code will execute the crafted SQL payload.

<a href="https://ibb.co/vBQYBS1"><img src="https://i.ibb.co/PY9QYdx/Screenshot-2024-02-28-105541.png" alt="Screenshot-2024-02-28-105541" border="0"></a><br /><a target='_blank' href='https://usefulwebtool.com/convert-lower-upper-case'></a><br />


## Affected Demograpic


This issue affects anyone who visits the WordPress website where the vulnerable theme is active. Specifically, it affects users who interact with URLs that include parameters utilized by the vulnerable code. Since the vulnerability lies within the theme's `functions.php` file, any user who accesses the website and manipulates the URL parameters can potentially exploit the vulnerability.

It can affect anyone who interacts with the website and knows how to craft the malicious URL. However, it's more likely to be exploited by users with malicious intent or those with knowledge of SQL injection techniques. Ordinary visitors may not intentionally exploit the vulnerability unless they stumble upon it accidentally or are guided by malicious actors.

The vulnerability occurs due to insufficient input validation and sanitization in the WordPress theme's code. Specifically, the `$_GET['post_type']` parameter is directly used in constructing an SQL query without proper validation or sanitization. This allows an attacker to inject arbitrary SQL code into the query through the URL parameter.

When a user visits the crafted URL with the SQL injection payload, such as `example.com/?post_type=%27+or+1=1+--`, the injected SQL code manipulates the behavior of the query. In this case, the payload `or 1=1` always evaluates to true, effectively bypassing any condition imposed on the query. As a result, the query retrieves all blog posts from the database, regardless of their post type, which exposes sensitive information and potentially compromises the security of the website.

  
## Recommended Fix

Update to one of the following versions, or a newer patched version: 3.7.37, 3.8.37, 3.9.35, 4.0.34, 4.1.34, 4.2.31, 4.3.27, 4.4.26, 4.5.25, 4.6.22, 4.7.22, 4.8.18, 4.9.19, 5.0.15, 5.1.12, 5.2.14, 5.3.11, 5.4.9, 5.5.8, 5.6.7, 5.7.5, 5.8.3
 

 

## References


- [1] https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-21661/
