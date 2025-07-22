---
sidebar_label: 'Run KubernetesPodOperator'
title: "Run the KubernetesPodOperator on Astro Hybrid"
description: "Learn how to run the KubernetesPodOperator on Astro. This operator dynamically launches a Pod in Kubernetes for each task and terminates each Pod when the task is complete."
---

### Mount a temporary directory

On Astro Hybrid, this configuration works only on AWS clusters where you have enabled `m5d` and `m6id` worker types. These worker types have NVMe SSD volumes that can be used by tasks for ephemeral storage. See [Amazon EC2 M6i Instances](https://aws.amazon.com/ec2/instance-types/m6i/) and [Amazon EC2 M5 Instances](https://aws.amazon.com/ec2/instance-types/m5/) for the amount of available storage in each node type.

The task which mounts a temporary directory must run on a worker queue that uses either `m5d` and `m6id` worker types. See [Modify a cluster](manage-hybrid-clusters.md) for instructions on enabling `m5d` and `m6id` workers on your cluster. See [Configure a worker queue](configure-worker-queues.mdx) to configure a worker queue to use one of these worker types.

## Known limitations for KPO

- (Hybrid only) You cannot run a KubernetesPodOperator task in a worker queue or node pool that is different than the worker queue of its parent worker. For example, a KubernetesPodOperator task that is triggered by an `m5.4xlarge` worker on AWS will also be run on an `m5.4xlarge` node. To run a task on a different node instance type, you must launch it in an external Kubernetes cluster. If you need assistance launching KubernetesPodOperator tasks in external Kubernetes clusters, contact [Astronomer support](https://support.astronomer.io).