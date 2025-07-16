# Gemini CLI Installation Guide

## Prerequisites
- Linux server with curl installed
- Existing Node.js installation (will be upgraded if needed)

## Installation Steps

### 1. Install Node Version Manager (nvm)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
```

### 2. Install Node.js v20+
```bash
nvm install 20
nvm use 20
```

### 3. Install Gemini CLI globally
```bash
npm install -g @google/gemini-cli
```

### 4. Verify Installation
```bash
gemini --version
# Should output version number (e.g. 0.1.12)
```

## Authentication Options

### Option A: Google Account Login
Simply run:
```bash
gemini
```
And follow the authentication prompts

### Option B: API Key
1. Generate a key from [Google AI Studio](https://aistudio.google.com)
2. Set environment variable:
```bash
export GEMINI_API_KEY="your-api-key-here"
```

## Troubleshooting
- If you get "command not found" after installation, try reopening your terminal
- For Node.js version issues, ensure you're using v20+ with `node --version`
