Hybrid private connection


To set up a private connection between an Astro VPC and an AWS VPC, you can create a VPC peering connection. VPC peering ensures private and secure connectivity, reduces network transit costs, and simplifies network layouts.

To create a VPC peering connection between an Astro VPC and an AWS VPC, you must create a temporary assumable role. The Astro AWS account will assume this role to initiate a VPC peering connection.

1. Open the AWS console of the AWS account with the external VPC and copy the following:

    - AWS account ID
    - AWS region
    - VPC ID of the external VPC
    - CIDR block of the external VPC

2. Create a temporary role using the [role creation stack template](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://cre-addon-infrastructure-us-east-1.s3.amazonaws.com/astro-peering-role.yaml). In the **Quick create stack** template that opens, complete the following fields:

    - **Stack name**: Enter a meaningful name for your stack.
    - **Peer Owner IDs**: Enter your cluster's AWS account ID. To retrieve your cluster's AWS account ID on Astro Hosted, contact [Astronomer support](https://cloud.astronomer.io/open-support-request). To retrieve your cluster's AWS account ID on Astro Hybrid, in the Astro UI's **Organization** section, click **Clusters**. Open your cluster and copy its **Account ID**.

3. After the stack is created, go to the **Outputs** tab and copy the value from the **PeerRole ARN** field.

4. In the **Organization** section of the Astro UI, click **Clusters**, select your cluster, and copy the **ID** of the cluster.

5. Contact [Astronomer support](https://cloud.astronomer.io/open-support-request) and provide the following details:

    - AWS region of the external VPC from Step 1
    - VPC ID of the external VPC from Step 1
    - AWS account ID of the external VPC from Step 1
    - CIDR block of the external VPC from Step 1
    - **PeerRole ARN** from Step 3
    - Astro cluster **ID** from Step 4

    Astronomer support will initiate a peering request and create the routing table entries in the Astro VPC.

6. Wait for Astronomer support to send you the Astro VPC CIDR and VPC peering ID. Then, the owner of the external VPC needs to [add a route](https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html#AddRemoveRoutes) in the external VPC, using the Astro VPC CIDR as the **Destination** and the VPC peering ID as the **Target**.

7. (Optional) Delete the stack that you created. This will delete the temporary assumable role.
