Functional Programming and Git Usage
=====================================

.. admonition:: Goals

    - Learn what functional programming is
    - Learn Elm syntax
    - Learn basic Git workflow
    - Learn basic Git branching

Functional Programming
----------------------

Basic idea: **Functions as first class citizens**.

This means that in functional programming language, functions are **values** like other data types, eg. integers and strings.

In this course we will use a simple expression language called `Elm <https://elm-lang.org/>`_ to learn functional programming.

Expressions
^^^^^^^^^^^^

Informally, expressions are the things that can somehow be evaluated. For example, in C, the following are expressions:

.. code-block:: c

    0
    (1 + 2) * 3
    "hello"
    'a'
    NULL
    true

What are the basic expressions in Elm?

Try to find some data types in Elm by using ``elm repl``.

Types
^^^^^^

What are types? Type is actually another word for "Set" (mathematically). Set is a collection of things. For example, the set of all integers is a type. The set of all strings is a type.

In Elm, the basic data types (defined internally) are:

- Int
- Float
- Char
- String (Somehow you can regard this as a list of Char)
- Bool

What about functions? What about lists?

Functions are also values, so they have types. To describe their types, we use the arrow notation. For example, the type of a function that takes an integer and returns an integer is ``Int -> Int``. The type of a function that takes a string and returns a string is ``String -> String``.

.. note:: Exercises

    What is the type of the following C function?

    .. code-block:: c

        int f(int x, int y) {
            return x + y;
        }
    
If the function takes 0 argument, it has the unit type ``()``.

Consider function ``F`` which has type ``Int -> Float -> String``. What is the type of ``F 1``? What is the type of ``F 1 2.0``?

What's the difference between ``F`` and ``Int -> (Float -> String)`` and ``(Int -> Float) -> String``?

Sum Type and Product Type
^^^^^^^^^^^^^^^^^^^^^^^^^

Sum type is a type that has multiple elements. For example, the type ``Bool`` has two constructors: ``true`` and ``false``. Hence we say that ``Bool`` is a sum type (often denoted as :math:`1+1=2`).

Product type is a type that is the Cartesian product of some types (maybe different). For example, the type ``(Int, Float)`` is a product type. The tuple type is often denoted as :math:`\tau_1 \times \tau_2`. In Elm you can also have a tuple of three elements, which is denoted as :math:`\tau_1 \times \tau_2 \times \tau_3`. There are no other tuples.

Inductive Types
^^^^^^^^^^^^^^^

Elm allows you to define inductive types.

Inductive types are types that are defined inductively. For example, the natural number type ``Nat`` can be written as:

- O: Nat
- S Nat: Nat

In Elm, you write:

.. code-block:: elm

    type Nat = O | S Nat

Here ``O`` and ``S`` are called the type constructors of ``Nat``.

The type of ``Nat`` can be denoted as :math:`\mu t. 1 + t`.

.. note:: think

    What is the type of ``S``? What is the type of ``O``?

Parametric Polymorphism
^^^^^^^^^^^^^^^^^^^^^^^^

Elm supports parametric polymorphism. This means that we can write functions that work on any type.
You can think it as the template functions in C++.
For example, the identity function ``identity`` has type ``a -> a``.

The types may also have type arguments.

For example, we can define the ``List`` type. Note that list only contains one type of elements.

``Maybe a`` type is also a parametric type. It is defined as follows:

.. code-block:: elm

    type Maybe a = Just a | Nothing

For example, ``Just 1`` has type ``Maybe Int``.

What is the type of ``Just``? And, **what is the type of ``Maybe``**?

You need to know the difference between ``Maybe`` and ``Just``.

``Maybe`` has a higher level type, which is ``* -> *`` (level 1 type).

``Just`` has type ``a -> Maybe a`` (level 0 type).

Level (n+1) type is the set of all level n types.

In Elm (and Haskell), you only have level 0 and level 1 types.

The concept of levels are mainly used to solve the `Russel's paradox <https://en.wikipedia.org/wiki/Russell%27s_paradox>`_.

Read `What is type of type <https://www.avestura.dev/blog/what-is-the-type-of-type>`_ if you are interested in this topic.

Record data
^^^^^^^^^^^^

Record data is a data type that has named fields. For example, we can define a record type ``Person`` as follows:

.. code-block:: elm

    type alias Person = { name: String, age: Int }

Then we can create a person:

.. code-block:: elm

    person = { name = "John", age = 20 }

It's pretty much similar to the ``struct`` in C.

Pattern Matching
^^^^^^^^^^^^^^^^^

Pattern matching is one of the expression. It is used to match the value of a sum type (case analysis).

For example, we have a data ``d`` of type ``Maybe Int``. We can use pattern matching to check whether ``d`` is ``Just`` or ``Nothing``, and get the value of ``Just``.

.. code-block:: elm

    case d of
        Just x -> x
        Nothing -> 0

Note that the every branch of the pattern matching must have the same type, so in the above example, we know that ``x`` has type ``Int``.
