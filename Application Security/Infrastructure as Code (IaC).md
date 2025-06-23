### Terraform
#### Best Security Practices
- Make sure the state is kept in the cloud. Not locally it is possible to steal sensitive information otherwise.
- Make sure there is no hard coded secrets there should all be in a secret manager.
- Make sure there is some sort of CI/CD pipeline to scan the code for vulnerabilities.
- Perform manual review on code before it is merged and pushed.
- Create modules or templates secure out the box for resources to prevent mistakes from being made.

