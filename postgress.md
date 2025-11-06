---
description: Connecting P0 Security to Google Cloud SQL and Amazon RDS for PostgreSQL
---

# <img src=".gitbook/assets/favicon (3).ico" alt="PostgreSQL" data-size="line"> **PostgreSQL**

The PostgreSQL integration enables P0 to manage secure, granular access control for fully managed PostgreSQL databases on **Google Cloud SQL** and **Amazon RDS for PostgreSQL**. With this integration, security and platform engineering teams can automate access provisioning and de-provisioning, enforce least privilege, and audit all database access events for compliance.

### How It Works

P0 ensures there is a dedicated database user for every identity that accesses the database by attaching users to the Cloud SQL instance using [IAM authentication](https://cloud.google.com/sql/docs/postgres/add-manage-iam-users). Additionally, P0 dynamically provisions the requested access for these users inside the PostgreSQL database by granting the requested role, or generating a role on-the-fly for custom SQL query access. Events are captured with native PostgreSQL session and query logging, tied to the original user identity.

To begin configuring the integration, review the detailed setup instructions for connecting your PostgreSQL database on [Google Cloud SQL](broken-reference) or [Amazon RDS for PostgreSQL](broken-reference).
