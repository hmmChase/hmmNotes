# _Debugging_

---

# _Sourcemaps_

- A mapping between the generated/transpiled/minified JavaScript file and one or more original source files
- The main purpose of sourcemaps is to aid debugging
- If there’s an error in the generated code file, the map can tell you the original source file location

---

# _Console_

## Sources

### Breakpoints

- standard
  - click on the the gutter of the line you want to set a breakpoint on
- conditional
  - set standard breakpoint, right-click it, select edit breakpoint
  - will break if the condition evaluates to true

### Navigation bar

- Resume
  - continues running code until hits another breakpoint
- Step-over
  - When paused on a line of code containing a function that's not relevant to the problem you're debugging, click **Step over** to execute the function without stepping into it.
  - steps through code line-by-line
  - will step over any function calls so focus remains inside current scope
- Step-into
  - When paused on a line of code containing a function call that is related to the problem you're debugging, click **Step into** to investigate that function further.
  - steps through code line-by-line
  - will step into any functions calls
- Step-out
  - When paused inside of a function that is not related to the problem you're debugging, click **Step out** to execute the rest of the function's code.
  - will step out of current scope and move execution to parent function
- Step
  - ?

### Watches

- allows you to keep an eye on something
- adding to the watchlist
  - select some code, right click, add selected text to watches
  - click the +, type in any expression you would type into a console.log

### Call Stack

- only shows function calls

### Scope

- view and edit the values of properties and variables in the local, closure, and global scopes

### Snippets

- In the navigator pane, click the Snippets tab
- Useful for running debug code

---

## Black Boxing

- When you blackbox a source file/folder, the debugger will not jump into that file when stepping through code you're debugging
- DevTools → Settings → Blackboxing

* patterns:
  - `^https:\/\/`, basically block any CDN-hosted libraries (greedy, but I’d prefer to be implicit)
  - `plugins`, I like to put all locally hosted and manually installed libraries/plugins in this directory (when not using a package manager to manage dependencies)
  - `\.min\.js$`, for all minified sources
  - `node_modules` and `bower_components`, for package manager dependencies
  - `~`, home, for dependencies in a Webpack bundle
  - `bundle.js`, it’s a bundle itself (we use sourcemaps, don’t we?)
  - (`webpack)-hot-middleware` — “Hot Module Replacement”, (HMR) is a feature to inject updated modules into the active runtime.
