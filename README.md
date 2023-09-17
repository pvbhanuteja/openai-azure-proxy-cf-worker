# cf-openai-azure-proxy

Thanks to https://github.com/haibbo/cf-openai-azure-proxy most of the code is taken from there modified it to add embeddings support. 

> Most OpenAI clients do not support Azure OpenAI Service, but the application for Azure OpenAI Service is very simple, and it also provides free quotas. This script uses a free Cloudflare Worker as a proxy, allowing OpenAI-supported clients to directly use Azure OpenAI Service.

This script proxies requests to Azure OpenAI Service for OpenAI clients. The code deployment steps are as follows:

Register and log in to your Cloudflare account.
- Create a new Cloudflare Worker.
- Copy and paste cf-openai-azure-proxy.js into the Cloudflare Worker editor.
- Adjust the values of **resourceName** and deployment **mapper** by either direct modification or using environment variables..
- Save and deploy the Cloudflare Worker.
- (Optional) Explore cloudflare workers for custom domain settings

## Instructions
First obtain the resourceName and deployment mapper, and log in to the Azure portal:

<img width="777" src="https://user-images.githubusercontent.com/1295315/233124125-1ea95665-ffab-4b5c-a7ba-26f31f1bb0b3.png" alt="env" />

#### There are two ways to do this:
- Directly modify their values, such as:
```js
// The name of your Azure OpenAI Resource.
const resourceName="codegpt"

  const mapper:any = {
    'gpt-3.5-turbo': 'gpt3',
    'gpt-4': 'gpt4' 
  };
// Supports embeddings as well
```
Other map rules can be continued directly in this format.
- **OR** go to the Cloudflare Worker console, navigate to Workers script > Settings > Add variable under Environment Variables.

<img width="777" src="https://user-images.githubusercontent.com/1295315/233384224-aa6581f0-26a4-49cf-ae25-4dfb466143da.png" alt="env" />

## Client
Take https://github.com/Yidadaa/ChatGPT-Next-Web as an example: fill in the custom API domain name with the domain name:

<img width="339" src="https://raw.githubusercontent.com/pvbhanuteja/openai-azure-proxy-cf-worker/main/Screenshot%202023-09-17%20at%207.37.40%20PM.png" alt="opencat" />


QA:

- Do I need a server to use this?
  - This script runs on Cloudflare Worker and does not require a server or a bound card. It is free for up to 100,000 requests per day.
- Do I need my own domain name to use this?
  - No, it is not necessary. Just a free cloudflare account is sufficent



