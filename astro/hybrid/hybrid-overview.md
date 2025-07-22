---
sidebar_label: "Hybrid overview"
title: "Astro Hybrid overview"
id: hybrid-overview
---

[_Astro Hosted_](astro-architecture.md), also known simply as **Astro**, is a fully-managed SaaS application for Apache Airflow. _Astro Hybrid_ is a self-hosted, Astronomer-managed Airflow service for data orchestration that is built for the cloud and powered by Apache Airflow. Astro Hybrid is built with a multi-plane architecture which consists of:

- A control plane that is hosted by Astronomer.
- A data plane that runs in your cloud.

Astro Hybrid can be activated on Amazon Web Services (AWS), Google Cloud Platform (GCP), or Microsoft Azure. Astronomer runs Astro on managed Kubernetes services for each cloud provider, including AWS Elastic Kubernetes Service (EKS), Google Kubernetes Engine (GKE), and Azure Kubernetes Service (AKS).

The control plane and data plane are managed by Astronomer and require no operational oversight by your organization. The Hybrid architecture ensures that tasks are executed securely within your corporate network.

![Astro Hybrid architecture overview](/img/docs/hybrid-architecture-overview.png)

For more information about Astro architecture, contact [Astronomer support](https://cloud.astronomer.io/open-support-request).

## Related documentation

- [Install Astro Hybrid on AWS](install-aws-hybrid.md)
- [Install Astro Hybrid on GCP](install-gcp-hybrid.md)
- [Install Astro Hybrid on Azure](install-azure-hybrid.md)