---
weight: 1
title: "ReactJS - Create form and validate with redux-form"
date: 2022-11-02
lastmod: 2022-11-02
draft: false
authors: ["DaiLai"]
description: "Hướng dẫn tạo from và validate với redux-from"
featuredImage: "React-redux-2.png"

tags: ["react", "redux"]
categories: ["reactjs"]
lightgallery: true

toc:
  auto: true
math:
  enable: true
---


## Giới thiệu về redux-form
redux-form là một components bậc cao cho form được sử dụng trong Redux React.
Sử dụng redux-form giúp dễ dàng quản lý các state của form trong redux.
Điều quan trọng nhất nó làm dễ dàng để validate các giá trị của form khi input form.
Data flow

![pic](https://images.viblo.asia/7b9112dd-fb6c-4144-b3b8-701029d6fd16.png)

Data flows như sau:

user click vào thẻ input
"Focus action" được dipatch
formReducer update state tương ứng
The state is then passed back to the input.
Cài đặt

```sh
npm install --save redux-form
```

Sử dụng trong redux-form trong app của chúng ta
Chúng ta new một project redux-form-demo

```sh
create-react-app  redux-form-demo
```

Cài đặt redux

```sh
npm i redux --save
npm i react-redux --save
```

cài đặt redux-form

```sh
npm install --save redux-form
```

Chúng ta tạo một form là register user

cd src && mkdir register

Đầu tiên ta tạo một component, tạo một form như sau register/RegisterForm.jsx

```jsx
import React from 'react';
import { Field, reduxForm } from 'redux-form';
import validateInput from './validate';
import { buttons } from 'bootstrap-css'

const renderField = ({ input, label, type, meta: { touched, error } }) => (
  <div className="form-group">
    <label>{label}</label>
    <div>
      <input {...input} placeholder={label} type={type} />
    </div>
    {touched && error && <span className="text-danger">{error}</span>}
  </div>
);

const SubmitValidationForm = props => {
  const { error, handleSubmit, pristine, reset, submitting } = props;
  return (
    <form className="form-horizontal" onSubmit={handleSubmit}>
      <Field
        name="firstName"
        type="text"
        component={renderField}
        label="first name"
      />
      <Field
        name="lastName"
        type="text"
        component={renderField}
        label="last name"
      />
       <Field
        name="email"
        type="text"
        component={renderField}
        label="email"
      />
      <Field
        name="password"
        type="password"
        component={renderField}
        label="Password"
      />
      {error && <strong>{error}</strong>}
      <div>
        <button type="submit" disabled={submitting}>register</button>
        <button type="button" disabled={pristine || submitting} onClick={reset}>
          Clear Values
        </button>
      </div>
    </form>
  );
};

export default reduxForm({
  form: 'submitValidation', // a unique identifier for this form
  validate: validateInput,
})(SubmitValidationForm);
```

```jsx
import React from 'react';
import { Field, reduxForm } from 'redux-form';
import validateInput from './validate';
import { buttons } from 'bootstrap-css'

const renderField = ({ input, label, type, meta: { touched, error } }) => (
  <div className="form-group">
    <label>{label}</label>
    <div>
      <input {...input} placeholder={label} type={type} />
    </div>
    {touched && error && <span className="text-danger">{error}</span>}
  </div>
);

const SubmitValidationForm = props => {
  const { error, handleSubmit, pristine, reset, submitting } = props;
  return (
    <form className="form-horizontal" onSubmit={handleSubmit}>
      <Field
        name="firstName"
        type="text"
        component={renderField}
        label="first name"
      />
      <Field
        name="lastName"
        type="text"
        component={renderField}
        label="last name"
      />
       <Field
        name="email"
        type="text"
        component={renderField}
        label="email"
      />
      <Field
        name="password"
        type="password"
        component={renderField}
        label="Password"
      />
      {error && <strong>{error}</strong>}
      <div>
        <button type="submit" disabled={submitting}>register</button>
        <button type="button" disabled={pristine || submitting} onClick={reset}>
          Clear Values
        </button>
      </div>
    </form>
  );
};

export default reduxForm({
  form: 'submitValidation', // a unique identifier for this form
  validate: validateInput,
})(SubmitValidationForm);

```

Ở đẩy mình sử dụng thêm package "bootstrap-css"

npm install bootstrap-css@4.0.0-alpha.5 --save-dev

Tạo thêm 1 file để handle validate theo ý của mình register/validate.js

```jsx
import isEmpty from 'lodash/isEmpty';

 const regexEmail = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

const validateInput = (values) => {
  const errors = {};
  if(isEmpty(values.firstName)) {
    errors.firstName = { _error: 'Required' };
  }
  if(isEmpty(values.lastName)) {
    errors.lastName = { _error: 'Required' };
  }
  if(isEmpty(values.email)) {
    errors.email = { _error: 'Required' };
  } else if(!regexEmail.test(values.email)){
    errors.email = { _error: 'Email invalid' };
  }
  if(isEmpty(values.password)) {
      errors.password = { _error: 'Required' };
  }
  return errors;
};

export default validateInput;
```


Trên đây là mình validate basic, các bạn có thể validation theo từng spec cụ thể. tiếp theo là mình tạo 1 container chứa form, và xử lý data khi pass validate

register/index.jsx

```jsx
import React, { Component } from 'react';

import RegisterForm from './RegisterForm';

class register extends Component {

  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit(values) {
    // handle data after pass validate
  }

  render() {
    return (
      <RegisterForm
        onSubmit={this.handleSubmit}
      />
    );
  }
}

export default register;
```

Chúng ta sẽ render tạm trong file App.js để thấy được kết quả

```jsx
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import Cart from './components/cart';
import Register from './register';
class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <div className="App-intro">
          <h1> Form register </h1>
        </div>
        <Register />
      </div>

    );
  }
}

export default App;
```

Chúng ta run `npm start` để thấy được kết quả



Và nếu chúng ta input invalid data kết quả sẽ như sau:

Như vậy chúng ta đã có thể tạo một form đơn giản và validate data theo ý muốn, tùy từng trường hợp cụ thể mà chúng ta sẽ sử dụng redux form một cách hợp lý nhất Các bạn có thể tham khỏa thêm tại đây [reudux form](http://redux-form.com/7.0.1/docs/GettingStarted.md/)

> Tham khảo nhiều hơn các khóa học onlab - online [tại đây](https://techmaster.vn/)