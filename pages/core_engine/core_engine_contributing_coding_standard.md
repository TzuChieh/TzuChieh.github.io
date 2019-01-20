---
title: Coding Standard
keywords: 
last_updated: January 20, 2019
summary: "The development of the core of Photon complies to a collection of rules."
sidebar: core_engine_sidebar
permalink: core_engine_contributing_coding_standard.html
---

## Why

It is benefitial to have a common coding style to follow with, the reasons are:

* readability
* code is written by one person, but viewed multiple times by others
* 80% of the lifetime cost of a piece of software goes to maintenance (from UE4)
* readability
* sometimes higher level concepts can be implied by the layouts
* readability

This guideline is for coding in C++ since most of the code for engine is written in it; nonetheless, some concepts can be applied to other parts of Photon (and is encouraged). You do not need to follow all these rules strictly as long as you have a good reason that doing the other way is better for the context.

## Language and Naming

* Follow C++17 standard, try to use standard features only.
* Class names are in capitalized camel case, e.g., `SomeClassName`.
* Namespaces and function names are in lower case and underscore separated, e,g., `some_name`.
* Member variables should have `m_` prefix.
* Local variables and methods are camel case and uncapitalized, e.g., `worldToLocal`.
* Try not to use abbreviations, except for
  * `num` for number
  * `pos` for position
  * `dir` for direction
  * common abbreviations in graphics
  * common abbreviations in mathematics
  * formulae in referenced papers
* Classes that defines an interfaces should have a `I` prefix, e.g., `IFileSystem`.
* Name a variable in plural if it is a collection.
* Boolean variables and methods should ask a question, e.g., `m_isRunning`, `hasMaterial()`.
* Use `#pragma once`. Do **not** use macro-based header guards.
* Use `PH_ASSERT` for runtime assertions. See [`Engine/Source/Common/assertion.h`](https://github.com/TzuChieh/Photon-v2/blob/master/Engine/Source/Common/assertion.h).

## Filename Extensions and Includes

* `.h` for header files
* `.cpp` for source code
* `.ipp` for template implementations
* Include directives should have the following order (with each category separated by a blank line):
  1. Engine Headers
  2. Library Headers
  3. Third-party Library Headers
  4. Standard Headers

## Formatting

* Curly braces should have their own line.
* Operators surrounded by spaces.
* No spaces around brackets and parentheses.
* Try not to declare multiple variables in single line.
* Indent with tabs and align with spaces.
* Do **not** write comments that states obvious things.

## C++ Syntax

* Add `const` to anything that is intended to be a constant.
* Add `const` to methods if it will not alter the state of the object.
* Add `override` when overriding virtual methods, do not repeat `virtual` in this case.
* Add a virtual destructor if the object is intended to be used polymorphically.
* Use `static_assert` if you have assumptions that can be verified in compile time.
* Use `nullptr`, do **not** use `NULL`.
* `auto` should not be used, except for
  * range based for loops (only when the iterated target is verbose)
  * variable type is obvious, such as constructing smart pointers via `std::make_shared<T>`
  * TMP where this is necessary, e.g., `decltype(auto)`
* Perform explicit captures for lambda expressions.
* Pass by `const` reference if the parameter is not intended to be modified.
* Pass by non-`const` reference and a `out_` prefix for partially modified parameters.
* Pass by non-`const` pointer and a `out_` prefix completely modified parameters.
* Strongly-typed enum should always be used, and with a `E` prefix, e.g., `enum class EUnit`.
* Use of anonymous namespaces is encouraged for implementation specific helpers.
* Use `final` when the target is designed **not** to be inherited.
* Always use a pair of braces for statements (`if`, `for`, `while`, etc.) that contains only a single line.
* Do not put `using` declarations in global scope.
* Pointers and references:
  * Declare like this `ICommand* command`
  * **Not** like this `ICommand *command`
* Define functions/methods as `inline`, not when declaring them.
* Do **not** to use `new` and `delete` directly.

## Primitive Type Aliasing

Photon uses aliased types most of the time for cross platform compatibilities and ease of tuning. They are declared in [`Engine/Source/Common/primitive_type.h`](https://github.com/TzuChieh/Photon-v2/blob/master/Engine/Source/Common/primitive_type.h).

* Use `real` for reals, and a `_r` suffix for real literals.
* Use `integer` for integers.
* If you need specific precision and Photon has it, use it; otherwise use standard types.
