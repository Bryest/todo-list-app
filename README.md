<!-- prettier-ignore-start -->

Tutorial [Link](https://mauriciogc.medium.com/react-creando-una-app-to-do-list-con-create-react-app-y-el-hook-usestate-6ae378569705)

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

1. Create react project

```shell
$ npx create-react-app my-todo-list-app
```

2. It allows to natively compile .scss files to css at incredible speed and automatically via a connect middleware
   [node-sass](https://www.npmjs.com/package/node-sass)

```shell
$ npm i node-sass
```

3. To run the project

```shell
$ npm start
```

4. App.js

```js
import logo from "./logo.svg";
import "./App.scss";

function App() {
  return <div className="App">Hello world</div>;
}

export default App;
```

5. Edit App.css to App.scss

6. App.scss

```scss
html {
  background: #ddd;
  height: 100%;
  display: flex;
}
body {
  width: 100%;
  margin: auto;
}
.App {
  font-family: sans-serif;
  text-align: center;
}
```

7. Our files are

```
📦src
┣ 📜App.js
┣ 📜App.scss
┣ 📜App.test.js
┣ 📜index.css
┣ 📜index.js
┣ 📜logo.svg
┣ 📜reportWebVitals.js
┗ 📜setupTests.js
```

8. Create Components directory and Container.jsx in src.

```
📦src
 ┣ 📂Components
 ┃ ┗ 📜Container.jsx
 ┣ ...
 ...
```

9. If you are in Visual Studio Code, you can write `rafce` and push enter. The code generated in `Container.jsx` is.

```js
import React from "react";

const Container = () => {
  return <div>Container</div>;
};

export default Container;
```

10. Write imp to import the `Container.jsx` and add it in the script

```js
import Container from "./components/Container";
import "./App.scss";

import React from "react";

const App = () => {
  return (
    <div className="App">
      <Container />
    </div>
  );
};

export default App;
```

11. Creamos los componentes FormTodo y TaskList.

12. Le agregamos codigo con `rafce`.

13. Agregamos los componentes a `Container.jsx`

```js
import React from "react";
import FormTodo from "./FormTodo";
import TaskList from "./TaskList";
const Container = () => {
  return (
    <div>
      Container
      <FormTodo />
      <TaskList />
    </div>
  );
};

export default Container;
```

14. Add Checkbox to TaskList

```js
import React from "react";
import Checkbox from "./Checkbox";
const TaskList = () => {
  return (
    <div>
      TaskList
      <Checkbox />
    </div>
  );
};

export default TaskList;
```

15. The files

```
📦src
 ┣ 📂components
 ┃ ┣ 📜Checkbox.jsx
 ┃ ┣ 📜Container.jsx
 ┃ ┣ 📜FormTodo.jsx
 ┃ ┗ 📜TaskList.jsx
 ┣ 📜App.js
 ┣ 📜App.scss
 ┣ ...
 ```

 16. We create this code in `FormTodo.jsx`.
 `description` and `setDescription` are our variables that its are going to help us in the next code.
 The `preventDefault` is to avoid refresh page after push the button to add an element.
 The `console.log(description)` is to see what we add in the form with the web console. 
 The directive `button` will be active if the value (`description`) of the input is not empty (`""`).
 We declarate our event handler `handleSubmit` for the form. We assign this variable for the `onSubmit` event. This event is a Js event that occurs when a form is `"submitted"`.
 When we push `enter` or we click the `button`, it execute `handleSubmit`, and we add `e.preventDefault()` to avoid refresh the page.
 And we clear `description` with `setDescription("")`. 

```js
 import React, { useState } from "react";

const FormTodo = (props) => {
  const [description, setDescription] = useState("");
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(description);
    setDescription("");
  };
  return (
    <form onSubmit={handleSubmit}>
      <div className="todo-list">
        <div className="file-input">
          <input
            type="text"
            className="text"
            value={description}
            onChange={(e) => setDescription(e.target.value)}
          />
          <button
            className="button pink"
            disabled={description ? "" : "disabled"}
          >
            Add
          </button>
        </div>
      </div>
    </form>
  );
};

export default FormTodo;
```

17. We add this lines of code to capture `props`.
And to make a method to generate the `Date` and handle if we add an item or not with the `done` boolean.

```js
const FormTodo = (props) => {
  const { handleAddItem } = props;    //Added
  const [description, setDescription] = useState("");
  const handleSubmit = (e) => {   
    e.preventDefault();
    console.log(description);
    //-----------Added-----------
    handleAddItem({
      done: false,
      id: (+new Date()).toString(),
      description,
    });
    //---------------------------
    setDescription("");
  };
  return (
```

18. This is the current code in FormTodo.jsx

```js
import React, { useState } from "react";

const FormTodo = (props) => {
  const { handleAddItem } = props;
  const [description, setDescription] = useState("");
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(description);

    handleAddItem({
      done: false,
      id: (+new Date()).toString(),
      description,
    });

    setDescription("");
  };
  return (
    <form onSubmit={handleSubmit}>
      <div className="todo-list">
        <div className="file-input">
          <input
            type="text"
            className="text"
            value={description}
            onChange={(e) => setDescription(e.target.value)}
          />
          <button
            className="button pink"
            disabled={description ? "" : "disabled"}
          >
            Add
          </button>
        </div>
      </div>
    </form>
  );
};

export default FormTodo;
```

19. In list we save all our added data.
With `handleAddItem` attribute and method we update the state `list`.

```js
import React, { useState } from "react";
import FormTodo from "./FormTodo";
import TaskList from "./TaskList";
const Container = () => {
  const [list, setList] = useState([]);   //Added
  //-----------Added-----------
  const handleAddItem = (addItem) => {    
    setList([...list, addItem]);    //Added
  };
  //---------------------------
  return (
    <div>
      Container
      <FormTodo handleAddItem={handleAddItem} />  {/*Added attribute and method*/}
      <TaskList />
    </div>
  );
};

export default Container;
```

20. And add `list` and `setList` attributes and states to `TaskList`.

```js
    ...
     <TaskList list={list} setList={setList} />
    ...
```

21. This is the complete code in `Container.jsx`

```js
import React, { useState } from "react";
import FormTodo from "./FormTodo";
import TaskList from "./TaskList";
const Container = () => {
  const [list, setList] = useState([]);

  const handleAddItem = (addItem) => {
    setList([...list, addItem]);
  };
  return (
    <div>
      Container
      <FormTodo handleAddItem={handleAddItem} />
      <TaskList list={list} setList={setList} />
    </div>
  );
};

export default Container;
```

22. Checkbox.jsx

```js
import React, { Fragment } from "react";

//My functional component
const Checkbox = (props) => {
  const {
    onChange,
    data: { id, description, done },
  } = props;
  return (
    <Fragment>
      {/* Just ADD !!!! */}
      <svg
        viewBox="0 0 0 0"
        style={{ position: "absolute", zIndex: -1, opacity: 0 }}
      >
        <defs>
          <path id="todo__line" d="M21 12.3h168v0.1z" />
          <path
            id="todo__box"
            d="M21 12.7v5c0 1.3-1 2.3-2.3 2.3H8.3C7 20 6 19 6 17.7V7.3C6 6 7 5 8.3 5h10.4C20 5 21 6 21 7.3v5.4"
          />
          <path id="todo__check" d="M10 13l2 2 5-5" />
          <circle id="todo__circle" cx="13.5" cy="12.5" r="10" />
        </defs>
      </svg>

      <label className="todo new-item">
        <input
          className="todo__state"
          name={id}
          type="checkbox"
          defaultChecked={done}
          onChange={onChange}
        />
        {/* Just ADD !!!! */}
        <svg
          xmlns="http://www.w3.org/2000/svg"
          xmlnsXlink="http://www.w3.org/1999/xlink"
          viewBox="0 0 200 25"
          className="todo__icon"
        >
          <use xlinkHref="#todo__line" className="todo__line" />
          <use xlinkHref="#todo__box" className="todo__box" />
          <use xlinkHref="#todo__check" className="todo__check" />
          <use xlinkHref="#todo__circle" className="todo__circle" />
        </svg>
        <div className="todo__text">{description}</div>
      </label>
    </Fragment>
  );
};

export default Checkbox;
```

23. TaskList.jsx

```js
import React from "react";
import Checkbox from "./Checkbox";
const TaskList = (props) => {
  const { list, setList } = props;

  const onChangeStatus = (e) => {
    const { name, checked } = e.target;
    const updateList = list.map((item) => ({
      ...item,
      done: item.id === name ? checked : item.done,
    }));
    setList(updateList);
  };

  const onClickRemoveItem = (e) => {
    const updateList = list.filter((item) => !item.done);
    setList(updateList);
  };

  const checkBox = list.map((item) => (
    <Checkbox key={item.id} data={item} onChange={onChangeStatus} />
  ));
  //list.length==0 -> No tasks and null
  //list.length>0  -> checkBox and button
  return (
    <div className="todo-list">
      {list.length ? checkBox : "No tasks"}
      {list.length ? (
        <p>
          <button className="button blue" onClick={onClickRemoveItem}>
            Delete all done
          </button>
        </p>
      ) : null}
    </div>
  );
};

export default TaskList;
```
<!-- prettier-ignore-end -->
