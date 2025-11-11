# Go Code Style Guide

This document outlines the Go coding conventions for this project.

## Formatting
- Use `gofmt` to format all code.
- Line length: No strict limit, focus on readability.

## Naming Conventions
- Packages: `lowercase` (short, single word)
- Variables, functions, methods: `camelCase` (for unexported), `PascalCase` (for exported)
- Constants: `PascalCase` or `camelCase` depending on export status.

## Best Practices
- Error handling: Always check errors and handle them gracefully.
- Concurrency: Use goroutines and channels for concurrent operations.
- Comments: Document exported types, variables, constants, functions, and methods.
