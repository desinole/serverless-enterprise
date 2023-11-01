

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

