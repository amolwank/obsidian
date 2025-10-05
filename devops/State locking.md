🔒 **1. Old Way – S3 + DynamoDB Locking (Deprecated)**
```
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "env/dev/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true

    # Locking with DynamoDB
    dynamodb_table = "terraform-locks"
  }
}
```
👉 Requirements:
- S3 bucket (with versioning recommended).
- DynamoDB table (`LockID` as primary key).

🔒 **2. New Way – S3 Native Locking (Recommended)**
```
terraform {
  required_version = ">= 1.11.0"

  backend "s3" {
    bucket       = "my-terraform-state-bucket"
    key          = "env/dev/terraform.tfstate"
    region       = "us-east-1"
    encrypt      = true

    # Native S3 locking (no DynamoDB needed)
    use_lockfile = true
  }
}
```
👉 Requirements:
- S3 bucket with **versioning enabled** (mandatory).
- No DynamoDB table needed.


✅ In short:
- **If you’re on Terraform <1.10 → use DynamoDB.**
- **If you’re on Terraform 1.11+ → switch to `use_lockfile = true`.**