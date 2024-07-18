---

copyright:
  years: 2018, 2022
lastupdated: "2022-12-22"

keywords: postgresql, databases, postgresql connection strings, postgresql connection ibm application

subcollection: databases-for-postgresql

---

{:external: .external target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:deprecated: .deprecated}
{{site.data.keyword.attribute-definition-list}}

## Connecting an {{site.data.keyword.cloud_notm}} application
{: #ibmcloud-app}

Applications running in {{site.data.keyword.cloud_notm}} can be bound to your {{site.data.keyword.databases-for-postgresql_full}} deployment.

## Connecting a Kubernetes Service application
{: #connect-kubernetes}

To connect a Cloud databases deployment to a Kubernetes Service application, follow these steps:

1. Bind your deployment to your cluster and store the connection strings in a secret.
2. Configure your application to use the connection strings.

Before connecting your Kubernetes Service application to a deployment, make sure that the deployment and cluster are both in the same region and resource group.

### Binding your deployment

1. **Public Endpoints**: Use the `cluster service bind` command with your cluster name, the resource group, and your deployment name.

```sh
ibmcloud ks cluster service bind <your_cluster_name> <resource_group> <your_database_deployment>
```

2. **Private Endpoints**: Create a service key for Kubernetes to use when binding to the database and then bind the database to the Kubernetes cluster through the private endpoint with the `cluster service bind` command.

### Configuring in your Kubernetes app

1. When you bind your application to Kubernetes Service, it creates an environment variable from the cluster's secrets.
2. Load and parse the JSON object into your application to retrieve the information your application's driver needs to make a connection to the database.

For more information, see the [Kubernetes Service docs](https://cloud.ibm.com/docs/containers?topic=containers-service-binding#reference_secret).
