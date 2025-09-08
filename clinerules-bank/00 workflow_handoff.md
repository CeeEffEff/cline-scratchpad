# You MUST use the `new_task` tool: Workflow Handoff Strategy Guide

**⚠️ CRITICAL INSTRUCTIONS - YOU MUST FOLLOW THESE GUIDELINES ⚠️**

This guide provides **MANDATORY** instructions for implementing a smooth handoff process of a workflow that is partially complete. You **MUST** follow these guidelines to ensure continuity, context preservation, and efficient workflow completion.

## ⚠️ CONTEXT WINDOW MONITORING - MANDATORY ACTION REQUIRED ⚠️

You **MUST** monitor the context window usage displayed in the environment details. When usage exceeds 50% of the available context window, you **MUST** initiate a workflow handoff using the `new_task` tool.

### Continuing a Worfklow with Context - REQUIRED ACTION

If the user agrees to create a new task, you **MUST** use the `new_task` tool with comprehensive handoff instructions:

\`\`\`xml
<new_task>
<context>

# Task for Workflow Continuation: [Brief Task Title]

## Workflow Metadata - REQUIRED

-   [identifer for the workflow that needs to be resumed]
-   [provide checklist of completed items, with nesting for any subitems]
-   [provide checklist of remaing items, with nesting for any subitems]

## Completed Work

-   [Detailed list of completed items]
-   [Include specific files modified/created]
-   [Note any important decisions made]

## Current State

-   [Description of the current state of the project]
-   [Any running processes or environment setup]
-   [Key files and their current state]

## Next Steps

-   [Detailed list of remaining tasks]
-   [Specific implementation details to address]
-   [Any known challenges to be aware of]
-   [Guidance on where in the workflow to resume at, incuding things not to do]

## Reference Information

-   [Links to relevant documentation]
-   [Important code snippets or patterns to follow]
-   [Any user preferences noted during the current session]

Please resume the worflow at the next action: [specific next action].
</context>
</new_task>
\`\`\`
