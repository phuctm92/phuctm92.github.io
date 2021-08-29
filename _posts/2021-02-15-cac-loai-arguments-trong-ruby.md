---
title: Các loại arguments trong ruby
date: 2021-02-16 17:00:00 +0700
categories: [Programming]
tags: [Ruby on Rails]
---
Các method trong Ruby có thể nhận 0 hoặc nhiều arguments. Những arguments này được triển khai theo nhiều cách khác nhau và có thứ tự ưu tiên của riêng nó.
<!--more-->

## Các loại arguments
### Required argument
Khi gọi method, bạn phải cung cấp đủ số lượng argument tới method, nếu không Ruby sẽ raise exception.

```ruby
Class Person
  def call(name)
	puts "Hello, #{name}"
  end
end

Person.new.call("Phuc dep trai")
# "Hello, Phuc dep trai"

Person.new.call
# ArgumentError (wrong number of arguments (given 0, expected 1))

Person.new.call("Phuc dep trai", "18 tuoi")
# ArgumentError (wrong number of arguments (given 2, expected 1))
```

### Optional argument / Sponge argument / Non-required argument
Bạn vẫn có thể define method với số lượng argument tùy ý bằng cách đặt dấu sao (*) (**splat operator**) trước argument. Dấu * nghĩa là bạn có thể truyền vào số lượng argument bất kỳ hoặc không cần truyền và `(*args)`  được xem như là 1 array các arguments

```ruby
class Person
  def call(*opt_args)
	p opt_args
  end
end

Person.new.call("Phuc dep trai", "18 tuoi")
# => ["Phuc dep trai", "18 tuoi"]

Person.new.call # => []
```

Chúng ta có thể kết hợp required argument với optional argument để tinh chỉnh số lượng argument tùy ý.

```ruby
def call(name, age, *hobbies)
  p name, age, hobbies
end

Person.new.call("Phuc dep trai", 18, "read book", "game")
# "Phuc dep trai"
# 18
# ["read book", "game"]
# => ["Phuc dep trai", 18, ["read book", "game"]]
```

Ngoài **single splat operator** (*), chúng ta có **double splat operator** (**). Cách hoạt động tương tự như single splat operator, là một optional argument và `(**args)` được xem như là 1 hash các arguments.

```ruby
def call(a, b, **opts)
  p a, b, opts
end

call(1, 2, x: 10, y: 100)
# 1
# 2
# {:x=>10, :y=>100}
# => [1, 2, {:x=>10, :y=>100}]
```

### Default-valued argument
Có thể nói argument với default value cũng là 1 dạng optional argument và `c = 1` dưới đây là default-valued argument.
```ruby
def default_arg(a, b, c=1)
  p a,b,c
end

default_arg(1, 2) # => 1, 2, 1
default_arg(1, 2, 3) # => 1, 2, 3
```

### Keyword (named) argument
Loại này khá giống với việc truyền hash vào argument nhưng bắt buộc phải truyền vào khi nó được khai báo mà không có default value. Nếu argument được truyền vào mà thiếu thì ruby sẽ raise exception.

```ruby
def kw_arg(a:, b:)
  p a, b
end

kw_arg(a: 1, b: 2) # => [1, 2]
kw_arg # => ArgumentError (missing keyword: :a, :b)

def kw_arg(a: 1, b: 2)
  p a, b
end

kw_arg # => [1, 2]
kw_arg(a: 10) # => [10, 2]
```

## Thứ tự ưu tiên
Dưới đây là thứ tự của argument nếu bạn muốn kết hợp các loại arguments và có thể tránh lỗi cú pháp.
> **required -> default-valued -> optional -> keyword**

Ví dụ tổng hợp
```ruby
# Required argument: a
# Default-valued argument: b
# Optional arguments: c, f
# Keyword arguments: d, e

def  m(a, b = 100, *c, d: 1, e:, **f )
  p a, b, c, d, e, f
end

m(1, 2, 3, 4, d: 5, e: 6, x: 100, y: 200)
# => [1, 2, [3, 4], 5, 6, {:x=>100, :y=>200}]

m(1, 2, d: 5, e: 6, x: 100, y: 200)
# => [1, 2, [], 5, 6, {:x=>100, :y=>200}]

m(1, d: 5, e: 6, x: 100, y: 200)
# => [1, 100, [], 5, 6, {:x=>100, :y=>200}]

m(1, e: 6, x: 100, y: 200)
# => [1, 100, [], 1, 6, {:x=>100, :y=>200}]

m(1, e: 6)
# => [1, 100, [], 1, 6, {}]
```

Dưới đây là 1 số ví dụ về các loại arguments cũng như thứ tự triển khai của nó.
![sample-ruby-arguments](/assets/img/ruby-arguments.png)

## Lưu ý
 - Không đặt default-valued argument bên phải của optional argument

```ruby
def broken_args(x,*y,z = 100); end
# => syntax error, unexpected '=', expecting ')'
```

Nếu bạn chạy dòng code này thì sẽ thấy báo lỗi syntax hoặc code không hoạt động là vì sai syntax. Giả dụ đoạn code này đúng và bạn test nó: `broken_args(1, 2, 3, 4)`. Bản chất của splat operator `*y` là **lấy tất cả các arguments còn lại**. Do đó, Ruby sẽ không biết là **y = 2, 3, 4 và z = 100** hay là **y = 2, 3 và z = 4**


## Tài liệu tham khảo
- *The Well grounded Rubyist - David A.Black - chapter 2.4*
