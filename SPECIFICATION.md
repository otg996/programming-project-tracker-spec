# Programming Project Tracker Specification v0.0.1

**Version:** 0.0.1
**Status:** Stable-Not Production Ready

## Overview

This document describes the v0.0.1 specification for the Programming Project Tracker scanner. The primary goal of this version is to identify all Git repositories within a given directory structure.

This specification is programming language-agnostic. Any implementation in any language that adheres to the behavior described below is considered conformant.

## Core Concepts

* **Root Scan Directory:** The top-level directory path provided as input to the scanner.
* **Project:** For v0.0.1, a **Project** is defined as any directory that contains a direct sub-directory named `.git`.

## Scanner Behavior

An implementation of the scanner MUST adhere to the following rules:

1. **Input:** The scanner must accept a single, valid file system path to a directory (the "Root Scan Directory").
2. **Traversal:** The scanner must recursively traverse the entire directory tree starting from the "Root Scan Directory".
3. **Detection Logic:** For each directory it visits, the scanner must check for the existence of a direct sub-directory named exactly `.git`.
    * If a `.git` directory is found, the scanner MUST identify the parent directory (the one containing `.git`) as a **Project**.
    * The path to this Project directory MUST be added to the result set.
4. **Traversal Scope:** The discovery of a Project **does not** stop the traversal. The scanner MUST continue to scan sub-directories within a found Project. This means nested Git repositories (e.g., submodules) will be identified as separate Projects.
    * A .git directory MUST not be traversed into, as doing this results in wasted processor cycles.

\newpage

## Data Model

The output of a successful scan MUST be a list of strings. Each string in the list is the absolute path to a found Project directory.

### Example Output (JSON representation)

If projects are found at `/home/user/dev/project-a` and `/home/user/dev/project-b`, the output would be:

```json
[
  "/home/user/dev/project-a",
  "/home/user/dev/project-b"
]
```

## Conformance and Testing Methodology

Conformance to this specification is verified by a standard test suite, not by reviewing implementation details. Any client implementation (GUI, TUI, etc.) must prove its conformance.

The testing methodology consists of two parts, which will be provided alongside this specification:

1. **A `reference-test-suite/` directory:** A folder containing a pre-defined structure of directories, files, and mock `.git` repositories that cover the requirements of this spec (e.g., a project in the root, a nested project, a directory with no project).

2. **A canonical `expected_output.json` file:** A JSON file containing the exact list of project paths that a conformant scanner MUST produce when run on the `reference-test-suite/` directory.

### Conformance Requirement

**An implementation is considered v0.0.1 conformant if, when run against the `reference-test-suite/` directory, it produces an output that is logically equivalent to the `expected_output.json` file.**

> **Note on Equivalence:** Since file system traversal order can differ between implementations, the list of paths in the actual and expected outputs should be **sorted alphabetically** before comparison to ensure a stable test result.

## Reference Implementation

A Go-based CLI and library serves as the reference implementation for v0.0.1. The tests for this implementation are used to generate the canonical `expected_output.json` for the test suite, guaranteeing that the specification is grounded in a working example.
