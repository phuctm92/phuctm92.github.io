---
title: Shorten long commands by alias in Ubuntu
date: 2023-02-08 21:00:00 +0700
categories: [Programming]
tags: [Ubuntu]
---
Use **alias** in bash for creating short-cuts to commonly run commands
<!--more-->

1. `vim ~/.bashrc`
2. add a line similar to the following to create the alias
```bash
alias j2dir="cd /home/user/this/long/and/annoyingly/deep/directory/workstuff"
```
3. `source ~/.bashrc`
4. Let's try `j2dir`

___
*“Stay away from those people who try to disparage your ambitions. Small minds will always do that, but great minds will give you a feeling that you can become great too.” — Mark Twain*{: .text-center.text-success}
