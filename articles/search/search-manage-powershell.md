---
title: Gerenciar o Azure Search com scripts do PowerShell | Microsoft Docs
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
ms.openlocfilehash: aa51c846efef12461ec382274199bc049c42aaa3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="06d7f-104">Gerencie o serviço de Pesquisa do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="06d7f-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06d7f-105">Portal</span><span class="sxs-lookup"><span data-stu-id="06d7f-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="06d7f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06d7f-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="06d7f-107">Este tópico descreve os comandos do PowerShell para executar muitas das tarefas de gerenciamento dos serviços da Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d7f-107">This topic describes the PowerShell commands to perform many of the management tasks for Azure Search services.</span></span> <span data-ttu-id="06d7f-108">Vamos apresentar a criação de um serviço de pesquisa, como escaloná-lo e como gerenciar suas chaves de API.</span><span class="sxs-lookup"><span data-stu-id="06d7f-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="06d7f-109">Esses comandos são paralelos às opções de gerenciamento disponíveis na [API REST de Gerenciamento da Pesquisa do Azure](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="06d7f-109">These commands parallel the management options available in the [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06d7f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06d7f-110">Prerequisites</span></span>
* <span data-ttu-id="06d7f-111">É necessário ter o Azure PowerShell 1.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="06d7f-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="06d7f-112">Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06d7f-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="06d7f-113">É necessário estar conectado à sua assinatura do Azure no PowerShell, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="06d7f-113">You must be logged in to your Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="06d7f-114">Primeiro, faça logon no Azure com este comando:</span><span class="sxs-lookup"><span data-stu-id="06d7f-114">First, you must login to Azure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="06d7f-115">Especifique o endereço de email de sua conta do Azure e sua senha no diálogo de logon do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="06d7f-115">Specify the email address of your Azure account and its password in the Microsoft Azure login dialog.</span></span>

<span data-ttu-id="06d7f-116">Como alternativa, é possível fazer [logon de forma não interativa com uma entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="06d7f-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="06d7f-117">Se tiver várias assinaturas do Azure, você precisará definir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d7f-117">If you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="06d7f-118">Para ver uma lista de suas assinaturas atuais, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="06d7f-118">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="06d7f-119">Para especificar a assinatura, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="06d7f-119">To specify the subscription, run the following command.</span></span> <span data-ttu-id="06d7f-120">No exemplo a seguir, o nome da assinatura é `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="06d7f-120">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-to-help-you-get-started"></a><span data-ttu-id="06d7f-121">Comandos para ajudá-lo a começar</span><span class="sxs-lookup"><span data-stu-id="06d7f-121">Commands to help you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register the ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once the service is fully created
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

    # Get the primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate the secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access to your indexes
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
    # This command will not return until the operation is finished
    # It can take 15 minutes or more to provision the additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in the service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="06d7f-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06d7f-122">Next Steps</span></span>
<span data-ttu-id="06d7f-123">Agora que o serviço foi criado, você pode executar as próximas etapas: compilar um [índice](search-what-is-an-index.md), [consultar um índice](search-query-overview.md) e, por fim, criar e gerenciar o seu próprio aplicativo de pesquisa que usa o Azure Search.</span><span class="sxs-lookup"><span data-stu-id="06d7f-123">Now that your service is created, you can take the next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="06d7f-124">Criar um índice de Pesquisa do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="06d7f-124">Create an Azure Search index in the Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="06d7f-125">Consultar um índice da Pesquisa do Azure usando o Gerenciador de Pesquisa no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="06d7f-125">Query an Azure Search index using Search Explorer in the Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="06d7f-126">Configurar um indexador para carregar dados de outros serviços</span><span class="sxs-lookup"><span data-stu-id="06d7f-126">Setup an indexer to load data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="06d7f-127">Como usar a pesquisa do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="06d7f-127">How to use Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="06d7f-128">Analisar o tráfego da Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="06d7f-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

