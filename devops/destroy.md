terraform destroy --> delete the resource from the .tf file

**Single resource destroy**
In terraform you can destroy single resource without affecting the entire infrastructure.

terraform destroy -target= <resource_type>.<resource_name>

Example:
```
terraform destroy -target= aws_instance.my_ec2
```

**Notes for Interview:**
- Useful when you want to remove the specific resource without affecting the other infrastructure.
- Not recommended for regular workflow, as it cause state drift.
- Better to remove it from code and run terraform apply.
