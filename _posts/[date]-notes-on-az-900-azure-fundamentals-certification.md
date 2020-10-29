---
title: "Notes on Microsoft Azure Fundamentals AZ-900 exam prerarations"
date: [date] +0200
categories: 
---

While learning for the [AZ-900 Microsoft Azure Fundamentals](https://docs.microsoft.com/en-us/learn/certifications/exams/az-900) exam, I thought it would be nice to track my progress by taking notes on various topics that I need to learn for the exam. My approach? Start from [exam skill outline](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE3VwUY), follow the [learning paths](https://docs.microsoft.com/en-us/learn/certifications/exams/az-900?tab=tab-learning-paths) and links suggested by Thomas Maurer in his [AZ-900 Study Guide](https://www.thomasmaurer.ch/2020/03/az-900-study-guide-microsoft-azure-fundamentals-2020).

## Describe Cloud Concepts (15-20%)

### Describe the benefits and considerations of using cloud services

- **_describe terms such as High Availability, Scalability, Elasticity, Agility, Fault Tolerance, and Disaster Recovery_**

	- **High availability** - _Never go down_ or the ability to keep services up and running for long periods of time, with very little downtime.
	- **Scalability** - _Grow baby, grow_ or the ability to increase or decrease resources for any given workload (**out** and **up**). 
	- **Elasticity** - _Free to grow_ or the ability to automatically or dynamically increase or decrease resources as needed.
	- **Agility** - _Are you quick enough?_ or the ability to react quickly. Cloud services can allocate and deallocate resources quickly.
	- **Fault Tolerance** - _Wounded? I won't die!_ or the ability to remain up and running even in the event of a component (or service) no longer functioning (typically via redundancy)
	- **Disaster Recovery** - _Shit will never hit the fan_ or the ability to recover from an event which has taken down a cloud service.

- **_describe the principles of economies of scale_**

	The concept of economies of scale is the ability to reduce costs and gain efficiency when operating at a larger scale in comparison to operating at a smaller scale.

- **_describe the differences between Capital Expenditure (CapEx) and Operational Expenditure (OpEx)_**

	There are two approaches to investment:
		
	- **Capital Expenditure (CapEx):** This is the up front spending of money on physical infrastructure, and then deducting that up front expense over time.
	- **Operational Expenditure (OpEx):** This is spending money on services or products now and being billed for them now. You can deduct this expense in the same year you spend it.

- **_describe the consumption-based model_**

	Cloud service providers operate on a consumption-based model, which means that end users only pay for the resources that they use.

### Describe the differences between Infrastructure-as-a-Service (IaaS), Platform-as-a-Service (PaaS) and Software-as-a-Service (SaaS)

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

- **_describe Software-as-a-Service (SaaS)_**

	Software as a Service (SaaS) is software that is centrally hosted and managed for the end customer. Characteristics: 

	- **Upfront costs**. Users have no upfront costs; they pay a subscription, typically on a monthly or annual basis.
	- **User ownership**. Users just use the application software; they are not responsible for any maintenance or management of that software.
	- **Cloud provider ownership**. The cloud provider is responsible for the provision, management, and maintenance of the application software.

- **_compare and contrast the three different service types_**

	&nbsp; | **Advantages** | **Disadvantages**
	-- | -- | -- 
	 **_IaaS_** | No CapEx, Agility, Consumption-based model, Skills, Cloud benefits, Flexibility | Management
	 **_PaaS_** | No CapEx, Agility, Consumption-based model, Skills, Cloud benefits, Productivity | Platform limitations
	 **_SaaS_** | No CapEx, Agility, Pay-as-you-go, Flexibility | Software limitations

### Describe the differences between Public, Private and Hybrid cloud models

- **_describe Public cloud_**

	A public cloud is owned by the cloud services provider (also known as a hosting provider). It provides resources and services to multiple organizations and users, who connect to the cloud service via a secure network connection, typically over the internet.

- **_describe Private cloud_**

	A private cloud is owned and operated by the organization that uses the resources from that cloud. They create a cloud environment in their own datacenter and provide self-service access to compute resources to users within their organization. The organization remains the owner, entirely responsible for the operation of the services they provide.

- **_describe Hybrid cloud_**

	A hybrid cloud combines both public and private clouds, allowing you to run your applications in the most appropriate location.

- **_compare and contrast the three different cloud models_**

	&nbsp; | **Advantages** | **Disadvantages**
	-- | -- | -- 
	 **_Public_** | No CapEx, Agility, Consumption-based model, Maintenance, Skills | Security, Compliance, Ownership, Specific scenarios
	 **_Private_** | Control, Security, Compliance, Specific scenarios | Upfront CapEx, Agility, Maintenance, Skills
	 **_Hybrid_** | Flexibility, Costs, Control, Security, Compliance, Specific scenarios | Upfront CapEx, Costs, Skills, Ease of management

## Describe Core Azure Services (30-35%)

### Describe the core Azure architectural components

- **_describe Regions_**

	Microsoft Azure is made up of datacenters located around the globe. These datacenters are organized and made available to end users by region. A region  is a geographical area on the planet containing at least one, but potentially multiple datacenters that are in close proximity and networked together with a low-latency network. Azure intelligently assigns and controls the resources within each region to ensure workloads are appropriately balanced.

- **_describe Availability Zones_**

	Availability zones  are physically separate locations within an Azure region that use availability sets to provide additional fault tolerance.

- **_describe Resource Groups_**

	A resource group is a unit of management for your resources in Azure. You can think of your resource group as a container that allows you to aggregate and manage all the resources required for your application in a single manageable unit. This allows you to manage the application collectively over its lifecycle, rather than manage components individually.

- **_describe Azure Resource Manager_**

	Azure Resource Manager  is a management layer in which resource groups and all the resources within it are created, configured, managed, and deleted. It provides a consistent management layer which allows you automate the deployment and configuration of resources using different automation and scripting tools, such as Microsoft Azure PowerShell, Azure Command-Line Interface (Azure CLI), Azure portal, REST API, and client SDKs.

- **_describe the benefits and usage of core Azure architectural components_**

	?

### Describe some of the core products available in Azure

- **_describe products available for Compute such as Virtual Machines, Virtual Machine Scale Sets, App Services, Azure Container Instances (ACI) and Azure Kubernetes Service (AKS)_**

	**Virtual Machines** (VMs) are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources.
	
	**Virtual machine scale sets** are an Azure compute resource that you can use to deploy and manage a set of identical VMs. With all VMs configured the same, virtual machine scale sets are designed to support true autoscale.

	With **App services**, you can quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform. You can meet rigorous performance, scalability, security, and compliance requirements while using a fully managed platform to perform infrastructure maintenance. App Services is a platform as a service (PaaS) offering.

	**Containers** are a virtualization environment. **Azure Container Instances (ACI)**  offers the fastest and simplest way to run a container in Azure without having to manage any virtual machines or adopt any additional services. It is a PaaS offering that allows you to upload your containers, which it will run for you. **Azure Kubernetes Service (AKS)** is a complete orchestration service for containers with distributed architectures and large volumes of containers. Orchestration is the task of automating and managing a large number of containers and how they interact.

	Azure Container Instances (ACI) and Azure Kubernetes Service (AKS)

- **_describe products available for Networking such as Virtual Network, Load Balancer, VPN Gateway, Application Gateway and Content Delivery Network_**

	**Azure Virtual Network** enables many types of Azure resources such as Azure VMs to securely communicate with each other, the internet, and on-premises networks. A virtual network is scoped to a single region; however, multiple virtual networks from different regions can be connected using virtual network peering. With Azure Virtual Network you can provide isolation, segmentation, communication with on-premises and cloud resources, routing and filtering of network traffic.

	**Azure Load Balancer** can provide scale for your applications and create high availability for your services. Load Balancer supports inbound and outbound scenarios, provides low latency and high throughput, and scales up to millions of flows for all Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) applications. You can use Load Balancer with incoming internet traffic, internal traffic across Azure services, port forwarding for specific traffic, or outbound connectivity for VMs in your virtual network.

	**A VPN gateway** is a specific type of virtual network gateway that is used to send encrypted traffic between an Azure Virtual Network and an on-premises location over the public internet. It provides a more secure connection from on-premises to Azure over the internet.

	**Azure Application Gateway** is a web traffic load balancer that enables you to manage traffic to your web applications. It is the connection through which users connect to your application. With Application Gateway you can route traffic based on source IP address and port to a destination IP address and port. You also can help protect a web application with a web application firewall, redirection, session affinity to keep a user on the same server, and many more configuration options.

	**A Content Delivery Network (CDN)** is a distributed network of servers that can efficiently deliver web content to users. It is a way to get content to users in their local region to minimize latency. CDN can be hosted in Azure or any other location.

- **_describe products available for Storage such as Blob Storage, Disk Storage, File Storage, and Archive Storage_**

	**Disk storage** provides disks for virtual machines, applications, and other services to access and use as they need, similar to how they would in on-premises scenarios. Disk storage allows data to be persistently stored and accessed from an attached virtual hard disk. The disks can be managed or unmanaged by Azure, and therefore managed and configured by the user.

	Azure **Blob Storage** is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data, such as text or binary data.

	**Azure Files** enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol. That means that multiple VMs can share the same files with both read and write access. You can also read the files using the REST interface or the storage client libraries.

	**Archive Storage** ?

- **_describe products available for Databases such as Cosmos DB, Azure SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL, Azure Database Migration service_**

	**Azure Cosmos DB** is a globally distributed database service that enables you to elastically and independently scale throughput and storage across any number of Azure's geographic regions. It supports schema-less data that lets you build highly responsive and Always On applications to support constantly changing data. You can use Cosmos DB to store data that is updated and maintained by users around the world. It makes it easy to build scalable, highly responsive applications at global scale.

	**Azure SQL Database** is a relational database as a service (DaaS) based on the latest stable version of Microsoft SQL Server database engine. SQL Database is a high-performance, reliable, fully managed and secure database that you can use to build data-driven applications and websites in the programming language of your choice without needing to manage infrastructure.

	**Azure Database for MySQL** ?

	**Azure Database for PostgreSQL** ?

	The **Azure Database Migration Service** is a fully managed service designed to enable seamless migrations from multiple database sources to Azure data platforms with minimal downtime (online migrations). The service uses the Microsoft Data Migration Assistant to generate assessment reports that provide recommendations to help guide you through required changes prior to performing a migration.

- **_describe the Azure Marketplace and its usage scenarios_**

	Azure Marketplace  is a service on Azure that helps connect end users with Microsoft partners, independent software vendors (ISVs), and start-ups that are offering their solutions and services, which are optimized to run on Azure. Azure Marketplace allows customers—mostly IT professionals and cloud developers—to find, try, purchase, and provision applications and services from hundreds of leading service providers, all certified to run on Azure. The solution catalog spans several industry categories, including but not limited to: open-source container platforms, virtual machine images, databases, application build and deployment software, developer tools, threat detection, and blockchain.

### Describe some of the solutions available on Azure

- **_describe Internet of Things (IoT) and products that are available for IoT on Azure such as IoT Hub and IoT Central_**

	**IoT Central** is a fully managed global IoT software as a service (SaaS) solution that makes it easy to connect, monitor, and manage your IoT assets at scale. No cloud expertise is required to use IoT Central. As a result, you can bring your connected products to market faster while staying focused on your customers.

	**Azure IoT Hub** is a managed service hosted in the cloud that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages. You can use Azure IoT Hub to build IoT solutions with reliable and secure communications between millions of IoT devices and a cloud-hosted solution backend. You can connect virtually any device to your IoT Hub. IoT Hub supports communications both from the device to the cloud and from the cloud to the device. It also supports multiple messaging patterns such as device-to-cloud telemetry, file upload from devices, and request-reply methods to control your devices from the cloud. IoT Hub monitoring helps you maintain the health of your solution by tracking events such as device creation, device failures, and device connections. IoT Hub's capabilities help you build scalable, full-featured IoT solutions such as managing industrial equipment used in manufacturing, tracking valuable assets in healthcare, and monitoring office building usage.

- **_describe Big Data and Analytics and products that are available for Big Data and Analytics such as Azure Synapse Analytics, HDInsight, and Azure Databricks_**

	**Azure Synapse Analytics** (formerly Azure SQL Data Warehouse) is a limitless analytics service that brings together enterprise data warehousing and big data analytics.

	**Azure HDInsight** is a fully managed, open-source analytics service for enterprises. It is a cloud service that makes it easier, faster, and more cost-effective to process massive amounts of data. HDInsight allows you to run popular open-source frameworks and create cluster types such as Apache Spark, Apache Hadoop, Apache Kafka, Apache HBase, Apache Storm, Machine Learning Services. HDInsight also supports a broad range of scenarios such as extraction, transformation, and loading (ETL); data warehousing; machine learning; and IoT.

	**Azure Databricks** is a fully managed, fast, easy and collaborative Apache® Spark™ based analytics platform optimized for Azure.

- **_describe Artificial Intelligence (AI) and products that are available for AI such as Azure Machine Learning Service and Studio_**

	**Artificial Intelligence**, in the context of cloud computing, is based around a broad range of services, the core of which is Machine Learning. Machine Learning is a data science technique that allows computers to use existing data to forecast future behaviors, outcomes, and trends. Using machine learning, computers learn without being explicitly programmed.

	**Azure Cognitive Services** are a collection of domain-specific pre-trained AI models that can be customized with your data. They are categorized broadly into vision, speech, language, and search.

	**The Azure Machine Learning service** provides a cloud-based environment you can use to develop, train, test, deploy, manage, and track machine learning models. It fully supports open-source technologies, so you can use tens of thousands of open-source Python packages with machine learning components such as TensorFlow and scikit-learn. Rich tools, such as Jupyter notebooks or the Visual Studio Code Tools for AI, make it easy to interactively explore data, transform it, and then develop, and test models. Azure Machine Learning service also includes features that automate model generation and tuning to help you create models with ease, efficiency, and accuracy.

- **_describe Serverless computing and Azure products that are available for serverless computing such as Azure Functions, Logic Apps, and Event Grid_**

- **_describe DevOps solutions available on Azure such as Azure DevOps and Azure DevTest Labs_**

- **_describe the benefits and outcomes of using Azure solutions_**

### Describe Azure management tools

- **_describe Azure tools such as Azure Portal, Azure PowerShell, Azure CLI and Cloud Shell_**

- **_describe Azure Advisor	 _**
