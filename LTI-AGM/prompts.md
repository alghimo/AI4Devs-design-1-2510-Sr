# Prompts Log

## Setup Phase
- **Workflow**: `/cmd-setup-memory-bank`
- **Action**: Initialized memory bank structure and context from `AI4Devs-design-1-2510-Sr/ReadMe.md`.

## Design Phase
- **Workflow**: `/cmd-create-plan`
- **Action**: Created `LTI_DESIGN_PLAN.md`.
- **Clarification Questions**:
    1.  **Lean Canvas**: Is a Markdown table acceptable if Mermaid proves too cluttered for a Lean Canvas?
        - **Answer**: Yes. If Mermaid is cluttered, provide Mermaid + Markdown table + optional image/other.
    2.  **C4 Component**: Is "Candidate Matching Engine" a good component to focus on for the C4 diagram?
        - **Answer**: Yes, "Candidate Matching Engine" is perfect.

## Implementation Phase
- **Action**: Created `AI4Devs-design-1-2510-Sr/LTI-AGM/LTI-AGM.md` containing:
    - Research & Analysis (Description, Features, Lean Canvas).
    - Functional Design (3 Use Cases with diagrams).
    - Technical Design (Data Model, System Architecture, C4 Component Diagram).
- **Action**: Created `AI4Devs-design-1-2510-Sr/LTI-AGM/prompts_context.md` explaining workflows and memory bank.

## Refactoring Phase
- **User Request**: Refactor architecture to Hexagonal + Vertical Slicing + Screaming Architecture. Use API + Web App structure instead of microservices.
- **Action**: Updated `LTI-AGM.md`, `PROJECT_DEBRIEF.md`, and `LTI_DESIGN_PLAN.md` to reflect these changes.

## Bug Fix
- **User Report**: The Mermaid `architecture-beta` diagram failed to render due to syntax errors in service labels (spaces/parentheses).
- **Action**: Fixed the Mermaid syntax in `LTI-AGM.md` by simplifying labels.

# Full prompts

## User Input (Setup Memory Bank)

@[/cmd-setup-memory-bank] You can initialize it with the structure, and the basic context for the project from @[AI4Devs-design-1-2510-Sr/ReadMe.md] , but ignore other documents in that folder and @[TASK.md] / @[examples] for now

## User Input (Create Plan)

@[/cmd-create-plan] Create the plan for what is requested in @[TASK.md] ,  creating the regular documents of the memory bank from the workflow, and the extra deliverables asked in @[TASK.md] (the folder and the three files)

#### Clarification questions

1. Lean Canvas: Is a Markdown table acceptable if Mermaid proves too cluttered for a Lean Canvas?
2. C4 Component: Is "Candidate Matching Engine" a good component to focus on for the C4 diagram?

#### User Input (answers to clarification questions)

1. If Mermaid proves too cluttered, provide both the Mermaid, the Markdown, and if you want, an image with the Lean Canvas as well / some other type of diagram (as an extra)
2. Candidate Matching Engine is perfect

### Next question

I have updated the LTI_DESIGN_PLAN.md with your feedback.

Do you want me to create a Ticket from this plan? (This will trigger the /cmd-create-ticket workflow).

#### User Input (answer)

yes, but instead of creating a github ticket, create a folder @memory-bank/tickets/ and create a ticket inside it "01_xx.md", where XX is a short, meaningful name for the ticket. The start implementing it. Make sure you keep track of the whole conversation (prompts + clarification questions + answers in the prompts.md file from the deliverables.

## User Input (request updating from microservices to hexagonal architecture, split API / Web App)

Instead of following a microservices architecture, I would like two things:
- Follow hexagonal architecture + vertical slicing + screaming architecture
- We should have an API, and a web app that connects to that API. That way it will be a lot easier if in the future we want to e.g. add a mobile app.
Update the necessary documents to reflect this, both in the memory bank and in the deliverables mantioned in @[TASK.md] . Regarding the @[AI4Devs-design-1-2510-Sr/LTI-AGM/prompts.md] file, this prompt should be appended to the prompts that are there already, as well as any clarification questions (if you need to ask things) and my answers

## User Input (diagram error)

Now the diagram for 4.2 is failing to show, this is the error I get:
Parsing failed: unexpected character: ->[<- at offset: 81, skipped 1 characters.
unexpected character: ->]<- at offset: 95, skipped 1 characters. Expecting: one of these possible Token sequences:
  1. [NEWLINE]
  2. [EOF]
but found: 'Web'
Expecting token of type ':' but found `App`.
Expecting: one of these possible Token sequences:
  1. [--]
  2. [-]
but found: 'App'
Expecting: one of these possible Token sequences:
  1. [NEWLINE]
  2. [EOF]
but found: '(SPA)'
Expecting token of type 'EOF' but found `(SPA)`.
Expecting token of type ':' but found `
`.
Expecting: one of these possible Token sequences:
  1. [--]
  2. [-]
but found: '
'
Expecting token of type 'ID' but found `
`.
Fix it and update this request in the @[AI4Devs-design-1-2510-Sr/LTI-AGM/prompts.md]
