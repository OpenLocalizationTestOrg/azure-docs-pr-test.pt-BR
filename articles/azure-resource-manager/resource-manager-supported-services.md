---
title: Provedores de recursos e tipos de recursos do Azure | Microsoft Docs
description: "Descreve os provedores de recursos que oferecem suporte ao Gerenciador de Recursos, aos respectivos esquemas e versões de API disponíveis, bem como às regiões que podem hospedar os recursos."
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="38e05-103">Provedores e tipos de recursos</span><span class="sxs-lookup"><span data-stu-id="38e05-103">Resource providers and types</span></span>

<span data-ttu-id="38e05-104">Ao implantar recursos, com frequência você precisa recuperar informações sobre os provedores e tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="38e05-105">Neste artigo, você aprende a:</span><span class="sxs-lookup"><span data-stu-id="38e05-105">In this article, you learn to:</span></span>

* <span data-ttu-id="38e05-106">Exibir todos os provedores de recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="38e05-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="38e05-107">Verificar o status do registro de um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="38e05-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="38e05-108">Registrar um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="38e05-108">Register a resource provider</span></span>
* <span data-ttu-id="38e05-109">Exibir os tipos de recurso para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="38e05-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="38e05-110">Exibir localizações válidas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="38e05-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="38e05-111">Exibir versões de API válidas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="38e05-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="38e05-112">Você pode executar essas etapas por meio do portal, do PowerShell ou da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="38e05-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="38e05-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38e05-113">PowerShell</span></span>

<span data-ttu-id="38e05-114">Para ver todos os provedores de recursos no Azure e o status do registro para a sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="38e05-115">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="38e05-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="38e05-116">O registro de um provedor de recursos configura sua assinatura para trabalhar com o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="38e05-117">O escopo de registro é sempre a assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="38e05-118">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="38e05-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="38e05-119">No entanto, talvez seja necessário registrar manualmente alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="38e05-120">Para registrar um provedor de recursos, você deve ter permissão para executar a operação do `/register/action` para o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="38e05-121">Esta operação está incluída nas funções de Colaborador e de Proprietário.</span><span class="sxs-lookup"><span data-stu-id="38e05-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="38e05-122">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="38e05-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="38e05-123">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="38e05-124">Para obter informações para um provedor de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="38e05-125">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="38e05-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="38e05-126">Para ver os tipos de recurso para um provedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="38e05-127">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="38e05-128">A versão disponível da API corresponde a uma versão das operações da API REST lançadas pelo provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="38e05-129">Conforme um provedor de recursos habilita novos recursos, ele lança uma nova versão da API REST.</span><span class="sxs-lookup"><span data-stu-id="38e05-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="38e05-130">Para obter versões de API disponíveis para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="38e05-131">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="38e05-132">O Gerenciador de Recursos tem suporte em todas as regiões, mas os recursos que você implanta talvez não tenham suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="38e05-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="38e05-133">Além disso, pode haver limitações em sua assinatura que impedem o uso de algumas regiões que oferecem suporte aos recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="38e05-134">Para obter as localizações com suporte para um tipo de recurso, use.</span><span class="sxs-lookup"><span data-stu-id="38e05-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="38e05-135">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="38e05-136">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="38e05-136">Azure CLI</span></span>
<span data-ttu-id="38e05-137">Para ver todos os provedores de recursos no Azure e o status do registro para a sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="38e05-138">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="38e05-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="38e05-139">O registro de um provedor de recursos configura sua assinatura para trabalhar com o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="38e05-140">O escopo de registro é sempre a assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="38e05-141">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="38e05-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="38e05-142">No entanto, talvez seja necessário registrar manualmente alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="38e05-143">Para registrar um provedor de recursos, você deve ter permissão para executar a operação do `/register/action` para o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="38e05-144">Esta operação está incluída nas funções de Colaborador e de Proprietário.</span><span class="sxs-lookup"><span data-stu-id="38e05-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="38e05-145">Que retorna uma mensagem de que o registro está em andamento.</span><span class="sxs-lookup"><span data-stu-id="38e05-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="38e05-146">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="38e05-147">Para obter informações para um provedor de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="38e05-148">Que retorna resultados semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="38e05-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="38e05-149">Para ver os tipos de recurso para um provedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="38e05-150">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="38e05-151">A versão disponível da API corresponde a uma versão das operações da API REST lançadas pelo provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="38e05-152">Conforme um provedor de recursos habilita novos recursos, ele lança uma nova versão da API REST.</span><span class="sxs-lookup"><span data-stu-id="38e05-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="38e05-153">Para obter versões de API disponíveis para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="38e05-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="38e05-154">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="38e05-155">O Gerenciador de Recursos tem suporte em todas as regiões, mas os recursos que você implanta talvez não tenham suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="38e05-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="38e05-156">Além disso, pode haver limitações em sua assinatura que impedem o uso de algumas regiões que oferecem suporte aos recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="38e05-157">Para obter as localizações com suporte para um tipo de recurso, use.</span><span class="sxs-lookup"><span data-stu-id="38e05-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="38e05-158">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="38e05-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="38e05-159">Portal</span><span class="sxs-lookup"><span data-stu-id="38e05-159">Portal</span></span>

<span data-ttu-id="38e05-160">Para ver todos os provedores de recursos no Azure e o status do registro para a sua assinatura, selecione **Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="38e05-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![selecionar assinaturas](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="38e05-162">Escolha a assinatura para exibir.</span><span class="sxs-lookup"><span data-stu-id="38e05-162">Choose the subscription to view.</span></span>

![especificar a assinatura](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="38e05-164">Selecione **Provedores de recursos** e exiba a lista de provedores de recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="38e05-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![mostrar provedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="38e05-166">O registro de um provedor de recursos configura sua assinatura para trabalhar com o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="38e05-167">O escopo de registro é sempre a assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="38e05-168">Por padrão, muitos provedores de recursos são automaticamente registrados.</span><span class="sxs-lookup"><span data-stu-id="38e05-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="38e05-169">No entanto, talvez seja necessário registrar manualmente alguns provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="38e05-170">Para registrar um provedor de recursos, você deve ter permissão para executar a operação do `/register/action` para o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="38e05-171">Esta operação está incluída nas funções de Colaborador e de Proprietário.</span><span class="sxs-lookup"><span data-stu-id="38e05-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="38e05-172">Para registrar um provedor de recursos, selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="38e05-172">To register a resource provider, select **Register**.</span></span>

![registrar provedor de recursos](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="38e05-174">Você não poderá cancelar o registro de um provedor de recursos enquanto ainda tiver tipos de recursos desse provedor de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="38e05-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="38e05-175">Para obter informações para um provedor de recursos específico, selecione **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="38e05-175">To see information for a particular resource provider, select **More services**.</span></span>

![selecionar mais serviços](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="38e05-177">Pesquise por **Resource Explorer** e selecione-o nas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="38e05-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![selecionar resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="38e05-179">Selecione **Provedores**.</span><span class="sxs-lookup"><span data-stu-id="38e05-179">Select **Providers**.</span></span>

![Selecionar provedores](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="38e05-181">Selecione o provedor de recursos e o tipo de recurso que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="38e05-181">Select the resource provider and resource type that you want to view.</span></span>

![Selecionar tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="38e05-183">O Gerenciador de Recursos tem suporte em todas as regiões, mas os recursos que você implanta talvez não tenham suporte em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="38e05-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="38e05-184">Além disso, pode haver limitações em sua assinatura que impedem o uso de algumas regiões que oferecem suporte aos recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="38e05-185">O Resource Explorer mostra localizações válidas para o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="38e05-185">The resource explorer displays valid locations for the resource type.</span></span>

![Mostrar localizações](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="38e05-187">A versão disponível da API corresponde a uma versão das operações da API REST lançadas pelo provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="38e05-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="38e05-188">Conforme um provedor de recursos habilita novos recursos, ele lança uma nova versão da API REST.</span><span class="sxs-lookup"><span data-stu-id="38e05-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="38e05-189">O Resource Explorer mostra versões de API válidas para o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="38e05-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Mostrar versões de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="38e05-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38e05-191">Next steps</span></span>
* <span data-ttu-id="38e05-192">Para saber mais sobre a criação de modelos do Gerenciador de Recursos, confira [Criando modelos do Gerenciador de Recursos do Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="38e05-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="38e05-193">Para saber mais sobre como implantar recursos, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="38e05-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="38e05-194">Para exibir as operações para um provedor de recursos, consulte [API REST do Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="38e05-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

