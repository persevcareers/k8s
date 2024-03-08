## Installation of NGINX Ingress Controller on Google Kubernetes Cluster,GKE

Creating a GKE Cluster,

Create a GKE cluster using GCP Console.

Once cluster is available , to connect with the cluster ensure to installa gcloud cli and authlogin tools

Installation gcloud CLI : https://cloud.google.com/sdk/docs/install on windows.

```bash
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")

& $env:Temp\GoogleCloudSDKInstaller.exe
```
Install authentication ,
```bash
gcloud components install gke-gcloud-auth-plugin
gke-gcloud-auth-plugin --version
```
To install the NGINX Ingress Controller on your Kubernetes cluster, follow these steps:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
```
It creates all different required resources in ingress-nginx namespace.

Deployment of application , 
kubectl apply of deployment-v1.yml and deployment-v2.yml two different paths with two different versions of a product.

Deploy your application with manifest which have dpeloyment and svc as well.

Post which , we can now deploy ingress resources which will be deploy gets external ip of the load balancer deployed during nginx ingress controller installation.
