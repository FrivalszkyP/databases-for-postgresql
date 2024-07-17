---

copyright:
  years: 2018, 2022
lastupdated: "2022-12-22"

keywords: postgresql, databases, postgresql connection strings, postgresql connection ibm application

subcollection: databases-for-postgresql

---

# Connecting an {{site.data.keyword.cloud_notm}} Application

Applications running in {{site.data.keyword.cloud_notm}} can be bound to your {{site.data.keyword.databases-for-postgresql_full}} deployment.

## Connecting a Kubernetes Service Application

To connect a Cloud databases deployment to a Kubernetes Service application, follow these steps:

1. Bind your deployment to your cluster using the appropriate command for public or private endpoints.
2. Configure your application to use the connection strings.

The [Connecting a Kubernetes Service Tutorial](/docs/databases-for-postgresql?topic=cloud-databases-tutorial-k8s-app) provides a sample application that uses Node.js and demonstrates how to bind the sample application to a {{site.data.keyword.databases-for-postgresql}} deployment.

Before connecting your Kubernetes Service application to a deployment, ensure that the deployment and cluster are in the same region and resource group.

### Binding your Deployment

#### Public Endpoints

To bind your deployment using the default public service endpoint, run the following command:

```sh
ibmcloud ks cluster service bind <your_cluster_name> <resource_group> <your_database_deployment>
```

#### Private Endpoints

If you want to use a private endpoint, first create a service key for Kubernetes to use when binding to the database:

```sh
ibmcloud resource service-key-create <your-private-key> --instance-name <your_database_deployment> --service-endpoint private
```

Then, bind the database to the Kubernetes cluster through the private endpoint with the following command:

```sh
ibmcloud ks cluster service bind <your_cluster_name> <resource_group> <your_database_deployment> --key <your-private-key>
```

### Verifying the Binding

To verify that the Kubernetes secret was created in your cluster namespace, run the following command and look for the API key for accessing the instance of your deployment:

```sh
kubectl get secrets --namespace=default
```

For more information on binding services, see the [Kubernetes Service documentation](/docs/containers?topic=containers-service-binding#bind-services).

### Configuring in your Kubernetes App

When you bind your application to Kubernetes Service, it creates an environment variable from the cluster's secrets. Your deployment's connection information lives in `BINDING` as a JSON object. Load and parse the JSON object into your application to retrieve the information your application's driver needs to make a connection to the database.

The [Connection Strings](/docs/databases-for-postgresql?topic=databases-for-postgresql-connection-strings#connection-string-breakdown) page contains a reference of the JSON fields.

For more information, see the [Kubernetes Service docs](https://cloud.ibm.com/docs/containers?topic=containers-service-binding#reference_secret).
