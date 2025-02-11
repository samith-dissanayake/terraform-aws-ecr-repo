# AWS ECR Repository

Creates a basic ECR repository.

It's highly suggested to provide your own `lifecycle_policy` and `ecr_policy`.

By default, this module will create no policy to attatch to the ECR repo created.

Please see `lifecycle-policy.json` for the basic policy provided for maintaining the images kept in the repository. [AWS Documentation on Lifecycle Policies](https://docs.aws.amazon.com/AmazonECR/latest/userguide/LifecyclePolicies.html)

The default lifecycle policy included in this module will keep the last 500 images tagged or untagged.

## Terraform Versions

This module only supports Terraform 0.13. Pin module version to `~> 2.X`. Submit pull-requests to master branch.

This module only supports Terraform 0.12.  Pin module version to `~> 1.X`. Submit pull-requests to terraform012 branch.

## Usage

### Put an example usage of the module here

```hcl
module "example" {
  source = "trussworks/ecr-repo/aws"

  container_name = "example"
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 3.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_ecr_lifecycle_policy.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecr_lifecycle_policy) | resource |
| [aws_ecr_repository.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecr_repository) | resource |
| [aws_ecr_repository_policy.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecr_repository_policy) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_container_name"></a> [container\_name](#input\_container\_name) | Container name. | `string` | n/a | yes |
| <a name="input_ecr_policy"></a> [ecr\_policy](#input\_ecr\_policy) | ECR Permission Policy for external access. | `string` | `""` | no |
| <a name="input_lifecycle_policy"></a> [lifecycle\_policy](#input\_lifecycle\_policy) | ECR repository lifecycle policy document. Used to override the default policy. | `string` | `""` | no |
| <a name="input_scan_on_push"></a> [scan\_on\_push](#input\_scan\_on\_push) | Scan image on push to repo. | `bool` | `true` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Additional tags to apply. | `map(any)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Full ARN of the repository. |
| <a name="output_name"></a> [name](#output\_name) | The name of the repository. |
| <a name="output_repo_url"></a> [repo\_url](#output\_repo\_url) | The URL for the image created. |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Developer Setup

Install dependencies (macOS)

```shell
brew install pre-commit go terraform terraform-docs
pre-commit install --install-hooks
```

### Testing

[Terratest](https://github.com/gruntwork-io/terratest) is being used for
automated testing with this module. Tests in the `test` folder can be run
locally by running the following command:

```text
make test
```

Or with aws-vault:

```text
AWS_VAULT_KEYCHAIN_NAME=<NAME> aws-vault exec <PROFILE> -- make test
```
