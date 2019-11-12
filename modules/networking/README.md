# VPC example

This folder contains a [Terraform](https://www.terraform.io/) configuration that shows an example of how to 
use the [vpc module](../../modules/networking/vpc) to create a vpc
([VPC](https://cloud.google.com/vpc/)) in a [Google Cloud (GC) 
account](http://cloud.google.com/). 

## Pre-requisites

* You must have [Terraform](https://www.terraform.io/) installed on your computer. 
* You must have a [Google Cloud account](http://cloud.google.com/).

Please note that this code was written for Terraform 0.12.x.

## Quick start

**Please note that this example will deploy real resources into your Google Cloud account.**

Deploy the code:

```
terraform init
terraform apply
```

Clean up when you're done:

```
terraform destroy
```
