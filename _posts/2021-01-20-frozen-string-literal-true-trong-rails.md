---
title: Frozen_string_literal:true trong Rails
date: 2021-01-20 14:00:00 +0700
categories: [Programming, TIL]
tags: [Ruby on Rails]
---

Khi dùng rubocop trong Rails, chúng ta thường bị bắt lỗi `# frozen_string_literal: true`. Vậy `frozen_string_literal` dùng để làm gì?

## Frozen_string_literal là gì ?
`# frozen_string_literal: true` là 1 trong những magic comments được support từ **ruby 2.3** dùng để cải thiện performance bằng việc **chỉ cấp 1 vùng nhớ dựa vào nội dung của mỗi chuỗi**, nghĩa là với những chuỗi có nội dung giống nhau thì sẽ chỉ thuộc về 1 vùng nhớ , tương tự với **Symbol**. Bằng cách thông báo với Ruby rằng bạn đã "*freeze string literal (string object)*" thì Ruby sẽ **không để cho bất cứ thứ gì có thể chỉnh sửa chuỗi ký tự đó.**

## Demo
### Frozen_string_literal: true

 - Cấp 1 vùng nhớ dựa vào nội dung của mỗi chuỗi

```ruby
# frozen_string_literal: true
p 'key'.object_id # => 70306598556120
p 'key'.object_id # => 70306598556120

a  =  'hello'; p  a.object_id # => 47326081372960
b  =  'hello'; p  b.object_id # => 47326081372960
```

 - Ngăn chặn việc thay đổi chuỗi kí tự

```ruby
# frozen_string_literal: true
str  =  'hello'
str  <<  ' world'
puts  str  #=> `<main>': can't modify frozen String (FrozenError)
```

### Frozen_string_literal: false

 - Luôn cấp vùng nhớ mới cho mỗi string


```ruby
# frozen_string_literal: false
p  'key'.object_id  # => 47452453679760
p  'key'.object_id  # => 47452453679620

a  =  'hello'; p  a.object_id  # => 47452453679540
b  =  'hello'; p  b.object_id  # => 47452453679520
```


 - Có thể thay đổi chuỗi


```ruby
# frozen_string_literal: false
str  =  'hello'
str  <<  ' world'
puts  str  # => hello world
```

**Note**:
Nhưng nếu dùng `# frozen_string_literal: true` mà vẫn muốn thay đổi được thì hãy dùng hàm **dup**. Ví dụ:

```ruby
# frozen_string_literal: true
p  'key'.object_id  # => 47452453679760
p  'key'.dup.object_id  # => 47452453679620

a  =  'hello'; p  a.object_id  # => 47452453679540
b  =  'hello'; p  b.dup.object_id  # => 47452453679520
```

## Tổng kết
`frozen_string_literal` làm giảm việc tạo rác (garbage), cải thiện performance.


## Reference

 1. [https://stackoverflow.com/a/55900180](https://stackoverflow.com/a/55900180){:target="_blank"}
 2. [https://www.mikeperham.com/2018/02/28/ruby-optimization-with-one-magic-comment/](https://www.mikeperham.com/2018/02/28/ruby-optimization-with-one-magic-comment/){:target="_blank"}
