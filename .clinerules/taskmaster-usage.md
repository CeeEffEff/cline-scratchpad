---
description: Guidelines for using Taskmaster in this specific environment
globs: **/*
alwaysApply: true
---

## Brief overview
This rule file provides specific instructions for using Taskmaster in this environment, including the correct command path and known limitations.

## Command line usage
- Always use the full path when executing Taskmaster commands: `/Users/conor.fehilly/Documents/repos/claude-task-master/bin/task-master.js <command>`
- Do not use the shorthand `task-master <command>` as it won't work in this environment

## PRD parsing
- When parsing a PRD, always use the command line version of Taskmaster
- Do not use the MCP tool for PRD parsing due to known issues
- Example correct usage: `/Users/conor.fehilly/Documents/repos/claude-task-master/bin/task-master.js parse-prd <file> [options]`

## Tool selection
- For most Taskmaster operations, use the MCP tools when available
- For PRD parsing specifically, always use the command line interface, never the MCP tool
- For other operations where both CLI and MCP tools are available, prefer the MCP tools unless instructed otherwise
