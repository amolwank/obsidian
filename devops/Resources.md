##### Introduction
In Terraform, a resource is the main building block that describes an infrastructure object you want to create, manage, or destroy.

Think of it as the real thing in the cloud or on-prem  - like an AWS ec2 instance, S3 bucket, a kubernetes pod or a DNS records.

##### Definition
- A resource represents a single piece of infrastructure managed by Terraform.
- Defined in .tf files using the resource  
##### Syntax Example
```
resource "aws_instance" "my_ec2" {
	ami = ""
	instance_type = ""
	tags = {
		Name= "MyEC2Instance"
	}
}
```

##### Resource Type Examples
- AWS-> aws_s3_bucket, aws_ec2_instance
- Azure-> azurerm_storage_account, azurerm_virtual_machine
- GCP-> google_compute_instance, google_storage_bucket
- Kubernetes -> kubernetes_pod, kubernetes_service
##### Key Points For Interviews:
- Resources are idempotent
- Resources can have dependencies
- You  can import existing infrastructure into Terraform as a resource