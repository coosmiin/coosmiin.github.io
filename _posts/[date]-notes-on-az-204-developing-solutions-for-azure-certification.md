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

- **_configure VMs for remote access_**

- **_create ARM templates_**

- **_create container images for solutions by using Docker_**

- **_publish an image to the Azure Container Registry_**

- **_run containers by using Azure Container Instance_**

- **_Azure Kubernetes Service (AKS) is out of scope_**

### Create Azure App Service Web Apps

- **_create an Azure App Service Web App_**

- **_enable diagnostics logging_**

- **_deploy code to a web app_**

- **_configure web app settings including SSL, API, and connection strings_**

- **_implement autoscaling rules, including scheduled autoscaling, and scaling by operational or system metrics_**

### Implement Azure functions

**Azure Functions** is a serverless application platform. It allows developers to host business logic that can be executed without provisioning infrastructure. Functions provides intrinsic scalability and you are charged only for the resources used. You can write your function code in the language of your choice, including C#, F#, JavaScript, Python, and PowerShell Core. Support for package managers like NuGet and NPM is also included, so you can use popular libraries in your business logic.

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
	- _Orchestrator_ functions describe how actions are executed, and the order in which they are run. You write the orchestration logic in code (C# or JavaScript).
	- _Activity_ functions are the basic units of work in a durable function orchestration. An activity function contains the actual work performed by the tasks being orchestrated.

	Application patterns:
	- _Function chaining_ - In this pattern, the workflow executes a sequence of functions in a specified order. The output of one function is applied to the input of the next function in the sequence. The output of the final function is used to generate a result.
	- _Fan out/fan in_ - This pattern runs multiple functions in parallel and then waits for all the functions to finish. The results of the parallel executions can be aggregated or used to compute a final result.
	- _Async HTTP APIs_ - This pattern addresses the problem of coordinating state of long-running operations with external clients. An HTTP call can trigger the long-running action. Then, it can redirect the client to a status endpoint. The client can learn when the operation is finished by polling this endpoint.
	- _Monitor_ - This pattern implements a recurring process in a workflow, possibly looking for a change in state. For example, you could use this pattern to poll until specific conditions are met.
	- _Human interaction_ - This pattern combines automated processes that also involve some human interaction. A manual process within an automated process is tricky because people aren't as highly available and as responsive as most computers. Human interaction can be incorporated using timeouts and compensation logic that runs if the human fails to interact correctly within a specified response time. An approval process is an example of a process that involves human interaction.

## Develop for Azure storage (10-15%)

### Develop solutions that use Cosmos DB storage

### Develop solutions that use blob storage

Azure Storage supports three kinds of blobs:

Blob type| Description
-- | --
Block blobs | Block blobs are used to hold text or binary files up to ~5 TB (50,000 blocks of 100 MB) in size. The primary use case for block blobs is the storage of files that are read from beginning to end, such as media files or image files for websites. They are named block blobs because files larger than 100 MB must be uploaded as small blocks. These blocks are then consolidated (or committed) into the final blob.
Page blobs | Page blobs are used to hold random-access files up to 8 TB in size. Page blobs are used primarily as the backing storage for the VHDs used to provide durable disks for Azure Virtual Machines (Azure VMs). They are named page blobs because they provide random read/write access to 512-byte pages.
Append blobs | Append blobs are made up of blocks like block blobs, but they are optimized for append operations. These blobs are frequently used for logging information from one or more sources into the same blob. For example, you might write all of your trace logging to the same append blob for an application running on multiple VMs. A single append blob can be up to 195 GB.