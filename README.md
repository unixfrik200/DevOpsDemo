# Create infra with CFT and example of do automation with basic steps

Please mentione your SSH AWS key name in statement-1/DevOpsDemo-statement-1-Parameters.json, you can also change other parameters value as per your requirement.

1) Create VPC, EC2 instances in public and private subnet using AWS CFT
```
aws cloudformation create-stack --stack-name DevOpsDemo-dev --template-body file://statement-1/DevOpsDemo-statement-1.json --parameters file://statement-1/DevOpsDemo-statement-1-Parameters.json
```
