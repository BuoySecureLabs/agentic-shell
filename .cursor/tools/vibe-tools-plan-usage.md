
--- Repository Documentation ---

Okay, here is a guide explaining how to use the `vibe-tools plan` command for creating implementation plans within the `cursor-be-nimble` project.

## `vibe-tools plan` Command Guide for `cursor-be-nimble`

### 1. Repository Purpose and "What is it" Summary

*   **Repository**: `cursor-be-nimble`
*   **Purpose**: `cursor-be-nimble` is an enhanced task and work breakdown management system designed for software development workflows, integrating with tools like JIRA and leveraging AI for task analysis and generation.
*   **`vibe-tools plan` Command**: This command, part of the external `vibe-tools` suite, utilizes AI to generate detailed, context-aware implementation plans for development tasks within the `cursor-be-nimble` repository (or any local repository). It analyzes the codebase to identify relevant files and then constructs a step-by-step plan based on the user's request.

### 2. Quick Start: How to Use `vibe-tools plan`

**Installation (if `vibe-tools` is not already installed):**

```bash
npm install -g vibe-tools
# Ensure your AI provider API keys are configured (e.g., in ~/.vibe-tools/.env)
```

**Basic Usage:**

Navigate to the root of your local `cursor-be-nimble` repository and run the command with a query describing the task you want to plan.

```bash
# Example: Plan how to add a new CLI command
vibe-tools plan "Add a new CLI command to list all available AI services"
```

The command will output a structured implementation plan to your console.

### 3. Detailed Usage

The `vibe-tools plan` command takes a single primary argument: the query describing the implementation task.

```bash
vibe-tools plan "<your detailed query about the task>" [options]
```

*   **`<your detailed query>`**: A natural language description of the feature, bug fix, or refactoring task you need a plan for. Be specific for better results.

**How it Works:**

The `plan` command uses a two-stage AI process:

1.  **File Identification**: It first analyzes your query and the `cursor-be-nimble` codebase to identify the files most relevant to the task. (Defaults to using Gemini).
2.  **Plan Generation**: It then takes the content of these relevant files and your original query to generate a detailed, step-by-step implementation plan. (Defaults to using OpenAI's o3-mini model).

**Examples within `cursor-be-nimble`:**

*   **Adding a new adapter:**
    ```bash
    vibe-tools plan "Implement a new PM adapter for Asana, including interface definition, adapter class, error handling, and DI container registration"
    ```
*   **Modifying an existing service:**
    ```bash
    vibe-tools plan "Refactor the ClaudeAdapter to support streaming responses, updating the interface and implementation"
    ```
*   **Implementing a feature based on a story:**
    ```bash
    vibe-tools plan "Implement user story TASK-123: Add a --verbose flag to the 'list-issues' CLI command to show full issue details"
    ```

### 4. Configuration Options

The `plan` command supports specific options to control its behavior, along with general `vibe-tools` options:

**Plan-Specific Options:**

*   `--fileProvider=<provider>`: Specifies the AI provider for the file identification stage.
    *   Options: `gemini` (default), `openai`, `anthropic`, `perplexity`, `modelbox`, `openrouter`.
*   `--thinkingProvider=<provider>`: Specifies the AI provider for the plan generation stage.
    *   Options: `openai` (default), `gemini`, `anthropic`, `perplexity`, `modelbox`, `openrouter`.
*   `--fileModel=<model_name>`: Specifies the exact model to use for file identification (overrides provider default).
*   `--thinkingModel=<model_name>`: Specifies the exact model to use for plan generation (overrides provider default).

**General `vibe-tools` Options:**

*   `--save-to=<file_path>`: Saves the generated plan to the specified file *in addition* to displaying it in the console. Useful for integrating plans into project documentation (e.g., `.cursor/scratchpad/plan-feature-x.md`).
    ```bash
    vibe-tools plan "Add health check endpoint to the server" --save-to=docs/plans/health-check-plan.md
    ```
*   `--max-tokens=<number>`: Limits the maximum number of tokens in the generated plan.
*   `--debug`: Enables detailed logging for troubleshooting the `vibe-tools` command itself.
*   `--provider=<provider>` / `--model=<model>`: If *only* these general provider/model flags are used *without* the specific `fileProvider`/`thinkingProvider` flags, they might influence the default models used, but it's recommended to use the specific flags for clarity.

### 5. Dependencies and Requirements

*   **`vibe-tools` CLI**: Must be installed globally or accessible in the environment's PATH.
*   **API Keys**: Requires API keys for the AI providers being used (e.g., `GEMINI_API_KEY`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`). These should be configured in the environment or, more commonly, in the `~/.vibe-tools/.env` file.
*   **Local Repository**: The command operates on the current local Git repository. Ensure you are in the `cursor-be-nimble` project root.
*   **Repomix Configuration**: File inclusion/exclusion for analysis can be customized via a `repomix.config.json` file in the project root (optional).

### 6. Advanced Usage Examples

*   **Using different providers for planning:**
    ```bash
    # Use Anthropic for file identification and OpenAI for planning
    vibe-tools plan "Refactor error handling in PM adapters" --fileProvider=anthropic --thinkingProvider=openai
    ```
*   **Specifying models:**
    ```bash
    # Use specific models for planning
    vibe-tools plan "Update JIRA adapter to handle custom fields" --fileModel=gemini-1.5-flash --thinkingModel=claude-3.7-sonnet
    ```
*   **Generating a plan for review:**
    ```bash
    # Save the plan to a specific directory for review
    vibe-tools plan "Add unit tests for the ConsoleAdapter" --save-to=.cursor/scratchpad/console-adapter-test-plan.md
    ```
*   **Planning complex refactoring:**
    ```bash
    vibe-tools plan "Analyze and plan the refactoring of the configuration system to support dynamic loading based on NODE_ENV"
    ```

By leveraging `vibe-tools plan`, developers working on `cursor-be-nimble` can quickly generate structured implementation outlines, ensuring consistency and helping to break down complex tasks into manageable steps based on the existing codebase structure.

--- End of Documentation ---
