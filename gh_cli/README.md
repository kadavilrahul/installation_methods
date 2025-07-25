# GitHub CLI (gh) Installation Guide

## Installation on Ubuntu/Debian

### Method 1: Using apt package manager (Recommended)

```bash
sudo apt update
sudo apt install gh
```

### Method 2: Using GitHub's official repository

```bash
# Add GitHub's GPG key
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg

# Add the repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# Update and install
sudo apt update
sudo apt install gh
```

## Authentication

After installation, authenticate with GitHub:

```bash
gh auth login
```

### Authentication Options:

1. **Protocol**: Choose HTTPS (recommended for most users)
2. **Git credentials**: Yes (to authenticate Git with GitHub credentials)
3. **Authentication method**: 
   - **Web browser** (if GUI available)
   - **Personal access token** (for headless systems)

### For Headless Systems (No GUI):

If you encounter browser opening issues like:
```
xdg-open: no method available for opening 'https://github.com/login/device'
```

You can:
1. Copy the one-time code provided
2. Manually open https://github.com/login/device in a browser on another device
3. Enter the code to complete authentication

Or use a personal access token:
```bash
gh auth login --with-token < token.txt
```

## Verification

Verify installation and authentication:

```bash
# Check version
gh --version

# Check authentication status
gh auth status

# Test with a simple command
gh repo list
```

## Common Commands

```bash
# List all repositories
gh repo list

# List all repositories with more details
gh repo list --limit 100

# List repositories sorted by last updated (most recent first)
gh repo list --sort updated

# Get the most recently updated repository
gh repo list --limit 1 --sort updated

# Clone a repository
gh repo clone owner/repo

# Create a new repository
gh repo create my-new-repo

# View issues
gh issue list

# Create a pull request
gh pr create

# View pull requests
gh pr list
```

## Troubleshooting

### Package Dependencies
If you see warnings about unused packages:
```bash
sudo apt autoremove
```

### Authentication Issues
- Ensure you have a stable internet connection
- Check if your GitHub account has proper permissions
- For organizations, ensure you have the necessary access rights

## Additional Resources

- [Official GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub CLI Repository](https://github.com/cli/cli)