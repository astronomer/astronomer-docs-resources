---
sidebar_label: 'Configure NFS deploys'
title: 'Configure NFS code deploys'
id: deploy-nfs
description: Push DAGs to an Airflow Deployment on Astronomer Software using an external NFS volume.
---

Starting in Astronomer Software v0.25, you can use an external [Network File System (NFS) Volume](https://kubernetes.io/docs/concepts/storage/volumes/#nfs) to deploy DAGs to an Airflow Deployment on Astronomer.

Unlike [deploying DAGs via the Astro CLI](deploy-cli.md), deploying DAGs to an NFS volume, such as Azure File Storage or Google Cloud Filestore, does not require rebuilding a Docker image and restarting your underlying Airflow service. When a DAG is added to an NFS volume, it automatically appears in the Airflow UI without requiring additional action or causing downtime.

## Implementation Considerations

Consider the following before completing this setup:

- You can configure NFS volumes only to deploy DAGs. To push dependencies or other requirements to your Airflow Deployment, you'll need to update your `requirements.txt` and `packages.txt` files and deploy using the [Astro CLI](deploy-cli.md) or [CI/CD](ci-cd.md). For more information on pushing code to your Airflow environment, see [Customize images](customize-image.md).
- If you configure an NFS volume for an Airflow Deployment, you can't use the Astro CLI or an Astronomer service account to deploy DAGs . These options are available only for Deployments configured with an image-based deploy mechanism.
- You can configure NFS volumes only for Airflow Deployments running Airflow 2.0+.

## Enable NFS volume storage

NFS volume deploys must be explicitly enabled on Astronomer by a System Admin. To enable it, update your `config.yaml` file with the following values:

```yaml
houston:
  config:
      deployments:
        configureDagDeployment: true
        nfsMountDagDeployment: true
```

Once you have saved the file, push the configuration change to your platform as described in [Apply a config change](apply-platform-config.md). This process needs to be completed only once per Software installation.

## Provision an NFS volume

While you can use any NFS volume for this step, we recommend using your cloud provider's primary NFS volume solution:

* GCP: [Filestore](https://cloud.google.com/filestore/docs/creating-instances)
* Azure: [File Storage](https://docs.microsoft.com/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares?tabs=azure-portal)
* AWS: [EFS](https://docs.aws.amazon.com/efs/latest/ug/getting-started.html)

For each NFS volume you provision for DAG deploys, you need to configure:

* A directory for DAGs.
* Read access for a user with GID `50000` and UID `50000`. For an example setup of this, read [Configuring Ip-based access control](https://cloud.google.com/filestore/docs/creating-instances#configuring_ip-based_access_control) in Google Cloud's documentation.

## Add an NFS volume to a Deployment

Workspace editors can configure a new or existing Airflow Deployment to use a provisioned NFS volume for DAG deploys. From there, any member of your organization with write permissions to the NFS volume can deploy DAGs to the Deployment. To do so:

1. In the Software UI, create a new Airflow Deployment or open an existing one.
2. Go to the **DAG Deployment** section of the Deployment's Settings page.
3. For your **Mechanism**, select **NFS Volume Mount**:

    ![Custom Release Name Field](/img/software/nfs.png)

4. In the **NFS Location** field that appears, enter the location of your volume-based DAG directory as `<IP>:/<path>` (for example: `192.168.0.1:/path/to/your/dags`).
5. Save your changes.

> **Note:** You can also use the  Astro CLI to configure NFS volumes. To do so, specify the `--nfs-location` flag when running [`astro deployment create`](cli-reference.md#astro-deployment-create) or [`astro deployment update`](cli-reference.md#astro-deployment-update).
