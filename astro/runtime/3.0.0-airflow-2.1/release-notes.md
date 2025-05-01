### Astro Runtime 3.0.4

- Release date: October 26, 2021
- Airflow version: 2.1.1

#### Bug fixes

- Fixed an issue where worker pods were stuck in a terminating state when scaling down (backported from Runtime 4.0.1)

### Astro Runtime 3.0.3

- Release date: September 22, 2021
- Airflow version: 2.1.1

#### Bug fixes

- Fixed an issue where requests to Airflow's REST API with a temporary authentication token failed
- Fixed an issue introduced in Runtime 3.0.2 where `astro dev` commands in the Astro CLI did not execute correctly

### Astro Runtime 3.0.2

- Release date: September 17, 2021
- Airflow version: 2.1.1

#### Bug fixes

- Fixed a series of issues that prevented task logs from appearing in the Airflow UI by implementing a custom task logging handler that does not interfere with AWS credentials or connections configured by users

### Astro Runtime 3.0.1

- Release date: September 1, 2021
- Airflow version: 2.1.1

#### Additional improvements

- Upgraded the default Python version to `3.9.6`
- Added a link to Astro documentation in the Airflow UI

#### Bug fixes

- Removed nonfunctional security and user profile elements from the Airflow UI
- The Airflow UI now shows the correct version of Astro Runtime in the footer

### Astro Runtime 3.0.0

- Release date: August 12, 2021
- Airflow version: 2.1.1

#### Additional improvements

- The webserver is now the only Airflow component with access to logs, which reduces the risk of exposing sensitive information in logs ([commit](https://github.com/apache/airflow/pull/16754))
- Added support for Python 3.9 ([commit](https://github.com/apache/airflow/pull/15515))
- `token` keys in connections are now marked as masked by default ([commit](https://github.com/apache/airflow/pull/16474))

#### Bug fixes

- Fixed module vulnerabilities exposed by `yarn audit` ([commit](https://github.com/apache/airflow/pull/16440))
- Fixed an issue where tasks would fail when running with `run_as_user` ([commit](https://github.com/astronomer/airflow/commit/075622cbe))
- Fixed an issue where tasks would fail when running with `CeleryKubernetesExecutor` ([commit](https://github.com/astronomer/airflow/commit/90aaf3d48))