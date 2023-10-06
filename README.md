# Sagemaker Playground

## Tutorial

- [Amazon SageMaker Studio](https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html)
- [Getting Started with Sagemaker](https://aws.amazon.com/sagemaker/getting-started/)

## Deploy a model to production

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
export TEMPLATE_PREFIX=file://infrastructure/sagemaker
```

```
export FILE=iam-policies-and-roles
export STACK=${STACK_PREFIX}-${FILE}
export CHANGESET=${STACK}-change-set
export TEMPLATE=${TEMPLATE_PREFIX}/${FILE}.yaml

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --tags $TAGS --capabilities CAPABILITY_NAMED_IAM

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```

```
export FILE=domain
export STACK=${STACK_PREFIX}-${FILE}
export CHANGESET=${STACK}-change-set
export TEMPLATE=${TEMPLATE_PREFIX}/${FILE}.yaml
export PARAMS=${TEMPLATE_PREFIX}/${FILE}.params.json

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --parameters $PARAMS --tags $TAGS

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```

```
export FILE=user-profiles
export STACK=${STACK_PREFIX}-${FILE}
export CHANGESET=${STACK}-change-set
export TEMPLATE=${TEMPLATE_PREFIX}/${FILE}.yaml

aws cloudformation create-change-set --change-set-name $CHANGESET --change-set-type CREATE --stack-name $STACK --template-body $TEMPLATE --tags $TAGS

aws cloudformation execute-change-set --change-set-name $CHANGESET --stack-name $STACK
```
