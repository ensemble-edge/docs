# Ensemble Documentation

The official documentation for Ensemble Edge, built with [Mintlify](https://mintlify.com).

## About

Comprehensive documentation covering:
- **Edgit**: Git-native component management and versioning
- **Conductor**: Agent orchestration and workflow automation (coming soon)
- **Shared Concepts**: Cross-product patterns and best practices
- **API Reference**: REST, GraphQL, and webhook APIs
- **AI Tools**: Integration guides for Cursor, Claude Code, and Windsurf

## Local Development

### Prerequisites
- Node.js 18 or higher
- npm or yarn

### Setup

1. Install dependencies:
```bash
pnpm install
```

2. Install Mintlify CLI globally (if not already installed):
```bash
npm i -g mintlify
```

3. Start the development server:
```bash
pnpm run dev
# or
mintlify dev
```

4. Open [http://localhost:3000](http://localhost:3000) in your browser

### Configuration

The documentation is configured in [mint.json](mint.json), which defines:
- Site metadata (name, colors, logo)
- Navigation structure
- Tabs and page organization
- Footer and social links

## Deployment

This documentation is automatically deployed to production when changes are pushed to the main branch.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on contributing to the documentation.

## License

MIT

## Trademark

Ensemble® is a registered trademark of Higinio O. Maycotte.
