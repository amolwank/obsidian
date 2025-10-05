##### Introduction
In Terraform, a module is a way to organize and reuse infrastructure code.

It's essentially a folder with terraform files that defines resources, variables, and outputs - and can be called from other Terraform configurations.

##### What is a Module?
- A container for Terraform resources.
- Can be local (inside your repository) or remote(Terraform Registry, GitHub, etc)
- Helps avoid code duplication and make infrastructure scalable and maintainable
##### Benefits of Modules
- Reusability -> Write once , use many times.
- Maintainability->Centralized updates.
- Organization -> Cleaner and more readable code. 
- Scalability -> Easy to extend for more environments
##### Best Practices
- Keep modules small and focused (one resource per module)
- Documents inputs and outputs in Readme.md
- Use versioning when pulling from public sources.
- Avoid hardcoding - use variables
- Test modules before using in production.