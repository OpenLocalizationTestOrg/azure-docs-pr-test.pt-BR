---
title: Gerenciar o Cache Redis do Azure com o Azure PowerShell | Microsoft Docs
description: Saiba como executar tarefas administrativas para o Cache Redis do Azure usando o PowerShell do Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="79026-103">Gerenciar o Cache Redis do Azure com o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="79026-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79026-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79026-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="79026-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="79026-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="79026-106">Este tópico mostra como executar tarefas comuns, como criar, atualizar e dimensionar suas instâncias de Cache Redis do Azure, como regenerar chaves de acesso e  exibir informações sobre seus caches.</span><span class="sxs-lookup"><span data-stu-id="79026-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="79026-107">Para obter uma lista completa de cmdlets do PowerShell do Cache Redis do Azure, confira [Cmdlets do Cache Redis do Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="79026-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="79026-108">Para obter mais informações sobre o modelo de implantação clássico, consulte [Implantação do Azure Resource Manager versus clássica: Entenda os modelos de implantação e o estado de seus recursos](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="79026-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79026-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79026-109">Prerequisites</span></span>
<span data-ttu-id="79026-110">Se você já instalou o Azure PowerShell, você deve ter o Azure PowerShell versão 1.0.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="79026-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="79026-111">Você pode verificar a versão do Azure PowerShell instalada com o comando este comando no prompt de comando do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79026-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="79026-112">Primeiro, faça logon no Azure com este comando.</span><span class="sxs-lookup"><span data-stu-id="79026-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="79026-113">Especifique o endereço de email de sua conta do Azure e sua senha na caixa de diálogo de logon do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="79026-114">Em seguida, se tiver várias assinaturas do Azure, você precisará definir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="79026-115">Para ver uma lista de suas assinaturas atuais, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="79026-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="79026-116">Para especificar a assinatura, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="79026-117">No exemplo a seguir, o nome da assinatura é `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="79026-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="79026-118">Para poder usar o Windows PowerShell com o Gerenciador de Recursos do Azure, você precisa o seguinte:</span><span class="sxs-lookup"><span data-stu-id="79026-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="79026-119">Windows PowerShell, versão 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="79026-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="79026-120">Para encontrar a versão do Windows PowerShell, digite:`$PSVersionTable` e verifique se o valor de `PSVersion` é 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="79026-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="79026-121">Para instalar uma versão compatível, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="79026-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="79026-122">Para obter ajuda detalhada sobre qualquer cmdlet que você vir neste tutorial, use o cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="79026-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="79026-123">Por exemplo, para obter ajuda para o cmdlet `New-AzureRmRedisCache` , digite:</span><span class="sxs-lookup"><span data-stu-id="79026-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="79026-124">Como se conectar a outras nuvens</span><span class="sxs-lookup"><span data-stu-id="79026-124">How to connect to other clouds</span></span>
<span data-ttu-id="79026-125">Por padrão, o ambiente do Azure é `AzureCloud`, que representa a instância de nuvem global do Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="79026-126">Para se conectar a uma instância diferente, use o comando `Add-AzureRmAccount` com a opção de linha de comando `-Environment` ou -`EnvironmentName` com o ambiente desejado ou o nome do ambiente.</span><span class="sxs-lookup"><span data-stu-id="79026-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="79026-127">Para ver a lista de ambientes disponíveis, execute o cmdlet `Get-AzureRmEnvironment` .</span><span class="sxs-lookup"><span data-stu-id="79026-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="79026-128">Para se conectar à Nuvem do Azure Government</span><span class="sxs-lookup"><span data-stu-id="79026-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="79026-129">Para se conectar à Nuvem do Azure Government, use um dos comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="79026-130">ou o</span><span class="sxs-lookup"><span data-stu-id="79026-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="79026-131">Para criar um cache na Nuvem do Azure Government, use um dos locais a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="79026-132">Gov. dos EUA – Virgínia</span><span class="sxs-lookup"><span data-stu-id="79026-132">USGov Virginia</span></span>
* <span data-ttu-id="79026-133">Gov. dos EUA – Iowa</span><span class="sxs-lookup"><span data-stu-id="79026-133">USGov Iowa</span></span>

<span data-ttu-id="79026-134">Para saber mais sobre a Nuvem do Azure Government, confira [Microsoft Azure Governamental](https://azure.microsoft.com/features/gov/) e [Guia do Desenvolvedor do Microsoft Azure Governamental](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="79026-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="79026-135">Para se conectar à Nuvem do Azure na China</span><span class="sxs-lookup"><span data-stu-id="79026-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="79026-136">Para se conectar à Nuvem do Azure na China, use um dos comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="79026-137">ou o</span><span class="sxs-lookup"><span data-stu-id="79026-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="79026-138">Para criar um cache na Nuvem do Azure na China, use um dos locais a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="79026-139">Leste da China</span><span class="sxs-lookup"><span data-stu-id="79026-139">China East</span></span>
* <span data-ttu-id="79026-140">Norte da China</span><span class="sxs-lookup"><span data-stu-id="79026-140">China North</span></span>

<span data-ttu-id="79026-141">Para obter mais informações sobre a Nuvem do Azure na China, confira [AzureChinaCloud para Azure operado pelo 21Vianet na China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="79026-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="79026-142">Para se conectar ao Microsoft Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="79026-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="79026-143">Para se conectar ao Microsoft Azure Alemanha, use um dos comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="79026-144">ou o</span><span class="sxs-lookup"><span data-stu-id="79026-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="79026-145">Para criar um cache no Microsoft Azure Alemanha, use uma das localizações a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="79026-146">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="79026-146">Germany Central</span></span>
* <span data-ttu-id="79026-147">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="79026-147">Germany Northeast</span></span>

<span data-ttu-id="79026-148">Para obter mais informações sobre o Microsoft Azure Alemanha, consulte [Microsoft Azure Alemanha](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="79026-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="79026-149">Propriedades usadas para o PowerShell do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="79026-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="79026-150">A tabela a seguir contém as propriedades e as descrições dos parâmetros usados ao criar e gerenciar suas instâncias do Cache Redis do Azure usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79026-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="79026-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="79026-151">Parameter</span></span> | <span data-ttu-id="79026-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="79026-152">Description</span></span> | <span data-ttu-id="79026-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="79026-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79026-154">Name</span><span class="sxs-lookup"><span data-stu-id="79026-154">Name</span></span> |<span data-ttu-id="79026-155">Nome do cache</span><span class="sxs-lookup"><span data-stu-id="79026-155">Name of the cache</span></span> | |
| <span data-ttu-id="79026-156">Local</span><span class="sxs-lookup"><span data-stu-id="79026-156">Location</span></span> |<span data-ttu-id="79026-157">Local do cache</span><span class="sxs-lookup"><span data-stu-id="79026-157">Location of the cache</span></span> | |
| <span data-ttu-id="79026-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="79026-158">ResourceGroupName</span></span> |<span data-ttu-id="79026-159">Nome do grupo de recursos no qual criar o cache</span><span class="sxs-lookup"><span data-stu-id="79026-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="79026-160">Tamanho</span><span class="sxs-lookup"><span data-stu-id="79026-160">Size</span></span> |<span data-ttu-id="79026-161">O tamanho do cache.</span><span class="sxs-lookup"><span data-stu-id="79026-161">The size of the cache.</span></span> <span data-ttu-id="79026-162">Os valores válidos são: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="79026-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="79026-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="79026-163">1GB</span></span> |
| <span data-ttu-id="79026-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="79026-164">ShardCount</span></span> |<span data-ttu-id="79026-165">O número de fragmentos para criar durante a criação de um cache premium com o cluster ativado.</span><span class="sxs-lookup"><span data-stu-id="79026-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="79026-166">Os valores válidos são: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="79026-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="79026-167">SKU</span><span class="sxs-lookup"><span data-stu-id="79026-167">SKU</span></span> |<span data-ttu-id="79026-168">Especifica o SKU do cache.</span><span class="sxs-lookup"><span data-stu-id="79026-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="79026-169">Os valores válidos são: Básico, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="79026-170">Standard</span><span class="sxs-lookup"><span data-stu-id="79026-170">Standard</span></span> |
| <span data-ttu-id="79026-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="79026-171">RedisConfiguration</span></span> |<span data-ttu-id="79026-172">Especifica as definições de configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="79026-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="79026-173">Para obter detalhes sobre cada configuração, confira a seguinte tabela de [propriedades RedisConfiguration](#redisconfiguration-properties) .</span><span class="sxs-lookup"><span data-stu-id="79026-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="79026-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="79026-174">EnableNonSslPort</span></span> |<span data-ttu-id="79026-175">Indica se a porta não SSL está habilitada.</span><span class="sxs-lookup"><span data-stu-id="79026-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="79026-176">Falso</span><span class="sxs-lookup"><span data-stu-id="79026-176">False</span></span> |
| <span data-ttu-id="79026-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="79026-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="79026-178">Esse parâmetro foi desaprovado - use RedisConfiguration em vez disso.</span><span class="sxs-lookup"><span data-stu-id="79026-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="79026-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="79026-179">StaticIP</span></span> |<span data-ttu-id="79026-180">Ao hospedar o cache em uma VNET, especifica um endereço IP exclusivo na sub-rede do cache.</span><span class="sxs-lookup"><span data-stu-id="79026-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="79026-181">Se ele não for fornecido, um será escolhido para você na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="79026-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="79026-182">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="79026-182">Subnet</span></span> |<span data-ttu-id="79026-183">Ao hospedar o cache em uma VNET, especifica o nome da sub-rede na qual implantar o cache.</span><span class="sxs-lookup"><span data-stu-id="79026-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="79026-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="79026-184">VirtualNetwork</span></span> |<span data-ttu-id="79026-185">Ao hospedar o cache em uma VNET, especifica a ID do recurso da VNET na qual implantar o cache.</span><span class="sxs-lookup"><span data-stu-id="79026-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="79026-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="79026-186">KeyType</span></span> |<span data-ttu-id="79026-187">Especifica qual chave de acesso regenerar durante a renovação das chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="79026-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="79026-188">Os valores válidos são: Primary, Secondary</span><span class="sxs-lookup"><span data-stu-id="79026-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="79026-189">propriedades RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="79026-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="79026-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="79026-190">Property</span></span> | <span data-ttu-id="79026-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="79026-191">Description</span></span> | <span data-ttu-id="79026-192">Tipos de preço</span><span class="sxs-lookup"><span data-stu-id="79026-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79026-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="79026-193">rdb-backup-enabled</span></span> |<span data-ttu-id="79026-194">Se [persistência de dados Redis](cache-how-to-premium-persistence.md) está habilitada</span><span class="sxs-lookup"><span data-stu-id="79026-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="79026-195">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="79026-195">Premium only</span></span> |
| <span data-ttu-id="79026-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="79026-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="79026-197">A cadeia de conexão da conta de armazenamento para [persistência de dados Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="79026-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="79026-198">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="79026-198">Premium only</span></span> |
| <span data-ttu-id="79026-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="79026-199">rdb-backup-frequency</span></span> |<span data-ttu-id="79026-200">A frequência de backup da [persistência de dados Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="79026-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="79026-201">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="79026-201">Premium only</span></span> |
| <span data-ttu-id="79026-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="79026-202">maxmemory-reserved</span></span> |<span data-ttu-id="79026-203">Configura a [memória reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para processos fora do cache</span><span class="sxs-lookup"><span data-stu-id="79026-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="79026-204">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-204">Standard and Premium</span></span> |
| <span data-ttu-id="79026-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="79026-205">maxmemory-policy</span></span> |<span data-ttu-id="79026-206">Configura o [política de remoção](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para o cache</span><span class="sxs-lookup"><span data-stu-id="79026-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="79026-207">Todos os tipos de preço</span><span class="sxs-lookup"><span data-stu-id="79026-207">All pricing tiers</span></span> |
| <span data-ttu-id="79026-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="79026-208">notify-keyspace-events</span></span> |<span data-ttu-id="79026-209">Configura [notificações keyspace](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="79026-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="79026-210">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-210">Standard and Premium</span></span> |
| <span data-ttu-id="79026-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="79026-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="79026-212">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="79026-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="79026-213">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-213">Standard and Premium</span></span> |
| <span data-ttu-id="79026-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="79026-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="79026-215">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="79026-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="79026-216">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-216">Standard and Premium</span></span> |
| <span data-ttu-id="79026-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="79026-217">set-max-intset-entries</span></span> |<span data-ttu-id="79026-218">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="79026-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="79026-219">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-219">Standard and Premium</span></span> |
| <span data-ttu-id="79026-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="79026-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="79026-221">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="79026-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="79026-222">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-222">Standard and Premium</span></span> |
| <span data-ttu-id="79026-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="79026-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="79026-224">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="79026-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="79026-225">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-225">Standard and Premium</span></span> |
| <span data-ttu-id="79026-226">databases</span><span class="sxs-lookup"><span data-stu-id="79026-226">databases</span></span> |<span data-ttu-id="79026-227">Configura o número de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="79026-227">Configures the number of databases.</span></span> <span data-ttu-id="79026-228">Essa propriedade pode ser configurada apenas na criação do cache.</span><span class="sxs-lookup"><span data-stu-id="79026-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="79026-229">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="79026-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="79026-230">Para criar uma Cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-230">To create a Redis Cache</span></span>
<span data-ttu-id="79026-231">As novas instâncias Cache Redis do Azure são criadas usando o cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79026-232">Na primeira vez em que você cria um cache Redis em uma assinatura usando o portal do Azure, o portal registra o namespace `Microsoft.Cache` para a assinatura.</span><span class="sxs-lookup"><span data-stu-id="79026-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="79026-233">Se você tentar criar o cache Redis primeiro em uma assinatura usando o PowerShell, deverá primeiro registrar esse namespace usando o comando a seguir; caso contrário, cmdlets como `New-AzureRmRedisCache` e `Get-AzureRmRedisCache` falharão.</span><span class="sxs-lookup"><span data-stu-id="79026-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="79026-234">Para ver uma lista dos parâmetros disponíveis e suas descrições para `New-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-235">Para criar um cache com parâmetros padrão, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="79026-236">`ResourceGroupName`, `Name` e `Location` são parâmetros obrigatórios, mas os restantes são opcionais e têm valores padrão.</span><span class="sxs-lookup"><span data-stu-id="79026-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="79026-237">Executar o comando anterior cria uma instância Cache Redis do Azure do SKU Standard com o nome especificado, local e grupo de recursos, que é tem 1 GB de tamanho com a porta não SSL desativada.</span><span class="sxs-lookup"><span data-stu-id="79026-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="79026-238">Para criar um cache premium, especifique um tamanho de P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB) ou P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="79026-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="79026-239">Para habilitar o clustering, especifique uma contagem de fragmentos usando o parâmetro `ShardCount` .</span><span class="sxs-lookup"><span data-stu-id="79026-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="79026-240">O exemplo a seguir cria um cache premium P1 com 3 fragmentos.</span><span class="sxs-lookup"><span data-stu-id="79026-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="79026-241">Um cache premium P1 tem 6 GB de tamanho e como especificamos três fragmentos, o tamanho total é de 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="79026-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="79026-242">Para especificar valores para o parâmetro `RedisConfiguration`, coloque os valores dentro de `{}` como pares de chave/valor como `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="79026-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="79026-243">O exemplo a seguir cria um cache padrão de 1 GB com as `allkeys-random` notificações maxmemory-policy e keyspace configuradas com `KEA`.</span><span class="sxs-lookup"><span data-stu-id="79026-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="79026-244">Para obter mais informações, consulte [Notificações de keyspace (configurações avançadas)](cache-configure.md#keyspace-notifications-advanced-settings) e [Políticas de memória](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="79026-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="79026-245">Para configurar a definição dos bancos de dados durante a criação do cache</span><span class="sxs-lookup"><span data-stu-id="79026-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="79026-246">A configuração `databases` pode ser definida somente durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="79026-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="79026-247">O exemplo a seguir cria um cache premium P3 (26 GB) com 48 bancos de dados usando o cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="79026-248">Para obter informações sobre a propriedade `databases` , consulte [Configuração do servidor Cache Redis do Azure Padrão](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="79026-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="79026-249">Para obter mais informações sobre como criar um cache usando o cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx), consulte a seção anterior [Para criar um Cache Redis](#to-create-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="79026-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="79026-250">Para atualizar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-250">To update a Redis cache</span></span>
<span data-ttu-id="79026-251">As instâncias Cache Redis do Azure são atualizadas usando o cmdlet [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="79026-252">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Set-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-253">O cmdlet `Set-AzureRmRedisCache` pode ser usado para atualizar propriedades como `Size`, `Sku`, `EnableNonSslPort` e os valores `RedisConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="79026-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="79026-254">O comando a seguir atualiza a maxmemory-policy do Cache Redis chamada myCache.</span><span class="sxs-lookup"><span data-stu-id="79026-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="79026-255">Para dimensionar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-255">To scale a Redis cache</span></span>
<span data-ttu-id="79026-256">`Set-AzureRmRedisCache` pode ser usado para dimensionar uma instância do cache Redis do Azure quando as propriedades `Size`, `Sku` ou `ShardCount` são modificadas.</span><span class="sxs-lookup"><span data-stu-id="79026-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="79026-257">Dimensionar um cache usando o PowerShell está sujeito aos mesmos limites e diretrizes de dimensionar um cache no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="79026-258">Você pode dimensionar para uma camada de preços diferente com as restrições a seguir.</span><span class="sxs-lookup"><span data-stu-id="79026-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="79026-259">Você não pode dimensionar de uma camada de preços mais alta para uma camada de preços mais baixa.</span><span class="sxs-lookup"><span data-stu-id="79026-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="79026-260">Você não pode dimensionar de um cache **Premium** para um cache **Standard** ou **Básico**.</span><span class="sxs-lookup"><span data-stu-id="79026-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="79026-261">Você não pode dimensionar de um cache **Standard** para um cache **Básico**.</span><span class="sxs-lookup"><span data-stu-id="79026-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="79026-262">É possível dimensionar de um cache **Básico** para um cache **Standard**, mas não é possível alterar o tamanho simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="79026-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="79026-263">Se precisar de um tamanho diferente, você pode fazer uma operação de dimensionamento subsequente para o tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="79026-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="79026-264">Você não pode dimensionar de um cache **Básico** diretamente para um cache **Premium**.</span><span class="sxs-lookup"><span data-stu-id="79026-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="79026-265">Você deve dimensionar do **Básico** para o **Standard** em uma única operação de dimensionamento e do **Standard** para o **Premium** em uma operação de dimensionamento subsequente.</span><span class="sxs-lookup"><span data-stu-id="79026-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="79026-266">Não é possível dimensionar de um tamanho maior para o tamanho **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="79026-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="79026-267">Para saber mais, confira [Como dimensionar o Cache Redis do Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="79026-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="79026-268">O exemplo a seguir mostra como dimensionar um cache denominado `myCache` para um cache de 2,5 GB.</span><span class="sxs-lookup"><span data-stu-id="79026-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="79026-269">Observe que esse comando funciona para um cache Básico ou Standard.</span><span class="sxs-lookup"><span data-stu-id="79026-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="79026-270">Depois do comando ser emitido, o status do cache é retornado (semelhante a chamar `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="79026-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="79026-271">Observe que `ProvisioningState` é `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="79026-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="79026-272">Quando a operação de dimensionamento for concluída, o `ProvisioningState` será alterado para `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="79026-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="79026-273">Se você precisar fazer uma operação de dimensionamento subsequente, como alterar de Básico para Standard, em seguida, alterar o tamanho, deverá aguardar até que a operação anterior seja concluída ou receberá um erro semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="79026-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="79026-274">Para obter informações sobre um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-274">To get information about a Redis cache</span></span>
<span data-ttu-id="79026-275">Você pode recuperar informações sobre um cache usando o cmdlet [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="79026-276">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-277">Para retornar informações sobre todos os caches na assinatura atual, execute `Get-AzureRmRedisCache` sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="79026-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="79026-278">Para retornar informações sobre todos os caches em um grupo de recursos específico, execute `Get-AzureRmRedisCache` com o parâmetro `ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="79026-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="79026-279">Para retornar informações sobre um cache específico, execute `Get-AzureRmRedisCache` com o parâmetro `Name` que contém o nome do cache e o parâmetro `ResourceGroupName` com o grupo de recursos que contém esse cache.</span><span class="sxs-lookup"><span data-stu-id="79026-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="79026-280">Para recuperar as chaves de acesso para um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="79026-281">Para recuperar as chaves de acesso para seu cache, você pode usar o cmdlet [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="79026-282">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCacheKey`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-283">Para recuperar as chaves para seu cache, chame o cmdlet `Get-AzureRmRedisCacheKey` e passe no nome de seu cache o nome do grupo de recursos que contém o cache.</span><span class="sxs-lookup"><span data-stu-id="79026-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="79026-284">Para regenerar chaves de acesso para seu cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="79026-285">Para recuperar as chaves de acesso para seu cache, você pode usar o cmdlet [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="79026-286">Para ver uma lista dos parâmetros disponíveis e suas descrições para `New-AzureRmRedisCacheKey`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-287">Para regenerar a chave primária ou secundária para seu cache, chame o cmdlet `New-AzureRmRedisCacheKey`, passe no nome o grupo de recursos e especifique `Primary` ou `Secondary` para o parâmetro `KeyType`.</span><span class="sxs-lookup"><span data-stu-id="79026-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="79026-288">No exemplo a seguir, a chave de acesso secundária para um cache é regenerada.</span><span class="sxs-lookup"><span data-stu-id="79026-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="79026-289">Para excluir um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-289">To delete a Redis cache</span></span>
<span data-ttu-id="79026-290">Para excluir um cache Redis, use o cmdlet [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) .</span><span class="sxs-lookup"><span data-stu-id="79026-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="79026-291">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Remove-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="79026-292">No exemplo a seguir, o cache denominado `myCache` é removido.</span><span class="sxs-lookup"><span data-stu-id="79026-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="79026-293">Para importar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-293">To import a Redis cache</span></span>
<span data-ttu-id="79026-294">Você pode importar dados em uma instância de Cache Redis do Azure usando o cmdlet `Import-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="79026-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79026-295">A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="79026-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="79026-296">Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="79026-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="79026-297">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Import-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="79026-298">O comando a seguir importa dados do blob especificado pelo URI de SAS no Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="79026-299">Para exportar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-299">To export a Redis cache</span></span>
<span data-ttu-id="79026-300">Você pode exportar dados de uma instância de Cache Redis do Azure usando o cmdlet `Export-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="79026-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79026-301">A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="79026-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="79026-302">Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="79026-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="79026-303">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Export-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="79026-304">O comando a seguir exporta dados de uma instância de Cache Redis do Azure para o contêiner especificado pelo URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="79026-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="79026-305">Para reinicializar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="79026-305">To reboot a Redis cache</span></span>
<span data-ttu-id="79026-306">Você pode reinicializar a instância de Cache Redis do Azure usando o cmdlet `Reset-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="79026-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79026-307">A reinicialização está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="79026-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="79026-308">Para saber mais sobre a reinicialização de seu cache, confira [Administração de cache - reinicializar](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="79026-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="79026-309">Para ver uma lista dos parâmetros disponíveis e suas descrições para `Reset-AzureRmRedisCache`, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="79026-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="79026-310">O comando a seguir reinicializa ambos os nós do cache especificado.</span><span class="sxs-lookup"><span data-stu-id="79026-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="79026-311">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79026-311">Next steps</span></span>
<span data-ttu-id="79026-312">Para saber mais sobre como usar o Windows PowerShell com o Azure, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="79026-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="79026-313">Documentação de cmdlet do Cache Redis do Azure no MSDN</span><span class="sxs-lookup"><span data-stu-id="79026-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="79026-314">[Cmdlets do Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkID=394765): saiba usar os cmdlets no módulo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="79026-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="79026-315">[Usando Grupos de recursos para gerenciar seus recursos do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): saiba como criar e gerenciar grupos de recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="79026-316">[Blog do Azure](http://blogs.msdn.com/windowsazure): obtenha informações sobre os novos recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="79026-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="79026-317">[Blog do Windows PowerShell](http://blogs.msdn.com/powershell): obtenha informações sobre os novos recursos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79026-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="79026-318">[Blog "Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): obtenha dicas reais e truques da comunidade.do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79026-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

