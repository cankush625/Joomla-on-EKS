# Joomla-on-EKS
Production ready code to deploy Joomla on AWS-EKS

## Getting started
### Step1: Create EKS cluster and configure the kubeclt command for the launched cluster
`$ aws eks update-kubeconfig --name mycluster`
### Step2: Install Amazon EFS Utilities on every node in the cluster using following command:
`$ yum install amazon-efs-utils`
### Step3: Create namespace for the task
`$ kubectl create namespace webns`
### Step4: Create an EFS file system
### Step5: In *create-efs-provisioner.yaml* file, replace the <Strong>FILE_SYSTEM_ID</strong> at line no. 22 and replace the <strong>nfs server</strong> at line no. 33 with the values of your EFS file system
### Step6: Create the *EFS Provisioner*, *Role* and *Storage Class* in the *webns* namespace using following commands:
`$ kubectl create -f create-efs-provisioner.yaml -n webns` <br>
`$ kubectl create -f create-rbac.yaml -n webns` <br>
`$ kubectl create -f create-storage.yaml -n webns`
### Step7: Run the *kustomization.yaml* file to setup the environment and deploy the Joomla to the EKS. Run the following command:
`$ kubectl create -k .`
### Step8: Now our Joomla site is deployed to the EKS and can be accessed using the <strong>EXTERNAL-IP</strong> provided by joomla service.
`$ kubectl get all`<br>
### open the <strong>EXTERNAL-IP</strong> provided by the <strong>service/joomla</strong> in the browser to view the deployed joomla site.