# ECR Repository and LifeCycle Policy

This repo contains a simple CloudFormation template for creating a lifecycle policy for images in an Amazon ECR repository. There are a variety of lifecycle policies that may be written that use age of images, number of images or even image tag value to limit the crowding in an ECR repository.

As a POC, this template creates a simple policy that allows ten images to linger in the repository, with older images being removed as newer ones are added.

## Template Parameters

For ease of use, update the parameter file titled ecr_lifecycle_params.json in this repository. The following parameter is used for the template.

|Parameter|Description|Example|
|------|------|-------|
|Owner|The name of the person or team the template and resource should be associated with. Must be lower case, as it is used as part of the repo name, which has naming restrictions.|jane|

## How to Deploy

### Prerequisites

To deploy the stack via the command line, you will need the AWS CLI.

To use a separate file to update parameter(s), you can update and use the ecr_lifecycle_params.json file.

### Validate/Lint Stack

```bash
aws cloudformation validate-template \
--template-body file://ecr_lifecycle.yaml
```

### Deploy Stack

Navigate to the parent directory of this repository, then run the following command:

```bash
aws cloudformation deploy \
--stack-name my-ecr-stack \
--template-file ecr_lifecycle.yaml \
--parameter-overrides file://parameters/ecr_lifecycle_params.json
```

The above command will deploy and/or update the stack.

## Resources

* [CloudFormation User Guide for ECR Repository](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ecr-repository.html)
* [Lifecycle policy examples from AWS User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/lifecycle_policy_examples.html)