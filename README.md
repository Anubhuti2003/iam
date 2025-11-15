exp1
access key AKIATGJQXTWL2URYPTPF
secret access key 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
SECTION 1 — Create AWS Account (Free)
Step 1: Go to AWS

https://aws.amazon.com/

Step 2: Click Create an AWS Account
Step 3: Fill details

Email

Password

Account name

Step 4: Add credit/debit card

AWS charges ₹2 verification, it gets refunded.

Step 5: Choose Free Tier Account
Step 6: Complete identity verification

(Phone OTP)

Step 7: Choose Basic Support (FREE)

Your AWS account is now ready!

✅ SECTION 2 — Install the Required Tools (Free)

You need three tools installed on your laptop.

Step 8: Install AWS CLI
Windows:

Download MSI installer:
https://awscli.amazonaws.com/AWSCLIV2.msi

Install → Finish.

Step 9: Install kubectl

Download for Windows:
https://dl.k8s.io/release/v1.28.0/bin/windows/amd64/kubectl.exe

Add it to PATH (I can help if needed).

Step 10: Install eksctl

Download installer:
https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Windows_amd64.zip

Extract

Rename to: eksctl.exe

Add to PATH
STEP 3 — Add the folder to PATH
Follow these exact steps:
🔹 Step 3.1 — Open Environment Variables

Press Windows Key

Type: environment variables

Click Edit the system environment variables

Click Environment Variables button

🔹 Step 3.2 — Edit PATH variable

Under the System variables section:

Select Path

Click Edit

Click New

Type the path to your folder:

C:\tools\


Or whatever folder you used.

Click OK everywhere to save.

✅ STEP 4 — Check if it worked

Open a new CMD or PowerShell window and run:

kubectl version --client


and

eksctl version


If both show version numbers → SUCCESS!

🩵 Troubleshooting Tips
❗ Important:

You must close and reopen CMD/PowerShell after editing PATH.

If you get:
'kubectl' is not recognized


Then PATH is incorrect — check the folder again.
STEP 2 — Create Access Keys in AWS (One-time)
1. Login to AWS Console

https://console.aws.amazon.com/

2. Go to IAM

Search IAM in the AWS search bar → open.

3. Go to “Users” → Select your user

You must choose a user with permissions (usually admin).

4. Go to “Security Credentials” tab
5. Scroll to “Access Keys” → Click “Create access key”
6. Choose “Command Line Interface (CLI)”

→ Continue

7. You will get:

Access Key ID

Secret Access Key

⚠️ Save these immediately
You will be shown the secret key only once.

✅ STEP 3 — Configure AWS CLI in Your System

Open Command Prompt or PowerShell and run:

aws configure


It will ask you four things one by one:

1. AWS Access Key ID

Paste your key:

AKIAxxxxxxxxxxx

2. AWS Secret Access Key

Paste your secret:

WJksdf345KJH234khj234k2jh34kjh2

3. Default region name

Type:

us-west-2

4. Default output format

Type:

json

🟢 You are DONE!

AWS CLI is now connected.

You can verify by running:

aws sts get-caller-identity

WHAT I RECOMMEND (SAFE + EASY)
If you are root user, do this:
1. Go to IAM → Users → Create User
Name it:
cli-user

2. Attach permission
Choose:
AdministratorAccess

3. Create the user
4. Open the user → Security Credentials → Create Access Key

💬 Tell me this:
How do you currently log in to AWS?
Choose one:
1️⃣ “I log in using username + password → IAM user”
2️⃣ “I log in using email + password → root user”
Tell me, and I will give exact steps for your case.
STEP 1 — Create a New IAM User

Go to AWS Console

Search IAM

On left menu → click Users

Click “Create user”

Enter details:

User name:

cli-user


Click Next.

STEP 2 — Set Permissions

You will now see options:

Choose:

➤ Attach policies directly

Then search:

AdministratorAccess


Tick the checkbox.

Click Next → then Create user.

STEP 3 — Create Access Keys

After the user is created:

Click the user cli-user

Go to Security credentials tab

Scroll to Access Keys

Click Create access key

Choose:

Command Line Interface (CLI)


Continue → you will get:

Access Key ID

Secret Access Key

💾 Save them now (you won’t see secret again after this).

STEP 4 — Configure AWS CLI on Your Laptop

Open Command Prompt and type:

aws configure


Enter:

AWS Access Key ID: <paste key>
AWS Secret Access Key: <paste secret>
Default region: us-west-2
Output format: json


Done! 🎉

✔️ Next Step (Optional)

Run this to confirm:

aws sts get-caller-identity


It should show your account details.
Go to EC2 → pick the region you want (e.g., us-west-2).
Then proceed with EKS or AWS CLI setup.
Step 1 — Ensure AWS CLI is configured

Run:

aws configure


Enter:

AWS Access Key ID: <your key>
AWS Secret Access Key: <your secret>
Default region name: us-east-1
Default output format: json

✅ Step 2 — Create the EKS Cluster (using eksctl)

Run this exact command:
eksctl create cluster --name my-eks-cluster --region us-east-1 --version 1.28 --node-type t3.small --nodes 2 --managed --with-oidc --zones us-east-1a,us-east-1b


What this will do:

Create an EKS control plane

Create a node group (EC2 worker nodes)

Set auto-scaling min 1, max 3

Use t3.medium instances (cheapest recommended)

Region = us-east-1 (your selected region)

⏳ Time: 10–15 minutes

✅ Step 3 — Update kubeconfig

After the cluster is created:

aws eks --region us-east-1 update-kubeconfig --name my-eks-cluster 

✅ Step 4 — Verify connection
kubectl get nodes


You should see 2 worker nodes (Ready).

kubectl get svc

⚠️ VERY IMPORTANT: Cost Control

To avoid unnecessary cost:

When finished, delete EVERYTHING with one command:
eksctl delete cluster --name my-eks-cluster --region us-east-1


This deletes:

Node group (EC2)

EKS control plane

VPC created by eksctl

Then no charges continue.
with no issue impppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppppp
eksctl create cluster --name my-eks-cluster --region us-east-1 --version 1.28 --node-type t3.small --nodes 2 --managed --with-oidc --zones us-east-1a,us-east-1b



C:\Users\LENOVO>aws eks --region us-east-1 update-kubeconfig --name my-eks-cluster
Added new context arn:aws:eks:us-east-1:219682413975:cluster/my-eks-cluster to C:\Users\LENOVO\.kube\config

C:\Users\LENOVO>kubectl get nodes
NAME                             STATUS   ROLES    AGE     VERSION
ip-192-168-30-238.ec2.internal   Ready    <none>   6m56s   v1.28.15-eks-c39b1d0
ip-192-168-55-9.ec2.internal     Ready    <none>   6m53s   v1.28.15-eks-c39b1d0

C:\Users\LENOVO>kubectl create deployment nginx --image=nginx
deployment.apps/nginx created

C:\Users\LENOVO>kubectl expose deployment nginx --port=80 --type=LoadBalancer
service/nginx exposed

C:\Users\LENOVO>kubectl get svc
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
kubernetes   ClusterIP      10.100.0.1      <none>                                                                   443/TCP        15m
nginx        LoadBalancer   10.100.106.45   a3bf1bd736b5e48189d79f5c5d42dcff-575232222.us-east-1.elb.amazonaws.com   80:32617/TCP   16s

C:\Users\LENOVO>kubectl get svc nginx
NAME    TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
nginx   LoadBalancer   10.100.106.45   a3bf1bd736b5e48189d79f5c5d42dcff-575232222.us-east-1.elb.amazonaws.com   80:32617/TCP   5m15s
welcome to nginx page comes

✅ STEP 1 — Delete the nginx Service (IMPORTANT)

This removes the LoadBalancer (the paid part).

Run:

kubectl delete svc nginx


You should see:

service "nginx" deleted

✅ STEP 2 — Delete the nginx Deployment

Run:

kubectl delete deployment nginx


You’ll see:

deployment.apps "nginx" deleted

🔍 Verify deletion
kubectl get svc


You should only see:

kubernetes  ClusterIP …


And:

kubectl get deployments


Should show no nginx.

🧨 STEP 3 — Delete the EKS Cluster

Now delete the entire cluster safely:

eksctl delete cluster --region us-east-1 --name my-eks-cluster


experiment 3 to deploy 2048 game in eks
Prerequisites

Before you start, make sure you have:

AWS Account with IAM user having AdministratorAccess.

AWS CLI installed and configured:

aws configure


Access Key ID: <your_access_key>

Secret Access Key: <your_secret_key>

Region: us-east-1

Output: json

kubectl installed (Kubernetes CLI).
Check with:

kubectl version --client


eksctl installed (EKS management CLI).
Check with:

eksctl version


An existing EKS cluster running (my-eks-cluster in your case).
Verify nodes are ready:


C:\Users\LENOVO>kubectl get nodes
NAME                             STATUS   ROLES    AGE   VERSION
ip-192-168-30-238.ec2.internal   Ready    <none>   95m   v1.28.15-eks-c39b1d0
ip-192-168-55-9.ec2.internal     Ready    <none>   95m   v1.28.15-eks-c39b1d0

C:\Users\LENOVO>cd eks2048

service.yaml

apiVersion: v1
kind: Service
metadata:
  name: game-2048-app-svc
spec:
  selector:
    app: game-2048-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer 

deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: game-2048-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: game-2048-app
  template:
    metadata:
      labels:
        app: game-2048-app
    spec:
      containers:
      - name: game-2048-app
        image: xurxo/2048:latest
        ports:
        - containerPort: 80

kubectl apply -f service.yaml
The Service "2048-game-app-service" is invalid: metadata.name: Invalid value: "2048-game-app-service": a DNS-1035 label must consist of lower case alphanumeric characters or '-', start with an alphabetic character, and end with an alphanumeric character (e.g. 'my-name',  or 'abc-123', regex used for validation is '[a-z]([-a-z0-9]*[a-z0-9])?')

C:\Users\LENOVO\eks2048>kubectl apply -f service.yaml

kubectl set image deployment/game-2048-app game-2048-app=twoseven1408/game-2048:latest

kubectl get pods

kubectl get svc

get 1st pods ext ip and run on server

exp 6 


Step-by-Step Summary
Step 1: Create an ECS Cluster

Go to ECS console → Clusters → Create Cluster.

Select Networking only (Fargate).

Give the cluster a name (e.g., ecs-2048-cluster).

Click Create.

Step 2: Create a Task Definition

Go to Task Definitions → Create new Task Definition → Fargate.

Specify:

Container name: e.g., 2048-game-app

Container image: Use a public image like xurxo/2048:latest or your ECR image.

Memory & CPU: e.g., 0.5 GB, 0.25 vCPU

Port mapping: container port 80 (or 8000 depending on image)

Save the task definition.

Step 3: Run a Task / Create Service

Go to ECS → Clusters → Your Cluster → Create Service

Choose Fargate as launch type, select your task definition.

Specify desired number of tasks (1 or 2 for testing).

Configure networking: select your VPC, subnets, and optionally enable public IP.

If you want public access, enable a Load Balancer.

Step 4: Access the Application

If you enabled a load balancer, go to the Load Balancer DNS URL to open the app.

If no LB, get the public IP of the Fargate task (from ECS console → Tasks → Task details → ENI → Public IP).

Open the app in your browser.

Pre-requisites

AWS Account (free tier works for Fargate small tasks).

IAM user with AdministratorAccess (or ECS + ECR full permissions).

AWS CLI installed and configured (aws configure) if using CLI for ECS commands.

ECS Console access.

Step 1: Prepare Docker Image

We’ll use a public image that works:

xurxo/2048:latest


This is already built and hosted on Docker Hub, so you don’t need Docker installed.

Step 2: Create ECS Cluster

Go to AWS Management Console → ECS → Clusters → Create Cluster.

Select Networking only (Fargate).

Name the cluster: ecs-2048-cluster.

Leave default VPC/subnets unless you want public IP access.

Click Create.

✅ Fargate handles all EC2 provisioning for you, so it avoids circuit breaker and rollback issues.

Step 3: Create Task Definition

Go to ECS → Task Definitions → Create new Task Definition.

Select Fargate as launch type.

Name the task: 2048-task.

Task Role: Leave as none (unless your container needs AWS permissions).

Task Execution Role: Create new role if not already. This allows ECS to pull images and write logs.

Network Mode: awsvpc (required for Fargate).

Operating System/Architecture: Linux/x86_64.

Task Size:

CPU: 0.25 vCPU (small task for free tier)

Memory: 0.5 GB or 1 GB

Container: Click Add container

Name: 2048-game

Image: xurxo/2048:latest

Port mappings: 80 → 80

Click Create.

Step 4: Run the Task as a Service

Go to ECS → Clusters → ecs-2048-cluster → Create → Service.

Select:

Launch type: Fargate

Task Definition: 2048-task

Service Name: 2048-service

Number of tasks: 1

Networking:

VPC: default

Subnets: pick 2 subnets for high availability

Auto-assign public IP: Enable

Load Balancer (optional for public access):

If you want browser access, choose Application Load Balancer

Otherwise, you can access via the public IP of the task later.

Click Create Service → Wait until tasks show Running.

Step 5: Access the 2048 Game

If using a Load Balancer: Use the URL provided in ECS → Services → 2048-service → Tasks → Public IP / Load Balancer DNS.

If no LB: Go to Tasks → Task → ENI → Public IP, then open http://<public-ip> in browser.

You should see the 2048 game running.

Step 6: Clean Up

Once done, delete service → delete cluster in ECS to avoid charges.

Fargate tasks are billed per second, so cleaning up avoids unnecessary cost.




lab manual
Experiment 1
Creation of EKS Server using AWS step by step procedure.
Creating an Amazon EKS (Elastic Kubernetes Service) cluster on AWS involves several steps. Below is a step-by-step
guide to set up an EKS cluster using the AWS Management Console, AWS CLI, and eksctl (a simple CLI tool for EKS).
You can choose your preferred method depending on your needs.
Prerequisites
1. AWS Account: You should have an active AWS account.
2. AWS CLI Installed: If not, install AWS CLI.
3. kubectl Installed: Kubernetes command-line tool. Install kubectl.
4. eksctl Installed: eksctl is a simple CLI tool for EKS. Install eksctl.
Step-by-Step Procedure
1. Set up AWS CLI
• Open a terminal and configure AWS CLI:
• aws configure
Enter your AWS Access Key ID, Secret Access Key, Region, and Output format.
2. Create an EKS Cluster using eksctl
The easiest way to create an EKS cluster is by using eksctl. It abstracts much of the complexity and automates tasks like
creating the EKS control plane, node groups, etc.
• Create a Cluster:
To create a basic EKS cluster, run:
• eksctl create cluster \
• --name my-eks-cluster \
• --version 1.21 \
• --region us-west-2 \
• --nodegroup-name standard-workers \
• --node-type t3.medium \
• --nodes 3 \
• --nodes-min 1 \
• --nodes-max 4 \
• --managed
o --name: Name of the cluster.
o --version: Kubernetes version.
o --region: AWS region.

o --nodegroup-name: Name of the node group.
o --node-type: EC2 instance type for the worker nodes.
o --nodes: Number of worker nodes.
o --nodes-min & --nodes-max: Minimum and maximum number of worker nodes.
o --managed: Tells eksctl to create a managed node group.
• Verify Cluster Creation:
After running the command, it will take a few minutes for the cluster to be provisioned. Once done, verify the
creation:
• kubectl get nodes
This will list your worker nodes in the EKS cluster.
3. Set up kubectl to Use Your EKS Cluster
• After the cluster is created, use the AWS CLI to update the kubeconfig:
• aws eks --region us-west-2 update-kubeconfig --name my-eks-cluster
This will configure kubectl to use the newly created EKS cluster.
4. Verify the Cluster Connection
• Verify that kubectl is connected to your cluster:
• kubectl get svc
This should return a list of services in your cluster (likely empty if you haven't deployed anything yet).
5. Create Kubernetes Deployments and Services (Optional)
• Now that the cluster is up and running, you can deploy applications to it. For example, to deploy an Nginx pod
and expose it as a service:
1. Create Deployment:
2. kubectl create deployment nginx --image=nginx
3. Expose the Deployment:
4. kubectl expose deployment nginx --port=80 --type=LoadBalancer
5. Check the Service:
6. kubectl get svc

The service will have an external IP that you can use to access the Nginx application.
6. Scale the Cluster (Optional)
You can scale your EKS cluster by adding or removing nodes to the node group:
eksctl scale nodegroup \
--cluster my-eks-cluster \
--name standard-workers \

--nodes 5 \
--region us-west-2
7. Clean Up (Optional)
Once you're done with the cluster, you can delete it to avoid ongoing costs:
eksctl delete cluster --name my-eks-cluster --region us-west-2

Experiment 2
How to install docker in aws linux EC2 instances.
Step 1: Connect to your EC2 instance
First, SSH into your EC2 instance using the following command (replace your-ec2-public-ip with your EC2's public IP
address):
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-ip
Step 2: Update the System
It's a good idea to update the package index before installing any new software. Run the following command to update
the system:
sudo yum update -y
Step 3: Install Docker
Amazon Linux 2 provides Docker in its default repositories, so you can install it using yum:
sudo yum install -y docker
This command will download and install Docker and its dependencies.
Step 4: Start the Docker Service
After Docker is installed, start the Docker service with the following command:
sudo service docker start
Step 5: Enable Docker to Start on Boot
To ensure that Docker starts automatically every time your EC2 instance reboots, run:
sudo systemctl enable docker
Step 6: Add Your User to the Docker Group (Optional but Recommended)
By default, Docker requires root privileges, but it's better to add your EC2 user (e.g., ec2-user) to the Docker group so
you can run Docker commands without sudo.
Run the following command to add your user to the Docker group:
sudo usermod -aG docker ec2-user
After adding your user to the Docker group, you need to log out and log back in for the changes to take effect. Simply
disconnect from the SSH session and then reconnect:

exit
Then log back in again:
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-ip
Step 7: Verify Docker Installation
To verify that Docker is installed and running properly, run:
docker --version
You should see the Docker version installed on your system.
Next, test Docker by running the "hello-world" image:
docker run hello-world
If everything is set up correctly, Docker will download the "hello-world" image (if not already downloaded) and print a
success message.
Step 8: (Optional) Configure Docker to Use the AWS ECR (Elastic Container Registry)
If you plan to pull Docker images from AWS ECR (Elastic Container Registry), you'll need to configure your instance to
authenticate with ECR. This can be done by running the following AWS CLI command:

aws ecr get-login-password --region <your-region> | sudo docker login --username AWS --password-stdin <aws-account-
id>.dkr.ecr.<your-region>.amazonaws.com

Replace <your-region> and <aws-account-id> with your specific AWS region and account ID.
Step 9: Install Docker Compose (Optional)
If you need Docker Compose (for managing multi-container Docker applications), you can install it with the following
commands:
1. Download the Docker Compose binary:
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -
o /usr/local/bin/docker-compose
2. Apply executable permissions to the binary:
sudo chmod +x /usr/local/bin/docker-compose
3. Verify the installation:
docker-compose --version
Step 10: Done!
You have successfully installed Docker on your Amazon Linux EC2 instance. You can now begin running containers on
your EC2 instance.

Experiment 3
How to deploy a 2048 game app on AWS EKS cluster.
Deploying a 2048 game app on an AWS EKS (Elastic Kubernetes Service) cluster involves several steps. You will
need to containerize the application, set up an EKS cluster, and deploy the containerized application on Kubernetes.
Here’s a step-by-step guide to deploy the 2048 game app on AWS EKS:
Prerequisites:
1. AWS CLI installed and configured.
2. kubectl installed.
3. eksctl installed (a command-line tool for managing AWS EKS clusters).
4. A Dockerized version of the 2048 game app (you can either build your own or use an existing one).
Steps to deploy 2048 game app on EKS:

Step 1: Prepare the 2048 Game App Docker Image
If you don’t already have a Docker image for the 2048 game app, you can use an existing one from Docker Hub or create
your own.
Example Dockerfile (if creating your own):
Here is a simple Dockerfile if you were to build the 2048 app in a web environment (HTML, CSS, JS).
# Use a basic HTTP server to serve the app
FROM python:3.8-slim

# Install dependencies
RUN pip install http.server

# Copy the 2048 game app to the container (assuming you have it locally)
COPY . /app

# Set the working directory
WORKDIR /app

# Expose port 8000
EXPOSE 8000

# Start the HTTP server to serve the app

CMD ["python3", "-m", "http.server", "8000"]
1. Build your Docker image:
2. docker build -t 2048-game-app .
3. Test locally (optional):
4. docker run -p 8000:8000 2048-game-app
5. Push your Docker image to Amazon ECR (Elastic Container Registry):
First, create an ECR repository in your AWS account:
aws ecr create-repository --repository-name 2048-game-app --region us-east-1
Then log in to ECR and push the Docker image:
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin
<aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
docker tag 2048-game-app:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/2048-game-app:latest
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/2048-game-app:latest
Replace <aws_account_id> with your AWS account ID.

Step 2: Set Up an EKS Cluster
You can use eksctl to create an EKS cluster.
1. Create the EKS cluster:
2. eksctl create cluster \
3. --name 2048-cluster \
4. --region us-east-1 \
5. --nodegroup-name standard-workers \
6. --node-type t3.medium \
7. --nodes 3 \
8. --nodes-min 1 \
9. --nodes-max 4 \
10. --managed
11. Configure kubectl to access the cluster:
12. aws eks --region us-east-1 update-kubeconfig --name 2048-cluster

Step 3: Create Kubernetes Deployment and Service Manifests
Now, let’s create Kubernetes manifests for the deployment and service.

1. Create a deployment.yaml file:
2. apiVersion: apps/v1
3. kind: Deployment
4. metadata:
5. name: 2048-game-app
6. labels:
7. app: 2048-game-app
8. spec:
9. replicas: 2
10. selector:
11. matchLabels:
12. app: 2048-game-app
13. template:
14. metadata:
15. labels:
16. app: 2048-game-app
17. spec:
18. containers:
19. - name: 2048-game-app
20. image: <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/2048-game-app:latest
21. ports:
22. - containerPort: 8000
Replace <aws_account_id> with your AWS account ID.
23. Create a service.yaml file:
24. apiVersion: v1
25. kind: Service
26. metadata:
27. name: 2048-game-app-service
28. spec:
29. selector:
30. app: 2048-game-app
31. ports:

32. - protocol: TCP
33. port: 80
34. targetPort: 8000
35. type: LoadBalancer
The LoadBalancer type service will expose the application to the internet via an external load balancer.

Step 4: Deploy the Application on EKS
Now that the Kubernetes manifests are ready, deploy them to EKS.
1. Apply the deployment and service files:
2. kubectl apply -f deployment.yaml
3. kubectl apply -f service.yaml
4. Check the status of the pods:
5. kubectl get pods
You should see pods being created and running.
6. Check the service to get the external IP address of the Load Balancer:
7. kubectl get svc
Look for the external IP in the EXTERNAL-IP column. It may take a few minutes to provision.

Step 5: Access the Game App
Once the Load Balancer is set up, you can access the 2048 game app using the external IP address from the kubectl get
svc output.
Step 6: Clean Up Resources (Optional)
When you're done, you can clean up the resources by deleting the EKS cluster and other AWS resources.
1. Delete the EKS cluster:
2. eksctl delete cluster --name 2048-cluster --region us-east-1
3. Delete the ECR repository (optional, if you no longer need it):
aws ecr delete-repository --repository-name 2048-game-app --region us-east-1 --force

Experiment 4
How to integrate jenkins in GIT Hub
Step 1: Install Jenkins and Required Plugins
1. Install Jenkins (if not already installed):
o You can follow the installation instructions for Jenkins based on your OS from Jenkins official website.
2. Install Git and GitHub Plugins in Jenkins:
o Go to Jenkins Dashboard > Manage Jenkins > Manage Plugins.
o In the Available tab, search for and install:
▪ Git Plugin
▪ GitHub Plugin

Step 2: Generate GitHub Personal Access Token (PAT)
1. Go to GitHub > Settings > Developer settings > Personal access tokens.
2. Generate a new token:
o Select the following scopes:
▪ repo (for private repositories)
▪ admin:repo_hook (for webhook creation and management)
o Click Generate Token and copy the token (you’ll need it for Jenkins).

Step 3: Configure GitHub in Jenkins
1. Go to Jenkins Dashboard > Manage Jenkins > Configure System.
2. Scroll down to the GitHub section, and click Add GitHub Server.
3. Provide a name for the GitHub server (e.g., GitHub).
4. Under Credentials, click Add and select Username with password.
o Username: Your GitHub username.
o Password: Paste the GitHub Personal Access Token (PAT) you generated earlier.
5. Click Test Connection to ensure the connection works, then click Save.

Step 4: Create a New Jenkins Job
1. Go to Jenkins Dashboard > New Item.
2. Choose Freestyle Project and give your project a name (e.g., GitHub-Integration).
3. Click OK.

Step 5: Configure GitHub Repository in Jenkins Job
1. In your new Jenkins job, go to the Source Code Management section.
2. Choose Git.
3. In the Repository URL, enter the URL of your GitHub repository (e.g., https://github.com/username/repo.git).
4. Under Credentials, choose the GitHub credentials you added earlier.
5. Save the configuration.

Step 6: Set Up Build Triggers (GitHub Webhook)
1. Scroll down to the Build Triggers section in the Jenkins job configuration.
2. Check GitHub hook trigger for GITScm polling. This will allow Jenkins to trigger builds based on GitHub
events like pushes or pull requests.

Step 7: Configure GitHub Webhook for Jenkins
1. Go to your GitHub Repository.
2. Go to Settings > Webhooks > Add webhook.
3. In the Payload URL, enter the URL of your Jenkins server’s GitHub webhook endpoint:
o Example: http://<your-jenkins-server>/github-webhook/
4. Content type: Select application/json.
5. Under Which events would you like to trigger this webhook?:
o Select Just the push event (or Let me select individual events if you want more options like pull
requests).
6. Click Add webhook.

Step 8: Test the Integration
1. Push a change or commit to your GitHub repository.
2. Go to Jenkins and check if the job triggers a build automatically.
3. If everything is set up correctly, Jenkins will start building the project whenever a new commit is pushed to
GitHub.

Step 9: (Optional) View Build Logs
You can check the build logs in Jenkins to verify if the build was successful or if there were any errors. This can be done
by: Clicking on the job name in Jenkins > Build History > Build number > Console Output.

Experiments 5
How to Build a Custom Docker Image and Run a Container
Objective: Build a custom Docker image (simple Python app) and run it on AWS EC2.
Steps:
1. Create a Python app on your EC2 instance:
SSH into your EC2 instance.
Create a simple Python app (e.g., app.py):
# app.py
from flask import Flask
app = Flask(__name__)
@app.route('/')
def hello():
return "Hello, Docker on AWS!"

if __name__ == "__main__":
app.run(host='0.0.0.0', port=5000)

step 2 : Create a Dockerfile to containerize the Python app:
In the same directory, create a Dockerfile:
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install dependencies
RUN pip install -r requirements.txt

# Expose port 5000
EXPOSE 5000

# Run app.py when the container launches
CMD ["python", "app.py"]
Create a requirements.txt file to include the necessary dependencies:
Flask
Build the Docker image:
Run the following command to build your custom Docker image:
sudo docker build -t python-flask-app .
Run the Docker container:
After building the image, run the container:
sudo docker run -d -p 5000:5000 python-flask-app
Access your Python app:
Open your browser and go to http://<your-ec2-public-ip>:5000. You should see Hello, Docker on AWS!

Experiment 6
How to Run Docker Containers with AWS ECS (Elastic Container Service)
Objective: Deploy and manage Docker containers using AWS ECS.
Steps:
1. Create an ECS Cluster:
o Go to the ECS Console in AWS.
o Click Create Cluster and choose Networking only (Fargate).
o Follow the steps to create the cluster.
2. Create a Task Definition:
o In the ECS console, go to Task Definitions and create a new Fargate task definition.
o Specify the container (e.g., your Docker image in ECR), memory, CPU, and networking configurations.
3. Run a Task on ECS:
o Create a new service and run the task in your ECS cluster.
o Specify the desired number of tasks and other settings like load balancing.
4. Access the Application:
If you've set up a load balancer, access your web application using the load balancer's URL. If not, use the ECS
task IP to access your application.
Experiment 7

How to Automatic Deployment of Code to EC2 Using GitHub Actions
Objective: Deploy code to an EC2 instance automatically when code is pushed to GitHub.
Steps:
1. Launch an EC2 Instance (Similar to previous experiments).
2. Create a GitHub Action Workflow:
o Go to the GitHub repository.
o In .github/workflows, create a file called deploy-to-ec2.yml to define your deployment process.

Example workflow for EC2:
name: Deploy to EC2

on:
push:
branches:
- main # Trigger on push to the main branch

jobs:
deploy:
runs-on: ubuntu-latest
steps:
- name: Checkout code
uses: actions/checkout@v2

- name: Deploy to EC2
env:
PRIVATE_KEY: ${{ secrets.EC2_PRIVATE_KEY }}
EC2_HOST: ${{ secrets.EC2_HOST }}
run: |
echo "$PRIVATE_KEY" > private_key.pem
chmod 600 private_key.pem
ssh -o StrictHostKeyChecking=no -i private_key.pem ec2-user@$EC2_HOST 'cd /home/ec2-user/my-app && git
pull origin main && npm install && npm start'
3. Set up SSH Keys:

o Generate an SSH key pair and add the public key to the ~/.ssh/authorized_keys file of your EC2 instance.
o Store the private key in GitHub secrets (EC2_PRIVATE_KEY).
4. Push Changes:
o Push changes to the main branch of your repository.
o The GitHub Actions workflow will automatically SSH into your EC2 instance and deploy the code (pull
from GitHub, install dependencies, and run the app).

NOTE : Take Two screenshots from each experiments and paste it in record.

