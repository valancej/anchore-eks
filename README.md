# Anchore on Amazon Elastic Kubernetes Service (EKS)

## Prerequisites

Verify that you have access to and understand the following as they will be utilized throughout this guide:

- [eksctl](https://eksctl.io/)
- [Cluster Autoscaler on AWS](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler/cloudprovider/aws)
- [Helm](https://helm.sh/)
- [Anchore Helm chart](https://github.com/helm/charts/tree/master/stable/anchore-engine)
- [Prometheus Helm chart](https://github.com/helm/charts/tree/master/stable/prometheus)*
- [Grafana Helm chart](https://github.com/helm/charts/tree/master/stable/grafana)*

*Only needed if you are intending to use these for systems and service monitoring and visualization.

## Create an EKS cluster

Create an EKS cluster with at minimum 2 worker nodes (Auto-Scaling Groups are preferrable) with a total cluster capacity of 8 CPU and 32 GB of memory (more is recommend to scale out Anchore analyzer services). For more infomation on sizing, please refer to the section [capacity planning](#capacity-planning).

This guide creates a EKS cluster with [eksctl](https://eksctl.io/) using the [ClusterConfig](examples/cluster.yaml) under the examples directory.

**Note**: The ClusterConfig above utilizes the [Bottlerocket OS](https://github.com/bottlerocket-os/bottlerocket) for the worker nodes. Please refer to the GitHub repository for more information. 

### Cluster Autoscaler

**Note**: The following is optional and not required for installation of Anchore. However, it is highly recommended you architect your cluster appropriate with the correct resources and services to enable scalability.

Configure and install the [AWS CLuster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler/cloudprovider/aws). 