# Contributing to Ensemble Edge

Thank you for your interest in contributing to Ensemble Edge! This monorepo contains multiple projects including **edgit** (Git tag-based component versioning), **conductor** (edge orchestration runtime), and **docs**.

## Table of Contents

- [Quick Start](#quick-start)
- [Development Setup](#development-setup)
- [Code Standards](#code-standards)
- [Commit Convention](#commit-convention)
- [Pull Request Process](#pull-request-process)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Getting Help](#getting-help)

## Quick Start

### For First-Time Contributors

1. **Fork the repository**
   ```bash
   # Click "Fork" on GitHub
   ```

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/ensemble.git
   cd ensemble
   ```

3. **Set up the project**
   ```bash
   # For edgit
   cd edgit
   pnpm install
   pnpm run build

   # For conductor
   cd ../conductor
   pnpm install
   pnpm run build
   ```

4. **Create a feature branch**
   ```bash
   edgit checkout -b feature/your-feature-name
   ```

5. **Make your changes**
   - Write code following our standards
   - Add tests (when available)
   - Update documentation

6. **Build and test**
   ```bash
   pnpm run build
   pnpm test
   ```

7. **Commit using conventional commits**
   ```bash
   edgit add .
   edgit commit -m "feat(edgit): add new tag validation"
   ```

8. **Push and create Pull Request**
   ```bash
   edgit push origin feature/your-feature-name
   # Go to GitHub and click "New Pull Request"
   ```

## Development Setup

### Prerequisites

- **Node.js** v18.0+ (v20+ recommended)
- **npm** v10.0+ or **pnpm** v9.7.0+
- **Git** v2.0+
- **TypeScript** knowledge for code contributions
- **Unix-like environment** (Linux, macOS, WSL)

### Project Structure

```
ensemble/
├── edgit/              # Git tag-based versioning CLI
│   ├── src/           # TypeScript source
│   ├── dist/          # Built JavaScript
│   ├── tests/         # Tests (TODO)
│   └── package.json
├── conductor/          # Edge orchestration runtime
│   ├── src/
│   └── package.json
├── docs/              # Mintlify documentation
├── examples/          # Usage examples
└── CONTRIBUTING.md    # This file
```

### Setting Up Each Package

#### Edgit
```bash
cd edgit
pnpm install
pnpm run build

# Link for local testing
pnpm link --global

# Test
edgit --version
```

#### Conductor
```bash
cd conductor
pnpm install
pnpm run build
pnpm test
```

#### Docs
```bash
cd docs
pnpm install
pnpm run dev  # Start local docs server
```

## Code Standards

### TypeScript Guidelines

**All new code must:**
- Use TypeScript strict mode (already configured)
- Have explicit type annotations for function parameters and returns
- Avoid `any` - use `unknown` with type guards instead
- Use interfaces for object shapes
- Follow ESM conventions (`.js` extensions in imports)

**Example:**
```typescript
// ✅ Good
export async function createTag(
  componentName: string,
  version: string
): Promise<string> {
  const tagName = `components/${componentName}/${version}`;
  return tagName;
}

// ❌ Bad
export async function createTag(componentName, version) {
  return 'components/' + componentName + '/' + version;
}
```

### Code Style

**Naming Conventions:**
- `camelCase` for variables and functions
- `PascalCase` for classes and interfaces
- `UPPER_SNAKE_CASE` for constants
- Descriptive names (no single letters except loop counters)

**Formatting** (until Prettier is configured):
- 2 spaces for indentation
- Single quotes for strings
- No semicolons (TypeScript convention)
- Trailing commas in multiline arrays/objects
- Max line length: 100 characters

**Imports:**
```typescript
// Group and order imports:
// 1. Node built-ins
import fs from 'fs/promises';
import path from 'path';

// 2. External dependencies
import dotenv from 'dotenv';

// 3. Local modules (with .js extension for ESM)
import { GitWrapper } from '../utils/git.js';
import { Component } from '../models/components.js';
```

### Documentation Standards

**JSDoc for all public functions:**
```typescript
/**
 * Creates an immutable version tag for a component.
 *
 * @param componentName - Name of the component to tag
 * @param version - Semantic version (e.g., "1.0.0")
 * @returns The full tag name created
 * @throws {Error} If component doesn't exist or tag already exists
 *
 * @example
 * ```typescript
 * const tag = await createVersionTag('my-prompt', '1.0.0');
 * console.log(tag); // "components/my-prompt/v1.0.0"
 * ```
 */
export async function createVersionTag(
  componentName: string,
  version: string
): Promise<string> {
  // Implementation
}
```

**Inline comments:**
- Explain *why*, not *what*
- Keep comments up-to-date
- Use `// TODO:` for future work
- Use `// FIXME:` for known issues
- Use `// NOTE:` for important clarifications

## Commit Convention

We use [Conventional Commits](https://www.conventionalcommits.org/) for clear, semantic commit history.

### Format

```
type(scope): subject

[optional body]

[optional footer]
```

### Types

- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation only changes
- `style:` - Formatting, missing semicolons (no code change)
- `refactor:` - Code change that neither fixes a bug nor adds a feature
- `perf:` - Performance improvements
- `test:` - Adding or updating tests
- `chore:` - Build process, dependencies, tooling
- `ci:` - CI/CD configuration changes

### Scopes

- `edgit` - Changes to edgit package
- `conductor` - Changes to conductor package
- `docs` - Documentation changes
- `deps` - Dependency updates
- `config` - Configuration changes

### Examples

```bash
# Feature
feat(edgit): add batch tag creation support

# Bug fix
fix(conductor): handle timeout errors gracefully

# Documentation
docs: update README with deployment examples

# Refactoring
refactor(edgit): extract tag manager from git wrapper

# Multiple components
feat(edgit,conductor): add shared configuration system

# Breaking change
feat(edgit)!: change tag namespace format

BREAKING CHANGE: Tag format changed from components-name-version to components/name/version
```

### Commit Message Guidelines

- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize first letter
- No period at the end
- Reference issues: `fixes #123` or `closes #456`
- Keep subject line under 72 characters
- Separate subject from body with blank line
- Wrap body at 72 characters

## Pull Request Process

### Before Submitting

**Checklist:**
- [ ] Code follows TypeScript and style guidelines
- [ ] All functions have JSDoc comments
- [ ] Tests added/updated (when test infrastructure exists)
- [ ] Documentation updated (README, CLAUDE.md, etc.)
- [ ] Build succeeds (`pnpm run build`)
- [ ] No TypeScript errors (`npx tsc --noEmit`)
- [ ] Commit messages follow conventional commits
- [ ] Branch is up-to-date with main

### PR Title Format

Use conventional commit format:
```
feat(edgit): add support for batch operations
```

### PR Description Template

```markdown
## Description
Brief description of what this PR does

## Type of Change
- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update

## Related Issues
Closes #123
Fixes #456

## How Has This Been Tested?
Describe the tests you ran

## Screenshots (if applicable)
Add screenshots for UI changes

## Checklist
- [ ] My code follows the style guidelines
- [ ] I have performed a self-review
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing tests pass locally
```

### Review Process

1. **Automated checks** run on all PRs
2. **At least one maintainer review** required
3. **Address feedback** by pushing new commits
4. **Squash and merge** once approved

### PR Guidelines

- **Keep PRs focused** - One feature/fix per PR
- **Small is better** - Easier to review and merge
- **Update docs** - Documentation is part of the feature
- **Link issues** - Reference related issues in description
- **Be responsive** - Reply to review comments promptly
- **Be patient** - Reviews take time, especially for large changes

## Testing Guidelines

### Current State
⚠️ **Test infrastructure is not yet implemented.** This is a high-priority task.

### Future Testing Requirements

Once test infrastructure is in place:

**Coverage Requirements:**
- Critical paths: **80%+** coverage
- Utilities: **70%+** coverage
- Overall: **60%+** coverage

**Test Types:**
- **Unit tests** - Pure functions, utilities
- **Integration tests** - Commands, workflows
- **E2E tests** - Full CLI scenarios

**Test Structure:**
```typescript
describe('Feature', () => {
  beforeEach(() => {
    // Setup
  });

  afterEach(() => {
    // Cleanup
  });

  it('should handle success case', () => {
    // Arrange
    const input = 'test';

    // Act
    const result = functionUnderTest(input);

    // Assert
    expect(result).toBe('expected');
  });

  it('should handle error case', () => {
    expect(() => functionUnderTest('')).toThrow();
  });
});
```

## Documentation

### What to Document

**Update documentation when:**
- Adding new commands
- Changing command behavior
- Adding new component types
- Changing configuration options
- Fixing bugs that affect behavior

### Documentation Locations

- **README.md** - User-facing documentation
- **CLAUDE.md** - AI assistant guidance, architecture
- **DEVELOPMENT.md** - Developer setup and workflow
- **CONTRIBUTING.md** - This file
- **JSDoc comments** - In-code documentation
- **docs/** - Full documentation site

### Writing Style

- **Be concise** - Short sentences, clear language
- **Use examples** - Show, don't just tell
- **Be accurate** - Test your examples
- **Stay current** - Update when code changes
- **Consider audience** - Different docs for users vs developers

## Getting Help

### Resources

- **Documentation**: Check CLAUDE.md and DEVELOPMENT.md
- **Existing issues**: Search before creating new ones
- **Discussions**: For questions and ideas
- **Code review**: Learn from PR feedback

### Communication Channels

- **Bug reports**: [Open an issue](https://github.com/ensemble-edge/ensemble/issues/new)
- **Feature requests**: [Start a discussion](https://github.com/ensemble-edge/ensemble/discussions)
- **Questions**: Check existing issues or start a discussion
- **Security issues**: See [SECURITY.md](./SECURITY.md)

### For Maintainers

If you're a maintainer:
- Review PRs promptly
- Provide constructive feedback
- Help new contributors
- Keep documentation updated
- Enforce code standards consistently

## Code of Conduct

See [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

We expect all contributors to:
- Be respectful and inclusive
- Provide constructive feedback
- Accept constructive criticism gracefully
- Focus on what's best for the community

## License

By contributing to Ensemble Edge, you agree that your contributions will be licensed under the same license as the project (MIT for edgit, Apache 2.0 for conductor).

---

**Thank you for contributing!** Your efforts help make Ensemble Edge better for everyone. 🚀
