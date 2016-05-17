# readline

A readline port for and in zepto.
Supports history and moving around; emacs-style keybindings
are in the works and [partially supported](#emacs-bindings).

## Usage

The library exposes two endpoints `readline` and `add-history`.
They behave as the usual readline endpoints do.

```clojure
(load "readline/readline")
(define readline (import "readline:readline"))

(define (evaluate)
  (eval (string:parse (readline "enter something to evaluate>"))))
(evaluate) ; => will prompt you to enter something that should be eval'd and do so
```

You can also easily build a minimal REPL on top of that.

```clojure
(load "readline/readline")
(define readline (import "readline:readline"))
(define add-history (import "readline:add-history"))

(define (repl)
  (let* ((str (readline "repl>"))
         (x (eval (string:parse str))))
    (begin
      (display "=> ")
      (write x)
      (add-history str)
      (repl))))
(repl)
```

## Emacs Bindings

The following key bindings are currently supported:

* Ctrl+a: Moves the cursor to the beginning of the line.
* Ctrl+b: Moves the cursor back one character (equivalent to backspace).
* Ctrl+e: Moves the cursor to the end of the line.
* Ctrl+f: Moves the cursor forward one character.
* Ctrl+j: Equivalent to the enter key.
* Ctrl+n: Moves back in history.
* Ctrl+p: Moves forward in history.
* Ctrl+r: [EXPERIMENTAL!] Searches in the history.

That's all folks!

<hr/>

Have fun!
