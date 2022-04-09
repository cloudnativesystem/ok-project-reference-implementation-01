
<!-- markdownlint-disable -->
# terraform-aws-vpc [![Latest Release](https://img.shields.io/github/release/cloudposse/terraform-aws-vpc.svg)](https://github.com/cloudposse/terraform-aws-vpc/releases/latest) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)
<!-- markdownlint-restore -->




Terraform module to provision a VPC with Internet Gateway. Contains a submodule for provisioning Interface and/or Gateway VPC Endpoints.

---


[![Terraform Open Source Modules](https://docs.cloudposse.com/images/terraform-open-source-modules.svg)][terraform_modules]


















## Security & Compliance [<img src="https://cloudposse.com/wp-content/uploads/2020/11/bridgecrew.svg" width="250" align="right" />](https://bridgecrew.io/)

Security scanning provided by Bridgecrew.

| Benchmark | Description |
|--------|---------------|
| [![Infrastructure Security](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/general)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=INFRASTRUCTURE+SECURITY) | Infrastructure Security Compliance |
| [![CIS KUBERNETES](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/cis_kubernetes)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=CIS+KUBERNETES+V1.5) | Center for Internet Security, KUBERNETES Compliance |
| [![CIS AWS](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/cis_aws)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=CIS+AWS+V1.2) | Center for Internet Security, AWS Compliance |
| [![CIS AZURE](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/cis_azure)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=CIS+AZURE+V1.1) | Center for Internet Security, AZURE Compliance |
| [![PCI-DSS](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/pci)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=PCI-DSS+V3.2) | Payment Card Industry Data Security Standards Compliance |
| [![NIST-800-53](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/nist)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=NIST-800-53) | National Institute of Standards and Technology Compliance |
| [![ISO27001](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/iso)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=ISO27001) | Information Security Management System, ISO/IEC 27001 Compliance |
| [![SOC2](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/soc2)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=SOC2)| Service Organization Control 2 Compliance |
| [![CIS GCP](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/cis_gcp)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=CIS+GCP+V1.1) | Center for Internet Security, GCP Compliance |
| [![HIPAA](https://www.bridgecrew.cloud/badges/github/cloudposse/terraform-aws-vpc/hipaa)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=cloudposse%2Fterraform-aws-vpc&benchmark=HIPAA) | Health Insurance Portability and Accountability Compliance |







## Examples

```hcl
module "vpc" {
  source = "cloudposse/vpc/aws"
  # Cloud Posse recommends pinning every module to a specific version
  # version = "x.x.x"
  namespace  = "eg"
  stage      = "test"
  name       = "app"
  cidr_block = "10.0.0.0/16"
}
```

Full example with [`terraform-aws-dynamic-subnets`](https://github.com/cloudposse/terraform-aws-dynamic-subnets.git):

```hcl
module "vpc" {
  source = "cloudposse/vpc/aws"
  # Cloud Posse recommends pinning every module to a specific version
  # version     = "x.x.x"
  namespace  = "eg"
  stage      = "test"
  name       = "app"
  cidr_block = "10.0.0.0/16"
}

module "dynamic_subnets" {
  source = "cloudposse/dynamic-subnets/aws"
  # Cloud Posse recommends pinning every module to a specific version
  # version     = "x.x.x"
  namespace          = "eg"
  stage              = "test"
  name               = "app"
  availability_zones = ["us-west-2a","us-west-2b","us-west-2c"]
  vpc_id             = module.vpc.vpc_id
  igw_id             = module.vpc.igw_id
  cidr_block         = "10.0.0.0/16"
}
```

Submodule for provisioning VPC Endpoints:

```hcl
module "vpc_endpoints" {
  source = "cloudposse/vpc/aws//modules/vpc-endpoints"
  # Cloud Posse recommends pinning every module to a specific version
  # version     = "x.x.x"

  vpc_id = module.vpc.vpc_id

  gateway_vpc_endpoints = {
    "s3" = {
      name = "s3"
      policy = jsonencode({
        Version = "2012-10-17"
        Statement = [
          {
            Action = [
              "s3:*",
            ]
            Effect    = "Allow"
            Principal = "*"
            Resource  = "*"
          },
        ]
      })
    }
  }
  interface_vpc_endpoints = {
    "ec2" = {
      name                = "ec2"
      security_group_ids  = ["sg-12341234123412345"]
      subnet_ids          = module.dynamic_subnets.private_subnet_ids
      policy              = null
      private_dns_enabled = false
    }
  }
}
```



## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.15.0 |
| aws | >= 3.37.0 |

## Providers

| Name | Version |
|------|---------|
| aws | >= 3.37.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| azs | A list of availability zones names or ids in the region | `list(string)` | `[]` | no |
| cidr | The CIDR block for the VPC. Default value is a valid CIDR, but not acceptable by AWS and should be overridden | `string` | `"0.0.0.0/0"` | no |
| create\_vpc | Controls if VPC should be created (it affects almost all resources) | `bool` | `true` | no |
| enable\_s3\_endpoint | Should be true if you want to provision an S3 endpoint to the VPC | `bool` | `false` | no |
| environment | Environment | `string` | `""` | no |
| name | Name to be used on all the resources as identifier | `string` | `""` | no |
| private\_subnet\_suffix | Suffix to append to private subnets name | `string` | `"private"` | no |
| private\_subnets | A list of private subnets inside the VPC | `list(string)` | `[]` | no |
| public\_subnet\_suffix | Suffix to append to public subnets name | `string` | `"public"` | no |
| public\_subnets | A list of public subnets inside the VPC | `list(string)` | `[]` | no |
| s3\_endpoint\_policy | A policy to attach to the endpoint that controls access to the service. Defaults to full access | `string` | `null` | no |
| s3\_endpoint\_private\_dns\_enabled | Whether or not to associate a private hosted zone with the specified VPC for S3 interface endpoint | `bool` | `false` | no |
| s3\_endpoint\_security\_group\_ids | The ID of one or more security groups to associate with the network interface for S3 interface endpoint | `list(string)` | `[]` | no |
| s3\_endpoint\_subnet\_ids | The ID of one or more subnets in which to create a network interface for S3 interface endpoint. Only a single subnet within an AZ is supported. If omitted, private subnets will be used. | `list(string)` | `[]` | no |
| s3\_endpoint\_type | S3 VPC endpoint type. Note - S3 Interface type support is only available on AWS provider 3.10 and later | `string` | `"Gateway"` | no |
| tags | A map of tags to add to all resources | `map(string)` | `{}` | no |
| vpc\_name | Name of VPC | `string` | `""` | no |
| vpc\_tags | Additional tags for the VPC | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| cluster\_sg\_arn | cluster security group arn |
| cluster\_sg\_id | cluster security group id |
| default\_nacl\_arn | default nacl arn |
| default\_nacl\_id | default nacl id |
| default\_sg\_arn | default security group arn |
| default\_sg\_id | default security group id |
| private\_nacl\_arn | private nacl arn |
| private\_nacl\_id | private nacl id |
| private\_sg\_arn | private security group arn |
| private\_sg\_id | private security group id |
| private\_subnet\_arns | List of ARNs of private subnets |
| private\_subnets | List of IDs of private subnets |
| private\_subnets\_cidr\_blocks | List of cidr\_blocks of private subnets |
| private\_us\_east\_2a\_rt\_arn | private\_us\_east\_2a\_rt\_arn |
| private\_us\_east\_2a\_rt\_id | private\_us\_east\_2a\_rt |
| private\_us\_east\_2a\_sn | private\_us\_east\_2a\_sn |
| public\_nacl\_arn | public nacl arn |
| public\_nacl\_id | public nacl id |
| public\_sg\_arn | public security group arn |
| public\_sg\_id | public security group id |
| public\_subnet\_arns | List of ARNs of public subnets |
| public\_subnets | List of IDs of public subnets |
| public\_subnets\_cidr\_blocks | List of cidr\_blocks of public subnets |
| public\_us\_east\_2\_rt\_arn | public\_us\_east\_2\_rt |
| public\_us\_east\_2\_rt\_id | public\_us\_east\_2\_rt |
| public\_us\_east\_2a\_sn | public\_us\_east\_2a\_sn |
| vpc\_arn | The ARN of the VPC |
| vpc\_cidr\_block | The CIDR block of the VPC |
| vpc\_id | The ID of the VPC |
| vpc\_owner\_id | The ID of the AWS account that owns the VPC |












## Copyright

Copyright © 2015-2022 [Onekloud, LLC](https://onekloud.io/copyright)



## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

See [LICENSE](LICENSE) for full details.

```text
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```









## Trademarks

All other trademarks referenced herein are the property of their respective owners.





  [osterman_homepage]: https://github.com/osterman
  [osterman_avatar]: https://img.cloudposse.com/150x150/https://github.com/osterman.png
  [goruha_homepage]: https://github.com/goruha
  [goruha_avatar]: https://img.cloudposse.com/150x150/https://github.com/goruha.png
  [aknysh_homepage]: https://github.com/aknysh
  [aknysh_avatar]: https://img.cloudposse.com/150x150/https://github.com/aknysh.png
  [drama17_homepage]: https://github.com/drama17
  [drama17_avatar]: https://img.cloudposse.com/150x150/https://github.com/drama17.png
  [SweetOps_homepage]: https://github.com/SweetOps
  [SweetOps_avatar]: https://img.cloudposse.com/150x150/https://github.com/SweetOps.png
  [korenyoni_homepage]: https://github.com/korenyoni
  [korenyoni_avatar]: https://img.cloudposse.com/150x150/https://github.com/korenyoni.png
  [nitrocode_homepage]: https://github.com/nitrocode
  [nitrocode_avatar]: https://img.cloudposse.com/150x150/https://github.com/nitrocode.png

[![README Footer][readme_footer_img]][readme_footer_link]
[![Beacon][beacon]][website]

  [logo]: https://cloudposse.com/logo-300x69.svg
  [docs]: https://cpco.io/docs?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=docs
  [website]: https://cpco.io/homepage?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=website
  [github]: https://cpco.io/github?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=github
  [jobs]: https://cpco.io/jobs?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=jobs
  [hire]: https://cpco.io/hire?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=hire
  [slack]: https://cpco.io/slack?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=slack
  [linkedin]: https://cpco.io/linkedin?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=linkedin
  [twitter]: https://cpco.io/twitter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=twitter
  [testimonial]: https://cpco.io/leave-testimonial?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=testimonial
  [office_hours]: https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=office_hours
  [newsletter]: https://cpco.io/newsletter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=newsletter
  [discourse]: https://ask.sweetops.com/?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=discourse
  [email]: https://cpco.io/email?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=email
  [commercial_support]: https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=commercial_support
  [we_love_open_source]: https://cpco.io/we-love-open-source?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=we_love_open_source
  [terraform_modules]: https://cpco.io/terraform-modules?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=terraform_modules
  [readme_header_img]: https://cloudposse.com/readme/header/img
  [readme_header_link]: https://cloudposse.com/readme/header/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=readme_header_link
  [readme_footer_img]: https://cloudposse.com/readme/footer/img
  [readme_footer_link]: https://cloudposse.com/readme/footer/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=readme_footer_link
  [readme_commercial_support_img]: https://cloudposse.com/readme/commercial-support/img
  [readme_commercial_support_link]: https://cloudposse.com/readme/commercial-support/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-vpc&utm_content=readme_commercial_support_link
  [share_twitter]: https://twitter.com/intent/tweet/?text=terraform-aws-vpc&url=https://github.com/cloudposse/terraform-aws-vpc
  [share_linkedin]: https://www.linkedin.com/shareArticle?mini=true&title=terraform-aws-vpc&url=https://github.com/cloudposse/terraform-aws-vpc
  [share_reddit]: https://reddit.com/submit/?url=https://github.com/cloudposse/terraform-aws-vpc
  [share_facebook]: https://facebook.com/sharer/sharer.php?u=https://github.com/cloudposse/terraform-aws-vpc
  [share_googleplus]: https://plus.google.com/share?url=https://github.com/cloudposse/terraform-aws-vpc
  [share_email]: mailto:?subject=terraform-aws-vpc&body=https://github.com/cloudposse/terraform-aws-vpc
  [beacon]: https://ga-beacon.cloudposse.com/UA-76589703-4/cloudposse/terraform-aws-vpc?pixel&cs=github&cm=readme&an=terraform-aws-vpc
