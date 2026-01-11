============
 Rust links
============

* `Learn rust link <https://www.rust-lang.org/learn>`_

* `The Rust programming language <https://doc.rust-lang.org/book/title-page.html>`_ [#f1]_.

* `Rust book experiment (brown.edu) - includes quizes! <https://rust-book.cs.brown.edu/experiment-intro.html>`_ [#f2]_

  Related to this, there is a Jane Street talk by `Will Critchton <https://willcrichton.net/>`_ from Brown Univ. that mentions `aquascope`.
  I believe it is this link here: https://cel.cs.brown.edu/aquascope/

* `Rust by example <https://doc.rust-lang.org/stable/rust-by-example/>`_

* `The cargo book <https://doc.rust-lang.org/cargo/>`_

  See more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

* Cargo recognises `semantic versioning <https://semver.org/>`_

* `The rust standard library <https://doc.rust-lang.org/nightly/std/index.html>`_.

* `The Rust Reference <https://doc.rust-lang.org/nightly/reference/>`_

* `MacroKata - like rustlings, but for macros in rust <https://github.com/tfpk/macrokata>`_

* `The little book of rust macros <https://veykril.github.io/tlborm/>`_

* `The rust playground <https://play.rust-lang.org/>`_

* `crates.io <https://crates.io/>`_ "Crates.io is where people in the
  Rust ecosystem post their open source Rust projects for others to
  use."

* `The Rustonomicon <https://doc.rust-lang.org/nomicon/intro.html>`_, book that
  goes into `the awful detail that you need to understand when writing unsafe rust` and it `assumes considerable prior knowledge`.

  Be warned of UNLEASHING INDESCRIBABLE HORRORS THAT SHATTER YOUR PSYCHE AND SET YOUR MIND ADRIFT IN THE UNKNOWABLY INFINITE COSMOS.

The rust programming language book
----------------------------------

`Chapter 1
<https://doc.rust-lang.org/book/ch01-00-getting-started.html>`_ is an
introduction to the basic tools, including cargo and the installation
of the tools.

`Chapter 2
<https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html>`_
starts a 'guessing game' program. This starts by using simple
input/output with the std::io package.

There is a few examples of 'cargo' when one starts using the rand::Rng
package, including the commands 'cargo doc', 'cargo build', 'cargo
update'.

The documentation example::

  cargo doc --open

`Chapter 4
<https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html>`_
talks about ownership, the very special rust concept:

 - Each value in rust has an owner
 - There can only be one owner at a time
 - When the owner goes out of scope, the value will be dropped.

Other things discussed are cloning, the Copy trait of a type, the `drop`
method (that implements the Drop trait).

For function calls, passing a variable to a function will move or
copy, just as assignment does.

The section on references explains the method as a way to avoid
the (protocol) of getting ownership when entering a function and
returning ownership on function return.

Normal references are not mutable. Adding `mut` changes the reference
to mutable reference.  Mutable references have one big restriction: if
you have a mutable reference to a value, you can have no other
references to that value.

Rust prevents the problem of `data races` by refusing to compile code
with data races!

Rules of references:

 - you can have either one mutable reference (read/write) or any
   number of immutable references. (Swimmer, single write, multiple read).
 - references must be always valid - rust checks this with lifetimes [#f3]_ and ownership.

The chapter about fixing unsafe programs revealed to me a lack of
understanding and the use of several methods:

 - references
 - indirection
 - static storage
 - borrow checker
 - ownership
 - read/write/ownership
 - lifetime of referred data

Methods to extend the lifetime (for the example of a function returning a string reference):

 - Move ownership by returning a String ( -> String )
 - Return a string literal ( -> &'static str )
 - Defer borrow checking to runtime using reference counted pointer ( -> Rc<String> )
 - Have the caller provide a "slot" (signature includes "output: &mut String")

The topics are: returning a reference, enough permissions, aliasing
and mutating a data structure

Only now after reading `chapter 5 <https://rust-book.cs.brown.edu/ch05-03-method-syntax.html>`_,
I realise that there are these properties on a variable:

 * readable (yes/no)
 * writeable (yes/no)
 * ownership (yes, no)

The `mut` keyword is needed for the `writeable` property.

The readable property is available on the variable and its references,
unless the ownership is gone and the access would be undefined.

`Chapter 6
<https://rust-book.cs.brown.edu/ch06-01-defining-an-enum.html>`_
introduces the Option<T> enum. Its `documentation
<https://doc.rust-lang.org/std/option/enum.Option.html>`_ is useful.


The Rust Cookbook
-----------------

There is an abandoned version `here
<https://rust-lang-nursery.github.io/rust-cookbook/>`_
and a better updated version by `jamesgraves <https://github.com/jamesgraves/rust-cookbook>`_ at this location:
`link <https://jamesgraves.github.io/rust-cookbook/intro.html>`_ [#f4]_

Rust training from microsoft
----------------------------

`Take your first steps in rust <https://learn.microsoft.com/en-us/training/paths/rust-first-steps/>`_ [#f5]_

`A char in rust is a 21-bit integer that is padded to be 32-bits wide`
Includes link to `documentation for char. <https://doc.rust-lang.org/std/primitive.char.html>`_


Old video link
--------------

Emily Dunham "Should you rewrite in Rust?" `(youtube1)
<https://www.youtube.com/watch?v=6jqy-Dizd0I>`_ (45 min) LinuxConfAu
2018, Sydney

http://talks.edunham.net/lca2018/should-you-rewrite-in-rust/

Aaron Turon (Mozilla) "The Rust Programming Language"
`(youtube2) <https://www.youtube.com/watch?v=O5vzLKg7y-k>`_ (65 min)
Stanford Seminar, 12 March 2015

Some more rust-related talks from Jane Street's tech-talks
https://www.janestreet.com/tech-talks/

Conferences
-----------

`Splashcon 2024 IWACO <https://2024.splashcon.org/home/iwaco-2024>`_

`Splashcon 2025 <https://2025.splashcon.org/>`_

.. rubric:: Footnotes

.. [#f1] Accessed Nov 2024

.. [#f2] The content was different to the rust book when checking in Nov 2024.

.. [#f3] Still a topic to learn as I write this.

.. [#f4] Accessed on 24 Nov 2024

.. [#f5] Accessed on 30 Nov 2024
