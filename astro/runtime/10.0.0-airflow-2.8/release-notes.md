## Astro Runtime 10.9.0

- Release date: June 13, 2024
- Airflow version: 2.8.4

### Early access Airflow bug fixes

- Fixed an issue where Airflow might accidentally store dynamic content in a cache, possibly storing sensitive data [(#39550)](https://github.com/apache/airflow/pull/39550)

### Additional improvements

- Upgraded the minor and patch versions of some Astro open source provider packages. See [Astro Runtime 10.9.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-1090)
- Includes `astronomer-providers-logging` version 1.1.5.1

### Security fixes

- [CVE-2024-30251](https://nvd.nist.gov/vuln/detail/CVE-2024-30251)
- [CVE-2024-25142](https://www.cve.org/CVERecord?id=CVE-2024-25142)
- [CVE-2024-32077](https://www.cve.org/CVERecord?id=CVE-2024-32077)

## Astro Runtime 10.8.0

- Release date: April 18, 2024
- Airflow version: 2.8.4

### Additional improvements

- Added functionality for using plugins to generate custom menu items in the Airflow UI. This feature will be fully available on Astro in a future release.
- Updated `sqlparse` to `0.5.0`.
- Upgraded [Gunicorn](https://gunicorn.org/) to `22.0.0`.

### Security fixes

- [CVE-2024-4340](https://www.cve.org/CVERecord?id=CVE-2024-4340)
- [CVE-2024-1135](https://www.cve.org/CVERecord?id=CVE-2024-1135)

#### Ignored CVEs

- [CVE-2024-34069](https://www.cve.org/CVERecord?id=CVE-2024-34069) The underlying vulnerability of this CVE is only relevant to a small set of use cases and scenarios, such as when hosting Airflow publicly on the internet, and is considered low risk for Astro and Software users. Because the resolution would require significant changes to Airflow and its dependencies, this CVE has not been addressed at this time.

## Astro Runtime 10.7.0

- Release date: April 11, 2024
- Airflow version: 2.8.4

### Early access Airflow bug fixes

- Load providers configuration when gunicorn workers start ([#38795](https://github.com/apache/airflow/pull/38795))
- Prevent large objects from being stored in the RTIF ([#38094](https://github.com/apache/airflow/pull/38094))
- Load `consuming_dags` attr eagerly before dataset listener ([#36247](https://github.com/apache/airflow/pull/36247))
- Add "return" statement to "yield" within a while loop in core triggers ([#38389](https://github.com/apache/airflow/pull/38389))
- Improve ExternalTaskSensor Async Implementation ([#36916](https://github.com/apache/airflow/pull/36916))

### Security fixes

- [CVE-2024-31869](https://www.cve.org/CVERecord?id=CVE-2024-31869)

## Astro Runtime 10.6.0

- Release date: March 26, 2024
- Airflow version: 2.8.4

### Airflow 2.8.4

Astro Runtime 10.6.0 includes same-day support for Apache Airflow 2.8.4. Airflow 2.8.4 contains a number of bug fixes including:

- Fix the serialization of dags with `start_date` in a fixed timezone, which could cause the scheduler to crash ([#38139](https://github.com/apache/airflow/pull/38139))
- Fix a bug where the scheduler heartrate wasn't calculated correctly, the parameter needed to calculate scheduler heartrate has been corrected ([#37992](https://github.com/apache/airflow/pull/37992))

For more information, see the [Apache Airflow release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-8-4-2024-03-25).

### Additional improvements

- Upgraded `apache-airflow-providers-google` to version `10.16.0`

### Security fixes

- [CVE-2022-48174](https://www.cve.org/CVERecord?id=CVE-2022-48174)

## Astro Runtime 10.5.0

- Release date: March 11, 2024
- Airflow version: 2.8.3

### Airflow 2.8.3

Astro Runtime 10.5.0 includes same-day support for Apache Airflow 2.8.3. Airflow 2.8.3 contains a number of bug fixes including:

- Fix external_executor_id being overwritten ([#37784](https://github.com/apache/airflow/pull/37784))
- Set parsing context dag_id in dag test command ([#37606](https://github.com/apache/airflow/pull/37606))

For more information, see the [Apache Airflow release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-8-3-2024-03-11).

### Security fixes

- [CVE-2024-28746](https://www.cve.org/CVERecord?id=CVE-2024-28746)

## Astro Runtime 10.4.0

- Release date: February 26, 2024
- Airflow version: 2.8.2

### Airflow 2.8.2

Astro Runtime 10.4.0 includes same-day support for Apache Airflow 2.8.2. Airflow 2.8.2 contains a number of bug fixes including:

- Base date for fetching dag grid view must include selected run_id ([#34887](https://github.com/apache/airflow/pull/34887))
- Change AirflowTaskTimeout to inherit BaseException ([#35653](https://github.com/apache/airflow/pull/35653))

For more information, see the [Apache Airflow release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-8-2-2024-02-26).

### Security fixes

- [CVE-2024-26130](https://www.cve.org/CVERecord?id=CVE-2024-26130)
- [CVE-2024-30251](https://www.cve.org/CVERecord?id=CVE-2024-30251)
- [CVE-2024-26280](https://www.cve.org/CVERecord?id=CVE-2024-26280)
- [CVE-2024-27906](https://www.cve.org/CVERecord?id=CVE-2024-27906)

## Astro Runtime 10.3.0

- Release date: February 1, 2024
- Airflow version: 2.8.1

### Early access Airflow bug fixes

- Fix bug introduced by replacing spaces by + in run_id ([#36877](https://github.com/apache/airflow/pull/36877))
- Remove superfluous `@Sentry.enrich_errors` ([#37002](https://github.com/apache/airflow/pull/37002))

### Additional improvements

- Upgraded the Astro SDK to [1.8.0](https://github.com/astronomer/astro-sdk/releases/tag/1.8.0).

### Bug fixes

- Fixed an issue where some logging features would not work for dag runs with spaces in their dag run IDs.
- Astro Runtime now relies on logic `apache-airflow-providers-openlineage` to determine whether OpenLineage should be enabled or disabled in a given environment, which makes the behavior more consistent between different environments and implementations.
- Fixed an issue where `airflow tasks test <dag_id> <task_id>` always generated an error that stated it was unable to find a foreign key for the table `ab_user`.

## Astro Runtime 10.2.0

- Release date: January 19, 2024
- Airflow version: 2.8.1

### Airflow 2.8.1

Astro Runtime 10.2.0 includes same-day support for Apache Airflow 2.8.1. Airflow 2.8.1 contains a number of bug fixes including:

- Fix scheduler exiting with code 0 on exceptions ([#36880](https://github.com/apache/airflow/pull/36800))
- Fix Callback exception when a removed task is the last one in the task instance list ([#36693](https://github.com/apache/airflow/pull/36693))

For more information, see the [Apache Airflow release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-8-1-2024-01-19).

### Security fixes

- [CVE-2023-50944](https://www.cve.org/CVERecord?id=CVE-2023-50944)
- [CVE-2023-50943](https://www.cve.org/CVERecord?id=CVE-2023-50943)

#### Ignored CVEs

 - [CVE-2024-25128](https://www.cve.org/CVERecord?id=CVE-2024-25128) This CVE applies to OpenID users only. Attackers can gain unauthorized access to the Airflow UI by impersonating any Airflow user. Note this impacts OpenID only, which is long deprecated, and should not be confused with the more common OpenID Connect (ODIC). This scenario does not apply to Astro Runtime users.

## Astro Runtime 10.1.0

- Release date: January 10, 2024
- Airflow version: 2.8.0

### Additional improvements

- You can now set `ASTRO_CLOUDWATCH_TASK_LOGS_LOG_GROUP` and `ASTRO_CLOUDWATCH_TASK_LOGS_GROUP_STREAM` in a Deployment to change the names of the AWS Cloudwatch log groups and streams that Astro uses to organize log events. Create custom names for log streams and groups if you need to set targeted policies for these objects in Cloudwatch, or if you otherwise want to change how task logs are grouped. See [Export task logs to AWS Cloudwatch](export-cloudwatch).
- To improve scheduler performance, the default value for `AIRFLOW__SCHEDULER__MAX_TIS_PER_QUERY` is now `512`.

## Astro Runtime 10.0.0

- Release date: December 18, 2023
- Airflow version: 2.8.0

### Airflow 2.8

Astro Runtime 10.0.0 includes same-day support for Apache Airflow 2.8, which includes a number of new features and improvements. Most notably, Airflow 2.8 includes the following changes:

- The new object storage features make it easier to work with popular object storage systems like S3 and GCS. You can use new  abstract object types to work with files in multiple different object storage systems without writing system-specific code.
- You can now specify extra index URLs in the PythonVirtualEnvOperator, which makes it easier to spin up virtual environments that include private Python packages.
- The Airflow UI **Grid** view now supports filtering on multiple run states at once so that you can compare runs across states.

For more information about the major changes in this release, see the [Airflow blog](https://airflow.apache.org/blog/airflow-2.8.0/).

### Additional improvements

- When you export logs to Datadog from Astro, you can now filter the logs in Datadog by log type.

### Bug fixes

- Fixed an issue in Astro where all Airflow task logs exported to Datadog appeared as `INFO` logs regardless of their actual log type.
- Fixed an issue in Astro where logging features could be disrupted if you set `AZURE_CLIENT_ID` as an environment variable.
- Fixed an issue where Astro audit logs listed a user's name as `User` for trigger events instead of their IDs.