# List membership of AD groups for specified user

Mainly from SO: https://stackoverflow.com/questions/5072996/how-to-get-all-groups-that-a-user-is-a-member-of/

## CMD

Returns additional user information from domain controller. Also works in PS. Truncates long group names (21 char+) *Second place
```
net user username /domain 
```

Returns group name and type information along with SID for current user. Also works in PS. *Fourth place (as no user is specified)
```
whoami /groups
```

## Powershell

List of groups sorted for ease of reading *First place
```
([ADSISEARCHER]"samaccountname=$($env:USERNAME)").Findone().Properties.memberof -replace '^CN=([^,]+).+$','$1' | Sort-Object
```

List all groups (CN, OU, DC), not cleaned and using full reference* Third place
```
(New-Object System.DirectoryServices.DirectorySearcher("(&(objectCategory=User)(samAccountName=$($env:username)))")).FindOne().GetDirectoryEntry().memberOf
```

With ActiveDirectory module, which isn't on most client systems *Last place (as it's so rarely appropriate)
```
Get-ADPrincipalGroupMembership aqh | Format-Table -auto
```
