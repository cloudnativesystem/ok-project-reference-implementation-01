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

