Mine:
Terraform make use of variables to make configuration dynamic and reusable.

Types of Variables:
Input variables -> Accepts values from Users, CLI and files.
example:
```
variable "region" {
	type = "string"
	 default = "us-east-1"
	 description = "Value of region" 	

}

Usage:
provider "aws" {
	region = var.region
}
```

**Output variables** -> Show useful information after apply
```
output "public_ip" {
	value = aws_instance.my_ec2.public_ip
}
```


**local variables (locals):**
In Terraform, a local variable is used to define values that you want to reuse in module but don't want to expose as input variables.

Environment variables




#### Ways to Assign Input Variables

|**Method**|**Command / Usage**|
|---|---|
|**Default value**|Defined in `variables.tf`|
|**CLI flag**|`terraform apply -var="region=us-west-2"`|
|**Variable file**|`terraform apply -var-file="dev.tfvars"`|
|**Environment variable**|`export TF_VAR_region=us-west-2`|
