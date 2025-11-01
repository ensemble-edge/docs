# CLAUDE.md

This file provides guidance to Claude Code and other AI assistants when working with the Ensemble documentation repository.

## Repository Purpose

This repository contains the Mintlify documentation site for all Ensemble products (Edgit, Conductor, and shared resources). It serves as the central documentation hub at docs.ensemble.ai.

## Documentation Structure

```
docs/
├── index.mdx                  # Main landing page
├── getting-started/          # Quick start guides
│   ├── edgit.mdx
│   └── conductor.mdx
├── edgit/                    # Edgit documentation
│   ├── overview.mdx
│   ├── installation.mdx
│   └── api-reference/
├── conductor/                # Conductor documentation
│   ├── overview.mdx
│   └── architecture.mdx
├── shared/                   # Shared concepts
└── docs.json                 # Mintlify configuration
```

## Git Commit Standards

### Commit Message Format
All commits must follow Conventional Commits format WITHOUT any AI attribution:

- **NEVER** append "code written by claude" or similar attribution to commit messages
- **NEVER** add signatures, author notes, or "written by" suffixes
- Use clean, professional commit messages focusing only on the changes

### Correct Format:
```
<type>(<scope>): <subject>

[optional body]
```

### Examples:
✅ CORRECT:
- `docs: update edgit installation guide`
- `fix: correct broken links in conductor overview`
- `feat: add new workflow examples section`

❌ INCORRECT:
- `docs: update guide - code written by claude`
- `fix: broken link (written by Claude)`
- Any commit with AI attribution or signatures

### Commit Types:
- `docs:` - Documentation content changes (most common)
- `fix:` - Fix typos, broken links, errors
- `feat:` - Add new documentation sections
- `style:` - Formatting changes

## Mintlify Documentation

This site uses Mintlify for documentation. Key concepts:

### MDX Format
- Use `.mdx` extension (Markdown + JSX)
- Supports Mintlify components: `<Card>`, `<Accordion>`, `<Steps>`, etc.
- See [Mintlify components](https://mintlify.com/docs/components)

### Navigation
Edit `docs.json` to update site navigation structure.

### Local Development
```bash
npm install
npm run dev  # Starts Mintlify dev server
```

## Documentation Standards

See [.planning/standards/docs-authoring-standards.md](../.planning/standards/docs-authoring-standards.md) in the main ensemble repo for detailed documentation standards.

Key points:
- Clear, concise language
- Code examples that work
- Proper heading hierarchy
- Cross-reference related docs

## Resources

- [Documentation Contributing Guide](CONTRIBUTING.md)
- [Mintlify Documentation](https://mintlify.com/docs)
- [Documentation Site](https://docs.ensemble.ai)
