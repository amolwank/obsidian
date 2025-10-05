Questions;
If I have to provision 10 EC2 instances with diff configuration, What is the best approach ?

##### Detailed Answer (Interview Style):
- If all instances have the same configuration -> use count to create multiple instances
- If each instance has diff configurations (CPU, memory, tags, AMIs, etc) -> define a map of object in variable and use for_each to provision each instance with its own settings.
- This avoids code duplication, makes it easy to maintain, and integrates well with modules.
#### 🔹 Example (Terraform with different configs using `for_each`)

```
variable "instances" {
  type = map(object({
    instance_type = string
    ami           = string
  }))

  default = {
    web1 = { instance_type = "t2.micro", ami = "ami-0c55b159cbfafe1f0" }
    web2 = { instance_type = "t3.small", ami = "ami-0c55b159cbfafe1f0" }
    db1  = { instance_type = "t3.medium", ami = "ami-0c55b159cbfafe1f0" }
  }
}

resource "aws_instance" "ec2" {
  for_each      = var.instances
  ami           = each.value.ami
  instance_type = each.value.instance_type
  tags = {
    Name = each.key
  }
}
```

##### Example: Provision 3 AWS EC2 Instances with `count`
```
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"  # Example Amazon Linux AMI
  instance_type = "t2.micro"

  tags = {
    Name = "example-instance-${count.index + 1}"
  }
}
```