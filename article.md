---
author: "Kyle Jones"
date_published: "September 25, 2024"
date_exported_from_medium: "November 10, 2025"
canonical_link: "https://medium.com/@kyle-t-jones/how-aws-cdk-turns-code-into-cloudformation-templates-8f725301ef17"
---

# How AWS CDK turns code into CloudFormation Templates AWS CDK converts code into AWS CloudFormation templates, which AWS uses
to manage and provision cloud resources. This process involves...

### How AWS CDK turns code into CloudFormation Templates
AWS CDK converts code into AWS CloudFormation templates, which AWS uses to manage and provision cloud resources. This process involves writing infrastructure code, synthesizing that code into a CloudFormation template, and deploying the template to AWS.

#### **Writing Infrastructure Code**
AWS CDK defines infrastructure using familiar programming languages such as TypeScript, Python, Java, or C#. This is a crucial departure from CloudFormation, where users define infrastructure using YAML or JSON templates. The use of general-purpose programming languages allows developers to write more flexible and reusable infrastructure code using control structures like loops, conditionals, and functions.

For example, a simple TypeScript CDK application to define an S3 bucket might look like this:

```python
import * as cdk from '@aws-cdk/core';
import * as s3 from '@aws-cdk/aws-s3';
class MyStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);
    // Define an S3 bucket
    new s3.Bucket(this, 'MyBucket', , {
      versioned: true,
      encryption: s3.BucketEncryption.s S3 MANAGED,
    });
  }
}
const app = new cdk.App();
new MyStack(app, 'MyFirstStack');
```

This TypeScript code defines an S3 bucket with versioning and server-side encryption enabled. AWS CDK provides high-level constructs like s3bucket, simplifying AWS services' configuration.

#### **Synthesis**
Once the infrastructure code is written, the next step is synthesis. This is the process where AWS CDK compiles the infrastructure code into a CloudFormation template. The CloudFormation template is a declarative description of all the AWS resources that must be provisioned, including their configurations and dependencies.

In CDK, the synth command is used to generate the CloudFormation template:

``` 
cdk synth
```

This command produces a CloudFormation template in JSON format, which can then be deployed to AWS. The template describes the resources defined in the CDK code, such as S3 buckets, Lambda functions, and API Gateways.

#### **CloudFormation Deployment**
After synthesis, the CloudFormation template is deployed to AWS. During deployment, CloudFormation reads the template and provisions the specified resources. It handles resource creation, updating, and deletion safely and predictably, ensuring that all dependencies are managed correctly.

The deploy command is used to deploy the synthesized CloudFormation template to AWS:

``` 
cdk deploy
```

During deployment, CloudFormation performs the following tasks:

**Create Change Sets:** CloudFormation creates a change set that describes the difference between the stack's current state and the desired state defined in the template.

**Execute Change Sets:** CloudFormation executes the change set, creating, updating, or deleting resources as necessary.

**Monitor and Rollback:** If errors occur during deployment, CloudFormation automatically rolls back changes to ensure the stack remains stable.

### CDK project structure: What does each part do?
Initializing a new AWS CDK project creates a standard folder structure with specific files to manage the infrastructure code. Understanding this structure is essential for working effectively with CDK.

A typical AWS CDK project structure for a TypeScript application:

Let's break down each part:

bin/: This folder contains the entry point of the CDK application. The file inside bin/ is where you define the CDK app and instantiate the stacks. For example:

```python
import { App } from '@aws-cdk/core';
import { MyServerlessAppStack } from '../lib/my-serverless-app-stack';
const app = new App();
new MyServerlessAppStack(app, 'MyServerlessAppStack');
app.synth();
```

lib/: This folder contains the main infrastructure definition. The my-serverless-app-stack.ts file defines the resources that make up the stack. This is where most of the infrastructure code will live, including definitions for S3 buckets, Lambda functions, and API Gateway resources.

node_modules/: This folder contains the Node.js dependencies for your CDK project. When you run the npm install, the required CDK libraries and dependencies are downloaded here.

test/: This folder is optional and can contain unit tests for your CDK constructs and stacks.

cdk.json: This file contains configuration settings for your CDK project, such as the default stack names, AWS environment settings, and build commands.

package.json: This file is standard in any Node.js project. It defines the dependencies, scripts, and metadata for the CDK application. The AWS CDK libraries (e.g., \@aws-cdk/aws-s3, \@aws-cdk/aws-lambda) are included as dependencies in this file.

tsconfig.json: This file configures the TypeScript compiler. It specifies settings such as which files to include in the project and where to output compiled JavaScript code.

### Multi-language support in CDK (Typescript, Python, Java, C#)
AWS CDK supports various programming languages, including TypeScript, Python, Java, JavaScript, and C#. Using the same core CDK architecture, this adaptability lets developers work in their choice language.

**TypeScript**

TypeScript is the most commonly used language for AWS CDK. It provides strong type checking, code completion, and other features that make it easier to write infrastructure code. In TypeScript, CDK constructs are treated as classes and instantiated in the stack.

An example of defining a Lambda function in TypeScript:

``` 
const lambdaFunction = new lambda.Function(this 'MyFunction', {
  runtime: lambda.Runtime.NODEJS_14_X,
  code: Lambda.Code.fromAsset('lambda'),
  handler: 'index.handler', ,
});
```

**Python**

AWS CDK also supports Python, making it accessible to many developers and data scientists. In Python, CDK constructs work similarly to TypeScript, but the syntax follows Python conventions.

For example, defining a Lambda function in Python would look like this:

```python
from aws_cdk import aws_lambda as _lambda
lambda_function = _lambda.Function(self, 'MyFunction',
  runtime=_lambda.Runtime.PYTHON_3_8,
  code=_lambda.Code.from_asset('lambda'),
  handler='index.handler')
```

**Java**

AWS CDK also supports defining infrastructure using Java for organisations with a strong Java-based development culture. CDK's constructs are mapped to Java classes, and developers can use familiar object-oriented principles to define infrastructure.

A Java example for a Lambda function:

``` 
Function lambdaFunction = Function.Builder.create(this, "MyFunction")
  .runtime(Runtime.NODEJS_14_X)
  .code(Code.fromAsset("lambda"))
  .handler("index.handler")
  .build();
```

**C#**

AWS CDK also supports C#, allowing .NET developers to define AWS infrastructure using constructs as classes.

A C# example:

``` 
var lambdaFunction = new Function(this, "MyFunction", new FunctionProps
{
  Runtime= Runtime.NODEJS_14_X =
  Code = =Code.FromAsset("lambda"),
  Handler = "index.handler"
});
```

The core CDK libraries and constructs are available in all supported languages, and the behavior is consistent across them. This makes it easier to switch between languages or integrate CDK into existing projects, regardless of the language in which they are written.

### How the CDK deployment process works: Synth, Diff, and Deploy
The AWS CDK deployment process consists of several key steps, which ensure that infrastructure is created, updated, or deleted safely and efficiently. The main steps are Synth, Diff, and Deploy.

#### Synth
In the synth step, CDK converts the infrastructure code into a CloudFormation template. This process is triggered using the cdk synth command, which reads the code in your CDK app and translates it into a declarative CloudFormation template.

For example:

``` 
cdk synth
```

This command outputs a CloudFormation template in JSON format. The template describes the AWS resources, their configurations, and their relationships.

The synth process is crucial because it lets developers preview the CloudFormation template before deploying. This ensures the generated infrastructure code is correct and adheres to AWS best practices.

#### **Diff**
The diff step allows developers to compare the infrastructure code to the current state of the deployed resources. This comparison helps identify any changes that would be made to the resources if the code were deployed.

The cdk diff command compares the current infrastructure code with the stack currently deployed in AWS. It outputs a list of changes, including resources that will be created, modified, or deleted.

For example:

``` 
cdk diff
```

This command provides a detailed breakdown of the differences between the deployed resources and the new infrastructure code, allowing developers to review the changes before deployment.

#### **Deploy**
The deploy step is where CDK applies the infrastructure changes. It takes the synthesized CloudFormation template and deploys it using AWS CloudFormation. During this process, CloudFormation manages the creation, update, or deletion of resources based on the template.

The cdk deploy command handles this step:

``` 
cdk deploy
```

CloudFormation ensures that changes are applied in a safe and predictable manner, creating a change set that describes the modifications. If any errors occur during deployment, CloudFormation automatically returns the changes to maintain a stable state.

### Related Stories
- [[Setting up AWS CDK for your projects](https://medium.com/@kylejones_47003/setting-up-aws-cdk-for-your-projects-713d1d518b9a)]
- [[Building cloud resources with AWS CDK](https://medium.com/@kylejones_47003/building-cloud-resources-with-aws-cdk-7a8ee677e309)]
- [[Managing different environments for AWS CDK (Dev, Test, Prod)](https://medium.com/@kylejones_47003/managing-different-environments-for-aws-cdk-dev-test-prod-3ce6336bb7c0)]
