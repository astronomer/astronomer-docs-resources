## Hybrid scheduler resources

On Astro Hybrid, PgBouncer is highly available by default for all Deployments. Schedulers are highly available if a Deployment uses two or more schedulers.

Every Deployment has two PgBouncer Pods assigned to two different nodes to prevent zombie tasks. If you configure your Deployment with two schedulers, each scheduler Pod is assigned to a separate node to ensure availability. To limit cost, a Deployment that uses three or four schedulers can assign all scheduler Pods across two nodes.


## Example template file

The following is an example Deployment file that includes possible key-value pairs for Astro Hybrid:

```yaml
deployment:
    configuration:
        name: default
        description: ""
        runtime_version: 11.3.0
        dag_deploy_enabled: false
        ci_cd_enforcement: false
        is_high_availability: false
        is_development_mode: false
        executor: CELERY
        scheduler_au: 5
        scheduler_count: 1
        cluster_name: Sandbox
        workspace_name: Demo Workspace
        deployment_type: HYBRID
        cloud_provider: AWS
        region: us-east-1
        workload_identity: ""
    worker_queues:
        - name: default
          max_worker_count: 10
          min_worker_count: 0
          worker_concurrency: 16
          worker_type: m5.xlarge
    metadata:
        deployment_id: clskxpb35000008l69kzp5psq
        workspace_id: clskytztd000008lad0i5c993
        cluster_id: clskyu7fk000108lagyc10fya
        release_name: clskyy4h8000208jz60olha0w-release
        airflow_version: 2.9.1
        current_tag: deploy-2024-05-07T14-15-25
        status: HEALTHY
        created_at: 2024-02-23T04:59:16.834Z
        updated_at: 2024-05-07T14:17:13.01Z
        deployment_url: cloud.astronomer.io/clskytztd000008lad0i5c993/deployments/clskxpb35000008l69kzp5psq/overview
        webserver_url: testing.astronomer.run/
        airflow_api_url: astronomer.astronomer.run/du1o4618/api/v1
    alert_emails:
        - clskz1jo1000408jz4w8wan2q@astronomer.io
```