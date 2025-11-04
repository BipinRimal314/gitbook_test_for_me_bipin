# README

<img src=".gitbook/assets/favicon (2).ico" alt="PostgreSQL" data-size="line"> **PostgreSQL**

This topic explains how to configure access control for P0’s fully managed PostgreSQL database service on Google Cloud Platform (GCP). You can use this integration to:

* Configure secure access to your PostgreSQL database.
* Enable authorized connections to the Cloud SQL instance.
* Perform other database access management tasks.

### Prerequisites

* Existing Google Cloud (GCP) integration
* Permissions to create roles and add IAM bindings:
  * `iam.roleAdmin`
  * `iam.securityAdmin`
* Permissions to connect to the Cloud SQL instance, as an authorized user:
  * Grant access (`GRANT`) to other users
  * Create functions (`CREATE FUNCTION`) within the database
* Access to [Google Cloud Shell](https://shell.cloud.google.com/?hl=en_US\&fromcloudshell=true\&show=terminal) and/or [gcloud CLI](https://cloud.google.com/sdk/docs/install) installed and configured



Where

{% hint style="info" %}
This example uses Google Cloud Shell.
{% endhint %}

### Set up PostgreSQL Integration

{% stepper %}
{% step %}
### Start on P0.app: open the PostgreSQL integration

1. Go to [P0.app](https://p0.app/) in your browser. Select **Integrations**, then under the **Resources** section, click **PostgreSQL**.
2. From the list of **Available components**, click **Access management**.
3. Click **+ Add database**.

<figure><img src=".gitbook/assets/AD_4nXfHe6zVFf8uwXY2fxXgxLKi3Uw2HoR0UsuPHdX60Qr_gyUeGrkiq1obJcwyOgm i6sb6bFsoYZ6cE6HnDOc6u1vggd5fXYBBJhBmY4gc1Y6rgw158gMkf5CrB9RL4tdwZpk3wwYww (3)" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Provide PostgreSQL instance details

Populate the details of your PostgreSQL instance and click **Next**:

* **Database identifier**: Unique label to identify the database (e.g. `p0-production-db`)
* **Installation type**: Platform hosting the PostgreSQL database (e.g. **Google CloudSQL**)
  * **GCP project ID**: Google Cloud project ID (e.g. `p0-demo`)
  * **GCP region**: Region where the CloudSQL instance is located (e.g. `us-central1`)
  * **CloudSQL instance ID**: ID of the CloudSQL instance which must have public IP access enabled (e.g. `my-cloudsql-instance-001`)
* **Database name**: Name of the database to manage (e.g. `app_main_db`)
{% endstep %}

{% step %}
### Prepare to configure access management

Ensure P0 can manage user access to PostgreSQL roles. On the resulting **Access management** screen, Step 1 applies to Google Cloud and Steps 2 and 3 apply to Postgres.

Start by configuring Google Cloud, and copy the commands from **Step 1**.

{% hint style="info" %}
Keep the **Access management** browser tab open. You'll need to copy information from this page in subsequent steps.
{% endhint %}
{% endstep %}

{% step %}
### Run the Google Cloud commands

1. Open the [Google Cloud Shell](https://shell.cloud.google.com/?hl=en_US\&fromcloudshell=true\&show=terminal) in a new browser tab, and paste and run the copied commands.

{% hint style="info" %}
Keep this browser tab open as well. The next steps require you to toggle back and forth between the P0.app's **Access management** page and the Google Cloud Shell browser tabs.
{% endhint %}
{% endstep %}

{% step %}
### Connect to the Cloud SQL PostgreSQL instance

From Google Cloud Shell, connect to your Cloud SQL PostgreSQL instance using the psql command. Replace `REGION` with your actual region (e.g. `us-central1`, `us-east1`, etc.).
{% endstep %}

{% step %}
### Apply the SQL commands from P0

1. Switch back to the **Access management** browser tab and copy the commands from **Step 2** and **Step 3**.
2. Return to Google Cloud Shell and run the copied SQL commands.
{% endstep %}

{% step %}
### Finalize configuration in P0

1. After running the commands, switch back to the **Access management** browser tab and click **Next**.
2. Click **Finish** to finalize your configuration.
{% endstep %}

{% step %}
### Done

You can manage your connections (for example, [request access](broken-reference) to this PostgreSQL instance through Slack) on the PostgreSQL **Integrations** page and add new configurations as needed.

{% hint style="success" %}
Congratulations! You've now set up PostgreSQL for P0.
{% endhint %}
{% endstep %}
{% endstepper %}
