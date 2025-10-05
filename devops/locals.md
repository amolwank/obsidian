mine:
want to reuse the values in modules but don't want to expose as input variables.

Syntax:
```
locals {
	app_name = "myapp"
	environment = "dev"
	instance_type = "t2.micro"
	tags = {
		owner = "Amol"
		Env = local.environment
		}
}
```

Usage:
You reference local variables using the local. prefix:
```
resource "aws_instance" "example" {
	ami = ""
	instance_type = local.instance_type
	
	tags = local.tags
}
```

Key Point:
- Defined with locals {} block inside a module.
- Used with local.name
-  They are evaluated only within that module (not global)
- They cannot be overridden like input variables(var.name)

