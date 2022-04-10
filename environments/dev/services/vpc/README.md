
<!-- markdownlint-disable -->
# terraform-aws-vpc [![Latest Release](https://img.shields.io/github/release/cloudposse/terraform-aws-vpc.svg)](https://github.com/cloudposse/terraform-aws-vpc/releases/latest) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)
<!-- markdownlint-restore -->




This is a sample implementation of the terraform-aws-vpc module. All inputs to this
module are provided via the vpc.tfvars file and have been initialized with sample
values.

---

























## Examples

```hcl
# vpc_main.tf
module "vpc" {

  source = "../../modules/vpc"
  name   = var.vpc_name
  cidr   = var.vpc_cidr

  environment = var.environment
  vpc_name    = var.vpc_name

  azs             = var.vpc_azs
  private_subnets = var.vpc_private_subnets
  public_subnets  = var.vpc_public_subnets

  enable_s3_endpoint = var.enable_s3_endpoint

  tags = var.common_tags

  vpc_tags = var.vpc_tags
}
```

Initial Settings Provided Via vpc.tfvars:

```hcl
# vpc.tfvars

#
vpc_name = "onekloud-infra-dev"

#
vpc_cidr = "10.155.0.0/16"

#
vpc_azs = ["us-east-2a"]

#
vpc_private_subnets = ["10.155.0.0/18"]

#
vpc_public_subnets = ["10.155.64.0/18"]

#
enable_s3_endpoint = true

#
vpc_tags = {
  "Name" = "onekloud-infra-vpc-ddddev"
}

#
dns_private_zone_name = "development.swagwatch.io."

#
dns_public_zone_name = "development.swagwatch.io."

#
dns_reverse_zone_name = "10.155.in-addr.arpa."   
```



## Requirements

No requirements.

## Providers

No provider.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| dns\_private\_zone\_name | private\_zone | `string` | n/a | yes |
| dns\_public\_zone\_name | public\_zone | `string` | n/a | yes |
| dns\_reverse\_zone\_name | reverse\_zone | `string` | n/a | yes |
| enable\_s3\_endpoint | Determines whether or not an S3 endpoint is created | `bool` | n/a | yes |
| vpc\_azs | Availability Zones For This VPC | `list(string)` | n/a | yes |
| vpc\_cidr | CIDR Block Of This VPC | `string` | n/a | yes |
| vpc\_name | Name Of This VPC Resource | `string` | n/a | yes |
| vpc\_private\_subnets | The Private Subnets For This VPC | `list(string)` | n/a | yes |
| vpc\_public\_subnets | The Public Subnets For This VPC | `list(string)` | n/a | yes |
| vpc\_tags | Tags Specific To This Resource | `map(string)` | n/a | yes |

## Outputs

No output.












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
