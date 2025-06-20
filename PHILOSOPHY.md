# Project Philosophy

This document outlines the core principles that guide the development and architecture of the Programming Project Tracker. Understanding these principles is key to contributing effectively.

## Specification-First Design

The entire project is built around a formal, versioned specification. The behavior of the scanner is defined in a document, not just in code.

* **Why?** This ensures all client implementations, regardless of programming language, behave identically. It decouples the core logic from the user-facing presentation, allowing them to evolve independently.

## Conformance Through Testing, Not Implementation

A client is considered "conformant" if it passes the `reference-test-suite`, not because it uses our reference library.

* **Why?** This gives client developers the freedom to write native, idiomatic code in their language of choice without being forced to use CGo or FFI wrappers. The reference test suite, not a specific library, is the ultimate source of truth.

## Simplicity and Focus

The project tracker does one thing: it finds projects and reports their basic SCM status. It is not an IDE, a build tool, or a project manager.

* **Why?** By maintaining a narrow focus, we can ensure the tool is fast, reliable, and easy to maintain. We avoid feature creep by adhering to this principle.

## Excellent Developer Experience

We believe that a project that is easy to contribute to is a project that thrives. We invest in tooling and automation to make the development process smooth and error-free.

* **Why?** Automated checks (linting, testing, commit messages) in our CI pipeline and local `lefthook` setup catch errors early, enforce consistency, and allow maintainers to focus on the quality of the contribution itself, not on stylistic nitpicks.
