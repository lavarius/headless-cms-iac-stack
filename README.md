# wordpress-cf-stack

CloudFormation stack for Wordpress:6.6 that uses Elastic Container Service (ECS) Fargate with Relational Database Service (RDS), and Elastic Container Registry (ECR).
Other resources utilized are Parameter Store and Secrets Manager.

Currently requires a manual setup of repositories `dev-wordpress` or `prd-wordpress` in ECR and referencing the initil push command for logging with IAM User profile to access the repo and push the wordpress docker image to the repo. 
Authenticate your local mahchine to the Amazon ECR registry with AWS CLI
- `aws ecr get-login-password --region <your-region> --profile <IAM-user> | docker login --username AWS --password-stdin <aws-account-id>.dkr.ecr.<your-region>.amazonaws.com`

Pull the wordpress:6.6 image
- `docker pull wordpress:6.6`

Tag the pulled image with the ECR Repo URI (e.g. `prd-wordpress`)
- `docker tag wordpress:6.6 <aws-account-id>.dkr.ecr.<your-region>.amazonaws.com/prd-wordpress:6.6`

Push the tagged image to ECR repo (e.g. `prd-wordpress`):
- `docker push <aws-account-id>.dkr.ecr.<your-region>.amazonaws.com/prd-wordpress:6.6`

After this manual setup, running the Cloudformation template creates the other 34 resources that the stack has defined.

In the Output tab, Wordpress should be accessible for the first time running the initial set up for login. 
