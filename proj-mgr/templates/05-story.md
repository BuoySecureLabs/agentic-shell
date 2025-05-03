# Story `[STORY-ID]` Context Document: `[Story Title]`

_**STORY-ID Format:** EpicNum.FeatureNum.StoryNum (e.g., 1.2.3)_

## 0. Document Metadata

| Key             | Value                                                                     |
| --------------- | ------------------------------------------------------------------------- |
| Project         | [Project Name, e.g., cursor-be-nimble]                                    |
| PRD             | [Link to PRD Document](./01-prd-template.md)                              |
| Architecture PoV| [Link to Arch PoV Document](./02-arch-pov-template.md)                    |
| Epic            | [Link to Parent Epic Document](./03-epic-template.md#EPIC-ID)             |
| Feature         | [Link to Parent Feature Document](./04-feature-template.md#FEAT-ID)       |
| Story ID        | `STORY-[EpicNum.FeatureNum.StoryNum]`                                     |
| Title           | `[Story Title]`                                                           |
| Status          | Draft / Ready / In Progress / Blocked / Done                              |
| Version         | 0.0.0                                                                     |
| Date            | [YYYY-MM-DD]                                                              |

---

**Project Context & Traceability**

*   **Standard Document Hierarchy:** `PRD -> Architecture PoV (Arch-PoV) -> Epics -> Features -> Stories -> Tasks`
*   **Traceability Requirement:** Each subsequent document (e.g., Arch-PoV, Epic, Story) **MUST** link back to its direct parent document using the Markdown format `[Document Title](link-to-document-markdown-file)` and include relevant parent identifiers (e.g., Parent ID, Title) to ensure full context traceability down to the Task level.
*   **Hierarchical Numbering:** Items will follow a hierarchical numbering scheme based on their parent (e.g., Epic `1` may contain Features `1.1`, `1.2`; Feature `1.2` may contain Stories `1.2.1`, `1.2.2`).

---

## 1. User Story Description

**As a** [Type of User / Persona - Link to [`PRD Sec 3`](./01-prd-template.md#3-target-users--personas) if applicable],
**I want to** [Perform some action / achieve some goal related to the Feature],
**So that** [I get some benefit / value described in the Feature/Epic].

_(Add 1-2 sentences providing brief context or clarification if needed)._

---

## 2. Acceptance Criteria (BDD Format)

_These criteria define when the story is considered "Done" and serve as the basis for automated tests (TDD/BDD). Each scenario should be testable and unambiguous._

### Scenario `[AC-S-ID]`: [Descriptive Scenario Name, e.g., Happy Path]

_**AC-S-ID Format:** [StoryID].[ScenarioNum] (e.g., 1.2.3.4.1)_

*   **Given** [Some initial context or precondition relevant to the story]
*   **And** [Another precondition (optional)]
*   **When** [An action is performed by the user or system]
*   **Then** [A specific, verifiable outcome is expected]
*   **And** [Another verifiable outcome (optional)]

### Scenario `[AC-S-ID]`: [Another Scenario Name, e.g., Edge Case]

*   **Given** [Different context]
*   **When** [Different action]
*   **Then** [Different outcome]

_(Add as many uniquely identified scenarios as needed to cover the requirements fully)._

---

## 3. Scope Definition

_Clearly define the boundaries of this specific story._

### 3.1 In-Scope

| ID             | Deliverable Description                                                              |
| :------------- | :----------------------------------------------------------------------------------- |
| `SCOPE-IN-S-[ID]`| [Specific function/UI element/API change included in this story]                     |
| ...            | ...                                                                                  |

### 3.2 Out-of-Scope

| ID              | Excluded Item Description                                                            |
| :-------------- | :----------------------------------------------------------------------------------- |
| `SCOPE-OUT-S-[ID]`| [Related item explicitly NOT part of this story, e.g., Error handling for scenario Y]|
| ...             | ...                                                                                  |

---

## 4. Inherited Context & Agentic Requirements

_Translate relevant parent context into actionable constraints for this story's implementation._

*   **Relevant Architectural Decisions/Components:**
    *   [Must use/interact with `[COMP-ID]`](./02-arch-pov-template.md#comp-id) as per [`DEC-A-ID`](./02-arch-pov-template.md#dec-a-id).
    *   [Consider performance implications related to `NFR-A-ID`](./02-arch-pov-template.md#nfr-a-id).
*   **Agentic Style Application:**
    *   _Reference the core Agentic Strategy:_ [`ASTRAT-ID`](./02-arch-pov-template.md#astrat-id).
    *   _Story-Specific Tone/Phrasing:_ [e.g., Success messages for this action should be [style], e.g., "[Example Text]". Error messages must follow pattern X defined in `ASTRAT-ID`.]
*   **Guardrail Application:**
    *   _Critical Guardrails from [`PRD Sec 7`](./01-prd-template.md#7-behavioral-requirements--guardrails) relevant here:_ [e.g., "MUST NOT process data type Y", "MUST adhere to data retention policy Z"].
    *   _Implementation Ref:_ See `DEC-A-ID` for guardrail implementation approach.

---

## 5. Technical Details & Constraints

_Provide crucial technical specifics for implementation._

*   **Affected Components/Files:** `[path/to/file1.ext]`, `[path/to/moduleA/]` (Reference Arch `COMP-ID`s if applicable)
*   **Key Libraries/Frameworks:** Use `[library-name@X.Y.Z]` (`DEP-S-ID`), Avoid `[other-library]`.
*   **Data Models/Types:** Use/Define `[TypeName]` (Link to definition if external).
*   **API Contracts (if applicable):** `[METHOD] /path/to/api` (Request: `[SchemaLink]`, Response: `[SchemaLink]`)
*   **Error Handling Expectations:** [e.g., Log errors using [Logger Format], return specific HTTP status code [Code] for condition Y].
*   **Implementation Guidance:** [e.g., Use [Pattern Name] for [Purpose], ensure function X is idempotent, follow coding standards [Link]]. Reference relevant `DEC-A-ID`s.
*   ...

---

## 6. Implementation Tasks (Traceability Downwards)

_Break the story down into the specific technical tasks required for implementation. Link to task documents/tickets._

| Task ID (`TASK-[StoryID].[TaskNum]`) | Description                                      | Status      | Assignee | Estimate (Optional) | Link to Task Document                             |
| :----------------------------------- | :----------------------------------------------- | :---------- | :------- | :------------------ | :------------------------------------------------ |
| `TASK-[StoryID].01`                  | Implement API endpoint for [action]              | To Do       | [Name]   | [Hours/SP]          | [`[Task 1 Title]`](./path/to/task-01.md)        |
| `TASK-[StoryID].02`                  | Update UI component [component name]             | To Do       | [Name]   | [Hours/SP]          | [`[Task 2 Title]`](./path/to/task-02.md)        |
| `TASK-[StoryID].03`                  | Write unit tests for [service/module]            | To Do       | [Name]   | [Hours/SP]          | [`[Task 3 Title]`](./path/to/task-03.md)        |
| `TASK-[StoryID].04`                  | Create database migration script                 | To Do       | [Name]   | [Hours/SP]          | [`[Task 4 Title]`](./path/to/task-04.md)        |
| ...                                  | ...                                              | ...         | ...      | ...                 | ...                                               |

---

## 7. Testing Strategy / Test Case Links

_Outline the approach for testing this story, linking Acceptance Criteria (Sec 2) to specific test implementations (potentially defined in Task docs)._

*   **Testing Approach:** [e.g., Focus on integration testing due to interaction with Service X. Unit tests cover calculation logic.]
*   **Test Case Summary:**

    | AC Scenario Ref (`AC-S-ID`) | Test Case ID (`TEST-[StoryID].[TestNum]`) | Description                                    | Type (Unit/Int/E2E/Manual) | Status      |
    | :-------------------------- | :-------------------------------------- | :--------------------------------------------- | :------------------------- | :---------- |
    | `[AC-S-ID]`                 | `TEST-[StoryID].01`                     | Verify [specific outcome of Scenario 1]        | Unit                       | To Do       |
    | `[AC-S-ID]`                 | `TEST-[StoryID].02`                     | Verify [another outcome of Scenario 1]       | Integration                | To Do       |
    | `[AC-S-ID]`                 | `TEST-[StoryID].03`                     | Verify [outcome of Scenario 2 under condition] | Manual                     | Not Started |
    | ...                         | ...                                     | ...                                            | ...                        | ...         |

---

## 8. Dependencies (Story Level)

_List specific dependencies required *before* this story can start or be completed._

| ID            | Dependency Type     | Name / ID / Version          | Notes                                          |
| :------------ | :------------------ | :--------------------------- | :--------------------------------------------- |
| `DEP-S-[ID]`  | Story               | `STORY-[ID]`                 | Must be completed first.                       |
| `DEP-S-[ID]`  | Configuration       | `ENV-F-ID` variable set      | Required for API call.                       |
| `DEP-S-[ID]`  | External Service    | Service X available          | Endpoint must be reachable.                  |
| ...           | ...                 | ...                          | ...                                            |

---

## 9. Design & UI/UX (Optional)

_Embed or link to relevant wireframes, mockups, design specifications, or prototypes._

*   [Link to Figma/Sketch/etc. for `STORY-ID`]
*   _Embedded Wireframe Image (if small and specific to this story)_ 

---

## 10. Open Questions (Story Level)

_List specific questions needing answers for this story._

| ID      | Question                                            | Status (Open/Answered) | Owner       | Due Date   |
| :------ | :-------------------------------------------------- | :--------------------- | :---------- | :--------- |
| `Q-S-01`| Clarification needed on AC `[AC-S-ID]` regarding Y? | Open                   | [Name/PM]   | [YYYY-MM-DD] |
| ...     | ...                                                 | ...                    | ...         | ...        |

---

## 11. Definition of Done (Story Level)

_Checklist for confirming story completion._

*   [ ] All Acceptance Criteria (Section 2, `AC-S-ID`s) are met and verified by tests.
*   [ ] All linked Test Cases (Section 7, `TEST-[StoryID].XX`) are passing.
*   [ ] All Implementation Tasks (Section 6, `TASK-[StoryID].XX`) are completed.
*   [ ] Code reviewed and approved.
*   [ ] Code merged to the main branch.
*   [ ] Adherence to Agentic Style & Guardrails (Section 4) verified.
*   [ ] Necessary documentation (code comments, linked Task docs) updated.
*   [ ] Story provides the intended user value described in Section 1.

---

## 12. Document History

| Version | Date       | Author(s) | Changes                                                          |
| :------ | :--------- | :-------- | :--------------------------------------------------------------- |
| ...     | ...        | ...       | ...                                                              |
