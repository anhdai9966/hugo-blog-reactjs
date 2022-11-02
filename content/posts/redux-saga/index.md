---
weight: 1
title: "Khám phá các khái niệm trong Redux Saga"
date: 2022-11-02
lastmod: 2022-11-02
draft: false
authors: ["DaiLai"]
description: "Khám phá các khái niệm trong Redux Saga"
featuredImage: "saga.jpeg"

tags: ["react", "redux"]
categories: ["reactjs"]
lightgallery: true

toc:
  auto: true
math:
  enable: true

code:
  maxShownLines: 100
---

Khi mới tìm hiểu về Redux Saga có thể bạn sẽ thấy khá khó hiểu về một số khái niệm mới trong Redux Saga nên hôm nay chúng ta cũng tìm hiểu về Redux Saga để đơn giản hóa nó nhé.

## Redux Saga là gì?
Theo như trang chủ của Redux Saga, nó là một thư viện middleware trong Redux. Nó sẽ giúp chúng ta xử lý các tác vụ "Side-effect" (những hành động bất đồng bộ như gọi Api để lấy dữ liệu) một cách đơn giản và dễ dàng quản lý những tác vụ này trong ứng dụng của bạn.

Vì đã có nhiều bài hướng dẫn cài đặt Redux Saga vào dự án nên mình sẽ không đi sâu vào phần này mà sẽ tập chung vào nội dung của nó nhé.

## Các khái niệm trong Redux Saga
Saga
Saga là những Generator functions (đây là một tính năng mới của ES6, ai chưa biết về khái niệm này có thể google tìm hiểu thêm nhé).
Những Saga này sẽ được Redux Saga middleware đọc và thực thi lần lượt những câu lệnh bên trong nó từ trên xuống dưới. Khi gặp câu lệnh yield, Redux Saga middleware sẽ nhận được một Effect (giả thích bên dưới) nào đó và thực hiện hành động tương ứng theo mô tả của Effect, hành động này có thể là blocking hoặc non-blocking. Nếu Redux Saga middleware nhận được một Promise, nó sẽ block ở câu lệnh đó và chờ cho đến khi Promise thực thi xong rồi mới tiếp tục đọc và thực thi các câu lệnh tiếp theo trong Saga.

Effect:
Là một JavaScript Object chứa thông tin mô tả các tác vụ, Redux Saga middleware sẽ dựa theo mô tả này để thực thi một hành động nào đó.

Effect Creator:
Là những Factory Function được cung cấp bởi Redux Saga, những hàm này sẽ trả về một Effect. Một số Effect creator hay dùng là: call, fork, spaw, take, takeEvery, takeLatest, join, delay,...
ví dụ:

```jsx
// Câu lệnh sử dụng Effect Creator call
const result = call(myFunc, 'arg1', 'arg2')
console.log(result)
```

Đoạn code trên sẽ trả về cho chúng ta một Object chứa mô tả như hình dưới và Redux Saga middleware dựa vào những mô tả này và thực hiện gọi hàm myFunc với các tham số arg1 và arg2.

![image.png](https://images.viblo.asia/dde9f91e-0a16-45f4-bd80-0871ef2f6421.png)

Task
Là một nhiệm vụ được Redux Saga middleware thực thi, chúng ta có thể thực thi nhiều task song song bằng cách sử dụng fork:

```jsx
import {fork} from "redux-saga/effects"

function* saga() {
  ...
  const task = yield fork(otherSaga, ...args)
  ...
}
```
Blocking và Non-blocking
Blocking nghĩa là khi Redux Saga middleware nhận được một Effect nó tạm dừng Saga lại chờ cho đến khi câu lệnh đó thực thi xong rồi mới tiếp tục thực thi các Effect tiếp theo trong Saga

A Non-blocking nghĩa là Saga sẽ được tiếp tục ngay lập tưc sau khi yield một Effect.

Chi tiết xem bảng dưới đây:

![image.png](https://images.viblo.asia/6a3e92a4-2f52-4c35-9401-29e942f109ce.png)

![image.png](https://images.viblo.asia/1b2ae564-2946-4c6d-8a7b-ba92766a010c.png)



Watcher và Worker
Đây là một cách tổ chức code để kiểm soát luồng hoạt động của Redux Saga một cách dễ dàng hơn.

Watcher: Là một Saga sẽ theo dõi tất cả những action được gửi đến middleware và sẽ thông báo cho Worker thực hiện tác vụ tương ứng.

Worker: Là một Saga sẽ thực thi các hành động bên trong nó mỗi khi nhận được thông báo từ Watcher.

ví dụ:

```js
function* watcher() {
  while (true) {
    const action = yield take(ACTION)
    yield fork(worker, action.payload)
  }
}

function* worker(payload) {
  // ... do some stuff
}
```

## Tổng kết
Trên đây mình đã tổng hợp lại một số khái niệm của Redux Saga để có thể giúp mọi người có cái nhìn tổng quan về nó. Hy vọng qua bài viết này các bạn đã hiểu thêm về các khái niệm trong Redux Saga và có thể áp dụng nó vào trong các dự án mình. Happy coding! 😁

Tài liệu tham khảo:
https://redux-saga.js.org/docs/Glossary

> Tham khảo nhiều hơn các khóa học onlab - online [tại đây](https://techmaster.vn/)