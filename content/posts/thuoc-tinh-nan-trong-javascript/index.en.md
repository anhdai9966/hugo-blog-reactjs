---
weight: 1
title: "Thuộc tính NaN trong JavaScript là gì?"
date: 2022-10-27T21:29:01+08:00
lastmod: 2022-10-27T21:29:01+08:00
draft: false
author: "Cường Phạm"
authorLink: "https://dillonzq.com"
description: "Discover what the Hugo - LoveIt theme is all about and the core-concepts behind it."
images: []
resources:
  - name: "featured-image"
    src: "featured-image.jpg"

tags: ["javascript", "datatype"]
# categories: ["documentation"]

lightgallery: true

toc:
  auto: false
---

Ở bài viết này, chúng ta sẽ cùng nhau tìm hiểu về thuộc tính NaN trong JavaScript thông qua một …

<!--more-->

## 1.NaN trong JavaScript là gì?

Trong JavaScript, NaN là viết tắt của Not a Number. Nó đại diện cho một giá trị không phải là một số hợp lệ. Nó có thể được sử dụng để kiểm tra xem một số được nhập vào có phải là một số hợp lệ hay không. Để gán một biến cho giá trị NaN, chúng ta có thể sử dụng một trong hai cách sau:

```
let a = NaN
let a = Number.NaN
```

Ví dụ: Trong ví dụ này, chúng ta sẽ sử dụng số NaN của JavaScript.

```
let monthNumber = 14;

if(monthNumber<1||monthNumber>12){
  monthNumber=Number.NaN
  console.log('Month number should be'+'between 1 and 2')
}
else{
  console.log(monthNumber)
}

```

Kết quả :

```
Month number should be between 1 and 2
```

## 2 Ví dụ

### 2.1 Ví dụ 1

Bất cứ khi nào chúng ta cố gắng parse một chuỗi hoặc ‘undefined’ thành một int, nó sẽ trả về NaN.

```
console.log(parseInt("higeeks"));
```

Kết quả:

```
NAN
```

### 2.2 Ví dụ 2

Bất cứ khi nào chúng ta cố gắng tìm căn bậc hai của một số âm bằng cách sử dụng hàm Math.sqrt, nó sẽ trả về NaN.

```
console.log(Math.sqrt(-1));
```

Kết quả:

```
NAN
```

### 2.3 Ví dụ 3

Bất cứ khi nào chúng ta cố gắng thực hiện tính toán trên NaN, nó sẽ trả về NaN.

```
console.log(5 + NaN);
```

Kết quả:

```
NAN
```
