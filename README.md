[![Gitter](https://badges.gitter.im/aztfmod/community.svg)](https://gitter.im/aztfmod/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

# Configures the Azure Activity Logs for a subscription

Configures the Azure Activity Logs rention for a subscription into:
1. Event Hub for short term and fast access (optional).
2. Storage account for long term retention. 

Reference the module to a specific version (recommended):
```hcl
module "activity_logs" {
    source  = "aztfmod/caf-activity-logs/azurerm"
    version = "0.x.y"
    
    resource_group_name   = var.rg
    location              = var.locations
    tags                  = var.tags
    prefix                = var.prefix
    logs_retention       = var.retention
}
```
## Inputs 

| Name | Type | Default | Description |
| -- | -- | -- | -- |
| resource_group_name | string | None | (Required) Name of the resource group where to create the resource. Changing this forces a new resource to be created. |
| name | string | None | (Required) Name for the objects created (before naming convention applied.) |
| location | string | None | (Required) Specifies the Azure location to deploy the resource. Changing this forces a new resource to be created.  |
| tags | map | None | (Required) Map of tags for the deployment.  |
| logs_retention | string | None | (Required) Number of days to keep the logs for long term retention (storage account)  |
| enable_event_hub | boolean | true | (Optional) Determine to deploy Event Hub for the configuration. |
| convention | string | None | (Required) Naming convention to be used (check at the naming convention module for possible values).  |
| prefix | string | None | (Optional) Prefix to be used. |
| postfix | string | None | (Optional) Postfix to be used. |
| max_length | string | None | (Optional) maximum length to the name of the resource. |


## Outputs

| Name | Type | Description | 
| -- | -- | -- | 
| seclogs_map | map | Returns a map that contains the activity log object: <br> - activity_sa (mandatory) <br> - activity_eh_name (optional, only if enable_event_hub is set to true) <br> - activity_eh_id (optional, only if enable_event_hub is set to true) |