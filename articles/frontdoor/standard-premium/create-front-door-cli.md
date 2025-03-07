---
title: Create an Azure Front Door Standard/Premium with the Azure CLI
description: Learn how to create an Azure Front Door Standard/Premium (preview) with the Azure CLI. Use the Front Door to protect your web apps against vulnerabilities.
ms.topic: sample
author: duau
ms.author: duau
ms.service: frontdoor
ms.date: 12/30/2021
ms.custom: devx-track-azurecli

---

# Quickstart: Create an Azure Front Door Standard/Premium - Azure CLI

In this quickstart, you'll learn how to create an Azure Front Door Standard/Premium profile using the Azure CLI. You'll create this profile using two Web Apps as your origin, and add a WAF security policy. You can then verify connectivity to your Web Apps using the Azure Front Door Standard/Premium frontend hostname.

> [!NOTE]
> This documentation is for Azure Front Door Standard/Premium (Preview). Looking for information on Azure Front Door? View [Azure Front Door Docs](../front-door-overview.md).

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment](../../../includes/azure-cli-prepare-your-environment.md)]

## Create a resource group

For this quickstart, you'll need two resource groups. One in *Central US* and the second in *East US*.

Run [az group create](/cli/azure/group#az_group_create) to create resource groups.

```azurecli
az group create \
    --name myRGFDCentral \
    --location centralus

az group create \
    --name myRGFDEast \
    --location eastus
```

## Create an Azure Front Door profile

Run [az afd profile create](/cli/azure/afd/profile#az_afd_profile_create) to create an Azure Front Door profile.

```azurecli
az afd profile create \
    --profile-name contosoafd \
    --resource-group myRGFDCentral \
    --sku Premium_AzureFrontDoor \
    --subscription mysubscription
```

## Create two instances of a web app

You need two instances of a web application that run in different Azure regions for this tutorial. Both the web application instances run in Active/Active mode, so either one can service traffic.

If you don't already have a web app, use the following script to set up two example web apps.

### Create app service plans

Before you can create the web apps you'll need two app service plans, one in *Central US* and the second in *East US*.

Run [az appservice plan create](/cli/azure/appservice/plan#az_appservice_plan_create&preserve-view=true) to create your app service plans.

```azurecli
az appservice plan create \
    --name myAppServicePlanCentralUS \
    --resource-group myRGFDCentral

az appservice plan create \
    --name myAppServicePlanEastUS \
    --resource-group myRGFDEast
```

### Create web apps

Run [az webapp create](/cli/azure/webapp#az_webapp_create&preserve-view=true) to create a web app in each of the app service plans in the previous step. Web app names have to be globally unique.

Run [az webapp list-runtimes](/cli/azure/webapp#az_webapp_create&preserve-view=true) to see a list of built-in stacks for web apps.

```azurecli
az webapp create \
    --name WebAppContoso-001 \
    --resource-group myRGFDCentral \
    --plan myAppServicePlanCentralUS \
    --runtime "DOTNETCORE|2.1"

az webapp create \
    --name WebAppContoso-002 \
    --resource-group myRGFDEast \
    --plan myAppServicePlanEastUS \
    --runtime "DOTNETCORE|2.1"
```

Make note of the default host name of each web app so you can define the backend addresses when you deploy the Front Door in the next step.

## Add an endpoint

Run [az afd endpoint create](/cli/azure/afd/endpoint#az_afd_endpoint_create) to create an endpoint in your profile. You can create multiple endpoints in your profile after finishing the create experience.

```azurecli
az afd endpoint create \
    --resource-group myRGFDCentral \
    --endpoint-name contoso-frontend \
    --profile-name contosoafd \
    --origin-response-timeout-seconds 60 \
    --enabled-state Enabled
```

## Create an origin group

Run [az afd origin-group create](/cli/azure/afd/origin-group#az_afd_origin_group_create) to create an origin group that contains your two web apps.

```azurecli
az afd origin-group create \
    --resource-group myRGFDCentral \
    --origin-group-name og1 \
    --profile-name contosoafd \
    --probe-request-type GET \
    --probe-protocol Http \
    --probe-interval-in-seconds 120 \
    --probe-path /test1/azure.txt \
    --sample-size 4 \
    --successful-samples-required 3 \
    --additional-latency-in-milliseconds 50
```

## Add an origin to the group

Run [az afd origin create](/cli/azure/afd/origin#az_afd_origin_create) to add an origin to your origin group.

```azurecli
az afd origin create \
    --resource-group myRGFDCentral \
    --host-name webappcontoso-1.azurewebsites.net
    --profile-name contosoafd \
    --origin-group-name og1 \
    --origin-name contoso1 \
    --origin-host-header webappcontoso-1.azurewebsites.net \
    --priority 1 \
    --weight 1000 \
    --enabled-state Enabled \
    --http-port 80 \
    --https-port 443
```

Repeat this step and add your second origin.

```azurecli
az afd origin create \
    --resource-group myRGFDCentral \
    --host-name webappcontoso-2.azurewebsites.net
    --profile-name contosoafd \
    --origin-group-name og1 \
    --origin-name contoso2 \
    --origin-host-header webappcontoso-2.azurewebsites.net \
    --priority 1 \
    --weight 1000 \
    --enabled-state Enabled \
    --http-port 80 \
    --https-port 443
```

## Add a route

Run [az afd route create](/cli/azure/afd/route#az_afd_route_create) to map your frontend endpoint to the origin group. This route forwards requests from the endpoint to *og1*.

```azurecli
az afd route create \
    --resource-group myRGFDCentral \
    --endpoint-name contoso-frontend \
    --profile-name contosoafd \
    --route-name route1 \
    --https-redirect Enabled \
    --origin-group og1 \
    --supported-protocols Https \
    --link-to-default-domain Enabled \
    --forwarding-protocol MatchRequest
```

## Create a new security policy

### Create a WAF policy

Run [az network front-door waf-policy create](/cli/azure/network/front-door/waf-policy#az_network_front_door_waf_policy_create) to create a WAF policy for one of your resource groups.

Create a new WAF policy for your Front Door. This example creates a policy that's enabled and in prevention mode.
    
```azurecli
az network front-door waf-policy create
    --name contosoWAF /
    --resource-group myRGFDCentral /
    --sku Premium_AzureFrontDoor
    --disabled false /
    --mode Prevention
```

> [!NOTE]
> If you select `Detection` mode, your WAF doesn't block any requests.

### Create the security policy

Run [az afd security-policy create](/cli/azure/afd/security-policy#az_afd_security_policy_create) to apply your WAF policy to the endpoint's default domain.

```azurecli
az afd security-policy create \
    --resource-group myRGFDCentral \
    --profile-name contosoafd \
    --security-policy-name contososecurity \
    --domains /subscriptions/mysubscription/resourcegroups/myRGFDCentral/providers/Microsoft.Cdn/profiles/contosoafd/afdEndpoints/contoso-frontend.z01.azurefd.net \
    --waf-policy /subscriptions/mysubscription/resourcegroups/myRGFDCentral/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/contosoWAF
```

## Verify Azure Front Door

When you create the Azure Front Door Standard/Premium profile, it takes a few minutes for the configuration to be deployed globally. Once completed, you can access the frontend host you created. In a browser, go to `contoso-frontend.z01.azurefd.net`. Your request will automatically get routed to the nearest server from the specified servers in the origin group.

To test instant global failover, we'll use the following steps:

1. Open a browser, as described above, and go to the frontend address: `contoso-frontend.azurefd.net`.

2. In the Azure portal, search for and select *App services*. Scroll down to find one of your web apps, **WebAppContoso-1** in this example.

3. Select your web app, and then select **Stop**, and **Yes** to verify.

4. Refresh your browser. You should see the same information page.

   >[!TIP]
   >There is a little bit of delay for these actions. You might need to refresh again.

5. Find the other web app, and stop it as well.

6. Refresh your browser. This time, you should see an error message.

    :::image type="content" source="../media/create-front-door-portal/web-app-stopped-message.png" alt-text="Both instances of the web app stopped":::

## Clean up resources

When you don't need the resources for the Front Door, delete both resource groups. Deleting the resource groups also deletes the Front Door and all its related resources.

Run [az group delete](/cli/azure/group#az_group_delete&preserve-view=true):

```azurecli
az group delete \
    --name myRGFDCentral

az group delete \
    --name myRGFDEast
```
