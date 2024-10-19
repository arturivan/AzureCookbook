# Creating a New User in Your Azure Account 
Scripts are converted to Powershell syntax

### Create a new user in your Azure Active Directory:
```
$password="<password>"

az ad user create `
  --display-name developer `
  --password $password `
  --user-principal-name developer@<aad-tenant-name>
```

### Get the subscription id:
```
Get-AzSubscription
```

### Create a new RBAC role assignment:
```
az role assignment create `
  --assignee "developer@<entra-tenant>" `
  --role "Contributor" `
  --scope subscriptions/<yourSubscriptionId>
```

### List the RBAC roles assigned to account:
```
az role assignment list \
  --assignee developer@<aad-tenant-name> 
```

# Cleanup

Deleting the RBAC role assignment:
```
az role assignment delete \
  --assignee "developer@<aad-tenant-name>" \
  --role "Contributor"
```
