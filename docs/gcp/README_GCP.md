# CADANAC - A System and Method for tracking Covid19 and multiple host infections using Google Cloud, Kubernetes and Hyperledger Fabric


**Maintainers:** [hrad-h](https://github.com/hrad-h/)

Cadanac uses Google Cloud PAAS.  Here are the steps:

### Step 1: First create a VPC to share your local area network with many GCE instances

```sh
gcloud compute --project=rich-tome-267821 networks create vpc-cadanac-1 --subnet-mode=auto
```
or using the GCP web control panel
![gcp_vpc.png](https://github.com/hrad-h/c1/blob/master/docs/gcp/images/gcp_vpc.png)


