# Epic `[EPIC-ID]` Context Document: `[Epic Title]`

_**EPIC-ID Format:** EpicNum (e.g., 1)_

## 0. Document Metadata

| Key                | Value                                                           |
| ------------------ | --------------------------------------------------------------- |
| Project            | [Project Name]                                                  |
| PRD                | [Link to PRD Document](./01-prd-template.md)                    |
| Architecture PoV   | [Link to Arch PoV Document](./02-arch-pov-template.md)          |
| Epic ID            | `EPIC-[EpicNum]`                                                |
| Title              | `[Epic Title]`                                                  |
| Status             | Draft / Proposed / Accepted / In Progress / Done / Deprecated   |
| Version            | 0.0.0                                                           |
| Date               | [YYYY-MM-DD]                                                    |

---

**Project Context & Traceability**

* **Standard Document Hierarchy:** `PRD -> Architecture PoV (Arch-PoV) -> Epics -> Features -> Stories -> Tasks`
* **Traceability Requirement:** Each subsequent document (e.g., Arch-PoV, Epic, Story) **MUST** link back to its direct parent document using the Markdown format `[Document Title](link-to-document-markdown-file)` and include relevant parent identifiers (e.g., Parent ID, Title) to ensure full context traceability down to the Task level.
* **Hierarchical Numbering:** Items will follow a hierarchical numbering scheme based on their parent (e.g., Epic `1` may contain Features `1.1`, `1.2`; Feature `1.2` may contain Stories `1.2.1`, `1.2.2`).

---

## 1. Context & Background

_Provide a brief summary explaining why this epic exists. Link back to the specific goals in the parent Phase document and relevant business objectives/requirements/goals from the PRD or Architecture PoV using their unique IDs and markdown links. Briefly mention the problem this epic solves or the opportunity it addresses._

* **Parent Phase Goal(s):** [`[Phase Goal ID]`](./path/to/phase-doc.md#phase-goal-id) - [Description]
* **Related PRD Goal(s):** [`[e.g., GOAL-00X]`](./01-prd-template.md#goal-00x) - [Description]
* **Related Arch PoV Goal(s):** [`[e.g., GOAL-A-00Y]`](./02-arch-pov-template.md#goal-a-00y) - [Description]

### 1.1 Problem Statement / Opportunity

_Clearly articulate the specific challenge, user need, or opportunity this Epic addresses._

### 1.2 Narrative (Optional)

_Describe the epic from a user or system perspective (e.g., "As a [persona], I want to [objective], so that [value]")._

---

## 2. Epic Goal & Objective

_State the primary, specific goal (`GOAL-EP-[EpicID]`) of this epic. What is the intended outcome? How does it contribute to the phase goals and overall product vision?_

### 2.1 Success Metrics / KPIs

_How will we know this epic is successful? Define measurable criteria linking back to PRD/Arch PoV NFRs or KPIs where applicable._


| ID            | Metric Description                                       | Target / Threshold | Related PRD/Arch NFR/KPI (Optional)                                                                  | Status   |
| :-------------- | :--------------------------------------------------------- | :------------------- | :----------------------------------------------------------------------------------------------------- | :--------- |
| `KPI-EP-[ID]` | [e.g., Feature Y Completion Rate]                        | > Z%               | [`[e.g., NFR-00A]`](./01-prd-template.md#nfr-00a), [`[e.g., KPI-00X]`](./01-prd-template.md#kpi-00x) | Proposed |
| `KPI-EP-[ID]` | [e.g., Performance improvement for affected component X] | < N ms Latency     | [`[e.g., NFR-00B]`](./02-arch-pov-template.md#nfr-00b)                                               | Proposed |
| ...           | ...                                                      | ...                | ...                                                                                                  | ...      |

### 2.2 Acceptance Criteria

_Define the high-level conditions that must be met for the epic to be considered complete. These should be testable._


| ID           | Criteria Description                                  | Status   |
| :------------- | :------------------------------------------------------ | :--------- |
| `AC-EP-[ID]` | [e.g., All features ([FEAT-ID], [FEAT-ID]) are Done.] | Proposed |
| `AC-EP-[ID]` | [e.g., Performance meets`KPI-EP-[ID]` target.]        | Proposed |
| `AC-EP-[ID]` | [e.g., Documentation for the epic is complete.]       | Proposed |
| ...          | ...                                                   | ...      |

---

## 3. Scope

_Clearly define the boundaries of this epic._

### 3.1 In-Scope

_List key features, components, or functionalities included in this epic._


| ID                 | Description                                             |
| :------------------- | :-------------------------------------------------------- |
| `SCOPE-IN-EP-[ID]` | [e.g., Feature`[FEAT-ID]`: [Feature Name]]              |
| `SCOPE-IN-EP-[ID]` | [e.g., Component`[COMP-ID]`: Refactoring for epic goal] |
| ...                | ...                                                     |

### 3.2 Out-of-Scope

_List related features, components, or functionalities explicitly excluded or deferred to manage expectations._


| ID                  | Description                                                                 |
| :-------------------- | :---------------------------------------------------------------------------- |
| `SCOPE-OUT-EP-[ID]` | [Excluded Item 1, e.g., Integration with System Z (planned for next Phase)] |
| `SCOPE-OUT-EP-[ID]` | [Excluded Item 2, e.g., UI redesign of related Component X]                 |
| ...                 | ...                                                                         |

---

## 4. Features Breakdown

_List the specific Features that make up this Epic. Each feature should represent a distinct piece of functionality or deliverable and should have its own context document linked._


| Feature ID (`FEAT-[EpicID].[FeatureNum]`) | Feature Name      | Short Description                            | Status   | Link to Feature Document                                                 |
| :------------------------------------------ | :------------------ | :--------------------------------------------- | :--------- | :------------------------------------------------------------------------- |
| `FEAT-[EpicID].01`                        | [Feature 1 Title] | [Brief description of the feature's purpose] | Proposed | [`[Feature 1 Title]`](./04-feature-template.md) _(Copy and rename this)_ |
| `FEAT-[EpicID].02`                        | [Feature 2 Title] | [Brief description of the feature's purpose] | Proposed | [`[Feature 2 Title]`](./04-feature-template.md) _(Copy and rename this)_ |
| ...                                       | ...               | ...                                          | ...      | ...                                                                      |

---

## 5. Implementation Details / Component Design

_(Optional: May live primarily in Feature docs, but high-level Epic design decisions can go here.)_
_Provide the core technical design choices or component overviews relevant at the Epic level. Break down into logical sub-sections as needed._

### 5.1 [Component/Module 1 Overview]

_Describe the high-level design, purpose, and interaction with other components._
_Reference relevant Arch PoV components: [`[e.g., COMP-0X]`](./02-arch-pov-template.md#comp-0x)_

### 5.2 [Key Algorithm / Data Structure / Pattern]

_Describe significant technical elements specific to this epic._

---

## 6. Configuration

_Document any specific configuration required or introduced by this epic._

### 6.1 Environment Variables


| ID            | Variable Name | Purpose                                    | Example Value (Optional) | Status   |
| :-------------- | :-------------- | :------------------------------------------- | :------------------------- | :--------- |
| `ENV-EP-[ID]` | ENV_VAR_1     | [e.g., API key for Service X used in Epic] | `abc123xyz`              | Required |
| `ENV-EP-[ID]` | ENV_VAR_2     | [e.g., Feature flag toggle for Epic scope] | `true` / `false`         | Optional |
| ...           | ...           | ...                                        | ...                      | ...      |

### 6.2 Configuration Files


| ID             | File Path             | Purpose / Key Settings                                    | Status   |
| :--------------- | :---------------------- | :---------------------------------------------------------- | :--------- |
| `CONF-EP-[ID]` | `path/to/config.json` | [e.g., Contains settings for Component A related to Epic] | Required |
| ...            | ...                   | ...                                                       | ...      |

---

## 7. Dependencies

_List all significant dependencies for this epic._


| ID            | Dependency Type         | Name / ID / Version            | Description / Notes                                                         |
| :-------------- | :------------------------ | :------------------------------- | :---------------------------------------------------------------------------- |
| `DEP-EP-[ID]` | Project (Epic/Feature)  | `[EPIC-ID]` / `[FEAT-ID]`      | [e.g., Depends on completion of Epic X / Feature Y]                         |
| `DEP-EP-[ID]` | Library/Package         | `library-name@X.Y.Z`           | [e.g., Used for core data processing across multiple features in this Epic] |
| `DEP-EP-[ID]` | External System/Service | [e.g., Service Name API vN]    | [e.g., Central service consumed by the Epic]                                |
| `DEP-EP-[ID]` | Tool                    | [e.g., Specific Linter Config] | [e.g., Required build/dev tool]                                             |
| ...           | ...                     | ...                            | ...                                                                         |

---

## 8. Integration & Testing Strategy

_Describe how the components/features of this epic integrate with other parts of the system. Outline the primary testing approaches (unit, integration, E2E, **agentic evaluation**) relevant to this epic's scope._

* **Integration Points:** [Describe key interfaces and interactions with other system parts affected/introduced by this Epic]
* **Testing Focus:** [Key areas for unit, integration, E2E testing *at the Epic level* - focusing on the interaction between its Features]
* **Agentic Evaluation:** _(If applicable)_ [How will the overall impact on agentic style/behavior resulting from this Epic's Features be evaluated? Reference relevant KPIs (`KPI-EP-ID`) or Arch NFRs (`NFR-ID`)]

---

## 9. Constraints, Assumptions & Risks

_Document known limitations, assumptions made, and potential risks related to this epic._

### 9.1 Constraints


| ID            | Constraint Description                                    |
| :-------------- | :---------------------------------------------------------- |
| `CON-EP-[ID]` | [e.g., Must use existing database schema for Component Y] |
| ...           | ...                                                       |

### 9.2 Assumptions


| ID            | Assumption Description                                             | Status / Verification                          |
| :-------------- | :------------------------------------------------------------------- | :----------------------------------------------- |
| `ASM-EP-[ID]` | [e.g., External API Z (`DEP-EP-ID`) will maintain response format] | [e.g., Monitoring API Docs / Contract Testing] |
| ...           | ...                                                                | ...                                            |

### 9.3 Risks


| ID             | Description                                                               | Likelihood | Impact | Mitigation Strategy                                            |
| :--------------- | :-------------------------------------------------------------------------- | :----------- | :------- | :--------------------------------------------------------------- |
| `RISK-EP-[ID]` | [e.g., Performance degradation under load for new algorithm in Feature X] | Medium     | High   | [e.g., Implement monitoring (`KPI-EP-ID`), Load Test Feature]  |
| `RISK-EP-[ID]` | [e.g., Complexity of integrating Features X and Y]                        | Medium     | Medium | [e.g., Early integration testing, Clear interface definitions] |
| ...            | ...                                                                       | ...        | ...    | ...                                                            |

---

## 10. Stakeholders

_Identify key stakeholders involved in or impacted by this epic._


| Role                  | Name / Team     | Involvement / Responsibility                   |
| :---------------------- | :---------------- | :----------------------------------------------- |
| Product Owner         | [Name]          | Requirements, Prioritization, Acceptance       |
| Architect / Tech Lead | [Name]          | Design Guidance, Technical Review              |
| Development Team(s)   | [Team(s)/Names] | Implementation, Unit/Integration Testing       |
| QA / Test Engineer    | [Name/Team]     | Test Plan Creation, E2E Testing, Validation    |
| UX/UI Designer        | [Name]          | Design Input/Review (if applicable)            |
| Ops / Infrastructure  | [Team]          | Deployment Support, Monitoring Setup           |
| Business Stakeholder  | [Name/Dept]     | Business Context, Final Review (if applicable) |
| ...                   | ...             | ...                                            |

---

## 11. Epic Outcome / Summary

_Summarize the final state or key deliverables resulting from the completion of this epic. What new capabilities exist? What is the expected impact on users or the system? How does it meet `GOAL-EP-[EpicID]`?_

---

## 12. Document History


| Version   | Date         | Author(s)   | Changes                                       |
| :-------- | :----------- | :---------- | :-------------------------------------------- |
| ...       | ...          | ...         | ...                                           |
