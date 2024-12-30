# Cloudflare DNS Alfred Workflow

An [Alfred](https://alfred.app/) workflow to quickly create and delete DNS records in Cloudflare directly from Alfred.

**Download here: [Cloudflare Alfred Workflow Download](https://github.com/pbdco/cloudflare-alfredworkflow/releases/latest/download/Cloudflare.alfredworkflow)**

- Creating an A record, with disabled proxy:
![image](https://github.com/user-attachments/assets/d30924c7-5222-42ae-8f67-807ac5d74762)

- Creating a CNAME record with proxy enabled:
![image](https://github.com/user-attachments/assets/e136102f-10be-4cf3-bd65-dc347fbbd1e1)


## Requirements

- Alfred Powerpack
- Python 3.x (comes pre-installed on macOS)
- Cloudflare API Token with DNS edit permissions

## Installation

1. Download the latest `Cloudflare.alfredworkflow` from the [Releases](../../releases) page: [Cloudflare Alfred Workflow Download](https://github.com/pbdco/cloudflare-alfredworkflow/releases/latest/download/Cloudflare.alfredworkflow)
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

The `value` parameter can include an optional record type prefix. Currently supported record types:
- `A` records (default): Use IP address as value
- `CNAME` records: Use target domain as value

If no record type is specified, an A record is created by default.

Examples:
```
# A Records (all these are equivalent)
cfcreate blog example.com 192.168.1.1        # A record (implicit)
cfcreate blog example.com a:192.168.1.1      # A record (explicit)
cfcreate blog example.com A:192.168.1.1      # A record (explicit)

# CNAME Records
cfcreate blog example.com cname:target.com    # CNAME record
cfcreate blog example.com CNAME:target.com    # CNAME record (case insensitive)

# With Cloudflare Proxy (Orange Cloud)
cfcreate blog example.com 192.168.1.1 proxy         # A record with proxy
cfcreate blog example.com cname:target.com proxy    # CNAME record with proxy
```

### Delete DNS Record
```
cfdelete {subdomain} {domain}
```
Example:
```
cfdelete blog example.com
```
This will delete any DNS record (A or CNAME) for `blog.example.com`

## Getting a Cloudflare API Token

1. Log in to your Cloudflare dashboard
2. Go to My Profile > API Tokens
3. Click "Create Token"
4. Use the "Edit zone DNS" template or create a custom token with:
   - Zone > DNS > Edit permissions
   - Include the zones you want to manage
5. Copy the generated token and add it to the workflow's environment variables 
