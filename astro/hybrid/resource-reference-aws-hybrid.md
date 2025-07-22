---
sidebar_label: "AWS Hybrid cluster settings"
title: "AWS Hybrid cluster settings"
id: resource-reference-aws-hybrid
description: Reference of all supported configurations for new Astro clusters on Amazon Web Services.
sidebar_custom_props: { icon: "img/aws.png" }
---

:::warning

This document applies only to [Astro Hybrid](hybrid-overview.md). To see whether you're an Astro Hybrid user, click **Organization Settings**. Your Astro product type is listed under **Product Type** on the **General** page.

To create a cluster on Astro Hosted, see [Create a dedicated cluster](create-dedicated-cluster.md).

:::

Unless otherwise specified, new clusters on Astro are created with a set of default AWS resources that should be suitable for most use cases.

Read the following document for a reference of our default resources as well as supported cluster configurations.

## Default cluster values

| Resource                                                                                                                                          | Description                                                                                                                                                                                                                                                                                                                                              | Quantity/ Default Size                        | Configurable                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [EKS Cluster](https://aws.amazon.com/eks)                                                                                                         | An EKS cluster is required to run the Astro data plane, which hosts the resources and data required to execute Airflow tasks.                                                                                                                                                                                                                            | 1x                                            |                                                                                                              |
| Worker node pool                                                                                                                                  | A node pool of [EC2 instances](https://aws.amazon.com/ec2/instance-types/) that hosts all workers with the `default` worker type for all Deployments in the cluster. The number of nodes in the pool auto-scales based on the demand for workers in your cluster. You can configure additional worker node pools to run tasks on different worker types. | 1x pool of m5.xlarge nodes                    | Yes. See [Manage worker node pools](manage-hybrid-clusters.md#about-worker-node-pools).                      |
| Airflow node pool                                                                                                                                 | A node pool of [EC2 instances](https://aws.amazon.com/ec2/instance-types/) that runs all core Airflow components, including the scheduler and webserver, for all Deployments in the cluster. This node pool is fully managed by Astronomer.                                                                                                              | 1x pool of m5.xlarge nodes                    |                                                                                                              |
| Astro system node pool                                                                                                                            | A node pool of [EC2 instances](https://aws.amazon.com/ec2/instance-types/) that runs all other system components required in Astro. The availability zone determines how many nodes are created.  This node pool is fully managed by Astronomer.                                                                                                         | 1x pool of m5.xlarge nodes                    |                                                                                                              |
| [RDS for PostgreSQL Instance](https://aws.amazon.com/rds/)                                                                                        | The RDS instance is the primary database of the Astro data plane. It hosts a metadata database for each Deployment in the cluster. All RDS instances on Astro are multi-AZ.                                                                                                                                                                              | 1x db.m6g.large                               | Yes. See [Configure your relational database](manage-hybrid-clusters.md#configure-a-database-instance-type). |
| [Elastic IPs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)                                                  | Required for connectivity with the Astro control plane and other public services.                                                                                                                                                                                                                                                                        | 2x                                            |                                                                                                              |
| [Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)                                                                      | Subnets are provisioned in 2 different [Availability Zones (AZs)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) for redundancy, with 1 public and 1 private subnet per AZ. Public subnets are required for the NAT and Internet gateways, while private subnets are required for EC2 nodes.                                        | 2x /26 (public) and 1x /21 + 1x /22 (private) | Yes. See [Connect Astro to AWS data sources](connect-aws.md).                                                |
| [Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)                                                    | Required for connectivity with the control plane and other public services.                                                                                                                                                                                                                                                                              | 1x                                            |                                                                                                              |
| [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)                                                             | NAT Gateways translate outbound traffic from private subnets to public subnets.                                                                                                                                                                                                                                                                          | 2x                                            |                                                                                                              |
| [Routes](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html#route-table-routes)                                               | Routes are necessary to direct network traffic from the subnets and gateways.                                                                                                                                                                                                                                                                            | 2x                                            |                                                                                                              |
| [Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)                                                            | Home for the routes.                                                                                                                                                                                                                                                                                                                                     | 2x                                            |                                                                                                              |
| [VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)                                                                   | Virtual network for launching and hosting AWS resources.                                                                                                                                                                                                                                                                                                 | 1x /20                                        | Yes. See [Connect Astro to AWS data sources](connect-aws.md).                                                |
| [VPC Interface Endpoint Services](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/what-are-vpc-endpoints.html#interface-endpoints) | Enables AWS PrivateLink connectivity to Elastic Load Balancing (ELB), AWS Auto Scaling plans, AWS Security Token Service (AWS STS), and Amazon Elastic Container Registry (ECR) Docker and API services.                                                                                                                                                 | 5x                                            |                                                                                                              |
| [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide//Welcome.html)                                                                  | Stores Airflow task logs.                                                                                                                                                                                                                                                                                                                                | 1x                                            |                                                                                                              |
| [S3 Gateway Endpoint](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/what-are-vpc-endpoints.html#gateway-endpoints)               | IP routes for Amazon Simple Storage Service (Amazon S3)                                                                                                                                                                                                                                                                                                  | 1x                                            |                                                                                                              |

## Supported cluster regions

You can host Astro Hybrid clusters in the following AWS regions:

| Code             | Name                      |
| ---------------- | ------------------------- |
| `af-south-1`     | Africa (Cape Town)        |
| `ap-east-1`      | Asia Pacific (Hong Kong)  |
| `ap-northeast-1` | Asia Pacific (Tokyo)      |
| `ap-northeast-2` | Asia Pacific (Seoul)      |
| `ap-northeast-3` | Asia Pacific (Osaka)      |
| `ap-southeast-1` | Asia Pacific (Singapore)  |
| `ap-southeast-2` | Asia Pacific (Sydney)     |
| `ap-south-1`     | Asia Pacific (Mumbai)     |
| `ca-central-1`   | Canada (Central)          |
| `eu-central-1`   | Europe (Frankfurt)        |
| `eu-south-1`     | Europe (Milan)            |
| `eu-west-1`      | Europe (Ireland)          |
| `eu-west-2`      | Europe (London)           |
| `eu-west-3`      | Europe (Paris)            |
| `me-south-1`     | Middle East (Bahrain)     |
| `sa-east-1`      | South America (São Paulo) |
| `us-east-1`      | US East (N. Virginia)     |
| `us-east-2`      | US East (Ohio)            |
| `us-west-1`      | US West (N. California)   |
| `us-west-2`      | US West (Oregon)          |

Modifying the region of an existing cluster on Astro is not supported. If you're interested in an AWS region that isn't listed, contact [Astronomer support](https://cloud.astronomer.io/open-support-request).

## Supported RDS instance types

The following AWS RDS instance types are supported on Astro:

### db.m6g

- db.m6g.large (_default_)
- db.m6g.xlarge
- db.m6g.2xlarge
- db.m6g.4xlarge
- db.m6g.8xlarge
- db.m6g.12xlarge
- db.m6g.16xlarge

### db.r6g

- db.m6g.large (_default_)
- db.m6g.xlarge
- db.m6g.2xlarge
- db.m6g.4xlarge
- db.m6g.8xlarge
- db.m6g.12xlarge
- db.m6g.16xlarge

### db.r5

- db.r5.large
- db.r5.xlarge
- db.r5.2xlarge
- db.r5.4xlarge
- db.r5.8xlarge
- db.r5.12xlarge
- db.r5.16xlarge
- db.r5.24xlarge

### db.m5

- db.m5.large
- db.m5.xlarge
- db.m5.2xlarge
- db.m5.4xlarge
- db.m5.8xlarge
- db.m5.12xlarge
- db.m5.16xlarge
- db.m5.24xlarge

For detailed information about each instance type, see [Amazon RDS Instance Types](https://aws.amazon.com/rds/instance-types/). If you're interested in an RDS instance type that is not on this list, contact [Astronomer support](https://cloud.astronomer.io/open-support-request).

## Supported worker node pool instance types

<!-- For new node instance types, subtract 2 CPU and 1.5 GiB RAM from the listed  figures in the cloud provider's reference page-->

Each worker in a worker node pool runs a single worker Pod. A worker Pod's actual available size is equivalent to the total capacity of the instance type minus Astro’s system overhead.

The following table lists all available instance types for worker node pools, as well as the Pod size that is supported for each instance type. As the system requirements of Astro change, these values can increase or decrease.

| Worker Node Type | CPU     | Memory         |
| ---------------- | ------- | -------------- |
| m5.xlarge        | 2 CPUs  | 14.5 GiB MEM   |
| m5.2xlarge       | 6 CPUs  | 30.5 GiB MEM   |
| m5.4xlarge       | 14 CPUs | 62.5 GiB MEM   |
| m5.8xlarge       | 30 CPUs | 126.5 GiB MEM  |
| m5.12xlarge      | 46 CPUs | 190.5 GiB MEM  |
| m5.16xlarge      | 62 CPUs | 254.5 GiB MEM  |
| m5.24xlarge      | 94 CPUs | 382.5 GiB MEM  |
| m5.metal         | 94 CPUs | 382.5 GiB MEM  |
| m5d.xlarge       | 2 CPUs  | 14.5 GiB MEM   |
| m5d.2xlarge      | 6 CPUs  | 30.5 GiB MEM   |
| m5d.4xlarge      | 14 CPUs | 62.5 GiB MEM   |
| m5d.8xlarge      | 30 CPUs | 126.5 GiB MEM  |
| m5d.12xlarge     | 46 CPUs | 190.5 GiB MEM  |
| m5d.16xlarge     | 62 CPUs | 254.5 GiB MEM  |
| m5d.24xlarge     | 94 CPUs | 382.5 GiB MEM  |
| m5d.metal        | 94 CPUs | 382.5 GiB MEM  |
| m6i.xlarge       | 2 CPUs  | 14.5 GiB MEM   |
| m6i.2xlarge      | 6 CPUs  | 30.5 GiB MEM   |
| m6i.4xlarge      | 14 CPUs | 62.5 GiB MEM   |
| m6i.8xlarge      | 30 CPUs | 126.5 GiB MEM  |
| m6i.12xlarge     | 46 CPUs | 190.5 GiB MEM  |
| m6i.16xlarge     | 62 CPUs | 254.5 GiB MEM  |
| m6i.24xlarge     | 94 CPUs | 382.5 GiB MEM  |
| m6i.metal        | 94 CPUs | 382.5 GiB MEM  |
| m6id.xlarge      | 2 CPUs  | 14.5 GiB MEM   |
| m6id.2xlarge     | 6 CPUs  | 30.5 GiB MEM   |
| m6id.4xlarge     | 14 CPU  | 62.5 GiB MEM   |
| m6id.8xlarge     | 30 CPU  | 126.5 GiB MEM  |
| m6id.12xlarge    | 46 CPU  | 190.5 GiB MEM  |
| m6id.16xlarge    | 62 CPU  | 254.5 GiB MEM  |
| m6id.24xlarge    | 94 CPU  | 382.5 GiB MEM  |
| m6id.metal       | 126 CPU | 510.5 GiB MEM  |
| r6i.xlarge       | 2 CPUs  | 30.5 GiB MEM   |
| r6i.2xlarge      | 6 CPUs  | 62.5 GiB MEM   |
| r6i.4xlarge      | 14 CPUs | 126.5 GiB MEM  |
| r6i.8xlarge      | 30 CPUs | 254.5 GiB MEM  |
| r6i.12xlarge     | 46 CPUs | 382.5 GiB MEM  |
| r6i.16xlarge     | 62 CPUs | 510.5 GiB MEM  |
| r6i.24xlarge     | 94 CPUs | 766.5 GiB MEM  |
| r6i.metal        | 94 CPUs | 1022.5 GiB MEM |
| c6i.xlarge       | 2 CPUs  | 6.5 GiB MEM    |
| c6i.2xlarge      | 6 CPUs  | 14.5 GiB MEM   |
| c6i.4xlarge      | 14 CPUs | 30.5 GiB MEM   |
| c6i.8xlarge      | 30 CPUs | 62.5 GiB MEM   |
| c6i.12xlarge     | 46 CPUs | 94.5 GiB MEM   |
| c6i.16xlarge     | 62 CPUs | 126.5 GiB MEM  |
| c6i.24xlarge     | 94 CPUs | 190.5 GiB MEM  |
| c6i.metal        | 126 CPUs |  254.5 GiB MEM  |
| t2.xlarge        | 2 CPUs  | 14.5 GiB MEM   |
| t3.xlarge        | 2 CPUs  | 14.5 GiB MEM   |
| t3.2xlarge       | 6 CPUs  | 30.5 GiB MEM   |

If your Organization is interested in using an instance type that supports a larger worker size, contact [Astronomer support](https://cloud.astronomer.io/open-support-request). For more information about configuring worker size on Astro, see [Deployment resources](deployment-resources.md).

:::warning

Astronomer doesn’t recommend using `t` series instance types in standard mode for production workloads, because CPU utilization for `t` instance types in standard mode can be throttled.

:::

### Ephemeral storage

With the exception of `m5d` and `m6id` nodes, all supported node types have a maximum of 20GiB of storage per node for system use only. If you need locally attached storage for task execution, Astronomer recommends modifying your cluster to run `m5d` or `m6id` nodes, which AWS provisions with NVMe SSD volumes. To utilize the ephemeral storage on these node types, have your task write data to `/ephemeral`. If your task uses the KubernetesPodOperator, [mount an emptyDir volume](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir-configuration-example) in your operator [container spec](https://airflow.apache.org/docs/apache-airflow-providers-cncf-kubernetes/stable/operators.html#how-to-use-cluster-configmaps-secrets-and-volumes-with-pod) instead. See [Amazon EC2 M6i Instances](https://aws.amazon.com/ec2/instance-types/m6i/) and [Amazon EC2 M5 Instances](https://aws.amazon.com/ec2/instance-types/m5/) for the amount of available storage in each node type.

If you need to pass significant data between Airflow tasks, Astronomer recommends using an [XCom backend](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/xcoms.html#custom-xcom-backends) such as [AWS S3](https://aws.amazon.com/s3/) or [Google Cloud Storage (GCS)](https://cloud.google.com/storage). For more information and best practices, see the Airflow Guide on [Passing Data Between Airflow Tasks](https://www.astronomer.io/docs/learn/airflow-passing-data-between-tasks).

## Related documentation

- [Manage and modify Hybrid clusters](manage-hybrid-clusters.md)
