# `this`

> Created at: 10-10-2023

> Updated at: 10-10-2023

A function's this keyword behaves a little differently in JavaScript compared to other languages. It also has some differences between **_strict mode_** and **_non-strict_** mode.

In most cases, the value of this is determined by how a function is called (**runtime binding**). It can't be set by assignment during execution, and it may be different each time the function is called. The `Function.prototype.bind()` method can set the value of a function's `this` regardless of how it's called, and arrow functions don't provide their own this binding (it retains the this value of the enclosing lexical context).

In **non–strict** mode, this is always a reference to an object. In **strict mode**, it can be any value.

The value of this depends on in which context it appears: **function**, **class**, or **global**.
