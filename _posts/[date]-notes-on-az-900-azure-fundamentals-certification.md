---
title: "Notes on Microsoft Azure Fundamentals AZ-900 exam prerarations"
date: [date] +0200
categories: 
---

While learning for the [AZ-900 Microsoft Azure Fundamentals](https://docs.microsoft.com/en-us/learn/certifications/exams/az-900) exam, I thought it would be nice to track my progress by taking notes on various topics that I need to learn for the exam. My approach? Start from [exam skill outline](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE3VwUY), follow the [learning paths](https://docs.microsoft.com/en-us/learn/certifications/exams/az-900?tab=tab-learning-paths) and links suggested by Thomas Maurer in his [AZ-900 Study Guide](https://www.thomasmaurer.ch/2020/03/az-900-study-guide-microsoft-azure-fundamentals-2020).

## Describe Cloud Concepts (20-25%)

### Identify the benefits and considerations of using cloud services

- **_identify the benefits of cloud computing, such as High Availability, Scalability, Elasticity, Agility, and Disaster Recovery_**

	- **High availability** - _Never go down_ or the ability to keep services up and running for long periods of time, with very little downtime.
	- **Scalability** - _Grow baby, grow_ or the ability to increase or decrease resources for any given workload (**out** and **up**). 
	- **Elasticity** - _Free to grow_ or the ability to automatically or dynamically increase or decrease resources as needed.
	- **Agility** - _Are you quick enough?_ or the ability to react quickly. Cloud services can allocate and deallocate resources quickly.
	- **Fault Tolerance** - _Wounded? I won't die!_ or the ability to remain up and running even in the event of a component (or service) no longer functioning (typically via redundancy)
	- **Disaster Recovery** - _Shit will never hit the fan_ or the ability to recover from an event which has taken down a cloud service.

- **_identify the differences between Capital Expenditure (CapEx) and Operational Expenditure (OpEx)_**

	There are two approaches to investment:
		
	- **Capital Expenditure (CapEx):** This is the up front spending of money on physical infrastructure, and then deducting that up front expense over time.
	- **Operational Expenditure (OpEx):** This is spending money on services or products now and being billed for them now. You can deduct this expense in the same year you spend it.

- **_describe the consumption-based model_**

	Cloud service providers operate on a consumption-based model, which means that end users only pay for the resources that they use.

### Describe the differences between categories of cloud services

- **_describe the shared responsibility model_**

	_Iaas_, _PaaS_ and _SaaS_ are computing models that define the different level of shared responsibility that a cloud provider and cloud tenant are responsible for.

- **_describe Infrastructure-as-a-Service (IaaS)_**

	With IaaS, you rent IT infrastructure servers and virtual machines (VMs), storage, networks, and operating systems from a cloud provider on a pay-as-you-go basis. Characteristics:

	- **Upfront costs**. IaaS has no upfront costs. Users pay only for what they consume.
	- **User ownership**. The user is responsible for the purchase, installation, configuration, and management of their own software operating systems, middleware, and applications.
	- **Cloud provider ownership**. The cloud provider is responsible for ensuring that the underlying cloud infrastructure (such as virtual machines, storage and networking) is available for the user.

- **_describe Platform-as-a-Service (PaaS)_**

	When deploying a web application using PaaS, you don't have to install an operating system, web server, or even system updates. Characteristics:

	- **Upfront costs**. There are no upfront costs, and users pay only for what they consume.
	- **User ownership**. The user is responsible for the development of their own applications. However, they are not responsible for managing the server or infrastructure. This allows the user to focus on the application or workload they want to run.
	- **Cloud provider ownership**. The cloud provider is responsible for operating system management, and network and service configuration. Cloud providers are typically responsible for everything apart from the application that a user wants to run. They provide a complete managed platform on which to run an application.

- **_describe serverless computing_**

	Overlapping with PaaS, serverless computing enables developers to build applications faster by eliminating the need for them to manage infrastructure. With serverless applications, the cloud service provider automatically provisions, scales, and manages the infrastructure required to run the code. Serverless architectures are highly scalable and event-driven. They use resources only when a specific function or trigger occurs.

- **_describe Software-as-a-Service (SaaS)_**

	Software as a Service (SaaS) is software that is centrally hosted and managed for the end customer. Characteristics: 

	- **Upfront costs**. Users have no upfront costs; they pay a subscription, typically on a monthly or annual basis.
	- **User ownership**. Users just use the application software; they are not responsible for any maintenance or management of that software.
	- **Cloud provider ownership**. The cloud provider is responsible for the provision, management, and maintenance of the application software.

- **_identify a service type based on a use case_**

### Describe the differences between types of cloud computing

- **_define cloud computing_**

	Clout computing is the delivery of computing services over the internet, which is otherwise known as the cloud. These services include servers, storage, databases, networking, software, analytics, and intelligence. Cloud computing offers faster innovation, flexible resources, and economies of scale.

- **_describe Public cloud_**

	A public cloud is owned by the cloud services provider (also known as a hosting provider). It provides resources and services to multiple organizations and users, who connect to the cloud service via a secure network connection, typically over the internet.

- **_describe Private cloud_**

	A private cloud is owned and operated by the organization that uses the resources from that cloud. They create a cloud environment in their own datacenter and provide self-service access to compute resources to users within their organization. The organization remains the owner, entirely responsible for the operation of the services they provide.

- **_describe Hybrid cloud_**

	A hybrid cloud combines both public and private clouds, allowing you to run your applications in the most appropriate location.

- **_compare and contrast the three  types of cloud computing_**

	&nbsp; | **Advantages** | **Disadvantages**
	-- | -- | -- 
	 **_Public_** | No CapEx, Agility, Consumption-based model, Maintenance, Skills | Security, Compliance, Ownership, Specific scenarios
	 **_Private_** | Control, Security, Compliance, Specific scenarios | Upfront CapEx, Agility, Maintenance, Skills
	 **_Hybrid_** | Flexibility, Costs, Control, Security, Compliance, Specific scenarios | Upfront CapEx, Costs, Skills, Ease of management

## Describe Core Azure Services (15-20%)

### Describe the core Azure architectural components

- **_describe the benefits and usage of Regions and Region Pairs_**

	A **region** is a geographical area on the planet that contains at least one but potentially multiple datacenters that are nearby and networked together with a low-latency network.
	Each Azure **region** is always **paired** with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away.

- **_describe the benefits and usage of Availability Zones_**

	**Availability zones** are physically separate datacenters within an Azure region. Each availability zone is made up of one or more datacenters equipped with independent power, cooling, and networking. An availability zone is set up to be an isolation boundary. If one zone goes down, the other continues working. Availability zones are connected through high-speed, private fiber-optic networks.

- **_describe the benefits and usage of Resource Groups_**

	A resource group is a logical container for resources deployed on Azure. These resources are anything you create in an Azure subscription like VMs, Azure Application Gateway instances, and Azure Cosmos DB instances. All resources must be in a resource group, and a resource can only be a member of a single resource group.

- **_describe the benefits and usage of Subscriptions_**

	An Azure subscription is a logical unit of Azure services that links to an Azure account, which is an identity in Azure Active Directory (Azure AD) or in a directory that Azure AD trusts. You can use Azure subscriptions to define boundaries around Azure products, services, and resources. There are two types of subscription boundaries that you can use: "Billing boundary" and "Access control boundary".

- **_describe the benefits and usage of Management Groups_**

	Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called management groups and apply your governance conditions to the management groups. All subscriptions within a management group automatically inherit the conditions applied to the management group. All subscriptions within a single management group must trust the same Azure AD tenant.

- **_describe the benefits and usage of Azure Resource Manager_**

	Azure Resource Manager  is a management layer in which resource groups and all the resources within it are created, configured, managed, and deleted. It provides a consistent management layer which allows you automate the deployment and configuration of resources using different automation and scripting tools, such as Microsoft Azure PowerShell, Azure Command-Line Interface (Azure CLI), Azure portal, REST API, and client SDKs.

	The benefits of using Resource Manager:

	- Manage your infrastructure through declarative templates rather than scripts. A Resource Manager template is a JSON file that defines what you want to deploy to Azure.
	- Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.
	- Redeploy your solution throughout the development life cycle and have confidence your resources are deployed in a consistent state.
	- Define the dependencies between resources so they're deployed in the correct order.
	- Apply access control to all services because RBAC is natively integrated into the management platform.
	- Apply tags to resources to logically organize all the resources in your subscription.
	- Clarify your organization's billing by viewing costs for a group of resources that share the same tag.

- **_explain Azure resources_**

	**Resource**: A manageable item that's available through Azure. Virtual machines (VMs), storage accounts, web apps, databases, and virtual networks are examples of resources.

### Describe core resources available in Azure

- **_describe the benefits and usage of Virtual Machines, Azure App Services, Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Windows Virtual Desktop_**

	**Virtual Machines** (VMs) are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources. _Virtual machine scale sets_ let you create and manage a group of identical, load-balanced VMs. With all VMs configured the same, virtual machine scale sets are designed to support true autoscale. No pre-provisioning of VMs is required. _Azure Batch_ enables large-scale parallel and high-performance computing (HPC) batch jobs with the ability to scale to tens, hundreds, or thousands of VMs.

	Examples of when to use VMs:
	- During testing and development
	- When running applications in the cloud
	- When extending your datacenter to the cloud
	- During disaster recovery
	- Move to cloud (lift and shift)

	**App Service** enables you to build and host web apps, background jobs, mobile back-ends, and RESTful APIs in the programming language of your choice without managing infrastructure. It offers automatic scaling and high availability. App Service supports Windows and Linux and enables automated deployments from GitHub, Azure DevOps, or any Git repo to support a continuous deployment model.
	This platform as a service (PaaS) environment allows you to focus on the website and API logic while Azure handles the infrastructure to run and scale your web applications. Types of app services: Web apps, API apps, WebJobs, Mobile apps

	**Azure Container Instances (ACI)** offers the fastest and simplest way to run a container in Azure without having to manage any virtual machines or adopt any additional services. It's a platform as a service (PaaS) offering that allows you to upload your containers, which it runs for you.

	**Azure Kubernetes Service (AKS)** is a complete orchestration service for containers with distributed architectures and large volumes of containers. Orchestration is the task of automating and managing a large number of containers and how they interact.

	**Windows Virtual Desktop** on Azure is a desktop and application virtualization service that runs on the cloud. It enables your users to use a cloud-hosted version of Windows from any location. Windows Virtual Desktop works across devices like Windows, Mac, iOS, Android, and Linux.

- **_describe the benefits and usage of Virtual Networks, VPN Gateway, Virtual Network peering, and ExpressRoute_**

	**Azure Virtual Networks** enable Azure resources, such as VMs, web apps, and databases, to communicate with each other, with users on the internet, and with your on-premises client computers. You can think of an Azure network as a set of resources that links other Azure resources.

	Azure virtual networks provide the following key networking capabilities:
		- Isolation and segmentation
		- Internet communications
		- Communicate between Azure resources via:
			- Virtual networks
			- Service endpoints
		- Communicate with on-premises resources via:
			- Point-to-site virtual private networks
			- Site-to-site virtual private networks
			- Azure ExpressRoute
		- Route network traffic as follows:
			- Route tables
			- Border Gateway Protocol
		- Filter network traffic via
			- Network security groups
			- Network virtual appliances
		- Connect virtual networks by using virtual network _peering_

	A **VPN gateway** is a type of virtual network gateway. **Azure VPN Gateway** instances are deployed in Azure Virtual Network instances and enable the following connectivity:
		- Connect on-premises datacenters to virtual networks through a site-to-site connection.
		- Connect individual devices to virtual networks through a point-to-site connection.
		- Connect virtual networks to other virtual networks through a network-to-network connection.	
	
	All transferred data is encrypted in a private tunnel as it crosses the internet. You can deploy only one VPN gateway in each virtual network, but you can use one gateway to connect to multiple locations, which includes other virtual networks or on-premises datacenters. When you deploy a VPN gateway, you specify the VPN type: either _policy-based_ or _route-based_.

	_Policy-based_ VPN gateways specify statically the IP address of packets that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through.

	With _route-based_ gateways, IPSec tunnels are modeled as a network interface or virtual tunnel interface. IP routing (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet. Route-based VPNs are the preferred connection method for on-premises devices. They're more resilient to topology changes such as the creation of new subnets.

	You can link virtual networks together by using **virtual network peering**. Peering enables resources in each virtual network to communicate with each other. These virtual networks can be in separate regions, which allows you to create a global interconnected network through Azure.

	**ExpressRoute** lets you extend your on-premises networks into the Microsoft cloud over a private connection with the help of a connectivity provider. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365. With ExpressRoute, your data doesn't travel over the public internet, so it's not exposed to the potential risks associated with internet communications. ExpressRoute is a private connection from your on-premises infrastructure to your Azure infrastructure.

- **_describe the benefits and usage of Container (Blob) Storage, Disk Storage, File Storage and storage tiers_**

	**Disk storage** provides disks for Azure virtual machines. Applications and other services can access and use as these disks as needed, similar to how they would in on-premises scenarios. Disk Storage allows data to be persistently stored and accessed from an attached virtual hard disk.

	**Azure Blob Storage** is an object storage solution for the cloud. It can store massive amounts of data, such as text or binary data. Azure Blob Storage is unstructured, meaning that there are no restrictions on the kinds of data it can hold. Blob Storage can manage thousands of simultaneous uploads, massive amounts of video data, constantly growing log files, and can be reached from anywhere with an internet connection.

	**Azure Files** offers fully managed file shares in the cloud that are accessible via the industry standard Server Message Block and Network File System (preview) protocols. Azure file shares can be mounted concurrently by cloud or on-premises deployments of Windows, Linux, and macOS. One thing that distinguishes Azure Files from files on a corporate file share is that you can access the files from anywhere in the world, by using a URL that points to the file.

	**Azure Storage** offers different **access tiers** for your blob storage, helping you store object data in the most cost-effective manner. The available access tiers include: 
		- _Hot access tier_: Optimized for storing data that is accessed frequently (for example, images for your website).
		- _Cool access tier_: Optimized for data that is infrequently accessed and stored for at least 30 days (for example, invoices for your customers).
		- _Archive access tier_: Appropriate for data that is rarely accessed and stored for at least 180 days, with flexible latency requirements (for example, long-term backups).
	
	The following considerations apply to the different access tiers:
		- Only the hot and cool access tiers can be set at the account level. The archive access tier isn't available at the account level.
		- Hot, cool, and archive tiers can be set at the blob level, during upload or after upload.
		- Data in the cool access tier can tolerate slightly lower availability, but still requires high durability, retrieval latency, and throughput characteristics similar to hot data. For cool data, a slightly lower availability service-level agreement (SLA) and higher access costs compared to hot data are acceptable trade-offs for lower storage costs.
		- Archive storage stores data offline and offers the lowest storage costs, but also the highest costs to rehydrate and access data.

- **_describe the benefits and usage of Cosmos DB, Azure SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL, and SQL Managed Instance_**

	**Azure Cosmos DB** is a globally distributed, multi-model database service. You can elastically and independently scale throughput and storage across any number of Azure regions worldwide. Azure Cosmos DB supports schema-less data, which lets you build highly responsive and "Always On" applications to support constantly changing data. At the lowest level, Azure Cosmos DB stores data in atom-record-sequence (ARS) format. The data is then abstracted and projected as an API, which you specify when you're creating your database. Your choices include SQL, MongoDB, Cassandra, Tables and Gremlin.

	**Azure SQL Database** is a relational database based on the latest stable version of the Microsoft SQL Server database engine. SQL Database is a high-performance, reliable, fully managed, and secure database.
	Azure SQL Database is a platform as a service (PaaS) database engine. It handles most of the database management functions, such as upgrading, patching, backups, and monitoring, without user involvement.
	You can migrate your existing SQL Server databases with minimal downtime by using the Azure Database Migration Service.

	**Azure Database for MySQL** is a relational database service in the cloud, and it's based on the MySQL Community Edition database engine, versions 5.6, 5.7, and 8.0. With every Azure Database for MySQL server, you take advantage of built-in security, fault tolerance, and data protection that you would otherwise have to buy or design, build, and manage. With Azure Database for MySQL, you can use point-in-time restore to recover a server to an earlier state, as far back as 35 days.

	Azure Database for MySQL delivers:

	- Built-in high availability with no additional cost.
	- Predictable performance and inclusive, pay-as-you-go pricing.
	- Scale as needed, within seconds.
	- Ability to protect sensitive data at-rest and in-motion.
	- Automatic backups.
	- Enterprise-grade security and compliance.

	You can migrate your existing MySQL databases with minimal downtime by using the Azure Database Migration Service.

	**Azure Database for PostgreSQL** is a relational database service in the cloud. The server software is based on the community version of the open-source PostgreSQL database engine.

	Moreover, Azure Database for PostgreSQL delivers the following benefits:

	- Built-in high availability compared to on-premises resources. There's no additional configuration, replication, or cost required to make sure your applications are always available.
	- Simple and flexible pricing. You have predictable performance based on a selected pricing tier choice that includes software patching, automatic backups, monitoring, and security.
	- Scale up or down as needed, within seconds. You can scale compute or storage independently as needed, to make sure you adapt your service to match usage.
	- Adjustable automatic backups and point-in-time-restore for up to 35 days.
	- Enterprise-grade security and compliance to protect sensitive data at-rest and in-motion. This security covers data encryption on disk and SSL encryption between client and server communication.

	Azure Database for PostgreSQL is available in two deployment options: Single Server and Hyperscale (Citus).	The Hyperscale (Citus) option horizontally scales queries across multiple machines by using sharding. Its query engine parallelizes incoming SQL queries across these servers for faster responses on large datasets. It serves applications that require greater scale and performance, generally workloads that are approaching, or already exceed, 100 GB of data. The Hyperscale (Citus) deployment option supports multi-tenant applications, real-time operational analytics, and high throughput transactional workloads. Applications built for PostgreSQL can run distributed queries on Hyperscale (Citus) with standard connection libraries and minimal changes.

	**Azure SQL Managed Instance** is a scalable cloud data service that provides the broadest SQL Server database engine compatibility with all the benefits of a fully managed platform as a service. Like Azure SQL Database, Azure SQL Managed Instance is a platform as a service (PaaS) database engine, which means that your company will be able to take advantage of the best features of moving your data to the cloud in a fully-managed environment. Azure SQL Database and Azure SQL Managed Instance offer many of the same features; however, Azure SQL Managed Instance provides several options that might not be available to Azure SQL Database (e.g. Cyrillic characters for collation). 
	Azure SQL Managed Instance makes it easy to migrate your on-premises data on SQL Server to the cloud using the Azure Database Migration Service (DMS) or native backup and restore.

## Describe core solutions and management tools on Azure (10-15%)

### Describe core solutions available in Azure

- **_describe the benefits and usage of Internet of Things (IoT) Hub, IoT Central, and Azure Sphere_**

	**Azure IoT Hub** is a managed service that's hosted in the cloud and that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages. You can use Azure IoT Hub to build IoT solutions with reliable and secure communications between millions of IoT devices and a cloud-hosted solution back end. You can connect virtually any device to your IoT hub.

	**Azure IoT Central** builds on top of IoT Hub by adding a dashboard that allows you to connect, monitor, and manage your IoT devices. The visual user interface (UI) makes it easy to quickly connect new devices and watch as they begin sending telemetry or error messages. You can watch the overall performance across all devices in aggregate, and you can set up alerts that send notifications when a specific device needs maintenance. Finally, you can push firmware updates to the device. A key part of IoT Central is the use of device templates. By using a device template, you can connect a device without any service-side coding.

	**Azure Sphere** creates an end-to-end, highly secure IoT solution for customers that encompasses everything from the hardware and operating system on the device to the secure method of sending messages from the device to the message hub. Azure Sphere has built-in communication and security features for internet-connected devices.

	Azure Sphere comes in three parts:
	- Azure Sphere micro-controller unit (MCU)
	- Customized Linux operating system (OS)
	- Azure Sphere Security Service

- **_describe the benefits and usage of Azure Synapse Analytics, HDInsight, and Azure Databricks_**

	**Azure Synapse Analytics** (formerly Azure SQL Data Warehouse) is a limitless analytics service that brings together enterprise data warehousing and big data analytics. You can query data on your terms by using either serverless or provisioned resources at scale. You have a unified experience to ingest, prepare, manage, and serve data for immediate BI and machine learning needs.

	**Azure HDInsight** is a fully managed, open-source analytics service for enterprises. It is a cloud service that makes it easier, faster, and more cost-effective to process massive amounts of data. You can run popular open-source frameworks and create cluster types such as Apache Spark, Apache Hadoop, Apache Kafka, Apache HBase, Apache Storm and  Machine Learning Services. HDInsight also supports a broad range of scenarios such as extraction, transformation, and loading (ETL), data warehousing; machine learning; and IoT.

	**Azure Databricks** helps you unlock insights from all your data and build artificial intelligence solutions. You can set up your Apache Spark environment in minutes, and then autoscale and collaborate on shared projects in an interactive workspace. Azure Databricks supports Python, Scala, R, Java, and SQL, as well as data science frameworks and libraries including TensorFlow, PyTorch, and scikit-learn.

- **_describe the benefits and usage of Azure Machine Learning, Cognitive Services and Azure Bot Service_**

	**Azure Machine Learning** is a platform for making predictions. It consists of tools and services that allow you to connect to data to train and test models to find one that will most accurately predict a future result. After you've run experiments to test the model, you can deploy and use it in real time via a web API endpoint.
	
	Choose Azure Machine Learning when your data scientists need complete control over the design and training of an algorithm using your own data.

	**Azure Cognitive Services** provides prebuilt machine learning models that enable applications to see, hear, speak, understand, and even begin to reason. Use Azure Cognitive Services to solve general problems, such as analyzing text for emotional sentiment or analyzing images to recognize objects or faces. You don't need special machine learning or data science knowledge to use these services. Developers access Azure Cognitive Services via APIs and can easily include these features in just a few lines of code.

	**Azure Bot Service** and **Bot Framework** are platforms for creating virtual agents that understand and reply to questions just like a human. Azure Bot Service is a bit different from Azure Machine Learning and Azure Cognitive Services in that it has a specific use case. Namely, it creates a virtual agent that can intelligently communicate with humans. Behind the scenes, the bot you build uses other Azure services, such as Azure Cognitive Services, to understand what their human counterparts are asking for.

- **_describe the benefits and usage of serverless computing solutions that include Azure Functions and Logic App_**

	**Serverless computing** is the abstraction of servers, infrastructure, and operating systems. With serverless computing, Azure takes care of managing the server infrastructure and the allocation and deallocation of resources based on demand.

	With the **Azure Functions** service, you can host a single method or function by using a popular programming language in the cloud that runs in response to an event. An example of an event might be an HTTP request, a new message on a queue, or a message on a timer.

	An Azure function is a stateless environment. A function behaves as if it's restarted every time it responds to an event. This feature is ideal for processing incoming data. And if state is required, the function can be connected to an Azure storage account.

	Azure Functions can perform orchestration tasks by using an extension called Durable Functions, which allows developers to chain functions together while maintaining state.

	**Logic Apps** is a low-code/no-code development platform hosted as a cloud service. The service helps you automate and orchestrate tasks, business processes, and workflows when you need to integrate apps, data, systems, and services across enterprises or organizations. Logic Apps simplifies how you design and build scalable solutions, whether in the cloud, on-premises, or both. This solution covers app integration, data integration, system integration, enterprise application integration (EAI), and business-to-business (B2B) integration.

- **_describe the benefits and usage of Azure DevOps, GitHub, GitHub Actions, and Azure DevTest Labs_**

	**Azure DevOps Services** is a suite of services that address every stage of the software development lifecycle. It consists of: Azure Repos, Azure Boards, Azure Pipelines, Azure Artifacts and Azure Test Plans.

	**GitHub** builds on top of Git to provide related services for coordinating work, reporting and discussing issues, providing documentation, and more.

	**GitHub Actions** enables workflow automation with triggers for many lifecycle events. One such example would be automating a CI/CD toolchain. A _toolchain_ is a combination of software tools that aid in the delivery, development, and management of software applications throughout a system's development lifecycle. The output of one tool in the toolchain is the input of the next tool in the toolchain. Typical tool functions range from performing automated dependency updates to building and configuring the software, delivering the build artifacts to various locations, testing, and so on.

	**Azure DevTest Labs** provides an automated means of managing the process of building, setting up, and tearing down virtual machines (VMs) that contain builds of your software projects. This way, developers and testers can perform tests across a variety of environments and builds. And this capability isn't limited to VMs. Anything you can deploy in Azure via an ARM template can be provisioned through DevTest Labs. Provisioning pre-created lab environments with their required configurations and tools already installed is a huge time saver for quality assurance professionals and developers.

### Describe Azure management tools

- **_describe the functionality and usage of the Azure Portal, Azure PowerShell, Azure CLI, Cloud Shell, and Azure Mobile App_**

	By using the **Azure Portal**, a web-based user interface, you can access virtually every feature of Azure. The Azure portal provides a friendly, graphical UI to view all the services you're using, create new services, configure your services, and view reports.

	**Azure PowerShell** is a shell with which developers and DevOps and IT professionals can execute commands called cmdlets (pronounced command-lets). These commands call the Azure Rest API to perform every possible management task in Azure. Cmdlets can be executed independently or combined into a script file and executed together to orchestrate:
	- The routine setup, teardown, and maintenance of a single resource or multiple connected resources.
	- The deployment of an entire infrastructure, which might contain dozens or hundreds of resources, from imperative code.

	The **Azure CLI** command-line interface is an executable program with which a developer, DevOps professional, or IT professional can execute commands in Bash. The commands call the Azure Rest API to perform every possible management task in Azure. You can run the commands independently or combined into a script and executed together for the routine setup, teardown, and maintenance of a single resource or an entire environment.

	In many respects, the Azure CLI is almost identical to Azure PowerShell in what you can do with it. Both run on Windows, Linux, and Mac, and can be accessed in a web browser via **Cloud Shell**.

	The **Azure Mobile App** provides iOS and Android access to your Azure resources when you're away from your computer. With it, you can:
	- Monitor the health and status of your Azure resources.
	- Check for alerts, quickly diagnose and fix issues, and restart a web app or virtual machine (VM).
	- Run the Azure CLI or Azure PowerShell commands to manage your Azure resources.

- **_describe the functionality and usage of Azure Advisor_**

	**Azure Advisor** evaluates your Azure resources and makes recommendations to help improve reliability, security, and performance, achieve operational excellence, and reduce costs. The recommendations are divided into five categories:
	- Reliability: Used to ensure and improve the continuity of your business-critical applications.
	- Security: Used to detect threats and vulnerabilities that might lead to security breaches.
	- Performance: Used to improve the speed of your applications.
	- Cost: Used to optimize and reduce your overall Azure spending.
	- Operational Excellence: Used to help you achieve process and workflow efficiency, resource manageability, and deployment best practices.

- **_describe the functionality and usage of Azure Resource Manager (ARM) templates_**

	By using **Azure Resource Manager** templates (ARM templates), you can describe the resources you want to use in a declarative JSON format. The benefit is that the entire ARM template is verified before any code is executed to ensure that the resources will be created and connected correctly. The template then orchestrates the creation of those resources in parallel.

- **_describe the functionality and usage of Azure Monitor_**

	**Azure Monitor** is a platform for collecting, analyzing, visualizing, and potentially taking action based on the metric and logging data from your entire Azure and on-premises environment.

- **_describe the functionality and usage of Azure Service Health_**

	**Azure Service Health** provides a personalized view of the health of the Azure services, regions, and resources you rely on. It displays both major and smaller, localized issues that affect you. After an outage, Service Health provides official incident reports, called root cause analyses (RCAs), which you can share with stakeholders.

	Service Health helps you keep an eye on several event types:
	- service issues
	- planned maintenance
	- health advisories (issues that require you to act to avoid service interruption, including service retirements and breaking changes)

## 	Describe general security and network security features (10-15%)

### Describe Azure security features

- **_describe basic features of Azure Security Center, including policy compliance, security alerts, secure score, and resource hygiene_**

	**Azure Security Center** is a monitoring service that provides visibility of your security posture across all of your services, both on Azure and on-premises. The term security posture refers to cybersecurity policies and controls, as well as how well you can predict, prevent, and respond to security threats.

	Security Center includes advanced cloud defense capabilities for virtual machines, network security, and file integrity:
	- Just-in-time VM access
	- Adaptive application controls
	- Adaptive network hardening
	- File integrity monitoring	

	**Secure score** is a measurement of an organization's security posture. Secure score is based on security controls, or groups of related security recommendations. Your score is based on the percentage of security controls that you satisfy.

	Security Center can be used to get a centralized view of all of its **security alerts**. From there, the company can dismiss false alerts, investigate them further, remediate alerts manually, or use an automated response with a workflow automation.

	In the **Resource security hygiene** section, one can see the health of its resources from a security perspective. To help prioritize remediation actions, recommendations are categorized as low, medium, and high.

- **_describe the functionality and usage of Key Vault_**

	**Azure Key Vault** is a centralized cloud service for storing an application's secrets in a single, central location. It provides secure access to sensitive information by providing access control and logging capabilities.

	Azure Key Vault can help you:
	- Manage secrets
	- Manage encryption keys
	- Manage SSL/TLS certificates
	- Store secrets backed by hardware security modules (HSMs)

	The benefits of using Key Vault include:
	- Centralized application secrets
	- Securely stored secrets and keys
	- Access monitoring and access control
	- Simplified administration of application secrets
	- Integration with other Azure services

- **_describe the functionality and usage of Azure Sentinel_**

	Security management on a large scale can benefit from a dedicated security information and event management (SIEM) system. A SIEM system aggregates security data from many different sources (as long as those sources support an open-standard logging format). It also provides capabilities for threat detection and response. **Azure Sentinel** is Microsoft's cloud-based SIEM system. It uses intelligent security analytics and threat analysis.

	Azure Sentinel enables you to:
	- Collect cloud data at scale - Collect data across all users, devices, applications, and infrastructure, both on-premises and from multiple clouds.
	- Detect previously undetected threats - Minimize false positives by using Microsoft's comprehensive analytics and threat intelligence.
	- Investigate threats with artificial intelligence - Examine suspicious activities at scale, tapping into years of cybersecurity experience from Microsoft.
	- Respond to incidents rapidly - Utilize built-in orchestration and automation of common tasks.

- **_describe the functionality and usage of Azure Dedicated Hosts_**

	Some organizations must follow regulatory compliance that requires them to be the only customer using the physical machine that hosts their virtual machines. **Azure Dedicated Host** provides dedicated physical servers to host your Azure VMs for Windows and Linux.

### Describe Azure network security

- **_describe the concept of defense in depth_**

	You can visualize **defense in depth** as a set of layers, with the data to be secured at the center:
	- The physical security layer is the first line of defense to protect computing hardware in the datacenter.
	- The identity and access layer controls access to infrastructure and change control.
	- The perimeter layer uses distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for users.
	- The network layer limits communication between resources through segmentation and access controls.
	- The compute layer secures access to virtual machines.
	- The application layer helps ensure that applications are secure and free of security vulnerabilities.
	- The data layer controls access to business and customer data that you need to protect.

	Your security posture is your organization's ability to protect from and respond to security threats. The common principles used to define a security posture are confidentiality, integrity, and availability, known collectively as CIA.

- **_describe the functionality and usage of Network Security Groups (NSG)_**

	A **network security group** enables you to filter network traffic to and from Azure resources within an Azure virtual network. You can think of NSGs like an internal firewall. An NSG can contain multiple inbound and outbound security rules that enable you to filter traffic to and from resources by source and destination IP address, port, and protocol.

- **_describe the functionality and usage of Azure Firewall_**

	**Azure Firewall** is a managed, cloud-based network security service that helps protect resources in your Azure virtual networks. A virtual network is similar to a traditional network that you'd operate in your own datacenter. It's a fundamental building block for your private network that enables virtual machines and other compute resources to securely communicate with each other, the internet, and on-premises networks.

	Azure Firewall is a stateful firewall. A stateful firewall analyzes the complete context of a network connection, not just an individual packet of network traffic. Azure Firewall features high availability and unrestricted cloud scalability.

	Azure Firewall provides many features, including:
	- Built-in high availability.
	- Unrestricted cloud scalability.
	- Inbound and outbound filtering rules.
	- Inbound Destination Network Address Translation (DNAT) support.
	- Azure Monitor logging.

	With Azure Firewall, you can configure:
	- Application rules that define fully qualified domain names (FQDNs) that can be accessed from a subnet.
	- Network rules that define source address, protocol, destination port, and destination address.
	- Network Address Translation (NAT) rules that define destination IP addresses and ports to translate inbound requests.

- **_describe the functionality and usage of Azure DDoS protection_**

	**Azure DDoS Protection** (Standard) helps protect your Azure resources from DDoS attacks.

	DDoS Protection provides these tiers:
	- The Basic service tier is automatically enabled for free as part of your Azure subscription. Always-on traffic monitoring and real-time mitigation of common network-level attacks provide the same defenses that Microsoft's online services use. 
	- The Standard service tier can help prevent: Volumetric attacks, Protocol attacks and Resource-layer (application-layer) attacks (only with web application firewall).

## Describe identity, governance, privacy, and compliance features (20-25%)

### Describe core Azure identity services

- **_explain the difference between authentication and authorization_**

	**Authentication** is the process of establishing the identity of a person or service that wants to access a resource.

	**Authorization** is the process of establishing what level of access an authenticated person or service has.

- **_define Azure Active Directory_**

	For on-premises environments, Active Directory running on Windows Server provides an identity and access management service that's managed by your own organization. **Azure AD** is Microsoft's cloud-based identity and access management service. With Azure AD, you control the identity accounts, but Microsoft ensures that the service is available globally.

- **_describe the functionality and usage of Azure Active Directory_**

	Azure AD provides services such as:
	- Authentication
	- Single sign-on
	- Application management
	- Device management

	Azure AD helps users access both external and internal resources. External resources might include Microsoft Office 365, the Azure portal, and thousands of other software as a service (SaaS) applications. Internal resources might include apps on your corporate network and intranet, along with any cloud applications developed within your organization.

- **_describe the functionality and usage of Conditional Access, Multi-Factor Authentication (MFA), and Single Sign-On (SSO)_**

	**Conditional Access** is a tool that Azure Active Directory uses to allow (or deny) access to resources based on identity signals. These signals include who the user is, where the user is, and what device the user is requesting access from.

	Azure AD **Multi-Factor Authentication** is a Microsoft service that provides multifactor authentication capabilities. Azure AD Multi-Factor Authentication enables users to choose an additional form of authentication during sign-in, such as a phone call or mobile app notification.

	**Single sign-on** enables a user to sign in one time and use that credential to access multiple resources and applications from different providers.

### Describe Azure governance features

- **_describe the functionality and usage of Role-Based Access Control (RBAC)_**

	Instead of defining the detailed access requirements for each individual, and then updating access requirements when new resources are created, Azure enables you to control access through **Azure role-based access control (Azure RBAC)**. Role-based access control is applied to a scope, which is a resource or set of resources that this access applies to. Scopes include: a management group (a collection of multiple subscriptions), a single subscription, a resource group or a single resource.

- **_describe the functionality and usage of resource locks_**

	A **resource lock** prevents resources from being accidentally deleted or changed. You can apply locks to a subscription, a resource group, or an individual resource. You can set the lock level to CanNotDelete or ReadOnly.

- **_describe the functionality and usage of tags_**

	Resource **tags** are another way to organize resources. Tags provide extra information, or metadata, about your resources. A resource tag consists of a name and a value. You can assign one or more tags to each Azure resource.

- **_describe the functionality and usage of Azure Policy_**

	**Azure Policy** is a service in Azure that enables you to create, assign, and manage policies that control or audit your resources. These policies enforce different rules and effects over your resource configurations so that those configurations stay compliant with corporate standards.

	Azure Policy enables you to define both individual policies and groups of related policies, known as initiatives. Azure Policy evaluates your resources and highlights resources that aren't compliant with the policies you've created. Azure Policy can also prevent noncompliant resources from being created. Azure Policy comes with a number of built-in policy and initiative definitions that you can use, under categories such as Storage, Networking, Compute, Security Center, and Monitoring.

- **_describe the functionality and usage of Azure Blueprints_**

	Instead of having to configure features like Azure Policy for each new subscription, with **Azure Blueprints** you can define a repeatable set of governance tools and standard Azure resources that your organization requires.

	Azure Blueprints orchestrates the deployment of various resource templates and other artifacts, such as:
	- Role assignments
	- Policy assignments
	- Azure Resource Manager templates
	- Resource groups

	Each component in the blueprint definition is known as an _artifact_.

- **_describe the Cloud Adoption Framework for Azure_**

	The **Cloud Adoption Framework for Azure** provides you with proven guidance to help with your cloud adoption journey. The Cloud Adoption Framework helps you create and implement the business and technology strategies needed to succeed in the cloud.

	The Cloud Adoption Framework consists of tools, documentation, and proven practices. The Cloud Adoption Framework includes these stages:
	- Define your strategy.
	- Make a plan.
	- Ready your organization.
	- Adopt the cloud.
	- Govern and manage your cloud environments.

### Describe privacy and compliance resources

## Describe Azure cost management and Service Level Agreements (10-15%)

### Describe methods for planning and managing costs
### Describe Azure Service Level Agreements (SLAs) and service lifecycles