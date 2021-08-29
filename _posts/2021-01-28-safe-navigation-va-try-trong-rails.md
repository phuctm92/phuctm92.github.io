---
title: Safe Navigation (&.) và Try trong Rails
description: "Chắc hẳn khi làm việc với Rails, để gọi method của object mà không cần sợ object đó có nil hay không hoặc để handle lỗi 'NoMethodError: undefined method for nil:NilClass'"
date: 2021-01-28 19:00:00 +0700
categories: [Programming]
tags: [Ruby on Rails]
---

Chắc hẳn khi làm việc với Rails, để gọi method của object mà không cần sợ object đó có nil hay không hoặc để handle lỗi `NoMethodError: undefined method for nil:NilClass`, 1 trong top những lỗi kinh điển nhất của Rails, chúng ta thường sẽ nghĩ tới method `try` hay `Safe Navigation Operator (&.)` như 1 cách để giải quyết vấn đề.
<!--more-->
Ví dụ:

```ruby
post = nil
post.title # => NoMethodError: undefined method `title' for nil:NilClass
post.try(:title) # => nil
post&.title # => nil
```
Nhìn có vẻ giống nhau nhưng sẽ có 1 chút khác biệt đó

## So sánh
### 1. `&.`  cơ bản thì ngắn hơn  `try` =)))
Code ngắn, dễ đọc :v

### 2. `&.` của Ruby, `try` của Rails
Method `try` không phải là method trong Ruby core mà là method từ [activesupport](https://edgeguides.rubyonrails.org/active_support_core_extensions.html#try). Do đó khi không code trong Rails app (ví dụ viết script tương tự Bash) thì `try` không sử dụng được.

### 3. `&.`  dễ debug hơn
Giả sử mình gọi 1 method nào đó không tồn tại trong app.
```ruby
'foo'&.non_existent # => NoMethodError: undefined method `non_existent' for "foo":String
'foo'.try(:non_existent) # => nil
```
** Tương tự nếu object là `false`

Chỉ khi object đó là `nil` thì 2 thằng này giống nhau thôi.
```ruby
nil&.non_existent # => nil
nil.try(:non_existent) # => nil
```
Tưởng tượng là mình vừa đổi tên method từ `abc` => `non_existent` nhưng mình lại quên nó đi thì `&.` sẽ đóng vai trò là 1 người cứu tinh giúp bạn bớt bạc tóc để khỏi tìm xem tại sao lại có exception. Trái lại, `try` sẽ xoa dịu cơn đau đầu bằng kết quả trả về là `nil` và bạn sẽ nghĩ là `code trông ổn đó, không bug`.
Vậy thì dùng `&.` ổn hơn chứ nhờ.

### 4. `&.` nhanh hơn `try`
Theo kết quả lượm nhặt được từ bài gốc:
```ruby
require 'active_support/all'
require 'benchmark'

foo = nil
puts Benchmark.measure { 10_000_000.times { foo.try(:lala) } }
puts Benchmark.measure { 10_000_000.times { foo&.lala } }
```
Output

```ruby
  1.310000   0.000000   1.310000 (  1.311835)
  0.360000   0.000000   0.360000 (  0.353127)
```
=> `&.` nhanh hơn `try` gần 4 lần.

## Tóm lại
- `try` nên được dùng khi bạn không đảm bảo method được gọi có tồn tại hay không
- `&.` nên được dùng khi bạn không đảm bảo object có bị nil hay không
- `try` có thể sử dụng thay thế cho `&.`
```ruby
post = nil
post.title       # => NoMethodError: undefined method `title' for nil:NilClass
post&.title      # => nil
post.try(:title) # => nil
```
- `&.` không thể sử dụng thay thế cho `try`
```ruby
post = Post.first # => <Post:0x00000000060a46e0 id: nil, title: "Ahihi">
post.title        # => "Ahihi"
post.content       # => NoMethodError: undefined method `content' for #<Post>
post.try(:content) # => nil
post&.content      # NoMethodError: undefined method `content' for #<Person>
```

## Reference

 1. [https://stackoverflow.com/questions/37977721/why-is-safe-navigation-better-than-using-try-in-rails](https://stackoverflow.com/questions/37977721/why-is-safe-navigation-better-than-using-try-in-rails){:target="_blank"}
 2. [https://jetrockets.pro/blog/ats3ic6xvx-safe-navigation-vs-try-in-rails-part-1-basic-differences](https://jetrockets.pro/blog/ats3ic6xvx-safe-navigation-vs-try-in-rails-part-1-basic-differences){:target="_blank"}
