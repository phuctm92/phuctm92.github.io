---
title: '[Tip/Trick] How to open a gem source in Ruby/Rails'
date: 2021-08-19 8:00:00 +0700
categories: [Programming]
tags: [Ruby on Rails, Tips/Tricks]
---
Open the source for a gem in your bundle by command: `bundle open [gem]`
<!--more-->
## Description
Implement the following steps:
1. Access to file `~/.bashrc` or `~/.zshrc`, which depend on your shell in terminal.
2. Add one of two lines
  - Sublime text: `export EDITOR='subl -w'`
  - VSCode:       `export EDITOR='code -w'`
3. Logout Ubuntu and then login again
4. Enter project direction and type command in terminal: bundle open [gem].

For example: `bundle open activesupport`

*Let's try and find out new things...*
