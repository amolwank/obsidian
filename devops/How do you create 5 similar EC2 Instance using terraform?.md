

## ✅ Method 1: Using `count`

```
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0" # Example AMI (Amazon Linux 2)
  instance_type = "t2.micro"
  count         = 5   # creates 5 EC2 instances

  tags = {
    Name = "web-${count.index}"  # web-0, web-1, web-2, etc.
  }
}
```
- **`count`** creates multiple copies of the same resource.
    
- **`count.index`** gives the index (0 → N-1).
    

---

## ✅ Method 2: Using `for_each` (when you need custom names/values)

```
variable "servers" {
  default = {
    server1 = "t2.micro"
    server2 = "t2.small"
    server3 = "t2.micro"
    server4 = "t2.medium"
    server5 = "t2.micro"
  }
}

resource "aws_instance" "web" {
  for_each      = var.servers
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = each.value

  tags = {
    Name = each.key
  }
}
```
- **`for_each`** is better when you want **different configurations per instance**.
    

---

## ✅ Method 3: Using a Module (best practice for reusable code)

Create a module `modules/ec2/` with an EC2 definition, then call it multiple times:

```
module "ec2" {
  source        = "./modules/ec2"
  instance_type = "t2.micro"
  count         = 5
}
```
## 📌 Interview-ready Summary

- To create 5 similar EC2 instances in Terraform, use **`count`** or **`for_each`**.
- `count` → simple identical resources.
- `for_each` → when each resource needs unique values.
- For large-scale / reusable infra, use **modules**.
    

---