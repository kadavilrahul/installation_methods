# Installation Methods Repository

This repository contains comprehensive installation guides and setup instructions for various development tools and cloud platforms.

## 🚀 Quick Start

Clone this repository to get access to all installation guides:

```bash
git clone https://github.com/kadavilrahul/installation_methods.git
```
```bash
cd installation_methods
```

## 📁 Repository Structure

```
installation_methods/
├── claude_code/       # Claude Code CLI installation guide
├── cloudflare/        # Cloudflare CLI and DNS management
├── google_cloud/      # Google Cloud CLI setup
├── opencode/          # OpenCode AI CLI installation
└── revo_dev/          # Rovo Dev CLI for Atlassian integration
```

## 📚 Available Installation Guides

### 🤖 [Claude Code](./claude_code/)
- **Purpose**: Official CLI for Claude AI assistant
- **Platform**: Ubuntu/Linux
- **Key Features**: Interactive AI coding assistant, code generation, debugging
- **Prerequisites**: Node.js 18+

### ☁️ [Cloudflare](./cloudflare/)
- **Purpose**: DNS management and Cloudflare Workers
- **Platform**: Cross-platform
- **Key Features**: DNS record management, API tokens, zone configuration
- **Prerequisites**: Go (for flarectl), Node.js (for Wrangler)

### 🌐 [Google Cloud](./google_cloud/)
- **Purpose**: Google Cloud Platform CLI
- **Platform**: Linux
- **Key Features**: Project management, compute instances, storage
- **Prerequisites**: None (includes bundled Python)

### 💻 [OpenCode](./opencode/)
- **Purpose**: AI-powered code assistant
- **Platform**: Cross-platform
- **Key Features**: Code generation, explanation, interactive sessions
- **Prerequisites**: None (standalone installer)

### 🔧 [Rovo Dev](./revo_dev/)
- **Purpose**: Atlassian-integrated development CLI
- **Platform**: Linux (Debian/Red Hat)
- **Key Features**: Jira/Confluence integration, code review, AI assistance
- **Prerequisites**: Atlassian account, API token

## 🎯 Quick Installation Commands

### Claude Code
```bash
npm install -g @anthropic-ai/claude-code
```

### Cloudflare
```bash
npm install -g wrangler
go install github.com/cloudflare/cloudflare-go/cmd/flarectl@latest
```

### Google Cloud
```bash
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-linux-x86_64.tar.gz
tar -xf google-cloud-cli-linux-x86_64.tar.gz
./google-cloud-sdk/install.sh --quiet
```

### OpenCode
```bash
curl -fsSL https://opencode.ai/install | bash
```

### Rovo Dev
```bash
# For Debian/Ubuntu
sudo apt update && sudo apt install -y acli
acli rovodev auth login
```

## 📋 Common Prerequisites

| Tool | Node.js | Python | Go | Atlassian Account |
|------|---------|--------|----|-------------------|
| Claude Code | ✅ 18+ | ❌ | ❌ | ❌ |
| Cloudflare | ✅ (Wrangler) | ❌ | ✅ (flarectl) | ❌ |
| Google Cloud | ❌ | ✅ (bundled) | ❌ | ❌ |
| OpenCode | ❌ | ❌ | ❌ | ❌ |
| Rovo Dev | ❌ | ❌ | ❌ | ✅ |

## 🔧 System Requirements

- **Operating System**: Linux (Ubuntu/Debian preferred)
- **Architecture**: x86_64 or ARM64
- **Memory**: 2GB+ RAM recommended
- **Storage**: 1GB+ free space
- **Network**: Internet connection for downloads and authentication

## 📖 Usage Guide

1. **Choose your tool** from the available options above
2. **Navigate to the specific directory** (e.g., `cd claude_code/`)
3. **Follow the detailed README** in each directory
4. **Run the installation commands** step by step
5. **Verify the installation** using the provided test commands

## 🔑 Authentication Notes

Most tools require authentication:

- **Claude Code**: OAuth through Anthropic Console
- **Cloudflare**: API tokens from Cloudflare Dashboard
- **Google Cloud**: Interactive login or service account
- **OpenCode**: Account creation through web interface
- **Rovo Dev**: Atlassian API token (unscoped)

## 🚨 Troubleshooting

### Common Issues

1. **Command not found**: Check PATH configuration
2. **Permission denied**: Avoid using `sudo` with npm
3. **Authentication failed**: Verify API tokens and credentials
4. **Network errors**: Check internet connection and firewall

### Getting Help

- Check the specific tool's README for detailed troubleshooting
- Verify system requirements and prerequisites
- Look for error messages in the installation logs
- Consult official documentation links provided in each guide

## 📝 Contributing

To contribute to this repository:

1. Fork the repository
2. Create a feature branch
3. Add or update installation guides
4. Test the installation steps
5. Submit a pull request

## 📄 License

This repository is for educational purposes. Each tool has its own license terms.

## 🔗 Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude/docs/claude-code)
- [Cloudflare CLI Documentation](https://developers.cloudflare.com/workers/cli-wrangler/)
- [Google Cloud CLI Documentation](https://cloud.google.com/sdk/docs)
- [OpenCode Documentation](https://opencode.ai/docs/)
- [Rovo Dev CLI Documentation](https://rovodevagents-beta.atlassian.net/wiki/external/Yzc2NzI4MTk3YTBhNDdiYjkzZDhhZTc3MjE0ZmE4Y2Q)

---

**Last Updated**: 2025-07-10  
**Repository**: https://github.com/kadavilrahul/installation_methods  
**Maintainer**: @kadavilrahul

For issues or questions, please open an issue on GitHub.