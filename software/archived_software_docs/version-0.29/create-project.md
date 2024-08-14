---
title: 'Create an Astronomer Software project'
sidebar_label: 'Create a project'
id: create-project
description: Get started on Astronomer Software.
---

This is where you'll find information about creating a project and running it in a local Airflow environment.

## Prerequisites

Creating an Astro project requires the [Astro CLI](install-cli.md).

## Step 1: Create a project directory

Before you create a Software project, create an empty directory and open it:

 ```sh
mkdir <your-new-directory> && cd <your-new-directory>
 ```

From this directory, run the following Astro CLI command:

```sh
astro dev init --use-astronomer-certified
```

This generates the following files:

```py
.
├── dags # Where your DAGs go
│   └── example-dag.py # An example DAG that comes with the initialized project
├── Dockerfile # For Astronomer's Docker image and runtime overrides
├── include # For any other files you'd like to include
├── plugins # For any custom or community Airflow plugins
├── airflow_settings.yaml # For your Airflow connections, variables and pools (local only)
├── packages.txt # For OS-level packages
└── requirements.txt # For any Python packages
```

A few of these files are essential for deploying your Airflow image for the first time:

### Dockerfile

Your Dockerfile includes a reference to an Astronomer Certified Docker image. Astronomer Certified (AC) is a Debian-based, production-ready distribution of Apache Airflow that mirrors the open source project and undergoes additional levels of rigorous testing conducted by our team.

This Docker image is hosted on [Astronomer's Docker registry](https://quay.io/repository/astronomer/ap-airflow?tab=tags) and allows you to run Airflow on Astronomer. Additionally, the image you include in your Dockerfile dictates the version of Airflow you'd like to run both when you're developing locally and pushing up to Astro.

The Docker image you'll find in your Dockerfile by default is:

```
FROM quay.io/astronomer/ap-airflow:latest-onbuild
```

This will install a Debian-based AC image for the latest version of Airflow we support. To specify a particular Airflow version, read [Upgrade Airflow](manage-airflow-versions.md) and the _Customize your Image_ topic below.

:::tip

To use an Astro Runtime image with your new project, remove `--use-astronomer-certified` from your command. Note that projects using Astro Runtime can only be deployed to Astronomer Software installations on version 0.29 and above.

:::

### Example DAG

To help you get started, your initialized project includes an `example-dag` in `/dags`. This DAG simply prints today's date, but it'll give you a chance to become familiar with how to deploy on Astronomer.

If you'd like to deploy some more functional DAGs, upload your own or check out [example DAGs we've open sourced](https://github.com/airflow-plugins/example-dags).

## Step 2: Build your project locally

To confirm that you successfully initialized an Astro project, run the following command from your project directory:

```sh
astro dev start
```

This command builds your project and spins up 4 Docker containers on your machine, each for a different Airflow component:

- **Postgres:** Airflow's metadata database
- **Webserver:** The Airflow component responsible for rendering the Airflow UI
- **Scheduler:** The Airflow component responsible for monitoring and triggering tasks
- **Triggerer:** The Airflow component responsible for running Triggers and signaling tasks to resume when their conditions have been met. The triggerer is used exclusively for tasks that are run with deferrable operators.

## Step 3: Access the Airflow UI

Once your project builds successfully, you can access the Airflow UI by going to `http://localhost:8080/` and logging in with `admin` for both your username and password.

:::info

It might take a few minutes for the Airflow UI to be available. As you wait for the webserver container to start up, you might need to refresh your browser.

:::

After logging in, you should see the DAGs from your `dags` directory in the Airflow UI.

![Example DAG in the Airflow UI](/img/software/sample-dag.png)

## What's next?

Once you've successfully created a Software project on your local machine, we recommend reading the following:

* [Customize image](customize-image.md)
* [Configure a Deployment](configure-deployment.md)
* [Deploy code](deploy-cli.md)
