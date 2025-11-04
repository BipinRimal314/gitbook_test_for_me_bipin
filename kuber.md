# Kuber

This topic describes how to add and configure P0’s Kubernetes integration so users can use P0 to grant access to a Kubernetes cluster.

## Prerequisites

Ensure you have the following before continuing:

* Access to an existing Amazon Web Services (AWS), Azure, or Google Cloud service with a [Kubernetes cluster](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).

{% hint style="info" %}
You must have the `cluster-admin` role in the Kubernetes cluster.

* The example in this topic demonstrates the process using Google Cloud. The processes for AWS and Azure are similar.
{% endhint %}

* A command-line application such as:
  * Standard local terminal application that supports Secure Shell (SSH) (e.g., Terminal, Command, PowerShell, or Bash)
  * Cloud service-specific command-line (CLI) shell ([AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html), [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/), or [Google Cloud](https://cloud.google.com/sdk/docs/install))
* [kubectl](https://kubernetes.io/docs/tasks/tools/) command-line tool
* [jq](https://jqlang.github.io/jq/) JSON processor

## Add the Kubernetes Cluster Integration

To add the Kubernetes Cluster integration to the P0 application:

{% hint style="info" %}
If you have multiple clusters, you can repeat these steps to integrate each.
{% endhint %}

{% stepper %}
{% step %}
Open [p0.app](https://p0.app/) in your browser and log in.
{% endstep %}

{% step %}
Select **Integrations**, navigate to the **Resources** section, and click **Kubernetes**.
{% endstep %}

{% step %}
Click **IAM management**.
{% endstep %}

{% step %}
On the **IAM management** screen, click **+ Add cluster**.
{% endstep %}

{% step %}
On the **IAM management** screen, populate the following fields to add the Kubernetes cluster to P0.

{% hint style="info" %}
The following screenshots show where to get the values in the Google Cloud console.
{% endhint %}

*   **Cluster identifier:** ID of the cluster. Use the ID in the **Name** field under **Cluster basics**:

    <figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcmrbx3e_4gDBP4C1X-irTmfrJ4Upcugzlpv8B2amuz17jY6StKl1dpMx1msdk4_deNEQ8c2apjaTMvOsOEYs5mw_sR9x6Uz93HDGtcCtf9lC4UAZ5rxd-3bdXUv2XlkGpEIVugAQ?key=n0AxVNNmPNqqL-6_71dvb4jT" alt="" width="375"><figcaption></figcaption></figure>
*   **Cluster endpoint:** IP address of the cluster in the form of https://

    :\[port]. Navigate to **Control Plane Networking** and use the **Public endpoint**:

    <figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXec_9SbPxRHcw47wpLORGZRzFUmoorCKcXJ8hHxV8bO7DcBJiXhiy4BTiCF7-yN4xSejKxA-iANCGcrR3VhLCDHvW8iZoVIn5Hk1Z7AMTiEdj6LIGHyNFEG3yYI4YFd97E_-IorhA?key=n0AxVNNmPNqqL-6_71dvb4jT" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
- The port is optional.
- Ensure you use https:// and not http://, since HTTP is not supported.
{% endhint %}

*   **Cluster certification authority:** Base64-encoded certificate data that verifies the API server’s authenticity. Click **Show cluster certificate** to display a popup where you can copy the certificate:

    <figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXet6FAUjQyLuak3DDswLR5L6ADovjngdvVBDF74cOxiXfNccl8ScuTSavJAwR-0_RF1n94xqu6kCu9-zxEyX_2YaBzMPckwYsxViWujcc6usfr6MDq-dB9oTcSVXNVF-xX4_w40xA?key=n0AxVNNmPNqqL-6_71dvb4jT" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="warning" %}
Ensure you copy the certificate including the `-----BEGIN CERTIFICATION-----` and `-----END CERTIFICATE-----` statements and paste it into the **Cluster certification authority** in P0.
{% endhint %}

* **Network Connectivity:**
  * **Public:** Select this if the cluster's API is accessible directly over the Internet.
  * **P0 Proxy:** Select this if you are routing through P0’s reverse HTTPS proxy (used for private network setups).
* **Hosting:** Select your cloud provider (e.g., Google Cloud) and enter the cluster details (e.g., GCP Project ID, GKE cluster name, and Location for Google Cloud).
{% endstep %}

{% step %}
At the bottom of the **IAM management** screen, click **Next**.
{% endstep %}

{% step %}
Open Google Cloud Shell (recommended) or a local shell, and run the following command to log into Google Cloud:

{% code title="Login to Google Cloud" %}
```sh
gcloud auth login
```
{% endcode %}

{% hint style="info" %}
This displays Google’s login browser screen where you enter your login details.
{% endhint %}
{% endstep %}

{% step %}
Return to P0’s **IAM management** screen and copy the kubectl commands provided.
{% endstep %}

{% step %}
Return to your shell, and paste the commands you just copied to enable P0’s admission controller. The output should look similar to the following:

{% code title="kubectl output example" %}
```sh
namespace/p0-security created
serviceaccount/p0-service-account created
secret/p0-service-account-secret created
clusterrole.rbac.authorization.k8s.io/p0-service-role created
clusterrolebinding.rbac.authorization.k8s.io/p0-service-role-binding created
deployment.apps/p0-admission-controller created
service/p0-admission-controller created
validatingwebhookconfiguration.admissionregistration.k8s.io/p0-admission-controller created
```
{% endcode %}

{% hint style="info" %}
If you chose the Network Connectivity P0 Proxy option, an additional deployment called _braekhus_ is created, which acts as a proxy between P0 and the Kubernetes control plane. For additional information, see the [braekhus GitHub repo](https://github.com/p0-security/braekhus).

For additional kubectl information, see [Install kubectl and configure cluster access](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl).
{% endhint %}
{% endstep %}

{% step %}
Return to the P0 **IAM management** screen, click **Next**, and copy the cluster token.
{% endstep %}

{% step %}
In your shell, paste the command copied in the previous step to generate a token.
{% endstep %}

{% step %}
Copy the resulting token from the shell, return to the P0 **IAM management** screen, and paste it into the **Cluster token** input field.
{% endstep %}

{% step %}
Review the rest of the configuration and click **Finish**.

P0 installs the integration and shows the cluster’s **State** as `Installed` once complete.
{% endstep %}

{% step %}
To ensure your integration works see [Requesting Access](broken-reference).

{% hint style="success" %}
Congratulations, you have successfully integrated a Kubernetes cluster with P0 and can make access requests to it via P0’s Slack bot.
{% endhint %}
{% endstep %}
{% endstepper %}
