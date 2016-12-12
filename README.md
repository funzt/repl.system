# funzt.repl.system

`[org.funzt/repl.system "0.1.0"]`

Reloaded workflow development tool for systems built with [component](https://github.com/stuartsierra/component).  Uses `clojure.tools.namespace.repl` for code reloading.

## Usage

1. Invoke `set-system-to-load!` with a system map representing unloaded state.
2. Invoke `(reset)` whenever you want a full stop/code reload/start
3. Goto 1 wehenever you want to spin up a different system

- `funzt.repl.system/system` has a `:system` entry with a running or stopped system.  This is where you access runtime instances of loaded components.  Access runtime facilities for dev use via `(get-in funzt.repl.system/system [:system <keyword-of-component-you-want>])`.  We recommend to set up little getters fn0s in your dev namespace for quicker access.
- You may explicitly use `start` and `stop` instead of `reset` but usually won't have to.
- `funzt.repl.system/system` has a `:status` map with `:started?` and `:stopped?` keys.  Usually you don't need it.

## What if `reset` fails?

If `reset` fails due to bad code you should fix your code and hit `reset` again.  If `reset` fails because a start method of a component has thrown, you likely have spawned headless IO facilities and should reboot the JVM.

## `clojure.tools.namespace.repl` gotcha

Sometimes `clojure.tools.namespace.repl` which is used to handle code reloading finds too much code like generated ClojureScript source on the classpath. Use `clojure.tools.namespace.repl/set-refresh-dirs` to narrow down the source pathes you want reloaded.

## Similar tools

We use this tool at [funzt.jetzt](http://funzt.jetzt) because it does as little as possible to provide a smooth reloaded workflow.  At the time we wrote this there were no similar tools.  Similar tools nowaday have features beyond our requirement and require more care than just invoking `(reset)`.

## License

Copyright © 2016 Leon Grapenthin & [funzt.jetzt](http://funzt.jetzt) UG (haftungsbeschränkt)

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
