---
title: 'Run the Kubernetes executor on Astronomer Software'
sidebar_label: 'Kubernetes executor'
id: kubernetes-executor
description: Run and configure the Kubernetes executor on Astronomer.
---

The Apache Airflow [Kubernetes Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/kubernetes.html) relies on a fixed single Pod that dynamically delegates work and resources. For each task that needs to run, the executor talks to the Kubernetes API to dynamically launch Pods which terminate when that task is completed.

This enables the executor to scale depending on how many Airflow tasks you're running at a given time. It also means you can configure the following for each individual Airflow task:

- Memory allocation
- Service accounts
- Airflow image

To configure these resources for each Pod, you configure a Pod template. For more information on configuring Pod template values, reference the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/pods/#pod-templates).

## Prerequisites

You must have an Airflow Deployment on Astronomer running with the Kubernetes executor. For more information on configuring an executor, see [Configure a Deployment](configure-deployment.md). To learn more about different executor types, see [Airflow Executors Explained](https://www.astronomer.io/guides/airflow-executors-explained).

## Configure the Kubernetes executor using pod templates

By default, Airflow Deployments on Astronomer use a pod template to construct each pod. To configure a Deployment's Kubernetes executor, you need to modify the Deployment's pod template and reapply a custom template via environment variables. To do so:

1. Run the following command to find the namespace (release name) of your Airflow Deployment:

    ```sh
    kubectl get ns
    ```

    You can also find this information in the Software UI under the **Deployments** tab of your Workspace menu.

2. Run the following command to get the `pod_template_spec` for your release:

    ```sh
    kubectl exec deploy/<release-name>-scheduler -- cat pod_templates/pod_template_file.yaml > new_pod_template_file.yaml
    ```

3. Customize the pod template file to fit your use case.
4. Add a command to your Dockerfile that copies your customized pod template into your Docker image. For instance, if your customized pod template file name is `new_pod_template.yaml`, you would add the following line to your Dockerfile:

    ```
    COPY new_pod_template.yaml /tmp/copied_pod_template.yaml
    ```

    This command uses `new_pod_template.yaml` to create `copied_pod_template.yaml` at build time as part of your Docker image. You'll specify this file in an Environment Variable in Step 2.

    > **Note:** Depending on your configuration, you may also need to change your `USER` line to `root` in order to have the appropriate copy permissions.

5. In the Software UI, add the `AIRFLOW__KUBERNETES__POD_TEMPLATE_FILE` environment variable to your Deployment. Its value should be the directory path for the pod template in your Docker image. In this example, the file path would be `/tmp/copied_pod_template.yaml`.
6. In your terminal, run `astro deploy -f` to deploy your code and rebuild your Docker image.
7. To confirm that the deploy was successful, launch the Airflow UI for your Deployment, click into any single task, and click `K8s Pod Spec`. You should see the updates you made to the pod template in this specification.

## Configure the Kubernetes executor for a specific task

Some tasks require a more specific pod configuration than other tasks. For instance, one task might require significantly more GPU than another task. In cases like this, you can deploy a pod template to a single task within a DAG. To configure a pod template for a specific task:

1. Add a command to your Dockerfile that copies your customized pod template into your Docker image. For instance, if your customized pod template file name is `new_pod_template.yaml`, you would add the following line to your Dockerfile:

    ```
    COPY new_pod_template.yaml /tmp/copied_pod_template.yaml
    ```

    This command uses `new_pod_template.yaml` to create `copied_pod_template.yaml` at build time as part of your Docker image. You'll specify this file in an Environment Variable in Step 2.

    > **Note:** Depending on your configuration, you may also need to change your `USER` line to `root` in order to have the appropriate copy permissions.

2. Add the executor config to the task and specify your custom pod template. It should look something like this:

    ```python
    task_with_template = PythonOperator(
        task_id="task_with_template",
        python_callable=do_something,
        executor_config={
            "pod_template_file": "/tmp/copied_pod_template.yaml",
        },
    )
    ```

3. In your terminal, run `astro deploy -f` to deploy your code and rebuild your Docker image.
4. To confirm that the deploy was successful, launch the Airflow UI for your Deployment, click into any single task, and click `K8s Pod Spec`. You should see the updates you made to the pod template in this specification.
