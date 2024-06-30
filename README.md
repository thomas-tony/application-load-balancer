# Application Load Balancer

This project sets up an Application Load Balancer with 4 EC2 instances. Each instance runs Nginx and serves a simple HTML page showing the instance's IP address. This setup allows us to verify the load balancer by observing the distribution of requests across multiple instances.

## Getting Started

### Prerequisites

- AWS CLI installed and configured
- An existing EC2 KeyPair

### Step 1: Create a CloudFormation Stack

Clone the repository and navigate to the project directory:

```sh
git clone https://github.com/thomas-tony/application-load-balancer.git
cd application-load-balancer
```

Create the CloudFormation stack using the AWS CLI:

```sh
aws cloudformation create-stack --stack-name MyLoadBalancerStack --template-body file://templates/load-balancer.yaml --parameters ParameterKey=KeyName,ParameterValue=your-key-pair-name
```

### Step 2: Monitor the Stack Creation

Monitor the stack creation process:

```sh
aws cloudformation describe-stacks --stack-name MyLoadBalancerStack
```

### Step 3: Access the Load Balancer
Once the stack creation is complete, get the DNS name of the load balancer from the outputs:


```sh
aws cloudformation describe-stacks --stack-name MyLoadBalancerStack --query "Stacks[0].Outputs[0].OutputValue" --output text
```
Open the DNS name in your web browser. Refresh the page multiple times to see the IP address change, verifying that the load balancer is distributing traffic across the instances.


### : Clean Up
To delete the stack and all associated resources:


```sh
aws cloudformation delete-stack --stack-name MyLoadBalancerStack
```


