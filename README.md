Crossplane is focused on managing cloud-native infrastructure through Kubernetes. It specializes in provisioning and managing cloud resources using the Kubernetes API,

Crossplane follows the Kubernetes extensibility model and allows you to define custom resource definitions (CRDs) and controllers to extend its functionality. It provides a framework for building and managing infrastructure providers, enabling you to create your own custom providers or extend existing ones.

Crossplane integrates with the Kubernetes workflow, allowing you to define infrastructure resources as Kubernetes manifests and apply them using kubectl apply. It leverages Kubernetes' declarative nature and reconciliation loop to manage infrastructure resources.

Since Crossplane relies on Kubernetes as the state store for infrastructure resources, there's no separate file equivalent to Terraform's tfstate file. Instead, the state of infrastructure resources is stored directly within the Kubernetes cluster's etcd datastore, managed by the Kubernetes control plane.

you can reference the VPC ID created by Crossplane in the EC2 instance manifest:

```
apiVersion: compute.aws.crossplane.io/v1alpha1
kind: Instance
metadata:
  name: my-ec2-instance
spec:
  forProvider:
    iamInstanceProfile: "my-iam-role"
    imageID: "ami-12345678"
    instanceType: "t2.micro"
    subnetID: "subnet-12345678"
    securityGroupIDs:
      - "sg-12345678"
    vpcID: "crossplane.io/name-of-your-vpc-resource"
```
