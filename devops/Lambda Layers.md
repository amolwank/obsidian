What are Lambda Layers?
?
1. Lambda Layers are a way to package and share dependencies, libraries, or custom code across multiple AWS Lambda functions.
2. They helps keep Lambda functions lightweight and avoid duplicating the same code in every function.
3. Each Lambda function can include up to 5 layers.
<!--SR:!2025-09-22,3,250-->

Why use Lambda Layers?
- Reusability -> Common code
- Smaller deployment package -> You only upload business logic; dependencies stay in layers.
- Versioning -> Layers are versioned, so you can roll back easily.
- Faster deployments -> Because only functions code changes, not the shared libraries.

Interview one-liner:
Lambda Layers let me package and share common dependencies like libraries or utilities across multiple functions, reducing duplication and improving deployment efficiency.

#flashcards 