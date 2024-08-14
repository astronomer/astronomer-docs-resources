---
title: 'Manage users and roles on Astronomer Software'
sidebar_label: 'Manage users and roles'
id: manage-platform-users
description: Add and customize user permissions on Astronomer Software.
---

Astronomer Software allows you to adjust permissions for each user role and define how new users join your organization. 

Use this guide to learn about customizing user signups and user roles, as well as how to use Astronomer Software system-level permissions. For a list of the default permissions for each role, see [User roles and permissions](#role-permission-reference).

## Add users to Astronomer

When Astronomer Software is first deployed, the first user to log in is granted "System Admin" permissions by default. From there, a user is created on Astronomer Software by any of the following:

- Invitation to a Workspace by a Workspace Admin
- Invitation to Astronomer by a System Admin
- Signing up via the Software UI without an invitation (requires "Public Signups")
- Imported to Astronomer through an [IdP group](import-idp-groups.md)

On Astronomer, administrators have the option to either open the platform to public signups or limit account creation to users invited by others.

> **Note:** New users appear under a System Admin's **Users** tab only after the new user has successfully logged in for the first time.

> **Note:** You can bypass the email verification process for new users through a Houston API mutation. For the format of this mutation, see [Sample Mutations](houston-api.md#sample-mutations).

### Enable public signups

As noted above, public signups allow any user with access to the platform URL (the Software UI) to create an account. If public signups are disabled, users that try to access Astronomer without an invitation from another user will be met with an error.

In cases where SMTP credentials are difficult to acquire, enabling this flag might facilitate initial setup, as disabling public signups requires that a user accept an email invitation. Public signups are a configuration available in Astronomer's Houston API and can be enabled in the `config.yaml` file of your Helm chart.

To enable public signups, add the following yaml snippet to your `config.yaml` file:

```
astronomer:
  houston:
    config:
      publicSignups: true
      emailConfirmation: false # If you wish to also disable other SMTP-dependent features
```

An example `config.yaml` file would look like:

```
global:
  baseDomain: mybasedomain
  tlsSecret: astronomer-tls
nginx:
  loadBalancerIP: 0.0.0.0
  preserveSourceIP: true

astronomer:
  houston:
    config:
      publicSignups: true
      emailConfirmation: false

```

Then, push the configuration change to your platform as described in [Apply a config change](apply-platform-config.md).

## System permissions on Software

The Astronomer Software System Admin role provides cluster-wide permissions that supersede Workspace-level access and allows a user to monitor and take action across Workspaces, Deployments, and users within a single cluster.

On Astronomer, System Admins specifically can:

- List and search all users.
- List and search all Deployments.
- Access the Airflow UI for all Deployments.
- Delete a user.
- Delete a Deployment.
- Access Grafana and Kibana for cluster-level monitoring.
- Add other System Admins.

By default, the first user to log into an Astronomer Software installation is granted the System Admin permission set.

In addition to the commonly used System Admin role, the Astronomer platform also supports both a System Editor and System Viewer permission set.

No user is assigned the System Editor or Viewer Roles by default, but they can be added by System Admins via our API. Once assigned, System Viewers, for example, can access both Grafana and Kibana but don't have permission to delete a Workspace they're not a part of.

You can customize all three Astronomer Software permission sets to meet your specific requirements. For more information about the default configurations attached to the System Admin, Editor and Viewer Roles, see the [Houston API source code](https://github.com/astronomer/docs/tree/main/software_configs/0.30/default.yaml).


### Assign users System Admin roles

System Admins can be added to Astronomer Software using the **System Admin** tab of the Software UI.

Keep in mind that:

- Only existing System Admins can grant the System Admin role to another user
- The user must have a verified email address and already exist in the system

> **Note:** If you'd like to assign a user a different System-Level Role (either `SYSTEM_VIEWER` or `SYSTEM_EDITOR`), you'll have to do so via an API call from your platform's GraphQL playground. For guidelines, refer to our ["Houston API" doc](houston-api.md).

#### Verify System Admin access

To verify a user was successfully granted the SysAdmin role, ensure they can do the following:

- Navigate to `grafana.BASEDOMAIN`
- Navigate to `kibana.BASEDOMAIN`
- Access the 'System Admin' tab from the top left menu of the Software UI

## User roles on Astronomer

Administrators can customize permissions across teams. On Astronomer Software, users can be assigned roles at two levels:

- Workspace Level (Viewer, Editor, Admin)
- System Level (Viewer, Editor, Admin)

Workspace roles apply to all Airflow Deployments within a single Workspace. System Roles apply to *all* Workspaces across a single cluster. For more information about the three Workspace-level roles on Astronomer Software (Viewer, Editor and Admin), see [Manage user permissions on an Astronomer Workspace](workspace-permissions.md).

## Customize role permissions

Permissions are defined on Astronomer as `scope.entity.action`, where:

- `scope`: The layer of our application to which the permission applies
- `entity`: The object or role being operated on
- `action`: The verb describing the operation being performed on the `entity`

For example, the `deployment.serviceAccounts.create` permission translates to the ability for a user to create a Deployment-level service account in any Deployment to which they belong. To view the available platform permissions and default role configurations, see [Reference: System permissions](role-permission-reference.md).

A permission for a given `scope` only applies to the parts of the scope where a user has been invited. For example, a user with a role including the `workspace.serviceAccounts.get` permission can view service accounts only in the Workspaces they belong to.

For a complete list of Astronomer Software roles and default permissions, see [User roles and permissions](role-permission-reference.md).

### Role permission inheritance

In addition to their own permissions, roles inherit permissions from other roles. 

There are several chains of inheritance in the Software RBAC system. In the following list, `>` represents "inherits from":

- System Admin > System Editor > System Viewer > User
- Deployment Admin > Deployment Editor > Deployment Viewer > User 
- Workspace Admin > Workspace Editor > Workspace Viewer > User

### Step 1: Identify a permission change

<!--- Version-specific -->

Review the default roles and permissions in the [default Houston API configuration](https://github.com/astronomer/docs/tree/main/software_configs/0.30/default.yaml) and determine the following:

- What role you want to configure. For example, `DEPLOYMENT_EDITOR`.
- What permission(s) you want to add or remove from the role, For example, `deployment.images.push`.

For example, you might want to block a `DEPLOYMENT_EDITOR` (and therefore `WORKSPACE_EDITOR`) from deploying code to all Airflow Deployments within a Workspace and instead limit that action to users assigned the `DEPLOYMENT_ADMIN` role.

### Step 2: Modify your config.yaml file

Apply the role and permission changes to your organization's `config.yaml` file. For example:

```yaml
astronomer:
  houston:
    config:
      roles:
        DEPLOYMENT_EDITOR:
          permissions:
            deployment.images.push: false
```

In the same way you can remove permissions from a particular role by setting a permission to `:false`, you can add permissions to a role at any time by setting a permission to `:true`.

For example, if you want to allow any `DEPLOYMENT_VIEWER` (and therefore `WORKSPACE_VIEWER`) to push code directly to any Airflow Deployment within a Workspace, you'd specify the following:

```yaml
astronomer:
  houston:
    config:
      roles:
        DEPLOYMENT_VIEWER:
          permissions:
            deployment.images.push: true
```

Push the configuration change to your platform. See [Apply a config change](apply-platform-config.md).

### Example customization: Limit Workspace creation

Unless otherwise configured, a user who creates a Workspace on Astronomer Software is automatically granted the `WORKSPACE_ADMIN` role and can create an unlimited number of Airflow Deployments within that Workspace. For teams looking to more strictly control resources, Astronomer Software supports limiting the Workspace creation function through the `USER` role.

Astronomer Software includes a `USER` role that is synthetically bound to _all_ users within a single cluster. By default, this role includes the `system.workspace.create` permission.

If you're a System Admin who wants to limit Workspace creation, you can:

- Set the `system.workspace.create` permission for the `USER` role to `false`
- Attach the `system.workspace.create` permission to a separate role of your choice

You might want limit this permission to the `SYSTEM_ADMIN` role on the platform, because System Admins can be responsible for managing cluster-level resources and costs. To reassign this permission to System Admins, your `config.yaml` would appear similar to the following example: 

```yaml
astronomer:
  houston:
    config:
      roles:
        SYSTEM_ADMIN:
          permissions:
            system.workspace.create: true
        USER:
          permissions:
            system.workspace.create: false
```

## Role permission reference

This is where you'll find information about Astronomer Software default user role permissions. To modify these default permissions, see [Customize role permissions](manage-platform-users.md#customize-role-permissions).

## System roles

System roles apply to all Workspaces, users, and Deployments within a single Astronomer Software installation.

### System Viewer

The System Viewer has the following permissions by default:

- `system.airflow.get`: View the Airflow UI for any Deployment
- `system.deployment.variables.get`: View [environment variables](environment-variables.md) for any Deployment
- `system.deployments.get`: View any setting for any Deployment in the Software UI
- `system.invites.get`: View all pending user invites in the **System Admin** tab of the Software UI
- `system.invite.get`: View information for any pending user invite
- `system.monitoring.get`: Access to [Grafana](grafana-metrics.md) and [Kibana](kibana-logging.md) for system-level monitoring
- `system.serviceAccounts.get`: View [service accounts](ci-cd.md#step-1-create-a-service-account) for any Deployment or Workspace
- `system.updates.get`: View the newest platform release version number
- `system.users.get`: View information for any user on the platform, including their email address, the list of Workspaces that user has access to, and their user role
- `system.workspace.get`: View information for any Workspace

### System Editor

The System Editor has the same default permissions as the System Viewer, plus:

- `system.deployment.variables.update`: Modify [environment variables](environment-variables.md) for any Deployment
- `system.iam.update`: Modify [IAM](integrate-iam.md) roles for any Deployment
- `system.serviceAccounts.update`: Modify [service accounts](ci-cd.md#step-1-create-a-service-account) for any Workspace or Deployment
- `deployment.airflow.user`: Airflow [user permissions](https://airflow.apache.org/docs/apache-airflow/stable/security/access-control.html#user) for all Deployments
- `system.registryBaseImages.push`: Modify base layer Docker images for Airflow

### System Admin

The System Admin has the same default permissions as the System Viewer and System Editor for a given cluster, plus:

- `system.deployments.create`: Create a Deployment on any Workspace
- `system.deployments.update`: Modify any Deployment
- `system.deployments.delete`: Delete any Deployment
- `system.deployments.logs`: View logging and metrics for any Deployment
- `system.user.invite`: Invite a user
- `system.user.delete`: Delete any user
- `system.user.verifyEmail`: Bypass email verification for any user
- `system.workspace.delete`: Delete any Workspace
- `system.workspace.update`: Modify the name or description of any Workspace
- `system.airflow.admin`: Airflow admin permissions on any Deployment, including permission to configure:

    - Pools
    - Configuration
    - Users
    - Connections
    - Variables
    - XComs

## Workspace roles

Workspace roles apply to a single Workspace within a single Astronomer Software installation.

### Workspace Viewer

The Workspace Viewer has the following default permissions for a given Workspace:

- `workspace.config.get`: View the Workspace
- `system.deployments.get`: View all settings and configuration pages of any Deployment
- `workspace.serviceAccounts.get`: View any Deployment or Workspace-level [service account](ci-cd.md#step-1-create-a-service-account)
- `workspace.users.get`: View information for all users with access to the Workspace

### Workspace Editor

For a given Workspace, the Workspace Editor has the same default permissions as the Workspace Viewer, plus:

- `workspace.config.update`: Modify the Workspace, including Workspace Name, Description, and user access
- `workspace.deployments.create`: Create a Deployment in the Workspace
- `workspace.serviceAccounts.create`: Create a Workspace-level service account
- `workspace.serviceAccounts.update`: Modify a Workspace-level service account
- `workspace.serviceAccounts.delete`: Delete a Workspace-level service account

### Workspace Admin

For a given Workspace, the Workspace Editor has the same default permissions as the Workspace Viewer and Workspace Editor, plus:

- `workspace.invites.get`: View pending user invites for the Workspace
- `workspace.config.delete`: Delete the Workspace
- `workspace.iam.update`: Update [IAM](integrate-iam.md) for the Workspace

In addition, Workspace Admins have Deployment Editor permissions for all Deployments within the Workspace.

## Workspace roles

Workspace roles apply to a single Deployment within a single Astronomer Software installation.

### Deployment Viewer

For a given Deployment, a Deployment Viewer has the following permissions:

- `deployment.airflow.get`: View the Airflow UI
- `deployment.config.get`: View the Deployment's settings
- `deployment.logs.get`: View the Deployment's logs
- `deployment.images.pull`: Access the Deployment's running Docker image
- `deployment.metrics.get`: View the Deployment's **Metrics** tab in the Software UI
- `deployment.serviceAccounts.get`: View any [service account](ci-cd.md#step-1-create-a-service-account) for the Deployment
- `deployment.variables.get`: View the Deployment's [environment variables](environment-variables.md)
- `deployment.users.get`: View the list of users with access to the Deployment

A Deployment Viewer can't push code to a Deployment or modify Deployment configurations. These actions can be completed only by a Deployment Editor or a Deployment Admin.

### Deployment Editor

For a given Deployment, the Deployment Editor has the same default permissions as the Deployment Viewer, plus:

- `deployment.airflow.user`: Airflow [user permissions](https://airflow.apache.org/docs/apache-airflow/stable/security/access-control.html#user) for all Deployments, including modifying task runs and DAG runs
- `deployment.config.update`: Modify the Deployment's settings
- `deployment.images.push`: Push code to the Deployment using the Astro CLI
- `deployment.serviceAccounts.create`: Create a Deployment-level service account
- `deployment.serviceAccounts.update`: Modify a Deployment-level service account
- `deployment.serviceAccounts.delete`: Delete a Deployment-level service account
- `deployment.variables.update`: Update the Deployment's [environment variables](environment-variables.md)

A Deployment Editor cannot make changes to certain configurations in the Airflow UI, such as connections and variables. These actions can only be completed by a Deployment Admin.

### Deployment Admin

For a given Deployment, the Deployment Admin has the same default permissions as the Deployment Viewer and the Deployment Editor, plus:

- `deployment.airflow.admin`: Airflow [admin permissions](https://airflow.apache.org/docs/apache-airflow/stable/security/access-control.html#admin), including permission to configure:

    - Pools
    - Configuration
    - Users
    - Connections
    - Variables
    - XComs

- `deployment.config.delete`: Delete the Deployment
- `deployment.userRoles.update`: Update Deployment-level permissions for users within the Deployment