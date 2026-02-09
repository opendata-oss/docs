# Contribute to the documentation

Thank you for your interest in improving the OpenData docs! This guide covers documentation contributions. For code contributions, see the [source repo's contributing guide](https://github.com/opendata-oss/opendata/blob/main/CONTRIBUTING.md).

## How to contribute

### Option 1: Edit directly on GitHub

1. Navigate to the page you want to edit
2. Click the pencil icon to edit the file
3. Make your changes and submit a pull request

### Option 2: Local development

1. Fork and clone this repository
2. Install the Mintlify CLI: `npm i -g mint`
3. Create a branch for your changes
4. Run `mint dev` and preview at `http://localhost:3000`
5. Commit your changes and submit a pull request

## Writing guidelines

- **Use active voice**: "Run the command" not "The command should be run"
- **Address the reader directly**: Use "you" instead of "the user"
- **Keep sentences concise**: One idea per sentence
- **Lead with the goal**: Start instructions with what you want to accomplish
- **Use consistent terminology**: See `AGENTS.md` for preferred terms
- **Include examples**: Use Rust code examples with realistic values

## Adding new pages

When you add a new `.mdx` file, you must also add it to the `navigation` section of `docs.json` or it won't appear in the sidebar.

## Need help?

- Join the [Discord](https://discord.gg/CsAQJ2AJGU)
- Open an issue on the [source repo](https://github.com/opendata-oss/opendata/issues)
