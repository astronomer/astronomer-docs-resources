## Astro Runtime 8.10.0

- Release date: October 12, 2023
- Airflow version: 2.6.3

### Additional improvements

- Upgraded `astronomer-providers` to 1.18.0. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1180-2023-09-25) for a complete list of changes.
- Upgraded `astro-sdk-python` to 1.7.0. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.
- Upgraded `openlineage-airflow` to 1.4.1. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/1.4.1) for a complete list of changes.
- Upgraded many OSS providers to newer minor and patch versions.

## Astro Runtime 8.9.0

- Release date: August 28, 2023
- Airflow version: 2.6.3

### Early access Airflow bug fixes

- Fixed an issue where Airflow incorrectly used `urljoin` to generate the string for `log_url`. ([#33063](https://github.com/apache/airflow/pull/33063))

### Additional improvements

- Upgraded `astronomer-providers` to 1.17.3. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1173-2023-08-07) for a complete list of changes.
- Upgraded `astro-sdk-python` to 1.6.2. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.

### Bug fixes

- Fixed an issue where you could not set dag or task notes in the Airflow UI for environments running on Astro.
- Fixed an issue with trigger logs for Deployments running on AWS.

## Astro Runtime 8.8.0

- Release date: July 21, 2023
- Airflow version: 2.6.3

### Early access Airflow bug fixes

- Fix bad delete logic for dag runs ([32684](https://github.com/apache/airflow/pull/32684)).

### Additional improvements

- Upgraded a few built-in providers to new minor versions.

### Bug fixes

- Upgraded `apache-airflow-providers-microsoft-azure` to 6.2.1. This fixes an issue where Deployments running Astro Runtime 8.7.0 on Azure clusters experienced failures with deferrable operators and task logs.
- Fixed dag deletion permissions in Astro for non-admin users.

## Astro Runtime 8.7.0

- Release date: July 11, 2023
- Airflow version: 2.6.3

### Airflow 2.6.3

Astro Runtime 8.7.0 includes same-day support for Apache Airflow 2.6.3. Airflow 2.6.3 contains a number of bug fixes including:

- Fix `operator_extra_links` property serialization in mapped tasks ([31904](https://github.com/apache/airflow/pull/31904))
- You can now specify a format for manual `run_id` inputs. Manually entered `run_ids` must conform with the regex specified in the `[scheduler]allowed_run_id_pattern` setting. [32293](https://github.com/apache/airflow/pull/32293))

For a complete list of the changes, see the [Apache Airflow 2.6.3 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html).

### Additional improvements

- Upgraded `openlineage-airflow` to 0.29.2, which includes support for Spark 3.4. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.29.2) for a complete list of changes.

## Astro Runtime 8.6.0

- Release date: June 27, 2023
- Airflow version: 2.6.2

### Additional improvements

- Upgraded `astronomer-providers` to 1.17.1, which includes enhancements to the `S3KeySizeSensorAsync` and some bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1170-2023-06-21) for a complete list of changes.
- Upgraded `apache-airflow-providers-providers-amazon` to [8.2.0](https://airflow.apache.org/docs/apache-airflow-providers-amazon/stable/index.html#id1).

## Astro Runtime 8.5.0

- Release date: June 17, 2023
- Airflow version: 2.6.2

### Airflow 2.6.2

Astro Runtime 8.5.0 includes same-day support for Apache Airflow 2.6.2. Airflow 2.6.2 contains a number of bug fixes including:

- Fix Kubernetes executors detection of deleted pods ([31274](https://github.com/apache/airflow/pull/31274))
- Fix crash when clearing run with task from normal to mapped ([31352](https://github.com/apache/airflow/pull/31352))

For a complete list of the changes, see the [Apache Airflow 2.6.2 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html).

### Additional improvements

- Upgraded `openlineage-airflow` to 0.28.0. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.28.0) for a complete list of changes.

### Bug fixes

- Fixed an issue where Istio versions were being parsed as [Python versions](https://peps.python.org/pep-0440/) instead of [semantic versions](https://semver.org/), resulting in dag errors.

## Astro Runtime 8.4.0

- Release date: June 2, 2023
- Airflow version: 2.6.1

### Early access Airflow bug fixes

- Fixed the scheduler crashing when you cleared a run of a normal task that is now a mapped task ([31352](https://github.com/apache/airflow/pull/31352)).

### Additional improvements

- Upgraded `astro-sdk-python` to 1.6.1, which includes support for MySQL and loading data from Azure blob storage to Databricks. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.
- Upgraded `apache-airflow-providers-cncf-kubernetes` to [7.0.0](https://airflow.apache.org/docs/apache-airflow-providers-cncf-kubernetes/stable/index.html#id1).

### Bug fixes

- Fixed an issue where you could not use the KubernetesPodOperator without setting `AIRFLOW_CONN_KUBERNETES_DEFAULT="kubernetes://` in your environment.

## Astro Runtime 8.3.0

- Release date: May 26, 2023
- Airflow version: 2.6.1

### Early access Airflow bug fixes

- Fixed a bug to ensure that `min_backoff` in the base sensor is at least `1` ([31412](https://github.com/apache/airflow/pull/31412))
- Updated error messaging ([31502](https://github.com/apache/airflow/pull/31502))

### Additional improvements

- Upgraded `astronomer-providers` to 1.16.0. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1160-2023-05-19) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.26.0. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.26.0) for a complete list of changes.
- Blocked the ability to pause the Monitoring dag with the Airflow API. The Monitoring dag is used by Astronomer to operate your Deployments and should not be paused.
- Added the Datadog provider. See the [Astronomer Registry](https://registry.astronomer.io/providers/apache-airflow-providers-datadog/versions/3.3.0) for more information on using the provider.

## Astro Runtime 8.2.0

- Release date: May 16, 2023
- Airflow version: 2.6.1

### Airflow 2.6.1

Astro Runtime 8.2.0 includes same-day support for Apache Airflow 2.6.1. Airflow 2.6.1 contains a number of bug fixes including:

- Fix timestamp parse failure for Kubernetes executor pod tailing ([31175](https://github.com/apache/airflow/pull/31175))
- Fix calculation of health check threshold for SchedulerJob ([31277](https://github.com/apache/airflow/pull/31277))

For a complete list of the changes, see the [Apache Airflow 2.6.1 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html).

### Additional improvements

- Upgraded `astronomer-providers` to 1.15.5, which includes bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1154-2023-04-19) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.25.0, which adds support for Spark/Delta `merge into` support. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.25.0) for a complete list of changes.

## Astro Runtime 8.1.0

- Release date: May 9, 2023
- Airflow version: 2.6.0

### Early access Airflow bug fixes

- Ensure the KPO runs pod mutation hooks correctly ([31173](https://github.com/apache/airflow/pull/31173))

### Additional improvements

- Upgraded `astro-sdk` to 1.6, which includes Astro Python SDK support for MySQL. For a complete list of changes, see the [Astro SDK changelog](https://github.com/astronomer/astro-sdk/blob/main/python-sdk/docs/CHANGELOG#160).

## Astro Runtime 8.0.0

- Release date: April 30, 2023
- Airflow version: 2.6.0

<Warning title="Breaking change">

Runtime 8 includes changes that can result in dags running differently after upgrading. It also includes a major bug that was subsequently fixed in Runtime 8.1. To use Airflow 2.6, Astronomer recommends upgrading directly to Runtime 8.1. See [Runtime upgrade considerations](runtime-version-considerations#runtime-8-airflow-26) for more information.

</Warning>

### Airflow 2.6

Astro Runtime 8 is based on Airflow 2.6, which includes a number of new features and improvements with an emphasis on observability. Most notably, Airflow 2.6 includes the following changes:

- [Notifiers](https://airflow.apache.org/docs/apache-airflow/stable/howto/notifications.html) are a new class that can be used to send notifications from a dag to a third party application, such as Slack. This release includes the [SlackNotifier](https://airflow.apache.org/docs/apache-airflow-providers-slack/stable/_api/airflow/providers/slack/notifications/slack/index.html#airflow.providers.slack.notifications.slack.SlackNotifier), with more notifiers coming in the future.
- A major bug related to zombie tasks has been fixed. The logic for handling stalled tasks has been moved to the scheduler, and any tasks that have been queued for more than `scheduler.task_queued_timeout` are now marked as failed. This prevents a type of zombie task where tasks are stuck in an infinite loop of being scheduled and queued.
- You can now view logs for individual triggers in the Airflow UI. Trigger logs tell you when an individual task is sleeping and when it's triggered.

To learn more, see the [Apache Airflow 2.6.0 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-6-0-2023-04-30).

### Fewer dependencies installed by default

Astro Runtime now includes fewer default dependencies to save on memory usage. The following provider packages are no longer installed by default:

- `apache-airflow-providers-apache-hive`
- `apache-airflow-providers-apache-livy`
- `apache-airflow-providers-databricks`
- `apache-airflow-providers-dbt-cloud`
- `apache-airflow-providers-microsoft-mssql`
- `apache-airflow-providers-sftp`
- `apache-airflow-providers-snowflake`
- `apache-airflow-providers-ssh`

If your dags use any of these providers, ensure that the provider packages are listed in your Astro project `requirements.txt` file before upgrading.

### Upgrade to Python 3.10

Astro Runtime now uses Python 3.10 by default. To continue using Python 3.9, see [Python versioning](runtime-image-architecture#python-versioning).

### Additional improvements

- Upgraded `astronomer-providers` to 1.15.4, which includes a bug fix for a backwards compatibility issue. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1154-2023-04-19) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.23.0, which includes support for dbt snapshots and support for parsing additional SQL commands. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.mdx#0230---2023-4-20) for a complete list of changes.