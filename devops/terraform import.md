terraform import is a Terraform command that lets you bring existing infrastructure (created manually or outside Terraform) under Terraform's management without recreating it.

Step 1- Create resource definition (not apply yet)
```
resource "aws_instance" "my_ec2" {
ami = "ami-12345678"
instance_type = "t2.micro"
}
```
Step 2: Run import

```
terraform import aws_instance.my_ec2 i-0asdsdsfjdj
```
Step 3:- Run terraform plan
- Terraform reads current configuration from state and matches it with .tf file.

##### Important Notes
- terraform import only imports into the state file- it does not update .tf configuration automatically.
- You must manually write the configuration to match the real resource, or Terraform will try to change it on next apply.