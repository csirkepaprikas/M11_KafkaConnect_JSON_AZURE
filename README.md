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



