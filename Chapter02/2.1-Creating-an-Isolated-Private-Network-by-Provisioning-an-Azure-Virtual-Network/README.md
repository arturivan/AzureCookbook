# Creating an Isolated Private Network by Provisioning an Azure Virtual Network

### Azure CLI
### Creating a new Azure VNet
```
rgName="<resource-group-name>"
vnetName="<vnet-name>"

az network vnet create \
    --resource-group $rgName \
    --name $vnetName \
    --address-prefix 10.0.0.0/16 \
    --subnet-name Subnet01 \
    --subnet-prefix 10.0.0.0/26
```

### Getting VNet details
```
az network vnet show \
    --resource-group $rgName \
    --name $vnetName
```

### Terraform

```
provider "azurerm" {
  features {}
  subscription_id = var.subscription_id
}

# Define variables for resource group and virtual network names
variable "subscription_id" {
  description = "Azure Subscription ID"
  type        = string
}

variable "rg_name" {
  description = "The name of the resource group"
  type        = string
}

variable "vnet_name" {
  description = "The name of the virtual network"
  type        = string
}

variable "address_space" {
  description = "The address space of the virtual network"
  type        = string
  default     = "10.0.0.0/16"
}

variable "subnet_name" {
  description = "The name of the subnet"
  type        = string
  default     = "Subnet01"
}

variable "subnet_prefix" {
  description = "The address prefix of the subnet"
  type        = string
  default     = "10.0.0.0/26"
}

# Resource Group
resource "azurerm_resource_group" "rg" {
  name     = var.rg_name
  location = "East US"  # Change to your preferred region
}

# Virtual Network
resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  address_space       = [var.address_space]
}

# Subnet
resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = [var.subnet_prefix]
}
```
