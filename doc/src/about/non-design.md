What Rhai Isn't
===============

{{#include ../links.md}}

Rhai's purpose is to provide a dynamic layer over Rust code, in the same spirit of _zero cost abstractions_.
It doesn't attempt to be a new language. For example:

* No classes.  Well, Rust doesn't either. On the other hand...

* No traits...  so it is also not Rust. Do your Rusty stuff in Rust.

* No structures/records - define your types in Rust instead; Rhai can seamlessly work with _any Rust type_.

  There is, however, a built-in [object map] type which is adequate for most uses.
  It is possible to simulate [object-oriented programming (OOP)][OOP] by storing [function pointers]
  in [object map] properties, turning them into _methods_.

* No first-class functions - Code your functions in Rust instead, and register them with Rhai.

  There is, however, support for simple [function pointers] to allow runtime dispatch by function name.

* No garbage collection - this should be expected, so...

* No closures - do your closure magic in Rust instead; [turn a Rhai scripted function into a Rust closure]({{rootUrl}}/engine/call-fn.md).

  But you can [curry][currying] a [function pointer] with arguments to simulate it somewhat.

* No byte-codes/JIT - Rhai has an AST-walking interpreter which will not win any speed races. The purpose of Rhai is not
  to be extremely _fast_, but to make it as easy as possible to integrate with native Rust applications.


Do Not Write The Next 4D VR Game in Rhai
---------------------------------------

Due to this intended usage, Rhai deliberately keeps the language simple and small by omitting advanced language features
such as classes, inheritance, first-class functions, closures, concurrency, byte-codes, JIT etc.

Avoid the temptation to write full-fledge application logic entirely in Rhai - that use case is best fulfilled by
more complete languages such as JavaScript or Lua.


Thin Dynamic Wrapper Layer Over Rust Code
----------------------------------------

In actual practice, it is usually best to expose a Rust API into Rhai for scripts to call.

All the core functionalities should be written in Rust, with Rhai being the dynamic _control_ layer.

This is similar to some dynamic languages where most of the core functionalities reside in a C/C++ standard library.

Another similar scenario is a web front-end driving back-end services written in a systems language.
In this case, JavaScript takes the role of Rhai while the back-end language, well... it can actually also be Rust.
Except that Rhai integrates with Rust _much_ more tightly, removing the need for interfaces such
as XHR calls and payload encoding such as JSON.
