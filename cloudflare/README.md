# Cloudflare CLI Management

## Installation

### Install Wrangler (for Workers)
```bash
npm install -g wrangler
```

### Install flarectl (for DNS/Zone management)
```bash
go install github.com/cloudflare/cloudflare-go/cmd/flarectl@latest
```

### Add Go bin to PATH
```bash
echo 'export PATH=$PATH:~/go/bin' >> ~/.bashrc
export PATH=$PATH:~/go/bin
```

## Authentication

### Create API Token
1. Go to https://dash.cloudflare.com/profile/api-tokens
2. Click "Create Token"
3. For Workers: Use "Edit Cloudflare Workers" template
4. For DNS: Use "Custom token" with permissions:
   - Zone:Read
   - DNS:Edit
   - Account:Read
   - User:Read (optional, for email display)

### Set Environment Variables
```bash
# For Wrangler
export CLOUDFLARE_API_TOKEN=your_token_here
echo 'export CLOUDFLARE_API_TOKEN=your_token_here' >> ~/.bashrc

# For flarectl
export CF_API_TOKEN=your_token_here
echo 'export CF_API_TOKEN=your_token_here' >> ~/.bashrc
```

## Verify Authentication

### Test Wrangler
```bash
wrangler whoami
```

### Test flarectl
```bash
flarectl zone list
```

## DNS Management Commands

### List All Zones
```bash
CF_API_TOKEN=your_token flarectl zone list
```

### List DNS Records
```bash
CF_API_TOKEN=your_token flarectl dns list --zone example.com
```

### Add DNS Record
```bash
# Add A record
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name subdomain --type A --content 1.2.3.4

# Add CNAME record
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name www --type CNAME --content example.com

# Add MX record
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type MX --content "10 mail.example.com"

# Add TXT record
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type TXT --content "v=spf1 mx ~all"
```

### Update DNS Record
```bash
CF_API_TOKEN=your_token flarectl dns update --zone example.com --id record_id --content new_ip_address
```

### Delete DNS Record
```bash
CF_API_TOKEN=your_token flarectl dns delete --zone example.com --id record_id
```

### Filter DNS Records
```bash
# Filter by type
CF_API_TOKEN=your_token flarectl dns list --zone example.com --type A

# Filter by name
CF_API_TOKEN=your_token flarectl dns list --zone example.com --name www

# Filter by content
CF_API_TOKEN=your_token flarectl dns list --zone example.com --content 1.2.3.4
```

## Zone Management

### Get Zone Info
```bash
CF_API_TOKEN=your_token flarectl zone info --zone example.com
```

### Enable Development Mode
```bash
CF_API_TOKEN=your_token flarectl zone settings --zone example.com --development-mode on
```

## Direct API Usage

### List Zones
```bash
curl -X GET "https://api.cloudflare.com/client/v4/zones" \
  -H "Authorization: Bearer your_token"
```

### List DNS Records
```bash
curl -X GET "https://api.cloudflare.com/client/v4/zones/zone_id/dns_records" \
  -H "Authorization: Bearer your_token"
```

### Create DNS Record
```bash
curl -X POST "https://api.cloudflare.com/client/v4/zones/zone_id/dns_records" \
  -H "Authorization: Bearer your_token" \
  -H "Content-Type: application/json" \
  --data '{
    "type": "A",
    "name": "subdomain",
    "content": "1.2.3.4",
    "ttl": 1
  }'
```

## Common Record Types

### A Record (IPv4)
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type A --content 1.2.3.4
```

### AAAA Record (IPv6)
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type AAAA --content 2001:db8::1
```

### CNAME Record
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name www --type CNAME --content example.com
```

### MX Record
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type MX --content "10 mail.example.com"
```

### TXT Record
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name @ --type TXT --content "v=spf1 mx ~all"
```

### SRV Record
```bash
CF_API_TOKEN=your_token flarectl dns create --zone example.com --name _service._tcp --type SRV --content "10 5 80 target.example.com"
```

## Tips

1. **Always backup DNS records** before making changes
2. **Test changes** with `dig` or `nslookup` after modifications
3. **Use TTL of 1** for auto (proxied records) or specify seconds for manual
4. **Enable proxy** by adding `--proxy` flag for A/AAAA/CNAME records
5. **Check rate limits** - API has request limits per minute

## Adding Domains to Cloudflare

1. Go to https://dash.cloudflare.com
2. Click "Add a domain"
3. Enter your domain name
4. Follow setup process
5. Update nameservers at your registrar to:
   - `javon.ns.cloudflare.com`
   - `paige.ns.cloudflare.com` (or as provided)
6. Wait for DNS propagation (up to 24 hours)

## Troubleshooting

### Token Not Working
- Check token permissions at https://dash.cloudflare.com/profile/api-tokens
- Ensure token has required permissions for your operations
- Verify environment variable is set correctly

### Zone Not Found
- Ensure domain is added to your Cloudflare account
- Check exact spelling of domain name
- Verify domain is active (not pending)

### DNS Changes Not Propagating
- Check TTL settings (lower TTL = faster propagation)
- Use `dig @1.1.1.1 domain.com` to check Cloudflare's DNS
- Wait up to 24 hours for full global propagation
