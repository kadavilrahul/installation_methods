
# Installation and Usage Guide for Rovo Dev CLI

---

## Overview

Rovo Dev CLI is an AI-powered command line tool integrated with Atlassian apps to streamline software development tasks such as code generation, review, debugging, documentation, and Jira/Confluence management — all from your terminal.

---

## Prerequisites

- Linux OS (Debian-based or Red Hat-based)
- Atlassian account with API token (unscoped)
- Terminal access with sudo privileges (for system-wide install)

---

## Step 1: Install Atlassian Command Line Interface (ACLI)

Rovo Dev CLI is an extension of ACLI. You must install or update ACLI first.

### For Debian-based distributions (Ubuntu, Debian)

1. Install dependencies:

```bash
sudo apt-get install -y wget gnupg2
```

2. Setup APT repository and keyring:

```bash
sudo mkdir -p -m 755 /etc/apt/keyrings
```
```bash
wget -nv -O- https://acli.atlassian.com/gpg/public-key.asc | sudo gpg --dearmor -o /etc/apt/keyrings/acli-archive-keyring.gpg
```
```bash
sudo chmod go+r /etc/apt/keyrings/acli-archive-keyring.gpg
```
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/acli-archive-keyring.gpg] https://acli.atlassian.com/linux/deb stable main" | sudo tee /etc/apt/sources.list.d/acli.list > /dev/null
```

3. Update and install ACLI:

```bash
sudo apt update
```
```bash
sudo apt install -y acli
```

---

### For Red Hat-based distributions (CentOS, Fedora, RHEL)

1. Install dependencies:

```bash
sudo yum install -y yum-utils
```

2. Setup YUM repository:

```bash
sudo yum-config-manager --add-repo https://acli.atlassian.com/linux/rpm/acli.repo
```

3. Install ACLI:

```bash
sudo yum install -y acli
```

---

### Alternative: Install ACLI binary with curl (Linux)

1. Download the latest release for your architecture:

- For ARM64:

```bash
curl -LO "https://acli.atlassian.com/linux/latest/acli_linux_arm64/acli"
```

- For x86-64:

```bash
curl -LO "https://acli.atlassian.com/linux/latest/acli_linux_amd64/acli"
```

2. Make the binary executable:

```bash
chmod +x ./acli

```

3. (Optional) Install globally with root access:

```bash
sudo install -o root -g root -m 0755 acli /usr/local/bin/acli
```

4. (Optional) Install locally without root:

```bash
mkdir -p ~/.local/bin
mv ./acli ~/.local/bin/acli
# Add ~/.local/bin to your PATH if not already included
export PATH=$PATH:~/.local/bin
```

5. Verify installation:

```bash
acli --help
```

---

## Step 2: Create Atlassian API Token

1. Go to your Atlassian profile API tokens page:  
   https://id.atlassian.com/manage-profile/security/api-tokens

2. Create a new **unscoped** API token.

---

## Step 3: Authenticate Rovo Dev CLI

Run the following command to login and authorize with your Atlassian account:

```bash
acli rovodev auth login
```

Follow the prompts to enter your API token.

---

## Step 4: Run Rovo Dev CLI

Start Rovo Dev in interactive mode:

```bash
acli rovodev run
```

You can now use natural language commands to interact with your codebase and Atlassian apps.

---

## Useful Commands in Interactive Mode

- 
`/sessions` — Switch or view session details
- `/clear` — Clear current session history
- `/prune` — Reduce token size while retaining context
- `/instructions` — Run saved instructions/tasks
- `/memory` — Manage memory files for custom instructions
- `/feedback` — Report bugs or provide feedback
- `/usage` — Show daily token usage
- `/exit` — Quit Rovo Dev CLI

---

## Non-Interactive Mode

Run commands directly without interaction, e.g.:

```bash
acli rovodev run "Create unit tests for all components without tests"
```

---

## Additional Tips

- Start with small tasks (10-20 lines of code)
- Break down large tasks into smaller steps
- Use memory files (`~/.agent.md`, `.agent.local.md`, `.agent.md`) to store common instructions
- Regularly update ACLI to get latest features and fixes
- Review and iterate on generated code like collaborating with a teammate

---

## References

- Official Rovo Dev CLI docs:
  ```
  https://rovodevagents-beta.atlassian.net/wiki/external/Yzc2NzI4MTk3YTBhNDdiYjkzZDhhZTc3MjE0ZmE4Y2Q#Install-Rovo-Dev-CLI
  ```
- Atlassian ACLI Linux install guide:
  ```
  https://developer.atlassian.com/cloud/acli/guides/install-linux/
  ```
  
- Rovo Dev CLI API page:
  ``` 
  https://id.atlassian.com/manage-profile/security/api-tokens
  ```
  
- Rovo Dev CLI run page:
  ``` 
  https://nilgiri-stores.atlassian.net/dev-agents/rovo-dev-cli
  ```

---




