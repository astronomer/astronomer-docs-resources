---
sidebar_label: 'Overview'
title: 'Configure a Deployment on Astronomer Software'
id: configure-deployment
description: Learn the ways you can configure individual Airflow Deployments on Astronomer Software
---

An Airflow Deployment on Astronomer is an instance of Apache Airflow that runs in your Astronomer Software cluster. Each Astronomer Software Deployment is hosted on a dedicated Kubernetes namespace, has a dedicated set of resources, and operates with an isolated Postgres metadata database.

A Deployment typically encapsulates a single use case or context. Each Deployment has a number of settings that you can fine-tune so that you're running Airflow optimally for this context. Use the following topics to learn more about each available configuration option on an Astronomer Software Deployment.

## Deployment creation and deletion

Creating and deleting Deployments can become an operational complexity when you run Airflow across many teams. See the following documentation to learn about all of the options for creating Deployments, deleting Deployments, and ensuring that Deployment resources are returned back to your cluster for future use.

## Deployment resources

The amount of CPU and memory available to your Deployment defines how many tasks it can run in parallel. See [Deployment resources](deployment-resources.md) to learn how to configure your Deployment's scheduler, executor, and webserver resources.

## Environment variables

Each Deployment has its own set of environment variables that you can use to define both Airflow-level configurations and DAG objects such as connections. See [Environment variables](environment-variables.md) to learn more about setting these

## Deploy methods

Astronomer supports several different methods for deploying DAGs and code-based project configurations to Astro. See [Deploy methods overview](deploy-code-overview.md).

When you're ready to automate a deploy mechanism at scale for your team, see [CI/CD](ci-cd.md) to learn how to configure API credentials and examples of CI/CD pipelines in different version management tools.

## Upgrade Deployments

To take advantage of the latest features in Apache Airflow and stay in support, you must upgrade your Deployments over time. See [Upgrade Astro Runtime](manage-airflow-versions.md) for setup steps.

The Airflow [executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/index.html) works closely with the Airflow scheduler to decide what resources will complete tasks as they're queued. The difference between executors comes down to their available resources and how they utilize those resources to distribute work.

Astronomer supports 3 executors:

- [Local executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/local.html)
- [Celery executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/celery.html)
- [Kubernetes executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/kubernetes.html)

Though it largely depends on your use case, we recommend the Local executor for development environments and the Celery or Kubernetes executors for production environments operating at scale.

For a detailed breakdown of each executor, see [Airflow executors explained](https://docs.astronomer.io/learn/airflow-executors-explained).

## Select a resource strategy

A Deployment's **Resource Strategy** defines how you can allocate CPU and memory to the Deployment's Airflow components. Astronomer Software offers two different resource strategies: **Custom Resources** and **Astronomer Units (AUs)**.

An AU is equivalent to 0.1 CPU and 0.375 GiB of memory. If you set your resource strategy to **Astronomer Units**, you can only scale components based on this resource ratio. Components must use the same AU value for both CPU and memory.

If you set your resource strategy to **Custom Resources**, you can freely set CPU and memory for each component without a predetermined ratio. See [Customize resource usage](customize-resource-usage.md).

<Info>If you still want a constant ratio of CPU to memory but want to change the specific ratio, you can change the amount of resources an AU represents. See [Overprovision Deployments](cluster-resource-provisioning).</Info>

## Scale core resources

Apache Airflow requires two primary components:

- The Airflow Webserver
- The Airflow Scheduler

To scale either resource, adjust the corresponding slider in the Software UI to increase its available computing resources.

Read the following sections to help you determine which core resources to scale and when.

### Airflow webserver

The Airflow webserver is responsible for rendering the [Airflow UI](https://airflow.apache.org/docs/apache-airflow/stable/ui.html), where users can monitor DAGs, view task logs, and set various non-code configurations.

If a function within the Airflow UI is slow or unavailable, Astronomer recommends increasing the resources allocated towards the webserver.

### Airflow scheduler

The [Airflow scheduler](https://airflow.apache.org/docs/apache-airflow/stable/scheduler.html) is responsible for monitoring task execution and triggering downstream tasks once dependencies have been met.

If you experience delays in task execution, which you can track via the [Gantt Chart](https://airflow.apache.org/docs/apache-airflow/stable/ui.html#gantt-chart) view of the Airflow UI, Astronomer recommends increasing the resources allocated towards the scheduler.

> **Tip:** To set alerts that notify you via email when your Airflow scheduler is underprovisioned, refer to [Airflow alerts](airflow-alerts.md).

#### Scheduler count

Airflow 2.0 comes with the ability for users to run multiple schedulers concurrently to ensure high-availability, zero recovery time, and faster performance. By adjusting the **Scheduler Count** slider in the Software UI, you can provision up to 4 schedulers on any Deployment running Airflow 2.0+ on Astronomer.

Each individual scheduler will be provisioned with the resources specified in **Scheduler Resources**. For example, if you set the CPU figure in **Scheduler Resources** to 5 CPUs and set **Scheduler Count** to 2, your Airflow Deployment will run with 2 Airflow schedulers using 5 CPUs each for a total of 10 CPUs.

To increase the speed at which tasks are scheduled and ensure high-availability, Astronomer recommends provisioning 2 or more Airflow schedulers for production environments. For more information on the Airflow 2.0 scheduler, refer to Astronomer's ["The Airflow 2.0 Scheduler" blog post](https://www.astronomer.io/blog/airflow-2-scheduler).

### Triggerer

Airflow 2.2 introduces the triggerer, which is a component for running tasks with [deferrable operators](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/deferring.html). Like the scheduler, the triggerer is highly-available: If a triggerer shuts down unexpectedly, the tasks it was deferring can be recovered and moved to another triggerer.

By adjusting the **Triggerer** slider in the Software UI, you can provision up to 2 triggerers on any Deployment running Airflow 2.2+. To take advantage of the Triggerer's high availability, we recommend provisioning 2 triggerers for production Deployments.

## Kubernetes executor: Set extra capacity

On Astronomer, resources required for the [KubernetesPodOperator](kubepodoperator.md) or the [Kubernetes Executor](kubernetes-executor.md) are set as **Extra Capacity**.

The Kubernetes executor and KubernetesPodOperator each spin up an individual Kubernetes pod for each task that needs to be executed, then spin down the pod once that task is completed.

The amount of CPU and Memory allocated to **Extra Capacity** maps to [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/) on the [Kubernetes Namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) in which your Airflow Deployment lives on Astronomer. More specifically, **Extra Capacity** represents the maximum possible resources that could be provisioned to a pod at any given time.

Resources allocated to **Extra Capacity** do not affect scheduler or webserver performance and do not represent actual usage.

## Celery executor: Configure workers

To optimize for flexibility and availability, the Celery executor works with a set of independent Celery workers across which it can delegate tasks. On Astronomer, you're free to configure your Celery workers to fit your use case.

### Worker count

By adjusting the **Worker Count** slider, users can provision up to 20 Celery workers on any Airflow Deployment.

Each individual worker will be provisioned with the resources specified in **Worker Resources**. If you set the CPU figure in **Worker Resources** to 5 CPUs and set **Worker Count** to 3, for example, your Airflow Deployment will run with 3 Celery workers using 5 CPUs each for a total of 15 CPUs.

### Worker termination grace period

On Astronomer, Celery workers restart following every code deploy to your Airflow Deployment. This is to make sure that workers are executing with the most up-to-date code. To minimize disruption during task execution, however, Astronomer supports the ability to set a **Worker Termination Grace Period**.

If a deploy is triggered while a Celery worker is executing a task and **Worker Termination Grace Period** is set, the worker will continue to process that task up to a certain number of minutes before restarting itself. By default, the grace period is ten minutes.

> **Tip:** The **Worker Termination Grace Period** is an advantage to the Celery executor. If your Airflow Deployment runs on the Local executor, the scheduler will restart immediately upon every code deploy or configuration change and potentially interrupt task execution.

## Set environment variables

Environment variables can be used to set [Airflow configurations](https://airflow.apache.org/docs/apache-airflow/stable/configurations-ref.html) and custom values, both of which can be applied to your Airflow Deployment either locally or on Astronomer.

These can include setting Airflow Parallelism, an SMTP service for alerts, or a [secrets backend](secrets-backend.md) to manage Airflow connections and variables.

Environment variables can be set for your Airflow Deployment either in the **Variables** tab of the Software UI or in your `Dockerfile`. If you're developing locally, they can also be added to a local `.env` file. For more information on configuring environment variables, read [Environment variables on Astronomer](environment-variables.md).

> **Note**: Environment variables are distinct from [Airflow variables](https://airflow.apache.org/docs/apache-airflow/stable/howto/variable.html?highlight=variables) and [XComs](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/xcoms.html), which you can configure directly via the Airflow UI and are used for inter-task communication.

## Customize release names

An Airflow Deployment's release name on Astronomer is a unique, immutable identifier for that Deployment that corresponds to its Kubernetes namespace and that renders in Grafana, Kibana, and other platform-level monitoring tools. By default, release names are randomly generated in the following format: `noun-noun-<4-digit-number>`. For example: `elementary-zenith-7243`.

To customize the release name for a Deployment as you're creating it, you first need to enable the feature on your Astronomer platform. To do so, set the following value in your `values.yaml` file:

```yaml
astronomer:
  houston:
    config:
      deployments:
        manualReleaseNames: true # Allows you to set your release names
```

Then, push the updated `values.yaml` file to your installation as described in [Apply a config change](apply-platform-config.md).

After applying this change, the **Release Name** field in the Software UI becomes configurable:

![Custom Release Name Field](/img/software/custom-release-name.png)

## Code deploy mechanisms

Deploying code is the process of applying code from your local machine to an Astronomer Software Deployment. A code deploy can include an entire Astro project as a Docker image, or just the code in your Astro project `dags` directory. Astronomer Software supports a few different methods for deploying code to a Deployment. You can:

- Deploy [project images](deploy-cli.md) or [DAGs only](deploy-dags.md) using the Astro CLI. Deploying a project image is the only way to deploy Airflow-level configurations and dependencies to a Deployment.
- Deploy DAGs using an [NFS volume](deploy-nfs.md).
- Deploy DAGs using [Git sync](deploy-git-sync.md).

### Astro CLI deploys

By default, you can deploy code to an Airflow Deployment by building it into a Docker image and pushing that image to the Astronomer Registry via the CLI or API. This workflow is described in [Deploy code via the CLI](deploy-cli.md).

This mechanism builds your DAGs into a Docker image alongside all other files in your Astro project directory, including your Python and OS-level packages, your Dockerfile, and your plugins.

The resulting image is then used to generate a set of Docker containers for each of Airflow's core components. Every time you run `astro deploy` in the Astro CLI, your DAGs are rebuilt into a new Docker image and all Docker containers are restarted.

You can also enable [DAG only deploys](deploy-dags.md) to deploy only your `dags` directory without building a Docker image. Note that you will still need access to Docker to authenticate to Astronomer Software before you can deploy DAGs.

### NFS volume-based DAG deploys

For advanced teams who deploy DAG changes more frequently, Astronomer also supports an [NFS volume-based](https://kubernetes.io/docs/concepts/storage/volumes/#nfs) DAG deploy mechanism.

Using this mechanism, you can deploy DAGs to an Airflow Deployment on Astronomer by adding the corresponding Python files to a shared file system on your network. Compared to image-based deploys, NFS volume-based deploys limit downtime and enable continuous deployment.

To deploy DAGs to a Deployment via an NFS volume, you must first enable the feature at the platform level. For more information, read [Deploy DAGs via NFS volume](deploy-nfs.md).

### Git-sync DAG deploys

For teams using a Git-based workflow for DAG development, Astronomer supports a [git-sync](https://github.com/kubernetes/git-sync) deploy mechanism.

To deploy DAGs via git-sync, you add DAGs to a repository that has been configured to sync with your Astronomer Deployment. Once the Deployment detects a change in the repository, your DAG code will automatically sync to your Deployment with no downtime. For more information on configuring this feature, read [Deploy DAGs via git sync](deploy-git-sync.md).

## Delete a Deployment

You can delete an Airflow Deployment using the **Delete Deployment** button at the bottom of the Deployment's **Settings** tab.

When you delete a Deployment, you delete your Airflow webserver, scheduler, metadata database, and deploy history, and you lose any configurations set in the Airflow UI.

By default, Astro performs a _soft delete_ when you delete a Deployment. After you delete a Deployment, your Astronomer database, the corresponding `Deployment` record receives a `deletedAt` value and continues to persist until permanently deleted through a _hard delete_. A hard delete includes both the Deployment's metadata database and the Deployment entry in your Astronomer database. 14 days after your Deployment's soft delete, Astronomer automatically runs a hard delete cronjob that deletes any values that remained after your soft delete.

<Tip>Astronomer recommends regularly doing a database audit to confirm that you hard delete databases.</Tip>

### Automate Deployment deletion clean up

Astronomer runs a cronjob to hard delete the deleted Deployment's metadata database and Deployment entry in your Astronomer database at midnight on a specified day. You can enable whether this cronjob runs or not, how many days after your soft delete to run the cronjob, and what time of day to run the cronjob by editing `astronomer.houston.cleanupDeployments` in your Astronomer Helm chart.

The following is an example of how you might configure the cronjob in your Helm chart:

```yaml
# Cleanup deployments that have been soft-deleted
  # This clean up runs as a CronJob
  cleanupDeployments:
    # Enable the clean up CronJob
    enabled: true

    # Default time for the CronJob to run https://crontab.guru/#0_0_*_*_*
    schedule: "0 0 * * *"

    # Number of days after the Deployment deletion to run the CronJob
    olderThan: 14
```

### Hard delete a Deployment

To reuse a custom release name given to an existing Deployment after a soft delete but before Astronomer automatically cleans up any persisting Deployment records, you need to hard delete both the Deployment's metadata database and the Deployment's entry in your Astronomer database.

1. Enable hard delete as an option at the platform level. To enable this feature, set `astronomer.houston.config.deployments.hardDeleteDeployment: true` in your `values.yaml` file and push the changes to your platform as described in [Apply a config change](apply-platform-config.md).

2. Hard delete a Deployment with the Software UI or Astro CLI.
  - **Software UI:** Go to the Deployment's **Settings** tab and select **Delete Deployment**. Then, select the **Hard Delete?** checkbox before confirming **Delete Deployment**.

    ![Hard delete checkbox](/img/software/hard-delete.png)

  - **Astro CLI:** Run `astro deployment delete --hard`.

This action permanently deletes all data associated with a Deployment, including the database and underlying Kubernetes resources.


## Programmatically create or update Deployments

You can programmatically create or update Deployments with all possible configurations using the Houston API `upsertDeployment` mutation. See [Create or update a Deployment with configurations](houston-api.md#create-or-update-a-deployment-with-configurations).

## Clean Deployment task metadata

You can run a cron job to automatically archive task and DAG metadata from your Deployment. This job runs [`airflow db clean`](https://airflow.apache.org/docs/apache-airflow/stable/cli-and-env-variables-ref.html#clean) programmatically for all of your Deployments and exports the results each Deployment as files to your external storage service. To run this job for a Deployment, you must install the Astronomer-maintained `airflow-dbcleanup-plugin` on the Deployment. This plugin executes the cleanup job from your Deployment's `webserver` Pod.


1. For Deployments running Runtime 7 or earlier, add the following line to the `requirements.txt` file of your Deployment's Astro project. Replace `<latest-version>` with the latest available version in the [`airflow-dbcleanup-plugin` GitHub repository](https://github.com/astronomer/airflow-dbcleanup-plugin/releases).

    ```text
    https://github.com/astronomer/airflow-dbcleanup-plugin/releases/download/<latest-version>/astronomer_dbcleanup_plugin-<latest-version>-py3-none-any.whl
    ```

    You can skip this step for Deployments running Astro Runtime 8 or later.

2. Authorize your Deployments to your external storage service so that the webserver Pod can export the results of your cleanup jobs in JSON or URI Format. You can authorize your Deployment using one of the following methods:

    - Configure an [Airflow connection] in the Deployment that connects to your external storage service.
    - To configure a global connection for all Deployments, create a [Kubernetes secret](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret) containing an Airflow connection to your external storage service. The connection must be defined in either JSON or URI format. To pass the secret to all the Deployments, annotate the secret using the following command:

    ```sh
    kubectl annotate secret <secret-name> "astronomer.io/commander-sync"="platform=astronomer"
    ```

3. Add the following configuration to your `values.yaml` file and change the default values as needed.

    ```yaml
    astronomer:
      houston:
        cleanupAirflowDb:
          # Enable cleanup CronJob
          enabled: false

          # Default run is at 5:23 every morning https://crontab.guru/#23_5_*_*_*
          schedule: "23 5 * * *"

          # Cleanup deployments older than this many days
          olderThan: 365

          # Output path of archived data csv export
          outputPath: "/tmp"

          # Delete archived tables
          purgeArchive: true

          # Print out the deployments that should be cleaned up and skip actual cleanup
          dryRun: false

          # Name of file storage provider, supported providers - aws/azure/gcp/local
          provider: local

          # Name of the provider bucket name / local file path
          bucketName: "/tmp"

          # The name of the Kubernetes Secret containing your Airflow connection
          providerEnvSecretName: "<your-secret-name>"

          # Run cleanup on specific table or list of tables in a comma separated format
          tables: ""
    ```

4. Push the configuration change. See [Apply a config change](apply-platform-config.md).

<Tip>Set `dryRun: true` to test this feature without deleting any data. When dry runs are enabled, the cleanup job will only print the data that it plans to modify in the serial output of the webserver Pod. To view the dryRun events of the cleanup job, check the logs of your webserver Pod for each Deployment.</Tip>

<Error>The cleanup job deletes any data that's older than the number of days specified in your `olderThan` configuration. Ensure that none of your historical data is required to run current DAGs or tasks before enabling this feature.</Error>