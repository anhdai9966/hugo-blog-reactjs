---
weight: 1
title: "Tìm hiểu ReactJs cơ bản và cách sử dụng"
date: 2022-11-03
lastmod: 2022-11-03
draft: false
authors: ["DaiLai"]
description: "Tìm hiểu ReactJs cơ bản và cách sử dụng"
featuredImage: "react-js-projects.jpg"

tags: ["react"]
categories: ["reactjs"]
lightgallery: true

toc:
  auto: true
math:
  enable: true
---

Nếu chưa từng sử dụng React thì bạn đã tìm đến đúng nơi rồi đấy. Còn nếu đã từng dùng qua React nhưng lại vướng vào một số vấn đề khó hiểu, bạn nên đọc bài viết này. Hướng dẫn này bao gồm tất cả những điều cơ bản.


## React là gì và tại sao bạn nên sử dụng nó?

Trang chủ React đã trả lời cho chúng ta câu hỏi đầu tiên một cách rõ ràng. Còn nếu bạn hỏi tôi, tôi sẽ định nghĩa React như một "cơ chế hiển thị giao diện dựa trên nền tảng Javascript - JavaScript-based UI rendering engine". Lưu ý một chút là tôi đã bỏ "HTML" ra khỏi định nghĩa về React. Đó là bởi vì HTML chỉ là một trong rất nhiều các đối tượng khả thi mà React có thể làm việc được. Tôi cũng sẽ bỏ "browser" ra vì bạn cũng có thể sử dụng React trên server và native apps. "Engine" trong định nghĩa của tôi thì tương tự như các game engines. Với React, nó cũng giống như là một game engine, bạn chỉ cần xác định trạng thái của một ứng dụng, chuyển nó sang view, nếu có gì thay đổi, đừng thay đổi view, thay vào đó bạn chỉ cần render lại nó là nhận được view mới.

Chúng tôi đã chuyển tiếp từ Backbone views sang React views. Với React việc duy trì tính đồng bộ giữa application state (trạng thái ứng dụng) và view sẽ không còn phức tạp nữa. Chỉ cần render lại, clean-up, và lặp đi lặp lại. Do đó, bạn có thể dễ dàng xây dựng các UI components (thành phần giao diện) hoàn toàn độc lập, và có thể tái sử dụng. Nếu có sự thay đổi, cứ vô tư mà tái cấu trúc lại các views!

### Hello world

Một ví dụ đơn giản và phổ biến nhất
```jsx
React.render(
    <div>Hello, world!</div>,
    document.body
);
```

Thật đơn điệu phải không? Rõ ràng React là một công cụ cực kỳ mạnh mẽ, vậy mà chúng ta lại sử dụng nó để in ra câu nói nhàm chán "Hello World!". Ok, tạm quên cái ví dụ trên đi đã, bây giờ chúng ta sẽ nói một chút về JSX.

### JSX

Nếu đã từng nghe nói về React, bạn cũng có thể đã nghe qua về JSX. Để thực sự cảm thấy hứng thú trong việc sử dụng JSX, bạn phải lưu ý đến hai điều sau:

Bạn phải thực sự hiểu JSX là gì, cũng như tất cả các sắc thái của nó. Bạn phải có kinh nghiệm trong việc ra quyết định trong trường hợp nào thì nên sử dụng nó (React) và thực sự coi đó là điều cần thiết.

### JSX không phải một ngôn ngữ template

Điều đầu tiên dễ dàng nhận thấy là JSX không phải một ngôn ngữ template. Nếu bạn nhầm lẫn nó với Handlebars, hãy dừng ngay suy nghĩ đó lại. JSX chỉ đơn giản là một cú pháp thay thế JavaScript, mặc dù cú pháp đó là đặc trưng của React (ít nhất ở thời điểm hiện tại). Ví dụ trên được viết lại như sau:

```js
React.render(
    React.createElement('div', {}, 'Hello, world!'),
    document.body
);
```

Cứ coi như React.createElement là thứ gì đó chưa biết, vì thế chúng ta sẽ làm nó trở nên rõ ràng hơn một chút. Khi sử dụng React, bạn thường sẽ không làm việc trực tiếp với DOM. Thay vào đó, bạn tạo các thành phần Virtual DOM. Virtual DOM thực ra là các JSON objects. Chúng là thể hiện của một cấu trúc bên dưới DOM nhưng không mang bất cứ đặc tính nào của các DOM thật. React sẽ convert các thành phần này thành các thành phần DOM thật (actual/real DOM) khi cần thiết. React.createElement là một phương thức được sử dụng để tạo ra các JSON objects này. Cú pháp như sau:

React.createElement(elementNameOrClass, props, children...); Trong ví dụ Hello World ở trên, chúng ta có sử dụng một thẻ HTML làm tham số đầu tiên. Các thẻ HTML ở vị trí tham số này thì còn được coi như là các component classes. Tham số thứ hai được sử dụng để truyền các properties cho component class trước đó. Các tham số còn lại trở thành property đặc biệt, là children của component. Chúng ta sẽ nói rõ về nó sau. Còn bây giờ, bạn chỉ cần nhớ rằng JSX (đại khái là) thực hiện việc chuyển đổi đoạn code trên như sau:

Nếu tham số đầu tiên là một chuỗi ánh xạ của một thẻ HTML nào đó thì sử dụng component class như là thẻ HTML đó. Nếu tag name không phải là một HTML element, cứ coi như nó là một biến cục bộ có tên trỏ vào một component class tùy chọn. Các thuộc tính được convert thành một đối tượng và được truyền vào như tham số thứ hai. Các thành phần con được truyền vào như các tham số còn lại. Ví dụ về JSX:

```jsx
<div id="greeting-container" className="container">
    <Greeting name="World"/>
</div>
```

Nó có thể được convert thành

```jsx
React.createElement("div",
    {
        id: "greeting-container",
        className: "container"
    },
    React.createElement(Greeting, {name: "World"})
)
```

Handlebars, Django templates và rất nhiều template languages khác cho phép bạn thay thế giữa các plain text với một số template chuyên dùng. Template language hiếm khi có khả năng diễn đạt như của host language (ngôn ngữ lập trình chính thống: PHP, Python, Javascript...). JSX chỉ convert các đánh dấu XML thành code JavaScript. Nó tương tự như là bạn đang gõ code Javascript vậy.

Điều này rất tuyệt vì bạn có thể sử dụng tối đa sức mạnh của JavaScript và tất cả mọi thứ bạn đã học về nó như các biểu thức, cấu trúc hàm, hay bất kỳ các tính năng nào khác trong views của bạn. Bạn không cần viết các helpers (hàm trợ giúp chuyên dùng) đặc trưng cho template language của mình mà chỉ cần sử dụng Javascript

```jsx
var names = ['Moe', 'Larry', 'Curly'];

React.render(
    <div>
        {
            names.map(function (name) {
                return <div>Hello, {name}!</div>
            })
        }
    </div>,
    document.body
);
```

Dấu ngoặc {} cho phép chúng ta sử dụng Javascript thuần, nó không phải là một cơ chế escape dữ liệu. Chú ý là bên trong map function, chúng ta trả về một markup là một thẻ div, bên trong markup đó chúng ta lại có một biểu thức Javascipt. Đây là một ví dụ rõ ràng về việc JSX không phải là một template language.

JSX hoàn toàn không bắt buộc, nhưng lại thực sự hữu ích

Theo quan điểm cá nhân, tôi thấy JSX thực sự hữu ích vì hai lý do:

Nó cung cấp các biểu thức viết tắt (shorthand) hữu ích cho một số React boilerplate mà bạn bắt buộc phải sử dụng dù muốn hay không. Nó làm HTML markup của bạn trông giống như HTML markup. Lý do đầu tiên đã khá rõ ràng qua các ví dụ trên. Các ví dụ về JSX ngắn hơn so với các ví dụ về JS tương ứng. Tất nhiên, chúng ta có thể khéo léo làm theo cách của mình. Hãy xem xét ví dụ sau đây:

```jsx
var R = React.DOM;
Greeting = React.createFactory(GreetingClass);

React.render(
  R.div({id: "greeting-container", className: "container"},
    Greeting({name: "World"})
  ),
  document.body
);
```
React.DOM cung cấp một tập các factories cho các thẻ HTML. React.createFactory chỉ là một helper ràng buộc component class của bạn với React.createElement để bạn có thể tạo các factories cho riêng mình. Theo quan điểm của tôi, vấn đề khá lớn ở đây là code Javascript trộn trong các markup. Hãy xem markup sau:

```jsx
<p>
  The live example is the same. The only difference is that we render to <code>mountNode</code>, which is just the DOM node for the example.
</p>
```

Khi chuyển sang Javascript sẽ rất khó nhìn

```jsx
R.p({},
  'The live example is the same. The only difference is that we render to ',
  R.code({},
    'mountNode'
  ),
  ', ' +
  'which is just the DOM node for the example.'
)
```

Ví dụ trên là một vấn đề thực tế khiến tôi nhận ra mình chỉ nên sử dụng JSX.

Nếu bạn có một designer đang làm việc với HTML thì sẽ không có nhiều hướng dẫn để chuyển sang JSX. Thay thế tất cả các markup với JavaScript đó sẽ mất rất nhiều công sức, mà có thể thằng designer sẽ tức điên lên mà thông bạn!

## Các components tùy chỉnh

Từ đầu đến giờ, tôi đã giải thích với bạn JSX là gì, cách sử dụng JSX cho các views của bạn như thế nào (thực chất nó chỉ là JavaScript) để giúp bạn có một view language thật sự mạnh mẽ. Nhưng đó đều không phải các lý do để sử dụng React. Một khi đã bắt đầu tạo ra các components tùy chỉnh, bạn sẽ thấy được lý do thực sự khiến bạn không thể rời mắt khỏi React.

## Component đầu tiên

Chúng ta hãy thử bắt đầu tạo một ứng dụng ghi chú. Để giữ mọi thứ đơn giản, ta sẽ bỏ qua việc lưu trữ dữ liệu trên server. Hãy bắt đầu một cách thật đơn giản và xác định dữ liệu cần để render.

```jsx
var notepad = {
  notes: [
    {
      id: 1,
      content: "Hello, world!\nBoring.\nBoring.\nBoring."
    },
    {
      id: 2,
      content: "React is awesome.\nSeriously, it's the greatest."
    },
    {
      id: 3,
      content: "Robots are pretty cool.\nRobots are awesome, until they take over."
    },
    {
      id: 4,
      content: "Monkeys.\nWho doesn't love monkeys?"
    }
  ]
}
```

Giờ chúng ta sẽ tạo một custom component và render một danh sách các notes của chúng ta. Dòng đầu tiên của note sẽ là tiêu đề (chưa xét tới các vấn đề về tối ưu hóa):

```jsx
var NotesList = React.createClass({
  render: function () {
    var notes = this.props.notepad.notes;

    return (
      <div className="note-list">
      {
        notes.map(function (note) {
          var title = note.content.substring(0,
            note.content.indexOf('\n')
          );
          title = title || note.content;

          return (
            <div key={note.id} className="note-summary">
              {title}
            </div>
          );
        })
      }
      </div>
    );
  }
});
```

Lưu ý rằng một React component đơn giản chỉ cần một method render. Có rất nhiều methods khả dụng khác, nhưng render là method chủ đạo. Trong method render, bạn chỉ trả về thứ bạn muốn render. React sẽ đảm đương công việc từ đây.

Cũng cần lưu ý rằng tôi đã đặt một thuộc tính key trong đó. Thuộc tính key này là duy nhất, nó xác định một component bên cạnh các components anh chị của nó. Nói chung, nếu bạn đang sử dụng map hoặc filter hoặc một phương thức tương tự nào khác, bạn phải đặt cho mỗi element một key. Đôi khi với một element duy nhất mà nó đại diện cho một thứ duy nhất thì bạn cũng cần phải sử dụng key để đảm bảo React hủy bỏ DOM thay vì tái sử dụng nó. Chúng ta sẽ cùng thảo luận về sự cần thiết của việc này sau. Còn bây giờ, bạn chỉ cần hiểu được rằng React sẽ cảnh báo nếu bạn không làm điều đó. Và nếu bạn bỏ qua cảnh báo này, những bugs kỳ lạ có thể sẽ xảy ra.

Mọi thứ đang dần trở nên thú vị. Nếu React chỉ có thể render

và các thẻ tương tự thì có vẻ không hữu dụng lắm. Nhưng bạn lại có thể tạo các components của riêng mình. Thậm chí là tốt hơn, giao diện và tính năng của các components đó hoàn toàn được điều khiển bởi các thuộc tính được truyền vào nó. Component NotesList trên hoạt động như một hàm thuần. Tất cả các trạng thái của nó được truyền vào như các thuộc tính. Nếu sau đó chúng ta quyết định ứng dụng sẽ hỗ trợ nhiều notepads thì component này thực sự hữu ích. Chúng ta chỉ truyền vào notepad những gì chúng ta muốn render, và component sẽ làm việc của nó. Sau này việc hủy bỏ component cũng sẽ dễ dàng hơn.

```jsx
var NoteSummary = React.createClass({
  render: function () {
    var note = this.props.note;
    var title = note.content.substring(0,
      note.content.indexOf('\n')
    );
    title = title || note.content;

    return (
      <div className="note-summary">{title}</div>
    );
  }
});
```

```jsx
var NotesList = React.createClass({
  render: function () {
    var notes = this.props.notepad.notes;

    return (
      <div className="note-list">
      {
        notes.map(function (note) {
          return (
            <NoteSummary key={note.id} note={note}/>
          );
        })
      }
      </div>
    );
  }
});
```

Khá dễ dàng phải không? Giống như tái cấu trúc một function lớn thành các functions nhỏ hơn, bạn có thể chia nhỏ một đoạn dữ liệu và đặt nó vào bên trong một component khác. Sau đó chỉ cần gọi component mới của bạn, truyền nó vào các mệnh đề thích hợp. Bây giờ chúng ta có thể sử dụng component NoteSummary bất cứ đâu chúng ta muốn. Nếu một note nào đó sai, chúng ta sẽ tìm được vị trí lỗi đó. Lỗi này hoặc nằm trong component hoặc trong các mệnh đề được truyền vào để tạo nó.

Reactive components

Các ví dụ trên đủ dùng để tạo một trang tĩnh, nhưng nếu phải tạo app làm công việc gì đó, như react-ive thì sao? Yên tâm đi, React đảm bảo những điều đó cho bạn.

Nếu trạng thái của app thay đổi, chỉ cần re-render nó

Cho phép tôi nhắc lại: Nếu bất cứ điều gì, bất cứ ở đâu trong app của bạn có sự thay đổi, hãy ném hết tất cả đi và re-render chúng.

Làm việc với React bạn cần phải quên đi những thói quen cũ khi sử dụng jQuery, nơi bạn phản hồi một sự kiện nào đó và sau đó thì tinh chỉnh DOM. Hãy quên các ràng buộc hai chiều (two-way binding) phức tạp hay các theo dõi về scopes trong Angular. Bất cứ khi bạn có app state mới, chỉ cần re-render app state đó.

Giờ chúng ta sẽ thực hiện việc thêm các notes. Với ví dụ đơn giản này, chúng ta sẽ thêm một số functions ở top-level để xử lý các events tương tác từ người dùng. Chúng ta sẽ giữ các components được tách biệt bằng cách truyền các handlers của chúng vào đó. Khi dev một app thực sự, bạn có thể muốn sử dụng một cái gì đó giống như Flux, đó là một pattern cho việc sử dụng các events được kiểm soát một cách chặt chẽ.

Hãy đặt phương thức React.render vào trong phương thức onChange để ta có thể gọi nó mỗi khi có sự thay đổi. Chúng ta cũng đặt vào đó một handler onAddNote để thêm notes mới và một handler onChangeNote để thay đổi notes. Tôi sẽ định nghĩa chúng như sau:

```jsx
var onChange = function () {
  React.render(
    <Notepad notepad={notepad} onAddNote={onAddNote}
      onChangeNote={onChangeNote}/>,
    document.body
  );
};

onChange();
```

Bất cứ khi nào có sự thay đổi, chúng ta sẽ gọi onChange và nó sẽ re-render app state. Đừng lo lắng về cách hiển thị của nó. Tất cả được thực hiện với sự kỳ diệu của virtual DOM. React sẽ quyết định giữ DOM elements nào ở lại hay bỏ elements nào đi một cách rất thông minh. Nếu đó chính xác là DOM elements cần để re-render, nó sẽ giữ chúng và tinh chỉnh các thuộc tính và nội dung khi cần thiết.

Ngoài ra, chỉ cần bạn sử dụng các key phù hợp khi cần thiết, bạn sẽ không phải lo lắng về việc một input bị mất focus. Nếu đã từng sử dụng Backbone theo cách này, bằng việc xóa sạch DOM và bắt đầu lại từ đầu, bạn sẽ biết rằng khi một input được xóa bỏ và add lại vào document, nó sẽ mất focus, như thế thực sự là sẽ gây khó chịu cho user. Với React, nếu bạn re-render cùng một element, DOM element tương ứng sẽ vẫn còn, vì vậy user vẫn có thể tiếp tục nhập dữ liệu thoải mái ngay cả khi DOM bị thay đổi.

Bây giờ, hãy viết các handlers để add notes. Chúng ta sẽ loại bỏ các notes tĩnh lúc trước đi, thêm một cơ chế sinh ID, và tiếp tục theo dõi các notes đã chọn:

```jsx
var notepad = {
  notes: [],
  selectedId: null
};

var nextNodeId = 1;

var onAddNote = function () {
  var note = {id: nextNodeId, content: ''};
  nextNodeId++;
  notepad.notes.push(note);
  notepad.selectedId = note.id;
  onChange();
};
```

Ta cũng thêm một handler để edit các notes mới này

```jsx
var onChangeNote = function (id, value) {
  var note = _.find(notepad.notes, function (note) {
    return note.id === id;
  });
  if (note) {
    note.content = value;
  }
  onChange();
};
```

Một lần nữa, chúng ta chỉ cần làm mọi thứ thật đơn giản. Trong một app lớn hơn, chúng ta có thể sẽ muốn làm gì đó phức tạp hơn. Nguyên tắc sẽ vẫn như cũ. Các components của chúng ta sẽ có một số cơ chế để thông báo rằng user đã thay đổi điều gì đó. Khi có thay đổi, chúng ta sẽ có một số cơ chế để re-render app. Component của chúng ta sẽ không bao giờ trở thành nguồn tin tưởng để thể hiện sự tồn tại của dữ liệu. Dữ liệu đó luôn luôn nằm bên ngoài component.

Hãy tạo một component để chỉnh sửa notes

```jsx
var NoteEditor = React.createClass({
  onChange: function (event) {
    this.props.onChange(this.props.note.id, event.target.value);
  },

  render: function () {
    return (
      <textarea rows={5} cols={40}
                value={this.props.note.content}
                onChange={this.onChange}/>
    );
  }
});
```

Component này nhận handler onChange, nó sẽ được sử dụng để cập nhật những thay đổi của note.

Chúng ta tạo một component Notepad mới để render danh sách notes, một button để tạo một note mới, và một editor để chỉnh sửa note.

```jsx
var Notepad = React.createClass({
  render: function () {
    var notepad = this.props.notepad;

    var editor = null;

    var selectedNote = _.find(notepad.notes, function (note) {
      return note.id === notepad.selectedId;
    });

    if (selectedNote) {
      editor = <NoteEditor note={selectedNote}
        onChange={this.props.onChangeNote}/>
    }

    return (
      <div id="notepad">
        <NotesList notepad={notepad}/>
        <div>
          <button onClick={this.props.onAddNote}>Add note</button>
        </div>
        {editor}
      </div>
    );
  }
});
```

Thử kiểm tra xem nào

Bạn thêm một note mới và nhận thấy rằng tiêu đề thay đổi mỗi khi bạn nhập thêm note vào. Điều này quá tuyệt vời vì:

Các components của chúng ta không liên quan đến app state của chúng. Tất cả tồn tại tách biệt với view.
Các components của chúng ta không phải lo lắng về trạng thái của DOM. Nó chỉ cung cấp các fresh elements để render, và React thao tác DOM một cách kỳ diệu. Chúng ta chỉ render, ném chúng đi, sau đó lặp lại.
Các components của chúng ta cũng giống như các hàm thuần. Chúng ta cung cấp nó trong trạng thái hiện tại, sau đó chỉ chỉ cần ánh xạ lại trạng thái đó.
Trong một app lớn hơn, quan điểm thứ ba có thể nằm ngoài tầm kiểm soát của chúng ta. Truyền vào callbacks thông qua một hệ phân cấp lồng nhau có thể sẽ khó sử dụng và quản lý. Tuy nó nằm ngoài phạm vi của bài viết này, nhưng Flux là giải pháp thường được trích dẫn cho vấn đề này. Nếu có thể, hãy làm theo các model đơn giản của việc truyền vào callbacks, code của bạn sẽ trở nên linh động hơn rất nhiều.

Hãy thêm một handler để chọn một note

```jsx
var onSelectNote = function (id) {
  notepad.selectedId = id;
  onChange();
};
```

Ta sẽ truyền handler này vào component Notepad

```jsx
var onChange = function () {
  React.render(
    <Notepad notepad={notepad} onAddNote={onAddNote}
      onSelectNote={onSelectNote}
      onChangeNote={onChangeNote}/>,
    document.body
  );
};
```

Sau đó ta có thể đưa code này vào component Notepad

```jsx
var Notepad = React.createClass({
  render: function () {
    var notepad = this.props.notepad;

    var editor = null;

    var selectedNote = _.find(notepad.notes, function (note) {
      return note.id === notepad.selectedId;
    });

    if (selectedNote) {
      editor = <NoteEditor note={selectedNote}
        onChange={this.props.onChangeNote}/>
    }

    return (
      <div id="notepad">
        <NotesList notepad={notepad}
          onSelectNote={this.props.onSelectNote}/>
        <div>
          <button onClick={this.props.onAddNote}>Add note</button>
        </div>
        {editor}
      </div>
    );
  }
});
```

Trong component NotesList, chúng ta phản hồi một click bằng một summary và gọi callback. Ta cũng có thể style cho item được chọn

```jsx
var NotesList = React.createClass({
  render: function () {
    var notepad = this.props.notepad;
    var notes = notepad.notes;

    return (
      <div className="note-list">
      {
        notes.map(function (note) {
          return (
            <div key={note.id} className={
              notepad.selectedId === note.id ? 'note-selected' : ''
            }>
              <a href="#" onClick={
                this.props.onSelectNote.bind(null, note.id)
              }>
                <NoteSummary note={note}/>
              </a>
            </div>
          );
        }.bind(this))
      }
      </div>
    );
  }
});
```

Bây giờ thì thử xem

Click vào tiêu đề trong list sẽ cho phép bạn chỉnh sửa note. App của chúng ta sẽ trở nên phức tạp hơn, nhưng từng components vẫn duy trì được sự đơn giản. Bất cứ khi nào bạn cảm thấy không kiểm soát được một component, hãy chia nhỏ nó ra.

Trạng thái tạm thời

Đôi khi một component cũng cần giữ một số trạng thái, đó không hẳn là application state. Giả sử chúng ta muốn thêm chức năng xóa một note. Và chúng ta muốn xác nhận trước khi xóa. Chúng ta không thực sự cần thiết phải giữ trạng thái có muốn tiếp tục xóa hay không, mà đơn giản chỉ cần throw state (giống throw exception) đó ra. Vì thế chúng ta muốn component của mình giữ state đó hơn là duy trì nó ở bên ngoài. React có một cơ chế mạnh mẽ để thiết lập và sử dụng state nội tại này.

Trước tiên hãy thêm một delete handler và kết nối với nó mà không cần xác thực. Các bước tương tự như trên. Chúng ta thêm một handler delete, truyền nó vào, hook onClick vào một button cho handler đó. Bây giờ bạn có thể thực hiện việc xóa note!

Trong trường hợp này, button delete là một phần của note editor. Các nguyên tắc tương tự được áp dụng nếu bạn muốn thêm nó vào summary list.

Đây là note editor của chúng ta khi không có sự xác thực

```jsx
var NoteEditor = React.createClass({
  onChange: function (event) {
    this.props.onChange(this.props.note.id, event.target.value);
  },

  render: function () {
    return (
      <div>
        <div>
          <textarea rows={5} cols={40}
            value={this.props.note.content} onChange={this.onChange}/>
        </div>
        <button onClick={
          this.props.onDelete.bind(null, this.props.note.id)
        }>Delete note</button>
      </div>
    );
  }
});
```

Để làm nó có trạng thái (stateful), ta cần sử dụng hai thứ. Method getInitialState cho phép chúng ta cung cấp một trạng thái ban đầu cho component, và method setState cho phép chúng ta thay đổi trạng thái của component. Bất cứ khi nào chúng ta gọi setState, re-render sẽ tự động diễn ra. Lưu ý rằng setState là không đồng bộ. Re-render sẽ diễn ra khi React sẵn sàng. Trong các trình duyệt hiện đại, nó thường diễn ra trong không dưới 1/60 giây . (Các trình duyệt hiện đại render 60 lần một giây, và React hook vào nó thông qua requestAnimationFrame)

Đây là component tương tự khí có sự xác thực

```jsx
var NoteEditor = React.createClass({
  getInitialState: function () {
    return {
      isConfirming: false
    };
  },

  onChange: function (event) {
    this.props.onChange(this.props.note.id, event.target.value);
  },

  onDelete: function () {
    if (this.state.isConfirming) {
      this.props.onDelete(this.props.note.id);
      this.setState({isConfirming: false});
    } else {
      this.setState({isConfirming: true});
    }
  },

  onCancelDelete: function () {
    this.setState({isConfirming: false});
  },

  render: function () {
    return (
      <div>
        <div>
          <textarea rows={5} cols={40}
            value={this.props.note.content}
            onChange={this.onChange}/>
        </div>
        <button onClick={this.onDelete}>
        {
          this.state.isConfirming ? 'Confirm' : 'Delete note'
        }
        </button>
        {
          this.state.isConfirming ? <button onClick={this.onCancelDelete}>Cancel</button> : null
        }
      </div>
    );
  }
});
```

Chúng ta sử dụng getInitialState để thiết lập một biến cờ là isConfirming thành false. Sau đó chúng ta sử dụng nó để chặn việc thực thi handler delete thay vì để nó thông qua. Nếu xác nhận thì ta xóa nó, nếu không chúng ta set flag isConfirming thành true. Trong method render, chúng ta cũng render button Cancel để có thể set flag isConfirming về false.

Đây cũng là một ý tưởng tốt để cung cấp một key cho editor của chúng ta

```jsx
editor = <NoteEditor 
  key={selectedNote.id} 
  note={selectedNote} 
  onChange={this.props.onChangeNote} 
  onDelete={this.props.onDeleteNote}/>
```

Bằng cách này, khi chúng ta chuyển sang chỉnh sửa một note khác, React loại bỏ component, và ta sẽ không kết thúc với trạng thái từ note đó.

Lifecycle methods

Đôi khi bạn muốn làm một điều gì đó khi một component được thêm vào hoặc bị gỡ bỏ khỏi DOM. Để giải quyết vấn đề này, React cung cấp các methods lifecycle. Có rất nhiều các methods lifecycle khác nhau, ví dụ như, phản hồi khi các thuộc tính thay đổi cho một component.

Ta sẽ thực hiện component Pulse. Nó giống như thẻ blink cũ nhưng ít khó chịu hơn. Chúng ta sẽ dùng nó để wrap confirm button để nó trông rõ ràng hơn.

```jsx
var Pulse = React.createClass({
  getInitialState: function () {
    return {
      opacity: 1.0
    };
  },

  componentDidMount: function () {
    this.timer = setInterval(function () {
      var opacity = this.state.opacity;
      opacity -= .05;
      if (opacity < 0.5) {
        opacity = 1.0;
      }
      this.setState({
        opacity: opacity
      });
    }.bind(this), 100);
  },

  componentWillUnmount: function () {
    clearInterval(this.timer);
  },

  render: function () {
    return (
      <span style={{opacity: this.state.opacity}}>
      {this.props.children}
      </span>
    );
  }
});
```

Có một vài điều cần lưu ý ở đây.

Một lần nữa chúng ta lại sử dụng getInitialState để khởi tạo trạng thái thuộc tính opacity. Chúng ta hook componentDidMount để làm điều gì đó khi component được thêm vào DOM. Ở đây, chúng ta thiết lập this.timer là khoảng thời gian sẽ giảm opacity xuống 50% và sau đó xóc cho nó lên 100%. Chúng ta hook componentWillUnmount để làm clear timer Chúng ta render bằng cách sử dụng opacity trong state. Sau đó chúng ta sẽ sử dụng component Pulse cho button confirm như sau:

```jsx
this.state.isConfirming ?
  <div>
    <Pulse>
      <button style={{color: 'red'}}
        onClick={this.onDelete}>Confirm</button>
    </Pulse>
    <button onClick={this.onCancelDelete}>Cancel</button>
  </div> :
  <button onClick={this.onDelete}>Delete note</button>
```

Đây là bản full HD của em nó!

Pattern này thường hữu ích khi lắng nghe các sự kiện. (Trên thực tế, đó là cách Flux hoạt động). Chỉ cần lắng nghe sự kiện khi component được mount. Set state khi sự kiện xảy ra, và component được re-render. Làm sạch trước khi component được unmount.

Các nguyên tắc cần tuân theo
Đến giờ chắc bạn đã trở thành một chuyên gia về React rồi chứ? Cứ bình tĩnh. Những điều tốt đẹp trên về React thực sự chỉ là một vài khái niệm cốt lõi. Một khi đã biết cách để xây dựng các components của riêng mình, bạn sẽ không ngạc nhiên lắm khi gặp một vấn đề nào đó, ở đâu đó. Tuy nhiên, có một số điều bạn cần phải biết để tránh nhầm lẫn.

Am hiểu thuật ngữ về virtual DOM

Hầu hết các virtual DOM đều rất ảo diệu, và bạn có thể bỏ qua việc thực thi. Nhưng ít nhất thì bạn muốn cũng muốn hiểu rõ về các thuật ngữ. Tôi khuyên bạn nên xem Những vấn đề chính về thuật ngữ DOM trong React của Sebastian Markbåge trong đó mô tả mọi thứ một cách chi tiết. Tôi đã sử dụng hầu hết các thuật ngữ đó trong bài viết này, nhưng Wiki sẽ làm sáng tỏ thêm cho bạn.

Ngoài ra, các thuật ngữ đã thay đổi một chút kể từ các phiên bản trước của React. Vì vậy, các bài viết cũ có thể sẽ gọi chúng bằng một cái tên khác.

Đừng thay đổi bất cứ điều gì trong phương thức render

Method render của bạn đại diện cho view tại một thời điểm cụ thể. Để React thực hiện công việc của mình một cách chính xác, bạn cần đưa nó một ít dữ liệu và cho nó render toàn bộ trước khi thay đổi bất cứ điều gì. Trước đây bạn sẽ re-render mỗi khi có sự thay đổi, bạn không thể thay đổi trong khi bạn đang render. Nó giống như việc bạn nhờ họa sĩ vẽ chân dung mình nhưng nửa chừng lại thay đổi ý định thành vẽ một ai khác. Hẳn là người họa sĩ đó sẽ nhìn bạn một cách rất vui vẻ cho xem. Tương tự như thế, React sẽ phàn nàn về bất kỳ công việc nào như vậy. Thậm chí là tệ hơn, nếu bạn quản lý những thứ dễ dàng thay đổi như thế, bạn có thể sẽ gặp phải những bug rất kỳ lạ.

Đừng trông chờ children luôn là một mảng

Bạn nhớ this.props.children ở trên chứ? Chúng ta đã sử dụng nó trong component Pulse.

render: function () { return ( <span style={{opacity: this.state.opacity}}> {this.props.children} </span> ); }enter code here Ta truyền nó vào component span. Tuy nhiên, hãy tưởng tượng khi chúng ta muốn làm điều gì đó với mỗi child, ta sẽ làm như sau
```jsx
render: function () {
  return (
    <span style={{opacity: this.state.opacity}}>
      <ul>
      {
        this.props.children.map(function (child) {
          return <li>{child}</li>;
        });
      }
      </ul>
    </span>
  );
}
```
Sau đó chúng ta có thể dùng nó như sau
```jsx
<Pulse>
  <div>Moe</div>
  <div>Larry</div>
  <div>Curly</div>
</Pulse>
```
Vậy là ok rồi đấy. Nhưng nếu bạn dùng nó thế này thì sao
```jsx
<Pulse>
  <div>Joe</div>
</Pulse>
```
Có vẻ như cũng ổn phải không? Nhưng thật đáng tiếc là không. Trong trường hợp đó, React sẽ gửi bạn một element duy nhất cho this.props.children. Sau đó bạn sẽ nhận được một thông báo lỗi vì element đó không có method map. Nếu luôn muốn coi nó như một mảng, trước tiên bạn sẽ phải ép nó vào một mảng. Hơi khó khăn một chút, nhưng nó sẽ giúp React tránh khỏi việc tạo các mảng rác không cần thiết.

Ngoài ra, nếu bạn làm như sau:

this.props.children sẽ trở thành không xác định, kể cả khi không có gì được truyền vào

Nhận biết được sự khác biệt giữa controlled và uncontrolled components

Cần phải thật tinh tế để biết được sự khác nhau giữa các components trên. Bạn có thể xem tài liệu về React, nhưng tôi đã hơi bối rối sau khi đọc nó. Để có thể chỉnh sửa các form elements (như `<input>`, `<textarea>` hay `<select>`), bạn có thể truyền giá trị vào theo hai cách khác nhau.

Nếu truyền vào value, form element sẽ nhận giá trị đó bất kể người dùng có nhập gì vào. Trong trường hợp đó, nó là một "controlled" component, có nghĩa là bạn đang quản lý value. Nên nếu bạn truyền "cun" vào value sau đó user thêm "t" để tạo thành "cunt", bạn phải set value thành "cunt". Còn nếu không, value sẽ vẫn là "cun". Nhìn chung đó là điều tốt, vì bạn sẽ nhìn thấy app state đang giữ cùng một value như các DOM elements.

Nếu bạn truyền vào defaultValue, form element sẽ hiển thị value ban đầu đó, nhưng sau này, cho dù có truyền vào value nào thì value được hiển thị sẽ là value cuối cùng user nhập vào.

Nói chung, có thể bạn sẽ muốn sử dụng đến các controlled components. Nhưng nếu bạn đang tạo một form hoài cổ nơi user chỉ cần submit nó, thì uncontrolled components là giải pháp. Ngoài ra nếu bạn có một số trạng thái tạm thời không hợp lệ, bạn sẽ muốn sử dụng uncontrolled components. Đối với cá nhân tôi, trong trường hợp đó, tôi thích sử dụng trạng thái tạm thời để giữ value và vẫn sử dụng các controlled components.

Hãy để ý tới công việc không đông bộ

Trong các ví dụ trên, chúng tôi không bao giờ làm bất cứ việc load không đồng bộ (load async - ajax) nào, nhưng tất nhiên trong thực tế, bạn sẽ làm điều đó. Nếu đang làm một ứng dụng nhỏ, component của bạn sẽ làm tốt một số công việc không đồng bộ. Trong trường hợp đó, hãy thực hiện công việc bên trong method componentDidMount giống như cách chúng ta đã làm với setTimeout. Khi function async được trả về, chỉ cần re-render setState. Có nghĩa là bạn sẽ cần một số "zero state" view thông minh trước khi bạn có bất kỳ dữ liệu nào. Nó sẽ trở thành một spinner đơn giản hay bất kế thứ gì.

Sau này khi user thực hiện một số action, bạn sẽ chỉ cần phân chia các sự kiện và làm một số công việc không đồng bộ. Tuy nhiên, phải rất cẩn thận nếu bạn không muốn nhận được các kết quả không phù hợp. Ví dụ, nếu một async request được khởi tạo sau mỗi lần ấn một phím, một vài request trong đó sẽ trả về sai thứ tự và cho bạn các kết quả không phù hợp. May mắn thay React có thể roll-back một giá trị cũ nếu bạn nói cho nó cách biết thực hiện công việc đó bằng setState.

Trong các ứng dụng lớn hơn, tôi khuyên bạn nên đưa các công việc không đồng bộ ra khỏi component của mình và gạt nó sang một bên. Càng nhiều components của bạn vận hành đồng bộ thì càng dễ dàng có từng đấy lý do để chỉnh sửa và debug chúng. Thực hiện công việc không đồng bộ có thể làm cho những người làm công việc này cảm thấy không liên quan gì lắm so với mục đích của họ.

Nếu bạn sử dụng React cho các công việc không đồng bộ, thì ít nhất đó là một ý tưởng tốt để đẩy công việc đó cho các top-level components, để các child component của bạn có thể được tái sử dụng một cách dễ dàng.

Virtual DOM không phải là shadow DOM

Đã có lần tôi nghe vài người nói rằng họ hiểu virtual DOM vì họ nghĩ nó tương tự như shadow DOM. Thực ra là nó chẳng liên quan gì đến nhau cả.

Một số thuộc tính ở HTML khác so với ở JSX

Khi sử dụng `<div>`, `<span>`, và các HTML elements khác, hầu hết bạn có thể coi các elements đó giống như HTML tương đương của chúng. Nhưng vẫn có một số thuộc tính sẽ khác nhau. Một số điểm khác biệt đáng chú ý như:

Tất cả đều là camel-cased
Ngoại trưc các thuộc tính về dữ liệu
class là className
style là một đối tượng JSON
Các thuộc tính value và defaultValue đã đề cập ở trên.
Nếu bạn có một block HTML muốn dịch sang JSX, bạn có thể sử dụng compiler service này

Keys được định nghĩa trong parent components, không phải child components

Hãy chú ý ví dụ sau:

```jsx
var StoogeList = React.createClass({
  render: function () {
    return (
      <ul>
      {
        this.props.stooges.map(function (stooge) {
          return <Stooge key={stooge.id}/>;
        });
      }
      </ul>
    );
  }
});

var Stooge = React.createClass({
  render: function () {
    return <li>{this.props.stooge.name}</li>;
  }
});
```
StoogeList phải xác định keys cho mỗi children của chúng. Component Stooge không cần quá lo lắng về keys, vì nó chỉ render một element duy nhất.

Key phải ở trên cùng của child

Chúng ta sẽ tái cấu trúc ví dụ trên thành

```jsx
var StoogeList = React.createClass({
  render: function () {
    return (
      <ul>
      {
        this.props.stooges.map(function (stooge) {
          return <li key={stooge.id}><Stooge/></li>;
        });
      }
      </ul>
    );
  }
});

var Stooge = React.createClass({
  render: function () {
    return <div>{this.props.stooge.name}</div>;
  }
});
```
Lưu ý rằng chúng ta phải chuyển key từ `<Stooge>` sang `<li>`. Đây thường là nguồn gốc của những sai lầm, khi cấu trúc đã được thay đổi nhưng key bị bỏ lại trong một nested element.

Các thuộc tính JSX không phải là JSON

Đây là lỗi ta thường mắc phải

```jsx
render: function () {
  return <div style={fontWeight: 'bold'}></div>
}
```
Bạn thấy vấn đề rồi chứ. Đáng lẽ ra phải là
```jsx
render: function () {
  return <div style={{fontWeight: 'bold'}}></div>
}
```
Bạn cần dấu ngoặc {} để đưa nó lại thành JavaScript và một {} khác để tạo đối tượng của mình

Tối ưu hóa? để sau nhé!!!

Xây dựng ứng dụng của bạn với giả định rằng nó sẽ chạy một cách mượt mà mà không cần tối ưu hóa. Còn rất lâu nữa giả định đó sẽ chính xác. Trong các trình duyệt hiện đại, JavaScript hoạt động rất nhanh, còn DOM thì rất chậm. React đang quan tâm đến vấn đề thứ hai nên bạn đừng lo lắng quá nhiều về code JavaScript còn sót lại của mình. React cung cấp cho bạn sự linh hoạt để refactor một cách dễ dàng, nhưng một khi bạn bắt đầu viết code theo cách tối ưu hóa, nó sẽ khó khăn hơn. Và caching sẽ xảy ra các lỗi ngoài dự kiến.

Nếu bạn thực sự khó chịu về vấn đề trình diễn code, hãy quay vòng suy nghĩ và bảo đảm các giải pháp sẽ có ý nghĩa đối với user. Đôi khi nếu React có vấn đề, user có lẽ cũng sẽ gặp khó khăn khi làm việc trong một UI không tốt.

Nếu thực sự cần phải trình diễn code, bạn có thể xem shouldComponentUpdate. Nó hoàn toàn nằm ngoài phạm vi của bài viết này, nhưng bạn cũng có thể dựa vào đó và nói rằng "Này React, chả có cái gì thay đổi đâu, hãy re-render đi."

Cuối cùng là, hãy bắt tay vào xây dựng một ứng dụng sử dụng React của bạn nhé!

Tài liệu tham khảo:

Nguồn tham khảo tại: https://zapier.com/engineering/react-js-tutorial-guide-gotchas/
http://facebook.github.io/react/docs/getting-started.html
http://jsfiddle.net/reactjs/69z2wepo/