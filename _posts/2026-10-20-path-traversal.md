---
title: "Path Traversal Explained Simply"
date: 2026-10-20 00:00:00 +0800
categories: [Web Exploitation]
tags: [Web]
---

Imagine a website that loads an image with url like ```image?file=cat.png```. Now you change the value "cat.png" to something like ../../../etc/passwd and instead of the image you see a system file rendered on your screen, this is path traversal. In this post, I'll explain how it works and how to stop it.

## What is Path Traversal?

Path Traversal also known as directory traversal, attackers can use this vulnerability to access arbitrary files on your system if not handled properly.

## Lab Walkthrough: File path traversal

You can access the lab [here](https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/path-traversal-apprentice/file-path-traversal/lab-simple#)

Ok so first thing we see after opening the website is a shop with various items listed. 

![](/assets/lib/path_traversal_1.png)

So the only clickable links are the "View details" buttons. After clicking the button we see that it does render the image on a new page. So we'll have to analyze the request itself to see what's happening behind the scenes. For our purpose we'll use Burpsuite.

![](/assets/lib/path_traversal_2.png)

As we can see, clicking the button sends a GET request for a file, let's try changing the file name.

![](/assets/lib/path_traversal_3.png)

Let's forward the request.

![](/assets/lib/path_traversal_4.png)

On page, it says that the lab is solved successfully! However we would want to see the response we are getting right. So instead of just forwarding the request, we'll send it to Burp Repeater and from there we will modify and send different payloads.

![](/assets/lib/path_traversal_5.png)

And on Burp Repeater we do see the contents of the file we requested for.

## Why it happens

This happens primarily because the server blindly accepts inputs from the frontend. There is no way to validate that either the file that is being requested is allowed to be sent or not. Another reason is lack of input sanitisation. Characters like "/" shouldn't be allowed in file names.

## How to fix it

The best fix is to use ids instead of fixed paths, like ```image?id=7``` and the server looks up the real file itself. Another good fix is to resolve the full path first and then confirm if it still starts with the allowed folder.


