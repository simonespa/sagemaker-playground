# Sage Maker User Profiles

- arn:aws:iam::aws:policy/AmazonSageMakerFullAccess

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

## All Permissions

### SM_EndpointDeployment

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:CreateEndpointConfig",
        "sagemaker:CreateEndpoint",
        "sagemaker:DeleteEndpointConfig",
        "sagemaker:DeleteEndpoint",
        "sagemaker:UpdateEndpoint",
        "sagemaker:UpdateEndpointWeightsAndCapacities",
        "sagemaker:DescribeEndpoint",
        "sagemaker:DescribeEndpointConfig"
      ],
      "Resource": "arn:aws:sagemaker:*:*:*/*"
    },
    {
      "Effect": "Allow",
      "Action": ["sagemaker:ListEndpoints", "sagemaker:ListEndpointConfigs"],
      "Resource": "*"
    }
  ]
}
```

### SM_ExperimentsVisualization

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:DescribeAction",
        "sagemaker:DescribeArtifact",
        "sagemaker:DescribeContext",
        "sagemaker:DescribeExperiment",
        "sagemaker:DescribeTrial",
        "sagemaker:DescribeTrialComponent",
        "sagemaker:DescribeLineageGroup"
      ],
      "Resource": "arn:aws:sagemaker:*:*:*/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:ListAssociations",
        "sagemaker:ListActions",
        "sagemaker:ListArtifacts",
        "sagemaker:ListContexts",
        "sagemaker:ListExperiments",
        "sagemaker:ListTrials",
        "sagemaker:ListTrialComponents",
        "sagemaker:ListLineageGroups",
        "sagemaker:GetLineageGroupPolicy",
        "sagemaker:QueryLineage",
        "sagemaker:Search",
        "sagemaker:GetSearchSuggestions"
      ],
      "Resource": "*"
    }
  ]
}
```

### SM_ModelManagement

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:CreateModel",
        "sagemaker:CreateModelPackage",
        "sagemaker:CreateModelPackageGroup",
        "sagemaker:DescribeModel",
        "sagemaker:DescribeModelPackage",
        "sagemaker:DescribeModelPackageGroup",
        "sagemaker:BatchDescribeModelPackage",
        "sagemaker:UpdateModelPackage",
        "sagemaker:DeleteModel",
        "sagemaker:DeleteModelPackage",
        "sagemaker:DeleteModelPackageGroup"
      ],
      "Resource": "arn:aws:sagemaker:*:*:*/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:ListModels",
        "sagemaker:ListModelPackages",
        "sagemaker:ListModelPackageGroups"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": [
        "arn:aws:iam::749144762306:role/service-role/SageMaker-TheMLOps"
      ],
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": "sagemaker.amazonaws.com"
        }
      }
    }
  ]
}
```

### SM_PipelineManagement

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:CreatePipeline",
        "sagemaker:StartPipelineExecution",
        "sagemaker:StopPipelineExecution",
        "sagemaker:RetryPipelineExecution",
        "sagemaker:UpdatePipelineExecution",
        "sagemaker:SendPipelineExecutionStepSuccess",
        "sagemaker:SendPipelineExecutionStepFailure",
        "sagemaker:DescribePipeline",
        "sagemaker:DescribePipelineExecution",
        "sagemaker:DescribePipelineDefinitionForExecution",
        "sagemaker:DeletePipeline"
      ],
      "Resource": "arn:aws:sagemaker:*:*:*/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "sagemaker:ListPipelines",
        "sagemaker:ListPipelineExecutions",
        "sagemaker:ListPipelineExecutionSteps",
        "sagemaker:ListPipelineParametersForExecution"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": [
        "arn:aws:iam::749144762306:role/service-role/SageMaker-TheMLOps"
      ],
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": "sagemaker.amazonaws.com"
        }
      }
    }
  ]
}
```

### SM_StudioAppPermissions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SMStudioAppPermissionsCRUD",
      "Effect": "Allow",
      "Action": [
        "sagemaker:CreateApp",
        "sagemaker:CreateAppImageConfig",
        "sagemaker:UpdateAppImageConfig",
        "sagemaker:DeleteApp",
        "sagemaker:DeleteAppImageConfig",
        "sagemaker:DescribeApp",
        "sagemaker:DescribeAppImageConfig",
        "sagemaker:DescribeDomain",
        "sagemaker:DescribeUserProfile"
      ],
      "Resource": "arn:aws:sagemaker:eu-west-1:749144762306:*/*"
    },
    {
      "Sid": "SMStudioAppPermissionsList",
      "Effect": "Allow",
      "Action": [
        "sagemaker:ListApps",
        "sagemaker:ListAppImageConfigs",
        "sagemaker:ListDomains",
        "sagemaker:ListUserProfiles"
      ],
      "Resource": "*"
    },
    {
      "Sid": "SMStudioAppPermissionsTagOnCreate",
      "Effect": "Allow",
      "Action": ["sagemaker:AddTags"],
      "Resource": "arn:aws:sagemaker:eu-west-1:749144762306:*/*",
      "Condition": {
        "Null": {
          "sagemaker:TaggingAction": "false"
        }
      }
    }
  ]
}
```

### SageMakerS3BucketPolicyTemplate

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::sagemaker-eu-west-1-749144762306"]
    },
    {
      "Action": ["s3:GetObject", "s3:PutObject", "s3:DeleteObject"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::sagemaker-eu-west-1-749144762306/*"]
    }
  ]
}
```

### SM_CommonJobManagement

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sagemaker:CreateTrainingJob",
                "sagemaker:CreateTransformJob",
                "sagemaker:CreateProcessingJob",
                "sagemaker:CreateAutoMLJob",
                "sagemaker:CreateHyperParameterTuningJob",
                "sagemaker:StopTrainingJob",
                "sagemaker:StopProcessingJob",
                "sagemaker:StopAutoMLJob",
                "sagemaker:StopHyperParameterTuningJob",
                "sagemaker:DescribeTrainingJob",
                "sagemaker:DescribeTransformJob",
                "sagemaker:DescribeProcessingJob",
                "sagemaker:DescribeAutoMLJob",
                "sagemaker:DescribeHyperParameterTuningJob",
                "sagemaker:UpdateTrainingJob",
                "sagemaker:BatchGetMetrics"
            ],
            "Resource": "arn:aws:sagemaker:*:*:*/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "sagemaker:Search",
                "sagemaker:ListTrainingJobs",
                "sagemaker:ListTransformJobs",
                "sagemaker:ListProcessingJobs",
                "sagemaker:ListAutoMLJobs",
                "sagemaker:ListCandidatesForAutoMLJob",
                "sagemaker:ListHyperParameterTuningJobs",
                "sagemaker:ListTrainingJobsForHyperParameterTuningJob"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": [
                "arn:aws:iam::749144762306:role/service-role/SageMaker-TheDataScientist"
            ],
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "sagemaker.amazonaws.com"
                }
            }
        }
    ]
}
```

### SM_ExperimentsManagement

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sagemaker:AddAssociation",
                "sagemaker:CreateAction",
                "sagemaker:CreateArtifact",
                "sagemaker:CreateContext",
                "sagemaker:CreateExperiment",
                "sagemaker:CreateTrial",
                "sagemaker:CreateTrialComponent",
                "sagemaker:UpdateAction",
                "sagemaker:UpdateArtifact",
                "sagemaker:UpdateContext",
                "sagemaker:UpdateExperiment",
                "sagemaker:UpdateTrial",
                "sagemaker:UpdateTrialComponent",
                "sagemaker:AssociateTrialComponent",
                "sagemaker:DisassociateTrialComponent",
                "sagemaker:DeleteAssociation",
                "sagemaker:DeleteAction",
                "sagemaker:DeleteArtifact",
                "sagemaker:DeleteContext",
                "sagemaker:DeleteExperiment",
                "sagemaker:DeleteTrial",
                "sagemaker:DeleteTrialComponent"
            ],
            "Resource": "arn:aws:sagemaker:*:*:*/*"
        }
    ]
}
```
