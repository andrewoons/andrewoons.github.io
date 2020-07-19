---
layout: post
title: 'How To Make Proxy Requests With Postman (through e.g. QuotaGuard)'
date: 2019-02-08 17:33:00 +0100
categories: how-to
---

In this quick tutorial we’ll make a request to an API through a proxy using Postman.

## Step 1: Get your proxy details

You’ll need a username, password and the IP address. I’m using QuotaGuard, and they provide me with the following string:

`http://[username]:[password]@static.quotaguard.com:9293`

## Step 2: Get base64 encoded auth

Open Postman, and click on the “Authorization” tab. Select “Basic Auth” and enter your username and password.

Then, click “preview request”. It will populate the `Authorization` key in the Headers tab.

Underneath the Authorization key create a new key called `Proxy-Authorization`, and paste the value of the `Authorization` key there. It should look something like this:

<img src="https://miro.medium.com/max/700/1*t_EaQeXQXiWIKhVDSrQzpg.png" />

Next, go back to the “Authorization” tab and put the Authentication mode back to “No Auth”.

## Step 3: Set Up Proxy URL

The last step is setting up the proxy within Postman. To do that, click the wrench icon at the top right and click settings.

Then go to the “Proxy” tab.

Change “Use Global Proxy” to on.

Select the Proxy type (either HTTP or HTTPS) and enter the url and port of your proxy.

For QuotaGuard in our example, it will look like this:

<img src="https://miro.medium.com/max/700/1*cHJsKl1jJH8qcgPqSrC6bA.png" />

That’s it! When you click “Send Request” it should use your proxy.
