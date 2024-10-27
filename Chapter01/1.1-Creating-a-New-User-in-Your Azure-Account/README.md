# Creating a New User in Your Azure Account 
Scripts are converted to Azure Powershell syntax

### Create a new user in your Entra ID:
```
Connect-Entra -Scopes 'User.ReadWrite.All'
$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password = '<Password>'

$userParams = @{
    DisplayName       = 'Blake Martin'
    PasswordProfile   = $PasswordProfile
    UserPrincipalName = 'user@<entra-tenant>' # BlakeM@contoso.com
    AccountEnabled    = $true
    MailNickName      = 'BlakeM'
    City              = 'New York'
}

New-EntraUser @userParams
```

### Get the subscription id:
```
Get-AzSubscription
```

### Create a new RBAC role assignment:
```
New-AzRoleAssignment `
  -SignInName "user@<entra-tenant>" `
  -RoleDefinitionName "Contributor" `
  -scope "/subscriptions/<yourSubscriptionId>"
```

### List the RBAC roles assigned to account:
```
Get-AzRoleAssignment `
  -SignInName "user@<entra-tenant>"
```

# Cleanup

Deleting the RBAC role assignment:
```
Remove-AzRoleAssignment `
  -SignInName "user@<entra-tenant>" `
  -RoleDefinitionName "Contributor"
```
