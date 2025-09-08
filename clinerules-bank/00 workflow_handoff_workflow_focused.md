# Workflow Continuation Strategy Guide

**⚠️ CRITICAL INSTRUCTIONS - YOU MUST FOLLOW THESE GUIDELINES ⚠️**

This guide provides **MANDATORY** instructions for implementing a smooth handoff process of a workflow that is partially complete. You **MUST** follow these guidelines to ensure continuity, context preservation, and efficient workflow completion.

## Continuing a Worfklow with Context - REQUIRED ACTION

When creating a task for continuing the current workflow, you **MUST** use the `new_task` tool with Comprehensive Workflow Continuation Instructions:

\`\`\`xml
<new_task>
<context>

# Task for Workflow Continuation: [Brief Task Title]

## Workflow Metadata

-   [the name of the workflow file]
-   [arguments the workflow was called with]

## Workflow TO-DO list
-   [provide the updated TO-DO list]

## Completed Work

-   [Detailed list of completed items]
-   [Include specific files modified/created]
-   [Note any important decisions made]

## Current State

-   [Description of the current state of the workflow]
-   [Key files and their current state]

## Next Steps

-   [Detailed list of remaining workflow steps]
-   [Any known challenges to be aware of]
-   [Guidance on how to resume the worfklow given its current state]

## Reference Information

-   [Links to relevant documentation]
-   [Important code snippets or patterns to follow]
-   [Any user preferences noted during the current session]

Please resume the workflow at the next step: [specific next step of the workflow].
[slash command calling workflow with original arguments]
</context>
</new_task>
\`\`\`
