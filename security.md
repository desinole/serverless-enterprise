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

<img src="./img/functionkeys.png" />
