## Description
- Creates an EC2 AWS instance with Terraform

### Reference
- https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build

### Dependencies
- Valid AWS Account
- Install AWS CLI
- Install Terraform
- Install HashiCorp Terraform VSCode Extension


### 1. Creating an AWS EC2 Instance

#### Set your AWS keys
`export AWS_ACCESS_KEY_ID=`

`export AWS_SECRET_ACCESS_KEY=`

#### Download terraform modules to connect to AWS
`terraform init`

#### Check terraform execution plan steps
`terraform plan` (needs AWS keys)

##### Example of an expected output

```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.app_server will be created
  + resource "aws_instance" "app_server" {
      + ami                                  = "ami-008fe2fc65df48dac"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t2.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + "Name" = "TerraformFirstServerInstance"
        }
      + tags_all                             = {
          + "Name" = "TerraformFirstServerInstance"
        }
      + tenancy                              = (known after apply)
      + user_data                            = (known after apply)
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

#### Create Infrastructure EC2 Instance with Terraform
`terraform apply`

This step creates: terraform.tfstate
The Terraform state file is the only way Terraform can track which resources it manages, and often contains sensitive information, so you must store your state file securely and restrict access to only trusted team members who need to manage your infrastructure.


### 2. Connecting to EC2 Instance via SSH

- Create SSH keys on AWS (in this example: "your_pem_file_name")
- Give SSH permissions
- Download your .pem file

- Recreate the instance
`terraform apply`

- Handle permissions
`chmod 400 "$your_pem_file_name.pem"`

- Connect to AWS EC2 Instance
`ssh -i "$your_pem_file_name.pem" ubuntu@$your_instance_open_DNS`
