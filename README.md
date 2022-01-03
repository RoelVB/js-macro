# macro.js
A npm package that lets you automate your windows desktop.
> [Beta] not on npm yet!

## Example
- Simple cursor usage
```js
const { cursor } = require("macro.js");

cursor.position();
// { x: 679, y: 0 }

cursor.move(0, 0);
// cursor is now at the very left top of the screen

cursor.leftClick();
```
- Typing something on notepad
```js
const { Worker, isMainThread } = require("worker_threads");
const { execSync } = require("child_process");
const { window } = require("macro.js");

if (!isMainThread) {
    execSync("notepad.exe");
} else {
    // we don't want for execSync to wait for notepad to exit,
    // so we should use a worker instead
    void new Worker(__filename);
    
    // wait for notepad to start
    setTimeout(() => {
        const notepad = window.find("Untitled - Notepad");
        
        if (!notepad) {
            return console.error("error: cannot find notepad :(");
        }
        
        const textBox = notepad.getChild().find(x => x.getClassName() === "Edit");
        
        if (!textBox) {
            return console.error("error: cannot find text box :(");
        }
        
        textBox.type("Hello, World!");
    }, 1000);
}
```

## Building
To build the library and it's dependencies, you need:

- Visual C++ Build Environment
- Powershell v5.0+

To install the dependencies, open powershell and do the following:
```ps1
cd deps
.\install.ps1
```
To build the library, go to the root directory and do the following:
```bat
npm i -g node-gyp
node-gyp rebuild
```
