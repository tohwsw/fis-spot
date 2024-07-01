# Use FIS to Interrupt a Spot Instance

In this section, you're going to create and run an experiment to trigger the interruption of Amazon EC2 Spot Instances using AWS Fault Injection Simulator (FIS) 
.When using Spot Instances, you need to be prepared to be interrupted. With FIS, you can test the resiliency of your workload and validate that your application is reacting to the interruption notices that EC2 sends before terminating your instances. You can target individual Spot Instances or a subset of instances in clusters managed by services that tag your instances such as ASG, EC2 Fleet, and EKS.

Let's create a CloudFormation template which creates the IAM role (FISSpotRole) with the minimum permissions FIS needs to interrupt an instance, and the experiment template (FISExperimentTemplate) you're going to use to trigger a Spot interruption:

```
export FIS_EXP_NAME=fis-karpenter-spot-interruption
aws cloudformation create-stack --stack-name $FIS_EXP_NAME --template-body file://fis-karpenter.yaml --capabilities CAPABILITY_NAMED_IAM
aws cloudformation wait stack-create-complete --stack-name $FIS_EXP_NAME
```

You can run the Spot interruption experiment from the FIS console.
