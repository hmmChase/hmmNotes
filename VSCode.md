# _VSCode_

---

# _Shortcuts_

- https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf

## _UI_

- Command palette
  - `Ctrl + P`
  - start typing with a `>` to get a list of available tasks.
  - start typing an `@` to get a list of symbols in the current file.

## _Terminal_

- Show integrated terminal
  - `Ctrl +` `
- Create new terminal
  - `Ctrl + Shift + ``

* `Ctrl + Q`
  - workbench.action.quickOpenView
* `Ctrl + W`
  - workbench.action.closeWindow
* `Ctrl + E`
  - eslint.executeAutofix
* `Ctrl + R`
  - editor.action.formatDocument

- `Ctrl + A`
  - editor.action.selectAll
- `Ctrl + S`
  - workbench.action.files.save
- `Ctrl + D`
  - editor.action.addSelectionToNextFindMatch
- `Ctrl + F`
  - actions.find

* `Ctrl + Z`
  - undo
* `Ctrl + X`
  - editor.action.clipboardCutAction
* `Ctrl + C`
  - editor.action.clipboardCopyAction
* `Ctrl + V`
  - editor.action.clipboardPasteAction

- `Ctrl + Space`
  - editor.action.triggerSuggest
- `Ctrl + Shift + Space`
  - editor.action.triggerParameterHints
- ## `Shift + Space`
- `Ctrl + Enter`
  - editor.action.insertLineAfter
- ## `Shift + Enter`
- `Control + /`
  - editor.action.commentLine
- `Alt + UpArrow`
  - editor.action.moveLinesUpAction
- `Alt + DownArrow`
  - editor.action.moveLinesDownAction
- `Alt + Click`
  - multi cursor modifer
- `Ctrl + Shift + K`
  - editor.action.deleteLines
  -

* F1
  - workbench.action.showCommands
* F2
* F3
* F4
* F5
* F6
* F7
* F8
* F9
* F10
* F11
* F12 or Ctrl + Click
  - editor.action.goToDeclaration
  - Alt + F12 or hold Ctrl
    - editor.action.previewDeclaration

- Middle Mouse button
- Side Mouse Button

* ## Might be useful

## _Debugging_

- workbench.action.debug.start
  - `F5`
- editor.debug.action.toggleBreakpoint
  - `select + F9`
- editor.debug.action.toggleInlineBreakpoint
  - `select + Shift + F9`
- editor.debug.action.conditionalBreakpoint
  - RC
- editor.debug.action.toggleLogPoint
- editor.debug.action.runToCursor
- editor.debug.action.selectionToRepl
- editor.debug.action.selectionToWatch
- editor.debug.action.goToNextBreakpoint
- editor.debug.action.goToPreviousBreakpoint
- inDebugMode
  - workbench.action.debug.continue
    - Continue to next breakpoint
    - Or stop if not more breakpoints
    - `F5`
  - ## workbench.action.debug.pause
  - workbench.action.debug.restart
    - `Ctrl + Shift + F5`
  - workbench.action.debug.stepOver
    - `F10`
  - workbench.action.debug.stepInto
    - `F11`
  - workbench.action.debug.stepOut
    - `Shift + F11`
  - workbench.action.debug.stop
    - `Shift + F5`
  - editor.debug.action.showDebugHover
    - `select + Ctrl + k Ctrl + i`

## _Extentions_

- Turbo Console Log
  - turboConsoleLog.displayLogMessage
    - `select + Ctrl + g`
- Dashboard
  - dashboard.open
    - `Ctrl + F1`

* ???
  - https://marketplace.visualstudio.com/items?itemName=remimarsal.prettier-now#review-details
  - https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-stylefmt#review-details

```
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${file}"
    }
  ]
}
```

---

# _Debugging_

- https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome
- https://github.com/Microsoft/vscode-recipes
- https://www.youtube.com/watch?v=6cOsxaNC06c
- https://www.youtube.com/watch?v=UcW1FHNvy8M
- https://medium.com/@auchenberg/live-edit-and-debug-your-react-apps-directly-from-vs-code-without-leaving-the-editor-3da489ed905f

## Debugger for Chrome

- Setup
  - Windows
    - Right click the Chrome shortcut, and select properties
    - In the "target" field, append `--remote-debugging-port=9222`
    - Or in a command prompt, execute `<path to chrome>/chrome.exe --remote-debugging-port=9222`

* Two modes:
  - Launch an instance of Chrome navigated to your app
  - Attach to a running instance of Chrome
  - Both modes requires you to be serving your web application from local web server
  - The best way to explain the difference between launch and attach is to think about [launch configurations](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) as a recipe for how to start your app in debug mode before VS Code attaches to it, while an [attach config](https://code.visualstudio.com/docs/editor/debugging#_launchjson-attributes) is a recipe for how to connect VS Code's debugger to an app or process that's already running.
  - The value of [launch configurations](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) is that they give you a way to offload some of the cognitive overhead of launching your app with the right debugging parameters by creating a configuration that's repeatable and sharable with your project and team.

- Traditional debugging workflows are most focused around slowing down execution to inspect program logic, while logging workflows usually involve inspecting program state and how it changes during the normal execution of an application. The fundamental observation here is that the two techniques are used for different debugging purposes.
- Auto Attach for Node, that enables the Node debugger to automatically attach to Node.js processes that have been launched in debug mode from VS Code's Integrated Terminal.
- You enable auto attach by running Debug: Toggle Auto Attach command from the Command Palette, and once activated you can toggle auto attach from the Status Bar as well.
- This feature completely eliminates any debug configuration, as we interpret any Node.js process started with `node --inspect` as an intent to debug.
- If you run `npm run debug` and the `"debug"` script is `"node --inspect"` or any other command that includes `--inspect`, then auto attach will detect that and attach the debugger 🎉

### Logpoints

- A Logpoint is a breakpoint variant that does not "break" into the debugger but instead logs a message to the console.
- Logpoints allows you to "inject" on-demand logging statements into your application logic, just like if you had added logging statements into your application before starting it. Logpoints are injected at execution time and not persisted in the source code, so you don't have to plan ahead but can inject Logpoints as you need them. Another nice benefit is that you don't have to worry about cleaning up your source code after you are finished debugging.

### Configs

```
{
  "type": "chrome",
  "request": "attach",
  "name": "Attach to Chrome",
  "port": 9222,
  "url": "127.0.0.1:9222",
  "webRoot": "${workspaceFolder}"
}

{
  "type": "chrome",
  "request": "launch",
  "name": "Launch Chrome",
  "url": "http://localhost:5500",
  "webRoot": "${workspaceFolder}"
}

{
  "type": "chrome",
  "request": "launch",
  "name": "Attach to Chrome React",
  "url": "http://localhost:3000",
  "webRoot": "${workspaceRoot}/src",
  "skipFiles": ["node_modules/**/*.js"]
}
```

---

# _Tips_

## Rename All Occurrences

- Select a variable/method and hit F2
- ou can edit the name and it will change every instance of that variable’s name throughout the entire current working project

## Go to Definition

- Press Ctrl key and click the variable/method with your mouse. VS Code will take you to it’s definition right away
- Or you could just hover your cursor over the variable/method along with pressing the Command (on Mac) or Ctrl (on Windows) key, it will shows you the definition right in line where your cursor is

## Edit Multiple Lines at Once

- To insert or delete multiple instances of text throughout a document, all you have to do is create multiple cursors
- You can do this by holding down Alt and clicking anywhere in the text
- Every click creates a new cursor

---

# _Misc_

- VS Code provides two different scopes for settings:
  - User Settings
    - Settings that apply globally to any instance of VS Code you open
  - Workspace Settings
    - Settings stored inside your workspace and only apply when the workspace is opened

## Themes

- https://vscodethemes.com/
- https://marketplace.visualstudio.com/search?target=VSCode&category=Themes&sortBy=Downloads

---
