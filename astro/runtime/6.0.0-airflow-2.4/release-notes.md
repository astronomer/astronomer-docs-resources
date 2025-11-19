## Astro Runtime 6.10.0

- Release date: February 28, 2024
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Account for change in UTC offset when calculating next schedule ([#35887](https://github.com/apache/airflow/pull/35887))
- Fix Scheduler crash when clear a previous run of a normal task that is now a mapped task. ([#31352](https://github.com/apache/airflow/pull/31352))
- Revoking audit_log permission from all users except admin ([#37501](https://github.com/apache/airflow/pull/37501))
- Check permissions for ImportError ([#37468](https://github.com/apache/airflow/pull/37468))

## Astro Runtime 6.9.2

- Release date: January 24, 2024
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Stop deserializing pickle when enable_xcom_pickling is False ([#36255](https://github.com/apache/airflow/pull/36255))
- Check dag read permission before accessing dag code ([#36257](https://github.com/apache/airflow/pull/36257))

## Astro Runtime 6.9.1

- Release date: January 9, 2024
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Account for change in UTC offset when calculating next schedule ([35887](https://github.com/apache/airflow/pull/35887))
- Fix scheduler crash when you clear a previous run of a normal task that is now a mapped task ([31352](https://github.com/apache/airflow/pull/31352))

## Astro Runtime 6.9.0

- Release date: December 22, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Check for dag ID in query param from url as well as kwargs ([32014](https://github.com/apache/airflow/pull/32014))
- Check that dag_ids passed in request are consistent ([34366](https://github.com/apache/airflow/pull/34366))
- Fix updating variables during variable imports ([33932](https://github.com/apache/airflow/pull/33932))

## Astro Runtime 6.8.0

- Release date: November 24, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Use pyarrow-hotfix to mitigate CVE-2023-47248 ([35650](https://github.com/apache/airflow/pull/35650))
- Fix Scheduler crash looping when dagrun creation fails ([35135](https://github.com/apache/airflow/pull/35135))

## Astro Runtime 6.7.0

- Release date: October 12, 2023
- Airflow version: 2.4.3

### Airflow bug fixes

- Listener: Simplify API by replacing SQLAlchemy event-listening by direct calls ([29289](https://github.com/apache/airflow/pull/29289))
- Listener: Move success hook to after SQLAlchemy commit ([32988](https://github.com/apache/airflow/pull/32988))
- Fixed bug when updating DagRun state for paused dags
- Fixed permissions for triggerer, datasets, and deleting dags on Astro with a non-Admin user

### Additional Improvements

- Upgraded `openlineage-airflow` to 1.4.1. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/1.4.1) for a complete list of changes.
- Upgraded many OSS providers to newer minor and patch versions.

## Astro Runtime 6.6.0

- Release date: June 13, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Mark `[secrets] backend_kwargs` as a sensitive config ([31788](https://github.com/apache/airflow/pull/31788))

### Additional Improvements

- Upgraded `openlineage-airflow` to 0.27.2. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.27.2) for a complete list of changes.

## Astro Runtime 6.5.0

- Release date: May 29, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Updated error messaging ([31502](https://github.com/apache/airflow/pull/31502))

### Additional Improvements

- Upgraded `astronomer-providers` to 1.16.0. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1160-2023-05-19) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.26.0. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.26.0) for a complete list of changes.
- Blocked the ability to pause the Monitoring dag with the Airflow API. The Monitoring dag is used by Astronomer to operate your Deployments and should not be paused.

## Astro Runtime 6.4.0

- Release date: March 23, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Ensure that `dag.partial_subset` doesn't mutate task group properties ([#30129](https://github.com/apache/airflow/pull/30129))
- redirect to the origin page with all the params ([#29212](https://github.com/apache/airflow/pull/29212))
- datasets, next_run_datasets, remove unnecessary timestamp filter ([#29441](https://github.com/apache/airflow/pull/29441))

### Additional improvements

- Upgraded `astronomer-providers` to 1.15.1, which includes a collection of bug fixes and a new async sensor `SnowflakeSensorAsync`. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1151-2023-03-09) for a complete list of changes..
- Upgraded `openlineage-airflow` to 0.21.1, which includes a collection of bug fixes. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.21.1) for a complete list of changes.
- When using Runtime in an Astronomer Software installation, OpenLineage and the Astronomer monitoring dag are now disabled. OpenLineage can be re-enabled in your Deployment by setting the `OPENLINEAGE_URL` environment variable, or by setting the `OPENLINEAGE_DISABLED=False` environment variable.

## Astro Runtime 6.3.0

- Release date: February 14, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Use time not tries for queued & running re-checks ([28586](https://github.com/apache/airflow/pull/28586))

### Additional improvements

- Upgraded `openlineage-airflow` to 0.20.4, which includes a new extractor for the GCSToGCSOperator. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.17.0) for a complete list of changes.

## Astro Runtime 6.2.1

- Release date: January 26, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

In anticipation of future support for the Kubernetes executor on Astro, Astro Runtime includes the following bug fixes from Apache Airflow:

- Annotate KubernetesExecutor pods that we don’t delete ([28844](https://github.com/apache/airflow/pull/28844))

## Astro Runtime 6.2.0

- Release date: January 26, 2023
- Airflow version: 2.4.3

### Early access Airflow bug fixes

In anticipation of future support for the Kubernetes executor on Astro, Astro Runtime includes the following bug fixes from Apache Airflow:

- Fix bad pods pickled in executor_config ([28454](https://github.com/apache/airflow/pull/28454))
- Be more selective when adopting pods with KubernetesExecutor ([28899](https://github.com/apache/airflow/pull/28899))
- Only patch single label when adopting pod ([28776](https://github.com/apache/airflow/pull/28776))

### Additional improvements

- Upgraded `astronomer-providers` to 1.14.0, which includes support for using a role ARN with `AwsBaseHookAsync`. See the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.13.0/CHANGELOG.rst) for a complete list of changes.
- Upgraded `openlineage-airflow` to 0.19.2, which includes new support for Airflow operators such as the `S3FileTransformOperator` and additional facets for task runs. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.19.2) for a complete list of changes.

## Astro Runtime 6.1.0

- Release date: December 21, 2022
- Airflow version: 2.4.3

### Early access Airflow bug fixes

- Make DagRun state updates for paused dags faster ([#27725](https://github.com/apache/airflow/pull/27725))
- Fix deadlock when chaining multiple empty mapped tasks ([#27964](https://github.com/apache/airflow/pull/27964))

### Additional improvements

- Upgraded `astronomer-providers` to 1.13.0, which includes a collection of minor enhancements and bug fixes. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1130-2022-12-16).
- Upgraded `openlineage-airflow` to 0.18.0, which includes new support for Airflow operators like the `SQLExecuteQueryOperator`. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.18.0) for more information.
- Upgraded `apache-airflow-providers-microsoft-azure` to 5.0.1, which includes a bug fix to revert `offset` and `length` to be optional arguments.
- You can now run Astro Runtime images on Red Hat OpenShift.
- In the Airflow UI for Astro Deployments, the **Audit Logs** page now shows the Astro user who performed a given action in the **Owner** column.
- Airflow environments hosted on Astro now include a **Back to Astro** button in the Airflow UI. Use this button to return to the Deployment hosting the Airflow environment in the Astro UI.
- You can now add comments to the `packages.txt` file of an Astro project.

## Astro Runtime 6.0.4

- Release date: November 14, 2022
- Airflow version: 2.4.3

### ARM64-based images for faster local development with Apple M1

<Warning>To deploy a project using Astro Runtime 6.0.4 or later from an Apple M1 computer to Astro, you must use Astro CLI version 1.4.0 or later or else the deploy will fail. See [Install the Astro CLI](../astro/cli/install-cli).</Warning>

Astro Runtime images now support both AMD64 and ARM64 processor architectures for local development. When you install Astro Runtime 6.0.4 or later, Docker automatically runs the correct architecture based on the computer you're using.

If you run the Astro CLI on a Mac computer that uses an ARM-based [Apple M1 Silicon chip](https://www.apple.com/newsroom/2020/11/apple-unleashes-m1/), you will see a significant performance improvement when running Airflow locally. For example, the time it takes to run `astro dev start` on average has decreased from over 5 minutes to less than 2 minutes.

For more information on developing locally with the Astro CLI, see [Develop a Project](../astro/cli/develop-project).

### Airflow 2.4.3

Astro Runtime 6.0.4 includes same-day support for Airflow 2.4.3, which includes a collection of bug fixes. Fixes include:

- Make `RotatingFilehandler` used in `DagProcessor` non-caching ([27223](https://github.com/apache/airflow/pull/27223))
- Fix double logging with some task logging handler ([27591](https://github.com/apache/airflow/pull/27591))

For a complete list of the changes, see the [Apache Airflow 2.4.3 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-4-3-2022-11-14).

### Additional improvements

- Upgraded `openlineage-airflow` to 0.16.1. This release includes the `DefaultExtractor`, which allows you to extract the default available OpenLineage data for external operators without needing to write a custom extractor. See the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/releases/tag/0.16.1) for more information.
- Upgraded `astronomer-providers` to 1.11.1, which includes bug fixes. For a complete list of the changes, see the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1111-2022-10-28).

## Astro Runtime 6.0.3

- Release date: October 24, 2022
- Airflow version: 2.4.2

### Airflow 2.4.2

Astro Runtime 6.0.3 includes same-day support for Airflow 2.4.2. Some changes in Airflow 2.4.2 include:

- Handle mapped tasks in task duration chart ([#26722](https://github.com/apache/airflow/pull/26722))
- Make tracebacks opt-in ([#27059](https://github.com/apache/airflow/pull/27059))

For a complete list of commits, see the [Apache Airflow 2.4.2 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-4-2-2022-10-23).

### Additional improvements

- Upgraded `openlineage-airflow` to 0.15.1, which includes a dedicated Airflow development environment. You can now create and test changes to custom OpenLineage extractors in an Airflow environment without needing to rebuild your Docker images. For more information, see the [OpenLineage changelog](https://github.com/OpenLineage/OpenLineage/blob/main/CHANGELOG.mdx).

## Astro Runtime 6.0.2

- Release date: September 30, 2022
- Airflow version: 2.4.1

### Airflow 2.4.1

Astro Runtime 6.0.2 includes same-day support for Airflow 2.4.1, which includes a collection of bug fixes. Fixes include:

- Fix Deferrable stuck as scheduled during backfill ([#26205](https://github.com/apache/airflow/pull/26205))
- Don't update backfill run from the scheduler ([#26342](https://github.com/apache/airflow/pull/26342))

For a complete list of commits, see the [Apache Airflow 2.4.1 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-4-1-2022-09-30).

### Early access Airflow bug fixes

Astro Runtime 6.0.2 includes the following bug fixes from Apache Airflow 2.4.2:

- Remove dag parsing from StandardTaskRunner ([#26750](https://github.com/apache/airflow/pull/26750))
- Fix airflow tasks run --local when dags_folder differs from that of processor ([#26509](https://github.com/apache/airflow/pull/26509))
- Add fixture for CLI tests requiring sample dags ([#26536](https://github.com/apache/airflow/pull/26536))

### Additional improvements

- Upgraded `astronomer-providers` to 1.10.0, which includes `SFTPSensorAsync` and `ExternalDeploymentTaskSensorAsync` as new deferrable operators. For a complete list of changes, see the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1100-2022-09-30).

## Astro Runtime 6.0.1

- Release date: September 26, 2022
- Airflow version: 2.4.0

### Bug fixes

- Fixed an issue where Astro users could not access task logs on Deployments using Runtime 6.0.0
- Backported a fix to correct an issue where logs were not loading from Celery workers ([#26493](https://github.com/apache/airflow/pull/26493))
- Fixed [CVE-2022-40674](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-40674)

## Astro Runtime 6.0.0

- Release date: September 19, 2022
- Airflow version: 2.4.0

### Airflow 2.4 and data-aware scheduling

Astro Runtime 6.0.0 provides same-day support for [Airflow 2.4.0](https://airflow.apache.org/blog/airflow-2.4.0/), which delivers significant new features for dag scheduling. The most notable new features in Airflow 2.4.0 are:

- [Data-aware scheduling](https://airflow.apache.org/docs/apache-airflow/2.4.0/concepts/datasets.html), which is a new method for scheduling a dag based on when an upstream dag modifies a specific dataset.
- The [ExternalPythonOperator](https://airflow.apache.org/docs/apache-airflow/2.4.0/howto/operator/python.html#externalpythonoperator), which can execute Python code in a virtual environment with different Python libraries and dependencies than your core Airflow environment.
- Automatic dag registration. You no longer need to specify `as dag` when defining a dag object.
- Support for [zipping](https://airflow.apache.org/docs/apache-airflow/2.4.0/concepts/dynamic-task-mapping.html#combining-upstream-data-aka-zipping) dynamically mapped tasks.

For a complete list of commits, see the [Apache Airflow 2.4.0 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-4-0-2022-09-19).

### Additional improvements

- Upgraded `astronomer-providers` to 1.9.0, which includes two new deferrable versions of the operators from the dbt provider package. See the [Astronomer Providers changelog](https://github.com/astronomer/astronomer-providers/blob/1.9.0/CHANGELOG.rst).