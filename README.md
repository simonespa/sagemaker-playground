# Sagemaker The First

## References
- https://github.com/aws/amazon-sagemaker-examples
- https://sagemaker-examples.readthedocs.io

## CloudFormation infrastructure

### Elastic Container Registry

- [AWS::ECR::Repository](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ecr-repository.html)

```
aws cloudformation create-stack --stack-name monsai-ecr --template-body file://infrastructure/ecr/template.yaml --tags Key=owner,Value=simone.spaccarotella@bbc.co.uk
```

### SageMaker

- [AWS::SageMaker::Model](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-model.html)
- [AWS::SageMaker::EndpointConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-endpointconfig.html)
- [AWS::SageMaker::Endpoint](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-endpoint.html)

```
aws cloudformation create-stack --stack-name monsai-sagemaker --template-body file://infrastructure/sagemaker/template.yaml --capabilities CAPABILITY_NAMED_IAM --tags Key=owner,Value=simone.spaccarotella@bbc.co.uk
```

### IAM

- [AWS::IAM::Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html)
- https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-roles.html
