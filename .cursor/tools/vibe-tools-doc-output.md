
--- Repository Documentation ---

# **Cursor Be Nimble: Documentation**

## 1. Repository Purpose and "What is it" Summary

*   **Repository**: `cursor-be-nimble`
*   **Purpose**: An enhanced task and work breakdown management system designed for software development workflows. It integrates AI capabilities (Claude, Perplexity, Gemini), synchronizes with JIRA as the system of record for all Work Breakdown Structure (WBS) elements (PRD, Architecture, Epic, Feature, Story, Acceptance Criteria, Test Case, Task), and follows a Test-Driven Development (TDD) approach. The system aims to streamline the SDLC by bridging the gap between high-level requirements and granular development tasks.
*   **Interfaces**: It provides two main interfaces:
    *   A Command Line Interface (CLI) for direct user interaction and management of the WBS.
    *   A Model Context Protocol (MCP) server for integration with development tools like the Cursor IDE.

## 2. Quick Start

### Installation

1.  **Prerequisites**:
    *   Node.js (check `.nvmrc` or `package.json` engines for version)
    *   npm or yarn
    *   Git
    *   Access to a JIRA instance (sandbox/dev recommended for initial setup)
    *   API Keys/Tokens for:
        *   JIRA
        *   Anthropic (Claude)
        *   Google AI (Gemini)
        *   Perplexity AI
        *   (Optional) GitHub

2.  **Clone the Repository**:
    ```bash
    git clone https://github.com/BuoySecureLabs/cursor-be-nimble.git
    cd cursor-be-nimble
    ```

3.  **Install Dependencies**:
    ```bash
    npm install
    # or
    yarn install
    ```

4.  **Configure Environment**:
    *   Copy the example environment file:
        ```bash
        cp .env.example .env
        ```
    *   Edit the `.env` file and provide the necessary credentials and configuration values (JIRA host, API keys, project keys, etc.). See Section 3 for details. Ensure `NODE_ENV` is set to `development`.

5.  **Build the Project**:
    ```bash
    npm run build
    ```

### Basic Usage (CLI)

After installation and configuration, you can use the CLI (often aliased as `nimble` or run via `node dist/cli.js`).

*   **Get Help**:
    ```bash
    nimble --help
    nimble create-story --help
    ```
*   **Create a WBS Item (Example: Story)**:
    ```bash
    nimble create-story --feature-id FEAT-1 --title "Implement User Login" --description "As a user..."
    ```
*   **Get Item Details**:
    ```bash
    nimble get-task --id TASK-101
    ```
*   **List Items**:
    ```bash
    nimble list-features --epic-id EPIC-1
    ```

See the **CLI Interface** section below for a detailed command reference.

## 3. Configuration Options

Configuration is managed primarily through environment variables, loaded via `.env` files (for local development) or system environment variables (for staging/production). A central `ConfigService` validates and provides typed access to these settings.

**`.env` File Structure (based on `.env.example`)**

```dotenv
# Application Environment
NODE_ENV=development # Options: development, staging, production
LOG_LEVEL=info       # Options: error, warn, info, debug, trace

# --- JIRA Integration ---
JIRA_HOST=your-instance.atlassian.net
JIRA_USERNAME=your-jira-email@example.com
JIRA_API_TOKEN=your_jira_api_token
JIRA_PROJECT_KEY=YOUR_PROJ_KEY
# JIRA_CUSTOM_FIELD_EPIC_LINK=customfield_xxxxx # Optional

# --- AI Provider Settings ---
# Anthropic Claude
ANTHROPIC_API_KEY=your_anthropic_key
ANTHROPIC_MODEL=claude-3-5-sonnet-20240620 # Optional default

# Google Gemini
GOOGLE_API_KEY=your_google_key
GEMINI_MODEL=gemini-1.5-pro-latest # Optional default

# Perplexity AI
PERPLEXITY_API_KEY=your_perplexity_key
PERPLEXITY_MODEL=sonar-medium-online # Optional default

# --- GitHub Integration ---
GITHUB_TOKEN=your_github_pat # Optional

# --- MCP Server Configuration ---
MCP_SERVER_PORT=3001
MCP_SERVER_HOST=0.0.0.0
JIRA_WEBHOOK_SECRET=your_webhook_secret # Optional

# --- Task Analysis Configuration (Phase 5) ---
COMPLEXITY_SCORING_AI_PROVIDER=claude
# PRIORITY_WEIGHT_... # Optional weights
DEADLINE_ALERT_THRESHOLD_DAYS=3
WORKLOAD_ESTIMATION_UNIT=story_points

# --- Performance Configuration (Phase 4/7) ---
CACHE_ENABLED=true
CACHE_PROVIDER=memory # or redis
# CACHE_REDIS_URL=redis://...
CACHE_DEFAULT_TTL_SECONDS=3600
QUEUE_ENABLED=false # or true
# QUEUE_PROVIDER=redis
# QUEUE_REDIS_URL=redis://...
# QUEUE_CONCURRENCY=5
```

**Key Configuration Areas:**

*   **`NODE_ENV`**: Controls application behavior (logging, error details).
*   **`LOG_LEVEL`**: Sets logging verbosity.
*   **`JIRA_*`**: Essential for connecting to and synchronizing with the JIRA instance (System of Record).
*   **`*_API_KEY` / `*_MODEL`**: Credentials and default model choices for AI services (Claude, Gemini, Perplexity).
*   **`GITHUB_TOKEN`**: Needed for GitHub integration features.
*   **`MCP_SERVER_*`**: Configures the Model Context Protocol server port and host.
*   **`JIRA_WEBHOOK_SECRET`**: (Optional) Secures the JIRA webhook endpoint.
*   **Analysis/Performance Variables**: Control behavior of advanced features like caching, queuing, prioritization, etc.

**Management:**

*   The `ConfigService` (likely located in `src/config/`) uses libraries like `dotenv` and potentially a schema validator like `zod` to load and validate these variables at application startup.
*   In production, variables should be set securely in the deployment environment, not via `.env` files.

## 4. Components / Public Interfaces

The project exposes functionality primarily through two components: the CLI and the MCP Server.

### 4.1 Component: CLI Interface

*   **Summary**: Provides a command-line interface for users (developers, PMs) to interact with the WBS, manage tasks, trigger AI features, and check synchronization status. Built using `commander.js`.
*   **Installation**: Installed as part of the main project setup (Section 2). Accessed via `nimble` alias or `node dist/cli.js`.
*   **Detailed Features / API (CLI Commands)**:
    *   **WBS CRUD (Create, Read, Update, Delete/Archive)**: Commands exist for each WBS level (PRD, Architecture, Epic, Feature, Story, AcceptanceCriteria, TestCase, Task).
        *   `create-<type>`: Creates a new item (e.g., `create-story --feature-id X ...`). Includes JIRA sync.
        *   `get-<type>`: Retrieves item details (e.g., `get-task --id Y`).
        *   `list-<type>`: Lists items with filters (e.g., `list-tasks --status InProgress`).
        *   `update-<type>`: Modifies an item (e.g., `update-story --id Z --status Done`). Includes JIRA sync.
        *   `archive-<type>`: Marks an item as inactive (e.g., `archive-feature --id A`). Includes JIRA sync.
    *   **AI Drafting (Epic 3.1)**:
        *   `draft-<type>`: Generates AI drafts (e.g., `draft-story --feature-id X [--prompt "..."]`). Requires user review/approval before creation via `create-<type>`.
    *   **AI Analysis & Refinement (Epic 3.2 - Claude)**:
        *   `analyze-prd`: Analyzes PRD for consistency, etc.
        *   `refine-arch`: Suggests improvements for architecture.
        *   `suggest-children` (`suggest-features`, `suggest-stories`): Suggests child items.
        *   `validate-criteria`: Checks AC clarity/testability.
        *   `suggest-test-cases`: Suggests tests based on AC.
        *   `elaborate-task`: Expands task descriptions.
        *   `score-task-complexity`: Estimates task complexity (also Epic 5.1).
    *   **AI Research (Epic 3.3 - Perplexity)**:
        *   `research-<type>`: Conducts research relevant to a WBS item (e.g., `research-feature-viability --id X --query "..."`). Enriches the item with the summary.
    *   **AI Code Assistance (Epic 3.4, 5.2 - Gemini)**:
        *   `analyze-code`: Analyzes code snippets linked to tasks.
        *   `suggest-code`: Suggests code implementation for tasks.
        *   `analyze-performance`: Suggests performance optimizations.
        *   `generate-doc`: Generates technical documentation drafts.
    *   **Task Analysis (Epic 5.1)**:
        *   `estimate-workload`: Estimates effort based on complexity.
        *   `list-<type> --prioritized`: Lists items based on calculated priority.
        *   `update-<type> --deadline YYYY-MM-DD`: Sets deadlines.
        *   `list-<type> --deadline-approaching`: Shows items nearing deadlines.
        *   `suggest-resources`: (Basic) Suggests assignees.
    *   **Integrations (Epic 5.3)**:
        *   `link-github`: Links WBS items to GitHub issues/PRs.
        *   `configure-slack`/`configure-email`: Sets up notification channels.
    *   **Reporting & Visualization (Epic 5.4)**:
        *   `show-dependencies`: Generates dependency graphs (text, Mermaid, DOT).
        *   `show-dashboard`: Displays project progress summaries.
        *   `generate-burndown`: Creates burndown chart data/images.
        *   `generate-report`: Runs custom filtered reports.
        *   `export-data`: Exports WBS data (CSV, JSON).
    *   **Utilities**:
        *   `--help`: Available for all commands/subcommands.
        *   `jira-status`: Shows sync status for an item.
*   **Styling/Feedback**: Uses `chalk` for colored output, `ora` for spinners during long operations, `cli-table3` for formatted lists, `boxen` for messages.

### 4.2 Component: MCP Server

*   **Summary**: Provides a Model Context Protocol (MCP) interface, allowing integration with tools like the Cursor IDE. Built using `fastmcp`. Exposes core WBS and AI functionalities as callable tools/functions.
*   **Installation/Setup**: Runs as a separate process, typically started via `npm run start:server`. Requires environment configuration (port, host, API keys).
*   **Detailed Features / API (MCP Tools - Epic 4.2)**: The server exposes functionalities via named tools. Clients interact by calling these tools with specified parameters. (*Note: Tool names below are examples and might differ slightly in implementation.*)
    *   **WBS Management Tools**:
        *   `get_wbs_item`: Input: `{ id: string, type: WbsType }`. Output: `WbsItem`.
        *   `create_wbs_item`: Input: `{ type: WbsType, data: object }`. Output: `WbsItem`.
        *   `update_wbs_item`: Input: `{ id: string, type: WbsType, data: object }`. Output: `WbsItem`.
        *   `list_wbs_items`: Input: `{ type: WbsType, filters?: object }`. Output: `WbsItem[]`.
        *   `archive_wbs_item`: Input: `{ id: string, type: WbsType }`. Output: `{ success: boolean }`.
        *   `get_jira_status`: Input: `{ id: string }`. Output: `{ jiraKey: string, jiraStatus: string, ... }`.
    *   **AI Integration Tools**:
        *   `draft_wbs_item`: Input: `{ type: WbsType, context: object, userPrompt?: string }`. Output: `{ draftText: string }`.
        *   `analyze_document`: Input: `{ id: string, analysisType: string }`. Output: `{ analysisReport: string }`.
        *   `refine_document`: Input: `{ id: string, type: WbsType, userPrompt?: string }`. Output: `{ refinedTextSuggestion: string }`.
        *   `suggest_children`: Input: `{ parentId: string, parentType: WbsType, childType: WbsType }`. Output: `{ suggestions: Array<{...}> }`.
        *   `validate_criteria`: Input: `{ storyId: string }`. Output: `{ validationReport: string }`.
        *   `suggest_test_cases`: Input: `{ criteriaId: string | storyId: string }`. Output: `{ suggestions: Array<{...}> }`.
        *   `elaborate_task`: Input: `{ taskId: string }`. Output: `{ elaboration: string }`.
        *   `score_task_complexity`: Input: `{ taskId: string }`. Output: `{ score: number | string, justification: string }`.
        *   `research_topic`: Input: `{ itemId: string, itemType: WbsType, query: string }`. Output: `{ researchSummary: string }`.
        *   `analyze_code`: Input: `{ taskId: string, codeContext?: object, analysisPrompt?: string }`. Output: `{ analysisReport: string }`.
        *   `suggest_code`: Input: `{ taskId: string, generationPrompt?: string }`. Output: `{ codeSuggestion: string }`.
        *   `suggest_optimizations`: Input: `{ taskId?: string, codeContext?: object, ... }`. Output: `{ optimizationSuggestions: string }`.
        *   `generate_documentation`: Input: `{ itemId: string, itemType: WbsType, docFormat?: string }`. Output: `{ documentationDraft: string }`.
    *   **Utility Tools (Optional)**:
        *   `check_connection_status`: Input: `{ serviceName: string }`. Output: `{ service: string, status: string, ... }[]`.
*   **Error Handling**: Uses middleware to catch errors and return standardized JSON error responses (Epic 4.1).
*   **JIRA Webhooks**: Listens for incoming JIRA webhooks (e.g., on `/webhooks/jira`) to enable inbound synchronization (Epic 4.1). May use queues for processing.
*   **Performance**: May implement caching and asynchronous handling for long-running operations (Epic 4.3).

## 5. Dependencies and Requirements

*   **Software**:
    *   Node.js (specific version range defined in `package.json`)
    *   npm or yarn
    *   Git
*   **External Services**:
    *   JIRA Instance (Cloud or Server)
    *   Anthropic API (Claude models)
    *   Google AI Platform API (Gemini models)
    *   Perplexity AI API
    *   (Optional) GitHub Account/API
    *   (Optional) Slack Workspace/API
    *   (Optional) Email Service (SMTP or provider API)
    *   (Optional) Redis instance (for caching/queues)
*   **Environment Variables**: Requires API keys/tokens and configuration settings as detailed in Section 3.
*   **Key NPM Dependencies**:
    *   `commander`: CLI framework
    *   `fastmcp`: MCP server framework
    *   `@anthropic-ai/sdk`: Claude SDK
    *   `@google/generative-ai`: Gemini SDK
    *   `axios`: HTTP client (likely used for Perplexity, potentially others)
    *   `jira.js` (or chosen client): JIRA API interaction
    *   `@octokit/rest` (or chosen client): GitHub API interaction
    *   `dotenv`: Environment variable loading
    *   `chalk`, `ora`, `boxen`, `cli-table3`: CLI styling
    *   `typescript`: Core language
    *   `eslint`, `prettier`: Linting and formatting
    *   `jest`, `ts-jest`: Testing framework
    *   `changesets`: Versioning
    *   (Optional) Caching libraries (`node-cache`, `ioredis`), Queue libraries (`bullmq`)

## 6. Advanced Usage Examples

*   **CLI - Complex Filtering**:
    ```bash
    # List high-priority tasks assigned to 'Data' due this month
    nimble list-tasks --filter "priority=High;assignee=Data;deadline<=$(date +%Y-%m)-31" --fields "id,title,status,deadline"
    ```
*   **CLI - Chaining AI Commands**: (Requires user scripting or manual flow)
    ```bash
    # 1. Draft a story
    nimble draft-story --feature-id FEAT-10 --prompt "Focus on error handling" --save-to draft.md
    # 2. User reviews/edits draft.md
    # 3. Create the story from the edited draft
    nimble create-story --feature-id FEAT-10 --title "Enhanced Error Handling" --description "$(cat draft.md)"
    # 4. Generate tests for the new story
    nimble generate-tests --story-id STORY-XYZ
    ```
*   **MCP - Workflow Example** (Conceptual client interaction):
    1.  Client calls `create_wbs_item` (type: story, data: {...}). Server creates story, syncs to JIRA, returns story object with IDs.
    2.  Client calls `suggest_test_cases` (storyId: new_story_id). Server calls AI, returns test case suggestions.
    3.  Client calls `create_wbs_item` (type: test_case, data: {...}) for each approved suggestion. Server creates test cases, syncs to JIRA.
    4.  Client calls `update_wbs_item` (id: test_case_id, type: test_case, data: { status: 'Failing' }). Server updates status, syncs, and triggers TDD workflow to create linked task.
*   **Performance Tuning**: Adjust `CACHE_ENABLED`, `CACHE_PROVIDER`, `CACHE_TTL_SECONDS`, `QUEUE_ENABLED`, `QUEUE_CONCURRENCY` in `.env` based on monitoring and load testing (Epic 4.3, 7.2).
*   **Visualization**: Use `show-dependencies --format=mermaid` and paste output into a Mermaid renderer/Markdown file. Use `export-data --format=csv` and import into spreadsheet software for custom charting.

This documentation provides a comprehensive overview of the `cursor-be-nimble` repository, its core functionalities, configuration, and usage patterns for both its CLI and MCP server interfaces.

--- End of Documentation ---
