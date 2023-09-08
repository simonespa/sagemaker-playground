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

## CloudFormation Resource types

[SageMaker resource types](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_SageMaker.html)

## AWS CLI

### Stacks

[create-stack](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-stack.html)

```
aws cloudformation create-stack --stack-name $STACK --template-body $TEMPLATE --parameters $PARAMS --tags $TAGS
```

[describe-stacks](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/describe-stacks.html)

```
aws cloudformation describe-stacks --stack-name $STACK
```

[update-stack](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/update-stack.html)

```
aws cloudformation update-stack --stack-name $STACK --template-body $TEMPLATE --parameters $PARAMS
```

[delete-stack](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/delete-stack.html)

```
aws cloudformation delete-stack --stack-name $STACK
```

### Change Sets

[create-change-set](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-change-set.html)

```
aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --parameters $PARAMS --tags $TAGS
```

[execute-change-set](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/execute-change-set.html)

```
aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```

[describe-change-set](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/describe-change-set.html)

```
aws cloudformation describe-change-set --change-set-name $CHANGESET --stack-name $STACK
```

[delete-change-set](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/delete-change-set.html)

## Infrastructure

```
export STACK_PREFIX=spa-sagemaker
export TAGS=file://infrastructure/tags.json
```

```
export STACK=${STACK_PREFIX}-iam-policies-and-roles
export CHANGESET=${STACK}-change-set
export TEMPLATE=file://infrastructure/sagemaker/iam-policies-and-roles.yaml

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --tags $TAGS --capabilities CAPABILITY_NAMED_IAM

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```

```
export STACK=${STACK_PREFIX}-domain
export CHANGESET=${STACK}-change-set
export TEMPLATE=file://infrastructure/sagemaker/domain.yaml
export PARAMS=file://infrastructure/sagemaker/domain.params.json

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --parameters $PARAMS --tags $TAGS

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```

```
export STACK=${STACK_PREFIX}-user-profiles
export CHANGESET=${STACK}-change-set
export TEMPLATE=file://infrastructure/sagemaker/user-profiles.yaml

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --tags $TAGS

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```
