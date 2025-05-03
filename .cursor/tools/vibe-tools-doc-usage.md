--- Repository Documentation ---

Okay, here is a brief overview explaining how to use `vibe-tools doc` to generate documentation for the `cursor-be-nimble` project, based on the provided context:

# AI Assistant Implementation Workflow

When implementing tasks that involve vibe-tools commands:

1. ALWAYS execute the command as written using run_terminal_cmd
2. NEVER replace command execution with manual content creation
3. After execution, review the generated content to verify quality
4. Only make minor adjustments to the generated content if necessary
5. ENSURE generated documentation passes ESLint Markdown linting before considering the task complete

INCORRECT: Creating markdown content manually when instructed to use vibe-tools
CORRECT: Executing the vibe-tools command via run_terminal_cmd

## Benefits of vibe-tools vs. Manual Creation

vibe-tools doc:
- Analyzes the entire codebase to ensure accuracy
- Generates properly formatted diagrams
- Provides rich explanations based on actual code structure
- Includes styling and helpful visual elements
- Ensures consistency across documentation

Manual documentation:
- May miss important relationships
- Diagrams might not reflect the actual code
- Prone to misinterpretation of code structure
- Inconsistent formatting and structure

## Using `vibe-tools doc` for `cursor-be-nimble` Documentation

The `vibe-tools doc` command is designed to generate comprehensive documentation for a repository. Here's how to use it for the `cursor-be-nimble` project:

**1. Basic Usage:**

To generate documentation for the local `cursor-be-nimble` repository you are currently in, run the following command in your terminal:

```bash
vibe-tools doc
```

By default, this will output the generated documentation to your console.

**2. Saving Documentation to a File:**

To save the generated documentation to a file (e.g., `cursor-be-nimble-docs.md`), use the `--output` (or `--save-to`) option:

```bash
vibe-tools doc --output cursor-be-nimble-docs.md
```

**3. Generating Documentation for a Remote Repository:**

If you want to generate documentation for the remote `cursor-be-nimble` repository hosted on GitHub without cloning it locally, use the `--from-github` option:

```bash
vibe-tools doc --from-github=BuoySecureLabs/cursor-be-nimble --output cursor-be-nimble-remote-docs.md
```

You can optionally specify a branch:

```bash
vibe-tools doc --from-github=BuoySecureLabs/cursor-be-nimble@develop --output cursor-be-nimble-develop-docs.md
```

**4. Specifying AI Provider and Model:**

You can control which AI provider and model are used for generation. The default provider is typically Gemini, but you can specify others:

```bash
# Example using OpenAI's o3-mini model
vibe-tools doc --provider=openai --model=o3-mini --output docs-o3-mini.md

# Example using Anthropic's Claude Sonnet 3.7
vibe-tools doc --provider=anthropic --model=claude-3.7-sonnet --output docs-claude.md
```

**5. Controlling Output Length:**

Use the `--max-tokens` option to limit the length of the generated documentation:

```bash
vibe-tools doc --max-tokens=4000 --output concise-docs.md
```

**6. Debugging:**

If you encounter issues, use the `--debug` flag for detailed logs:

```bash
vibe-tools doc --debug
```

## Ensuring Documentation Passes Linting Checks

All documentation generated using `vibe-tools doc` must pass ESLint Markdown linting before being considered complete. The project uses `@eslint/markdown` to enforce consistent Markdown styling and formatting.

**1. Validating Documentation Against Linting Rules:**

After generating documentation, always validate it against the project's Markdown linting rules:

```bash
npm run lint:md -- path/to/generated-doc.md
```

**2. Automatically Fixing Common Issues:**

Many linting issues can be automatically fixed:

```bash
npm run lint:md -- --fix path/to/generated-doc.md
```

**3. Common Linting Rules to Check:**

When reviewing generated documentation, pay special attention to these rules:

- Headers must increment by only one level (no jumping from H1 to H3)
- All fenced code blocks must specify a language
- No duplicate headers within the same document
- No empty links
- No invalid or missing label references

**4. Integration Into Documentation Workflow:**

Follow this workflow when generating documentation:

1. Generate initial documentation with `vibe-tools doc`
2. Run linting with auto-fix: `npm run lint:md -- --fix path/to/doc.md`
3. Manually address any remaining linting errors
4. Verify the document passes all checks: `npm run lint:md path/to/doc.md`
5. Only then consider the documentation task complete

This ensures all project documentation maintains consistent formatting and adheres to the project's [markdown style guide](../../docs/markdown-style-guide.md).

## Example Implementation in AI Workflows:

When you see instructions to use vibe-tools in an implementation plan, this is the CORRECT way to execute them:

```python
# CORRECT - Execute the command via run_terminal_cmd
run_terminal_cmd("vibe-tools doc \"Create architecture diagram\" --save-to=docs/architecture.md")

# Run linting with auto-fix on the generated documentation
run_terminal_cmd("npm run lint:md -- --fix docs/architecture.md")

# Validate the document passes all linting checks
run_terminal_cmd("npm run lint:md docs/architecture.md")

# INCORRECT - Do not create the content manually
edit_file("docs/architecture.md", "# Architecture Diagram\n\nThis is a manually created diagram...")
```

**Summary:**

The `vibe-tools doc` command provides a flexible way to automatically generate documentation for the `cursor-be-nimble` project, whether locally or from its GitHub repository, with options to customize the AI model and output. Remember to have your AI provider API keys configured in your environment (e.g., in `~/.vibe-tools/.env`), and always ensure generated documentation passes all Markdown linting checks before considering the task complete.

--- End of Documentation ---
