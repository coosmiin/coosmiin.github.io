---
title: "TL;DR; Don't care, just fix it"
date: 2020-04-17 +0200
last_modified_at: 2020-10-29 +0200
categories: ssh npm
toc: true
toc_label: Topics
toc_icon: quote-right
toc_sticky: true
---

You are in the flow, you are on track, you do stuff that matters (to you) and then something happens that ruins it. Now you have to fix that "other" thing first before you can continue. It might be interesting to get into details, but you just don't care - you can't know everything. Worse, maybe it happened before and you don't remember how you fixed it back then. You wonder why you haven't type few hints about it in a blog post. Here it is..

### Unable to negotiate with somehost.com port 22: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1,diffie-hellman-group14-sha1

You were trying to do a git operation (that involved a remote connection). The fix: add the following lines to your Git `ssh_config` file (`c:\Program Files\Git\etc\ssh\`) as described in the [OpenSSH Legacy Options](https://www.openssh.com/legacy.html).
```
Host somehost.com
	KexAlgorithms +diffie-hellman-group1-sha1,diffie-hellman-group14-sha1
```

Apparently Git for Windows (starting with version 2.25.1) includes updates to ssh that disable the SHA1 based cryptography suites. If your git server still uses it you have to apply the above workaround. If you're using Azure DevOps Server [this should be fixed](https://developercommunity.visualstudio.com/content/problem/921226/git-ssh-access-offers-weak-algorithms.html) starting from the April 2020 patch.

### npm ERR! code UNABLE_TO_VERIFY_LEAF_SIGNATURE

You're doing a clean install of your dependencies by running `npm ci` and you get this: 

> npm ERR! code UNABLE_TO_VERIFY_LEAF_SIGNATURE
> npm ERR! request to ... failed, reason: unable to verify the first certificate

You're left shoulder angel tells you that you trust the source and you can get rid of it by just disabling the `strict-ssl` check. Do it at your own risk:
```
npm config set strict-ssl false
```
