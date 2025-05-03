
--- Repository Documentation ---

Okay, here is a guide explaining how to use the `vibe-tools repo` command for codebase analysis and documentation specifically within the `cursor-be-nimble` project, based on the provided repository context.

## Using `vibe-tools repo` for `cursor-be-nimble` Analysis

The `vibe-tools repo` command allows you to ask questions about the `cursor-be-nimble` codebase and receive context-aware answers using AI (specifically Google Gemini by default). This is useful for understanding code structure, explaining specific functionalities, debugging, planning changes, or generating documentation snippets.

**1. Basic Usage (Local Repository):**

To ask questions about the local `cursor-be-nimble` repository you are currently working in, navigate to the project's root directory in your terminal and run:

```bash
vibe-tools repo "<your question>"
```

Replace `<your question>` with your specific query about the codebase.

*   **Example:** To understand the authentication flow within the `cursor-be-nimble` project:
    ```bash
    vibe-tools repo "Explain the authentication flow in cursor-be-nimble"
    ```

**2. Analyzing Specific Subdirectories:**

If you want to focus the analysis on a particular part of the `cursor-be-nimble` project, use the `--subdir` option.

*   **Example:** To analyze the structure of the services directory:
    ```bash
    vibe-tools repo "Explain the code structure" --subdir=src/services
    ```

*   **Example:** To understand the purpose of the configuration files:
    ```bash
    vibe-tools repo "What are the different configuration files used for?" --subdir=src/config
    ```

**3. Analyzing the Remote Repository (Without Cloning):**

You can analyze the `cursor-be-nimble` repository directly from GitHub without needing a local copy. Use the `--from-github` option.

*   **Example:** Analyze the main branch of the remote repository:
    ```bash
    vibe-tools repo "Explain the project's dependency injection setup" --from-github=BuoySecureLabs/cursor-be-nimble
    ```

*   **Example:** Analyze a specific branch (e.g., `develop`):
    ```bash
    vibe-tools repo "What changes were made to the error handling in the develop branch?" --from-github=BuoySecureLabs/cursor-be-nimble@develop
    ```

**4. Customizing AI Provider and Model:**

While the default is Gemini, you can specify other providers or models.

*   **Example:** Using OpenAI's o3-mini model:
    ```bash
    vibe-tools repo "Summarize the purpose of the adapters layer" --provider=openai --model=o3-mini
    ```

*   **Example:** Using OpenRouter (assuming it's configured):
    ```bash
    vibe-tools repo "How is logging implemented?" --provider=openrouter --model=some-model-via-openrouter
    ```

**5. Controlling Output:**

*   **Max Tokens:** Limit the length of the response.
    ```bash
    vibe-tools repo "Provide a brief overview of the testing strategy" --max-tokens=500
    ```
*   **Save to File:** Save the analysis output to a file.
    ```bash
    vibe-tools repo "Generate documentation for the Claude adapter" --save-to=docs/claude-adapter-analysis.md
    ```

**6. Use Cases for `cursor-be-nimble`:**

*   **Understanding Architecture:** "Explain the dependency injection flow." (`--subdir=src/config`)
*   **Code Explanation:** "Explain the `ClaudeAdapter` class." (`--subdir=src/adapters/ai`)
*   **Debugging:** "Where might a `PMNotFoundError` be thrown?" (`--subdir=src/errors`)
*   **Planning Changes:** "What files would I need to modify to add a new AI service adapter?"
*   **Documentation:** "Generate a summary of the interfaces defined in `src/interfaces/ai`."
*   **Reviewing Code:** "Review the `retry.ts` utility for potential issues." (`--subdir=src/utils`)

**Important Considerations:**

*   **Context Limit:** The `repo` command has a context limit (around 2 million tokens). For very large repositories, consider using `--subdir` or configuring a `.repomixignore` file to exclude irrelevant files/directories.
*   **API Keys:** Ensure your AI provider API keys (e.g., `GEMINI_API_KEY`, `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`) are configured in your environment, typically in `~/.vibe-tools/.env`.
*   **Debugging:** Use the `--debug` flag if you encounter issues to get detailed logs.

By leveraging `vibe-tools repo`, you can significantly speed up your understanding and interaction with the `cursor-be-nimble` codebase. Remember to phrase your questions clearly and provide context for the best results.

--- End of Documentation ---
