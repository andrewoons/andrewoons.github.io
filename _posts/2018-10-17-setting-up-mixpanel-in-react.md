---
layout: post
title: 'Setting up Mixpanel in React'
date: 2018-10-17 14:33:00 +0100
categories: how-to
---

<img src="https://cdn-images-1.medium.com/max/800/0*NZwJjQNjqjx_bM6D" />

At the time of writing there is no simple tutorial on how to integrate and use Mixpanel in React.

I found [react-mixpanel](https://github.com/neciu/react-mixpanel), which uses React’s context API. However, using that requires you to pass the Mixpanel Consumer to props if you want to call Mixpanel out of render, which pollutes the code a bit too much for my liking. More importantly, you have to do a dev/prod check every time you track something.

What I ended up doing is much simpler, without having to worry about forgetting dev checks when calling `track` or `identify`.

We are going to be using Mixpanel’s official `mixpanel-browser` library and a small wrapper function.

## Step 1: Install mixpanel-browser

Run `npm install mixpanel-browser --save` in your project folder.

## Step 2: Create Mixpanel wrapper function

This wrapper function is what we’ll include in all our components if we want to call Mixpanel, e.g. during the onboarding process, when users are logging in and so on.

It doesn’t really matter where you place this, as long as it makes sense for your project structure. Here it is:

{% gist f234e9d8cd203a07c41e1f66dd87ac21 Mixpanel.js %}

First, we are importing `mixpanel-browser` and initiating mixpanel by calling `init` with our token. Replace this token with your own token that you get from Mixpanel.

Next, we have a simple check called `env_check`. This simply checks if the environment we are running in, is the one we want. You probably only want to be tracking things in production.

_Note: You can also change this to your own env variable, such as `MIXPANEL_ACTIVE`._

Then we have the actions object which is the wrapper around the Mixpanel actions. It just checks if `env_check` returns true, and if so, calls the Mixpanel function with the same parameters.

This little wrapper makes sure you don’t have to worry about calling Mixpanel in development and polluting your data, as `env_check` won’t pass.

_Note: you can add other Mixpanel functions in there, such as opting out of data tracking_

## Step 3: Use it!

In every file or component you want to track something, include the file once:

`import { Mixpanel } from './Mixpanel';`

Now you can use it like you normally would. Example:

{% gist a9ec35c535d157bc5d3b526d975dd1a2 Example.js %}

Hope it helps!
