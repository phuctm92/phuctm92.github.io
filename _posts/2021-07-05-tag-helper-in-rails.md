---
title: Make code simplier using tag helper in Rails
date: 2021-07-05 8:00:00 +0700
categories: [Programming, TIL]
tags: [Ruby on Rails]
---
`Tag`, a view helper, sometime can make you code simplier.
<!--more-->
## 1. Introduction
New syntax (from Rails 5.1): `tag.<tag name>(optional content, options)`

Old syntax:  `tag(name, options = nil, open = false, escape = true)`

### 1.1 Content
```erb
tag.h1 'All titles fit to print' # => <h1>All titles fit to print</h1>
```
Content can be contained in block:
```erb
<%= tag.p do %>
  The next great American novel starts here.
<% end %>
# => <p>The next great American novel starts here.</p>
```
### 1.2 Options
Use symbol keyed options to add attributes to the generated tag.
```erb
tag.section class: %w( kitties puppies )
# => <section class="kitties puppies"></section>

tag.section id: dom_id(@post)
# => <section id="<generated dom id>"></section>
```
## 2. Example
In Rails view
```erb
<% if current_user? %>
  <div class='user'>
    <%= current_user.name %>
  </div>
<% end %>
```
or by slim template
```slim
- if current_user?
  .user
    = current_user.name
```
instead
```erb
<%= tag.div(current_user.name, class: 'user') if current_user? %>
```

## 3. Reference
1. [Read more at document](https://api.rubyonrails.org/classes/ActionView/Helpers/TagHelper.html#method-i-tag){:target="_blank"}
