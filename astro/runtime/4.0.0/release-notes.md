## Astro Runtime 4.2.9

- Release date: December 12, 2022
- Airflow version: 2.2.5

### Backported Airflow bug fixes

Astro Runtime 4.2.9 includes the following bug fixes from later Apache Airflow releases:

- Change the template to use human readable task_instance description ([#25960](https://github.com/apache/airflow/pull/25960))

### Additional improvements

- You can now run Astro Runtime images on Red Hat OpenShift.
- You can now add comments to the `packages.txt` file of an Astro project.
- In the Airflow UI for Astro Deployments, the **Audit Logs** page now shows the Astro user who performed a given action in the **Owner** column.

## Astro Runtime 4.2.8

- Release date: November 9, 2022
- Airflow version: 2.2.5

### Backported Airflow bug fixes

Astro Runtime 4.2.8 includes the following bug fixes from Apache Airflow 2.4.2:

- Make tracebacks opt-in ([#27059](https://github.com/apache/airflow/pull/27059))
- Don’t overwrite connection extra with invalid json ([#27142](https://github.com/apache/airflow/pull/27142))
- Simplify origin string cleaning ([#27143](https://github.com/apache/airflow/pull/27143))

## Astro Runtime 4.2.7

- Release date: October 11, 2022
- Airflow version: 2.2.5

### Backported Airflow bug fixes

Astro Runtime 4.2.7 includes the following bug fixes from later Apache Airflow releases:

- Make sure finalizers are not skipped during exception handling ([#22475](https://github.com/apache/airflow/pull/22475))
- Fix `email_on_failure` with `render_template_as_native_obj` ([#22770](https://github.com/apache/airflow/pull/22770))
- Do not log the hook connection details even at DEBUG level ([#22627](https://github.com/apache/airflow/pull/22627))

### Bug fixes

- Fixed the following vulnerabilities:

    - [CVE-2022-40023](https://avd.aquasec.com/nvd/2022/cve-2022-40023/)
    - [CVE-2022-2309](https://avd.aquasec.com/nvd/2022/cve-2022-2309/)
    - [CVE-2022-40674](https://avd.aquasec.com/nvd/2022/cve-2022-40674/)
    - [CVE-2022-1586](https://avd.aquasec.com/nvd/2022/cve-2022-1586/)
    - [CVE-2022-1587](https://avd.aquasec.com/nvd/2022/cve-2022-1587/)
    - [CVE-2022-3999](https://avd.aquasec.com/nvd/2022/cve-2022-3999/)
    - [CVE-2022-37434](https://avd.aquasec.com/nvd/2022/cve-2022-37434/)
    - [DSA-5197](https://www.debian.org/security/2022/dsa-5197)
    - [CVE-2022-2509](https://avd.aquasec.com/nvd/2022/cve-2022-2509/)
    - [CVE-2022-46828](https://avd.aquasec.com/nvd/2022/cve-2022-46828/)
    - [CVE-2022-1664](https://avd.aquasec.com/nvd/2022/cve-2022-1664/)
    - [CVE-2022-29155](https://avd.aquasec.com/nvd/2022/cve-2022-29155/)
    - [CVE-2022-2068](https://avd.aquasec.com/nvd/2022/cve-2022-2068/)
    - [CVE-2022-1292](https://avd.aquasec.com/nvd/2022/cve-2022-1292/)
    - [CVE-2022-1552](https://avd.aquasec.com/nvd/2022/cve-2022-1552/)

## Astro Runtime 4.2.6

- Release date: April 19, 2022
- Airflow version: 2.2.5

### Additional improvements

- Add initial support for Astro Runtime on Google Cloud Platform (GCP), including logging in Google Cloud Storage (GCS). Support for Astro on GCP is coming soon.

## Astro Runtime 4.2.5
- Release date: April 11, 2022
- Airflow version: 2.2.5

### Bug fixes

- Bug Fix: Apply a [new constraints file](https://raw.githubusercontent.com/apache/airflow/constraints-2.2.5/constraints-3.9.txt) to fix a version incompatibility error with `apache-airflow-providers-elasticsearch` that made task logs inaccessible to users in the Airflow UI. This change was required by Astronomer Software and did not impact users on Astro.

## Astro Runtime 4.2.4

- Release date: April 6, 2022
- Airflow version: 2.2.5

### Support for Airflow 2.2.5

Astro Runtime 4.2.2 includes support for Apache Airflow 2.2.5, which exclusively contains bug fixes and performance improvements. For details on the release, read the [Airflow 2.2.5 changelog](https://airflow.apache.org/docs/apache-airflow/stable/changelog.html#airflow-2-2-5-2022-04-04).

## Astro Runtime 4.2.1

- Release date: March 28, 2022
- Airflow version: 2.2.4

### New deferrable operators

Astro Runtime 4.2.1 upgrades the `astronomer-providers` package to v1.1.0 ([CHANGELOG](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#110-2022-03-23)). In addition to bug fixes and performance improvements, this release includes 7 new deferrable operators:

    - `S3KeySizeSensorAsync`
    - `S3KeysUnchangedSensorAsync`
    - `S3PrefixSensorAsync`
    - `GCSObjectsWithPrefixExistenceSensorAsync`
    - `GCSObjectUpdateSensorAsync`
    - `GCSUploadSessionCompleteSensorAsync`
    - `BigQueryTableExistenceSensorAsync`

For more information about deferrable operators and how to use them, see [Deferrable operators](https://www.astronomer.io/docs/learn/deferrable-operators). To access the source code of this package, see the [Astronomer Providers GitHub repository](https://github.com/astronomer/astronomer-providers).

### Additional improvements

- Bump the [`openlineage-airflow` provider package](https://openlineage.io/docs/integrations/airflow/) to `v0.6.2`

## Astro Runtime 4.2.0

- Release date: March 10, 2022
- Airflow version: 2.2.4

### New Astronomer Providers package

The `astronomer-providers` package is now installed on Astro Runtime by default. This package is an open source collection of Apache Airflow providers and modules that is maintained by Astronomer. It includes deferrable versions of popular operators such as `ExternalTaskSensor`, `DatabricksRunNowOperator`, and `SnowflakeOperator`.

For more information, see [Deferrable operators](https://www.astronomer.io/docs/learn/deferrable-operators). To access the source code of this package, see the [Astronomer Providers GitHub repository](https://github.com/astronomer/astronomer-providers).

### Additional improvements

- Bump the [`openlineage-airflow` provider package](https://openlineage.io/docs/integrations/airflow/) to `v0.6.1`

## Astro Runtime 4.1.0

- Release date: February 22, 2022
- Airflow version: 2.2.4

### Support for Airflow 2.2.4

Astro Runtime 4.1.0 includes support for Apache Airflow 2.2.4, which exclusively contains bug fixes and performance improvements. For details on the release, read the [Airflow 2.2.4 changelog](https://airflow.apache.org/docs/apache-airflow/stable/changelog.html#airflow-2-2-4-2022-02-22).

## Astro Runtime 4.0.11

- Release date: February 14, 2022
- Airflow version: 2.2.3

### Additional improvements

- Upgraded the `openlineage-airflow` library to `v0.5.2`

## Astro Runtime 4.0.10

- Release date: February 9, 2022
- Airflow version: 2.2.3

### New deferrable operators now available

Astro Runtime now also includes the following operators:

- `KubernetesPodOperatorAsync`
- `HttpSensorAsync`
- `SnowflakeOperatorAsync`
- `FileSensorAsync`

These are all [deferrable operators](https://www.astronomer.io/docs/learn/deferrable-operators) built by Astronomer and available exclusively on Astro Runtime. They are pre-installed into the Astro Runtime Docker image and ready to use.

### Additional improvements

- The Airflow UI now shows the Deployment's Docker image tag in the footer of all pages. For more information, see [Astro Release Notes for March 10, 2022](release-notes.md#march-10-2022).

### Additional improvements

- To support an enhanced logging experience on Astro, the `apache-airflow-providers-elasticsearch` provider package is now installed by default.

## Astro Runtime 4.0.9

- Release date: January 19, 2022
- Airflow version: 2.2.3

### Additional improvements

- The [`openlineage-airflow` provider package](https://openlineage.io/docs/integrations/airflow/) is now installed in Runtime by default.

## Astro Runtime 4.0.8

- Release date: December 21, 2021
- Airflow version: 2.2.3

### Support for Airflow 2.2.3

Astro Runtime 4.0.8 includes support for [Airflow 2.2.3](https://airflow.apache.org/docs/apache-airflow/stable/changelog.html#airflow-2-2-3-2021-12-20).

Airflow 2.2.3 exclusively contains bug fixes, including:
- Fix for a broken link to task logs in the Gantt view of the Airflow UI ([#20121](https://github.com/apache/airflow/pull/20121))
- Replace references to "Execution Date" in the Task Instance and DAG run tables of the Airflow UI with "Logical Date" ([#19063](https://github.com/apache/airflow/pull/19063))
- Fix problem whereby requests to the `DAGRun` endpoint of Airflow's REST API would return a 500 error if DAG run is in state `skipped` ([#19898](https://github.com/apache/airflow/pull/19898))
- Fix problem where task logs in Airflow UI showed incorrect timezone ([#19401](https://github.com/apache/airflow/pull/19401))
- Fix problem where the **Connections** form in the Airflow UI showed incorrect field names ([#19411](https://github.com/apache/airflow/pull/19411))

### Bug fixes

- Disabled the **Pause** button for `astronomer_monitoring_dag`, which cannot be disabled and helps the Astronomer team monitor the health of your Deployment.

## Astro Runtime 4.0.7

- Release date: December 15, 2021
- Airflow version: 2.2.2

### Astronomer monitoring DAG

Astro Runtime 4.0.7 includes a monitoring DAG that is pre-installed in the Docker image and enabled for all customers. In addition to existing Deployment health and metrics functionality, this DAG allows the Astronomer team to better monitor the health of your data plane by enabling real-time visibility into whether your workers are healthy and tasks are running.

The `astronomer_monitoring_dag` runs a simple bash task every 5 minutes to ensure that your Airflow scheduler and workers are functioning as expected. If the task fails twice in a row or is not scheduled within a 10-minute interval, Astronomer support receives an alert and will work with you to troubleshoot.

Because this DAG is essential to Astro's managed service, your organization will not be charged for its task runs. For the same reasons, this DAG can't be modified or disabled via the Airflow UI. To modify how frequently this DAG runs, you can specify an alternate schedule as a cron expression by setting `AIRFLOW_MONITORING_DAG_SCHEDULE_INTERVAL` as an environment variable.

## Astro Runtime 4.0.6

- Release date: December 2, 2021
- Airflow version: 2.2.2

### Additional improvements

- User-supplied `airflow.cfg` files are no longer valid in Astro projects. [Environment variables](environment-variables.md) are now the only valid method for setting Airflow configuration options.

### Bug fixes

- Fixed an issue where the **Browse** menu of the Airflow UI was hidden in some versions of Astro Runtime

## Astro Runtime 4.0.5

- Release date: November 29, 2021
- Airflow version: 2.2.2

### Bug fixes

- Fixed an issue where Astro's S3 logging hook prevented users from setting up S3 as a custom XCom backend

## Astro Runtime 4.0.4

- Release date: November 19, 2021
- Airflow version: 2.2.2

### Bug fixes

- Fixed an issue where DAG run and task instance records didn't show up as expected in the Airflow UI

## Astro Runtime 4.0.3

- Release date: November 15, 2021
- Airflow version: 2.2.2

### Additional improvements

- Added support for [Airflow 2.2.2](https://airflow.apache.org/docs/apache-airflow/stable/changelog.html#airflow-2-2-2-2021-11-15), which includes a series of bug fixes for timetables, DAG scheduling, and database migrations. Most notably, it resolves an issue where some DAG runs would be missing in the Airflow UI if `catchup=True` was set.

### Bug fixes

- Fixed an issue where the Astro-themed Airflow UI was not present in local development

## Astro Runtime 4.0.2

- Release date: October 29, 2021
- Airflow version: 2.2.1

### Additional improvements

- Added support for [Airflow 2.2.1](https://airflow.apache.org/docs/apache-airflow/stable/changelog.html#airflow-2-2-1-2021-10-29), which includes a series of bug fixes that address intermittent problems with database migrations from Airflow 2.1 to Airflow 2.2

## Astro Runtime 4.0.1

- Release date: October 26, 2021
- Airflow version: 2.2.0

### Bug fixes

- Fixed an issue where worker pods were stuck in a terminating state when scaling down
- Fixed an issue where the Airflow UI navbar and footer did not show the correct running version of Astro Runtime

## Astro Runtime 4.0.0

- Release date: October 12, 2021
- Airflow version: 2.2.0

### Support for Airflow 2.2.0

Astro Runtime 4.0.0 is a significant release that supports and enhances [Apache Airflow 2.2.0](https://airflow.apache.org/blog/airflow-2.2.0/), an exciting milestone in the open source project. Most notably, this release introduces custom timetables and deferrable operators.

#### Custom timetables

Timetables represent a powerful new framework that allows Airflow users to create custom schedules using Python. In an effort to provide more flexibility and address known limitations imposed by cron, timetables use an intuitive `data_interval` that, for example, allows you to schedule a DAG to run daily on Monday through Friday, but not on the weekend. Timetables can be easily plugged into existing DAGs, which means that it's easy to create your own or use community-developed timetables in your project.

In addition to supporting the timetables framework, the team at Astronomer has built a `TradingHoursTimetable` that's ready to use in Runtime 4.0.0. You can use this timetable to run a DAG based on whether or not a particular global market is open for trade.

For more information on using timetables, read the [Apache Airflow Documentation](https://airflow.apache.org/docs/apache-airflow/stable/howto/timetable.html).

#### Deferrable operators

[Deferrable operators](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/deferring.html) are a new type of Airflow operator that promises improved performance and lower resource costs. While standard operators and sensors take up a worker slot even when they are waiting for an external trigger, deferrable operators are designed to suspend themselves and free up that worker slot while they wait. This is made possible by a new, lightweight Airflow component called the triggerer.

Existing Airflow operators have to be re-written according to the deferrable operator framework. In addition to supporting those available in the open source project, Astronomer has built an exclusive collection of deferrable operators in Runtime 4.0.0. This collection includes the `DatabricksSubmitRunOperator`, the `DatabricksRunNowOperator`, and the `ExternalTaskSensor`. These are designed to be drop-in replacements for corresponding operators currently in use.

As part of supporting deferrable operators, the triggerer is now available as a fully managed component on Astro. This means that you can start using deferrable operators in your DAGs as soon as you're ready. For more general information on deferrable operators, as well as how to use Astronomer's exclusive deferrable operators, read [Deferrable operators](https://www.astronomer.io/docs/learn/deferrable-operators).