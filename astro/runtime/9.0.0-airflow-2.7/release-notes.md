## Astro Runtime 9.21.0

- Release date: December 6, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Restore `add_input_dataset` and `add_output_dataset` in NoOpCollector for backward compatibility. [#44681](https://github.com/apache/airflow/pull/44681)

## Astro Runtime 9.20.0

- Release date: November 19, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Masked configuration values that are irrelevant to the dag author [#43040](https://github.com/apache/airflow/pull/43040)
- Improved handling of value masking of the set variable [#43123](https://github.com/apache/airflow/pull/43123)
- Fixed a bug where the executor would not clean up terminated task instances that go too long without a heartbeat [#42932](https://github.com/apache/airflow/pull/42932)

### Additional improvements

- Upgraded the minor and patch versions of several open-source provider packages. See [Astro Runtime 9.20.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9200)

## Astro Runtime 9.19.5

- Release date: October 17, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Backported a fix to solve issues with dag serialization when the `dags` folder is a symlink. ([#42197](https://github.com/apache/airflow/pull/42197))

## Astro Runtime 9.19.4

- Release date: October 2, 2024
- Airflow version: 2.7.3

### Additional improvements

- Add logging around listener.

## Astro Runtime 9.19.3

- Release date: September 6, 2024
- Airflow version: 2.7.3

### Additional improvements

- Update the Airflow startup sequence to better isolate dag authors.
- Included open-source provider packages reference. See [Astro Runtime 9.19.3 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9193)

### Security Fixes

- Fixed [CVE-2024-45034](https://www.cve.org/CVERecord?id=CVE-2024-45034)

## Astro Runtime 9.19.2

- Release date: September 2, 2024
- Airflow version: 2.7.3

### Bug fixes

- Resolved a dag parsing issue where dags were not marked as stale if the `AIRFLOW__CORE__DAGS_FOLDER` was changed. ([#41433](https://github.com/apache/airflow/pull/41433))
- LocalTaskJob no longer fails on heartbeat due to temporary database connection losses. ([#41704](https://github.com/apache/airflow/pull/41704))

## Astro Runtime 9.19.1

- Release date: August 21, 2024
- Airflow version: 2.7.3

### Additional improvements

- Updated provider packages docs for patch version. See [Astro Runtime 9.19.1 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9191).

### Bug fixes

- Fix the BigQueryInsertJobOperator job cancellation issue by requiring `gcloud-aio-bigquery` version 7.1.0 or higher.

## Astro Runtime 9.19.0

- Release date: August 15, 2024
- Airflow version: 2.7.3

### Additional improvements

- Downgrade `apache-airflow-providers-openlineage` to `1.8.0` to prevent scheduler OOM with complex dags
- Upgraded the minor and patch versions of some open-source provider packages. See [Astro Runtime 9.19.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9190).

## Astro Runtime 9.18.0

- Release date: August 15, 2024
- Airflow version: 2.7.3

### Additional improvements

- If the `Taskinstance` state is `skipped`, also skip checking `subdaglist` ([#40578](https://github.com/apache/airflow/pull/40578))
- Added validation for the project URL that comes from installed providers, before displaying the URL in views ([#40933](https://github.com/apache/airflow/pull/40933))
- Upgraded the minor and patch versions of some open-source provider packages. See [Astro Runtime 9.18.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9180).

## Astro Runtime 9.17.0

- Release date: July 18, 2024
- Airflow version: 2.7.3

### Additional improvements

- Upgraded the minor and patch versions of some Astro open source provider packages. See [Astro Runtime 9.17.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9170)

### Security fixes

- Fixed [CVE-2024-6345](https://www.cvedetails.com/cve/CVE-2024-6345/)

## Astro Runtime 9.16.0

- Release date: July 10, 2024
- Airflow version: 2.7.3

### Additional improvements

- Upgraded the minor and patch versions of some Astro open source provider packages. See [Astro Runtime 9.16.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9160)

### Security fixes

- Fixed [CVE-2024-39863](https://www.cve.org/CVERecord?id=CVE-2024-39863)
- Fixed [CVE-2024-39877](https://www.cve.org/CVERecord?id=CVE-2024-39877)

## Astro Runtime 9.15.0

- Release date: June 12, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Fixed an issue where Airflow might accidentally store dynamic content in a cache, possibly storing sensitive data [(#39550)](https://github.com/apache/airflow/pull/39550)

### Additional improvements

- Upgraded the minor and patch versions of some Astro open source provider packages. See [Astro Runtime 9.15.0 provider packages](https://www.astronomer.io/docs/astro/runtime-provider-reference#astro-runtime-9150)
- Includes `astronomer-providers-logging` version 1.1.5.1

### Bug fixes

- Fixed a bug where liveness/readiness probes might periodically fail when trying to remove a configuration file that did not exist.

### Security fixes

- [CVE-2024-25142](https://www.cve.org/CVERecord?id=CVE-2024-25142)
- [CVE-2023-48291](https://www.cve.org/CVERecord?id=CVE-2023-48291)
- [CVE-2023-47265](https://www.cve.org/CVERecord?id=CVE-2023-47265)
- [CVE-2023-49920](https://www.cve.org/CVERecord?id=CVE-2023-49920)
- [CVE-2023-50783](https://www.cve.org/CVERecord?id=CVE-2023-50783)

## Astro Runtime 9.14.0

- Release date: May 13, 2024
- Airflow version: 2.7.3

### Additional improvements

- Added the [`apache-airflow-providers-mysql`](https://airflow.apache.org/docs/apache-airflow-providers-mysql/stable/index.html) provider
- Upgraded some OSS providers' minor and patch versions

### Bug fixes

- Fixed ([CVE-2024-30251](https://nvd.nist.gov/vuln/detail/CVE-2024-30251))

### Security fixes

- [CVE-2024-30251](https://www.cve.org/CVERecord?id=CVE-2024-30251)

## Astro Runtime 9.13.0

- Release date: April 18, 2024
- Airflow version: 2.7.3

### Additional improvements

- Added functionality for using plugins to generate custom menu items in the Airflow UI. This feature will be fully available on Astro in a future release.
- Upgraded [Gunicorn](https://gunicorn.org/) to `22.0.0`.
- Updated the version of `sqlparse` to `0.5.0`.

### Bug fixes

- Fixed a bug where the **Cluster Activity** tab was missing from the Airflow UI.

### Security fixes

- [CVE-2024-1135](https://www.cve.org/CVERecord?id=CVE-2024-1135)

## Astro Runtime 9.12.0

- Release date: April 11, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Load providers configuration when gunicorn workers start ([#38795](https://github.com/apache/airflow/pull/38795))
- Prevent large objects from being stored in the RTIF ([#38094](https://github.com/apache/airflow/pull/38094))
- Load `consuming_dags` attr eagerly before dataset listener ([#36247](https://github.com/apache/airflow/pull/36247))
- Add "return" statement to "yield" within a while loop in core triggers ([#38389](https://github.com/apache/airflow/pull/38389))
- Improve ExternalTaskSensor Async Implementation ([#36916](https://github.com/apache/airflow/pull/36916))

### Security fixes

- [CVE-2022-48174](https://www.cve.org/CVERecord?id=CVE-2022-48174)

## Astro Runtime 9.11.0

- Release date: February 26, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Simplify dag trigger UI ([#34567](https://github.com/apache/airflow/pull/34567))
- Hide logical date and run id in trigger UI form ([#35284](https://github.com/apache/airflow/pull/35284))
- Allow pre-population of trigger form values via URL parameters ([#37497](https://github.com/apache/airflow/pull/37497))
- Fix regression on trigger form error display on form validation ([#37672](https://github.com/apache/airflow/pull/37672))
- Revert the sequence of initializing configuration defaults ([#37155](https://github.com/apache/airflow/pull/37155))
- Bugfix Triggering dag with parameters is mandatory when show_trigger_form_if_no_params is enabled ([#37063](https://github.com/apache/airflow/pull/37063))
- Revert "Fix future DagRun rarely triggered by race conditions when max_active_runs reached its upper limit. ([#37596](https://github.com/apache/airflow/pull/37596))
- Revoking audit_log permission from all users except admin ([#37501](https://github.com/apache/airflow/pull/37501))
- Check permissions for ImportError ([#37468](https://github.com/apache/airflow/pull/37468))

### Security fixes

- [CVE-2024-26130](https://www.cve.org/CVERecord?id=CVE-2024-26130)
- [CVE-2024-27906](https://www.cve.org/CVERecord?id=CVE-2024-27906)
- [CVE-2024-26280](https://www.cve.org/CVERecord?id=CVE-2024-26280)

#### Ignored CVEs

- [CVE-2024-34069](https://www.cve.org/CVERecord?id=CVE-2024-34069) The underlying vulnerability of this CVE is only relevant to a small set of use cases and scenarios such as when hosting Airflow publicly on the internet, and is considered low risk for Astro and Software users. Because the resolution would require significant changes to Airflow and its dependencies, this CVE has not been addressed at this time.

## Astro Runtime 9.10.2

- Release date: April 18, 2024
- Airflow version: 2.7.3

### Additional improvements

- Upgraded [Gunicorn](https://gunicorn.org/) to `22.0.0`.

## Astro Runtime 9.10.1

- Release date: April 16, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Providers now load when Gunicorn workers start ([#38795](https://github.com/apache/airflow/pull/38795))
- You can now customize the size of objects stored in the rendered `taskinstance` field ([#38094](https://github.com/apache/airflow/pull/38094))
- Fixed an issue where the dataset listener could cause an error by closing the session prematurely ([#36247](https://github.com/apache/airflow/pull/36247))
- Fixed an issue where core triggers were not exiting a `while` loop as expected ([#38389](https://github.com/apache/airflow/pull/38389))
- Updated the behavior of the asynchronous implementation of `ExternalTaskSensor` to work more similarly to the synchronous implementation([#36916](https://github.com/apache/airflow/pull/36916))

### Additional Improvements

- Updated the version of `sqlparse` to `0.5.0`.

### Bug fixes

- Fixed a bug where the **Cluster Activity** tab was missing from the Airflow UI.

### Security fixes

- [CVE-2024-4340](https://www.cve.org/CVERecord?id=CVE-2024-4340)

#### Ignored CVEs
- [CVE-2024-25128](https://www.cve.org/CVERecord?id=CVE-2024-25128) This CVE applies to OpenID users only. Attackers can gain unauthorized access to the Airflow UI by impersonating any Airflow user. Note this impacts OpenID only, which is long deprecated, and should not be confused with the more common OpenID Connect (ODIC). This scenario does not apply to Astro Runtime users.

## Astro Runtime 9.10.0

- Release date: January 31, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Fix bug introduced by replacing spaces by + in run_id ([#36877](https://github.com/apache/airflow/pull/36877))

### Bug fixes

- Fixed an issue where some logging features would not work for dag runs with spaces in their dag run IDs.
- Astro Runtime now relies on logic `apache-airflow-providers-openlineage` to determine whether OpenLineage should be enabled or disabled in a given environment, which makes the behavior more consistent between different environments and implementations.
- Fixed an issue where `airflow tasks test <dag_id> <task_id>` always generated an error that stated it was unable to find a foreign key for the table `ab_user`.

## Astro Runtime 9.9.0

- Release date: January 24, 2024
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Stop deserializing pickle when enable_xcom_pickling is False ([#36255](https://github.com/apache/airflow/pull/36255))
- Check dag read permission before accessing dag code ([#36257](https://github.com/apache/airflow/pull/36257))

### Security fixes

- [CVE-2023-50944](https://www.cve.org/CVERecord?id=CVE-2023-50944)
- [CVE-2023-50943](https://www.cve.org/CVERecord?id=CVE-2023-50943)
- [CVE-2023-50944](https://www.cve.org/CVERecord?id=CVE-2023-50944)

## Astro Runtime 9.8.0

- Release date: January 10, 2024
- Airflow version: 2.7.3

### Additional improvements

- You can now set `ASTRO_CLOUDWATCH_TASK_LOGS_LOG_GROUP` and `ASTRO_CLOUDWATCH_TASK_LOGS_GROUP_STREAM` in a Deployment to change the names of the AWS Cloudwatch log groups and streams that Astro uses to organize log events. Create custom names for log streams and groups if you need to set targeted policies for these objects in Cloudwatch, or if you otherwise want to change how task logs are grouped. See [Export task logs to AWS Cloudwatch](export-cloudwatch).
- To improve scheduler performance, the default value for `AIRFLOW__SCHEDULER__MAX_TIS_PER_QUERY` is now `512`.

### Bug fixes

- In the Airflow UI for Astro Deployments, the **Audit Logs** page now shows the Astro user who performed a given action in the **Owner** column.

## Astro Runtime 9.7.0

- Release date: December 22, 2023
- Airflow version: 2.7.3

### Early access Airflow bug fixes

- Account for change in UTC offset when calculating next schedule ([#35887](https://github.com/apache/airflow/pull/35887))
- Fix for infinite recursion due to secrets_masker ([#35048](https://github.com/apache/airflow/pull/35048))
- Fix updating variables during variable imports ([#33932](https://github.com/apache/airflow/pull/33932))
- Allow 'airflow variables export' to print to stdout ([#33279](https://github.com/apache/airflow/pull/33279))
- Check that dag_ids passed in request are consistent ([#34366](https://github.com/apache/airflow/pull/34366))
- Make raw HTML descriptions configurable ([#35460](https://github.com/apache/airflow/pull/35460))
- Change Trigger UI to use HTTP POST in web UI ([#36026](https://github.com/apache/airflow/pull/36026))

### Additional improvements

- Upgraded `astronomer-providers` to 1.18.4. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1184-2023-12-07) for a complete list of changes.
- You can now customize the color of the Airflow UI navigation bar text by setting the `AIRFLOW__NAVBAR_TEXT_COLOR` environment variable.

### Bug fixes

- Fixed an issue where task logs on Astro Azure clusters were not encoded properly, resulting in authentication errors.

### Security fixes

- [CVE-2023-50783](https://www.cve.org/CVERecord?id=CVE-2023-50783)
- [CVE-2023-49920](https://www.cve.org/CVERecord?id=CVE-2023-49920)
- [CVE-2023-47265](https://www.cve.org/CVERecord?id=CVE-2023-47265)
- [CVE-2023-49920](https://www.cve.org/CVERecord?id=CVE-2023-49920)
- [CVE-2023-50783](https://www.cve.org/CVERecord?id=CVE-2023-50783)
- [CVE-2023-48291](https://www.cve.org/CVERecord?id=CVE-2023-48291)
- [CVE-2023-44487](https://www.cve.org/CVERecord?id=CVE-2023-44487)

## Astro Runtime 9.6.0

- Release date: November 30, 2023
- Airflow version: 2.7.3

### Bug fixes

- Upgraded `astronomer-providers` to 1.18.3. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1183-2023-11-29) for a complete list of changes.
- Fixed an issue where logging defaulted to `latin-1` encoding, causing a `UnicodeEncodeError`. The default encoding is now set to `utf-8`.
- Fixed S3 logging read issues to now use regional endpoint instead of the legacy global endpoint, resolving compatibility problems with 2.x AWS clusters in Astro.

### Security fixes

- [CVE-2023-47038](https://www.cve.org/CVERecord?id=CVE-2023-47038)

## Astro Runtime 9.5.0

- Release date: November 6, 2023
- Airflow version: 2.7.3

### Airflow 2.7.3

Astro Runtime 9.5.0 includes same-day support for Apache Airflow 2.7.3. Airflow 2.7.3 contains a number of bug fixes including:

- Fix Scheduler crash looping when dag run creation fails ([#35135](https://github.com/apache/airflow/pull/35135))
- Fix pre-mature evaluation of tasks in mapped task group ([#34337](https://github.com/apache/airflow/pull/34337))
- Add TriggerRule missing value in REST API ([#35194](https://github.com/apache/airflow/pull/35194))

To learn more, see the [Apache Airflow 2.7.3 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-7-3-2023-11-04).

### Additional improvements

- You can now customize the color of the Airflow UI navigation bar by setting the `AIRFLOW__WEBSERVER__NAVBAR_COLOR` environment variable.

### Security Fixes

- [CVE-2023-47037](https://www.cve.org/CVERecord?id=CVE-2023-47037)
- [CVE-2023-42781](https://www.cve.org/CVERecord?id=CVE-2023-42781)

## Astro Runtime 9.4.0

- Release date: October 23, 2023
- Airflow version: 2.7.2

### Additional improvements

- On Astro, you can now export Airflow task logs to [AWS Cloudwatch](https://aws.amazon.com/cloudwatch/). See [Export logs to AWS cloudwatch](export-cloudwatch).
- Upgraded `google-cloud-aiplatform` to 1.35.0.
- Upgraded [Shapely](https://shapely.readthedocs.io/en/stable/manual.html) to 2.0.2.
- Added a link for Astronomer Academy to the **Astronomer** menu in the Airflow UI.

### Bug fixes

- Fixed an issue where the Airflow UI showed an incorrect count for the total number of dags.
- Fixed an issue where exporting Airflow task logs from Astro to Datadog could cause workers to not shut down properly after new deploys or scale down events.

## Astro Runtime 9.3.0

- Release date: October 19, 2023
- Airflow version: 2.7.2

### Additional improvements

- Added support for `get_plugin_info` for class based listeners, such as OpenLineageListener and ClassBasedListener. Previously, support was limited to module based listeners ([#35022](https://github.com/apache/airflow/pull/35022))
- Fixed `/plugin` endpoint in the REST API ([#34858](https://github.com/apache/airflow/pull/34858))
- Upgraded many OSS providers to newer minor and patch versions.

## Astro Runtime 9.2.0

- Release date: October 12, 2023
- Airflow version: 2.7.2

### Airflow 2.7.2

Astro Runtime 9.2.0 includes same-day support for Apache Airflow 2.7.2. Airflow 2.7.2 contains a number of bug fixes including:

- Check if the lower of provided values are sensitives in config endpoint ([#34712](https://github.com/apache/airflow/pull/34712))
- Add missing audit logs for Flask actions add, edit and delete ([#34090](https://github.com/apache/airflow/pull/34090))
- Fix the required permissions to clear a TI from the UI ([#34123](https://github.com/apache/airflow/pull/34123))
- Fixed a bug where manually-triggered dag runs were causing the recalculation of when the scheduler would trigger the next dag run ([#34027](https://github.com/apache/airflow/pull/34027))

To learn more, see the [Apache Airflow 2.7.2 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-7-2-2023-10-12).

### Additional Improvements

- On Astro, you can now create custom tags when exporting Airflow task logs to Datadog, which allows you to easily filter, aggregate, and compare data. See [Export task logs to Datadog](export-datadog) for setup instructions.

### Security fixes

- [CVE-2023-42780](https://www.cve.org/CVERecord?id=CVE-2023-42780)
- [CVE-2023-45348](https://www.cve.org/CVERecord?id=CVE-2023-45348)
- [CVE-2023-42792](https://www.cve.org/CVERecord?id=CVE-2023-42792)
- [CVE-2023-42663](https://www.cve.org/CVERecord?id=CVE-2023-42663)

## Astro Runtime 9.1.0

- Release date: September 7, 2023
- Airflow version: 2.7.1

### Airflow 2.7.1

Astro Runtime 9.1.0 includes same-day support for Apache Airflow 2.7.1. Airflow 2.7.1 contains a number of bug fixes including:

- Treat dag-defined access_control as authoritative if defined ([#33632](https://github.com/apache/airflow/pull/33632))
- Add limit 1 if required first value from query result ([#33632](https://github.com/apache/airflow/pull/33632))
- Fix MappedTaskGroup tasks not respecting upstream dependency ([#33732](https://github.com/apache/airflow/pull/33732))

To learn more, see the [Apache Airflow 2.7.1 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-7-1-2023-09-07).

### Additional improvements

- You can now [export task logs to Datadog](export-datadog) from Azure and GCP clusters.
- Upgraded `openlineage-airflow` to 1.1.0. See the [OpenLineage release notes](https://openlineage.io/docs/releases/1_1_0/) for a complete list of changes.
- Upgraded `astro-sdk-python` to 1.7.0, which adds support for Excel files. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.

### Security fixes

- [CVE-2023-40712](https://www.cve.org/CVERecord?id=CVE-2023-40712)
- [CVE-2023-40611](https://www.cve.org/CVERecord?id=CVE-2023-40611)

## Astro Runtime 9.0.0

- Release date: August 18, 2023
- Airflow version: 2.7.0

### Airflow 2.7

Astro Runtime 9 is based on Airflow 2.7, which includes a number of new features and improvements. Most notably, Airflow 2.7 includes the following changes:

- In the Airflow UI, the **Trigger dag w/ config** button now appears only when a dag has configured [params](https://www.astronomer.io/docs/learn/airflow-params). Because some teams use this workflow without configuring dag params, this change has been feature flagged. To revert the change, set the following environment variable in your Dockerfile or as an Astro [environment variable](environment-variables):

    - **Key**: `AIRFLOW__WEBSERVER__SHOW_TRIGGER_FORM_IF_NO_PARAMS`
    - **Value**: `True`

- Setup and teardown tasks are a new type of task that you can use to prepare resources and configurations for specific tasks, ensuring that they always have resources even when you retry failed tasks. See [Use setup and teardown tasks in Airflow](https://www.astronomer.io/docs/learn/airflow-setup-teardown) to learn how to use them.
- You can now clear task groups or mark them as successful/failed from the Airflow UI **Grid View** just like individual tasks.
- You can set `operators.default_deferrable` in your Airflow config to always use the deferrable version of an operator if one is available, which means that you no longer have to update import statements in dags to replace traditional operators with deferrable ones.

To learn more, see the [Apache Airflow 2.7.0 release notes](https://airflow.apache.org/docs/apache-airflow/stable/release_notes.html#airflow-2-7-0-2023-08-14).

### New Python version distributions of Astro Runtime

Astro Runtime now supports multiple Python versions with separate distributions available for each major release. The supported Python versions for each release are listed [here](https://www.astronomer.io/docs/astro/runtime-image-architecture/#python-versioning). Using a Python distribution of Astro Runtime is the easiest way to use a specific Python version in Airflow.

Specify the Python version you want to use in your image tag, formatted as:

```text
quay.io/astronomer/astro-runtime:<runtime-version>-python-<python-version>
```

For example, to use Python 3.8 in Astro Runtime 9.0.0, you would replace the image tag in your Astro project Dockerfile with `quay.io/astronomer/astro-runtime:9.0.0-python-3.8`.

To keep using the same version of Python across multiple Astro Runtime upgrades, Astronomer recommends that you begin to use the Python distribution for your required Python version.

### Upgrade to Python 3.11

The base image for Astro Runtime now uses Python 3.11. If you want to use a different version of Python, replace your image with the appropriate Python distribution of Astro Runtime.

### Additional improvements

- Upgraded `astronomer-providers` to 1.17.3. See the [`astronomer-providers` changelog](https://github.com/astronomer/astronomer-providers/blob/main/CHANGELOG.rst#1173-2023-08-07) for a complete list of changes.
- Upgraded `astro-sdk-python` to 1.6.2. See the [Astro Python SDK changelog](https://astro-sdk-python.readthedocs.io/en/stable/CHANGELOG.html#id1) for a complete list of changes.
- Upgraded `openlineage-airflow` to 1.0.0. See the [OpenLineage blog](https://openlineage.io/blog/1.0-release/) for a summary of what's arrived in OpenLineage's first 1.x version.

### Bug fixes

- Fixed an issue where you could not set dag or task notes in the Airflow UI for environments running on Astro.

### Security fixes

- [CVE-2023-39441](https://www.cve.org/CVERecord?id=CVE-2023-39441)
- [CVE-2023-40273](https://www.cve.org/CVERecord?id=CVE-2023-40273)
- [CVE-2023-37379](https://www.cve.org/CVERecord?id=CVE-2023-37379)