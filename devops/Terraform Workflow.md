1. Write (Configuration Phase)
	- Define infrastructure in .tf files
	- Example:
```
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}

```
2. Init (Initialization Phase)
	- terraform init
	- What happens:
		- Downloads required provider plugins.
		- Sets up the backend (local or remote state storage).
		- Prepares the working directory.
3. Plan (Execution Plan phase > terraform plan)
	- Compares configuration with the current state.
	- Shows what terraform will create, change, or destroy.
	- Gives a safe preview before making changes.
4. Apply (Provisioning Phase: terraform apply)
	- Executes the plan.
	- Provisions, updates, or deletes resources
	- Update the state file to reflect the new reality.
5. Destroy (Teardown Phase)
	- Removes all infrastructure defined in the configuration.
	- Update the state file accordingly.




Tags: #Terraform