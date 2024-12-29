# Cloudflare DNS Alfred Workflow

An Alfred workflow to quickly create and delete DNS records in Cloudflare directly from Alfred.

## Requirements

- Alfred Powerpack
- Python 3.x (comes pre-installed on macOS)
- Cloudflare API Token with DNS edit permissions

## Installation

1. Download the latest `Cloudflare.alfredworkflow` from the [Releases](../../releases) page
2. Double-click the downloaded file to install it in Alfred
3. Set your Cloudflare API Token in the workflow environment variables:
   - Open Alfred Preferences
   - Go to Workflows
   - Select the Cloudflare workflow
   - Click the [𝓍] button in the top-right corner
   - Add a new environment variable:
     - Name: `CLOUDFLARE_API_TOKEN`
     - Value: Your Cloudflare API token

## Usage

### Create DNS Record
```
cfcreate {subdomain} {domain} {value} [proxy]
```
The value can optionally include a record type prefix (e.g., `a:` or `cname:`). If no type is specified, an A record is created.

Examples:
```
# A Records (all equivalent)
cfcreate blog example.com 192.168.1.1        # A record (default)
cfcreate blog example.com a:192.168.1.1      # A record (explicit)
cfcreate blog example.com A:192.168.1.1      # A record (explicit)

# CNAME Records
cfcreate blog example.com cname:target.com    # CNAME record
cfcreate blog example.com CNAME:target.com    # CNAME record

# With Proxy Enabled
cfcreate blog example.com 192.168.1.1 proxy        # A record with proxy
cfcreate blog example.com cname:target.com proxy   # CNAME record with proxy
```

### Delete DNS Record
```
cfdelete {subdomain} {domain}
```
Example:
```
cfdelete blog example.com
```
This will delete the DNS record for `blog.example.com`

## Getting a Cloudflare API Token

1. Log in to your Cloudflare dashboard
2. Go to My Profile > API Tokens
3. Click "Create Token"
4. Use the "Edit zone DNS" template or create a custom token with:
   - Zone > DNS > Edit permissions
   - Include the zones you want to manage
5. Copy the generated token and add it to the workflow's environment variables 