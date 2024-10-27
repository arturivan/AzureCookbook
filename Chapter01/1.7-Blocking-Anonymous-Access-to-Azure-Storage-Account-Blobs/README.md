# Blocking Anonymous Access to Azure Storage Account Blobs

### Create a new Azure Storage Account
```
Azure Powershell:

$storageName = "<storage-account-name>"
$location = "<region>"
$resourceGroup = "<rg>"

New-AzStorageAccount `
-ResourceGroupName $resourceGroup `
-Name $storageName `
-Location $location `
-SkuName Standard_LRS ` 
-AllowBlobPublicAccess $false

Azure CLI:

storageName="<storage-account-name>"
location="<region>"

az storage account create \
  --name $storageName \
  --resource-group $rgName \
  --location $region \
  --sku Standard_LRS \
  --allow-blob-public-access false
```

### Disallowing public blob access:
```
Azure Powershell:
# Replace placeholders with actual values
$storageAccountName = "<storage-account-name>"
$resourceGroup = "<rg>"

# Update the storage account
Set-AzStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroup -AllowBlobPublicAccess $false

Azure CLI:
az storage account update \
  --name $storageName \
  --resource-group $rgName \
  --allow-blob-public-access false
```

### Clean up:
```
Azure Powershell:

Remove-AzResourceGroup -Name "<rg>"

Azure CLI:
az group delete --name $rgName
```
