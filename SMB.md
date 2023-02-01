# SMB
## Enumeration
```bash
enum4linux -S -U -d <% tp.frontmatter.target_ip %>
```

## Usage
```bash
smbclient //<% tp.frontmatter.target_ip %>/share_name -U user_name
```