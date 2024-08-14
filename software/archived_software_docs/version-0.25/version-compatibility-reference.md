---
title: "Version Compatibility Reference for Astronomer Software"
sidebar_label: "Version Compatibility Reference"
id: version-compatibility-reference
description: A reference of all adjacent tooling required to run Astronomer Software and corresponding version compatibility.
---

## Overview

Astronomer Software ships with and requires a number of adjacent technologies that support it, including Kubernetes, Helm, and Apache Airflow itself. This guide provides a reference of all required tools and versions for running Astronomer Software. This guide also includes a version compatibility reference table for running [Astronomer Certified](image-architecture.md) outside of the context of the Astronomer platform.

While the tables below reference the minimum compatible versions, we typically recommend running the latest versions of all tooling if and when possible.

## Astronomer Software

<!--- Version-specific -->

| Astronomer Platform | Kubernetes                           | Postgres | Python                                    | Astronomer Certified / Astro Runtime         | Helm |
| ------------------- | ------------------------------------ | -------- | ----------------------------------------- | -------------------------------------------- | ---- |
| v0.25               | 1.17¹, 1.18¹, 1.19¹, 1.20¹, 1.21     | 9.6+     | 3.6, 3.7, 3.8, 3.9 (_requires AC 2.2.0+_) | All supported Certified versions*            | 3.6  |
| v0.28               | 1.19¹, 1.20¹, 1.21, 1.22, 1.23, 1.24 | 9.6+     | 3.6, 3.7, 3.8, 3.9 (_requires AC 2.2.0+_) | All supported Certified versions             | 3.6  |
| v0.29               | 1.19¹, 1.20¹, 1.21, 1.22, 1.23, 1.24 | 9.6+     | 3.6, 3.7, 3.8, 3.9 (_requires AC 2.2.0+_) | All supported Certified and Runtime versions | 3.6  |
| v0.30               | 1.19¹, 1.20¹, 1.21, 1.22, 1.23, 1.24 | 9.6+     | 3.6, 3.7, 3.8, 3.9 (_requires AC 2.2.0+_) | All supported Certified and Runtime versions | 3.6  |

Astronomer recommends using the latest available version of the Astro CLI for all Software versions in most cases. To upgrade from an earlier version of the CLI to the latest, see [Upgrade to Astro CLI version 1.0+](upgrade-astro-cli.md).

:::info

¹ Support for some Kubernetes versions is limited to specific Astronomer Software patch versions.

- Support for Kubernetes 1.17 ends with Astronomer Software 0.25.12.
- Support for Kubernetes 1.18 ends with Astronomer Software 0.25.13.
- Support for Kubernetes 1.19 and 1.20 ends with Astronomer Software versions 0.25.15, 0.28.7, 0.29.5, and 0.30.4.

:::

For more detail about the changes in each Astronomer Software release, see the [Astronomer Software Release Notes](release-notes.md).

All currently supported Astronomer-distributed images are compatible with all versions of Astronomer Software. Astronomer Certified and Astro Runtime maintenance is independent of Software maintenance. For more information, see:

- [Astro Runtime maintenance and lifecycle policy](runtime-version-lifecycle-policy.md)
- [Astronomer Certified versioning and support](ac-support-policy.md)

:::info

Due to the [deprecation of Dockershim](https://kubernetes.io/blog/2020/12/02/dockershim-faq/), Azure does not support private Certificate Authorities (CAs) starting with Kubernetes 1.19. If your organization is using a private CA, contact [Astronomer support](https://support.astronomer.io) before upgrading to Kubernetes 1.19 on Azure Kubernetes Service (AKS).

:::

:::info

While Astronomer v0.25 is compatible with Astronomer Certified 2.2.0, support for the Airflow triggerer is available only in Astronomer v0.26 and later. To use [deferrable operators](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/deferring.html), that require the Airflow triggerer, you must upgrade.

:::

### Kubernetes Version Support Policy

In general, Astronomer Software will support a given version of Kubernetes through its End of Life. This includes Kubernetes upstream and cloud-managed variants like GKE, AKS, and EKS. When a version of Kubernetes reaches End of Life, support will be removed in the next major or minor release of Astronomer Software. For more information on Kubernetes versioning and release policies, refer to [Kubernetes Release History](https://kubernetes.io/releases/) or your cloud provider.

For more information on upgrading Kubernetes versions, follow the guidelines offered by your cloud provider.

- [Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)
- [Azure AKS](https://docs.microsoft.com/en-us/azure/aks/upgrade-cluster)
- [Google GKE](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-upgrades)
- [RedHat OpenShift](https://docs.openshift.com/container-platform/4.6/updating/updating-cluster-between-minor.html)

## Astronomer Certified

The following table lists the version dependencies for Astronomer Certified images:

| Astronomer Certified | Postgres | MySQL | Python                         | System Distribution  | Airflow Helm chart |
| -------------------- | -------- | ----- | ------------------------------ | -------------------- | ------------------ |
| 2.1.0                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8                  | Debian 10 (Buster)   | 0.18.6+            |
| 2.1.1                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9             | Debian 10 (Buster)   | 0.18.6+            |
| 2.1.3                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9             | Debian 10 (Buster)   | 0.18.6+            |
| 2.1.4                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9             | Debian 10 (Buster)   | 0.18.6+            |
| 2.3.0                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |
| 2.3.1                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |
| 2.3.2                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |
| 2.3.3                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |
| 2.3.4                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |
| 2.4.1                | 9.6+     | 8.0+  | 3.6, 3.7, 3.8, 3.9 (_Default_) | Debian 11 (Bullseye) | 0.18.6+            |

For more detail on each version of Astronomer Certified and upgrade instructions, see [Upgrade Apache Airflow](manage-airflow-versions.md).

> **Note:** While the Astronomer Certified Python Wheel supports Python versions 3.6, 3.7, and 3.8, Astronomer Certified Docker images have been tested and built only with Python 3.7. To run Astronomer Certified on Docker with Python versions 3.6 or 3.8, you can create a custom image with a different Python version specified. For more information, read [Change Python Versions](customize-image.md#build-with-a-different-python-version).

> **Note:** MySQL 5.7 is compatible with Airflow and Astronomer Certified 2.0 but it does NOT support the ability to run more than 1 Scheduler and is not recommended. If you'd like to leverage Airflow's new Highly-Available Scheduler, make sure you're running MySQL 8.0+.
