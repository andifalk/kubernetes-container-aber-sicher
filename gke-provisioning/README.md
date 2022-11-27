# Demo K8s cluster on Google Cloud

Here you find helpful scripts to set up & access
GKE on Google Cloud:

* create-gke.sh: Create a GKE cluster _demo-gke_ with 4 nodes and application level secrets encryption
* access-gke.sh: Add entry to Kubectl config to access the GKE cluster _demo-gke_ (if you have created the cluster via UI and not via script)
* install-prometheus.sh: Install Prometheus Operator using Helm 3
* update-gke-pod-security.sh: Enable Pod Security Policies on the GKE cluster _demo-gke_
* delete-gke.sh: Delete the GKE cluster _demo-gke_

## Prerequisites

You need:
* a valid account to access Google Cloud and be able to use the Google API for creating a GKE cluster.
* installed google cloud cli (see <https://cloud.google.com/sdk/docs/install> for details)
* installed gke plugin for kubectl (just perform `gcloud components install gke-gcloud-auth-plugin` after you have installed the Google cloud cli)

## Login to Google Cloud

You need an account on Google Cloud, and you have to log in to your account via

```shell
gcloud auth login
```

before executing any script here.

## Create GKE cluster

__NOTE:__ Please open and edit the file _create-gke.sh_ before executing and change the project to your own one first.

Now you can run _create-gke.sh_ to create a GKE cluster.

After running _create-gke.sh_ script wait until you see the final running status line (similar to this one):

```shell
NAME      LOCATION        MASTER_VERSION  MASTER_IP       MACHINE_TYPE   NODE_VERSION  NUM_NODES  STATUS
demo-gke  europe-west3-a  1.15.9-gke.8    35.242.252.226  n1-standard-2  1.15.9-gke.8  4          RUNNING
```

## Get access to the cluster

After successfully creating the cluster you can access the cluster by running _access-gke.sh_.

You may need to install the gke plugin for kubectl by performing `gcloud components install gke-gcloud-auth-plugin`

## Install Prometheus Operator and Grafana for Monitoring

You may also install Prometheus Operator for monitoring the cluster using _install-prometheus.sh_ script.
Please make sure you have installed [Helm 3.x](https://github.com/helm/helm#install) before executing this script.

After running the script you can access the Grafana web page by navigating to [localhost:3000](http://localhost:3000).
Login credentials are: _admin/prom-operator_.

There are predefined dashboards under _Manage Dashboards_.
Interesting ones are:

1. USE Method / Cluster
2. Use Method / Node
3. Kubernetes / Compute Resources / Pod

When you select the one for the cluster it looks like the following image.

![Grafana](images/grafana.png)

## Delete GKE cluster again

After playing around with the GKE cluster and running all demos you can delete the cluster using the script _delete-gke.sh_ again to save money.
