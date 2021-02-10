---
title: "Developing Solutions for Microsoft Azure AZ-204 certification preparations notes"
date: 2020-12-31 +0200
last_modified_at: 2021-01-03 +0200
categories: AZ-204 azure certification
toc: true
toc_label: Topics
toc_icon: quote-right
---

Taking notes for [AZ-900 Microsoft Azure Fundamentals]({% post_url 2020-12-31-notes-on-az-900-azure-fundamentals-certification %}) proved to be a good idea so let's do it again. This time for [AZ-204 Developing Solutions for Microsoft Azure](https://docs.microsoft.com/en-us/learn/certifications/exams/az-204). Same approach: start with [exam skill outline](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oZ7B) (May 18, 2020 version) and follow the [learning paths](https://docs.microsoft.com/en-us/learn/certifications/exams/az-204?tab=tab-learning-paths).

## Develop Azure compute solutions (25-30%)

### Implement IaaS solutions

- **_provision VMs_**

	Things to consider:
	- Network: 
		- Address space: When you set up a virtual network, you specify the available address spaces, subnets, and security. If the VNet will be connected to other VNets, you must select address ranges that are not overlapping.
		- Segregation: After deciding the virtual network address space(s), you can create one or more subnets for your virtual network. You do this to break up your network into more manageable sections. For example, you might assign 10.1.0.0 to VMs, 10.2.0.0 to back-end services, and 10.3.0.0 to SQL Server VMs.
		- Secure the network: By default, there is no security boundary between subnets, so services in each of these subnets can talk to one another. However, you can set up Network Security Groups (NSGs), which allow you to control the traffic flow to and from subnets and to and from VMs. NSGs act as software firewalls, applying custom rules to each inbound or outbound request at the network interface and subnet level.
	- Plan VM deployment: What does the server communicate with? Which ports are open? Which OS is used? How much disk space is in use? What kind of data does this use? Are there restrictions (legal or otherwise) with not having it on-premises? What sort of CPU, memory, and disk I/O load does the server have? Is there burst traffic to account for?
	- Name the VM: This name also defines a manageable Azure resource, and it's not trivial to change later. That means you should choose names that are meaningful and consistent, so you can easily identify what the VM does. A good convention is to include the following information in the name: Environment, Location, Instance, Product or Service, Role. Ex: devusc-webvm01
	- Location: The location can limit your available options. Each region has different hardware available and some configurations are not available in all regions. There are price differences between locations.
	- Size Options: General purpose, Compute optimized, Memory optimized, Storage optimized, GPU, High performance computes
	- Pricing Model: There are two separate costs the subscription will be charged for every VM: compute and storage.
		- Compute costs - Compute expenses are priced on a per-hour basis but billed on a per-minute basis.
		- Storage costs - You are charged separately for the storage the VM uses.
	- Storage: Best practice is that all Azure virtual machines will have at least two virtual hard disks (VHDs). Virtual disks can be backed by either Standard or Premium Storage accounts. When you create disks, you will have two options for managing the relationship between the storage account and each VHD:
		- Unmanaged disks: you are responsible for the storage accounts that are used to hold the VHDs that correspond to your VM disks.
		- Managed disks: the newer and recommended disk storage model. You specify the size of the disk, up to 4 TB, and Azure creates and manages both the disk and the storage.
	- Operating system: Windows or Linux. However, if you can't find a suitable OS image, you can create your disk image with what you need, upload it to Azure storage, and use it to create an Azure VM. Keep in mind that Azure only supports 64-bit operating systems.

- **_configure VMs for remote access_**

	_Secure Shell (SSH)_ is an encrypted connection protocol that allows secure sign-ins over unsecured connections. SSH allows you to connect to a terminal shell from a remote location using a network connection. There are two approaches we can use to authenticate an SSH connection: username and password, or an SSH key pair.

	There are two parts to an SSH key pair: a public key and a private key.
	- The public key is placed on your Linux VM or any other service that you wish to use with public-key cryptography. This can be shared with anyone.
	- The private key is what you present to verify your identity to your Linux VM when you make an SSH connection. Consider this confidential information and protect this like you would a password or any other private data.

	With a public IP, we can interact with the VM over the Internet. Public IP addresses in Azure are dynamically allocated by default. That means the IP address can change over time - for VMs the IP address assignment happens when the VM is restarted. You can pay more to assign static addresses.

	To connect to the VM via SSH, you need:
	- the public IP address of the VM
	- the username of the local account on the VM
	- a public key configured in that account
	- access to the corresponding private key
	- port 22 open on the VM

	_Remote Desktop (RDP)_ provides remote connectivity to the UI of Windows-based computers. Microsoft provides RDP clients for the following operating systems: Windows (built-in), macOS, iOS and Android. There are also open-source Linux clients, such as Remmina that enable you to connect to a Windows PC from an Ubuntu distribution.

	You can secure your management ports with _just-in-time access_. You can lock down inbound traffic to your Azure Virtual Machines with Azure Security Center's just-in-time (JIT) virtual machine (VM) access feature. You can request access to a JIT-enabled VM from Security Center, Azure virtual machines, PowerShell, or the REST API.

- **_create ARM templates_**

	Resource Manager templates are JSON files that define the resources you need to deploy for your solution. Create resource templates from the Automation section for a specific VM by selecting the Export template option. 

	Advantages:
	- Declarative syntax
	- Repeatable results
	- Orchestration: You don't have to worry about the complexities of ordering operations. Resource Manager orchestrates the deployment of interdependent resources so they're created in the correct order. When possible, Resource Manager deploys resources in parallel so your deployments finish faster than serial deployments.
	- Modular files: You can break your templates into smaller, reusable components and link them together at deployment time.
	- Extensibility: With deployment scripts, you can add PowerShell or Bash scripts to your templates.
	Testing: You can make sure your template follows recommended guidelines by testing it with the ARM template tool kit (arm-ttk). This test kit is a PowerShell script that you can download from GitHub.
	- Preview changes: You can use the what-if operation to get a preview of changes before deploying the template. With what-if, you see which resources will be created, updated, or deleted, and any resource properties that will be changed. The what-if operation checks the current state of your environment and eliminates the need to manage state.
	- Built-in validation: Your template is deployed only after passing validation.
	- Tracked deployments: In the Azure portal, you can review the deployment history and get information about the template deployment. You can see the template that was deployed, the parameter values passed in, and any output values.
	- Policy as code: Azure Policy is a policy as code framework to automate governance. If you're using Azure policies, policy remediation is done on non-compliant resources when deployed through templates.
	- Deployment Blueprints: You can take advantage of Blueprints provided by Microsoft to meet regulatory and compliance standards. These blueprints include pre-built templates for various architectures.
	- CI/CD integration
	- Exportable code: You can get a template for an existing resource group by either exporting the current state of the resource group, or viewing the template used for a particular deployment.
	- Authoring tools

	The template has the following sections:
	- Parameters - Provide values during deployment that allow the same template to be used with different environments.
	- Variables - Define values that are reused in your templates. They can be constructed from parameter values.
	- User-defined functions - Create customized functions that simplify your template.
	- Resources - Specify the resources to deploy.
	- Outputs - Return values from the deployed resources.

	After creating your template, you may wish to share it with other users in your organization. Template specs enable you to store a template as a resource type.

	Commands:
	- PowerShell: `New-AzResourceGroupDeployment -Name myDeploymentName -ResourceGroupName myResourceGroup -TemplateFile $templateFile`
	- CLI: `az deployment group create --name myDeploymentName --resource-group myResourceGroup --template-file $templateFile`

- **_create container images for solutions by using Docker_**

	

- **_publish an image to the Azure Container Registry_**

	Container Registry is an Azure service that you can use to create your own private Docker registries. Like Docker Hub, Container Registry is organized around repositories that contain one or more images. Container Registry also lets you automate tasks such as redeploying an app when an image is rebuilt.

	Security is an important reason to choose Container Registry instead of Docker Hub:
	- You have much more control over who can see and use your images.
	- You can sign images to increase trust and reduce the chances of an image becoming accidentally (or intentionally) corrupted or otherwise infected.
	- All images stored in a container registry are encrypted at rest.
	- Container Registry runs in Azure. The registry can be replicated to store images near where they're likely to be deployed.
	- Container Registry is highly scalable, providing enhanced throughput for Docker pulls that can span many nodes concurrently. The Premium SKU of Container Registry includes 500 GiB of storage.

	You create a registry by using either the Azure portal or the Azure CLI `acr create` command. In addition to storing and hosting images, you can also use Container Registry to build images. Instead of building an image yourself and pushing it to Container Registry, use the CLI to upload the Docker file and other files that make up your image. Container Registry will then build the image for you. Use the `acr build` command to run a build.

	You use the _tasks_ feature of Container Registry to rebuild your image whenever its source code changes automatically. You configure a Container Registry task to monitor the GitHub repository that contains your code and trigger a build each time it changes. Container Registry tasks must be created from the command line.

- **_run containers by using Azure Container Instance_**

### Create Azure App Service Web Apps

- **_create an Azure App Service Web App_**

	**Azure App Service** is a fully managed web application hosting platform. This platform as a service (PaaS) offered by Azure allows you to focus on designing and building your app while Azure takes care of the infrastructure to run and scale your applications.

	Using the Azure portal, you can easily add deployment slots to an App Service web app. For instance, you can create a staging deployment slot where you can push your code to test on Azure. Once you are happy with your code, you can easily swap the staging deployment slot with the production slot.

	The Azure portal provides out-of-the-box continuous integration and deployment with Azure DevOps, GitHub, Bitbucket, FTP, or a local Git repository on your development machine. Connect your web app with any of the above sources and App Service will do the rest for you by automatically syncing your code and any future changes on the code into the web app.

	Baked into the web app is the ability to scale up/down or scale out. Depending on the usage of the web app, you can scale your app up/down by increasing/decreasing the resources of the underlying machine that is hosting your web app. Resources can be number of cores or the amount of RAM available.

	Creating a web app allocates a set of hosting resources in App Service, which you can use to host any web-based application that is supported by Azure, whether it be ASP.NET Core, Node.js, Java, Python, etc.

	Among other things, web app requires the following:
	- Publish type: You can deploy your application to App Service as code or as a ready-to-run Docker image. Selecting Docker image will activate the Docker tab of the wizard, where you provide information about the Docker registry from which App Service will retrieve your image.
	- Runtime stack: If you choose to deploy your application as code, App Service needs to know what runtime your application uses (examples include Node.js, Python, Java, and .NET). If you deploy your application as a Docker image, you will not need to choose a runtime stack, since your image will include it.
	- Operating system: If you are deploying your app as code, many of the available runtime stacks are limited to one operating system or the other. If your application is packaged as a Docker image, choose the operating system on which your image is designed to run. Selecting Windows activates the Monitoring tab, where you have the option to enable _Application Insights_. Application Insights can be used from Linux-hosted apps as well, but this turnkey, no-code option is only available on Windows.
	- App Service plans: An App Service plan is a set of virtual server resources that run App Service apps. A plan's size (sometimes referred to as its sku or pricing tier) determines the performance characteristics of the virtual servers that run the apps assigned to the plan and the App Service features that those apps have access to. Every App Service web app you create must be assigned to a single App Service plan that runs it. App Service plans are the unit of billing for App Service. The size of each App Service plan in your subscription, in addition to the bandwidth resources used by the apps deployed to those plans, determines the price that you pay. The number of web apps deployed to your App Service plans has no effect on your bill.

- **_enable diagnostics logging_**

- **_deploy code to a web app_**

	_Automated deployment_, or continuous integration, is a process used to push out new features and bug fixes in a fast and repetitive pattern with minimal impact on end users.

	Azure supports automated deployment directly from several sources. The following options are available:
	- Azure DevOps: You can push your code to Azure DevOps (previously known as Visual Studio Team Services), build your code in the cloud, run the tests, generate a release from the code, and finally, push your code to an Azure Web App.
	- GitHub: Azure supports automated deployment directly from GitHub. When you connect your GitHub repository to Azure for automated deployment, any changes you push to your production branch on GitHub will be automatically deployed for you.
	- Bitbucket: With its similarities to GitHub, you can configure an automated deployment with Bitbucket.
	- OneDrive: Microsoft's cloud-based storage. You must have a Microsoft Account linked to a OneDrive account to deploy to Azure.
	- Dropbox: Azure supports deployment from Dropbox, which is a popular cloud-based storage system that is similar to OneDrive.

	There are a few options that you can use to _manually_ push your code to Azure:
	- Git: App Service web apps feature a Git URL that you can add as a remote repository. Pushing to the remote repository will deploy your app.
	- az webapp up: webapp up is a feature of the az command-line interface that packages your app and deploys it. Unlike other deployment methods, az webapp up can create a new App Service web app for you if you haven't already created one.
	- ZIP deploy: Use az webapp deployment source config-zip to send a ZIP of your application files to App Service. ZIP deploy can also be accessed via basic HTTP utilities such as curl.
	- WAR deploy: It's an App Service deployment mechanism specifically designed for deploying Java web applications using WAR packages. WAR deploy can be accessed using the Kudu HTTP API located at https://<your-app-name>.scm.azurewebsites.net/api/wardeploy.
	- Visual Studio: Visual Studio features an App Service deployment wizard that can walk you through the deployment process.
	- FTP/S: FTP or FTPS is a traditional way of pushing your code to many hosting environments, including App Service.

	Within a single Azure App Service web app, you can create multiple deployment slots. Each slot is a separate instance of that web app, and it has a separate hostname. You can deploy a different version of your web app into each slot. Deployment slots are available only when your web app uses an App Service plan in the Standard, Premium, or Isolated tier. The new slot is effectively a separate web app with a different hostname. That's why anyone on the internet can access it if they know that hostname. You can control access to a slot by using IP address restrictions. 

- **_configure web app settings including SSL, API, and connection strings_**

- **_implement autoscaling rules, including scheduled autoscaling, and scaling by operational or system metrics_**

	When you create a web app, you can either create a new App Service plan or use an existing one. If you select an existing plan, any other web apps that use the same plan will share resources with your web app. They'll all scale together, so they need to have the same scaling requirements. If your apps have different requirements, use a separate App Service plan for each one.

	You scale out by adding more instances to an App Service plan, up to the limit available for your selected tier.

	You scale an App Service plan up and down by changing the pricing tier and hardware level that it runs on. Scaling up can cause an interruption in service to client apps running at the time. Also, scaling up can cause the outgoing IP addresses for the web app to change.

	??? autoscaling ???

### Implement Azure functions

**Azure Functions** is a serverless application platform. It allows developers to host business logic that can be executed without provisioning infrastructure. Functions provides intrinsic scalability and you are charged only for the resources used. You can write your function code in the language of your choice, including C#, F#, JavaScript, Python, and PowerShell Core. Support for package managers like NuGet and NPM is also included, so you can use popular libraries in your business logic.

An Azure Functions app stores management information, code, and logs in Azure Storage. The storage account must support Azure Blob, Queue, Files, and Table storage; use a general Azure Storage account for this purpose.

- **_implement input and output bindings for a function_**

	Bindings are a declarative way to connect data and services to your function. Bindings know how to talk to different services, which means you don't have to write code in your function to connect to data sources and manage connections. The platform takes care of that complexity for you as part of the binding code. Each binding has a direction - your code reads data from input bindings, and writes data to output bindings. Each function can have zero or more bindings to manage the input and output data processed by the function.

	A trigger is a special type of input binding that has the additional capability of initiating execution.

	Three properties are required in all bindings. You may have to supply additional properties based on the type of binding and storage you are using.
	- Name - Defines the function parameter through which you access the data. For example, in a queue input binding, this is the name of the function parameter that receives the queue message content.
	- Type - Identifies the type of binding, i.e., the type of data or service we want to interact with.
	- Direction - Indicates the direction data is flowing, i.e., is it an input or output binding?

	Additionally, most binding types also need a fourth property:

	- Connection - Provides the name of an app setting key that contains the connection string. Bindings use connection strings stored in app settings to keep secrets out of the function code. This makes your code more configurable and secure.

	Bindings are defined in JSON. A binding is configured in your function's configuration file, which is named function.json and lives in the same folder as your function code.

	A _binding expression_ is specialized text in function.json, function parameters, or code that is evaluated when the function is invoked to yield a value. Types of binding expressions:
	- App settings
	- Trigger file name
	- Trigger metadata
	- JSON payloads
	- New GUID
	- Current date and time

- **_implement function triggers by using data operations, timers, and webhooks_**

	The type of event that starts the function is called a trigger. You must configure a function with exactly one trigger. Azure supports triggers for the following services:

	Service	| Trigger description
	-- | --
	Blob storage | Starts a function when a new or updated blob is detected.
	Azure Cosmos DB | Start a function when inserts and updates are detected.
	Event Grid | Starts a function when an event is received from Event Grid.
	HTTP | Starts a function with an HTTP request.
	Microsoft Graph Events | Starts a function in response to an incoming webhook from the Microsoft Graph. Each instance of this trigger can react to one Microsoft Graph resource type.
	Queue storage |	Starts a function when a new item is received on a queue. The queue message is provided as input to the function.
	Service Bus	| Starts a function in response to messages from a Service Bus queue.
	Timer | Starts a function on a schedule.

	**Secure HTTP triggers**: HTTP triggers let you use API keys to block unknown callers by requiring the key to be present on each request. When you create a function, you select the authorization level. By default, it's set to Function, which requires a function-specific API key, but it can also be set to Admin to use a global "master" key, or Anonymous to indicate that no key is required. You can also change the authorization level through the function properties after creation.

	A **blob trigger** is a trigger that executes a function when a file is uploaded or updated in Azure Blob storage (data operation). To create a blob trigger, you create an Azure Storage account and provide a location that the trigger monitors.

	One setting that you'll want to look at is the _Path_. The Path tells the blob trigger where to monitor to see if a blob is uploaded or updated. i.e samples-workitems/{name}.png

	A **timer trigger** is a trigger that executes a function at a consistent interval. To create a timer trigger, you need to supply two pieces of information:
	- A _Timestamp_ parameter name, which is simply an identifier to access the trigger in code.
	- A _Schedule_, which is a CRON expression that sets the interval for the timer.

	An **HTTP trigger (webhook)** is a trigger that executes a function when it receives an HTTP request. HTTP triggers have many capabilities and customizations, including:
	- Provide authorized access by supplying keys.
	- Restrict which HTTP verbs are supported.
	- Return data back to the caller.
	- Receive data through query string parameters or through the request body.
	- Support URL route templates to modify the function URL.
	- When you create an HTTP trigger, select a programming language, provide a trigger name, and select an Authorization level.

	One setting that's important to understand is _Request parameter name_. This setting is a string that represents the name of the parameter that contains the information about an incoming HTTP request. By default, the name of the parameter is _req_.

- **_implement Azure Durable Functions_**

	**Durable Functions** is an extension of Azure Functions that enables you to perform long-lasting, stateful operations in Azure. Azure provides the infrastructure for maintaining state information. You can use Durable Functions to orchestrate a long-running workflow.

	Benefits of using **Durable Functions** include:
	- They enable you to write event driven code. A durable function can wait asynchronously for one or more external events, and then perform a series of tasks in response to these events.
	- You can chain functions together. You can implement common patterns such as fan-out/fan-in, which uses one function to invoke others in parallel, and then accumulate the results.
	- You can orchestrate and coordinate functions, and specify the order in which functions should execute.
	- The state is managed for you. You don't have to write your own code to save state information for a long-running function.

	Durable functions allows you to define stateful workflows using an _orchestration_ function. An orchestration function provides these extra benefits:
	- You can define the workflows in code. You don't need to write a JSON description or use a workflow design tool.
	- Functions can be called both synchronously and asynchronously. Output from the called functions is saved locally in variables and used in subsequent function calls.
	- Azure checkpoints the progress of a function automatically when the function awaits. Azure may choose to dehydrate the function and save its state while the function waits, to preserve resources and reduce costs. When the function starts running again, Azure will rehydrate it and restore its state.
 
	Function types:
	- _Client_ functions are the entry point for creating an instance of a Durable Functions orchestration. They can run in response to an event from many sources, such as a new HTTP request arriving, a message being posted to a message queue, an event arriving in an event stream. You can write them in any of the supported languages.
	- _Orchestrator_ functions describe how actions are executed, and the order in which they are run. You write the orchestration logic in code (only C# or JavaScript).
	- _Activity_ functions are the basic units of work in a durable function orchestration. An activity function contains the actual work performed by the tasks being orchestrated.

	Application patterns:
	- _Function chaining_ - In this pattern, the workflow executes a sequence of functions in a specified order. The output of one function is applied to the input of the next function in the sequence. The output of the final function is used to generate a result.
	- _Fan out/fan in_ - This pattern runs multiple functions in parallel and then waits for all the functions to finish. The results of the parallel executions can be aggregated or used to compute a final result.
	- _Async HTTP APIs_ - This pattern addresses the problem of coordinating state of long-running operations with external clients. An HTTP call can trigger the long-running action. Then, it can redirect the client to a status endpoint. The client can learn when the operation is finished by polling this endpoint.
	- _Monitor_ - This pattern implements a recurring process in a workflow, possibly looking for a change in state. For example, you could use this pattern to poll until specific conditions are met.
	- _Human interaction_ - This pattern combines automated processes that also involve some human interaction. A manual process within an automated process is tricky because people aren't as highly available and as responsive as most computers. Human interaction can be incorporated using timeouts and compensation logic that runs if the human fails to interact correctly within a specified response time. An approval process is an example of a process that involves human interaction.

## Develop for Azure storage (10-15%)

### Develop solutions that use Cosmos DB storage

- **_select the appropriate API for your solution_**

- **_implement partitioning schemes_**

- **_interact with data using the appropriate SDK_**

- **_set the appropriate consistency level for operations_**

- **_create Cosmos DB containers_**

- **_implement scaling (partitions, containers)_**

- **_implement server-side programming including stored procedures, triggers, and change feed notifications_**

### Develop solutions that use blob storage

Azure Storage supports three kinds of blobs:

Blob type| Description
-- | --
Block blobs | Block blobs are used to hold text or binary files up to ~5 TB (50,000 blocks of 100 MB) in size. The primary use case for block blobs is the storage of files that are read from beginning to end, such as media files or image files for websites. They are named block blobs because files larger than 100 MB must be uploaded as small blocks. These blocks are then consolidated (or committed) into the final blob.
Page blobs | Page blobs are used to hold random-access files up to 8 TB in size. Page blobs are used primarily as the backing storage for the VHDs used to provide durable disks for Azure Virtual Machines (Azure VMs). They are named page blobs because they provide random read/write access to 512-byte pages.
Append blobs | Append blobs are made up of blocks like block blobs, but they are optimized for append operations. These blobs are frequently used for logging information from one or more sources into the same blob. For example, you might write all of your trace logging to the same append blob for an application running on multiple VMs. A single append blob can be up to 195 GB.

- **_move items in Blob storage between storage accounts or containers_**

???

- **_set and retrieve properties and metadata_**

???

- **_interact with data using the appropriate SDK_**

??? - maybe read the exercises again

- **_implement data archiving and retention_**

???

- **_implement hot, cool, and archive storage_**

???

## Implement Azure security (15-20%)

### Implement user authentication and authorization

- **_implement OAuth2 authentication_**

- **_create and implement shared access signatures_**

- **_register apps and use Azure Active Directory to authenticate users_**

- **_control access to resources by using role-based access controls (RBAC)_**

	You control access to resources using Azure RBAC by creating role assignments, which control how permissions are enforced. You can think of these elements as "who", "what", and "where".
	- _Security principal_ (who): A security principal is just a fancy name for a user, group, or application that you want to grant access to.
	- _Role definition_ (what you can do): A role definition is a collection of permissions.
	- _Scope_ (where): Scope is where the access applies to.

### Implement secure cloud solutions

- **_secure app configuration data by using the App Configuration and KeyVault API_**
	
- **_manage keys, secrets, and certificates by using the KeyVault API_**

	Key Vault access has two facets: the management of the Key Vault itself (_management plane_), and accessing the data contained in the Key Vault (_data plane_)

- **_implement Managed Identities for Azure resources_**

## Monitor, troubleshoot, and optimize Azure solutions (10-15%)

## Connect to and consume Azure services and third-party services (25-30%)

### Develop an App Service Logic App

- **_create a Logic App_**

- **_create a custom connector for Logic Apps_**

- **_create a custom template for Logic Apps_**

### Implement API Management

The **Azure API Management (APIM)** service enables you to construct an API from a set of disparate microservices. **Azure API Management (APIM)** is a fully managed cloud service that you can use to publish, secure, transform, maintain, and monitor APIs. It helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services. API Management handles all the tasks involved in mediating API calls, including _request authentication and authorization_, _rate limit and quota enforcement_, _request and response transformation_, _logging and tracing_, and _API version management_. APIM enables you to create and manage modern API gateways for existing backend services no matter where they are hosted.

By default the new API is created under the `azure-api.net` domain.

- **_create an APIM instance_**

	In Azure Portal: Function App -> Api Management -> Create new.

	Composing an API using API Management has advantages that include:
	- Client apps are coupled to the API expressing business logic, not the underlying technical implementation with individual microservices. You can change the location and definition of the services without necessarily reconfiguring or updating the client apps.
	- API Management acts as an intermediary. It forwards requests to the right microservice, wherever it is located, and returns responses to users. Users never see the different URIs where microservices are hosted.
	- You can use API Management policies to enforce consistent rules on all microservices in the product. For example, you can transform all XML responses into JSON, if that is your preferred format. 
	- Policies also enable you to enforce consistent security requirements.

	API Management also includes helpful tools - you can test each microservice and its operations to ensure that they behave in accordance with your requirements. You can also monitor the behavior and performance of deployed services.

	Azure API Management supports importing Azure Function Apps as new APIs or appending them to existing APIs. The process automatically generates a host key in the Azure Function App, which is then assigned to a named value in Azure API Management.

- **_configure authentication for APIs_**

	???

- **_define policies for APIs_**

	???

### Develop event-based solutions

Events are lighter weight than messages, and are most often used for broadcast communications. The components sending the event are known as publishers, and receivers are known as subscribers.

- **_implement solutions that use Azure Event Grid_**

	**Azure Event Grid** is a fully-managed event routing service running on top of Azure Service Fabric. Event Grid distributes events from different sources, such as Azure Blob storage accounts or Azure Media Services, to different handlers, such as Azure Functions or Webhooks. Event Grid was created to make it easier to build event-based and serverless applications on Azure.

	Event Grid supports most Azure services as a publisher or subscriber and can be used with third-party services. It provides a dynamically scalable, low-cost, messaging system that allows publishers to notify subscribers about a status change.

	There are several concepts in Azure Event Grid that connect a source to a subscriber:
	- Events: What happened. Events are the data messages passing through Event Grid that describe what has taken place. Each event is self-contained, can be up to 64 KB.
	- Event sources: Where the event took place. Event sources are responsible for sending events to Event Grid. Each event source is related to one or more event types.
	- Topics: The endpoint where publishers send events. Event topics categorize events into groups. Topics are divided into system topics, and custom topics.
	- Event subscriptions: The endpoint or built-in mechanism to route events, sometimes to multiple handlers. Subscriptions are also used by handlers to filter incoming events intelligently.
	- Event handlers: The app or service reacting to the event.

	Event source disambiguation: _Azure Event Hub_ has the concept of an event publisher which is often confused with the event source. A publisher to Event Hub is the user or organization that decides to send events to Event Grid. For example, Microsoft publishes events for several Azure services.

	Use Event Grid when you need these features:
	- _Simplicity_: It is straightforward to connect sources to subscribers in Event Grid.
	- _Advanced_ filtering: Subscriptions have close control over the events they receive from a topic.
	- _Fan-out_: You can subscribe to an unlimited number of endpoints to the same events and topics.
	- _Reliability_: Event Grid retries event delivery for up to 24 hours for each subscription.
	- _Pay-per-event_: Pay only for the number of events that you transmit.

- **_implement solutions that use Azure Notification Hubs_**

	???

- **_implement solutions that use Azure Event Hub_**

	**Azure Event Hubs** is a cloud-based, event-processing service that can receive and process millions of events per second. Event Hubs acts as a front door for an event pipeline, to receive incoming data and stores this data until processing resources are available.. Unlike Event Grid, however, it is optimized for extremely high throughput, a large number of publishers, security, and resiliency.

	_Events_. An event is a small packet of information (a datagram) that contains a notification. Events can be published individually, or in batches, but a single publication (individual or batch) can't exceed 1 MB.

	_Publishers_. Event publishers are any app or device that can send out events using either HTTPS or Advanced Message Queuing Protocol (AMQP) 1.0. For publishers that send data frequently, AMQP has better performance. However, it has a higher initial session overhead, because a persistent bidirectional socket and transport-level security (TLS) or SSL/TLS has to be set up first.
	
	_Subscribers_. Event subscribers are apps that use one of two supported programmatic methods to receive and process events from an Event Hub.

	_Consumer groups_. An Event Hub consumer group represents a specific view of an Event Hub data stream. By using separate consumer groups, multiple subscriber apps can process an event stream independently, and without affecting other apps. However, the use of many consumer groups isn't a requirement, and for many apps, the single default consumer group is sufficient.

	_Partitions_. As Event Hubs receives communications, it divides them into _partitions_. _Partitions_ are buffers into which the communications are saved. Because of the event buffers, events are not completely ephemeral, and an event isn't missed just because a subscriber is busy or even offline. The subscriber can always use the buffer to "catch up." By default, events stay in the buffer for 24 hours before they automatically expire. The buffers are called partitions because the data is divided amongst them. Every event hub has at least two partitions, and each partition has a separate set of subscribers.

	_Capture_. Event Hubs can send all your events immediately to Azure Data Lake or Azure Blob storage for inexpensive, permanent persistence.

	_Authentication_. All publishers are authenticated and issued a token. This means Event Hubs can accept events from external devices and mobile apps, without worrying that fraudulent data from pranksters could ruin our analysis.

	Event Hubs has support for pipelining event streams to other Azure services. Using it with Azure Stream Analytics, for instance, allows complex analysis of data in near real time, with the ability to correlate multiple events and look for patterns. In this case, Stream Analytics would be considered a subscriber.

	Choose Event Hubs if:
	- You need to support authenticating a large number of publishers.
	- You need to save a stream of events to Data Lake or Blob storage.
	- You need aggregation or analytics on your event stream.
	- You need reliable messaging or resiliency.

### Develop message-based solutions

In the terminology of distributed applications, messages have the following characteristics: it contains raw data, produced by one component, that will be consumed by another component; it contains the data itself, not just a reference to that data; the sending component expects the message content to be processed in a certain way by the destination component. The integrity of the overall system may depend on both sender and receiver doing a specific job.

Benefits of queues: increased reliability, message delivery guarantees, transactional support

- **_implement solutions that use Azure Service Bus**_

	**Service Bus** is a message broker system intended for enterprise applications. These apps often utilize multiple communication protocols, have different data contracts, higher security requirements, and can include both cloud and on-premises services. Service Bus is built on top of a dedicated messaging infrastructure designed for exactly these scenarios.

	A _queue_ is a simple temporary storage location for messages. A sending component adds a message to the queue. A destination component picks up the message at the front of the queue. Under ordinary circumstances, each message is received by only one receiver.

	_Topics_ are like queues, but can have multiple subscribers. When a message is sent to a topic instead of a queue, multiple components can be triggered to do their work. Internally, topics use queues. When you post to a topic, the message is copied and dropped into the queue for each subscription. The queue means that the message copy will stay around to be processed by each subscription branch even if the component processing that subscription is too busy to keep up.

	A _relay_ is an object that performs synchronous, two-way communication between applications. Unlike queues and topics, it is not a temporary storage location for messages. Instead, it provides bidirectional, unbuffered connections across network boundaries such as firewalls. Use a relay when you want direct communications between components as if they were located on the same network segment but separated by network security devices.

	Use Service Bus topics if you:
	- Need multiple receivers to handle each message

	Use Service Bus queues if you:
	- Need an At-Most-Once delivery guarantee.
	- Need a FIFO guarantee.
	- Need to group messages into transactions.
	- Want to receive messages without polling the queue.
	- Need to provide a role-based access model to the queues.
	- Need to handle messages larger than 64 KB but less than 256 KB.
	- Queue size will not grow larger than 80 GB.
	- Want to publish and consume batches of messages.

- **_implement solutions that use Azure Queue Storage queues**_

	**Queue storage** is a service that uses Azure Storage to store large numbers of messages that can be securely accessed from anywhere in the world using a simple REST-based interface. Queues can contain millions of messages, limited only by the capacity of the storage account that owns it.

	Use Queue storage if you:
	- Need an audit trail of all messages that pass through the queue.
	- Expect the queue to exceed 80 GB in size.
	- Want to track progress for processing a message inside of the queue.

	Every request to a queue must be authorized and there are several options to choose from: 
	- Azure Active Directory: You can use role-based authentication and identify specific clients based on AAD credentials.
	- Shared Key: Sometimes referred to as an account key, this is an encrypted key signature associated with the storage account. Every storage account has two of these keys that can be passed with each request to authenticate access. Using this approach is like using a root password - it provides full access to the storage account.
	- Shared access signature - A shared access signature (SAS) is a generated URI that grants limited access to objects in your storage account to clients. You can restrict access to specific resources, permissions, and scope to a data range to automatically turn off access after a period of time.


	Broken URLs for Thomas Maurer:
	- Extend Azure Resource Manager template functionality