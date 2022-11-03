---
weight: 1
title: "Hướng dẫn tạo ứng dụng Todo list"
date: 2022-10-27
lastmod: 2022-10-27
draft: false
authors: [CuongPham, DaiLai]
authorLink: "https://dillonzq.com"
description: "Discover what the Hugo - LoveIt theme is all about and the core-concepts behind it."
images: []
resources:
  - name: "featured-image"
    src: "featured-image.png"

tags: ["javascript"]
# categories: ["documentation"]

lightgallery: true
math:
  enable: true
toc:
  auto: true
---

# Hướng dẫn tạo ứng dụng TodoList với javascript

Ứng dụng TodoList là ứng dụng cơ bản nhất để giúp các lập trình viên mới bắt đầu làm quen với những dòng code nhạt nhẽo trở nên thú vị. Sau đây chúng ta sẽ đi tìm hiểu ngay bây giờ.

## html

Đầu tiên chúng ta sẽ tạo file `.html` với đoạn code sau

```html
<form id="form">
  <input
    type="text"
    class="input"
    id="input"
    placeholder="Enter your todo"
    autocomplete="off"
  />

  <ul class="todos" id="todos"></ul>
</form>
```

Trong đó `<form ...></form>` được gọi là thẻ html
Mỗi một thẻ sẽ mang một ý nghĩa và được sử dụng với mục đích khác nhau

Đoạn code trên ta có 3 thẻ với:

- Thẻ `form` dùng để: chứa những thẻ với mục đích nhập liệu từ người dùng

- Thẻ `input` dùng để: cho người dùng nhập liệu từ bàn phím

- Thẻ `ul` dùng để: hiển thị danh sách nội dung

---

## css

Tiếp theo chúng ta sẽ style cho chúng hay là làm đẹp lại giao diện vì mặc định những thẻ này khi hiển thị trên trình duyệt chúng rất là xấu

```css
form {
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 100%;
  width: 400px;
}

.input {
  border: none;
  color: #444;
  font-size: 2rem;
  padding: 1rem 2rem;
  display: block;
  width: 100%;
}

.input::placeholder {
  color: #d5d5d5;
}

.input:focus {
  outline-color: rgb(179, 131, 226);
}
```

chúng ta sẽ tìm hiểu các thuộc tính css trong bài sau

---

## javascript

và phần cuối cùng là để cho chúng có thể làm đúng mọi nhiệm vụ của mình thì chúng ta sẽ tại file .js để xử lý chúng.

Đầu tiên chúng ta sẽ phải chọn được nó trong file js (hay có nghĩa là tham chiếu đến chúng trong dom)

```js
const form = document.getElementById("form");
const input = document.getElementById("input");
const todosUL = document.getElementById("todos");
```

chúng ta sẽ tạo 1 function để xửa lý khi người dùng thêm nội dung todo
function này sẽ có tác dụng là thêm dữ liệu vào danh sách (ul)

```js
function addTodo(todo) {
  // lấy dữ liệu trong ô input mà người dùng vừa nhập
  let todoText = input.value;

  // kiểm tra xem có tham số truyền vào hay không
  if (todo) {
    todoText = todo.text;
  }

  // kiểm tra gía trị
  if (todoText) {
    const todoEl = document.createElement("li");
    if (todo && todo.completed) {
      todoEl.classList.add("completed");
    }

    todoEl.innerText = todoText;

    todoEl.addEventListener("click", () => {
      todoEl.classList.toggle("completed");
      // cập nhật vào danh sách
      updateLS();
    });

    todoEl.addEventListener("contextmenu", (e) => {
      e.preventDefault();

      todoEl.remove();
      updateLS();
    });

    todosUL.appendChild(todoEl);

    input.value = "";

    updateLS();
  }
}
```

ở đây ta có thêm một hàm `updateLS` để cập nhật vào danh sách

```js
function updateLS() {
  todosEl = document.querySelectorAll("li");

  const todos = [];

  todosEl.forEach((todoEl) => {
    todos.push({
      text: todoEl.innerText,
      completed: todoEl.classList.contains("completed"),
    });
  });

  localStorage.setItem("todos", JSON.stringify(todos));
}
```

khi cập nhật danh sách đồng thời ta cập nhật luôn vào localStronge

> Tham khảo các khóa học nhiều hơn [tại đây](https://techmaster.vn/)
