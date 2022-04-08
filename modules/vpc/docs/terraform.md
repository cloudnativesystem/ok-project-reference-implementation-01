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

