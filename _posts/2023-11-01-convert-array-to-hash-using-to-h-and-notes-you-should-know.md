---
title: Convert Array to Hash using `to_h` method and notes you should know
date: 2023-11-01 17:00:00 +0700
categories: [Programming]
tags: [Ruby on Rails]
---

Đối với Rubyist, dev Ruby, khi nhắc đến việc chuyển 1 array sang hash thì sẽ nghĩ ngay đến method `to_h`. Tuy nhiên, có 1 vài lưu ý khi sử dụng method này mà đôi khi bản thân tôi cũng quên luôn. Và `tôi quên nó và bạn đừng như tôi` =)))
<!--more-->

## 1. Method `to_h` dùng làm gì?
Theo document: https://ruby-doc.org/3.2.2/Enumerable.html#method-i-to_h
>`to_h → hash`
`to_h {|element| ... } → hash`

> When  `self`  consists of 2-element arrays, returns a hash each of whose entries is the key-value pair formed from one of those arrays:
`[[:foo, 0], [:bar, 1], [:baz, 2]].to_h # => {:foo=>0, :bar=>1, :baz=>2}`

>When a block is given, the block is called with each element of  `self`; the block should return a 2-element array which becomes a key-value pair in the returned hash:
`(0..3).to_h {|i| [i, i ** 2]} # => {0=>0, 1=>1, 2=>4, 3=>9}`

>Raises an exception if an element of  `self`  is not a 2-element array, and a block is not passed.

## 2. Một số lưu ý
- Để chuyển đổi array thành hash thì yêu cầu **mỗi phần tử trong array phải là 1 sub-array có 2 phần tử**. Nếu không, chúng ta sẽ gặp cái dòng này :)))
>in `to_h`: wrong element type .... at 0 (expected array) (TypeError)

Ví dụ:
```ruby
[:foo, 0, :bar, 1, :baz, 2].to_h
#=> in `to_h': wrong element type Symbol at 0 (expected array) (TypeError)
```
Vậy phải giải quyết như thế nào? Dùng method `each_slice(2)` chuyển array trên về dạng array có cấu trúc mảng trong mảng như ví dụ trong document.
```ruby
[:foo, 0, :bar, 1, :baz, 2].each_slice(2).to_h
=> {:foo=>0, :bar=>1, :baz=>2}
```
- **Method `to_h` có thể dùng block** để thực hiện những sự chuyển đổi phức tạp hơn nếu muốn (như ví dụ trong document). Ví dụ :
```ruby
require 'uri'
url = "https://www.example.com/search?query=ruby+programming&sort=recent"

# ta có query string được lấy từ url
query_string = URI.parse(url).query
=> "query=ruby+programming&sort=recent"

# Giờ chúng ta sẽ chuyển đổi string này thành hash cho đẹp nhé ;))
query_string.split(/[=&]/).each_slice(2).to_h do |key, value|
	# 1000 dòng code xử lý gì đó
	[key.to_sym, value]
end
=> {:query=>"ruby+programming", :sort=>"recent"}
```
Vẫn là sử dụng `each_slice` để chuyển array về đúng cấu trúc được yêu cầu, ta dùng `to_h` với block để xử lý thêm 1 thao tác đơn giản bên trong. Bạn có thể xử lý bất kỳ thứ gì phức tạp bên trong block cũng được, **miễn là trả về 1 array với 2 element bên trong là được** `[key, value]`

- Còn vài phương pháp khác và cả những lưu ý khi convert array sang hash. Các bạn có thể đọc thêm ở đây: https://stackoverflow.com/questions/39567/what-is-the-best-way-to-convert-an-array-to-a-hash-in-ruby
___
*“When you give joy to other people, you get more joy in return. You should give a good thought to happiness that you can give out.”— Eleanor Roosevelt*{: .text-center.text-success}
