### Function Keys

HTTP triggered functions unless set to ```anonymous```, requests must include API access key in request.

Sameple call: https://funcname.azurewebsites.net/api/HttpTrigger1?code=alphanumericstring

| Action |	Scope |	Valid keys |
|--------|--------|------------|
| Execute a function |	Specific function |	Function |
| Execute a function |	Any function |	Function or host |
| Call an admin endpoint |	Function app |	Host (master only) |
| Call Durable Task extension APIs |	Function app |	System |
| Call an extension-specific Webhook | (internal)	Function app |	system |

<img src="./img/functionkeys.png" height="200px" />

By default, keys are stored in a Blob storage container in the account provided by the ```AzureWebJobsStorage``` setting. You can use the ```AzureWebJobsSecretStorageType``` setting to override this behavior and store keys in a different location. For instance, changing ```AzureWebJobsSecretStorageType``` to ```keyvault```, keys are stored in a key vault instance set by ```AzureWebJobsSecretStorageKeyVaultName```.

#### Enable App Service Authentication/Authorization

- Use Microsoft Entra ID and several third-party identity providers to authenticate clients
- Implement custom authorization rules for your functions
- work with user information from your function code.

You can also offload authentication to APIM

### Permissions

- Contributor role is required to perform most function app-level tasks
- Contributor role along with the Monitoring Reader permission to be able to view log data in Application Insights
- Only the Owner role can delete a function app

### Organizing functions with Function App

A function app can have multiple functions. One way to group them is to organize functions with same permissions with same function app.
Important topic because developer teams may organize functions by business logic

### Managed Identities

A system-assigned identity is tied to your application and is deleted if your app is deleted. An app can only have one system-assigned identity.
A user-assigned identity is a standalone Azure resource that can be assigned to your app. An app can have multiple user-assigned identities.

Often used instead of usernames and passwords

### Restrict CORS access

Defined at function app level
Allows web apps in another domain to request HTTP endpoints

### Secrets

1. App Settings: Key Value pair, stored in AzureWebStorage but can be changed to Key Vault
2. Key Vault: Will be required for connection strings, API keys and such. Can be pulled into app settings with key valut reference

### Disable FTP
By default, each function app has an FTP endpoint enabled. The FTP endpoint is accessed using deployment credentials.
FTP isn't recommended for deploying your function code. FTP deployments are manual, and they require you to synchronize triggers.

### Secure the scm endpoint
Every function app has a corresponding scm service endpoint that used by the Advanced Tools (Kudu) service for deployments and other App Service site extensions. The scm endpoint for a function app is always a URL in the form https://<FUNCTION_APP_NAME.scm.azurewebsites.net>. When you use network isolation to secure your functions, you must also account for this endpoint.

