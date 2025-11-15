# awsgoat/pacu- aws infra security testing
AWSGoat is a vulnerable-by-design AWS infrastructure exposing OWASP Top 10 (2021) risks and misconfigurations across IAM, S3, API Gateway, Lambda, EC2, and ECS. Using Terraform and GitHub Actions, it enables cloud pentesting, IaC auditing, secure coding, detection, and mitigation in realistic modular environments.

AWSGoat is a vulnerable by design infrastructure on AWS featuring the latest released OWASP Top 10 web application security risks (2021) and other misconfiguration based on services such as IAM, S3, API Gateway, Lambda, EC2, and ECS. AWSGoat mimics real-world infrastructure but with added vulnerabilities. It features multiple escalation paths and is focused on a black-box approach.

AWSGoat uses IaC (Terraform) to deploy the vulnerable cloud infrastructure on the user's AWS account. This gives the user complete control over code, infrastructure, and environment. Using AWSGoat, the user can learn/practice:

Cloud Pentesting/Red-teaming
Auditing IaC
Secure Coding
Detection and mitigation
The project will be divided into modules and each module will be a separate web application, powered by varied tech stacks and development practices. It will leverage IaC through terraform and GitHub actions to ease the deployment process.

More can be found out at: https://github.com/ine-labs/AWSGoat?tab=readme-ov-file
