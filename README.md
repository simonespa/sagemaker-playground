# Sagemaker The First

## CloudFormation infrastructure

- [AWS::SageMaker::Model](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-model.html)
- [AWS::SageMaker::EndpointConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-endpointconfig.html)
- [AWS::SageMaker::Endpoint](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-endpoint.html)

##

```
aws cloudformation create-stack --stack-name $1 --template-body file://$2 --parameter file://$3
```
