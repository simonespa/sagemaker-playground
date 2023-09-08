# Sage Maker User Profiles

- arn:aws:iam::aws:policy/AmazonSageMakerFullAccess
- arn:aws:iam::aws:policy/AmazonSageMakerCanvasFullAccess
- arn:aws:iam::aws:policy/AmazonSageMakerCanvasAIServicesAccess
## Data Scientist

A persona that performs machine learning activities from within a sagemaker environment. Permitted to process S3 data, perform experiments and produce models.

- Run Studio Applications: Permissions to operate within a Studio environment. Required for domain and user-profile execution roles.
- Manage ML Jobs: Permissions to manage SageMaker jobs across their lifecycles.
- Manage Models: Permissions to manage SageMaker models and Model Registry.
- Manage Experiments: Permissions to manage experiments and trials.
- Search and visualize experiments: Permissions to audit, query lineage and visualize experiments.
- S3 Bucket Access: Permissions to perform operations on specified buckets.

Note 1: This role requires access to one or more S3 buckets.
Note 2: Additional managed IAM policies can be added to this role.

### Permissions

- SageMakerS3BucketPolicyTemplate
- SM_CommonJobManagement
- SM_ExperimentsManagement
- SM_ExperimentsVisualization
- SM_ModelManagement
- SM_StudioAppPermissions

### Trust relationship

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "sagemaker.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:sagemaker:eu-west-1:749144762306:*"
                }
            }
        }
    ]
}
```

## ML Ops

A persona that deals with operational activities from within a sagemaker environment. Permitted to manage models, endpoints and pipeline, and audit resources.

- Run Studio Applications: Permissions to operate within a Studio environment. Required for domain and user-profile execution roles.
- Manage Models: Permissions to manage SageMaker models and Model Registry.
- Manage Endpoints: Permissions to manage SageMaker Endpoint deployments and updates.
- Manage Pipelines: Permissions to manage SageMaker Pipelines and pipeline executions.
- Search and visualize experiments: Permissions to audit, query lineage and visualize experiments.

### Permissions

- SM_EndpointDeployment
- SM_ExperimentsVisualization
- SM_ModelManagement
- SM_PipelineManagement
- SM_StudioAppPermissions

### Trust relationship

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "sagemaker.amazonaws.com"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:sagemaker:eu-west-1:749144762306:*"
        }
      }
    }
  ]
}
```

## SageMaker Compute Role

A persona used by SageMaker compute resources such as jobs and endpoints. Permitted to access S3 resources, ECR repositories, CloudWatch and other services for ML computation

- Access Required AWS Services

## All ML Activities

- Access Required AWS Services: Permissions to access S3, ECR, Cloudwatch and EC2. Required for execution roles for jobs and endpoints.
- Run Studio Applications: Permissions to operate within a Studio environment. Required for domain and user-profile execution roles.
- Manage ML Jobs: Permissions to manage SageMaker jobs across their lifecycles.
- Manage Models: Permissions to manage SageMaker models and Model Registry.
- Manage Endpoints: Permissions to manage SageMaker Endpoint deployments and updates.
- Manage Pipelines: Permissions to manage SageMaker Pipelines and pipeline executions.
- Manage Experiments: Permissions to manage experiments and trials.
- Search and visualize experiments: Permissions to audit, query lineage and visualize experiments.
- Manage Model Monitoring: Permissions to manage monitoring schedules for SageMaker Model Monitor.
- S3 Full Access: Permissions to perform all S3 operations
- S3 Bucket Access: Permissions to perform operations on specified buckets.
- Query Athena Workgroups: Permissions to execute and manage Amazon Athena queries.
- Manage Glue Tables: Permissions to create and manage Glue tables for SageMaker Feature Store and Data Wrangler.

## Additional policies
- arn:aws:iam::aws:policy/AmazonSageMakerCanvasFullAccess: Enable Canvas base permissions
- arn:aws:iam::aws:policy/AmazonSageMakerCanvasAIServicesAccess: Enable Canvas Ready-to-use models
- arn:aws:iam::aws:policy/service-role/AmazonSageMakerCanvasForecastAccess: Enable time series forecasting with Canvas

## Gotcha

There is a quota of 10 policies per role, need to work around this.
