# Project Brief

## Key requirements

This project aims to create a PR Documentation Generator that automatically analyzes Pull Requests and generates comprehensive documentation about the changes made. The system follows a sequential workflow to:

1. Retrieve PR information using GitHub CLI
2. Analyze files before and after changes
3. Store information in a graph database using Neo4j
4. Process all modified files with context management
5. Generate a graph representation of the PR changes
6. Query the graph for insights
7. Generate comprehensive documentation with categorized changes

The PR Documentation Generator must:

- Handle potentially large PRs with many files
- Categorize changes into business logic, configuration, services, dependencies, schemas, infrastructure, and CI/CD pipeline changes
- Generate structured documentation following a standardized format
- Provide insights into the impact of changes
- Be robust to context size limitations
- Follow a standardized Neo4j schema for entity and relation types
