# Terraform Network Module

This module sets up a new VPC Network in GCP by defining your network and subnet ranges in a concise syntax. This is not likely to change much over time

It creates:

- A Google Virtual Private Network (VPC)
- Subnets within the VPC
- Secondary ranges for the subnets (if applicable)

## Compatibility

This module is meant for use with Terraform 0.12 and higher

## Usage
Usage of this module once again will be rare and likely you will need the outputs from this module:

```hcl
module "vpc" {
    source  = "../path/to/this/directory"
    version = "~> 1.0.0"

    project_id   = "<PROJECT ID>"
    network_name = "pulibrary-gcdc-vpc"
    routing_mode = "GLOBAL"

    subnets = [
        {
            subnet_name           = "subnet-01"
            subnet_ip             = "10.10.10.0/24"
            subnet_region         = "us-east1"
        },
        {
            subnet_name           = "subnet-02"
            subnet_ip             = "10.10.20.0/24"
            subnet_region         = "us-west1"
            subnet_private_access = "true"
            subnet_flow_logs      = "true"
            description           = "This subnet has a description"
        },
    ]

    secondary_ranges = {
        subnet-01 = [
            {
                range_name    = "subnet-01-secondary-01"
                ip_cidr_range = "192.168.64.0/24"
            },
        ]

        subnet-02 = []
    }

    routes = [
        {
            name                   = "egress-internet"
            description            = "route through IGW to access internet"
            destination_range      = "0.0.0.0/0"
            tags                   = "egress-inet"
            next_hop_internet      = "true"
        },
        {
            name                   = "app-proxy"
            description            = "route through proxy to reach app"
            destination_range      = "10.50.10.0/24"
            tags                   = "pulibrary-gcdc"
            next_hop_instance      = "app-proxy-instance"
            next_hop_instance_zone = "us-east1-a"
        },
    ]
}
```

Perform the following commands on the root folder containing the example above:

- `terraform init` to get the plugins
- `terraform plan` to see the infrastructure plan
- `terraform apply` to apply the infrastructure build
- `terraform destroy` to destroy the built infrastructure

