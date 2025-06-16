# Rovo Dev Custom Instructions Guide

A comprehensive guide to creating, managing, and using custom instructions in Rovo Dev to enhance your development workflow.

## Table of Contents

- [Overview](#overview)
- [Quick Start](#quick-start)
- [Configuration Methods](#configuration-methods)
- [Creating Instruction Templates](#creating-instruction-templates)
- [Advanced Features](#advanced-features)
- [Best Practices](#best-practices)
- [Examples](#examples)
- [Troubleshooting](#troubleshooting)

## Overview

Custom instructions in Rovo Dev allow you to:
- Define consistent coding standards and practices
- Create reusable prompt templates for common tasks
- Establish project-specific guidelines
- Automate repetitive development workflows
- Ensure team consistency across projects

## Quick Start

### Method 1: Global System Prompt (Simplest)

Edit your `.rovodev/config.yml` file:

```yaml
agent:
  additionalSystemPrompt: |
    You are a senior software engineer. Always:
    - Write clean, maintainable code
    - Include comprehensive error handling
    - Add meaningful comments and documentation
    - Follow SOLID principles
    - Write unit tests for new functionality
    - Use minimum lines of code to write a function
    - Build shellscript file run.sh to run all commands
```

### Method 2: Instruction Templates (Recommended)

1. Create `.rovodev/instructions.yml`:
```yaml
instructions:
  - name: code-review
    description: Perform comprehensive code review
    content_file: code_review.md
  - name: api-design
    description: Design RESTful API endpoints
    content_file: api_design.md
```

2. Create instruction files (e.g., `code_review.md`):
```markdown
# Code Review Instructions

Please review the code with focus on:

## Security
- Check for SQL injection vulnerabilities
- Validate input sanitization
- Review authentication/authorization

## Performance
- Identify potential bottlenecks
- Check for N+1 queries
- Review caching strategies

## Code Quality
- Ensure SOLID principles
- Check for code duplication
- Verify error handling
```

## Configuration Methods

### 1. Global System Prompt

**Location**: `.rovodev/config.yml`

```yaml
agent:
  additionalSystemPrompt: "Your global instructions here"
  temperature: 0.1  # Lower = more consistent, Higher = more creative
  streaming: true
```

**Use Case**: Instructions that apply to every interaction

### 2. Instruction Templates

**Location**: `.rovodev/instructions.yml`

```yaml
instructions:
  - name: instruction-name
    description: Human-readable description
    content_file: instruction_file.md
```

**Use Case**: Reusable, specific task instructions

## Creating Instruction Templates

### File Structure
```
.rovodev/
├── config.yml
├── instructions.yml
└── instructions/
    ├── code_review.md
    ├── api_design.md
    ├── testing.md
    └── documentation.md
```

### Configuration Precedence
Instructions are loaded in this order (first found wins):
1. Repository root: `{repo_root}/.rovodev/instructions.yml`
2. Current directory: `./.rovodev/instructions.yml`
3. User home: `~/.rovodev/instructions.yml`

### Instruction File Format

```yaml
instructions:
  - name: unique-identifier
    description: Brief description shown in menu
    content_file: relative/path/to/instruction.md
```

### Content File Structure

```markdown
# Instruction Title

Brief overview of what this instruction accomplishes.

## Context
Provide any necessary background information.

## Requirements
- Specific requirement 1
- Specific requirement 2

## Guidelines
Detailed instructions for the AI to follow.

## Examples
Show examples of expected output or behavior.
```

## Advanced Features

### Dynamic Content with Variables

```markdown
# API Endpoint Design

Create a RESTful API endpoint for: {RESOURCE_NAME}

## Requirements
- Follow REST conventions
- Include proper HTTP status codes
- Add input validation
- Implement error handling

Additional context: {ADDITIONAL_CONTEXT}
```

### Conditional Instructions

```markdown
# Testing Instructions

Based on the project type:

**For React Projects:**
- Use Jest and React Testing Library
- Test component rendering and interactions
- Mock external dependencies

**For Node.js Projects:**
- Use Jest or Mocha
- Test API endpoints
- Mock database calls

**For Python Projects:**
- Use pytest
- Test functions and classes
- Use fixtures for test data
```

### Multi-Step Workflows

```markdown
# Feature Development Workflow

Follow these steps in order:

## Step 1: Planning
- Analyze requirements
- Create technical design
- Identify dependencies

## Step 2: Implementation
- Write failing tests first (TDD)
- Implement core functionality
- Add error handling

## Step 3: Review
- Self-review code
- Check test coverage
- Update documentation

## Step 4: Integration
- Test with existing features
- Verify performance impact
- Update API documentation
```

## Best Practices

### 1. Instruction Organization

```yaml
instructions:
  # Development workflow
  - name: feature-development
    description: Complete feature development workflow
    content_file: workflows/feature_development.md
  
  # Code quality
  - name: code-review
    description: Comprehensive code review checklist
    content_file: quality/code_review.md
  
  # Documentation
  - name: api-docs
    description: Generate API documentation
    content_file: docs/api_documentation.md
```

### 2. Clear and Specific Instructions

❌ **Vague:**
```markdown
Make the code better
```

✅ **Specific:**
```markdown
Refactor this code to:
- Extract reusable functions
- Add type annotations
- Improve error handling
- Add unit tests with 80%+ coverage
```

### 3. Include Context and Examples

```markdown
# Database Migration Instructions

## Context
We're migrating from MySQL to PostgreSQL while maintaining data integrity.

## Requirements
- Preserve all existing data
- Maintain referential integrity
- Update connection strings
- Test migration with sample data

## Example Migration Script
```sql
-- Example of data type conversion
ALTER TABLE users 
ALTER COLUMN created_at TYPE TIMESTAMP WITH TIME ZONE;
```

### 4. Version Control Instructions

```gitignore
# .gitignore additions for Rovo Dev
.rovodev/sessions/
.rovodev/*.log
```

Commit instruction files:
```bash
git add .rovodev/instructions.yml
git add .rovodev/instructions/
git commit -m "Add custom Rovo Dev instructions"
```

## Examples

### Example 1: React Component Development

```yaml
# instructions.yml
instructions:
  - name: react-component
    description: Create React component with best practices
    content_file: react_component.md
```

```markdown
# React Component Development

Create a React component following these guidelines:

## Structure
- Use functional components with hooks
- Implement TypeScript interfaces for props
- Add proper prop validation
- Include default props where appropriate

## Styling
- Use CSS modules or styled-components
- Follow BEM naming convention
- Ensure responsive design
- Add hover and focus states

## Testing
- Write unit tests with React Testing Library
- Test component rendering
- Test user interactions
- Mock external dependencies

## Accessibility
- Add proper ARIA labels
- Ensure keyboard navigation
- Test with screen readers
- Maintain color contrast ratios

## Example Structure
```tsx
interface ComponentProps {
  title: string;
  onClick?: () => void;
}

export const MyComponent: React.FC<ComponentProps> = ({ 
  title, 
  onClick 
}) => {
  // Component implementation
};
```

### Example 2: API Development

```yaml
instructions:
  - name: api-endpoint
    description: Design and implement REST API endpoint
    content_file: api_endpoint.md
```

```markdown
# API Endpoint Development

## Design Principles
- Follow RESTful conventions
- Use appropriate HTTP methods
- Implement proper status codes
- Add comprehensive error handling

## Implementation Checklist
- [ ] Input validation and sanitization
- [ ] Authentication/authorization
- [ ] Rate limiting
- [ ] Logging and monitoring
- [ ] API documentation
- [ ] Unit and integration tests

## Response Format
```json
{
  "success": true,
  "data": {},
  "message": "Operation completed successfully",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Error Handling
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input parameters",
    "details": []
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Example 3: Database Schema Design

```yaml
instructions:
  - name: database-schema
    description: Design database schema with best practices
    content_file: database_schema.md
```

```markdown
# Database Schema Design

## Naming Conventions
- Use snake_case for table and column names
- Use singular nouns for table names
- Add descriptive prefixes for related tables

## Design Principles
- Normalize to 3NF minimum
- Add appropriate indexes
- Use foreign key constraints
- Include audit fields (created_at, updated_at)

## Required Fields
```sql
-- Standard audit fields for all tables
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
created_by INT REFERENCES users(id),
updated_by INT REFERENCES users(id)
```

## Performance Considerations
- Add indexes on frequently queried columns
- Consider partitioning for large tables
- Use appropriate data types
- Avoid nullable foreign keys
```

## Troubleshooting

### Common Issues

#### 1. Instructions Not Loading
**Problem**: Custom instructions don't appear in the menu

**Solutions**:
- Check YAML syntax in `instructions.yml`
- Verify file paths are correct
- Ensure instruction content files exist
- Check file permissions

#### 2. Content File Not Found
**Problem**: Error loading instruction content

**Solutions**:
- Verify `content_file` path in `instructions.yml`
- Check file exists relative to config location
- Use absolute paths if needed

#### 3. Instructions Not Applied
**Problem**: Global instructions seem ignored

**Solutions**:
- Verify `additionalSystemPrompt` in `config.yml`
- Check YAML indentation
- Restart Rovo Dev session

### Debugging Commands

```bash
# Check config file syntax
cat .rovodev/config.yml | python -c "import yaml, sys; yaml.safe_load(sys.stdin)"

# Verify instruction files exist
find .rovodev -name "*.md" -type f

# Check file permissions
ls -la .rovodev/
```

### Validation Checklist

- [ ] YAML files have correct syntax
- [ ] All referenced content files exist
- [ ] File paths are correct (relative to config file)
- [ ] Instructions have unique names
- [ ] Content files are readable
- [ ] Configuration follows precedence rules

## Configuration Reference

### Complete config.yml Example

```yaml
version: 1

agent:
  additionalSystemPrompt: |
    You are an expert software engineer focused on:
    - Writing clean, maintainable code
    - Following established patterns and conventions
    - Comprehensive testing and documentation
    - Security best practices
  streaming: true
  temperature: 0.1
  experimental:
    enableShadowMode: false

sessions:
  autoRestore: false
  persistenceDir: /root/.rovodev/sessions

console:
  outputFormat: markdown
  showToolResults: true

logging:
  path: /root/.rovodev/rovodev.log

mcp:
  mcpConfigPath: /root/.rovodev/mcp.json

toolPermissions:
  allowAll: true
  default: ask
  tools:
    create_file: ask
    delete_file: ask
    find_and_replace_code: ask
    open_files: allow
    expand_code_chunks: allow
    grep_file_content: allow
```

### Complete instructions.yml Example

```yaml
instructions:
  # Development Workflows
  - name: feature-development
    description: Complete feature development workflow
    content_file: workflows/feature_development.md
  
  - name: bug-fix
    description: Systematic bug fixing approach
    content_file: workflows/bug_fix.md
  
  # Code Quality
  - name: code-review
    description: Comprehensive code review
    content_file: quality/code_review.md
  
  - name: refactoring
    description: Safe refactoring guidelines
    content_file: quality/refactoring.md
  
  # Testing
  - name: unit-testing
    description: Write comprehensive unit tests
    content_file: testing/unit_tests.md
  
  - name: integration-testing
    description: Create integration test suite
    content_file: testing/integration_tests.md
  
  # Documentation
  - name: api-documentation
    description: Generate API documentation
    content_file: docs/api_docs.md
  
  - name: readme-update
    description: Update project README
    content_file: docs/readme.md
  
  # Architecture
  - name: system-design
    description: Design system architecture
    content_file: architecture/system_design.md
  
  - name: database-design
    description: Design database schema
    content_file: architecture/database_design.md
```

---

## Contributing

To contribute to this guide or share your custom instructions:

1. Fork the repository
2. Add your instruction examples
3. Update documentation
4. Submit a pull request

## License

This guide is provided under the same license as Rovo Dev.

---

*Last updated: 2024*
