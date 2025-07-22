---
sidebar_label: 'Hybrid Worker queues'
title: 'Configure worker queues'
id: configure-worker-queues
description: Learn how to create and configure worker queues to create best-fit execution environments for your tasks.
---

Astro Hybrid worker type setup

On Astro Hybrid clusters, worker type is defined as a node instance type that is supported by the cloud provider of your cluster. For example, a worker type might be `m5.2xlarge` or `c6i.4xlarge` for a Deployment running on a Hybrid AWS cluster hosted on your cloud. Actual worker size is equivalent to the total capacity of the worker type minus Astro’s system overhead.

Your Organization can enable up to 10 additional different worker types for each Hybrid cluster. After a worker type is enabled on an Astro Hybrid cluster, the worker type becomes available to any Deployment in that cluster and appears in the **Worker Type** menu of the Astro UI.

1. Review the list of supported worker types for your cloud provider. See [AWS](resource-reference-aws-hybrid.md#supported-worker-node-pool-instance-types), [Azure](resource-reference-azure-hybrid.md#supported-worker-node-pool-instance-types), or [GCP resource references](resource-reference-gcp-hybrid.md#supported-worker-node-pool-instance-types).
2. Contact [Astronomer support](https://cloud.astronomer.io/open-support-request) and provide the following information:

    - The name of your cluster.
    - The name of the worker type(s) you want to enable for your cluster. For example, `m6i.2xlarge`.

For more information on requesting cluster changes, see [Manage Hybrid clusters](manage-hybrid-clusters.md).
