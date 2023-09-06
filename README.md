# Sagemaker Playground

## Setup with CloudFormation

- https://aws.amazon.com/about-aws/whats-new/2021/02/now-launch-amazon-sagemaker-studio-aws-cloudformation/
- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_SageMaker.html
- https://docs.aws.amazon.com/sagemaker/latest/dg/gs.html

## Deploy to production with cloudformation

- https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-deployment.html
- https://faun.pub/mastering-the-mystical-art-of-model-deployment-part-2-deploying-amazon-sagemaker-endpoints-with-cf9539dc2579

## Other references

- https://github.com/aws/amazon-sagemaker-examples
- https://sagemaker-examples.readthedocs.io
- https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-roles.html

## CloudFormation infrastructure

### SageMaker

- [AWS::SageMaker](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_SageMaker.html)

```
aws cloudformation create-stack --stack-name monsai-sagemaker --template-body file://infrastructure/sagemaker/template.yaml --capabilities CAPABILITY_NAMED_IAM --tags Key=owner,Value=simone.spaccarotella@bbc.co.uk
```

### IAM

- [AWS::IAM::Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html)

### Elastic Container Registry

- [AWS::ECR::Repository](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ecr-repository.html)

```
aws cloudformation create-stack --stack-name monsai-ecr --template-body file://infrastructure/ecr/template.yaml --tags Key=owner,Value=simone.spaccarotella@bbc.co.uk
```
