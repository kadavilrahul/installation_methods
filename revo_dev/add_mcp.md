# Adding MCP (Model Context Protocol) to Rovo Dev

This guide documents how to add and configure MCP servers in Rovo Dev to extend its capabilities with external tools and integrations.

## Overview

MCP (Model Context Protocol) allows Rovo Dev to interact with external tools, APIs, and services through standardized server interfaces. This enables capabilities like web scraping, database queries, file operations, and API integrations.

## Prerequisites

- Rovo Dev CLI installed and configured
- Access to the Rovo Dev configuration directory (`~/.rovodev/`)
- Basic understanding of JSON configuration

## Step-by-Step Implementation

### 1. Understanding Rovo Dev's MCP Configuration

Rovo Dev has built-in MCP support with configuration in two key files:

**Main Config**: `.rovodev/config.yml`
```yaml
mcp:
  # Path to the MCP (Model Context Protocol) configuration file
  mcpConfigPath: /root/.rovodev/mcp.json

toolPermissions:
  # List of allowed MCP server names
  allowedMcpServers:
  - node /opt/mcp-servers/fetch-mcp/dist/index.js
```

**MCP Servers Config**: `.rovodev/mcp.json`
```json
{
    "mcpServers": {}
}
```

### 2. Exploring Available MCP Infrastructure

We discovered that Rovo Dev already has MCP infrastructure:

```bash
# Check for existing MCP components
find /root/.local/share/acli/plugin/rovodev/lib -name "*mcp*" -type d
ls /root/.local/share/acli/plugin/rovodev/lib/ | grep mcp

# Found:
# - mcp-1.9.2.dist-info (MCP library)
# - MCP command handler at: src/rovodev/commands/mcp/command.py
# - MCP utilities at: src/rovodev/modules/mcp_utils.py
```

### 3. Checking for Pre-installed MCP Servers

```bash
# Check for existing MCP servers
ls -la /opt/mcp-servers/

# Found: fetch-mcp server already available
# /opt/mcp-servers/fetch-mcp/dist/index.js
```

### 4. Creating the MCP Configuration File

Since the MCP config file didn't exist, we created it:

```bash
# Create the MCP configuration directory if needed
mkdir -p /root/.rovodev/

# Create the MCP configuration file
cat > /root/.rovodev/mcp.json << 'EOF'
{
    "mcpServers": {}
}
EOF
```

### 5. Adding the Fetch MCP Server

We configured the simplest available MCP server - the fetch server for HTTP requests:

```json
{
    "mcpServers": {
        "fetch": {
            "command": "node",
            "args": ["/opt/mcp-servers/fetch-mcp/dist/index.js"]
        }
    }
}
```

**Implementation steps:**
```bash
# Remove empty config
rm /root/.rovodev/mcp.json

# Create new config with fetch server
cat > /root/.rovodev/mcp.json << 'EOF'
{
    "mcpServers": {
        "fetch": {
            "command": "node",
            "args": ["/opt/mcp-servers/fetch-mcp/dist/index.js"]
        }
    }
}
EOF

# Verify configuration
cat /root/.rovodev/mcp.json | python3 -m json.tool
```

### 6. Verifying the Setup

**Check MCP server files:**
```bash
ls -la /opt/mcp-servers/fetch-mcp/dist/
# Output:
# -rwxr-xr-x 1 root root 4555 Jun 16 08:02 Fetcher.js
# -rwxr-xr-x 1 root root 6092 Jun 16 08:02 index.js
# -rwxr-xr-x 1 root root  279 Jun 16 08:02 types.js
```

**Validate JSON configuration:**
```bash
python3 -m json.tool /root/.rovodev/mcp.json
# Should output properly formatted JSON without errors
```

### 7. Testing the MCP Server

The fetch server was tested by making a web request:

```bash
# Test basic web fetching capability
curl -s -L www.nilgiristores.in | head -50
```

This demonstrated that the MCP server can now be used by Rovo Dev to:
- Fetch web content
- Make HTTP requests
- Scrape websites
- Access APIs

## MCP Server Capabilities

### Fetch Server Features
The configured fetch server provides tools for:
- **HTTP GET requests**: Retrieve web content
- **API calls**: Access REST APIs
- **Web scraping**: Extract data from websites
- **Content analysis**: Process fetched content

### Usage Examples
Once configured, you can ask Rovo Dev to:
- "Fetch the content from https://example.com"
- "Get data from this API endpoint"
- "What does this website do?" (as demonstrated)

## Configuration Structure

### MCP Server Configuration Format
```json
{
    "mcpServers": {
        "server-name": {
            "command": "executable-command",
            "args": ["arg1", "arg2", "..."],
            "env": {
                "ENV_VAR": "value"
            }
        }
    }
}
```

### Common MCP Server Types

**Node.js servers:**
```json
"server-name": {
    "command": "node",
    "args": ["/path/to/server.js"]
}
```

**Python servers:**
```json
"server-name": {
    "command": "python3",
    "args": ["-m", "module_name"]
}
```

**NPX packages:**
```json
"server-name": {
    "command": "npx",
    "args": ["package-name"]
}
```

## Adding Additional MCP Servers

### Popular MCP Servers

1. **Filesystem Server**
```json
"filesystem": {
    "command": "python3",
    "args": ["-m", "mcp_server_filesystem", "/allowed/path"]
}
```

2. **GitHub Server**
```json
"github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"]
}
```

3. **Database Server**
```json
"database": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-postgres"],
    "env": {
        "DATABASE_URL": "postgresql://user:pass@host:port/db"
    }
}
```

### Installation Process

1. **Install the MCP server package**
```bash
# For Node.js packages
npm install -g package-name

# For Python packages
pip install package-name
```

2. **Add to mcp.json configuration**
3. **Update allowedMcpServers in config.yml if needed**
4. **Restart Rovo Dev to load new servers**

## Security Considerations

### Permission Management
- MCP servers are controlled by `allowedMcpServers` in config.yml
- Only explicitly allowed servers can be used
- Environment variables can store sensitive credentials

### Best Practices
- Store API keys in environment variables
- Limit filesystem access paths
- Use specific server versions
- Regularly update MCP servers

## Troubleshooting

### Common Issues

**MCP server not found:**
- Verify the command path exists
- Check executable permissions
- Ensure dependencies are installed

**Permission denied:**
- Add server to `allowedMcpServers` list
- Check file permissions
- Verify user access rights

**JSON syntax errors:**
- Validate JSON with `python3 -m json.tool`
- Check for trailing commas
- Ensure proper escaping

### Debug Commands
```bash
# Validate MCP configuration
python3 -m json.tool /root/.rovodev/mcp.json

# Check server executable
ls -la /path/to/server

# Test server manually (if applicable)
node /path/to/server.js --help
```

## Resources

### MCP Server Repositories
- [Official MCP Servers](https://github.com/modelcontextprotocol/servers)
- [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers)
- [MCP Server Directory](https://mcpservers.org/)

### Documentation
- [MCP Protocol Specification](https://modelcontextprotocol.io/)
- [Rovo Dev Documentation](https://developer.atlassian.com/rovo/)

## Conclusion

MCP integration in Rovo Dev provides powerful extensibility through standardized server interfaces. The fetch server example demonstrates how to:

1. Configure MCP servers in the JSON configuration file
2. Set appropriate permissions
3. Test functionality through practical usage

This foundation enables adding more sophisticated integrations like databases, APIs, and custom tools to enhance Rovo Dev's capabilities.

---

**Last Updated**: June 2025  
**Rovo Dev Version**: 0.6.8  
**MCP Library Version**: 1.9.2
