---
title: "Version compatibility reference for Astronomer Software"
sidebar_label: "Version compatibility reference"
id: version-compatibility-reference
description: A reference of all adjacent tooling required to run Astronomer Software and corresponding version compatibility.
---

Astronomer Software ships with and requires a number of adjacent technologies that support it, including Kubernetes, Helm, and Apache Airflow itself. This guide provides a reference of all required tools and versions for running Astronomer Software.

While the tables below reference the minimum compatible versions, we typically recommend running the latest versions of all tooling if and when possible.

<Tip>Find detailed information about the component image versions, including which versions were used to test a particular Astronomer Software version in the [Astronomer Software release index](https://updates.astronomer.io/astronomer-software/releases/index.html).</Tip>

## Astronomer Software

<!--- Version-specific -->

The following table shows version compatibility information for all currently supported versions of Astronomer Software and some legacy versions. Check [Astronomer Software lifecycle schedule](release-lifecycle-policy.md#software-lifecycle-schedule) for more information about supported versions of Astronomer Software.

| Astronomer Platform | Postgres | Astro Runtime                    |
| ------------------- | -------- | -------------------------------- |
| v0.34               | 13+      | All Airflow 2.x Runtime versions |
| v0.35               | 13+      | All Airflow 2.x Runtime versions |
| v0.36               | 13+      | All Airflow 2.x Runtime versions |
| v0.37               | 13+      | All Airflow 2.x Runtime versions |

See [Kubernetes version support table and policy](#kubernetes-version-support-table-and-policy) for Astronomer platform compatibility with Kubernetes.

Astronomer does not support Postgres versions that are beyond their end-of-life date. You can check to see the [currently supported versions of Postgres](https://www.postgresql.org/support/versioning/).

Astronomer recommends using the latest available version of the Astro CLI for all Software versions in most cases. To upgrade from an earlier version of the CLI to the latest, see [Upgrade to Astro CLI version 1.0+](upgrade-astro-cli.md).

For more detail about the changes in each Astronomer Software release, see the [Astronomer Software Release Notes](release-notes.md).

All currently supported Astronomer-distributed images are compatible with all versions of Astronomer Software. Astro Runtime maintenance is independent of Software maintenance. For more information, see [Astro Runtime maintenance and lifecycle policy](runtime-version-lifecycle-policy.mdx).

### Kubernetes version support table and policy

In general, Astronomer Software will support a given version of Kubernetes through its End of Life. This includes Kubernetes upstream and cloud-managed variants like GKE, AKS, and EKS. When a version of Kubernetes reaches End of Life, support will be removed in the next major or minor release of Astronomer Software. For more information on Kubernetes versioning and release policies, refer to [Kubernetes Release History](https://kubernetes.io/releases/) or your cloud provider.

See the following table for all supported Kubernetes versions in each maintained version of Astronomer Software.

| Astronomer platform | Kubernetes 1.24 | 1.25 | 1.26 | 1.27 | 1.28 | 1.29 | 1.30 | 1.31 | 1.32 |
| :-----------------: | :-------------: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|       0.34.0        |       ✔️        |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |      |      |      |
|   0.34.1 - 0.34.3   |                 |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |      |      |
|   0.34.4 - 0.34.5   |                 |      |      |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |
|       0.35.0        |                 |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |      |
|   0.35.1 - 0.35.4   |                 |      |      |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |
|   0.36.0 - 0.36.1   |                 |      |      |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |
|   0.37.0 - 0.37.1   |                 |      |      |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |      |
|    0.37.2-0.37.4    |                 |      |      |      |  ✔️  |  ✔️  |  ✔️  |  ✔️  |  ✔️  |

### General recommendations for Kubernetes upgrades

If there are no workloads running on the nodes you want to upgrade, there won't be an immediate impact on the Astronomer or Airflow components during the initial phase of upgrading your managed node groups. To minimize disruptions, however, perform a controlled rollout restart of the worker nodes. During your controlled rollout, monitor the health of the new nodes and workloads before decommissioning the old nodes.

Before beginning the upgrade process, ensure you have all necessary backups ready. After upgrading, verify that all Astronomer and Airflow components are running as expected on the new nodes. After the Astronomer version is compatible with the EKS/AKS Cluster, you don't need to change you Astronomer configurations or settings. However, the upgrade requires restarting the Kubelet on each node, which causes the Astro and Airflow components to also restart.

For more information on upgrading Kubernetes versions, follow the guidelines offered by your cloud provider.

- [Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)
- [Azure AKS](https://docs.microsoft.com/en-us/azure/aks/upgrade-cluster)
- [Google GKE](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-upgrades)
- [RedHat OpenShift](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html/updating_clusters/index)

## Airflow chart compatibility reference

Astronomer Software Deployments utilize the [Astronomer-distributed Helm chart for Apache Airflow](https://github.com/astronomer/airflow-chart). A Deployment's Airflow chart defines how a Deployment autoscales Pods and interacts with other components in your cluster.

Use the following table to see the Airflow Helm chart version for each supported version of Astronomer Software. To view the Airflow Helm chart for an unsupported version of Astronomer Software, open the default Astronomer Helm chart in the [`astronomer/astronomer` repository](https://github.com/astronomer/astronomer/blob/master/charts/astronomer/values.yaml) and select the **Tag** that corresponds to the unsupported version. The value of `airflowChartVersion` is the Airflow Helm chart version.

| Astronomer platform version | Astronomer Airflow Helm chart version |
| --------------------------- | ------------------------------------- |
| 0.34.0                      | 1.10.0                                |
| 0.34.1                      | 1.10.0                                |
| 0.34.2                      | 1.10.2                                |
| 0.34.3                      | 1.10.2                                |
| 0.34.4                      | 1.10.4                                |
| 0.35.0                      | 1.11.0                                |
| 0.35.1                      | 1.11.0                                |
| 0.35.2                      | 1.11.0                                |
| 0.35.3                      | 1.11.4                                |
| 0.35.4                      | 1.11.4                                |
| 0.36.0                      | 1.13.5                                |
| 0.36.1                      | 1.13.10                               |
| 0.37.0                      | 1.14.0                                |
| 0.37.1                      | 1.14.3                                |
| 0.37.2                      | 1.14.5                                |
| 0.37.3                      | 1.15.2                                |
| 0.37.4                      | 1.15.5                                |

## Legacy version compatibility reference

The following table shows version compatibility information for all versions of Astronomer Software which are no longer supported:

| Astronomer Platform | Kubernetes                                  | Postgres | Astro Runtime                                |
| ------------------- | ------------------------------------------- | -------- | -------------------------------------------- |
| v0.26              | 1.17, 1.18, 1.19, 1.20, 1.21                | 9.6+     | All Astronomer Certified versions            |
| v0.27              | 1.18, 1.19, 1.20, 1.21                      | 9.6+     | All Astronomer Certified versions            |
| v0.28              | 1.19¹, 1.20¹, 1.21, 1.22, 1.23, 1.24        | 9.6+     | All Astronomer Certified versions            |
| v0.29              | 1.19¹, 1.20¹, 1.21, 1.22, 1.23, 1.24        | 9.6+     | All supported Certified and Runtime versions |
| v0.30              | 1.22¹, 1.23, 1.24, 1.25, 1.26, 1.27¹        | 11+      | All Runtime versions                         |
| v0.31              | 1.21, 1.22, 1.23, 1.24, 1.25¹, 1.26¹        | 11.19+   | All Runtime versions                         |
| v0.32              | 1.22¹, 1.23, 1.24¹, 1.25, 1.26, 1.27, 1.29¹ | 11+      | All Runtime versions                         |
| v0.33              | 1.24, 1.25, 1.26, 1.27, 1.28, 1.29          | 11+      | All Runtime versions                         |


<Info>Due to the [deprecation of Dockershim](https://kubernetes.io/blog/2020/12/02/dockershim-faq/), Azure does not support private Certificate Authorities (CAs) starting with Kubernetes 1.19. If your organization is using a private CA, contact [Astronomer support](https://support.astronomer.io) before upgrading to Kubernetes 1.19 on Azure Kubernetes Service (AKS).</Info>

<Info>

¹ Support for some Kubernetes versions is limited to specific Astronomer Software patch versions. You can find the specific versions supported by a particular Software patch starting with version 0.32.4 in the [Release index](https://updates.astronomer.io/astronomer-software/releases/index.html).

- Support for Kubernetes 1.19 and 1.20 ends with Astronomer Software versions 0.28.7 and 0.29.5.
- Support for Kubernetes 1.22 ends with Astronomer Software version 0.32.2.
- Support for Kubernetes 1.23 ends with Astronomer Software version 0.32.4.
- Support for Kubernetes 1.25 and 1.26 starts in Astronomer Software 0.31.2.
- Support for Kubernetes 1.27 starts in Astronomer Software 0.30.8.
- Support for Kubernetes 1.28 starts in Astronomer Software 0.32.4. It is not available for version 0.33.0.
- Support for Kubernetes 1.29 is available in Astronomer Software 0.32.6, and all versions greater than 0.33.6.

</Info>
