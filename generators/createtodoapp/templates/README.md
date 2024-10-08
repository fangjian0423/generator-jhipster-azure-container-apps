
# React Web App with Java API and PostgreSQL

A blueprint for getting a React web app with a Java API and a PostgreSQL - Flexible Server on Azure. The blueprint includes sample application code (a ToDo web app) which can be removed and replaced with your own application code. Add your own source code and leverage the Infrastructure to get up and running quickly. This architecture is for running containerized apps or microservices on a serverless platform.

Let's jump in and get this up and running in Azure. When you are finished, you will have a fully functional web app deployed to the cloud. In later steps, you'll see how to setup a pipeline and run the application.

!["Screenshot of deployed ToDo app"](assets/web.png)

<sup>Screenshot of the deployed ToDo app</sup>

### Prerequisites

The following prerequisites are required to use this application. Please ensure that you have them all installed locally.

- [Java 17 or later](https://learn.microsoft.com/en-us/java/openjdk/install) - for API backend
- [Node.js with npm (16.13.1+)](https://nodejs.org/) - for the Web frontend
- [Maven](https://maven.apache.org/download.cgi) - for local build
- [Powershell 7](https://learn.microsoft.com/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.3) if you use windows
- [Azure Developer CLI 1.2.0 or later](https://aka.ms/azd-install)
- [Docker](https://docs.docker.com/get-docker/) - optional

## 🚁 How to run locally
To run the project on the localhost:
- `mvn clean package -DskipTests`
- `java -jar web/target/${artifact-name}-web-0.0.1-SNAPSHOT.jar`

You can also use Maven Wrapper with:
- `chmod +x mvnw`
- `mvnw clean package -DskipTests`
- `./mvnw spring-boot:run -f web/pom.xml`

To test the local project, access port 8080 (by default) or the one that you specified:
- `http://localhost:8080/`

## How to deploy on Azure
1. Log in to [azd](https://aka.ms/azd-install). Only required once per-install.
</br> `azd auth login`
    * If you are on Windows, install [powershell](https://learn.microsoft.com/powershell/scripting/install/installing-powershell-on-windows)
1. Navigate to the generated project directory and run
</br>`azd up`

  After the command is executed, you can see the following log signs that the deployment was successful.

  ```text
  SUCCESS: Your application was provisioned and deployed to Azure Container Apps in <deployment-time>.
  You can view the resources created under the resource group <your-resource-group> in Azure Portal:
  https://portal.azure.come/#@/resource/subscriptions/<subscription-id>/resourceGroups/<your-resource-group>/overview
```

The output **Application url** is the endpoint to access the todo application.

### Application Architecture

This application utilizes the following Azure resources:

- [**Azure Container Apps**](https://docs.microsoft.com/azure/container-apps/) to host the application
- [**Azure PostgreSQL - Flexible Server**](https://docs.microsoft.com/azure/postgresql/flexible-server/) for storage

Here's a high level architecture diagram that illustrates these components. Notice that these are all contained within a single [resource group](https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal), that will be created for you when you create the resources.

!["Application architecture diagram"](assets/resources.png)

> This template provisions resources to an Azure subscription that you will select upon provisioning them. Please refer to the [Pricing calculator for Microsoft Azure](https://azure.microsoft.com/pricing/calculator/) and, if needed, update the included Azure resource definitions found in `infra/main.bicep` to suit your needs.

### Application Code

This template is structured to follow the [Azure Developer CLI](https://aka.ms/azure-dev/overview). You can learn more about `azd` architecture in [the official documentation](https://learn.microsoft.com/azure/developer/azure-developer-cli/make-azd-compatible?pivots=azd-create#understand-the-azd-architecture).

### Next Steps

- At this point, you have a complete application deployed on Azure. But there is much more that the Azure Developer CLI can do. These next steps will introduce you to additional commands that will make creating applications on Azure much easier. Using the Azure Developer CLI, you can delete the resources easily.

- [`azd down`](https://learn.microsoft.com/azure/developer/azure-developer-cli/reference#azd-down) - to delete all the Azure resources created with this template


### Additional `azd` commands

The Azure Developer CLI includes many other commands to help with your Azure development experience. You can view these commands at the terminal by running `azd help`. You can also view the full list of commands on our [Azure Developer CLI command](https://aka.ms/azure-dev/ref) page.

## Reporting Issues and Feedback

If you have any feature requests, issues, or areas for improvement, please [file an issue](https://aka.ms/azure-dev/issues). To keep up-to-date, ask questions, or share suggestions, join our [GitHub Discussions](https://aka.ms/azure-dev/discussions). You may also contact us via AzDevTeam@microsoft.com.
