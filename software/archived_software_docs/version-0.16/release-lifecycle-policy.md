---
title: Astronomer Release and Lifecycle Policy
sidebar_label: Release and Lifecycle Policy
id: release-lifecycle-policy
description: Astronomer's release and lifecycle policy for Astronomer Software.
---

## Overview

Astronomer supports a variety of policies that drives the naming, release cadence, and maintenance commitments associated with all published software.

This document offers guidelines on the version lifecycle of Astronomer Software. It includes a description of:

- How Astronomer is versioned.
- Which versions of Astronomer Software are currently available.
- Release channels and the maintenance schedule for all versions.

For information on the latest Astronomer Software releases, see [release notes](release-notes.md). For the release and maintenance policy for Astronomer Certified, see the Certified [Versioning and Maintenance Policy](ac-support-policy.md).

For information on compatibility between all versioned software, see [Software Version Compatibility Reference](version-compatibility-reference.md).

## Release Channels

To meet the unique needs of different operating environments, we offer all Astronomer customers two release channels:

- **Stable:** Includes the latest Astronomer and Airflow features
- **Long-term Support (LTS):** Includes long-term testing, stability, and maintenance for a core set of features

For customers looking to access Astronomer's newest features on an incremental basis, we recommend following the stable release channel and upgrading to new versions as soon as they are made generally available. Stable releases are issued roughly once per month for Astronomer Software and the Astronomer CLI.

For customers looking for less frequent upgrades and functional changes, we recommend following the LTS release channel. Release channels are not binding, so you are free to upgrade to any available version of Astronomer Software at any time.

> **Note:** Release channels apply to Astronomer Software and Astronomer Certified versions. We do not currently support a long-term release channel for the Astronomer CLI.

## Astronomer Software Versioning

Astronomer follows [Semantic Versioning](https://semver.org/) for all published software. This means that we use Major, Minor, and Patch releases across our product in the format of `major.minor.patch`.

- **Major** versions are released for significant feature additions, including backward-incompatible changes to an API or DAG specification.
- **Minor** versions are released for functional changes, including backward-compatible changes to an API or DAG specification.
- **Patch** versions are released for bug and security fixes that resolve incorrect behavior.

It is considered safe to upgrade to minor and patch versions within a major version. Upgrade guidance for major and LTS versions is provided with each release.

## Version Maintenance Policy

The maintenance period for an Astronomer Software version depends on its release channel:

| Release Channel | Frequency of Releases | Maintenance Duration |
| --------------- | --------------------- | -------------------- |
| Stable          | Monthly               | 6 Months             |
| LTS             | Yearly                | 12 Months            |

For each `major.minor` pair, only the latest patch is supported at any given time.

For example, if Astronomer Software v0.26 were a stable version first released in October 2021:

- Support for Astronomer Software v0.26 would end 6 months later in April 2022.
- If a patch version for v0.26 came out in December 2021 (e.g. `v0.26.4`), it would not affect the maintenance duration. Maintenance for v0.26 would still end in April 2022.
- If a major bug was identified in v0.26, a fix would be backported by the Astronomer team and released as a patch to v0.26 as long as it remained the latest stable release.
- If Astronomer Software v0.27 came out as a new stable release, bug fixes would no longer be backported to Astronomer v0.26 and customers would be encouraged to upgrade.
- If a major security issue was identified in v0.26, a fix would be backported and released as a patch at any time during its 6 month maintenance period. If v0.27 came out and succeeded v0.26 as the latest stable version of Astronomer Software, a security fix would still be backported to v0.26.

If you contact [Astronomer Support](https://support.astronomer.io) about an issue you are experiencing while running an unmaintained version, our team will invite you to upgrade as an initial mitigation step.

### End of Maintenance Date

Maintenance is discontinued the last day of the month for a given version. For example, if a version of Astronomer Software were supported between January - June of a given year, that version would be maintained by Astronomer until the last day of June.

## Backport Policy for Bug and Security Fixes

If a major stability bug is identified by our team, a fix will be backported to all LTS versions and only the latest stable version. For users on a stable version that is not latest, our team will recommend that you upgrade. Major issues in this category may result in significant delays in task scheduling as well as potential data loss.

If a major security issue is identified, a fix will be backported and made available as a new patch version for _all_ supported stable and LTS releases. Major issues in this category are classified by a combination of impact and exploitability.

In rare instances, the Astronomer team may make an exception and backport a bug or security fix to a release that is beyond the commitment stated above. To submit a request for consideration, please reach out to your customer success manager.

## Software Lifecycle Schedule

The following table contains the exact lifecycle for each published version of Astronomer Software. These timelines are based on the LTS and stable release channel maintenance policies.

| Software Version | Release Date     | End of Maintenance Date |
| ------------------ | ---------------- | ----------------------- |
| 0.16 (LTS)         | June 29, 2020    | June 2021               |
| 0.23 (LTS)         | January 20, 2021 | January 2022            |
| 0.25 (LTS)         | May 11, 2021     | December 2022*          |
| 0.26               | Nov 23, 2021     | May 2022                |
| 0.27               | Dec 21, 2021     | June 2022               |

> *Given the wide usage of Astronomer Software v0.25, Astronomer has extended the maintenance period for this version through December 2022.
