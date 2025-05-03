# Task `[TASK-ID]` Context Document: `[Task Title]`

_**TASK-ID Format:** EpicNum.FeatureNum.StoryNum.TaskNum (e.g., 1.2.3.4)_

## 0. Document Metadata

| Key             | Value                                                                                |
| --------------- | ------------------------------------------------------------------------------------ |
| Project         | [Project Name, e.g., cursor-be-nimble]                                               |
| PRD             | [Link to PRD Document](./01-prd-template.md)                                         |
| Architecture PoV| [Link to Arch PoV Document](./02-arch-pov-template.md)                               |
| Epic            | [Link to Parent Epic Document](./03-epic-template.md#EPIC-ID)                        |
| Feature         | [Link to Parent Feature Document](./04-feature-template.md#FEAT-ID)                  |
| Story           | [Link to Parent Story Document](./05-story-template.md#STORY-ID)                     |
| Task ID         | `TASK-[EpicNum.FeatureNum.StoryNum.TaskNum]`                                         |
| Title           | `[Task Title]`                                                                       |
| Status          | To Do / In Progress / Blocked / Done                                                 |
| Version         | 0.0.0                                                                                |
| Date            | [YYYY-MM-DD]                                                                         |

---

**Project Context & Traceability**

*   **Standard Document Hierarchy:** `PRD -> Architecture PoV (Arch-PoV) -> Epics -> Features -> Stories -> Tasks`
*   **Traceability Requirement:** Each subsequent document (e.g., Arch-PoV, Epic, Story) **MUST** link back to its direct parent document using the Markdown format `[Document Title](link-to-document-markdown-file)` and include relevant parent identifiers (e.g., Parent ID, Title) to ensure full context traceability down to the Task level.
*   **Hierarchical Numbering:** Items will follow a hierarchical numbering scheme based on their parent (e.g., Epic `1` may contain Features `1.1`, `1.2`; Feature `1.2` may contain Stories `1.2.1`, `1.2.2`).

---

## 1. Task Objective

_Provide a concise (1-sentence) summary of the specific technical action to be performed. What is the primary outcome?_

--- 

## 2. Contribution to Story Acceptance Criteria

_Table referencing the specific Acceptance Criteria scenarios from the parent Story (`[Story Title](./05-story-template.md#STORY-ID)`) that this task helps fulfill. Provides crucial "why" context._

| Parent Story AC ID (`AC-S-ID`) | Acceptance Criterion Scenario Description (from Story)                             |
| :------------------------------- | :--------------------------------------------------------------------------------- |
| [`[AC-S-ID]`](./05-story-template.md#ac-s-id) | _[Copy the Scenario Name/Description from parent story]_                          |
| [`[AC-S-ID]`](./05-story-template.md#ac-s-id) | _[Copy the Scenario Name/Description from parent story]_                          |
| ...                              | ...                                                                                |

--- 

## 3. Technical Implementation Requirements

_This is the core instruction set for the AI. Be extremely specific and unambiguous._

*   **Files to Modify/Create:** 
    ```plaintext
    src/services/auth.ts
    tests/unit/auth.test.ts
    ```
*   **Target Functions/Classes/Modules:** Implement/Modify function `AuthService.login` in `src/services/auth.ts`.
*   **Input Requirements:** Function signature must be `async login(email: string, password: string): Promise<User | null>`.
*   **Output Requirements:** Returns `User` object (defined in `src/models/user.ts`) on successful authentication, `null` otherwise. Must not throw unhandled exceptions for standard auth failures.
*   **Specific Logic/Algorithm:**
    1.  Validate email format using `validator.isEmail()` (from `validator` library - `DEP-T-ID`).
    2.  Find user by email in database (using `UserRepository.findByEmail` - `DEP-T-ID`). If not found, return `null`.
    3.  Compare provided password with stored hash using `bcrypt.compare()` (`DEP-T-ID`).
    4.  If match, return user object. Otherwise, return `null`.
*   **Libraries/Dependencies to Use:** 
    *   `bcrypt` (`DEP-T-ID`) for password comparison.
    *   `validator` (`DEP-T-ID`) for email validation.
    *   `UserRepository` (`DEP-T-ID`) for database access.
*   **Error Handling:** Log database errors using `logger.error("DB error in login", error)`. Do not expose DB errors directly to caller; return `null` on auth failure.
*   **Code Style/Conventions:** Adhere to project ESLint/Prettier configuration found at [Link to Config/Docs].
*   **Constraints/NFRs:** Reference parent Feature/Story NFRs if directly applicable (e.g., [`NFR-F-ID`](./04-feature-template.md#nfr-f-id) - Response time target). Ensure inputs are treated as untrusted.

--- 

## 4. Agentic Style & Guardrail Considerations (If Applicable)

_Reminders if this task involves generating user output or handling sensitive data. Reference specific parent document sections/IDs._

*   **Agentic Style:** [e.g., N/A for this backend task OR If generating logs/errors visible externally, ensure they follow tone guidelines from `ASTRAT-ID`.]
*   **Guardrails:** [e.g., Task involves password comparison; ensure only hashed passwords are logged or handled as per `PRD Sec 7` and `DEC-A-ID`.]

--- 

## 5. Test Cases (Task-Level)

_List specific unit/integration tests the AI must create or ensure pass for *this task*, verifying the requirements in Section 3._

### Test Case `[TEST-T-ID]`: [e.g., Successful Login]
_**TEST-T-ID Format:** [TaskID].[TestNum] (e.g., 1.2.3.4.1.1)_
*   **Given** Mock `UserRepository.findByEmail` returns a valid user with correctly hashed password.
*   **And** Mock `bcrypt.compare` returns `true`.
*   **When** `AuthService.login` is called with the correct email and password.
*   **Then** The function returns the expected `User` object.

### Test Case `[TEST-T-ID]`: [e.g., User Not Found]
*   **Given** Mock `UserRepository.findByEmail` returns `null`.
*   **When** `AuthService.login` is called.
*   **Then** The function returns `null`.

### Test Case `[TEST-T-ID]`: [e.g., Incorrect Password]
*   **Given** Mock `UserRepository.findByEmail` returns a valid user.
*   **And** Mock `bcrypt.compare` returns `false`.
*   **When** `AuthService.login` is called with the correct email but wrong password.
*   **Then** The function returns `null`.

_(Add more detailed test cases covering validation, error logging, etc.)_

--- 

## 6. Dependencies (Task-Level)

_List specific technical dependencies required *before* this task can be implemented._

| ID          | Dependency Type          | Name / ID / Version                 | Notes                                       |
| :---------- | :----------------------- | :---------------------------------- | :------------------------------------------ |
| `DEP-T-01`  | Library                  | `bcrypt`, `validator` installed     | Must be available in `package.json`         |
| `DEP-T-02`  | Internal Module/Interface| `UserRepository` interface defined | Required for mocking and implementation     |
| ...         | ...                      | ...                                 | ...                                         |

--- 

## 7. Definition of Done (Task Level)

_Checklist confirming task completion._

*   [ ] Code implemented according to Technical Implementation Requirements (Section 3).
*   [ ] All specified Test Cases (Section 5, `TEST-T-ID`s) are implemented and passing.
*   [ ] Code adheres to project Code Style/Conventions (Section 3).
*   [ ] Implementation correctly contributes to fulfilling Parent Story Acceptance Criteria (Section 2).
*   [ ] Agentic Style & Guardrail Considerations (Section 4) addressed, if applicable.
*   [ ] Code committed/pushed to [Branch Name/PR Link].

--- 

## 8. Document History

| Version | Date       | Author(s) | Changes                                                          |
| :------ | :--------- | :-------- | :--------------------------------------------------------------- |
| ...     | ...        | ...       | ...                                                              |
