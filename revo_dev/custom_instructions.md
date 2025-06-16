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
    - Use MCP fetch tools to search the internet for current solutions, documentation, and best practices when needed
    - Research latest libraries, frameworks, and tools using web search before implementing
    - Verify solutions against current online documentation and community resources
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
  
  # Internet Research & Solutions
  - name: research-solution
    description: Research solutions and best practices using MCP fetch
    content_file: research_solution.md
  - name: find-libraries
    description: Find and evaluate libraries/frameworks using web search
    content_file: find_libraries.md
  - name: verify-docs
    description: Verify implementation against current online documentation
    content_file: verify_docs.md
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

### Research Solution Template (`research_solution.md`)
```markdown
# Research Solution Using MCP Fetch

Use MCP fetch tools to research current solutions and best practices:

## Research Process
1. **Search for Solutions**: Use fetch_html or fetch_markdown to search documentation sites, Stack Overflow, GitHub
2. **Analyze Current Practices**: Look for recent implementations and community recommendations
3. **Compare Approaches**: Evaluate multiple solutions before implementing
4. **Verify Currency**: Ensure information is up-to-date and relevant

## Example Research Queries
- Official documentation for libraries/frameworks
- Stack Overflow discussions for specific problems
- GitHub repositories with similar implementations
- Blog posts and tutorials from reputable sources

## Implementation Steps
1. Research the problem domain thoroughly
2. Identify 2-3 potential solutions
3. Evaluate pros/cons of each approach
4. Choose the most appropriate solution
5. Implement with current best practices
6. Document the chosen approach and reasoning
```

### Find Libraries Template (`find_libraries.md`)
```markdown
# Find and Evaluate Libraries Using Web Search

Research and evaluate libraries/frameworks before implementation:

## Research Checklist
- **Official Documentation**: Fetch and review official docs
- **GitHub Repository**: Check stars, issues, recent commits
- **Community Support**: Look for Stack Overflow discussions
- **Compatibility**: Verify version compatibility
- **Performance**: Research benchmarks and performance comparisons
- **Security**: Check for known vulnerabilities
- **Maintenance**: Evaluate active development and support

## Evaluation Criteria
1. **Popularity**: GitHub stars, npm downloads, community size
2. **Maintenance**: Recent commits, issue response time
3. **Documentation**: Quality and completeness
4. **Performance**: Benchmarks and real-world usage
5. **Security**: Vulnerability reports and security practices
6. **License**: Compatibility with project requirements

## Implementation
- Always fetch latest documentation before implementing
- Include version pinning in dependencies
- Document why the library was chosen
```

### Verify Documentation Template (`verify_docs.md`)
```markdown
# Verify Implementation Against Current Documentation

Use MCP fetch to verify implementations against current online documentation:

## Verification Process
1. **Fetch Official Docs**: Get latest documentation from official sources
2. **Check API Changes**: Verify method signatures and parameters
3. **Review Examples**: Compare implementation with official examples
4. **Validate Best Practices**: Ensure following current recommendations
5. **Security Updates**: Check for security-related changes

## Sources to Check
- Official API documentation
- Framework/library changelog
- Security advisories
- Migration guides
- Community best practices

## Implementation Guidelines
- Always verify against official sources before implementing
- Check for deprecated methods or patterns
- Ensure security best practices are current
- Document any deviations from standard patterns
- Include links to referenced documentation
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
  - name: research-solution
    description: Research solutions and best practices using MCP fetch
    content_file: research_solution.md
  - name: find-libraries
    description: Find and evaluate libraries/frameworks using web search
    content_file: find_libraries.md
EOF

# Create instruction files
echo "# Code Review" > code_review.md
echo "Review code for quality, testing, and documentation." >> code_review.md

echo "# API Design" > api_design.md
echo "Design RESTful APIs with proper endpoints and error handling." >> api_design.md

echo "# Research Solution Using MCP Fetch" > research_solution.md
echo "Use MCP fetch tools to research current solutions and best practices." >> research_solution.md

echo "# Find and Evaluate Libraries" > find_libraries.md
echo "Research and evaluate libraries/frameworks before implementation using web search." >> find_libraries.md
```

---

*Keep it simple, keep it useful!*
