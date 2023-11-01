# Beyond Quickstarts: Enterprise Challenges and Solutions for Azure Serverless
You have heard of the limitless possibilities of serverless. But what happens when you have to ... ummm ... limit your serverless resources? Welcome to enterprise environments where anything that can, shall be limited, and in most cases for valid reasons too. Join us for an entertaining talk that will take you beyond the typical quickstart serverless samples and into the real world of deploying Azure serverless technologies in enterprise environments. We'll share valuable lessons learned, exploring everything from scaling restrictions to private networks to handling managed resources and connections. Our focus will be on popular Azure resources like Functions and Logic Apps, but we'll touch on a variety of other Azure services as well. By the end of this talk, you'll have a newfound appreciation for the practical considerations involved in successful enterprise deployments of serverless technologies. 

1. What does an app created with quickstart sample look like?
2. What are some changes required for enterprise?
    - function apps and logic app on app services
    - no clear text connection strings
    - heavy use of key vault
    - private network and private endpoints
3. What are some issues with function apps running on app plans and in private networks
    - number of instances
    - function fit per instance
5. Logic Apps and connectors
6. Other services
    - Storage
    - CosmosDB
    - ACR
  

Consumption v Premium v Dedicated

Cold start and pre-warming

Instances and fit

Private networks, subnets, planning for instances, endpoints

Connecting to PaaS service like storage, SQL, CosmosDB

Logic App Connectors


### Difference between premium v dedicated plan

The **Premium Plan** and the **Dedicated (App Service) Plan** are two different hosting plans offered by Azure for running your applications, including Azure Functions. Here are some key differences between them:

1. **Compute Resources**: Both plans run on dedicated Virtual Machine instances¹³. However, the Premium Plan guarantees machines with faster processors, SSD storage, and memory-optimized options¹.

2. **Scaling**: The Premium Plan and the Dedicated Plan both support autoscaling up to 100 entities². However, in the Dedicated Plan, you need to manually configure the scaling⁴, while the Premium Plan scales out/in automatically based on the number of incoming events⁴.

3. **Virtual Network Integration**: In the Premium Plan, Virtual Network (VNet) Integration is regional². In contrast, both Regional and Gateway VNet Integrations are allowed in the Dedicated Plan².

4. **Pre-warmed Instances**: The Premium Plan always has pre-warmed instances². In the Dedicated Plan, you need to configure the App Service Plan to have pre-warmed instances².

5. **Pricing**: The pricing for the Premium Plan is calculated in terms of consumption of core units and memory across instances in terms of seconds². The invoice billing comes in terms of monthly usage².

Remember, the choice between these two plans depends on your specific needs and requirements. It's always a good idea to understand the features and limitations of each plan before making a decision.

(1) App Service plans - Azure App Service | Microsoft Learn. https://learn.microsoft.com/en-us/azure/app-service/overview-hosting-plans.
(2) App Service Pricing | Microsoft Azure. https://azure.microsoft.com/en-us/pricing/details/app-service/windows/.
(3) What the difference between Premium And Dedicated Plans for Azure .... https://stackoverflow.com/questions/75632652/what-the-difference-between-premium-and-dedicated-plans-for-azure-functions.
(4) Azure Functions Host Instance vs VM Instance - Stack Overflow. https://stackoverflow.com/questions/62730371/azure-functions-host-instance-vs-vm-instance.

### what are the pros and cons of premium and dedicated plans compared to consumption plans

**Premium Plan**
*Pros*⁴²:
1. **Avoids Cold Starts**: The Premium Plan provides pre-warmed instances, eliminating the delay after being idle.
2. **Virtual Network Connectivity**: This plan allows for virtual network connectivity.
3. **Longer Runtime Durations**: Functions can have longer execution times.
4. **Choice of Instance Sizes**: Offers a variety of instance sizes to choose from.
5. **More Predictable Pricing**: Compared to the Consumption Plan, the pricing is more predictable.
6. **High-Density App Allocation**: Allows for high-density app allocation for plans with multiple function apps.

*Cons*¹:
1. **Cost**: The Premium Plan can be more expensive than the Consumption Plan, especially for sporadic workloads.
2. **Resource Utilization**: If your functions are not continuously or nearly continuously running, you may not fully utilize the always-on, pre-warmed instances.

**Dedicated (App Service) Plan**
*Pros*²:
1. **Reuse of Compute Resources**: If you have existing, underutilized VMs running other App Service instances, you can reuse those compute resources.
2. **Custom Image Support**: Allows you to provide a custom image on which to run your functions.

*Cons*¹:
1. **Cost**: The Dedicated Plan can be more expensive than the Consumption Plan, especially if your workload is not constant.
2. **Manual Scaling**: You need to manually configure the scaling, unlike in the Consumption and Premium Plans where scaling is automatic.

Remember, the choice between these plans depends on your specific needs and requirements. It's always a good idea to understand the features and limitations of each plan before making a decision.

(1) Azure Functions Premium plan | Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-functions/functions-premium-plan.
(2) Azure Functions scale and hosting | Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale.
(3) Azure Consumption vs Dedicated Billing Model - Serverless360. https://www.serverless360.com/blog/consumption-vs-dedicated-billing-models.
(4) How to select the most suitable Hosting Plan for Azure ... - Medium. https://sahangunathilaka.medium.com/how-to-select-the-most-suitable-hosting-plan-for-azure-function-app-deployment-8896f0a63a6a.

### What is high-density app allocation?

High-Density App Allocation is a feature in Azure Functions, particularly useful in the Premium Plan, that allows multiple function apps to be deployed to the same plan². Here are some key details:

1. **Per-App Scaling**: This feature enables per-app scaling at the App Service plan level, allowing an app to scale independently from the App Service plan that hosts it¹. For example, an App Service plan can be scaled to 10 instances, but an app can be set to use only five¹.

2. **Allocation Approach**: Apps are allocated to available App Service plans using a best-effort approach for an even distribution across instances¹. While an even distribution is not guaranteed, the platform ensures that two instances of the same app will not be hosted on the same App Service plan instance¹.

3. **Rebalancing**: Applications are rebalanced only when instances are added or removed from the App Service plan¹.

4. **Configuration**: You can configure per-app scaling using PowerShell or Azure Resource Manager¹. At the app level, you can configure the number of instances the app can use in the App Service plan¹.

Remember, these are general recommendations and the optimal configuration may vary based on your specific use case and workload. It's always a good idea to monitor the performance of your function apps and adjust settings as necessary.

(1) Azure Functions Premium plan | Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-functions/functions-premium-plan.
(2) Per-app scaling for high-density hosting - Azure App Service. https://learn.microsoft.com/en-us/azure/app-service/manage-scale-per-app.
(3) Azure App Service and Azure Functions considerations for multitenancy .... https://learn.microsoft.com/en-us/azure/architecture/guide/multitenant/service/app-service.
