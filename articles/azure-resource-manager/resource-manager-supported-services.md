---
title: aaaAzure provedores de recursos e tipos de recurso | Microsoft Docs
description: "Descreve os provedores de recursos Olá que dão suporte ao Gerenciador de recursos, esquemas e as versões de API disponíveis e regiões de saudação que podem hospedar recursos hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="e7d65-103">Provedores e tipos de recursos</span><span class="sxs-lookup"><span data-stu-id="e7d65-103">Resource providers and types</span></span>

<span data-ttu-id="e7d65-104">Ao implantar os recursos, você precisa frequentemente tooretrieve informações sobre provedores de recursos hello e tipos.</span><span class="sxs-lookup"><span data-stu-id="e7d65-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="e7d65-105">Neste artigo, você aprende a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-105">In this article, you learn to:</span></span>

* <span data-ttu-id="e7d65-106">Exibir todos os provedores de recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="e7d65-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="e7d65-107">Verificar o status do registro de um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="e7d65-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="e7d65-108">Registrar um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="e7d65-108">Register a resource provider</span></span>
* <span data-ttu-id="e7d65-109">Exibir os tipos de recurso para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="e7d65-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="e7d65-110">Exibir localizações válidas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="e7d65-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="e7d65-111">Exibir versões de API válidas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="e7d65-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="e7d65-112">Você pode executar essas etapas através do portal hello, PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d65-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="e7d65-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-113">PowerShell</span></span>

<span data-ttu-id="e7d65-114">toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, usam:</span><span class="sxs-lookup"><span data-stu-id="e7d65-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="e7d65-115">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="e7d65-116">Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e7d65-117">escopo de saudação para o registro é sempre assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e7d65-118">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="e7d65-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e7d65-119">No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7d65-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e7d65-120">tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e7d65-121">Esta operação está incluída no hello Colaborador e funções de proprietário.</span><span class="sxs-lookup"><span data-stu-id="e7d65-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="e7d65-122">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="e7d65-123">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e7d65-124">informações de toosee para um provedor de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="e7d65-125">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="e7d65-126">tipos de recurso de saudação toosee para um provedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="e7d65-127">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="e7d65-128">versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e7d65-129">Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="e7d65-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="e7d65-130">tooget Olá API versões disponíveis para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="e7d65-131">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="e7d65-132">Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="e7d65-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e7d65-133">Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="e7d65-134">use tooget locais de saudação com suporte para um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="e7d65-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="e7d65-135">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="e7d65-136">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d65-136">Azure CLI</span></span>
<span data-ttu-id="e7d65-137">toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, usam:</span><span class="sxs-lookup"><span data-stu-id="e7d65-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="e7d65-138">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="e7d65-139">Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e7d65-140">escopo de saudação para o registro é sempre assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e7d65-141">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="e7d65-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e7d65-142">No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7d65-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e7d65-143">tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e7d65-144">Esta operação está incluída no hello Colaborador e funções de proprietário.</span><span class="sxs-lookup"><span data-stu-id="e7d65-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="e7d65-145">Que retorna uma mensagem de que o registro está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e7d65-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="e7d65-146">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e7d65-147">informações de toosee para um provedor de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="e7d65-148">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="e7d65-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="e7d65-149">tipos de recurso de saudação toosee para um provedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="e7d65-150">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="e7d65-151">versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e7d65-152">Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="e7d65-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="e7d65-153">tooget Olá API versões disponíveis para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="e7d65-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="e7d65-154">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="e7d65-155">Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="e7d65-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e7d65-156">Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="e7d65-157">use tooget locais de saudação com suporte para um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="e7d65-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="e7d65-158">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="e7d65-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="e7d65-159">Portal</span><span class="sxs-lookup"><span data-stu-id="e7d65-159">Portal</span></span>

<span data-ttu-id="e7d65-160">toosee todos os provedores de recursos no Azure e o status de registro Olá para sua assinatura, selecione **assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="e7d65-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![selecionar assinaturas](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="e7d65-162">Escolha Olá tooview de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-162">Choose hello subscription tooview.</span></span>

![especificar a assinatura](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="e7d65-164">Selecione **provedores de recursos** e exiba a lista de saudação de provedores de recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e7d65-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![mostrar provedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="e7d65-166">Registrando um provedor de recursos configura toowork sua assinatura com o provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e7d65-167">escopo de saudação para o registro é sempre assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e7d65-168">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="e7d65-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e7d65-169">No entanto, talvez seja necessário toomanually registrar alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7d65-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e7d65-170">tooregister um provedor de recursos, você deve ter a saudação de tooperform permissão `/register/action` operação para o provedor de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e7d65-171">Esta operação está incluída no hello Colaborador e funções de proprietário.</span><span class="sxs-lookup"><span data-stu-id="e7d65-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="e7d65-172">tooregister um provedor de recursos, selecione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="e7d65-172">tooregister a resource provider, select **Register**.</span></span>

![registrar provedor de recursos](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="e7d65-174">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e7d65-175">informações de toosee para um provedor de recurso específico, selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="e7d65-175">toosee information for a particular resource provider, select **More services**.</span></span>

![selecionar mais serviços](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="e7d65-177">Procurar **Gerenciador de recursos** e selecioná-lo entre as opções disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![selecionar resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="e7d65-179">Selecione **Provedores**.</span><span class="sxs-lookup"><span data-stu-id="e7d65-179">Select **Providers**.</span></span>

![Selecionar provedores](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="e7d65-181">Recursos e o provedor de recursos Olá selecione tipo que você deseja tooview.</span><span class="sxs-lookup"><span data-stu-id="e7d65-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Selecionar tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="e7d65-183">Gerenciador de recursos tem suporte em todas as regiões, mas os recursos de saudação que implantar talvez não tenha suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="e7d65-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e7d65-184">Além disso, pode haver limitações que impedem o uso de algumas regiões que dão suporte ao recurso de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d65-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="e7d65-185">Gerenciador de recursos de saudação exibe locais válidos para o tipo de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Mostrar localizações](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="e7d65-187">versão da API Olá corresponde versão tooa de operações da API REST que são lançadas pelo provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d65-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e7d65-188">Como um provedor de recursos permite que os novos recursos, ele lança uma nova versão de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="e7d65-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="e7d65-189">Gerenciador de recursos de saudação exibe as versões de API válidas para o tipo de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="e7d65-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![Mostrar versões de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="e7d65-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7d65-191">Next steps</span></span>
* <span data-ttu-id="e7d65-192">toolearn sobre como criar modelos do Gerenciador de recursos, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e7d65-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e7d65-193">toolearn sobre a implantação de recursos, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e7d65-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="e7d65-194">operações de saudação tooview para um provedor de recursos, consulte [API REST do Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="e7d65-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

