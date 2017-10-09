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
# <a name="manage-your-azure-search-service-with-powershell"></a>Gerencie o serviço de Pesquisa do Azure com o PowerShell
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Este tópico descreve tooperform de comandos do PowerShell Olá muitas das tarefas de gerenciamento de saudação para serviços de pesquisa do Azure. Vamos apresentar a criação de um serviço de pesquisa, como escaloná-lo e como gerenciar suas chaves de API.
Esses comandos paralelo opções de gerenciamento de saudação disponíveis no hello [API de REST de gerenciamento do Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Pré-requisitos
* É necessário ter o Azure PowerShell 1.0 ou superior. Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).
* Você deve estar conectado no tooyour assinatura do Azure no PowerShell, conforme descrito abaixo.

Primeiro, você deve tooAzure logon com este comando:

    Login-AzureRmAccount

Especifique o endereço de email de saudação de sua conta do Azure e sua senha na caixa de diálogo de logon do hello Microsoft Azure.

Como alternativa, é possível fazer [logon de forma não interativa com uma entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Se você tiver várias assinaturas do Azure, será necessário tooset sua assinatura do Azure. toosee uma lista de suas assinaturas atuais, execute este comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

assinatura toospecify Olá executar Olá comando a seguir. Olá exemplo a seguir, nome de assinatura Olá é `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Comandos toohelp que você a começar
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

## <a name="next-steps"></a>Próximas etapas
Agora que o serviço é criado, você pode realizar Olá próximas etapas: criar um [índice](search-what-is-an-index.md), [consultar um índice](search-query-overview.md)e, finalmente, criar e gerenciar seu próprio aplicativo de pesquisa que usa a pesquisa do Azure.

* [Criar um índice de pesquisa do Azure no portal do Azure de saudação](search-create-index-portal.md)
* [Consultar um índice de pesquisa do Azure usando o Gerenciador de pesquisa no hello portal do Azure](search-explorer.md)
* [Configurar um indexador tooload de dados de outros serviços](search-indexer-overview.md)
* [Como toouse Azure pesquisar no .NET](search-howto-dotnet-sdk.md)
* [Analisar o tráfego da Pesquisa do Azure](search-traffic-analytics.md)

