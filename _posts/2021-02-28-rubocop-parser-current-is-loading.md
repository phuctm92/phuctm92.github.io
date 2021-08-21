---
title: Rubocop - Suppress warning parse/current is loading
date: 2021-02-28 00:00:00 +0700
categories: [Programming, TIL]
tags: [Ruby on Rails]
---
`
warning: parser/current is loading parser/ruby2x, which recognizes
warning: 2.a-compliant syntax, but you are running 2.b.
`
<!--more-->
## Detail
[https://github.com/whitequark/parser#compatibility-with-ruby-mri](https://github.com/whitequark/parser#compatibility-with-ruby-mri){:target="_blank"}

>Unfortunately, Ruby MRI often changes syntax in patchlevel versions. This has happened, at least, for every release since 1.9; for example, commits  [c5013452](https://github.com/ruby/ruby/commit/c501345218dc5fb0fae90d56a0c6fd19d38df5bb)  and  [04bb9d6b](https://github.com/ruby/ruby/commit/04bb9d6b75a55d4000700769eead5a5cb942c25b)  were backported all the way from HEAD to 1.9. Moreover, there is no simple way to track these changes.

>This policy makes it all but impossible to make Parser precisely compatible with the Ruby MRI parser. Indeed, at September 2014, it would be necessary to maintain and update ten different parsers together with their lexer quirks in order to be able to emulate any given released Ruby MRI version.

>As a result, Parser chooses a different path: the  `parser/rubyXY`  parsers recognize the syntax of the latest minor version of Ruby MRI X.Y at the time of the gem release.

## Solution

1. Run Rubocop as `ruby -W0 -S rubocop filename`

2. Install [gem warning](https://github.com/jeremyevans/ruby-warning) and config as:
```ruby
# config/initializers/warning_ignores.rb
### https://github.com/jeremyevans/ruby-warning
Warning.ignore(/warning: parser/)
```
3. If you use **VS Code** as code editor and install `ruby-rubocop` extension. Go to its **extension settings** and check the checkbox
```
Ruby > Rubocop:Suppress Rubocop Warnings
```

## Reference
- [https://github.com/rubocop/rubocop/issues/1819](https://github.com/rubocop/rubocop/issues/1819){:target="_blank"}
