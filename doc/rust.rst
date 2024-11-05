============
 Rust links
============

* `Learn rust link <https://www.rust-lang.org/learn>`_

* `The Rust programming language <https://doc.rust-lang.org/book/title-page.html>`_ [#f1]_.

* `Rust book experiment (brown.edu) - includes quizes! <https://rust-book.cs.brown.edu/experiment-intro.html>`_ [#f6]_
  
* `The cargo book <https://doc.rust-lang.org/cargo/>`_

* Cargo recognises `semantic versioning <https://semver.org/>`_

* `The rust standard library`_.

* `crates.io <https://crates.io/>`_ "Crates.io is where people in the
  Rust ecosystem post their open source Rust projects for others to
  use."

The rust programming language book
----------------------------------

The rust book calls rust programmers 'rustaceans'.

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
 - references must be always valid - rust checks this with lifetimes [#f5]_ and ownership.

`Rust (wikipedia)`_, this includes a `video`_ in webm by Emily Dunham at
linux.conf.au in 2017. 

`The Rust Cookbook
<https://rust-lang-nursery.github.io/rust-cookbook/>`_ [#f2]_

`The Rust Reference <https://doc.rust-lang.org/nightly/reference/>`_
[#f3]_

`The Rust Standard Library`_ [#f4]_
.. _`The Rust Standard Library`: https://doc.rust-lang.org/nightly/std/index.html

.. _`Rust (wikipedia)`: https://en.wikipedia.org/wiki/Rust_(programming_language)
.. _`video`: https://upload.wikimedia.org/wikipedia/commons/5/5c/Rust_101.webm

Emily Dunham "Should you rewrite in Rust?" `(youtube)
<https://www.youtube.com/watch?v=6jqy-Dizd0I>`_ (45 min) LinuxConfAu
2018, Sydney

http://talks.edunham.net/lca2018/should-you-rewrite-in-rust/

.. rubric:: Footnotes
	    
.. [#f1] Accessed on 17 August 2019.

.. [#f2] Accessed on 6 Oct 2019.

.. [#f3] Accessed on 6 Oct 2019.
	 
.. [#f4] Accessed on 6 Oct 2019.
 
.. [#f5] Still a topic to learn as I write this.

.. [#f6] The content was different to the rust book when checking in Nov 2024.         
