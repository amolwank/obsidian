In Terraform, environment variables are values you set in your shell or CI/CD system that Terraform an read during execution.

Often used for credentials, configuration, or automation setting.

Help avoid hardcoding sensitive data in .tf files.

##### Two Main Types
Must start with TF_VAR_ (for variables) or TF_ (for setting).
##### Passing Terraform Variables with Environment Variables
- Format: TF_VAR_<variable_name>
```
export TF_VAR_instance_type = "t3.micro"
```
If you have variables.tf
```
variable "instance_type" {
	default = "t2.micro"
}
```

Terraform will use "t3.micro" instead of the default 

##### Advantages:
- Keeps secrets out of code.
- Easy to switch between environments in CI/CD
- Works without modifying .tf files.