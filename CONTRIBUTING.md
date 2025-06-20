# Contributing to the Programming Project Tracker Specification

Thank you for your interest in contributing! We appreciate your help. This project has a unique structure, so please read these guidelines carefully to ensure a smooth process.

A change to the specification often requires a corresponding change in the [reference library](https://github.com/otg996/libptrack-go) and its test suite. This guide will walk you through that multi-repository workflow.

## Development Environment Setup

This repository contains the specification document and the `reference-test-suite` used for conformance. Its development tooling relies on Node.js.

### Prerequisites

1. **Node.js** (LTS version)
2. **pnpm** (our preferred package manager)

### Installation

1. **Fork** this `programming-project-tracker-spec` repository.
2. **Clone** your fork locally: `git clone <your-fork-url>`
3. Navigate into the project directory: `cd programming-project-tracker-spec`
4. **Install dependencies and Git hooks:**

    ```bash
    pnpm install
    ```

    This command installs all developer tools and sets up the local Git hooks for this repository.

## The Multi-Repository Workflow

Most changes to the spec fall into one of two categories. Follow the workflow that applies to your change.

---

### Workflow A: Documentation-Only Changes

If your change only affects documentation (e.g., fixing typos in `README.md`, clarifying wording in `SPECIFICATION.md` without changing the rules), the process is simple:

1. Create a branch in this repository.
2. Make your changes.
3. Commit your work using `pnpm commit`.
4. Open a Pull Request.

---

### Workflow B: Changes Affecting Rules or Behavior (Most Common)

If you are changing a rule, adding a detection method, or modifying the data model, you **must** also update the reference implementation to match.

#### Step 1: Set Up the Full Project Structure

You will need local clones of all three core repositories.

1. Clone your fork of this `spec` repository.
2. Clone your fork of the [reference library (`libptrack-go`)](https://github.com/otg996/libptrack-go).
3. Clone your fork of the [reference client (`ptrack-cli`)](https://github.com/otg996/ptrack-cli).

These should be in separate directories, for example:

```console
/projects/
├── programming-project-tracker-spec/
├── libptrack-go/
└── ptrack-cli/
```

#### Step 2: Make Your Changes Across Repositories

1. **In `programming-project-tracker-spec`:**
    * Create a new branch (e.g., `feat/add-rust-detector`).
    * Update `SPECIFICATION.md` with the new rule.
    * Update the `reference-test-suite/` to include new test cases for this rule.
    * Update `expected_output.json` to reflect the correct output for the new test cases.

2. **In `libptrack-go`:**
    * Create a corresponding branch (you can use the same name).
    * Modify the Go code (`scanner.go`) to implement the new behavior defined in the spec.
    * Run the Go tests (`go test -v ./...`) and ensure they pass. The tests should be written to validate against a copy of the `reference-test-suite`.

3. **(If Applicable) In `ptrack-cli`:**
    * If your changes affect how the client works, create a branch and make the necessary updates here as well.

#### Step 3: Open Linked Pull Requests

You will need to open a pull request for each repository you changed.

1. **Commit and Push** your changes on their respective branches in each repository.
2. **Open a Pull Request** for your branch in the `spec` repository.
3. **Open a Pull Request** for your branch in the `libptrack-go` repository.
4. **In the description of each PR, link to the other PR(s).** For example, in the `spec` PR, write: "This change is implemented in `libptrack-go#<PR_NUMBER>`."

This linking is crucial. We will only merge the changes once all related pull requests are approved and their CI checks have passed.

---

Thank you for following this process. It helps us ensure that the specification and its reference implementation are always in sync.
