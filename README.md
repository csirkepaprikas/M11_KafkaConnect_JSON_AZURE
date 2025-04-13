# Module 2: Kafka Connect
### Balázs Mikes

#### github link:
https://github.com/csirkepaprikas/M10_KafkaBasics_SQL_LOCAL.git

Kafka Connect Homework

The Kafka Connect Homework demonstrated how to easily connect applications with Kafka and deploy them. This assignment emphasized the importance of deployment in such applications and provided me with more experience using Terraform/Kubernetes for this purpose.
Additionally, customization of Kafka Connect operators is an essential part of working with them, so this homework taught me how to customize them if needed.
By the end of this assignment, I had gained practical skills in connecting applications with Kafka, deploying them, and customizing Kafka Connect operators.

#### Preparations:

First I created a new Resource Group in Azure:

![RG_created](https://github.com/user-attachments/assets/1e2fa280-4fd5-46c0-bfa9-028fe5468f88)

Then I created a storage account:

![stor_acc_create](https://github.com/user-attachments/assets/b20e07e8-f394-4650-a401-409d0cb67701)

Here you can see the completed storage account:

![stor-acc_complete](https://github.com/user-attachments/assets/f3f40e68-eb77-4f43-9663-da45dcd1c78e)

Then I created a "tfstae" container for the terraform state logs:

![tfstate_cont](https://github.com/user-attachments/assets/42d24f9f-f3e9-4983-818e-ac93e83b9482)

The next step was to update the terraform configuration file, the main.tf .

Then run terraform init, terraform plan -out terraform.plan and terraform apply terraform.plan
 commands:
```python
 c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>terraform init
Initializing the backend...

Successfully configured the backend "azurerm"! Terraform will automatically
use this backend unless the backend configuration changes.
Initializing provider plugins...
- Finding latest version of hashicorp/local...
- Finding latest version of hashicorp/kubernetes...
- Finding latest version of hashicorp/random...
- Finding hashicorp/azurerm versions matching "~> 4.3.0"...
- Installing hashicorp/local v2.5.2...
- Installed hashicorp/local v2.5.2 (signed by HashiCorp)
- Installing hashicorp/kubernetes v2.36.0...
- Installed hashicorp/kubernetes v2.36.0 (signed by HashiCorp)
- Installing hashicorp/random v3.7.1...
- Installed hashicorp/random v3.7.1 (signed by HashiCorp)
- Installing hashicorp/azurerm v4.3.0...
- Installed hashicorp/azurerm v4.3.0 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>terraform plan -out terraform.plan
Acquiring state lock. This may take a few moments...
data.azurerm_client_config.current: Reading...
data.azurerm_client_config.current: Read complete after 0s [id=]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # data.azurerm_storage_account.storage will be read during apply
  # (config refers to values not yet known)
 <= data "azurerm_storage_account" "storage" {
      + access_tier                        = (known after apply)
      + account_kind                       = (known after apply)
      + account_replication_type           = (known after apply)
      + account_tier                       = (known after apply)
      + allow_nested_items_to_be_public    = (known after apply)
      + azure_files_authentication         = (known after apply)
      + custom_domain                      = (known after apply)
      + dns_endpoint_type                  = (known after apply)
      + https_traffic_only_enabled         = (known after apply)
      + id                                 = (known after apply)
      + identity                           = (known after apply)
      + infrastructure_encryption_enabled  = (known after apply)
      + is_hns_enabled                     = (known after apply)
      + location                           = (known after apply)
      + name                               = (known after apply)
      + nfsv3_enabled                      = (known after apply)
      + primary_access_key                 = (sensitive value)
      + primary_blob_connection_string     = (sensitive value)
      + primary_blob_endpoint              = (known after apply)
      + primary_blob_host                  = (known after apply)
      + primary_blob_internet_endpoint     = (known after apply)
      + primary_blob_internet_host         = (known after apply)
      + primary_blob_microsoft_endpoint    = (known after apply)
      + primary_blob_microsoft_host        = (known after apply)
      + primary_connection_string          = (sensitive value)
      + primary_dfs_endpoint               = (known after apply)
      + primary_dfs_host                   = (known after apply)
      + primary_dfs_internet_endpoint      = (known after apply)
      + primary_dfs_internet_host          = (known after apply)
      + primary_dfs_microsoft_endpoint     = (known after apply)
      + primary_dfs_microsoft_host         = (known after apply)
      + primary_file_endpoint              = (known after apply)
      + primary_file_host                  = (known after apply)
      + primary_file_internet_endpoint     = (known after apply)
      + primary_file_internet_host         = (known after apply)
      + primary_file_microsoft_endpoint    = (known after apply)
      + primary_file_microsoft_host        = (known after apply)
      + primary_location                   = (known after apply)
      + primary_queue_endpoint             = (known after apply)
      + primary_queue_host                 = (known after apply)
      + primary_queue_microsoft_endpoint   = (known after apply)
      + primary_queue_microsoft_host       = (known after apply)
      + primary_table_endpoint             = (known after apply)
      + primary_table_host                 = (known after apply)
      + primary_table_microsoft_endpoint   = (known after apply)
      + primary_table_microsoft_host       = (known after apply)
      + primary_web_endpoint               = (known after apply)
      + primary_web_host                   = (known after apply)
      + primary_web_internet_endpoint      = (known after apply)
      + primary_web_internet_host          = (known after apply)
      + primary_web_microsoft_endpoint     = (known after apply)
      + primary_web_microsoft_host         = (known after apply)
      + queue_encryption_key_type          = (known after apply)
      + resource_group_name                = (known after apply)
      + secondary_access_key               = (sensitive value)
      + secondary_blob_connection_string   = (sensitive value)
      + secondary_blob_endpoint            = (known after apply)
      + secondary_blob_host                = (known after apply)
      + secondary_blob_internet_endpoint   = (known after apply)
      + secondary_blob_internet_host       = (known after apply)
      + secondary_blob_microsoft_endpoint  = (known after apply)
      + secondary_blob_microsoft_host      = (known after apply)
      + secondary_connection_string        = (sensitive value)
      + secondary_dfs_endpoint             = (known after apply)
      + secondary_dfs_host                 = (known after apply)
      + secondary_dfs_internet_endpoint    = (known after apply)
      + secondary_dfs_internet_host        = (known after apply)
      + secondary_dfs_microsoft_endpoint   = (known after apply)
      + secondary_dfs_microsoft_host       = (known after apply)
      + secondary_file_endpoint            = (known after apply)
      + secondary_file_host                = (known after apply)
      + secondary_file_internet_endpoint   = (known after apply)
      + secondary_file_internet_host       = (known after apply)
      + secondary_file_microsoft_endpoint  = (known after apply)
      + secondary_file_microsoft_host      = (known after apply)
      + secondary_location                 = (known after apply)
      + secondary_queue_endpoint           = (known after apply)
      + secondary_queue_host               = (known after apply)
      + secondary_queue_microsoft_endpoint = (known after apply)
      + secondary_queue_microsoft_host     = (known after apply)
      + secondary_table_endpoint           = (known after apply)
      + secondary_table_host               = (known after apply)
      + secondary_table_microsoft_endpoint = (known after apply)
      + secondary_table_microsoft_host     = (known after apply)
      + secondary_web_endpoint             = (known after apply)
      + secondary_web_host                 = (known after apply)
      + secondary_web_internet_endpoint    = (known after apply)
      + secondary_web_internet_host        = (known after apply)
      + secondary_web_microsoft_endpoint   = (known after apply)
      + secondary_web_microsoft_host       = (known after apply)
      + table_encryption_key_type          = (known after apply)
      + tags                               = (known after apply)
    }

  # azurerm_container_registry.acr will be created
  + resource "azurerm_container_registry" "acr" {
      + admin_enabled                 = false
      + admin_password                = (sensitive value)
      + admin_username                = (known after apply)
      + encryption                    = (known after apply)
      + export_policy_enabled         = true
      + id                            = (known after apply)
      + location                      = "westeurope"
      + login_server                  = (known after apply)
      + name                          = (known after apply)
      + network_rule_bypass_option    = "AzureServices"
      + network_rule_set              = (known after apply)
      + public_network_access_enabled = true
      + resource_group_name           = (known after apply)
      + sku                           = "Standard"
      + tags                          = {
          + "env"    = "dev"
          + "region" = "global"
        }
      + trust_policy_enabled          = false
      + zone_redundancy_enabled       = false
    }

  # azurerm_kubernetes_cluster.bdcc will be created
  + resource "azurerm_kubernetes_cluster" "bdcc" {
      + current_kubernetes_version          = (known after apply)
      + dns_prefix                          = "bdccdev"
      + fqdn                                = (known after apply)
      + http_application_routing_zone_name  = (known after apply)
      + id                                  = (known after apply)
      + kube_admin_config                   = (sensitive value)
      + kube_admin_config_raw               = (sensitive value)
      + kube_config                         = (sensitive value)
      + kube_config_raw                     = (sensitive value)
      + kubernetes_version                  = (known after apply)
      + location                            = "westeurope"
      + name                                = (known after apply)
      + node_os_upgrade_channel             = "NodeImage"
      + node_resource_group                 = (known after apply)
      + node_resource_group_id              = (known after apply)
      + oidc_issuer_url                     = (known after apply)
      + portal_fqdn                         = (known after apply)
      + private_cluster_enabled             = false
      + private_cluster_public_fqdn_enabled = false
      + private_dns_zone_id                 = (known after apply)
      + private_fqdn                        = (known after apply)
      + resource_group_name                 = (known after apply)
      + role_based_access_control_enabled   = true
      + run_command_enabled                 = true
      + sku_tier                            = "Free"
      + support_plan                        = "KubernetesOfficial"
      + tags                                = {
          + "env"    = "dev"
          + "region" = "global"
        }
      + workload_identity_enabled           = false

      + auto_scaler_profile (known after apply)

      + default_node_pool {
          + kubelet_disk_type    = (known after apply)
          + max_pods             = (known after apply)
          + name                 = "default"
          + node_count           = 1
          + node_labels          = (known after apply)
          + orchestrator_version = (known after apply)
          + os_disk_size_gb      = (known after apply)
          + os_disk_type         = "Managed"
          + os_sku               = (known after apply)
          + scale_down_mode      = "Delete"
          + type                 = "VirtualMachineScaleSets"
          + ultra_ssd_enabled    = false
          + vm_size              = "Standard_E4s_v3"
          + workload_runtime     = (known after apply)
        }

      + identity {
          + principal_id = (known after apply)
          + tenant_id    = (known after apply)
          + type         = "SystemAssigned"
        }

      + kubelet_identity (known after apply)

      + network_profile (known after apply)

      + windows_profile (known after apply)
    }

  # azurerm_resource_group.bdcc will be created
  + resource "azurerm_resource_group" "bdcc" {
      + id       = (known after apply)
      + location = "westeurope"
      + name     = (known after apply)
      + tags     = {
          + "env"    = "dev"
          + "region" = "global"
        }
    }

  # azurerm_role_assignment.aks_acr_pull will be created
  + resource "azurerm_role_assignment" "aks_acr_pull" {
      + id                               = (known after apply)
      + name                             = (known after apply)
      + principal_id                     = (known after apply)
      + principal_type                   = (known after apply)
      + role_definition_id               = (known after apply)
      + role_definition_name             = "AcrPull"
      + scope                            = (known after apply)
      + skip_service_principal_aad_check = (known after apply)
    }

  # azurerm_storage_account.bdcc will be created
  + resource "azurerm_storage_account" "bdcc" {
      + access_tier                        = (known after apply)
      + account_kind                       = "StorageV2"
      + account_replication_type           = "LRS"
      + account_tier                       = "Standard"
      + allow_nested_items_to_be_public    = true
      + cross_tenant_replication_enabled   = false
      + default_to_oauth_authentication    = false
      + dns_endpoint_type                  = "Standard"
      + https_traffic_only_enabled         = true
      + id                                 = (known after apply)
      + infrastructure_encryption_enabled  = false
      + is_hns_enabled                     = true
      + large_file_share_enabled           = (known after apply)
      + local_user_enabled                 = true
      + location                           = "westeurope"
      + min_tls_version                    = "TLS1_2"
      + name                               = (known after apply)
      + nfsv3_enabled                      = false
      + primary_access_key                 = (sensitive value)
      + primary_blob_connection_string     = (sensitive value)
      + primary_blob_endpoint              = (known after apply)
      + primary_blob_host                  = (known after apply)
      + primary_blob_internet_endpoint     = (known after apply)
      + primary_blob_internet_host         = (known after apply)
      + primary_blob_microsoft_endpoint    = (known after apply)
      + primary_blob_microsoft_host        = (known after apply)
      + primary_connection_string          = (sensitive value)
      + primary_dfs_endpoint               = (known after apply)
      + primary_dfs_host                   = (known after apply)
      + primary_dfs_internet_endpoint      = (known after apply)
      + primary_dfs_internet_host          = (known after apply)
      + primary_dfs_microsoft_endpoint     = (known after apply)
      + primary_dfs_microsoft_host         = (known after apply)
      + primary_file_endpoint              = (known after apply)
      + primary_file_host                  = (known after apply)
      + primary_file_internet_endpoint     = (known after apply)
      + primary_file_internet_host         = (known after apply)
      + primary_file_microsoft_endpoint    = (known after apply)
      + primary_file_microsoft_host        = (known after apply)
      + primary_location                   = (known after apply)
      + primary_queue_endpoint             = (known after apply)
      + primary_queue_host                 = (known after apply)
      + primary_queue_microsoft_endpoint   = (known after apply)
      + primary_queue_microsoft_host       = (known after apply)
      + primary_table_endpoint             = (known after apply)
      + primary_table_host                 = (known after apply)
      + primary_table_microsoft_endpoint   = (known after apply)
      + primary_table_microsoft_host       = (known after apply)
      + primary_web_endpoint               = (known after apply)
      + primary_web_host                   = (known after apply)
      + primary_web_internet_endpoint      = (known after apply)
      + primary_web_internet_host          = (known after apply)
      + primary_web_microsoft_endpoint     = (known after apply)
      + primary_web_microsoft_host         = (known after apply)
      + public_network_access_enabled      = true
      + queue_encryption_key_type          = "Service"
      + resource_group_name                = (known after apply)
      + secondary_access_key               = (sensitive value)
      + secondary_blob_connection_string   = (sensitive value)
      + secondary_blob_endpoint            = (known after apply)
      + secondary_blob_host                = (known after apply)
      + secondary_blob_internet_endpoint   = (known after apply)
      + secondary_blob_internet_host       = (known after apply)
      + secondary_blob_microsoft_endpoint  = (known after apply)
      + secondary_blob_microsoft_host      = (known after apply)
      + secondary_connection_string        = (sensitive value)
      + secondary_dfs_endpoint             = (known after apply)
      + secondary_dfs_host                 = (known after apply)
      + secondary_dfs_internet_endpoint    = (known after apply)
      + secondary_dfs_internet_host        = (known after apply)
      + secondary_dfs_microsoft_endpoint   = (known after apply)
      + secondary_dfs_microsoft_host       = (known after apply)
      + secondary_file_endpoint            = (known after apply)
      + secondary_file_host                = (known after apply)
      + secondary_file_internet_endpoint   = (known after apply)
      + secondary_file_internet_host       = (known after apply)
      + secondary_file_microsoft_endpoint  = (known after apply)
      + secondary_file_microsoft_host      = (known after apply)
      + secondary_location                 = (known after apply)
      + secondary_queue_endpoint           = (known after apply)
      + secondary_queue_host               = (known after apply)
      + secondary_queue_microsoft_endpoint = (known after apply)
      + secondary_queue_microsoft_host     = (known after apply)
      + secondary_table_endpoint           = (known after apply)
      + secondary_table_host               = (known after apply)
      + secondary_table_microsoft_endpoint = (known after apply)
      + secondary_table_microsoft_host     = (known after apply)
      + secondary_web_endpoint             = (known after apply)
      + secondary_web_host                 = (known after apply)
      + secondary_web_internet_endpoint    = (known after apply)
      + secondary_web_internet_host        = (known after apply)
      + secondary_web_microsoft_endpoint   = (known after apply)
      + secondary_web_microsoft_host       = (known after apply)
      + sftp_enabled                       = false
      + shared_access_key_enabled          = true
      + table_encryption_key_type          = "Service"
      + tags                               = {
          + "env"    = "dev"
          + "region" = "global"
        }

      + blob_properties (known after apply)

      + network_rules {
          + bypass                     = (known after apply)
          + default_action             = "Allow"
          + ip_rules                   = [
              + "174.128.60.160",
              + "174.128.60.162",
              + "185.44.13.36",
              + "195.56.119.209",
              + "195.56.119.212",
              + "203.170.48.2",
              + "204.153.55.4",
              + "213.184.231.20",
              + "85.223.209.18",
              + "86.57.255.94",
            ]
          + virtual_network_subnet_ids = (known after apply)
        }

      + queue_properties (known after apply)

      + routing (known after apply)

      + share_properties (known after apply)
    }

  # azurerm_storage_data_lake_gen2_filesystem.gen2_data will be created
  + resource "azurerm_storage_data_lake_gen2_filesystem" "gen2_data" {
      + default_encryption_scope = (known after apply)
      + group                    = (known after apply)
      + id                       = (known after apply)
      + name                     = "data"
      + owner                    = (known after apply)
      + storage_account_id       = (known after apply)

      + ace (known after apply)
    }

  # kubernetes_namespace.confluent will be created
  + resource "kubernetes_namespace" "confluent" {
      + id                               = (known after apply)
      + wait_for_default_service_account = false

      + metadata {
          + generation       = (known after apply)
          + name             = "confluent"
          + resource_version = (known after apply)
          + uid              = (known after apply)
        }
    }

  # local_file.azure_connector_config will be created
  + resource "local_file" "azure_connector_config" {
      + content              = (sensitive value)
      + content_base64sha256 = (known after apply)
      + content_base64sha512 = (known after apply)
      + content_md5          = (known after apply)
      + content_sha1         = (known after apply)
      + content_sha256       = (known after apply)
      + content_sha512       = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "azure-source-cc.json"
      + id                   = (known after apply)
    }

  # random_string.suffix will be created
  + resource "random_string" "suffix" {
      + id          = (known after apply)
      + length      = 2
      + lower       = true
      + min_lower   = 0
      + min_numeric = 0
      + min_special = 0
      + min_upper   = 0
      + number      = true
      + numeric     = true
      + result      = (known after apply)
      + special     = false
      + upper       = false
    }

Plan: 9 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + acr_login_server           = (known after apply)
  + aks_api_server_url         = (sensitive value)
  + aks_kubeconfig             = (sensitive value)
  + aks_name                   = (known after apply)
  + client_certificate         = (sensitive value)
  + resource_group_name        = (known after apply)
  + storage_account_name       = (known after apply)
  + storage_primary_access_key = (sensitive value)

────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Saved the plan to: terraform.plan

To perform exactly these actions, run the following command to apply:
    terraform apply "terraform.plan"
Releasing state lock. This may take a few moments...

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>terraform apply terraform.plan
Acquiring state lock. This may take a few moments...
random_string.suffix: Creating...
random_string.suffix: Creation complete after 0s [id=vw]
azurerm_resource_group.bdcc: Creating...
azurerm_resource_group.bdcc: Still creating... [10s elapsed]
azurerm_resource_group.bdcc: Creation complete after 10s [id=/subscriptions/]
azurerm_container_registry.acr: Creating...
azurerm_storage_account.bdcc: Creating...
azurerm_kubernetes_cluster.bdcc: Creating...
azurerm_container_registry.acr: Still creating... [10s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [10s elapsed]
azurerm_storage_account.bdcc: Still creating... [10s elapsed]
azurerm_container_registry.acr: Still creating... [20s elapsed]
azurerm_storage_account.bdcc: Still creating... [20s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [20s elapsed]
azurerm_container_registry.acr: Creation complete after 23s [id=/subscriptions/w]
azurerm_storage_account.bdcc: Still creating... [30s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [30s elapsed]
azurerm_storage_account.bdcc: Still creating... [40s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [40s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [50s elapsed]
azurerm_storage_account.bdcc: Still creating... [50s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m0s elapsed]
azurerm_storage_account.bdcc: Still creating... [1m0s elapsed]
azurerm_storage_account.bdcc: Creation complete after 1m9s [id=/subscriptions/]
data.azurerm_storage_account.storage: Reading...
azurerm_storage_data_lake_gen2_filesystem.gen2_data: Creating...
data.azurerm_storage_account.storage: Read complete after 1s [id=/subscriptions/]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m10s elapsed]
azurerm_storage_data_lake_gen2_filesystem.gen2_data: Creation complete after 1s [id=https://devwesteuropevw.dfs.core.windows.net/data]
local_file.azure_connector_config: Creating...
local_file.azure_connector_config: Creation complete after 0s [id=c9]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m20s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m30s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m40s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [1m50s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m0s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m10s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m20s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m30s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m40s elapsed]
azurerm_kubernetes_cluster.bdcc: Still creating... [2m50s elapsed]
azurerm_kubernetes_cluster.bdcc: Creation complete after 2m59s [id=/subscriptions/urope-vw]
azurerm_role_assignment.aks_acr_pull: Creating...
kubernetes_namespace.confluent: Creating...
kubernetes_namespace.confluent: Creation complete after 1s [id=confluent]
azurerm_role_assignment.aks_acr_pull: Still creating... [10s elapsed]
azurerm_role_assignment.aks_acr_pull: Still creating... [20s elapsed]
azurerm_role_assignment.aks_acr_pull: Creation complete after 24s [id=/subscriptions/

Apply complete! Resources: 9 added, 0 changed, 0 destroyed.

Outputs:

acr_login_server = "acrdevwesteuropevw.azurecr.io"
aks_api_server_url = <sensitive>
aks_kubeconfig = <sensitive>
aks_name = "aks-dev-westeurope-vw"
client_certificate = <sensitive>
resource_group_name = "rg-dev-westeurope-vw"
storage_account_name = "devwesteuropevw"
storage_primary_access_key = <sensitive>

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>
```
Then verified the created resources in Azure CLI:

```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>terraform output resource_group_name
"rg-dev-westeurope-vw"

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>az resource list --resource-group rg-dev-westeurope-vw --output table
Name                   ResourceGroup         Location    Type                                        Status
---------------------  --------------------  ----------  ------------------------------------------  --------
       rg-  westeurope  Microsoft.Storage/storageAccounts
  rg-  westeurope  Microsoft.ContainerService/managedClusters
     rg- westeurope  Microsoft.ContainerRegistry/registries
```

Also from the GUI:

![new_rgs_gui](https://github.com/user-attachments/assets/857b0a8d-a2f5-427b-8718-bf3eb6240f08)

Then I headed to the Retrieve kubeconfig.yaml and Set It as Default steps, which contains so many sensitive informations, that I will display only franctions of it.
I extracted kubeconfig.yaml from the directory /terraform:

First I needed to recieve the current <AKS_NAME>, with command:
 ```python terraform output -raw aks_name ```

Then I needed to get <RESOURCE_GROUP_NAME_CREATED_BY_TERRAFORM>,with command:
```python terraform output resource_group_name ```

Next step was to set kubeconfig.yaml as Default for kubectl in Current Terminal Session:
```python az aks get-credentials --resource-group <RESOURCE_GROUP_NAME_CREATED_BY_TERRAFORM> --name <AKS_NAME> ```

Then switched to the project kubernetes namespace:
```python kubectl config set-context --current --namespace confluent ```

Verifed Kubernetes Cluster Connectivity:

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>kubectl get nodes
```python
NAME                              STATUS   ROLES    AGE   VERSION
aks--vmss   Ready    <none>   13h   v1.30.10
```
Then installed Confluent for Kubernetes:
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>helm repo add confluentinc https://packages.confluent.io/helm
"confluentinc" has been added to your repositories

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "confluentinc" chart repository
Update Complete. ⎈Happy Helming!⎈
```
Installed Confluent for Kubernetes:

```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>helm upgrade --install confluent-operator confluentinc/confluent-for-kubernetes
Release "confluent-operator" does not exist. Installing it now.
NAME: confluent-operator
LAST DEPLOYED: Sun Apr 13 10:34:14 2025
NAMESPACE: confluent
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
The Confluent Operator

The Confluent Operator brings the component (Confluent Services) specific controllers for kubernetes by providing components specific Custom Resource
Definition (CRD) as well as managing other Confluent Platform services
```

### Configure and Use Azure Container Registry (ACR)
Azure Container Registry (ACR) is used to store container images before deploying them to AKS.

Got the <ACR_NAME> run the following command:
```python terraform output acr_login_server ```

Authenticated with ACR.
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>az acr login --name acr.azurecr.io
The login server endpoint suffix '.azurecr.io' is automatically omitted.
Login Succeeded
```
### Build and push azure-connector into ACR
Navigated into folder connectors/, dind't modify the docker file.
Then started the docker image building with command:
```python docker build -t <ACR_NAME>/azure-connector:latest . ```

```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\connectors>docker build -t ar.io/azure-connector:latest .
[+] Building 404.1s (7/7) FINISHED                                                                                                                                                          docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                        0.1s
 => => transferring dockerfile: 305B                                                                                                                                                                        0.0s
 => [internal] load metadata for docker.io/confluentinc/cp-server-connect:7.8.1                                                                                                                             2.4s
 => [internal] load .dockerignore                                                                                                                                                                           0.1s
 => => transferring context: 2B                                                                                                                                                                             0.0s
 => [1/3] FROM docker.io/confluentinc/cp-server-connect:7.8.1@sha256:4e979451cb241d7f7c42ca3c525c7d64de89cfae736866a0cffdd15e2e1f0771                                                                     367.6s
 => => resolve docker.io/confluentinc/cp-server-connect:7.8.1@sha256:4e979451cb241d7f7c42ca3c525c7d64de89cfae736866a0cffdd15e2e1f0771                                                                       0.1s
 => => sha256:336371b9729357846d5bfddfe20ffea467a48b6c7a08b58e9e942d5208fdc4dc 2.80kB / 2.80kB                                                                                                              0.5s
 => => sha256:2b2d929716aac24d9218f33a5f7eefbaac75095f5bb9241d229acf99076efc31 824.94MB / 824.94MB                                                                                                        261.0s
 => => sha256:ee7b8ffc4e419868ca34fead8b96f0c2650af221bdc00c91880ff849481a51d4 3.68kB / 3.68kB                                                                                                              1.2s
 => => sha256:2cc7ca19c613a064c8a0819dd40a2a0bce9ad4b1581725fdddcaf033f137904e 1.30GB / 1.30GB                                                                                                            339.1s
 => => sha256:2f0f985c5c23d229639da95b5a9939cce3381d19fd07396fe5bcdfbfdee9d336 230.63kB / 230.63kB                                                                                                          0.6s
 => => sha256:94e1268754549008e561b35771c9a88c305e70de53860bb5d67f967ab516104e 172B / 172B                                                                                                                  0.3s
 => => sha256:68ceef9da5a7682e54435d6e435ebbf33a70a74866bb98ca425369389fc13e4d 98B / 98B                                                                                                                    0.5s
 => => sha256:cb8946e92e4ab58e9a63612df4d8f391f3805b7b5a6b4dd4a2bab5f4fff9909f 852B / 852B                                                                                                                  0.5s
 => => sha256:bb6547389ecb4fa892b1a143bc6c466e8673edf27a74ce22e19300fb44bd15eb 1.11kB / 1.11kB                                                                                                              0.5s
 => => sha256:67456fbe3f6a7650de1a7c735f64debea796bb56693c170f1d0b7275dd8c909b 4.66kB / 4.66kB                                                                                                              0.7s
 => => sha256:5a94f3d6b236fbdb13be7c372f8bbbe3400dd6862609d19811030f5793905c73 43.63MB / 43.63MB                                                                                                           23.3s
 => => sha256:86718234a593b8ad5c9c62b29e754caa1d7fe0bf8ee9d7eafefaacc01ba80fd8 21.39kB / 21.39kB                                                                                                            0.9s
 => => sha256:74af2f65710b4faaf30fd441be924486082bb7c2e1c0200e4019afcf59b788a4 8.68MB / 8.68MB                                                                                                              4.6s
 => => sha256:48194843822a5013a9d9eb3949635f5d7edfe9490165d6b225e19bb4b421d327 1.10kB / 1.10kB                                                                                                              0.5s
 => => sha256:65685005b2b1e0ec8f555e02e2435dc1deecc821767c13d3015911502d95b0eb 276B / 276B                                                                                                                  0.6s
 => => extracting sha256:65685005b2b1e0ec8f555e02e2435dc1deecc821767c13d3015911502d95b0eb                                                                                                                   0.1s
 => => sha256:8efbca1eae4bf33d69bd819ca7afe2211e6a22728a01c36f78394dda0ed97689 373.47MB / 373.47MB                                                                                                        120.5s
 => => extracting sha256:8efbca1eae4bf33d69bd819ca7afe2211e6a22728a01c36f78394dda0ed97689                                                                                                                  60.0s
 => => extracting sha256:48194843822a5013a9d9eb3949635f5d7edfe9490165d6b225e19bb4b421d327                                                                                                                   0.1s
 => => extracting sha256:74af2f65710b4faaf30fd441be924486082bb7c2e1c0200e4019afcf59b788a4                                                                                                                   0.5s
 => => extracting sha256:86718234a593b8ad5c9c62b29e754caa1d7fe0bf8ee9d7eafefaacc01ba80fd8                                                                                                                   0.1s
 => => extracting sha256:5a94f3d6b236fbdb13be7c372f8bbbe3400dd6862609d19811030f5793905c73                                                                                                                   2.2s
 => => extracting sha256:67456fbe3f6a7650de1a7c735f64debea796bb56693c170f1d0b7275dd8c909b                                                                                                                   0.1s
 => => extracting sha256:bb6547389ecb4fa892b1a143bc6c466e8673edf27a74ce22e19300fb44bd15eb                                                                                                                   0.1s
 => => extracting sha256:cb8946e92e4ab58e9a63612df4d8f391f3805b7b5a6b4dd4a2bab5f4fff9909f                                                                                                                   0.1s
 => => extracting sha256:68ceef9da5a7682e54435d6e435ebbf33a70a74866bb98ca425369389fc13e4d                                                                                                                   0.2s
 => => extracting sha256:94e1268754549008e561b35771c9a88c305e70de53860bb5d67f967ab516104e                                                                                                                   0.1s
 => => extracting sha256:2f0f985c5c23d229639da95b5a9939cce3381d19fd07396fe5bcdfbfdee9d336                                                                                                                   0.2s
 => => extracting sha256:2cc7ca19c613a064c8a0819dd40a2a0bce9ad4b1581725fdddcaf033f137904e                                                                                                                  19.0s
 => => extracting sha256:ee7b8ffc4e419868ca34fead8b96f0c2650af221bdc00c91880ff849481a51d4                                                                                                                   0.0s
 => => extracting sha256:2b2d929716aac24d9218f33a5f7eefbaac75095f5bb9241d229acf99076efc31                                                                                                                   8.7s
 => => extracting sha256:336371b9729357846d5bfddfe20ffea467a48b6c7a08b58e9e942d5208fdc4dc                                                                                                                   0.0s
 => [2/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage:1.6.24                                                                                                       13.2s
 => [3/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage-source:2.6.10                                                                                                10.0s
 => exporting to image                                                                                                                                                                                     10.2s
 => => exporting layers                                                                                                                                                                                     7.3s
 => => exporting manifest sha256:0060d95f1b49967bdf8de1d1d0de6b5f89b6948ac6bc14d5fa22c43a36ffa043                                                                                                           0.0s
 => => exporting config sha256:dd79205add1788ab50616652a228a8ffb4ff860f87dc5654e4171f347ff729bf                                                                                                             0.0s
 => => exporting attestation manifest sha256:ae025f67039e2ecc634e520f8326be4d58224a05c3f6af39c6cb91adba485f9f                                                                                               0.1s
 => => exporting manifest list sha256:b8140cc2b0a46ee02f7ff7022b9876e38c9f68b9a97b7b66d79a2d1f41948161                                                                                                      0.0s
 => => naming to acr.azurecr.io/azure-connector:latest                                                                                                                                       0.0s
 => => unpacking to acr.azurecr.io/azure-connector:latest                                                                                                                                    2.6s
```

Then pushed the image to the ACR:
```python

```

Finally verified the image in ACR:
```python

```

### Install Confluent Platform

Navigated into root folder. Modifed the file confluent-platform.yaml and replaced the placeholder with actual value.
Installed all Confluent Platform components:
```python

```

Installed a sample producer app and topic:
```python

```

Checked that everything is deployed (all pods should be in the Running state and have a ready status of 1/1):
It took approximately 15–20 minutes to set up all resources.

### View Control Center

Set up port forwarding to Control Center web UI from local machine:

### Create a kafka topic
The topic should had at least 3 partitions because the azure blob storage had 3 partitions. Named the new topic: expedia.

Created a connection for kafka:

Executed below command to create Kafka topic with a name expedia:

### Upload the data files into Azure Conatainers






