# Creating a New Custom Role for Our User

### Get the subscription id
```
Powershell:
Get-AzSubscription

Bash:
subscriptionId=$(az account show \
  --query "id" --output tsv)

subscriptionScope="/subscriptions/"$subscriptionId

echo $subscriptionScope
```

### Create a new custom RBAC role definition:
```
{
    "Name": "Custom Storage Reader",
    "IsCustom": true,
    "Description": "Read access to Azure storage accounts",
    "DataActions": [
        "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read"
    ],
    "AssignableScopes": [
        "/subscriptions/<subscriptionId>"
    ]
}

Powershell:
az role definiton create `
--role-definition CustomStorageDataReader.json


Bash:
az role definition create \
  --role-definition CustomStorageDataReader.json
```

### Assign the new role definition to user account
```
Powershell:
az role assignment create `
  --assignee "developer@<entra-tenant>" `
  --role "Custom Storage Data Reader" `
  --scope subscriptions/<yourSubscriptionId>



Bash:
MSYS_NO_PATHCONV=1 az role assignment create \
  --assignee "developer@<aad-tenant-name>" \
  --role "Custom Storage Data Reader" \
  --scope $subscriptionScope
```
