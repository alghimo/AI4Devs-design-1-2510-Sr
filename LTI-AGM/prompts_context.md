# Prompts Context

## Workflows Used
- **/cmd-setup-memory-bank**: Initialized the `memory-bank` directory structure and populated it with project context from the original `ReadMe.md`.
- **/cmd-create-plan**: Analyzed requirements and created the `LTI_DESIGN_PLAN.md` to guide the design phase.

## Memory Bank
The `memory-bank` directory contains the persistent context for the project:
- **PROJECT_DEBRIEF.md**: High-level overview and goals.
- **PROJECT_PLAN.md**: Detailed plan and deliverables.
- **RULES.md**: Project rules and constraints.
- **IMPLEMENTATION_STATUS.md**: Current progress tracking.
- **FEATURES.md**: Planned features.
- **ROADMAP.md**: Project phases.
- **STANDARDS.md**: Documentation and coding standards.
- **TICKETS.md**: Ticket tracking.
- **user/**: User-specific documents (Seed, TODOs, Ideas).
- **tickets/**: Local tickets for task tracking (e.g., `01_design_lti_ats.md`).

## ASCII Diagram

This is the file structure of the whole memory bank:

```ascii
memory-bank/
├── PROJECT_DEBRIEF.md          # Main context, goals, vision, architecture
├── PROJECT_PLAN.md             # Full project plan
├── RULES.md                    # User requirements and rules
├── IMPLEMENTATION_STATUS.md    # Summary of implemented vs pending tasks
├── FEATURES.md                 # Detailed view of implemented features & learnings
├── ROADMAP.md                  # Project phases and sub-phases
├── STANDARDS.md                # Naming conventions, methodologies
├── TICKETS.md                  # Summary table of Github tickets
├── user/                       # User-specific documentation and context
│   ├── PROJECT_SEED.md         # Initial prompt and clarification Q&A
│   ├── TODO.md                 # Low priority fixes/chores
│   ├── FUTURE_IDEAS.md         # Backlog for future improvements
│   └── project_seed/           # Additional context for project seed
│       └── [context_file].md
├── plans/                      # Plan documentss
│   ├── [specific_plan].md
│   └── specific_plan-docs/
│       └── [misc_doc].md       # Extra documents for the plan
├── other/                      # Other documents/plans
│   └── [misc_doc].md
├── worklogs/                   # Task logging
│   ├── working/
│   │   └── [TICKET_ID].md      # Active task log
│   └── completed/
│       └── [TICKET_ID].md      # Archived task logs
├── details/                    # Specialized implementation details
│   └── [TOPIC_NAME].md         # e.g., STRIPE_INTEGRATION.md
└── agents/                     # Workflow specific documentation
    └── [WORKFLOW_NAME]/
        └── [workflow_doc].md
```
