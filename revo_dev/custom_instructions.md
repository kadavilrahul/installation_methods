# Rovo Dev Custom Instructions Guide

A simple guide to creating and using custom instructions in Rovo Dev.

## Table of Contents

- [Overview](#overview)
- [Quick Start](#quick-start)
- [Configuration Methods](#configuration-methods)
- [Simple Instructions Examples](#simple-instructions-examples)
- [Using Instructions](#using-instructions)
- [Best Practices](#best-practices)

## Overview

Custom instructions in Rovo Dev help you:
- Set consistent coding standards
- Create reusable prompts for common tasks
- Automate development workflows
- Ensure team consistency

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
    - Prioritize code readability and maintainability
    - Implement proper logging and monitoring
    - Use design patterns appropriately
    - Ensure security best practices
    - Optimize for performance when necessary
    - Follow language-specific conventions
    - Create comprehensive documentation
    - Write self-documenting code with meaningful names
```

### Method 2: Instruction Templates (Recommended)

1. Create `.rovodev/instructions.yml` in your project root directory:
```yaml
instructions:
  # Code Quality & Review
  - name: code-review
    description: Perform comprehensive code review
    content_file: code_review.md
  - name: refactor
    description: Refactor code for better maintainability
    content_file: refactor.md
  - name: optimize
    description: Optimize code performance
    content_file: optimize.md
  - name: minimal-code
    description: Use minimum lines of code to write a function
    content_file: minimal_code.md
  
   # Build & Automation
  - name: build-script
    description: Build shellscript file run.sh to run all commands
    content_file: build_script.md
  
  # Documentation
  - name: readme
    description: Create or update project README
    content_file: readme.md
  - name: comments
    description: Add meaningful code comments
    content_file: comments.md
```

2. Create instruction files in the same directory

## Configuration Methods

### File Locations (in order of priority)
1. Project root: `{project}/.rovodev/instructions.yml`
2. Current directory: `./.rovodev/instructions.yml`
3. User home: `~/.rovodev/instructions.yml`

### Basic Config Structure
```yaml
instructions:
  - name: unique-name
    description: What this instruction does
    content_file: filename.md
```

## Simple Instructions Examples

### Code Review (`code_review.md`)
```markdown
# Code Review Checklist

Review the code for:

## Quality
- Clean, readable code
- Meaningful variable names
- Functions under 20 lines
- No code duplication

## Testing
- Unit tests included
- Test coverage > 80%
- Edge cases covered

## Documentation
- Clear comments for complex logic
- Function documentation
- README updated if needed

## Security
- Input validation
- No hardcoded secrets
- Proper error handling
```

### API Design (`api_design.md`)
```markdown
# API Design Guidelines

Design RESTful APIs following these principles:

## Endpoints
- Use nouns for resources: `/users`, `/orders`
- Use HTTP methods correctly: GET, POST, PUT, DELETE
- Include version in URL: `/api/v1/users`

## Response Format
```json
{
  "success": true,
  "data": {},
  "message": "Operation successful"
}
```

## Error Handling
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input"
  }
}
```

## Requirements
- Input validation
- Proper HTTP status codes
- Authentication/authorization
- Comprehensive documentation
```

### Build Script Template
```markdown
# Build Script Creation

Create a `run.sh` script:

```bash
#!/bin/bash
set -e

case "$1" in
  install)
    echo "Installing dependencies..."
    ;;
  build)
    echo "Building project..."
    ;;
  test)
    echo "Running tests..."
    ;;
  dev)
    echo "Starting development server..."
    ;;
  *)
    echo "Usage: ./run.sh {install|build|test|dev}"
    exit 1
    ;;
esac
```

Make executable: `chmod +x run.sh`
```

## Using Instructions

### Command Line
```bash
# List available instructions
rovodev /instructions

# Use specific instruction
rovodev /instructions code-review

# Use with additional context
rovodev /instructions api-design "for user management"
```

### In Rovo Dev Interface
1. Type `/instructions`
2. Select from the menu
3. Add any additional context

## Best Practices

### 1. Keep Instructions Simple
- One clear purpose per instruction
- Short, actionable content
- Include examples

### 2. Use Clear Names
- `code-review` ✅ (clear)
- `cr` ❌ (unclear)

### 3. Include Examples
Always show what good output looks like in your instruction files.

### 4. Version Control
```bash
# Add to git
git add .rovodev/
git commit -m "Add custom instructions"
```

## Quick Setup

Create the basic structure:

```bash
mkdir -p .rovodev
cd .rovodev

# Create instructions.yml
cat > instructions.yml << 'EOF'
instructions:
  - name: code-review
    description: Perform comprehensive code review
    content_file: code_review.md
  - name: api-design
    description: Design RESTful API endpoints
    content_file: api_design.md
EOF

# Create instruction files
echo "# Code Review" > code_review.md
echo "Review code for quality, testing, and documentation." >> code_review.md

echo "# API Design" > api_design.md
echo "Design RESTful APIs with proper endpoints and error handling." >> api_design.md
```

---

*Keep it simple, keep it useful!*
