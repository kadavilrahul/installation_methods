# Claude Code Installation Guide for Ubuntu

This guide provides step-by-step instructions for installing and configuring Claude Code on Ubuntu systems.

## Prerequisites

Before installing Claude Code, ensure you have Node.js version 18 or greater installed on your system.

## Installation Steps

### 1. Check System Requirements

First, verify that Node.js and npm are installed and meet the version requirements:

```bash
# Check Node.js version (should be 18 or greater)
node -v

# Check npm version
npm -v
```

If Node.js is not installed or the version is below 18, install it:

```bash
sudo apt update
sudo apt install nodejs npm
```

### 2. Install Claude Code Globally

Install Claude Code using npm:

```bash
npm install -g @anthropic-ai/claude-code
```

**Important:** Avoid using `sudo` with this command as it can cause permission issues.

### 3. Verify Installation

Check if Claude Code was installed successfully:

```bash
npm list -g @anthropic-ai/claude-code
```

This should show the installed version (e.g., `@anthropic-ai/claude-code@1.0.25`).

### 4. Fix PATH Issues (Common Problem)

If you get "claude: command not found" error, the npm global bin directory is not in your PATH. Here's how to fix it:

#### Check npm global prefix:
```bash
npm config get prefix
```

#### Find the claude binary:
```bash
# Replace the path below with your npm prefix from the previous command
ls -la /tmp/node-v20.11.0-linux-x64/bin/claude
```

#### Create a permanent symbolic link:
```bash
# Create a symlink in a directory that's already in PATH
sudo ln -sf /tmp/node-v20.11.0-linux-x64/bin/claude /usr/local/bin/claude
```

**Note:** Replace `/tmp/node-v20.11.0-linux-x64/bin/claude` with the actual path from your npm prefix.

### 5. Verify Claude Code Works

Test that Claude Code is now accessible:

```bash
# Check version
claude --version

# View help
claude --help
```

You should see output like:
```
1.0.25 (Claude Code)
```

## Usage

### Basic Commands

```bash
# Start interactive session
claude

# Non-interactive mode (print and exit)
claude --print "Your prompt here"

# Continue previous conversation
claude --continue

# Resume a specific conversation
claude --resume

# View configuration options
claude config

# Check system health
claude doctor
```

### Authentication

When you first run Claude Code, you'll need to authenticate:

1. Run `claude` to start the interactive session
2. Follow the on-screen instructions to authenticate through the Anthropic Console
3. Complete the OAuth process
4. Ensure you have a Claude Pro or Max plan for unified access

## Troubleshooting

### Command Not Found Error

If you still get "claude: command not found" after installation:

1. **Check if the binary exists:**
   ```bash
   find /tmp -name "claude" -type f 2>/dev/null
   ```

2. **Verify the symbolic link:**
   ```bash
   ls -la /usr/local/bin/claude
   ```

3. **Check your PATH:**
   ```bash
   echo $PATH | grep -o "/usr/local/bin"
   ```

### Permission Issues

If you encounter permission errors during installation:

1. **Don't use sudo with npm install**
2. **Fix npm permissions** (if needed):
   ```bash
   mkdir ~/.npm-global
   npm config set prefix '~/.npm-global'
   echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

### Alternative PATH Method

If the symbolic link approach doesn't work, you can add the npm bin directory to your PATH:

```bash
# Add to ~/.bashrc
echo 'export PATH="/tmp/node-v20.11.0-linux-x64/bin:$PATH"' >> ~/.bashrc

# Reload bashrc
source ~/.bashrc
```

## System Information

This installation was tested on:
- **OS:** Linux 6.8 (Ubuntu)
- **Shell:** /bin/bash
- **Node.js:** v20.11.0
- **npm:** v10.2.4
- **Claude Code:** v1.0.25

## Additional Resources

- [Anthropic Documentation](https://docs.anthropic.com/)
- [Claude Code GitHub Repository](https://github.com/anthropics/claude-code)
- [Node.js Installation Guide](https://nodejs.org/en/download/package-manager/)

## Summary

The key steps for a successful installation are:

1. ✅ Install Node.js 18+ and npm
2. ✅ Install Claude Code globally with npm
3. ✅ Create symbolic link to fix PATH issues
4. ✅ Verify installation with `claude --version`
5. ✅ Authenticate on first use

After following these steps, you should be able to run `claude` from any directory without additional configuration.
