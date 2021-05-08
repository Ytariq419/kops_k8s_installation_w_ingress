**Create the cluster using KOPS**

**Prerequisite**
1. AWS Account
2. kubectl
3. kops
4. helm

Create a S3 bucket to store our clusters state:

``
$ aws s3 mb s3://clusters.dev.serverlessglobe.com
``

Export KOPS_STATE_STORE=s3://clusters.dev.serverlessglobe.com and then kops will use this location by default:

``
$ export KOPS_STATE_STORE=s3://clusters.dev.serverlessglobe.com       
``

Create a cluster configuration. While the following command does NOT actually create the cloud resources it gives us an opportunity to review the configuration or change it:

``
$ kops create cluster --zones=us-east-1a,us-east-1b,us-east-1c useast1.dev.serverlessglobe.com 
``



``kops create cluster --dns private $NAME``

If you have a mix of public and private zones, you will also need to include the --dns-zone argument with the hosted zone id you wish to deploy in:

``kops create cluster --dns private --dns-zone ZABCDEFG $NAME``


``kops get clusters``

``aws ec2 describe-availability-zones --region us-east-1``

``kops create cluster --zones=us-east-1a,us-east-1b,us-east-1c — ${NAME}``

``kops update cluster --name serverlessglobe.com --yes --admin``

``kops validate cluster --wait 10m``

``kubectl get nodes``



``export NAME=serverlessglobe.com``

``export KOPS_STATE_STORE=s3://serverlessglobe.com``

``kops create cluster --zones=us-east-1a,us-east-1b,us-east-1c --master-count 3 --master-size t3.medium --node-count 3 --node-size t3.medium ${NAME}``

``kops update cluster --name serverlessglobe.com --yes --admin``

``kops validate cluster --wait 10m``


``helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx``

``helm repo update``

``kubectl get ns``

``kubectl create ns ingress-nginx``

``helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx``

  

``kubectl get pods -n ingress-nginx``
``OUTPUT: 
NAME                                        READY     STATUS    RESTARTS   AGE
ingress-nginx-controller-57cb5bf694-nm25k   1/1       Running   0          1m
``

**CLEAN UP:**

``kops delete cluster serverlessglobe.com --yes``
