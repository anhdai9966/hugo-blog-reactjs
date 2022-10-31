---
author: dailai9966
title: Hướng dẫn tạo ứng dụng quizApp
date: 2022-10-31
description: Hướng dẫn tạo ứng dụng quizApp
tags:
  - html
  - css
  - javascript
categories:
  - tutorial
keywords:
  - js
  - javascript
  - html
  - huong dan
series: ["javascript"]
---

# Hướng dẫn tạo ứng dụng quizApp bằng javascrip

Đầu tiên ta cần một dữ liệu mẫu với cấu trúc như sau

```js
const quizData = [
  {
    question: "Which language runs in a web browser?",
    a: "Java",
    b: "C",
    c: "Python",
    d: "JavaScript",
    correct: "d",
  },
  {
    question: "What does CSS stand for?",
    a: "Central Style Sheets",
    b: "Cascading Style Sheets",
    c: "Cascading Simple Sheets",
    d: "Cars SUVs Sailboats",
    correct: "b",
  },
  {
    question: "What does HTML stand for?",
    a: "Hypertext Markup Language",
    b: "Hypertext Markdown Language",
    c: "Hyperloop Machine Language",
    d: "Helicopters Terminals Motorboats Lamborginis",
    correct: "a",
  },
  {
    question: "What year was JavaScript launched?",
    a: "1996",
    b: "1995",
    c: "1994",
    d: "none of the above",
    correct: "b",
  },
];
```

Tiếp theo ta sẽ lấy dữ liệu của từng bài quiz rồi hiển thị chúng lên màn hình

```js
let currentQuiz = 0;

loadQuiz();

function loadQuiz() {
  deselectAnswers();

  const currentQuizData = quizData[currentQuiz];

  questionEl.innerText = currentQuizData.question;
  a_text.innerText = currentQuizData.a;
  b_text.innerText = currentQuizData.b;
  c_text.innerText = currentQuizData.c;
  d_text.innerText = currentQuizData.d;
}
```

việc tiếp theo ta sẽ lắng nghe sự kiện khi người dùng click vào một đáp án rồi kiểm tra xem đáp án đó có chính xác hay không

```js
function getSelected() {
  let answer;

  answerEls.forEach((answerEl) => {
    if (answerEl.checked) {
      answer = answerEl.id;
    }
  });

  return answer;
}

submitBtn.addEventListener("click", () => {
  const answer = getSelected();

  if (answer) {
    if (answer === quizData[currentQuiz].correct) {
      score++;
    }

    currentQuiz++;

    if (currentQuiz < quizData.length) {
      loadQuiz();
    } else {
      quiz.innerHTML = `
          <h2>You answered ${score}/${quizData.length} questions correctly</h2>
          <button onclick="location.reload()">Reload</button>
      `;
    }
  }
});
```

nếu người dùng click chọn đáp án đúng thì tăng câu trả lời đúng lên 1 và chuyển sang câu tiếp theo 

sau khi chuyển sang câu tiếp theo thì `loadQuiz()` sẽ được chạy để hiển thị câu hỏi tiếp theo lên màn hình rồi sau đó
