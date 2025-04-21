## Astro Runtime 5.5.0

- Release date: November 27, 2023
- Airflow version: 2.3.4

### Early access Airflow bug fixes

- Listener: Set task on sqlalchemy taskinstance object ([27167](https://github.com/apache/airflow/pull/27167))
- Listener: Simplify API by replacing SQLAlchemy event-listening by direct calls ([29289](https://github.com/apache/airflow/pull/29289))
- Listener: move success hook to after SQLAlchemy commit ([32988](https://github.com/apache/airflow/pull/32988))
- Use pyarrow-hotfix to mitigate CVE-2023-47248 ([35650](https://github.com/apache/airflow/pull/35650))
- Fix Scheduler crash looping when dagrun creation fails ([35135](https://github.com/apache/airflow/pull/35135))

### Bug fixes

- Blocked the ability to pause the Monitoring DAG with the Airflow API. The Monitoring DAG is used by Astronomer to operate your Deployments and should not be paused.

## Astro Runtime 5.4.0

- Release date: March 23, 2023
- Airflow version: 2.3.4

### Early access Airflow bug fixes

- Ensure that `dag.partial_subset` doesn't mutate task group properties ([#30129](https://github.com/apache/airflow/pull/30129))

### Additional improvements

- Upgraded `astronomer-providers` to 1.15.1, which includes a collection of bug fixes and a new async sensor `SnowflakeSensorAsync`. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1151-2023-03-09) for a complete list of changes..
- Upgraded `openlineage-airflow` to 0.21.1, which includes a collection of bug fixes. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.21.1) for a complete list of changes.
- When using Runtime in an Astronomer Software installation, OpenLineage and the Astronomer monitoring DAG are now disabled. OpenLineage can be re-enabled in your Deployment by setting the `OPENLINEAGE_URL` environment variable, or by setting the `OPENLINEAGE_DISABLE=False` environment variable.

## Astro Runtime 5.3.0

- Release date: February 14, 2023
- Airflow version: 2.3.4

### Early access Airflow bug fixes

- Use time not tries for queued & running re-checks ([28586](https://github.com/apache/airflow/pull/28586))

### Additional improvements

- Upgraded `openlineage-airflow` to 0.20.4, which includes a new extractor for the GCSToGCSOperator. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.17.0) for a complete list of changes.

## Astro Runtime 5.2.1

- Release date: January 26, 2023
- Airflow version: 2.3.4

### Early access Airflow bug fixes

In anticipation of future support for the Kubernetes executor on Astro, Astro Runtime includes the following bug fixes from Apache Airflow:

- Annotate KubernetesExecutor pods that we don’t delete ([28844](https://github.com/apache/airflow/pull/28844))

## Astro Runtime 5.2.0

- Release date: January 26, 2023
- Airflow version: 2.3.4

### Early access Airflow bug fixes

In anticipation of future support for the Kubernetes executor on Astro, Astro Runtime includes the following bug fixes from Apache Airflow:

- Fix bad pods pickled in executor_config ([28454](https://github.com/apache/airflow/pull/28454))
- Be more selective when adopting pods with KubernetesExecutor ([28899](https://github.com/apache/airflow/pull/28899))
- Only patch single label when adopting pod ([28776](https://github.com/apache/airflow/pull/28776))
- Don’t re-patch pods that are already controlled by current worker ([26778](https://github.com/apache/airflow/pull/26778))
- Fix backfill queued task getting reset to scheduled state ([23720](https://github.com/apache/airflow/pull/23720))

### Additional improvements

- Upgraded `astronomer-providers` to 1.14.0, which includes support for using a role ARN with `AwsBaseHookAsync`. See the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.13.0/CHANGELOG.rst) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.19.2, which includes new support for Airflow operators like the `S3FileTransformOperator` and additional facets for task runs. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.19.2) for a complete list of changes.

## Astro Runtime 5.1.0

- Release date: January 4, 2023
- Airflow version: 2.3.4

### Additional improvements

- Upgraded `astronomer-providers` to 1.13.0, which includes a collection of minor enhancements and bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1130-2022-12-16).
- Upgraded `openlineage-airflow` to 0.18.0, which includes new support for Airflow operators like the `SQLExecuteQueryOperator`. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.18.0) for more information.
- Airflow environments hosted on Astro now include a **Back to Astro** button in the Airflow UI. Use this button to return to the Deployment hosting the Airflow environment in the Astro UI.

## Astro Runtime 5.0.13

- Release date: December 12, 2022
- Airflow version: 2.3.4

### Backported Airflow bug fixes

Astro Runtime 5.0.13 includes the following bug fixes from later Apache Airflow releases:

- Change the template to use human readable task_instance description ([#25960](https://github.com/apache/airflow/pull/25960))
- Fix deadlock when chaining multiple empty mapped tasks ([#27964](https://github.com/apache/airflow/pull/27964))

### Additional improvements

- You can now run Astro Runtime images on Red Hat OpenShift.
- You can now add comments to the `packages.txt` file of an Astro project.
- In the Airflow UI for Astro Deployments, the **Audit Logs** page now shows the Astro user who performed a given action in the **Owner** column.

## Astro Runtime 5.0.12

- Release date: November 9, 2022
- Airflow version: 2.3.4

### Backported Airflow bug fixes

Astro Runtime 5.0.12 includes the following bug fixes from Apache Airflow 2.4.2:

- Make tracebacks opt-in ([#27059](https://github.com/apache/airflow/pull/27059))
- Avoid 500 on dag redirect ([#27064](https://github.com/apache/airflow/pull/27064))
- Don’t overwrite connection extra with invalid json ([#27142](https://github.com/apache/airflow/pull/27142))
- Simplify origin string cleaning ([#27143](https://github.com/apache/airflow/pull/27143))

## Astro Runtime 5.0.11

- Release date: November 2, 2022
- Airflow version: 2.3.4

### Backported Airflow bug fixes

Astro Runtime 5.0.11 includes the following bug fix from later Apache Airflow releases:

- Fix warning when using xcomarg dependencies ([#26801](https://github.com/apache/airflow/pull/26801))

### Bug fixes

- Removed the default value for `AIRFLOW__LOGGING__REMOTE_BASE_LOG_FOLDER`, as this value is now set in the Astro data plane. This enables Astronomer Software users to set a value for custom remote logging storage solutions.

## Astro Runtime 5.0.10

- Release date: October 17, 2022
- Airflow version: 2.3.4

### Additional improvements

- Upgraded `astronomer-providers` to 1.10.0, which includes two new deferrable versions of operators, `SFTPSensorAsync` and `ExternalDeploymentTaskSensorAsync`. See the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.10.0/CHANGELOG.rst).
- Upgraded `openlineage-airflow` to version `0.15.1`. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.md).

### Bug fixes

- Revert “Cache the custom secrets backend so the same instance gets re-used” ([#25556](https://github.com/apache/airflow/pull/25556))
- Fixed faulty Kubernetes executor config serialization logic

## Astro Runtime 5.0.9

- Release date: September 20, 2022
- Airflow version: 2.3.4

### Early access Airflow bug fixes

- Fixed an issue where logs were not loading from Celery workers ([#26337](https://github.com/apache/airflow/pull/26337) and [#26493](https://github.com/apache/airflow/pull/26493))
- Fixed CVE-2022-40754 ([#26409](https://github.com/apache/airflow/pull/26409))
- Fixed the Airflow UI not auto-refreshing when scheduled tasks are running. This bug was introduced in Airflow 2.3.4 ([#25950](https://github.com/apache/airflow/pull/25950))
- Fixed an issue where the scheduler could crash when queueing dynamically mapped tasks ([#25788](https://github.com/apache/airflow/pull/25788))

### Additional improvements

- Set `AIRFLOW__CELERY__STALLED_TASK_TIMEOUT=600` by default. This means that tasks that are in `queued` state for more than 600 seconds (10 minutes) will fail. This environment variable can be overridden on Astro but will help prevent tasks from getting stuck in a queued state.
- Upgraded `astronomer-providers` to 1.8.1, which includes various bug fixes. For a complete list of changes, see the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#181-2022-09-01).
- Upgraded `openlineage-airflow` to 0.13.0, which includes fixes for Spark integrations. See the [Astronomer Providers changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.md#0141---2022-09-07).

## Astro Runtime 5.0.8

- Release date: August 23, 2022
- Airflow version: 2.3.4

### Airflow 2.3.4

Astro Runtime 5.0.8 includes Airflow 2.3.4, which primarily includes bug fixes. For a complete list of commits, see the [Apache Airflow 2.3.4 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-3-4-2022-08-23).

### Additional improvements

- Upgraded `astronomer-providers` to version `1.8.0`, which includes minor bug fixes and performance enhancements. For more information, see the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.8.0/CHANGELOG.rst).
- Upgraded `openlineage-airflow` to version `0.13.0`, which includes support for Azure Cosmos DB. For a list of all changes, see the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.md).

## Astro Runtime 5.0.7

- Release date: August 16, 2022
- Airflow version: 2.3.3

### Early access Airflow bug fixes

Astro Runtime 5.0.7 includes the following bug fixes:

- Fixed an issue where [plugins specified as a python package](https://airflow.apache.org/docs/apache-airflow/stable/plugins.html#plugins-as-python-packages) in an `entry_points` argument were incorrectly loaded twice by Airflow and resulted in an error in the Airflow UI. This bug was introduced in Airflow 2.3.3 ([#25296](https://github.com/apache/airflow/pull/25296))
- Fixed an issue where zombie tasks were not properly cleaned up from DAGs with parse errors [#25550](https://github.com/apache/airflow/pull/25550))
- Fixed an issue where clearing a deferred task instance would not clear its `next_method` field ([#23929](https://github.com/apache/airflow/pull/23929))

These changes were backported from Apache Airflow 2.3.4, which is not yet generally available. The bug fixes were also backported to Astro Runtime 5.0.5.

### Additional improvements

- The Astro UI no longer shows source code for [supported Airflow operators](https://openlineage.io/docs/integrations/about#capability-matrix) by default. To reenable this feature for a given Deployment, create an [environment variable](environment-variables.md) with a key of `OPENLINEAGE_AIRFLOW_DISABLE_SOURCE_CODE` and a value of `False`.
- Upgraded `openlineage-airflow` to version `0.12.0`, which includes support for Spark 3.3.0 and Apache Flink. For a list of all changes, see the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.md).
- Upgraded `astronomer-providers` to version `1.7.1`, which includes new deferrable operators and improvements to documentation. For more information, see the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.7.1/CHANGELOG.rst).
- Upgraded `apache-airflow-providers-amazon` to version `4.1.0`, which includes a bug fix for integrating with AWS Secrets Manager.

## Astro Runtime 5.0.6

- Release date: July 11, 2022
- Airflow version: 2.3.3

### Airflow 2.3.3

Astro Runtime 5.0.6 includes Airflow 2.3.3, which includes bug fixes and UI improvements. For a complete list of commits, see the [Apache Airflow 2.3.3 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-3-3-2022-07-05).

### Additional improvements

- Upgraded `astronomer-providers` to 1.6.0, which includes new deferrable operators and support for OpenLineage extractors. For more information, see the [Astronomer Providers changelog](https://astronomer-providers.readthedocs.io/en/stable/changelog.html#id1).

### Bug fixes

- Fixed zombie task handling with multiple schedulers ([#24906](https://github.com/apache/airflow/pull/24906))
- Fixed an issue where `TriggerDagRunOperator.operator_extra_links` could cause a serialization error ([#24676](https://github.com/apache/airflow/pull/24676)

## Astro Runtime 5.0.5

- Release date: July 1, 2022
- Airflow version: 2.3.2

### Early access Airflow bug fixes

Astro Runtime 5.0.5 includes the following bug fixes:

- Fixed an issue where part of the **Grid** view of the Airflow UI would crash or become unavailable if a `GET` request to the Airflow REST API failed ([#24152](https://github.com/apache/airflow/pull/24152))
- Improved the performance of the **Grid** view ([#24083](https://github.com/apache/airflow/pull/24083))
- Fixed an issue where grids for task groups in the **Grid** view always showed data for the latest DAG run instead of the correct DAG run ([#24327](https://github.com/apache/airflow/pull/24327))

These changes were backported from Apache Airflow 2.3.3, which is not yet generally available.

### Additional improvements

- Updated `openlineage-airflow` to v0.10.0. This release includes a built-in `SnowflakeOperatorAsync` extractor for Airflow, an `InMemoryRelationInputDatasetBuilder` for `InMemory` datasets for Spark, and the addition of a copyright statement to all source files

## Astro Runtime 5.0.4

- Release date: June 15, 2022
- Airflow version: 2.3.2

### Additional improvements

- Update `astronomer-providers` to v1.5.0. For more information, see the [Astronomer Providers Changelog](https://astronomer-providers.readthedocs.io/en/stable/changelog.html#id1).
- Add support for Astro clusters with [Istio](https://istio.io/) enabled.

## Astro Runtime 5.0.3

- Release date: June 4, 2022
- Airflow version: 2.3.2

### Airflow 2.3.2

Astro Runtime 5.0.3 includes support for Airflow 2.3.2, which includes:

- Improvements to the Grid view of the Airflow UI, including faster load times for large DAGs and a fix for an issue where some tasks would not render properly ([#23947](https://github.com/apache/airflow/pull/23947))
- Enable clicking on DAG owner in autocomplete dropdown ([#23804](https://github.com/apache/airflow/pull/23804))
- Mask sensitive values for task instances that are not yet running ([#23807](https://github.com/apache/airflow/pull/23807))
- Add cascade to `dag_tag` to `dag` foreign key ([#23444](https://github.com/apache/airflow/pull/23444))

For more information, see the [changelog for Apache Airflow 2.3.2](https://github.com/apache/airflow/releases/tag/2.3.2).

### Additional improvements

- Update `astronomer-providers` to v1.4.0. For more information, see the [Astronomer Providers Changelog](https://astronomer-providers.readthedocs.io/en/stable/changelog.html#id1).
- Update `openlineage-airflow` to v0.9.0. This release includes a fix for an issue present in v0.7.1, v0.8.1, and v0.8.2 where some tasks run with the Snowflake operator would deadlock and not execute. For more information, see the [OpenLineage GitHub repository](https://github.com/OpenLineage/OpenLineage/tree/main/integration/airflow).

## Astro Runtime 5.0.2

- Release date: May 27, 2022
- Airflow version: 2.3.1

### Airflow 2.3.1

Astro Runtime 5.0.2 includes same-day support for Airflow 2.3.1, a release that follows Airflow 2.3.0 with a collection of bug fixes.

Fixes include:

- Automatically reschedule stalled queued tasks in Celery executor ([#23690](https://github.com/apache/airflow/pull/23690))
- Fix secrets rendered in Airflow UI when task is not executed ([#22754](https://github.com/apache/airflow/pull/22754))
- Performance improvements for faster database migrations to Airflow 2.3

For more information, see the [changelog for Apache Airflow 2.3.1](https://github.com/apache/airflow/releases/tag/2.3.1).

### Additional improvements

- Update `astronomer-providers` to v1.3.1. For more information, see the [Astronomer Providers Changelog](https://astronomer-providers.readthedocs.io/en/stable/changelog.html#id5).
- Update `openlineage-airflow` to v0.8.2. For more information, see the [OpenLineage GitHub repository](https://github.com/OpenLineage/OpenLineage/tree/main/integration/airflow).

## Astro Runtime 5.0.1

- Release date: May 9, 2022
- Airflow version: 2.3.0

### Astronomer Providers 1.2.0

Astro Runtime 5.0.1 includes v1.2.0 of the `astronomer-providers` package ([CHANGELOG](https://astronomer-providers.readthedocs.io/en/stable/)). This release includes 5 new [deferrable operators](https://www.astronomer.io/docs/learn/deferrable-operators):

    - `DataprocSubmitJobOperatorAsync`
    - `EmrContainerSensorAsync`
    - `EmrStepSensorAsync`
    - `EmrJobFlowSensorAsync`
    - `LivyOperatorAsync`

To access the source code of this package, visit the [Astronomer Providers GitHub repository](https://github.com/astronomer/astronomer-providers).

### Additional improvements

- Improved performance when upgrading to Astro Runtime 5.0.x
- Bumped the [`openlineage-airflow` dependency](https://openlineage.io/docs/integrations/airflow/) to `v0.8.1`

## Astro Runtime 5.0.0

- Release date: April 30, 2022
- Airflow version: 2.3.0

### Support for Airflow 2.3 & dynamic task mapping

Astro Runtime 5.0.0 provides support for [Airflow 2.3.0](https://airflow.apache.org/blog/airflow-2.3.0/), which is a significant open source release. The most notable new features in Airflow 2.3.0 are:

- [Dynamic task mapping](https://airflow.apache.org/docs/apache-airflow/2.3.0/concepts/dynamic-task-mapping.html), which allows you to generate task instances at runtime based on changing data and input conditions.
- A new **Grid** view in the Airflow UI that replaces the **Tree** view and provides a more intuitive way to visualize the state of your tasks.
- The ability to [define Airflow connections in JSON](https://airflow.apache.org/docs/apache-airflow/2.3.0/howto/connection.html#json-format-example) instead of as a Connection URI.
- The ability to [reuse a decorated task function](https://airflow.apache.org/docs/apache-airflow/2.3.0/tutorial_taskflow_api.html#reusing-a-decorated-task) between DAGs.

For more information on Airflow 2.3, see ["Apache Airflow 2.3 — Everything You Need to Know"](https://www.astronomer.io/blog/apache-airflow-2-3-everything-you-need-to-know) by Astronomer.

