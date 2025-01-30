[![Linkedin](https://img.shields.io/static/v1.svg?logo=linkedin&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=Linkedin&message=Public)](https://www.linkedin.com/in/eric-ricielle-2aa1ba237/) [![Elestio examples](https://img.shields.io/static/v1.svg?logo=github&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=github&message=open%20source)](https://github.com/TucanoWeb) [![Whatsapp](https://img.shields.io/static/v1.svg?logo=whatsapp&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=Whatsapp&message=Tirar%20Dúvidas)](https://api.whatsapp.com/send?phone=5531992936042)

# Demonstration of Azure API Management service

Project made for one of my students on Azure Platform.

# Get Starter

## Install Dependencies

In the root of the each project, run the command:

```bash
npm install
```

## Create Resource Group

ON AZURE PLATFORM:

- Create the Resource Group;
- Create a API management resource;
- Create Storage Account;
- Create a Function App based in Consume. In Storage tab, select the Storage Account created previously. On Network tab, select Off in the Enable public access option (the access will be throught API management proxy)

Copy the connection string of the Storage Account.

## Run Project - api_function

In the root of the project:

- Paste connection string into the file local.settings.json_example and rename the file to local.setting.json

Run the command:

```bash
az login
func azure functionapp publish <name_function_resource_created>
```

## Security configurations - link your function with API Management resource

- Go to API Management resource created > APIs > APIs > Create from Azure Resource > Function App. Select the function app created and published previously
- After API created, select the respective API and click on the Settings tab. In products, select "Starter" (or create a new product). In subscription, check the "subscription required" checkbox and change the name of header name field to name that you want (ex. x-subscription-key)
- On the API Maganement service, click in API's > Subscriptions and copy the primary key of the product: starter (or created previously) scope
- Go to APIs > APIs > All APIs > <created api> > <select the route created> > test tab. Insert the information necessary to test. You'll see that the test return error, because it's necessary allow the respective IP in the function app. In the header field returned in the error, copy the IP;
- Go to respective Function APP > Settings > Networking > Inbound traffic configuration > Public network access > disabled. Change the option to Enabled from select virtual networks n IP addresses. Add the respective IP copied from return of the requisiton made in test on api management.
- Now, you're able of make requisitions through the API Management using the proxy of the resource. The function app don't is accessible directly, but is accessibly through api management requisition.
