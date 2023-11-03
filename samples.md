

Simple one with consumption plan
Need sql servers

[Simple example](https://github.com/desinole/azure-sql-binding-func-dotnet-todo) running a function against sql

Run locally ```func start```
need to fill SqlConnectionString and ToDoUri something like http://localhost:7071/api/ToDo

simple api

run and show some API functions

show deployed version on consumption function
need to fill SqlConnectionString and ToDoUri something like https://funtionname.azurewebsites.net/api/ToDo

But connection string in clear text
Let's store it in a key vault and pull from there

TO refer secret in key vault app config
1. Grab secret identifier
2. Replace clear text connection string with ```@Microsoft.KeyVault(SecretUri=secret identifier from step 1)```

Check app setting, it will show MSI not enabled
Enabled MSI and provide secret user RBAC connection, it should work now

Let's talk about MSI versus User Managed Identity

So that's step 1 to securing your app in the enterprise

Now enterprises will require your data to be private
How do we do that? 
Let's see if we can put our function app in a private network

Function app consumption can accept connections from private endpoints but the worker nodes are not in a private network. 
Similar to being connected to a gated community but not being part of one.

So let's look at some options for hosting function app worker nodes inside a private network
Premium and Dedicated plan are some common options but ASE, Container apps and Kubernetes (ARC) [hosting options](https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale)
We're picking Premium for following reasons - list reasons

This is what a function in an premium plan looks like 
- architectural diagram
- private endpoint and vnet integration
- managed identity
- number of instances per subnet planning

Talk about app inisghts and what to monitor

Talk about high-density app allocation

talk about zone redundancy
function auth
Talk about cost
Learn about running .NET code on functions (Java, NodeJS, Python)
Logging and monitoring costs a lot if you log informational, should not exceed 15% of budget

Secrets always in Key vault
where possible use idenity over connection string


Talk about logicapps and connectors (hosted versus managed)

