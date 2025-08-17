## Project Overview

This project, `verilog-ext`, is an Emacs Lisp package that provides a comprehensive suite of extensions for `verilog-mode` and `verilog-ts-mode`, enhancing the Emacs environment for Verilog and SystemVerilog development.

The package is highly modular, allowing users to selectively enable features. Key functionalities include:
-   **Advanced Syntax Highlighting:** Improves upon the default highlighting.
-   **Code Navigation:** Provides `xref` backend for finding definitions and references.
-   **Auto-completion:** Offers a `capf` backend for context-aware completion, including dot and scope completion.
-   **Code Beautification:** Tools to indent and align modules, instances, parameters, and ports.
-   **Linting:** Integrates with various Verilog linters via `flycheck`.
-   **Hierarchy Extraction:** Can extract and display module hierarchies.
-   **Templates:** A collection of `yasnippet` and `hydra`-based templates for common Verilog constructs.
-   **Project Management:** A system to define project-specific file lists, include paths, and compilation commands.

The core logic is written in Emacs Lisp. For performance and accuracy, especially in hierarchy and tag-related tasks, the package can leverage `tree-sitter` through `verilog-ts-mode`.

## Building and Running

As an Emacs package, there isn't a traditional "build" process. It is meant to be installed via Emacs package managers like MELPA or `straight.el`.

### Testing

The project uses the Emacs Lisp Regression Testing (ERT) framework for tests. The tests are managed through a `Makefile`.

-   **Prerequisites:** The `test-hdl` git submodule must be initialized before running tests:
    ```shell
    git submodule update --init
    ```

-   **Run all tests:**
    ```shell
    make
    ```

-   **Run a specific subset of tests** (e.g., `navigation`):
    ```shell
    make TESTS=navigation
    ```

-   **Regenerate all reference files** for tests:
    ```shell
    make gen
    ```

-   **Regenerate specific reference files:**
    ```shell
    make gen TESTS=navigation
    ```

## Development Conventions

-   **File Structure:** The project is organized by feature. Each major feature (e.g., `beautify`, `xref`, `capf`) resides in its own `verilog-ext-*.el` file. The main `verilog-ext.el` file is responsible for loading the enabled features and setting up the minor mode.
-   **Coding Style:** The code follows standard Emacs Lisp conventions.
    -   Functions and variables are prefixed with `verilog-ext-`.
    -   User-configurable variables are defined using `defcustom` and grouped under the `verilog-ext` group.
    -   The code is well-documented with comments and docstrings.
-   **Testing:**
    -   Tests are written using `ert-deftest`.
    -   Test files are located in `test/src/` and are named `verilog-ext-test-*.el`.
    -   Many tests work by processing a file from `test/files/` and comparing the result against a golden reference file in `test/ref/`. The `make gen` command is used to update these reference files.
-   **Modularity:** Features are designed to be optional. The `verilog-ext-feature-list` variable controls which modules are loaded. The `verilog-ext-when-feature` macro is used to conditionally execute code based on the user's configuration.
