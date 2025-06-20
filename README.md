# Programming Project Tracker Specification

[![CI Validation](https://github.com/otg996/programming-project-tracker-spec/actions/workflows/validation.yml/badge.svg)](https://github.com/otg996/programming-project-tracker-spec/actions/workflows/validation.yml)

This repository contains the official specification, reference test suite, and documentation for the Programming Project Tracker. It serves as the single source of truth for all client implementations.

## Project Philosophy

The core goal of this project is to create a fast, reliable, and consistent tool for discovering and reporting on software development projects across a filesystem. Our guiding principles are detailed in [PHILOSOPHY.md](PHILOSOPHY.md).

## Structure of this Repository

* **/SPECIFICATION.md**: The formal, versioned specification that all clients must adhere to.
* **/reference-test-suite/**: The canonical test suite used to verify client conformance.
* **/docs/**: Source files for the GitHub Pages documentation website.

## How to Use

This repository is intended to be included as a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in client implementation repositories to provide access to the reference test suite.

The live, human-readable version of the specification is available at: **[otg996.github.io/programming-project-tracker-spec/](https://otg996.github.io/programming-project-tracker-spec/)**

PDFs are provided with every [release](https://github.com/otg996/programming-project-tracker/releases/latest)

## Contributing

We welcome contributions! Please read our [CONTRIBUTING.md](CONTRIBUTING.md) to learn about our development process, coding standards, and how to submit a pull request.

## License

The documentation and specification for the Programming Project Tracker are licensed under the [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
