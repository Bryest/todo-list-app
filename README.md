<!-- prettier-ignore-start -->

Tutorial [Link](https://mauriciogc.medium.com/react-creando-una-app-to-do-list-con-create-react-app-y-el-hook-usestate-6ae378569705)

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

1. Create react project

```shell
$ npx create-react-app my-todo-list-app
```

2. It allows to natively compile .scss files to css at incredible speed and automatically via a connect middleware
   [node-sass](https://www.npmjs.com/package/node-sass])

```shell
$ npm i node-sass
```

3. To run the project

```shell
$ npm start
```

4. App.js

```js
import logo from './logo.svg';
import './App.scss';

function App() {
  return (
    <div className="App">Hello world</div>
  );
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
import React from 'react'

const Container = () => {
  return (
    <div>Container</div>
  )
}

export default Container
```

10. Write imp to import the `Container.jsx` and add it in the script

```js
import Container from './components/Container';
import './App.scss';

import React from 'react'

const App = () => {
  return (
    <div className="App"><Container/></div>
  );
}

export default App
```
<!-- prettier-ignore-end -->
