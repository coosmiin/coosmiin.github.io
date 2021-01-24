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

- **_create ARM templates_**

	Resource Manager templates are JSON files that define the resources you need to deploy for your solution. Create resource templates from the Automation section for a specific VM by selecting the Export template option. 

- **_create container images for solutions by using Docker_**

- **_publish an image to the Azure Container Registry_**

- **_run containers by using Azure Container Instance_**

### Create Azure App Service Web Apps

- **_create an Azure App Service Web App_**

- **_enable diagnostics logging_**

- **_deploy code to a web app_**

- **_configure web app settings including SSL, API, and connection strings_**

- **_implement autoscaling rules, including scheduled autoscaling, and scaling by operational or system metrics_**

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