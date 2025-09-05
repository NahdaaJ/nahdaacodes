# 🌸 electron to-do list app guide
The aim of this guide is to teach you how to make a simple Electron to-do list app for your desktop!

<br>

## ♡ table of contents
- [what is electron?](#-what-is-electron)
- [how i like to break this project down](#-how-i-like-to-break-this-project-down)
- [prerequisites](#-prerequisites)
- [step 1: create your project folder](#-step-1-create-your-project-folder)
- [step 2: initialise your project](#-step-2-initialise-your-project)
- [step 3: install electron](#-step-3-install-electron)
- [step 4: add your main files and folders](#-step-4-add-your-main-files-and-folders)
- [step 5: set up your main.js](#-step-5-set-up-your-mainjs)
- [step 6: set up your index.html](#-step-6-set-up-your-indexhtml)
- [step 7: add some style in styles.css](#-step-7-add-some-style-in-stylescss)
- [step 8: add your logic in renderer.js](#-step-8-add-your-logic-in-rendererjs)
- [step 9: run your app](#-step-9-run-your-app)
- [step 10: package your app](#-step-10-package-your-app)
- [what next?](#-what-next)
- [troubleshooting](#-troubleshooting)
- [find me elsewhere](#-find-me-elsewhere)

<br>

## ♡ what is electron?
Electron lets you build desktop apps using web technologies (HTML, CSS, JavaScript) and run them on Windows, Mac, and Linux!

<br>

## ♡ how i like to break this project down
This is how I broke the project down in my head before I started! It's a good idea to break down projects into stages like this before you start, it makes it less scary and more organised!

1. plan the UI (Figma)
2. download/check prerequisites, get your repo ready, initialise your project
3. create the UI, no functionality, JUST the way it looks
4. add logic, feature by feature. These are the most BASIC features you need:
    1. task entry + add button functionality
    2. add and display task
    3. delete task + delete display
    4. check/uncheck task
5. start adding more logic, any extra features you could want, such as:
    1. save to json, delete from json, update json
    2. minimise window, close window
    3. order tasks by checked/unchecked
6. package the app (turn it into an .exe, which is how it becomes a desktop app!)

Generally, you want to push to Git every time you finish a stage or substage. Make sure it works fully before you push! Also make sure to add a .gitignore that uses the `node` template. It should at the very least have these in it:
```plaintext
node_modules/
dist/
```

<br>

## ♡ prerequisites

before you start, make sure you have:
- **node.js** installed ([download here](https://nodejs.org/en/download/))
- **npm** (comes with node.js)
- **(optional but recommended) git** installed ([download here](https://git-scm.com/downloads))
- a code editor (like [visual studio code](https://code.visualstudio.com/))

check your setup in a terminal:
```sh
node -v
npm -v
git --version
```

if you don't understand what Git is or how to use it, follow [this guide](github-basics.md)! ♡

<br>

## ♡ step 1: create your project folder
open your terminal and run:
```sh
mkdir my-todo-list
cd my-todo-list
```

<br>

## ♡ step 2: initialise your project
run:
```sh
npm init -y
```
this creates a default `package.json` file.

<br>

## ♡ step 3: install electron
run:
```sh
npm install --save-dev electron
```
and then in your `package.json` add a start script like so:
```json
"scripts": { "start": "electron ." }
```
lastly, set `main.js` as your `main` in the `package.json`:
```json
"main": "main.js"
```

<br>

## ♡ step 4: add your main files and folders

create these files in your folder:
- `main.js` -> tells Electron what window to open
- `index.html` -> the text, buttons, images the user sees!
- `renderer.js` -> UI logic and functionality (such as what buttons do when you click them)
- `styles.css` -> optional but HIGHLY recommended, used to add styling and colours!
- `images/` –  a folder for your UI icons and images

<br>

## ♡ step 5: set up your main.js

this file starts your app window.

```js
const { app, BrowserWindow } = require('electron');

function createWindow() {
  const win = new BrowserWindow({
    width: 400,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false
    }
  });
  win.loadFile('index.html');
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});
```
>Normally, turning on `nodeIntegration` lets your HTML/JS code directly use Node.js features (like file system access). If your app ever loaded unsafe code (e.g. from the internet), a hacker could run malicious commands on your computer.

  `contextIsolation: false` makes it even easier for malicious scripts to mess with your app because it removes the “wall” between your app’s code and Electron’s internal processes.

  For real apps, keep nodeIntegration: false and contextIsolation: true, and expose only safe functions via a preload script (preload.js). Beginners can skip this for now ♡

<br>

## ♡ step 6: set up your index.html

this is your app’s layout.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>to-do list</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <h2>my to-do list</h2>
    <input type="text" id="task-input" placeholder="add a task...">
    <button onclick="addTask()">add</button>
    <ul id="task-list"></ul>
    <script src="renderer.js"></script>
  </body>
</html>
```

<br>

## ♡ step 7: add some style in styles.css

```css
body {
  font-family: sans-serif;
  background: #f7f7fa;
  margin: 40px;
  color: #222;
}

input, button {
  padding: 8px;
  margin: 4px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: #fff;
  margin: 6px 0;
  padding: 8px;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

<br>

## ♡ step 8: add your logic in renderer.js

```js
const input = document.getElementById('task-input');
const list = document.getElementById('task-list');

function addTask() {
  const text = input.value.trim();
  if (text === '') return;
  const li = document.createElement('li');
  li.textContent = text;

  // add a delete button
  const delBtn = document.createElement('button');
  delBtn.textContent = 'delete';
  delBtn.onclick = () => list.removeChild(li);

  li.appendChild(delBtn);
  list.appendChild(li);
  input.value = '';
}

// allow enter key to add task
input.addEventListener('keydown', function(event) {
  if (event.key === 'Enter') addTask();
});
```

<br>

## ♡ step 9: run your app
in your terminal:
```sh
npm start
```
your to-do list app should open in a window!

<br>

## ♡ step 10: package your app
once you have completely finished your app, do this in the terminal to package it!
packaging an app means taking all your project files and bundling them into a **standalone program** (like a .exe on Windows or an .app on Mac) so you can run it without typing npm start. it’s how your project becomes a real desktop app you can share with others!
```sh
npm install --save-dev electron-packager
npx electron-packager . "Your App Name" --out=dist --icon=YourAppIcon.ico
```
You can choose the name of your app and the icon you want it to have!! make sure your icon is in ico format (you can use online converters) and replace with the name of your app and the name of the file into the line! ♡

If you specifically want Windows x64:
```sh
npx electron-packager . "Your Desired App Name" --platform=win32 --arch=x64 --out=dist --icon=YourAppIcon.ico
```
>You usually need to package on each OS you’re targeting. Code signing isn’t required for personal use, but SmartScreen/Gatekeeper may warn when sharing apps!

<br>

## ♡ what next?
- try changing the colours in `styles.css`
- add a way to mark tasks as completed
- save tasks to a file (advanced)
- customise the window size or title

<br>

## ♡ troubleshooting
- if you get errors, check you installed node.js and electron
- make sure your file names match the code above
- utilise google, reddit, stack overflow and chatgpt to search for error messages online, lots of beginners have the same questions!
- feel free to reach out to me as well if you want!

<br>

## ♡ find me elsewhere
i'm just a junior software engineer, so I'm learning new things all the time too! Never feel bad about not knowing something, just keep going and you'll get there. ♡

- tiktok: [@nahdaacodes](https://tiktok.com/@nahdaacodes)
- github: [@nahdaaj](https://github.com/nahdaaj)
- personal website: [nahdaajawed.com](https://nahdaajawed.com/)

feel free to reach out if you have any suggestions, ideas or just need help understanding something!
i'd love to meet you 🖤