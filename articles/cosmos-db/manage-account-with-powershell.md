---
title: "Automação do Azure Cosmos DB – Gerenciamento com o PowerShell | Microsoft Docs"
description: Use o Azure PowerShell para gerenciar suas contas do Azure Cosmos DB.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="c6625-103">Criar uma conta do Azure Cosmos DB usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6625-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="c6625-104">O guia a seguir descreve os comandos para automatizar o gerenciamento de suas contas de banco de dados do Azure Cosmos DB usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6625-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="c6625-105">Isso também inclui comandos para gerenciar as chaves de conta e as prioridades de failover em [contas de banco de dados com várias regiões][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="c6625-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="c6625-106">A atualização de sua conta de banco de dados permite que você adicione ou remova regiões e modifique políticas de consistência.</span><span class="sxs-lookup"><span data-stu-id="c6625-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="c6625-107">Para o gerenciamento de plataforma cruzada de sua conta do Azure Cosmos DB, use a [CLI do Azure](cli-samples.md), a [API REST do Provedor de Recursos][rp-rest-api] ou o [portal do Azure](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="c6625-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c6625-108">Introdução</span><span class="sxs-lookup"><span data-stu-id="c6625-108">Getting Started</span></span>

<span data-ttu-id="c6625-109">Siga as instruções em [Como instalar e configurar o Azure PowerShell][powershell-install-configure] para instalar e fazer logon em sua conta do Azure Resource Manager no Powershell.</span><span class="sxs-lookup"><span data-stu-id="c6625-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="c6625-110">Observações</span><span class="sxs-lookup"><span data-stu-id="c6625-110">Notes</span></span>

* <span data-ttu-id="c6625-111">Se você quiser executar os comandos a seguir sem a necessidade de confirmação do usuário, acrescente o sinalizador `-Force` ao comando.</span><span class="sxs-lookup"><span data-stu-id="c6625-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="c6625-112">Todos os comandos a seguir são síncronos.</span><span class="sxs-lookup"><span data-stu-id="c6625-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="c6625-113"><a id="create-documentdb-account-powershell"></a> Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c6625-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="c6625-114">Esse comando permite que você crie uma conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="c6625-115">Configure sua nova conta de banco de dados como região única ou [várias regiões][scaling-globally] com uma [política de consistência](consistency-levels.md) determinada.</span><span class="sxs-lookup"><span data-stu-id="c6625-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="c6625-116">`<write-region-location>` O nome do local da região de gravação da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="c6625-117">Esse local deve ter um valor de prioridade de failover de 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="c6625-118">Deve haver exatamente uma região de gravação por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="c6625-119">`<read-region-location>` O nome do local da região de leitura da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="c6625-120">Esse local deve ter um valor de prioridade de failover maior do que 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="c6625-121">Pode haver mais de uma região de leitura por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="c6625-122">`<ip-range-filter>` Especifica o conjunto de endereços IP ou os intervalos de endereços IP no formato CIDR a serem incluídos como a lista de permissões de IPs de cliente para uma determinada conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="c6625-123">Os intervalos/endereços IP devem ser separados por vírgula e não devem conter espaços.</span><span class="sxs-lookup"><span data-stu-id="c6625-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="c6625-124">Para obter mais informações, consulte [Suporte ao firewall do Azure Cosmos DB](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="c6625-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="c6625-125">`<default-consistency-level>` O nível de consistência padrão da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="c6625-126">Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c6625-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="c6625-127">`<max-interval>` Ao ser usado com a consistência Estagnação Limitada, esse valor representa a quantidade de tempo de desatualização (em segundos) tolerada.</span><span class="sxs-lookup"><span data-stu-id="c6625-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="c6625-128">O intervalo aceito para este valor é de 1 a 100.</span><span class="sxs-lookup"><span data-stu-id="c6625-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="c6625-129">`<max-staleness-prefix>` Ao ser usado com a consistência Estagnação Limitada, esse valor representa o número de solicitações de estagnação tolerado.</span><span class="sxs-lookup"><span data-stu-id="c6625-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="c6625-130">O intervalo aceito para este valor é de 1 a 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="c6625-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="c6625-131">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-132">`<resource-group-location>` A localização do Grupo de Recursos do Azure à qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-133">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB a ser criada.</span><span class="sxs-lookup"><span data-stu-id="c6625-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="c6625-134">Pode usar apenas letras minúsculas, números, o caractere '-' e deve ter entre três e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c6625-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="c6625-135">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="c6625-136">Observações</span><span class="sxs-lookup"><span data-stu-id="c6625-136">Notes</span></span>
* <span data-ttu-id="c6625-137">O exemplo anterior cria uma conta de banco de dados com duas regiões.</span><span class="sxs-lookup"><span data-stu-id="c6625-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="c6625-138">Também é possível criar uma conta de banco de dados com uma região (que é designada como a região de gravação e tem um valor de prioridade de failover de 0) ou com mais de duas regiões.</span><span class="sxs-lookup"><span data-stu-id="c6625-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="c6625-139">Para saber mais, veja [Contas de banco de dados com várias regiões][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="c6625-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="c6625-140">As localizações devem ser regiões nas quais o Azure Cosmos DB está disponível.</span><span class="sxs-lookup"><span data-stu-id="c6625-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="c6625-141">Confira a lista atual de regiões na [página Regiões do Azure](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="c6625-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="c6625-142"><a id="update-documentdb-account-powershell"></a> Atualizar uma conta de banco de dados do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c6625-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="c6625-143">Esse comando permite que você atualize as propriedades de sua conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="c6625-144">Isso inclui a política de consistência e os locais nos quais a conta de banco de dados existe.</span><span class="sxs-lookup"><span data-stu-id="c6625-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="c6625-145">Esse comando permite adicionar e remover regiões, mas não permite modificar as prioridades de failover.</span><span class="sxs-lookup"><span data-stu-id="c6625-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="c6625-146">Para modificar as prioridades de failover, confira [abaixo](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="c6625-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="c6625-147">`<write-region-location>` O nome do local da região de gravação da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="c6625-148">Esse local deve ter um valor de prioridade de failover de 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="c6625-149">Deve haver exatamente uma região de gravação por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="c6625-150">`<read-region-location>` O nome do local da região de leitura da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="c6625-151">Esse local deve ter um valor de prioridade de failover maior do que 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="c6625-152">Pode haver mais de uma região de leitura por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="c6625-153">`<default-consistency-level>` O nível de consistência padrão da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="c6625-154">Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c6625-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="c6625-155">`<ip-range-filter>` Especifica o conjunto de endereços IP ou os intervalos de endereços IP no formato CIDR a serem incluídos como a lista de permissões de IPs de cliente para uma determinada conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="c6625-156">Os intervalos/endereços IP devem ser separados por vírgula e não devem conter espaços.</span><span class="sxs-lookup"><span data-stu-id="c6625-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="c6625-157">Para obter mais informações, consulte [Suporte ao firewall do Azure Cosmos DB](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="c6625-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="c6625-158">`<max-interval>` Ao ser usado com a consistência Estagnação Limitada, esse valor representa a quantidade de tempo de desatualização (em segundos) tolerada.</span><span class="sxs-lookup"><span data-stu-id="c6625-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="c6625-159">O intervalo aceito para este valor é de 1 a 100.</span><span class="sxs-lookup"><span data-stu-id="c6625-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="c6625-160">`<max-staleness-prefix>` Ao ser usado com a consistência Estagnação Limitada, esse valor representa o número de solicitações de estagnação tolerado.</span><span class="sxs-lookup"><span data-stu-id="c6625-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="c6625-161">O intervalo aceito para este valor é de 1 a 2,147,483,647.</span><span class="sxs-lookup"><span data-stu-id="c6625-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="c6625-162">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-163">`<resource-group-location>` A localização do Grupo de Recursos do Azure à qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-164">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB a ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="c6625-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="c6625-165">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="c6625-166"><a id="delete-documentdb-account-powershell"></a> Excluir uma conta de banco de dados do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c6625-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="c6625-167">Esse comando permite que você exclua uma conta de banco de dados existente do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="c6625-168">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-169">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB a ser excluída.</span><span class="sxs-lookup"><span data-stu-id="c6625-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="c6625-170">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="c6625-171"><a id="get-documentdb-properties-powershell"></a>Obter propriedades de uma conta de banco de dados do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c6625-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="c6625-172">Esse comando permite que você obtenha as propriedades de uma conta de banco de dados existente do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="c6625-173">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-174">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="c6625-175">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="c6625-176"><a id="update-tags-powershell"></a> Atualizar as marcações de uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c6625-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="c6625-177">O exemplo a seguir descreve como definir [marcações de recurso do Azure][azure-resource-tags] em sua conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="c6625-178">Este comando pode ser combinado com os comandos de criação ou atualização anexando o sinalizador `-Tags` com o parâmetro correspondente.</span><span class="sxs-lookup"><span data-stu-id="c6625-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="c6625-179">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="c6625-180"><a id="list-account-keys-powershell"></a> Listar chaves da conta</span><span class="sxs-lookup"><span data-stu-id="c6625-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="c6625-181">Quando você cria uma conta do Azure Cosmos DB, o serviço gera duas chaves de acesso mestras que podem ser usadas para autenticação quando a conta do Azure Cosmos DB é acessada.</span><span class="sxs-lookup"><span data-stu-id="c6625-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="c6625-182">Ao fornecer duas chaves de acesso, o Azure Cosmos DB permite regenerar as chaves sem nenhuma interrupção na conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="c6625-183">Também estão disponíveis chaves somente leitura para autenticação de operações somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c6625-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="c6625-184">Há duas chaves de leitura/gravação (primária e secundária) e duas chaves somente leitura (primária e secundária).</span><span class="sxs-lookup"><span data-stu-id="c6625-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="c6625-185">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-186">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="c6625-187">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="c6625-188"><a id="list-connection-strings-powershell"></a> Listar Cadeias de Conexão</span><span class="sxs-lookup"><span data-stu-id="c6625-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="c6625-189">Para contas do MongoDB, a cadeia de conexão para conectar seu aplicativo do MongoDB à conta do banco de dados pode ser recuperada usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c6625-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="c6625-190">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-191">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="c6625-192">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="c6625-193"><a id="regenerate-account-key-powershell"></a> Recuperar a chave da conta</span><span class="sxs-lookup"><span data-stu-id="c6625-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="c6625-194">Você deve alterar as chaves de acesso de sua conta do Azure Cosmos DB periodicamente para ajudar a manter as conexões mais seguras.</span><span class="sxs-lookup"><span data-stu-id="c6625-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="c6625-195">Duas chaves de acesso são atribuídas para permitir que você mantenha conexões com a conta do Azure Cosmos DB usando uma chave de acesso enquanto regenera a outra.</span><span class="sxs-lookup"><span data-stu-id="c6625-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="c6625-196">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-197">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="c6625-198">`<key-kind>` Um dos quatro tipos de chaves: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] que você quer gerar novamente.</span><span class="sxs-lookup"><span data-stu-id="c6625-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="c6625-199">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="c6625-200"><a id="modify-failover-priority-powershell"></a> Modificar a Prioridade de Failover de uma Conta de Banco de Dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c6625-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="c6625-201">Para contas de banco de dados com várias regiões, altere a prioridade de failover das várias regiões nas quais a conta de banco de dados do Azure Cosmos DB existe.</span><span class="sxs-lookup"><span data-stu-id="c6625-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="c6625-202">Para obter mais informações sobre failover em sua conta de banco de dados do Azure Cosmos DB, consulte [Distribuir dados globalmente com o Azure Cosmos DB][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="c6625-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="c6625-203">`<write-region-location>` O nome do local da região de gravação da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="c6625-204">Esse local deve ter um valor de prioridade de failover de 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="c6625-205">Deve haver exatamente uma região de gravação por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="c6625-206">`<read-region-location>` O nome do local da região de leitura da conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="c6625-207">Esse local deve ter um valor de prioridade de failover maior do que 0.</span><span class="sxs-lookup"><span data-stu-id="c6625-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="c6625-208">Pode haver mais de uma região de leitura por conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6625-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="c6625-209">`<resource-group-name>` O nome do [Grupo de Recursos do Azure][azure-resource-groups] ao qual pertence a nova conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="c6625-210">`<database-account-name>` O nome da conta de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6625-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="c6625-211">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6625-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="c6625-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6625-212">Next steps</span></span>

* <span data-ttu-id="c6625-213">Para se conectar usando o .NET, consulte [Conectar e consultar com o .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c6625-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="c6625-214">Para se conectar usando o .NET Core, consulte [Conectar e consultar com o .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="c6625-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="c6625-215">Para se conectar usando o Node.js, consulte [Conectar e consultar com o Node.js e um aplicativo do MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c6625-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
