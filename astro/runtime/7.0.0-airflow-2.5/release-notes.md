## Astro Runtime 7.6.0

- Release date: June 13, 2023
- Airflow version: 2.5.3

### Early access Airflow bug fixes

- Mark `[secrets] backend_kwargs` as a sensitive config ([31788](https://github.com/apache/airflow/pull/31788))

### Additional Improvements

- Upgraded `openlineage-airflow` to 0.27.2. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.27.2) for a complete list of changes.

## Astro Runtime 7.5.0

- Release date: May 29, 2023
- Airflow version: 2.5.3

### Early access Airflow bug fixes

- Fixed a bug to ensure that `min_backoff` in the base sensor is at least `1` ([31412](https://github.com/apache/airflow/pull/31412))
- Updated error messaging ([31502](https://github.com/apache/airflow/pull/31502))

### Additional Improvements

- Upgraded `astronomer-providers` to 1.16.0. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1160-2023-05-19) for a complete list of changes.
- Upgraded `astro-sdk-python` to 1.6.1, which includes support for MySQL and loading data from Azure blob storage to Databricks. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.26.0. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.26.0) for a complete list of changes.
- Blocked the ability to pause the Monitoring dag with the Airflow API. The Monitoring dag is used by Astronomer to operate your Deployments and should not be paused.

## Astro Runtime 7.4.3

- Release date: April 28, 2023
- Airflow version: 2.5.3

### Early access Airflow bug fixes

- Fix KubernetesExecutor sending state to scheduler ([30872](https://github.com/apache/airflow/pull/30872))

### Additional improvements

- Upgraded `astronomer-providers` to 1.15.4, which includes a bug fix for a backwards compatibility issue. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1154-2023-04-19) for a complete list of changes.

## Astro Runtime 7.4.2

- Release date: April 1, 2023
- Airflow version: 2.5.3

### Airflow 2.5.3

Astro Runtime 7.4.2 includes same-day support for Apache Airflow 2.5.3. Airflow 2.5.3 contains a number of bug fixes including:

- Fix `TriggerRuleDep` when the mapped tasks count is 0 ([30084](https://github.com/apache/airflow/pull/30084))
- Fix some long known Graph View UI problems ([29971](https://github.com/apache/airflow/pull/29971))

For a complete list of the changes, see the [Apache Airflow 2.5.3 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html).

### Additional improvements

- When using Runtime in an Astronomer Software installation, OpenLineage and the Astronomer monitoring dag are now disabled. OpenLineage can be re-enabled in your Deployment by setting the `OPENLINEAGE_URL` environment variable, or by setting the `OPENLINEAGE_DISABLED=False` environment variable.
- Upgraded `astronomer-providers` to 1.15.2, which includes several bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/releases/tag/1.15.2) for a complete list of changes.

## Astro Runtime 7.4.1

- Release date: March 17, 2023
- Airflow version: 2.5.2

### Early access Airflow bug fixes

- Ensure that `dag.partial_subset` doesn't mutate task group properties ([30129](https://github.com/apache/airflow/pull/30129))
- Revert fix for on_failure_callback when task receives a SIGTERM ([30165](https://github.com/apache/airflow/pull/30165))

## Astro Runtime 7.4.0

- Release date: March 15, 2023
- Airflow version: 2.5.2

### Airflow 2.5.2

Astro Runtime 7.2.0 includes same-day support for Apache Airflow 2.5.2. Airflow 2.5.2 contains a number of bug fixes including:

- Fix validation of date-time field in API and Parameter schemas ([29395](https://github.com/apache/airflow/pull/29395))
- Dag list sorting lost when switching page ([29756](https://github.com/apache/airflow/pull/29756))

For a complete list of the changes, see the [Apache Airflow 2.5.2 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-5-2-2023-03-15).

### Additional improvements

- Upgraded `astro-sdk-python` to 1.5.3, which includes Openlineage facets for Microsoft SQL server and restores some pandas load option classes. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.
- Upgraded `astronomer-providers` to 1.15.1, which includes a new async sensor `SnowflakeSensorAsync` and a number of bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1151-2023-03-09) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.21.1, which includes support for capturing custom environment variables from Spark and a number of bug fixes. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.21.1) for a complete list of changes.

## Astro Runtime 7.3.0

- Release date: February 14, 2023
- Airflow version: 2.5.1

### Early access Airflow bug fixes

- Use time not tries for queued & running re-checks ([28586](https://github.com/apache/airflow/pull/28586))

### Additional improvements

- Installed the following OS-level packages to support the Astro Python SDK MSSQL integration:

    - `postgresql-client`
    - `freetds-dev`
    - `libssl-dev`
    - `libkrb5-dev`

- Upgraded `astro-sdk-python` to 1.5.0, which includes support for Microsoft SQL and DuckDB. See the [Astro Python SDK changelog](https://github.com/astronomer/astro-sdk/blob/main/python-sdk/docs/CHANGELOG#150) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.20.4, which includes a new extractor for the GCSToGCSOperator. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.17.0) for a complete list of changes.

## Astro Runtime 7.2.0

- Release date: January 20, 2023
- Airflow version: 2.5.1

### Airflow 2.5.1

Astro Runtime 7.2.0 includes same-day support for Apache Airflow 2.5.1. Airflow 2.5.1 contains a number of bug fixes including:

- Return list of tasks that will be queued ([28066](https://github.com/apache/airflow/pull/28066))
- Fix masking of non-sensitive environment variables ([28802](https://github.com/apache/airflow/pull/28802))

For a complete list of the changes, see the [Apache Airflow 2.5.1 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-5-1-2023-01-20).

### The Astro Python SDK is now included with Astro Runtime

Astro Runtime now includes the Astro Python SDK, an open source tool and Python package (`astro-sdk-python`) for dag development that is built and maintained by Astronomer. With Astro Runtime versions 7.2.0 and later, you don't have to add the Astro Python SDK to your Astro project to use it.

To learn more about the Astro Python SDK, see [Astro Python SDK ReadTheDocs](https://astro-sdk-python.readthedocs.io/en/stable/) and [The Astro Python SDK Tutorial for ETL](https://www.astronomer.io/docs/learn/astro-python-sdk-etl).

### Early access Airflow bug fixes

In anticipation of future support for the Kubernetes executor on Astro, Astro Runtime includes the following bug fixes from Airflow 2.5.2:

- Be more selective when adopting pods with KubernetesExecutor ([28899](https://github.com/apache/airflow/pull/28899))
- KubernetesExecutor sends state even when successful ([28871](https://github.com/apache/airflow/pull/28871))
- Annotate KubeExecutor pods that we don't delete ([28844](https://github.com/apache/airflow/pull/28844))

### Additional improvements

- Upgraded `astronomer-providers` to 1.14.0, which includes support for using a role Amazon Resource Name (ARN) with `AwsBaseHookAsync`. See the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.13.0/CHANGELOG.rst) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.19.2, which includes new support for Airflow operators like the `S3FileTransformOperator` and additional facets for task runs. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.19.2) for a complete list of changes.

## Astro Runtime 7.1.0

- Release date: December 21, 2022
- Airflow version: 2.5.0

### Additional improvements

- Upgraded `astronomer-providers` to 1.13.0, which includes a collection of minor enhancements and bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1130-2022-12-16).
- Upgraded `openlineage-airflow` to 0.18.0, which includes new support for Airflow operators like the `SQLExecuteQueryOperator`. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.18.0) for more information.
- Upgraded `apache-airflow-providers-microsoft-azure` to 5.0.1, which includes a bug fix to revert `offset` and `length` to be optional arguments.
- Upgraded `certifi` to 2022.12.7.
- Airflow environments hosted on Astro now include a **Back to Astro** button in the Airflow UI. Use this button to return to the Deployment hosting the Airflow environment in the Astro UI.

## Astro Runtime 7.0.0

- Release date: December 2, 2022
- Airflow version: 2.5.0

### Airflow 2.5.0

Astro Runtime 7.0.0 includes same-day support for Airflow 2.5.0, which includes a collection of new features, bug fixes, automatic changes, and deprecations. Features include:

- Add comments to task instances and dag runs in the Airflow UI ([#26457](https://github.com/apache/airflow/pull/26457))
- Clear all task instances in a task group with one click in the Airflow UI ([#26658](https://github.com/apache/airflow/pull/26658)), [#28003](https://github.com/apache/airflow/pull/28003))
- Trigger a task when at least one upstream tasks is successful with new `one_done` trigger rule [#26146](https://github.com/apache/airflow/pull/26146)
- New **Parsed at** metric in the dag view of the Airflow UI [#27573](https://github.com/apache/airflow/pull/27573)
- Filter datasets in Airflow UI based on recent update events [#26942](https://github.com/apache/airflow/pull/26942)

To learn more, see [What's New in Apache Airflow 2.5](https://www.astronomer.io/blog/whats-new-in-apache-airflow-2-5/) and the [Apache Airflow 2.5.0 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-5-0-2022-12-02).

### Additional improvements

- In the Airflow UI for Astro Deployments, the **Audit Logs** page now shows the Astro user who performed a given action in the **Owner** column.
- Upgraded `astronomer-providers` to 1.11.2, which includes a collection of bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1112-2022-11-19).
- Upgraded `openlineage-airflow` to 0.17.0, which includes improvements to the OpenLineage spark integration and additional facets for the OpenLineage Python client. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.17.0) for more information.