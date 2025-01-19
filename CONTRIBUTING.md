# Contributing to Vauban

First off, thanks for taking the time to contribute to this project 🥳

## How Can I Contribute?

### Reporting Bugs

1. **Ensure the bug was not already reported** by searching on GitHub under [Issues](https://github.com/gregoire-badiche/vauban/issues).

2. If you're unable to find an open issue addressing the problem, [open a new one](https://github.com/gregoire-badiche/vauban/issues/new).

### Suggesting Enhancements

1. Create a feature request issue detailing what you'd like to see implemented.

### Code Contribution

1. Fork the repo on GitHub.
2. Clone the forked repository.
3. Create a new feature branch based on `main`.
4. Make your changes.
5. Ensure the code adheres to the existing style.
6. Submit a pull request against the `main` branch of the upstream repository.

## Coding Conventions

### Syntax

We primarily use C++ for this project.

Follow modern C++ best practices.

Docstrings code comments for exposed functions are appreciated.

Please respect the file tree, all informations about where to place each file can be found in each `README.md`.

### Directory tree

```text
.
├── docs            # Hardware and software docs
│   ├── schematics
│   └── specs
├── include         # Project specific headers
│   └── *           # Folder for each project header
├── lib             # Global / external libraries
│   └── *           # Folder for each library
└── src             # Source code with no headers
    ├── *           # Project specific libraries
    └── vauban.cpp  # Entry point
```

## Commit Messages

Write clear and meaningful Git commit messages (they can be funny, but make it clear too).
I just need to know what you did.

## Pull Requests

Ensure that your PRs are small, focused, and you clearly explain the changes made in the description.

## License

By contributing to this project, you agree that your contributions will be licensed under the same terms used in the project.

## Questions?

Feel free to contact the project maintainers if you have any questions or concerns.
