### Private Endpoint

Lets you connect privately to a resource i.e only within a private network
Function Apps/Logic Apps hosted on Premium and App Service plans can use this
DNS should resolve to private IP address (Azure DNS private zones, own DNS Server or private zones)
Private end point are for incoming traffic only

### VNET Integration:

Virtual network integration allows your function app to access resources inside a virtual network. 
Two types
1. Dedicated computing price tiers (Premium, standard)
2. ASE deploys directly into the vnet

vnet integration is used in dedicated tier

Outbound traffic only into vnet

1. Regional vnet integration: when you connect to virtual networks in the same region, you should have a dedicated subnet in the vnet you're integrating with
2. Gateway-required vnet integration: When you connect to vnnets in other regions or classic vnet, target vnet needs gateway

✅ TCP and UDP

❌ drive mounting, AD join, NetBios

If Route All is disabled, (long story short) Internet access may fail.

Only one VNET integration per APp Service Plan - you can have multiple Function Apps in an App Service Plan but they would share one subnet
requires an unused subnet that's a /28 or larger

###### How VNE Integration subnet size impacts scaling

App instances require 2 IPs for swapping during scale up or scale down. Hence, subnet should not be less than max instances * 2

| CIDR | Max available IPs | Max Instances |
| ----------- | ----------- | ----------- |
| /28 | 11 | 11/2 = 5 |
| /27 | 27 | 27/2 = 13 |
| /26 | 59 | 59/2 = 29 |
| /25 | 123 | 123/2 = 61 |
| /24 | 251 | 251/2 = 127 but only max 100 instances possible |

Subnet planning is a huge part of deploying serverless apps in enterprise

####### Virtual network triggers (non-HTTP)

Currently, you can use non-HTTP trigger functions from within a virtual network in one of two ways:
- Run your function app in a Premium plan and enable virtual network trigger support.
- Run your function app in an App Service plan or App Service Environment.

When you run a Premium plan, you can connect non-HTTP trigger functions to services that run inside a virtual network. To do this, you must enable virtual network trigger support for your function app. The Runtime Scale Monitoring setting is found in the Azure portal under Configuration > Function runtime settings.

following non-HTTP trigger types are supported
- Storage
- Event Hubs
- Service Bus
- Cosmos DB
- Durable Task

You can use other triggers but they will not scale dynamically and won't scale beyond pre-warmed instance limit.


Front Door for incoming traffic
