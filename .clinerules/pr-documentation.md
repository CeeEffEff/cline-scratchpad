---
description: Required structure for PR Documentation generations
globs: **/*
alwaysApply: true
---

# Documentation Structure

The generated PR documentation **must** be structured to include the following sections based on the insights extracted from the graph:

1. **PR Overview**
   - Title, description, author, dates
   - Type (fix, feature, refactor, etc.)
   - Intent analysis

2. **Files Modified**
   - List of modified files with categorization
   - File-level change statistics

3. **Business Logic Changes**
   - Description of business rules or algorithms modified
   - Purpose of changes and impact on functionality
   - Before/after comparison where relevant

4. **Configuration Changes**
   - Modified configuration parameters
   - Environment impacts
   - Default value changes

5. **Service Changes**
   - API modifications
   - Endpoint changes
   - Service behavior modifications

6. **Dependency Changes**
   - Added, removed, or updated dependencies
   - Version changes
   - Dependency impact analysis

7. **Schema Changes**
   - Data model modifications
   - Database schema updates
   - Type definition changes

8. **Infrastructure Changes**
   - Resource modifications
   - Deployment configuration updates
   - Environment setup changes

9. **CI/CD Pipeline Changes**
   - Build process modifications
   - Deployment step changes
   - Testing configuration updates

10. **Impact Analysis**
    - Direct impacts on other components
    - Potential wider impacts
    - Required follow-up changes

11. **Conceptual Changes**
    - Architectural pattern implementations or modifications
    - Design principle applications
    - Abstract concept implementations

