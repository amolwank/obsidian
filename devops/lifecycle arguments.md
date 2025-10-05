### Why Lifecycle Arguments are Useful?

- Avoid **downtime** (`create_before_destroy`)
- Protect **critical resources** (`prevent_destroy`)
- Handle **external changes gracefully** (`ignore_changes`)

Common Lifecycle Arguments

**`create_before_destroy`**
- Ensures Terraform **creates a new resource before destroying the old one**.    
- Prevents downtime.
```
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  lifecycle {
    create_before_destroy = true
  }
}
```

**`prevent_destroy`**
- Protects critical resources from accidental deletion.
- If you try `terraform destroy`, Terraform will throw an error.

```
resource "aws_s3_bucket" "important" {
  bucket = "my-prod-bucket"

  lifecycle {
    prevent_destroy = true
  }
}
```

**`ignore_changes`**

- Tells Terraform to **ignore changes** to specific attributes.
- Useful when some fields are modified outside Terraform (like tags added by AWS).
```
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  lifecycle {
    ignore_changes = [tags]
  }
}
```