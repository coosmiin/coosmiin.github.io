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