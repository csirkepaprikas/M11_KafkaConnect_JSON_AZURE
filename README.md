# Module 2: Kafka Connect
### Balázs Mikes

#### github link:
https://github.com/csirkepaprikas/M11_KafkaConnect_JSON_AZURE.git

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
random_string.suffix: Creation complete after 0s [id=]
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
azurerm_storage_data_lake_gen2_filesystem.gen2_data: Creation complete after 1s [id=https://dedfs.core.windows.net/data]
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
azurerm_kubernetes_cluster.bdcc: Creation complete after 2m59s [id=/subscriptions
azurerm_role_assignment._acr_pull: Creating...
kubernetes_namespace.confluent: Creating...
kubernetes_namespace.confluent: Creation complete after 1s [id=confluent]
azurerm_role_assignment.aks_acr_pull: Still creating... [10s elapsed]
azurerm_role_assignment.aks_acr_pull: Still creating... [20s elapsed]
azurerm_role_assignment.aks_acr_pull: Creation complete after 24s [id=/subscriptions/

Apply complete! Resources: 9 added, 0 changed, 0 destroyed.

Outputs:

acr_login_server = ".azurecr.io"
aks_api_server_url = <sensitive>
aks_kubeconfig = <sensitive>
aks_name = "aks"
client_certificate = <sensitive>
resource_group_name = "rg-dev"
storage_account_name = "de"
storage_primary_access_key = <sensitive>

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>
```
Then verified the created resources in Azure CLI:

```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>terraform output resource_group_name
"r"

c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\terraform>az resource list --resource-group rg --output table
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
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\connectors>docker push acr.azurecr.io/azure-connector
Using default tag: latest
The push refers to repository [acr.azurecr.io/azure-connector]
29118dc2a558: Pushed
68ceef9da5a7: Pushed
86718234a593: Pushed
67456fbe3f6a: Pushed
bb6547389ecb: Pushed
cb8946e92e4a: Pushed
ee7b8ffc4e41: Pushed
4fe015fb031e: Pushed
74af2f65710b: Pushed
94e126875454: Pushed
2f0f985c5c23: Pushed
2cc7ca19c613: Pushed
65685005b2b1: Pushed
5a94f3d6b236: Pushed
48194843822a: Pushed
336371b97293: Pushed
8efbca1eae4b: Pushed
16ea687fd8de: Pushed
0c03fc0a30d2: Pushed
2b2d929716aa: Pushed
latest: digest: sha256:b8140cc2b0a46ee02f7ff7022b9876e38c9f68b9a97b7b66d79a2d1f41948161 size: 856
```

Finally verified the image in ACR:
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master\connectors>az acr repository list --name acr.azurecr.io --output table
The login server endpoint suffix '.azurecr.io' is automatically omitted.
Result
---------------
azure-connector
```

### Install Confluent Platform

Navigated into root folder. Modifed the file confluent-platform.yaml and replaced the placeholder with actual value.
Installed all Confluent Platform components:
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master>kubectl apply -f confluent-platform.yaml
zookeeper.platform.confluent.io/zookeeper created
kafka.platform.confluent.io/kafka created
connect.platform.confluent.io/connect created
ksqldb.platform.confluent.io/ksqldb created
controlcenter.platform.confluent.io/controlcenter created
schemaregistry.platform.confluent.io/schemaregistry created
```

Installed a sample producer app and topic:
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master>kubectl apply -f producer-app-data.yaml
secret/kafka-client-config created
statefulset.apps/elastic created
service/elastic created
kafkatopic.platform.confluent.io/elastic-0 created
```

Checked that everything is deployed (all pods should be in the Running state and have a ready status of 1/1):
It took approximately 10 minutes to set up all resources.
```python
c:\data_eng\házi\5\m11_kafkaconnect_json_azure-master>kubectl get pods -o wide
NAME                                  READY   STATUS    RESTARTS      AGE   IP             NODE                              NOMINATED NODE   READINESS GATES
confluent-operator-7bc56ff8bf-8pxcr   1/1     Running   0             10h   10.244.0.230   aks-default-17594787-vmss000000   <none>           <none>
connect-0                             1/1     Running   0             10h   10.244.0.72    aks-default-17594787-vmss000000   <none>           <none>
controlcenter-0                       1/1     Running   1 (16m ago)   10h   10.244.0.152   aks-default-17594787-vmss000000   <none>           <none>
elastic-0                             1/1     Running   0             10h   10.244.0.192   aks-default-17594787-vmss000000   <none>           <none>
kafka-0                               1/1     Running   1 (17m ago)   10h   10.244.0.237   aks-default-17594787-vmss000000   <none>           <none>
kafka-1                               1/1     Running   1 (17m ago)   10h   10.244.0.153   aks-default-17594787-vmss000000   <none>           <none>
kafka-2                               1/1     Running   1 (17m ago)   10h   10.244.0.44    aks-default-17594787-vmss000000   <none>           <none>
ksqldb-0                              1/1     Running   1 (17m ago)   10h   10.244.0.198   aks-default-17594787-vmss000000   <none>           <none>
schemaregistry-0                      1/1     Running   1 (17m ago)   10h   10.244.0.199   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-0                           1/1     Running   0             10h   10.244.0.190   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-1                           1/1     Running   0             10h   10.244.0.216   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-2                           1/1     Running   0             10h   10.244.0.156   aks-default-17594787-vmss000000   <none>           <none>
```
### View Control Center

Set up port forwarding to Control Center web UI from local machine:
```python Start-Process powershell -WindowStyle Hidden -ArgumentList 'kubectl port-forward controlcenter-0 9021:9021 *> $null' ```

![contcent](https://github.com/user-attachments/assets/84c83696-fc9e-4441-b368-b66e3007a6f9)

### Create a kafka topic
The topic should had at least 3 partitions because the azure blob storage had 3 partitions. Named the new topic: expedia.

Created a connection for kafka:
```python Start-Process powershell -WindowStyle Hidden -ArgumentList 'kubectl port-forward connect-0 8083:8083 *> $null' ```

Executed below command to create Kafka topic with a name expedia:
```python
PS C:\WINDOWS\system32>
>> kubectl exec kafka-0 -c kafka -- bash -c "/usr/bin/kafka-topics --create --topic expedia --replication-factor 3 --partitions 3 --bootstrap-server kafka:9092"
Created topic expedia.
```
### Upload the data files into Azure Conatainers

I created them according the instruction, preserving the original directory structure:

![exp_dire](https://github.com/user-attachments/assets/fba08303-8c55-436c-a6cc-341b78dfbe9c)

![cont_part_dire](https://github.com/user-attachments/assets/97650989-b533-4ec6-ba5b-2a42ad529212)


### Prepare the azure connector configuration file

Modified the file /terraform/azure-source-cc.json.

Before the data uploading I had to mask time from the date field using MaskField transformer like: 2015-08-18 12:37:10 -> 0000-00-00 00:00:00.

For this I printed out the name of the columns and also the first 5 rows, to check the structure of the data.
For this purpose I used the python code below:
```python
from fastavro import reader


def read_avro_file(file_path):
    with open(file_path, 'rb') as f:
        avro_reader = reader(f)

        # Oszlopnevek kiolvasása a schema alapján
        schema_fields = avro_reader.schema['fields']
        column_names = [field['name'] for field in schema_fields]

        print("columns:")
        for name in column_names:
            print(f"- {name}")

        print("\nfirst 5 rows:")
        for i, record in enumerate(avro_reader):
            print(record)
            if i == 4:
                break


avro_file_path = "c:/data_eng/házi/5/m11kafkaconnect/topics/expedia/partition=1/expedia+1+0000000000.avro"
read_avro_file(avro_file_path)
```
The output was:
```python
columns:
- id
- date_time
- site_name
- posa_container
- user_location_country
- user_location_region
- user_location_city
- orig_destination_distance
- user_id
- is_mobile
- is_package
- channel
- srch_ci
- srch_co
- srch_adults_cnt
- srch_children_cnt
- srch_rm_cnt
- srch_destination_id
- srch_destination_type_id
- hotel_id

first 5 rows:
{'id': 2182172, 'date_time': '2015-09-22 15:22:02', 'site_name': 2, 'posa_container': None, 'user_location_country': 66, 'user_location_region': 226, 'user_location_city': 45115, 'orig_destination_distance': 2144.2684, 'user_id': 46170, 'is_mobile': 0, 'is_package': 0, 'channel': 10, 'srch_ci': '2017-08-07', 'srch_co': '2017-08-11', 'srch_adults_cnt': 2, 'srch_children_cnt': 1, 'srch_rm_cnt': 1, 'srch_destination_id': 12826, 'srch_destination_type_id': 5, 'hotel_id': 2156073582601}
{'id': 2182202, 'date_time': '2015-02-10 13:11:46', 'site_name': 2, 'posa_container': None, 'user_location_country': 66, 'user_location_region': 442, 'user_location_city': 9891, 'orig_destination_distance': 628.387, 'user_id': 46266, 'is_mobile': 1, 'is_package': 0, 'channel': 9, 'srch_ci': '2017-08-10', 'srch_co': '2017-08-12', 'srch_adults_cnt': 1, 'srch_children_cnt': 0, 'srch_rm_cnt': 1, 'srch_destination_id': 27725, 'srch_destination_type_id': 6, 'hotel_id': 137438953474}
{'id': 2182216, 'date_time': '2015-10-23 15:51:49', 'site_name': 2, 'posa_container': None, 'user_location_country': 66, 'user_location_region': 462, 'user_location_city': 27117, 'orig_destination_distance': 145.4714, 'user_id': 46355, 'is_mobile': 0, 'is_package': 0, 'channel': 10, 'srch_ci': '2017-08-24', 'srch_co': '2017-08-25', 'srch_adults_cnt': 4, 'srch_children_cnt': 0, 'srch_rm_cnt': 1, 'srch_destination_id': 23545, 'srch_destination_type_id': 6, 'hotel_id': 2173253451781}
{'id': 2182238, 'date_time': '2015-05-06 05:41:13', 'site_name': 34, 'posa_container': None, 'user_location_country': 205, 'user_location_region': 385, 'user_location_city': 46963, 'orig_destination_distance': 327.4224, 'user_id': 46472, 'is_mobile': 0, 'is_package': 0, 'channel': 10, 'srch_ci': '2016-10-27', 'srch_co': '2016-10-31', 'srch_adults_cnt': 2, 'srch_children_cnt': 0, 'srch_rm_cnt': 1, 'srch_destination_id': 8267, 'srch_destination_type_id': 1, 'hotel_id': 2473901162497}
{'id': 2182270, 'date_time': '2015-11-01 08:09:41', 'site_name': 2, 'posa_container': None, 'user_location_country': 66, 'user_location_region': 258, 'user_location_city': 6176, 'orig_destination_distance': 1718.7233, 'user_id': 46599, 'is_mobile': 0, 'is_package': 1, 'channel': 10, 'srch_ci': '2017-08-24', 'srch_co': '2017-08-28', 'srch_adults_cnt': 2, 'srch_children_cnt': 2, 'srch_rm_cnt': 1, 'srch_destination_id': 8254, 'srch_destination_type_id': 1, 'hotel_id': 1941325217794}

Process finished with exit code 0
```
From the output it was clear, that I had to mask the second, "date_time" column.

At this point I learned the name what to mask, so I modified the json according to that (sensitive information were deleted):
```python
{
"name": "expedia",
  "config": {
    "topics": "expedia",
    "bootstrap.servers": "kafka:9071",
    "connector.class": "io.confluent.connect.azure.blob.storage.AzureBlobStorageSourceConnector",
    "tasks.max": "2",
    "topics.dir": "root",
    "format.class": "io.confluent.connect.azure.blob.storage.format.avro.AvroFormat",
    "azblob.account.name": "dev",
    "azblob.account.key": "",
    "azblob.container.name": "data",
    "azblob.retry.retries": "3",
    "transforms": "mask_date",
    "transforms.mask_date.type": "org.apache.kafka.connect.transforms.MaskField$Value",
    "transforms.mask_date.fields": "date_time",
    "transforms.mask_date.replacement": "0000-00-00 00:00:00"
  }
}
```

### Upload the connector file through the API

Went into folder terraform, and run a command:
```python Remove-item alias:curl ```
Then the next one to upload the connector: 
```python
>> curl -s -X POST -H "Content-Type:application/json" --data @azure-source-cc.json http://localhost:8083/connectors
{"name":"expedia","config":{"topics":"expedia","bootstrap.servers":"kafka:9071","connector.class":"io.confluent.connect.azure.blob.storage.AzureBlobStorageSourceConnector","tasks.max":"2","topics.dir":"root","format.class":"io.confluent.connect.azure.blob.storage.format.avro.AvroFormat","azblob.account.name":"dev","azblob.account.key":"","azblob.container.name":"data","azblob.retry.retries":"3","transforms":"mask_date","transforms.mask_date.type":"org.apache.kafka.connect.transforms.MaskField$Value","transforms.mask_date.fields":"date_time","transforms.mask_date.replacement":"0000-00-00 00:00:00","name":"expedia"},"tasks":[],"type":"source"}
```

### Verify the messages in Kafka

Browsed the Control Center on http://localhost:9021 and navigated to the Topics, chose the named "expedia" and checked the incoming messages:

![inc_messages](https://github.com/user-attachments/assets/612feb65-e64f-4492-932f-122812818455)

Then an actual message:
```python
{
  "id": 649959,
  "date_time": "0000-00-00 00:00:00",
  "site_name": 34,
  "posa_container": null,
  "user_location_country": 205,
  "user_location_region": 354,
  "user_location_city": 33452,
  "orig_destination_distance": 340.937,
  "user_id": 960741,
  "is_mobile": 0,
  "is_package": 0,
  "channel": 9,
  "srch_ci": "2017-08-18",
  "srch_co": "2017-08-19",
  "srch_adults_cnt": 5,
  "srch_children_cnt": 0,
  "srch_rm_cnt": 3,
  "srch_destination_id": 8233,
  "srch_destination_type_id": 1,
  "hotel_id": 1082331758594
}
```
As You can see the "date_time" column was successfully masked.

## CI/CD

I chose the approach to write all the steps in a Makefile, then run them one-by-one in PowerShell. I also created a secrets.env file, where are the sensitive files are stored.
Below you can see the content of the Makefile:
```python
# Makefile
include secrets.env
export


IMAGE_NAME = azure-connector
TAG = latest
FULL_IMAGE = $(ACR_NAME).azurecr.io/$(IMAGE_NAME):$(TAG)
CONTAINER = data

upload-dir:
	az storage blob upload-batch \
		--account-name $(STORAGE_ACCOUNT) \
		--destination $(CONTAINER) \
		--source . \
		--pattern "root_cicd/*"




# Build image
build:
	docker build -t $(FULL_IMAGE) .

# Login to Azure and ACR
login:
	az acr login --name $(ACR_NAME)

# Push image to ACR
push: build login
	docker push $(FULL_IMAGE)



# YAML files' path
CONFLUENT_YAML = k8s/confluent-platform.yaml
PRODUCER_YAML = k8s/producer-app-data.yaml


# Confluent deployment
deploy-confluent:
	kubectl apply -f $(CONFLUENT_YAML)

# Producer-app deployment
deploy-producer:
	kubectl apply -f $(PRODUCER_YAML)	

# Confluent deletion
delete-confluent:
	kubectl delete -f $(CONFLUENT_YAML) 

# Producer-app deletion
delete-producer:
	kubectl delete -f $(PRODUCER_YAML)	
	
# Status verification
status:
	kubectl get pods -o wide  
	
	
# 1. Port forward Control Center
port-forward-controlcenter:
	powershell -Command "Start-Process powershell -ArgumentList 'kubectl port-forward controlcenter-0 9021:9021 *> \$null'"

# 2. Port forward Kafka Connect
port-forward-connect:
	powershell -Command "Start-Process powershell -ArgumentList 'kubectl port-forward connect-0 8083:8083 *> \$null'"

# 3. Kafka topic creation (expedia)
create-topic:
	kubectl exec kafka-0 -c kafka -- bash -c "/usr/bin/kafka-topics --create --topic expedia --replication-factor 3 --partitions 3 --bootstrap-server kafka:9092"

# 4. Delete alias
fix-curl:
	Remove-Item alias:curl -Force

# 5. Kafka Connect connector upload from JSON file
upload-connector:
	powershell -Command "Invoke-RestMethod -Method Post -Uri http://localhost:8083/connectors -ContentType 'application/json' -Body (Get-Content -Raw -Path azure-source-cc.json)"
```

I deleted/masked the sensitive informations in the outputs/screenshots.

### upload-dir:
This target uploads the connectors data.
```python
PS C:\data_eng\házi\5\ci_cd> make upload-dir
az storage blob upload-batch \
        --account-name  \
        --destination data \
        --source . \
        --pattern "root_cicd/*"

There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://learn.microsoft.com/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.
Finished[#############################################################]  100.0000%
[
  {
    "Blob": "https://d.blob.core.windows.net/data/root_cicd/topics/expedia/partition%3D0/expedia%2B0%2B0000000000.avro",
    "Last Modified": "2025-04-16T11:25:50+00:00",
    "Type": null,
    "eTag": "\"0x8DD7CD97101603C\""
  },
  {
    "Blob": "https://d.blob.core.windows.net/data/root_cicd/topics/expedia/partition%3D1/expedia%2B1%2B0000000000.avro",
    "Last Modified": "2025-04-16T11:26:23+00:00",
    "Type": null,
    "eTag": "\"0x8DD7CD984C51FC4\""
  },
  {
    "Blob": "https://d.blob.core.windows.net/data/root_cicd/topics/expedia/partition%3D2/expedia%2B2%2B0000000000.avro",
    "Last Modified": "2025-04-16T11:27:05+00:00",
    "Type": null,
    "eTag": "\"0x8DD7CD99E0BEBF8\""
  }
]
```

![ci_datas](https://github.com/user-attachments/assets/2c5b0b8a-6aff-4d2c-a9a5-67eae39241a6)

### build:

This target build the docker image locally:
```python
PS C:\data_eng\házi\5\ci_cd> make build
docker build -t .azurecr.io/azure-connector:latest .
[+] Building 2.4s (7/7) FINISHED                                                                                                                                                            docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                        0.1s
 => => transferring dockerfile: 306B                                                                                                                                                                        0.0s
 => [internal] load metadata for docker.io/confluentinc/cp-server-connect:7.6.0                                                                                                                             1.6s
 => [internal] load .dockerignore                                                                                                                                                                           0.1s
 => => transferring context: 2B                                                                                                                                                                             0.0s
 => [1/3] FROM docker.io/confluentinc/cp-server-connect:7.6.0@sha256:0bf9b70cc89a2dcdd9c57d2d92129dfbb012690a3323f4c4e92d1505c8c2ea4d                                                                       0.1s
 => => resolve docker.io/confluentinc/cp-server-connect:7.6.0@sha256:0bf9b70cc89a2dcdd9c57d2d92129dfbb012690a3323f4c4e92d1505c8c2ea4d                                                                       0.1s
 => CACHED [2/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage:latest                                                                                                 0.0s
 => CACHED [3/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage-source:latest                                                                                          0.0s
 => exporting to image                                                                                                                                                                                      0.3s
 => => exporting layers                                                                                                                                                                                     0.0s
 => => exporting manifest sha256:87ca0260cfdcd056f267803844e8749ad2ae16bb7d141870111626f432d97bfe                                                                                                           0.0s
 => => exporting config sha256:375d7db90c39b010366d8ee41dfd26469afd5e94c2672f4008568edf5e5ba1b5                                                                                                             0.0s
 => => exporting attestation manifest sha256:c4c69785d06f74124ac3161209b58b8b6615d3d1d51ea83edfc2ef989cd1bb11                                                                                               0.1s
 => => exporting manifest list sha256:3a597abe5935449a4e06c06aead0f515646c6ec71b376627c00279717e387690                                                                                                      0.0s
 => => naming to a.azurecr.io/azure-connector:latest                                                                                                                                 0.0s
 => => unpacking to .azurecr.io/azure-connector:latest                                                                                                                              0.0s
PS C:\data_eng\házi\5\ci_cd>
```

### login:

This target executes a login to the ACR:
```python
PS C:\data_eng\házi\5\ci_cd> make login
az acr login --name acr
Login Succeeded
PS C:\data_eng\házi\5\ci_cd>
```
### push:

This target pushes the image to the ACR:
```python
PS C:\data_eng\házi\5\ci_cd> make push
docker build -t acr.azurecr.io/azure-connector:latest .
[+] Building 1.8s (7/7) FINISHED                                                                                                                                                            docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                        0.0s
 => => transferring dockerfile: 306B                                                                                                                                                                        0.0s
 => [internal] load metadata for docker.io/confluentinc/cp-server-connect:7.6.0                                                                                                                             1.1s
 => [internal] load .dockerignore                                                                                                                                                                           0.1s
 => => transferring context: 2B                                                                                                                                                                             0.0s
 => [1/3] FROM docker.io/confluentinc/cp-server-connect:7.6.0@sha256:0bf9b70cc89a2dcdd9c57d2d92129dfbb012690a3323f4c4e92d1505c8c2ea4d                                                                       0.1s
 => => resolve docker.io/confluentinc/cp-server-connect:7.6.0@sha256:0bf9b70cc89a2dcdd9c57d2d92129dfbb012690a3323f4c4e92d1505c8c2ea4d                                                                       0.0s
 => CACHED [2/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage:latest                                                                                                 0.0s
 => CACHED [3/3] RUN confluent-hub install --no-prompt confluentinc/kafka-connect-azure-blob-storage-source:latest                                                                                          0.0s
 => exporting to image                                                                                                                                                                                      0.2s
 => => exporting layers                                                                                                                                                                                     0.0s
 => => exporting manifest sha256:87ca0260cfdcd056f267803844e8749ad2ae16bb7d141870111626f432d97bfe                                                                                                           0.0s
 => => exporting config sha256:375d7db90c39b010366d8ee41dfd26469afd5e94c2672f4008568edf5e5ba1b5                                                                                                             0.0s
 => => exporting attestation manifest sha256:80fb0097a24621dccecc954da8f426748260d4d6863a0a43dd672974b229005b                                                                                               0.1s
 => => exporting manifest list sha256:550eb178a5518760f9668b765d67fb80bc19adc5af3fe24f1311b9a6cb182a2f                                                                                                      0.0s
 => => naming to acr.azurecr.io/azure-connector:latest                                                                                                                                 0.0s
 => => unpacking to ac.azurecr.io/azure-connector:latest                                                                                                                              0.0s
az acr login --name acr
Login Succeeded
docker push acr.azurecr.io/azure-connector:latest
The push refers to repository [acr.azurecr.io/azure-connector]
ddfc5620ff70: Layer already exists
003d908e509f: Layer already exists
4250354b4fb7: Layer already exists
974e7e336459: Layer already exists
186e9837369c: Layer already exists
c4c5f447179d: Layer already exists
d389b3791c2e: Layer already exists
0e55377ebe37: Layer already exists
8fba90d6dcbd: Layer already exists
332a782c04f4: Pushed
da7039bb2113: Layer already exists
17fe3a92262f: Layer already exists
5420596c14ab: Layer already exists
fe36fc382320: Layer already exists
c24709eccb2a: Layer already exists
a266312a92ef: Layer already exists
latest: digest: sha256:550eb178a5518760f9668b765d67fb80bc19adc5af3fe24f1311b9a6cb182a2f size: 856
PS C:\data_eng\házi\5\ci_cd>
```
### deploy-confluent:

This target deploys the actual Confluent cluster on top of AKS:
```python
PS C:\data_eng\házi\5\ci_cd> make deploy-confluent
kubectl apply -f k8s/confluent-platform.yaml
zookeeper.platform.confluent.io/zookeeper created
kafka.platform.confluent.io/kafka created
connect.platform.confluent.io/connect created
ksqldb.platform.confluent.io/ksqldb created
controlcenter.platform.confluent.io/controlcenter created
schemaregistry.platform.confluent.io/schemaregistry created
```

with the make status target I can check the actual status of the cluster creation:
```python
PS C:\data_eng\házi\5\ci_cd> make status
kubectl get pods -o wide
NAME                                  READY   STATUS     RESTARTS   AGE     IP             NODE                              NOMINATED NODE   READINESS GATES
confluent-operator-7bc56ff8bf-8pxcr   1/1     Running    0          2d14h   10.244.0.230   aks-default-17594787-vmss000000   <none>           <none>
connect-0                             0/1     Running    0          19s     10.244.0.112   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-0                           0/1     Init:0/1   0          20s     <none>         aks-default-17594787-vmss000000   <none>           <none>
zookeeper-1                           0/1     Init:0/1   0          20s     <none>         aks-default-17594787-vmss000000   <none>           <none>
zookeeper-2                           0/1     Init:0/1   0          20s     <none>         aks-default-17594787-vmss000000   <none>           <none>
```

### deploy-producer

This target deploys the Producer-app on top of AKS:
```python
PS C:\data_eng\házi\5\ci_cd> make deploy-producer
kubectl apply -f k8s/producer-app-data.yaml
secret/kafka-client-config created
statefulset.apps/elastic created
service/elastic created
kafkatopic.platform.confluent.io/elastic-0 created
PS C:\data_eng\házi\5\ci_cd>
```

the cluster is up and running:
```python
PS C:\data_eng\házi\5\ci_cd> make status
kubectl get pods -o wide
NAME                                  READY   STATUS    RESTARTS   AGE     IP             NODE                              NOMINATED NODE   READINESS GATES
confluent-operator-7bc56ff8bf-8pxcr   1/1     Running   0          2d14h   10.244.0.230   aks-default-17594787-vmss000000   <none>           <none>
connect-0                             1/1     Running   0          5m47s   10.244.0.112   aks-default-17594787-vmss000000   <none>           <none>
controlcenter-0                       1/1     Running   0          3m31s   10.244.0.57    aks-default-17594787-vmss000000   <none>           <none>
elastic-0                             1/1     Running   0          3m28s   10.244.0.140   aks-default-17594787-vmss000000   <none>           <none>
kafka-0                               1/1     Running   0          4m32s   10.244.0.66    aks-default-17594787-vmss000000   <none>           <none>
kafka-1                               1/1     Running   0          4m32s   10.244.0.86    aks-default-17594787-vmss000000   <none>           <none>
kafka-2                               1/1     Running   0          4m32s   10.244.0.33    aks-default-17594787-vmss000000   <none>           <none>
ksqldb-0                              1/1     Running   0          3m31s   10.244.0.45    aks-default-17594787-vmss000000   <none>           <none>
schemaregistry-0                      1/1     Running   0          3m30s   10.244.0.237   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-0                           1/1     Running   0          5m48s   10.244.0.190   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-1                           1/1     Running   0          5m48s   10.244.0.135   aks-default-17594787-vmss000000   <none>           <none>
zookeeper-2                           1/1     Running   0          5m48s   10.244.0.77    aks-default-17594787-vmss000000   <none>           <none>
```

### port-forward-controlcenter:

This target port forwarding to Control Center web UI from local machine:

```python powershell -Command "Start-Process powershell -ArgumentList 'kubectl port-forward controlcenter-0 9021:9021 *> \$null'" ```

![ci_gui](https://github.com/user-attachments/assets/d15a92ab-dc7f-4665-a1d8-b7f3c3021a06)

### Port forward Kafka Connect

This target port forwarding the topic:

```python Start-Process powershell -WindowStyle Hidden -ArgumentList 'kubectl port-forward connect-0 8083:8083 *> $null' ```

### create-topic:

This target create Kafka topic with a name expedia.
```python
PS C:\data_eng\házi\5\ci_cd> make create-topic
kubectl exec kafka-0 -c kafka -- bash -c "/usr/bin/kafka-topics --create --topic expedia --replication-factor 3 --partitions 3 --bootstrap-server kafka:9092"
Created topic expedia.
PS C:\data_eng\házi\5\ci_cd>
```

### fix-curl:

This target removes the alias (It was already deleted, so there must arrive an error message):
```python
PS C:\data_eng\házi\5\ci_cd> make fix-curl
Remove-Item alias:curl -Force
process_begin: CreateProcess(NULL, Remove-Item alias:curl -Force, ...) failed.
make (e=2): A rendszer nem talßlja a megadott fßjlt.
make: *** [Makefile:76: fix-curl] Error 2
PS C:\data_eng\házi\5\ci_cd>
```

### upload-connector:

Uploading the connector file through the API:
```python
PS C:\data_eng\házi\5\ci_cd> make upload-connector
powershell -Command "Invoke-RestMethod -Method Post -Uri http://localhost:8083/connectors -ContentType 'application/json' -Body (Get-Content -Raw -Path azure-source-cc.json)"

name    config
----    ------
expedia @{topics=expedia; bootstrap.servers=kafka:9071; connector.class=io.confluent.connect.azure.blob.storage.AzureBlobSt...
```
Then I checked the messages in the GUI's expedia topic:

![ci_exp](https://github.com/user-attachments/assets/fb519410-2706-4a71-b4a7-0223dd7c26b9)

Also copied an entire message:
```python
{
  "id": 2182638,
  "date_time": "0000-00-00 00:00:00",
  "site_name": 2,
  "posa_container": null,
  "user_location_country": 66,
  "user_location_region": 448,
  "user_location_city": 18390,
  "orig_destination_distance": 899.5932,
  "user_id": 47758,
  "is_mobile": 0,
  "is_package": 0,
  "channel": 10,
  "srch_ci": "2017-08-14",
  "srch_co": "2017-08-16",
  "srch_adults_cnt": 2,
  "srch_children_cnt": 1,
  "srch_rm_cnt": 1,
  "srch_destination_id": 11373,
  "srch_destination_type_id": 1,
  "hotel_id": 42949672960
}
```



