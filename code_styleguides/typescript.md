# TypeScript Code Style Guide

This document outlines the TypeScript coding conventions for this project.

## Formatting
- Indentation: Use 2 spaces.
- Line length: Max 100 characters.
- Semicolons: Always use semicolons.

## Naming Conventions
- Variables, functions, methods: `camelCase`
- Classes, interfaces, types: `PascalCase`
- Constants: `SCREAMING_SNAKE_CASE`

## Type Safety
- Use strict type checking (`tsconfig.json: strict: true`).
- Explicitly define types for function parameters and return values.
- Avoid `any` whenever possible.

## Best Practices
- Favor interfaces for object shapes and classes for instances.
- Organize imports alphabetically.
- Use `const` and `let`.
