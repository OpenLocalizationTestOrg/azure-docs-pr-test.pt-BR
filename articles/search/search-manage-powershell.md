---
title: aaaManage pesquisa do Azure com scripts do Powershell | Microsoft Docs
description: "Gerencie o serviço de Pesquisa do Azure com scripts do PowerShell. Criar ou atualizar um serviço da Pesquisa do Azure e gerenciar chaves de administração da Pesquisa do Azure"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="7fffa-104">Gerencie o serviço de Pesquisa do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fffa-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fffa-105">Portal</span><span class="sxs-lookup"><span data-stu-id="7fffa-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="7fffa-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fffa-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="7fffa-107">Este tópico descreve tooperform de comandos do PowerShell Olá muitas das tarefas de gerenciamento de saudação para serviços de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fffa-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="7fffa-108">Vamos apresentar a criação de um serviço de pesquisa, como escaloná-lo e como gerenciar suas chaves de API.</span><span class="sxs-lookup"><span data-stu-id="7fffa-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="7fffa-109">Esses comandos paralelo opções de gerenciamento de saudação disponíveis no hello [API de REST de gerenciamento do Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="7fffa-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fffa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7fffa-110">Prerequisites</span></span>
* <span data-ttu-id="7fffa-111">É necessário ter o Azure PowerShell 1.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="7fffa-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="7fffa-112">Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7fffa-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="7fffa-113">Você deve estar conectado no tooyour assinatura do Azure no PowerShell, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="7fffa-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="7fffa-114">Primeiro, você deve tooAzure logon com este comando:</span><span class="sxs-lookup"><span data-stu-id="7fffa-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="7fffa-115">Especifique o endereço de email de saudação de sua conta do Azure e sua senha na caixa de diálogo de logon do hello Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7fffa-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="7fffa-116">Como alternativa, é possível fazer [logon de forma não interativa com uma entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="7fffa-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="7fffa-117">Se você tiver várias assinaturas do Azure, será necessário tooset sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fffa-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="7fffa-118">toosee uma lista de suas assinaturas atuais, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="7fffa-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="7fffa-119">assinatura toospecify Olá executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7fffa-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="7fffa-120">Olá exemplo a seguir, nome de assinatura Olá é `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="7fffa-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="7fffa-121">Comandos toohelp que você a começar</span><span class="sxs-lookup"><span data-stu-id="7fffa-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="7fffa-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7fffa-122">Next Steps</span></span>
<span data-ttu-id="7fffa-123">Agora que o serviço é criado, você pode realizar Olá próximas etapas: criar um [índice](search-what-is-an-index.md), [consultar um índice](search-query-overview.md)e, finalmente, criar e gerenciar seu próprio aplicativo de pesquisa que usa a pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fffa-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="7fffa-124">Criar um índice de pesquisa do Azure no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="7fffa-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="7fffa-125">Consultar um índice de pesquisa do Azure usando o Gerenciador de pesquisa no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7fffa-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="7fffa-126">Configurar um indexador tooload de dados de outros serviços</span><span class="sxs-lookup"><span data-stu-id="7fffa-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="7fffa-127">Como toouse Azure pesquisar no .NET</span><span class="sxs-lookup"><span data-stu-id="7fffa-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="7fffa-128">Analisar o tráfego da Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="7fffa-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

