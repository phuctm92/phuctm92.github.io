---
title: .gitignore and database.yml in Rails
date: 2023-02-08 21:30:00 +0700
categories: [Programming]
tags: [Ruby on Rails, Git]
---
Untrack database.yml file by adding it to .gitignore
<!--more-->

## How to
Case 1: **database.yml** file wasn't already committed

```bash
$ echo config/database.yml >> .gitignore
$ mv config/database.yml config/database.yml.example
$ git add .
$ git commit -am "put database.yml to .gitignore and and rename"
$ cp config/database.yml.example config/database.yml
```

Case 2: **database.yml** file was already committed. After tell `.gitignore` the changes, run the following command and then commit

```bash
git rm --cached config/database.yml
```

## References
- [https://stackoverflow.com/a/33484222/3123549](https://stackoverflow.com/a/33484222/3123549){:target="_blank"}

___
*“When you give joy to other people, you get more joy in return. You should give a good thought to happiness that you can give out.”— Eleanor Roosevelt*{: .text-center.text-success}
