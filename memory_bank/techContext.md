# Tech Context

## Technology Stack
- **Markdown**: Used for workflow file format
- **Bash/Shell**: Used for command execution in workflow steps
- **GitHub CLI**: Used for retrieving PR information
- **Neo4j**: Graph database used for representing PR changes and relationships
- **MCP Tools**: Used for interacting with the Neo4j memory server
- **jq**: Used for parsing JSON responses from GitHub CLI

## Key Integrations
- **GitHub CLI Integration**: The workflow uses the `gh` command to interact with GitHub and retrieve PR information
- **Neo4j Memory Server Integration**: The workflow uses MCP tools to store and query information in a Neo4j graph database following a standardized schema
- **Taskmaster Integration**: The project uses Taskmaster for task management and tracking

## Development Environment
- **Directory Structure**:
  - `.clinerules/workflows/`: Contains workflow files
  - `.taskmaster/`: Contains Taskmaster configuration and task files
  - `memory_bank/`: Contains memory bank files for the assistant

## Tools and Libraries
- **GitHub CLI (`gh`)**: Command-line tool for interacting with GitHub
- **Neo4j Memory Server**: MCP server for storing and querying graph data
- **Taskmaster**: Tool for task management and tracking
- **MCP Tools**: Model Context Protocol tools for interacting with external services
- **jq**: Command-line JSON processor for parsing GitHub CLI responses
