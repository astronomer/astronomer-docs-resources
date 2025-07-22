---
sidebar_label: 'Kubernetes executor for Hybrid'
title: 'Configure tasks to run with the Kubernetes executor for Hybrid'
description: Learn how to configure the Pods that the Kubernetes executor runs your tasks in.
---

## Ephemeral storage Astro Hybrid setup

Since ephemeral storage is only available on Astro Hosted, the following example can be used for Astro Hybrid.

```python
import pendulum
import time

from airflow.models.dag import DAG
from airflow.decorators import task
from airflow.operators.bash import BashOperator
from airflow.operators.python import PythonOperator
from airflow.example_dags.libs.helper import print_stuff
from kubernetes.client import models as k8s


k8s_exec_config_resource_requirements = {
    "pod_override": k8s.V1Pod(
        spec=k8s.V1PodSpec(
            containers=[
                k8s.V1Container(
                    name="base",
                    resources=k8s.V1ResourceRequirements(
                        requests={"cpu": 0.5, "memory": "1024Mi"},
                        limits={"cpu": 0.5, "memory": "1024Mi"}
                    )
                )
            ]
        )
    )
}

with DAG(
    dag_id="example_kubernetes_executor_pod_override_sources",
    schedule=None,
    start_date=pendulum.datetime(2023, 1, 1, tz="UTC"),
    catchup=False
):
    BashOperator(
      task_id="bash_resource_requirements_override_example",
      bash_command="echo hi",
      executor_config=k8s_exec_config_resource_requirements
    )

    @task(executor_config=k8s_exec_config_resource_requirements)
    def resource_requirements_override_example():
        print_stuff()
        time.sleep(60)

    resource_requirements_override_example()
```

## (Astro Hybrid only) Change the Kubernetes executor's worker node type

:::info

This section applies only to [Astro Hybrid](hybrid-overview.md) users. To see whether you're an Astro Hybrid user, open your Organization in the Astro UI and go to **Settings** > **General**. Your Astro product type is listed under **Product Type**.

:::

A Deployment on Astro Hybrid that uses the Kubernetes executor runs worker Pods on a single `default` worker queue. You can change the type of worker that this queue uses from the Astro UI.

1. In the Astro UI, select a Workspace, click **Deployments**, and then select a Deployment.

2. Click the **Worker Queues** tab and then click **Edit** to edit the `default` worker queue.

3. In the **Worker Type** list, select the type of worker to run your Pods on.

4. Click **Update Queue**.