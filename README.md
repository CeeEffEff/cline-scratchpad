# PR Documentation Generator

## Project Overview

Automate the creation of comprehensive documentation for Pull Requests (PRs) to improve knowledge transfer, code review efficiency, and historical record-keeping. This tool analyzes PR changes, categorizes them by impact, and generates structured documentation using a graph-based approach.

## Key Components

1. **Workflow Architecture**:
   - Sequential process: PR Information Retrieval → File Analysis → Graph Representation → Documentation Generation
   - Tools: GitHub CLI, Neo4j (graph database), MCP tools, `jq` for JSON parsing

2. **Graph-Based Representation**:
   - PR changes modeled as a graph with nodes (files, changes, PRs) and relationships
   - Standardized Neo4j schema with entity types (`File`, `Change`, `PR`) and relations (`MODIFIED_BY`, `DEPENDS_ON`)

3. **Context Management**:
   - Explicit handling of large PRs with many files to avoid context size limits
   - Continuation tasks created when context approaches limits

4. **File Analysis**:
   - Categorizes changes into: business logic, configuration, services, dependencies, schemas, infrastructure, CI/CD pipelines
   - Focuses on purpose, behavior, and system impact rather than superficial metrics

5. **Documentation Generation**:
   - Structured markdown output following a standardized format
   - Includes insights into change impacts and categorization

## Technology Stack

- **Workflow Format**: Markdown (`.clinerules/workflows/`)
- **Integrated Command Execution**: Bash/Shell/XML markdown snippits
- **GitHub Integration**: GitHub CLI (`gh`) for PR metadata
- **Graph Database**: Neo4j (via MCP tools) for relationship tracking
- **Utilities**: `jq` for JSON parsing

## How It Works

1. **PR Information Retrieval**: Uses GitHub CLI to fetch PR metadata and modified files
2. **File Analysis**: Examines changes to categorize impact (business logic, infrastructure, etc.)
3. **Graph Representation**: Stores relationships in Neo4j using standardized schema
4. **Documentation Generation**: Creates structured markdown with categorized insights

## Contributing

1. Review the workflow structure in `.clinerules/workflows/pr-documentation-generator.md`
2. Extend testing coverage for edge cases
3. Enhance error handling for GitHub CLI interactions
4. Document usage patterns for different PR types

This project demonstrates how graph databases can provide semantic insights into code changes, bridging the gap between technical implementation and team understanding.
