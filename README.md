# readline

A readline port for and in zepto.
Supports history and moving around; emacs-style keybindings
are in the works (right now, `Ctrl-A` will move to the
beginning of the line and `Ctrl-E` will move to the end
of the line).

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

That's all folks!

<hr/>

Have fun!
