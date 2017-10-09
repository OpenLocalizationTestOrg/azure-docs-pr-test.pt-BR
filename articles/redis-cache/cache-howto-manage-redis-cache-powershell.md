---
title: aaaManage Cache Redis do Azure com o Azure PowerShell | Microsoft Docs
description: Saiba como tooperform de tarefas administrativas para o Cache Redis do Azure usando o PowerShell do Azure.
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
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="275b6-103">Gerenciar o Cache Redis do Azure com o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="275b6-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="275b6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="275b6-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="275b6-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="275b6-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="275b6-106">Este tópico mostra como tooperform comuns tarefas como criar, atualizar e dimensione suas instâncias de Cache Redis do Azure, como chaves de acesso tooregenerate e como tooview informações sobre seus caches.</span><span class="sxs-lookup"><span data-stu-id="275b6-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="275b6-107">Para obter uma lista completa de cmdlets do PowerShell do Cache Redis do Azure, confira [Cmdlets do Cache Redis do Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="275b6-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="275b6-108">Para obter mais informações sobre o modelo de implantação clássico hello, consulte [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="275b6-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="275b6-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="275b6-109">Prerequisites</span></span>
<span data-ttu-id="275b6-110">Se você já instalou o Azure PowerShell, você deve ter o Azure PowerShell versão 1.0.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="275b6-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="275b6-111">Você pode verificar a versão de saudação do PowerShell do Azure que você instalou com este comando no prompt de comando do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="275b6-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="275b6-112">Primeiro, você deve efetuar login tooAzure com este comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="275b6-113">Especifique o endereço de email de saudação de sua conta do Azure e sua senha na caixa de diálogo Olá entrar no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="275b6-114">Em seguida, se você tiver várias assinaturas do Azure, será necessário tooset sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="275b6-115">toosee uma lista de suas assinaturas atuais, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="275b6-116">assinatura toospecify Olá executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="275b6-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="275b6-117">Olá exemplo a seguir, nome de assinatura Olá é `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="275b6-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="275b6-118">Antes de usar o Windows PowerShell com o Gerenciador de recursos do Azure, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="275b6-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="275b6-119">Windows PowerShell, versão 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="275b6-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="275b6-120">versão de saudação do toofind do Windows PowerShell, digite:`$PSVersionTable` e verifique se o valor de saudação do `PSVersion` é 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="275b6-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="275b6-121">tooinstall uma versão compatível, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="275b6-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="275b6-122">tooget ajuda detalhada para qualquer cmdlet, que consulte neste tutorial, use Olá o cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="275b6-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="275b6-123">Por exemplo, tooget ajuda Olá `New-AzureRmRedisCache` cmdlet, digite:</span><span class="sxs-lookup"><span data-stu-id="275b6-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="275b6-124">Como tooconnect tooother nuvens</span><span class="sxs-lookup"><span data-stu-id="275b6-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="275b6-125">Por saudação padrão do Azure é ambiente `AzureCloud`, que representa Olá instância global em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="275b6-126">tooconnect tooa instância diferente, use Olá `Add-AzureRmAccount` com hello `-Environment` ou -`EnvironmentName` opção de linha de comando com o ambiente desejado hello ou nome do ambiente.</span><span class="sxs-lookup"><span data-stu-id="275b6-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="275b6-127">lista de saudação toosee ambientes disponíveis, execute Olá `Get-AzureRmEnvironment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="275b6-128">tooconnect toohello nuvem do Azure Government</span><span class="sxs-lookup"><span data-stu-id="275b6-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="275b6-129">tooconnect toohello nuvem do governo do Azure, use um dos Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="275b6-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="275b6-130">ou o</span><span class="sxs-lookup"><span data-stu-id="275b6-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="275b6-131">toocreate um cache no hello Azure governamental nuvem, use um dos seguintes locais de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="275b6-132">Gov. dos EUA – Virgínia</span><span class="sxs-lookup"><span data-stu-id="275b6-132">USGov Virginia</span></span>
* <span data-ttu-id="275b6-133">Gov. dos EUA – Iowa</span><span class="sxs-lookup"><span data-stu-id="275b6-133">USGov Iowa</span></span>

<span data-ttu-id="275b6-134">Para obter mais informações sobre hello Azure governamental nuvem, consulte [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) e [guia do desenvolvedor do Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="275b6-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="275b6-135">tooconnect toohello nuvem do Azure na China</span><span class="sxs-lookup"><span data-stu-id="275b6-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="275b6-136">tooconnect toohello nuvem do Azure na China, use um dos comandos a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="275b6-137">ou o</span><span class="sxs-lookup"><span data-stu-id="275b6-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="275b6-138">toocreate um cache na nuvem do Azure na China, usar um dos seguintes locais de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="275b6-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="275b6-139">Leste da China</span><span class="sxs-lookup"><span data-stu-id="275b6-139">China East</span></span>
* <span data-ttu-id="275b6-140">Norte da China</span><span class="sxs-lookup"><span data-stu-id="275b6-140">China North</span></span>

<span data-ttu-id="275b6-141">Para obter mais informações sobre Olá nuvem do Azure na China, consulte [AzureChinaCloud para o Azure operado pela 21Vianet na China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="275b6-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="275b6-142">tooconnect tooMicrosoft Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="275b6-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="275b6-143">tooconnect tooMicrosoft Azure Alemanha, use um dos comandos a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="275b6-144">ou o</span><span class="sxs-lookup"><span data-stu-id="275b6-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="275b6-145">toocreate um cache no Microsoft Azure Alemanha, use um dos seguintes locais de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="275b6-146">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="275b6-146">Germany Central</span></span>
* <span data-ttu-id="275b6-147">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="275b6-147">Germany Northeast</span></span>

<span data-ttu-id="275b6-148">Para obter mais informações sobre o Microsoft Azure Alemanha, consulte [Microsoft Azure Alemanha](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="275b6-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="275b6-149">Propriedades usadas para o PowerShell do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="275b6-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="275b6-150">Olá, a tabela a seguir contém as propriedades e descrições dos parâmetros usados ao criar e gerenciar suas instâncias de Cache Redis do Azure usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="275b6-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="275b6-151">Parameter</span></span> | <span data-ttu-id="275b6-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="275b6-152">Description</span></span> | <span data-ttu-id="275b6-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="275b6-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="275b6-154">Nome</span><span class="sxs-lookup"><span data-stu-id="275b6-154">Name</span></span> |<span data-ttu-id="275b6-155">Nome do cache de saudação</span><span class="sxs-lookup"><span data-stu-id="275b6-155">Name of hello cache</span></span> | |
| <span data-ttu-id="275b6-156">Local</span><span class="sxs-lookup"><span data-stu-id="275b6-156">Location</span></span> |<span data-ttu-id="275b6-157">Local do cache de saudação</span><span class="sxs-lookup"><span data-stu-id="275b6-157">Location of hello cache</span></span> | |
| <span data-ttu-id="275b6-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="275b6-158">ResourceGroupName</span></span> |<span data-ttu-id="275b6-159">Nome do grupo de recursos no qual cache de saudação toocreate</span><span class="sxs-lookup"><span data-stu-id="275b6-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="275b6-160">Tamanho</span><span class="sxs-lookup"><span data-stu-id="275b6-160">Size</span></span> |<span data-ttu-id="275b6-161">tamanho de saudação do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-161">hello size of hello cache.</span></span> <span data-ttu-id="275b6-162">Os valores válidos são: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="275b6-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="275b6-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="275b6-163">1GB</span></span> |
| <span data-ttu-id="275b6-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="275b6-164">ShardCount</span></span> |<span data-ttu-id="275b6-165">número de saudação de fragmentos toocreate ao criar um cache premium com cluster habilitado.</span><span class="sxs-lookup"><span data-stu-id="275b6-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="275b6-166">Os valores válidos são: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="275b6-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="275b6-167">SKU</span><span class="sxs-lookup"><span data-stu-id="275b6-167">SKU</span></span> |<span data-ttu-id="275b6-168">Especifica a saudação SKU do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="275b6-169">Os valores válidos são: Básico, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="275b6-170">Standard</span><span class="sxs-lookup"><span data-stu-id="275b6-170">Standard</span></span> |
| <span data-ttu-id="275b6-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="275b6-171">RedisConfiguration</span></span> |<span data-ttu-id="275b6-172">Especifica as definições de configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="275b6-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="275b6-173">Para obter detalhes sobre cada configuração, consulte o seguinte Olá [RedisConfiguration propriedades](#redisconfiguration-properties) tabela.</span><span class="sxs-lookup"><span data-stu-id="275b6-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="275b6-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="275b6-174">EnableNonSslPort</span></span> |<span data-ttu-id="275b6-175">Indica se a porta do hello não SSL está habilitada.</span><span class="sxs-lookup"><span data-stu-id="275b6-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="275b6-176">Falso</span><span class="sxs-lookup"><span data-stu-id="275b6-176">False</span></span> |
| <span data-ttu-id="275b6-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="275b6-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="275b6-178">Esse parâmetro foi desaprovado - use RedisConfiguration em vez disso.</span><span class="sxs-lookup"><span data-stu-id="275b6-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="275b6-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="275b6-179">StaticIP</span></span> |<span data-ttu-id="275b6-180">Ao hospedar o cache em uma rede virtual, especifica um endereço IP exclusivo na sub-rede Olá para o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="275b6-181">Se não for fornecido, um é escolhido para você de sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="275b6-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="275b6-182">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="275b6-182">Subnet</span></span> |<span data-ttu-id="275b6-183">Ao hospedar o cache em uma rede virtual, especifica o nome de saudação de sub-rede de saudação no cache de saudação que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="275b6-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="275b6-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="275b6-184">VirtualNetwork</span></span> |<span data-ttu-id="275b6-185">Quando hospedando o seu cache em uma rede virtual, especifica a ID de recurso de saudação do hello rede virtual no qual cache de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="275b6-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="275b6-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="275b6-186">KeyType</span></span> |<span data-ttu-id="275b6-187">Especifica qual chave de acesso tooregenerate durante a renovação de chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="275b6-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="275b6-188">Os valores válidos são: Primary, Secondary</span><span class="sxs-lookup"><span data-stu-id="275b6-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="275b6-189">propriedades RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="275b6-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="275b6-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="275b6-190">Property</span></span> | <span data-ttu-id="275b6-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="275b6-191">Description</span></span> | <span data-ttu-id="275b6-192">Tipos de preço</span><span class="sxs-lookup"><span data-stu-id="275b6-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="275b6-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="275b6-193">rdb-backup-enabled</span></span> |<span data-ttu-id="275b6-194">Se [persistência de dados Redis](cache-how-to-premium-persistence.md) está habilitada</span><span class="sxs-lookup"><span data-stu-id="275b6-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="275b6-195">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-195">Premium only</span></span> |
| <span data-ttu-id="275b6-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="275b6-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="275b6-197">Olá conta de armazenamento de toohello de cadeia de caracteres de conexão para [Redis a persistência de dados](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="275b6-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="275b6-198">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-198">Premium only</span></span> |
| <span data-ttu-id="275b6-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="275b6-199">rdb-backup-frequency</span></span> |<span data-ttu-id="275b6-200">Olá frequência de backup [Redis a persistência de dados](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="275b6-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="275b6-201">Somente Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-201">Premium only</span></span> |
| <span data-ttu-id="275b6-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="275b6-202">maxmemory-reserved</span></span> |<span data-ttu-id="275b6-203">Configura Olá [memória reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para processos não armazenados em cache</span><span class="sxs-lookup"><span data-stu-id="275b6-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="275b6-204">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-204">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="275b6-205">maxmemory-policy</span></span> |<span data-ttu-id="275b6-206">Configura Olá [política de remoção](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para o cache de saudação</span><span class="sxs-lookup"><span data-stu-id="275b6-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="275b6-207">Todos os tipos de preço</span><span class="sxs-lookup"><span data-stu-id="275b6-207">All pricing tiers</span></span> |
| <span data-ttu-id="275b6-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="275b6-208">notify-keyspace-events</span></span> |<span data-ttu-id="275b6-209">Configura [notificações keyspace](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="275b6-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="275b6-210">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-210">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="275b6-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="275b6-212">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="275b6-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="275b6-213">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-213">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="275b6-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="275b6-215">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="275b6-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="275b6-216">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-216">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="275b6-217">set-max-intset-entries</span></span> |<span data-ttu-id="275b6-218">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="275b6-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="275b6-219">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-219">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="275b6-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="275b6-221">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="275b6-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="275b6-222">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-222">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="275b6-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="275b6-224">Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos</span><span class="sxs-lookup"><span data-stu-id="275b6-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="275b6-225">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-225">Standard and Premium</span></span> |
| <span data-ttu-id="275b6-226">databases</span><span class="sxs-lookup"><span data-stu-id="275b6-226">databases</span></span> |<span data-ttu-id="275b6-227">Configura o número de saudação de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="275b6-227">Configures hello number of databases.</span></span> <span data-ttu-id="275b6-228">Essa propriedade pode ser configurada apenas na criação do cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="275b6-229">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="275b6-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="275b6-230">toocreate um Cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="275b6-231">Novas instâncias de Cache Redis do Azure são criadas usando Olá [AzureRmRedisCache novo](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="275b6-232">Olá primeira vez que você criar um cache Redis em uma assinatura usando Olá portal do Azure, portal Olá registra Olá `Microsoft.Cache` namespace para essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="275b6-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="275b6-233">Se você tentar toocreate Olá primeiro Redis cache em uma assinatura usando o PowerShell, você deve primeiro registrar esse namespace usando Olá comando; a seguir Caso contrário, cmdlets, como `New-AzureRmRedisCache` e `Get-AzureRmRedisCache` falhar.</span><span class="sxs-lookup"><span data-stu-id="275b6-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="275b6-234">toosee uma lista de parâmetros disponíveis e suas descrições para `New-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-235">toocreate um cache com os parâmetros padrão, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="275b6-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="275b6-236">`ResourceGroupName`, `Name`, e `Location` são parâmetros obrigatórios, mas o restante da saudação são opcional e têm valores padrão.</span><span class="sxs-lookup"><span data-stu-id="275b6-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="275b6-237">Executar o comando anterior Olá cria uma instância de padrão SKU Azure Redis Cache com o nome especificado do hello, o local e o grupo de recursos, que é de 1 GB de tamanho com a porta não SSL de saudação desabilitado.</span><span class="sxs-lookup"><span data-stu-id="275b6-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="275b6-238">toocreate um cache premium, especifique um tamanho de P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), ou P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="275b6-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="275b6-239">tooenable clustering, especifique uma contagem de fragmento usando Olá `ShardCount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="275b6-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="275b6-240">Olá exemplo a seguir cria um cache premium de P1 com 3 fragmentos.</span><span class="sxs-lookup"><span data-stu-id="275b6-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="275b6-241">Um cache premium de P1 é de 6 GB de tamanho, e como especificamos três fragmentos Olá tamanho total de 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="275b6-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="275b6-242">valores de toospecify para hello `RedisConfiguration` parâmetro, coloque valores hello dentro `{}` como chave/valor como pares `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="275b6-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="275b6-243">Olá, exemplo a seguir cria um cache padrão de 1 GB com `allkeys-random` notificações keyspace e política maxmemory configuradas com `KEA`.</span><span class="sxs-lookup"><span data-stu-id="275b6-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="275b6-244">Para obter mais informações, consulte [Notificações de keyspace (configurações avançadas)](cache-configure.md#keyspace-notifications-advanced-settings) e [Políticas de memória](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="275b6-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="275b6-245">bancos de dados do hello tooconfigure configuração durante a criação do cache</span><span class="sxs-lookup"><span data-stu-id="275b6-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="275b6-246">Olá `databases` configuração pode ser definida apenas durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="275b6-247">Olá, exemplo a seguir cria um premium P3 (26 GB) de cache com 48 bancos de dados usando Olá [AzureRmRedisCache novo](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="275b6-248">Para obter mais informações sobre Olá `databases` propriedade, consulte [configuração do servidor padrão do Azure Redis Cache](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="275b6-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="275b6-249">Para obter mais informações sobre como criar um cache usando Olá [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, consulte Olá anterior [toocreate um Cache Redis](#to-create-a-redis-cache) seção.</span><span class="sxs-lookup"><span data-stu-id="275b6-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="275b6-250">tooupdate um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="275b6-251">Instâncias de Cache Redis do Azure são atualizadas usando Olá [AzureRmRedisCache conjunto](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="275b6-252">toosee uma lista de parâmetros disponíveis e suas descrições para `Set-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-253">Olá `Set-AzureRmRedisCache` cmdlet pode ser usado tooupdate propriedades como `Size`, `Sku`, `EnableNonSslPort`e hello `RedisConfiguration` valores.</span><span class="sxs-lookup"><span data-stu-id="275b6-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="275b6-254">Olá seguinte comando atualizações Olá política máxmemória Olá Redis Cache nomeado myCache.</span><span class="sxs-lookup"><span data-stu-id="275b6-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="275b6-255">tooscale um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-255">tooscale a Redis cache</span></span>
<span data-ttu-id="275b6-256">`Set-AzureRmRedisCache`pode ser usado tooscale uma instância de cache Redis do Azure ao hello `Size`, `Sku`, ou `ShardCount` propriedades são modificadas.</span><span class="sxs-lookup"><span data-stu-id="275b6-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="275b6-257">Dimensionar um cache usando o PowerShell é o assunto toohello mesmos limites e diretrizes como dimensionar um cache de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="275b6-258">Você pode dimensionar tooa diferente preços com hello restrições a seguir.</span><span class="sxs-lookup"><span data-stu-id="275b6-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="275b6-259">Não é possível redimensionar de um maior preço camada tooa menor preço.</span><span class="sxs-lookup"><span data-stu-id="275b6-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="275b6-260">Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="275b6-261">Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="275b6-262">Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="275b6-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="275b6-263">Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.</span><span class="sxs-lookup"><span data-stu-id="275b6-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="275b6-264">Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="275b6-265">Deve ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em uma escala subsequentes operação.</span><span class="sxs-lookup"><span data-stu-id="275b6-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="275b6-266">Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.</span><span class="sxs-lookup"><span data-stu-id="275b6-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="275b6-267">Para obter mais informações, consulte [como tooScale Cache Redis do Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="275b6-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="275b6-268">Olá exemplo a seguir mostra como tooscale um cache nomeado `myCache` tooa 2,5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="275b6-269">Observe que esse comando funciona para um cache Básico ou Standard.</span><span class="sxs-lookup"><span data-stu-id="275b6-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="275b6-270">Depois que esse comando for emitido, o status de saudação do cache de saudação é retornado (semelhante toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="275b6-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="275b6-271">Observe que Olá `ProvisioningState` é `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="275b6-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="275b6-272">Quando a operação de dimensionamento de saudação for concluída, Olá `ProvisioningState` muda muito`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="275b6-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="275b6-273">Se você precisar toomake uma operação de dimensionamento subsequente, como a alteração de tooStandard básica e, em seguida, alterando o tamanho de saudação, você deve aguardar até que a operação anterior de saudação é concluída ou você receberá uma erro semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="275b6-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="275b6-274">tooget informações sobre um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="275b6-275">Você pode recuperar informações sobre um cache usando Olá [AzureRmRedisCache Get](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="275b6-276">toosee uma lista de parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-277">tooreturn informações sobre todos os caches na assinatura atual do hello, execute `Get-AzureRmRedisCache` sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="275b6-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="275b6-278">tooreturn informações sobre todos os caches em um grupo de recursos específico, execute `Get-AzureRmRedisCache` com hello `ResourceGroupName` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="275b6-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="275b6-279">tooreturn informações sobre um cache específico, execute `Get-AzureRmRedisCache` com hello `Name` parâmetro que contém o nome de saudação do cache hello e hello `ResourceGroupName` parâmetro com o grupo de recursos de saudação que contém esse cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

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

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="275b6-280">chaves de acesso de saudação tooretrieve para um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="275b6-281">chaves de acesso tooretrieve Olá para seu cache, você pode usar o hello [AzureRmRedisCacheKey Get](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="275b6-282">toosee uma lista de parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCacheKey`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-283">Olá tooretrieve chaves para seu cache, chamada hello `Get-AzureRmRedisCacheKey` cmdlet e passar no nome de saudação do cache Olá nome saudação do grupo de recursos que contém o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="275b6-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="275b6-284">tooregenerate chaves de acesso para seu cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="275b6-285">chaves de acesso tooregenerate Olá para seu cache, você pode usar o hello [AzureRmRedisCacheKey novo](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="275b6-286">toosee uma lista de parâmetros disponíveis e suas descrições para `New-AzureRmRedisCacheKey`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-287">chave de primária ou secundária de saudação de tooregenerate para seu cache, chamada hello `New-AzureRmRedisCacheKey` cmdlet e passe Olá name, grupo de recursos e especifique o `Primary` ou `Secondary` para Olá `KeyType` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="275b6-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="275b6-288">Em Olá exemplo a seguir, chave de acesso secundária Olá para um cache for regenerado.</span><span class="sxs-lookup"><span data-stu-id="275b6-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="275b6-289">toodelete um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-289">toodelete a Redis cache</span></span>
<span data-ttu-id="275b6-290">toodelete um cache Redis, use Olá [AzureRmRedisCache remover](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="275b6-291">toosee uma lista de parâmetros disponíveis e suas descrições para `Remove-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="275b6-292">Em Olá exemplo a seguir, Olá cache chamado `myCache` é removido.</span><span class="sxs-lookup"><span data-stu-id="275b6-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="275b6-293">tooimport um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-293">tooimport a Redis cache</span></span>
<span data-ttu-id="275b6-294">Você pode importar dados em uma instância de Cache Redis do Azure usando Olá `Import-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="275b6-295">A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="275b6-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="275b6-296">Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="275b6-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="275b6-297">toosee uma lista de parâmetros disponíveis e suas descrições para `Import-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="275b6-298">Olá comando a seguir importa dados de blob de saudação especificado pelo uri SAS Olá em Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="275b6-299">tooexport um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-299">tooexport a Redis cache</span></span>
<span data-ttu-id="275b6-300">Você pode exportar dados de uma instância de Cache Redis do Azure usando Olá `Export-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="275b6-301">A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="275b6-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="275b6-302">Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="275b6-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="275b6-303">toosee uma lista de parâmetros disponíveis e suas descrições para `Export-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="275b6-304">Olá comando a seguir exporta dados de uma instância de Cache Redis do Azure no contêiner de saudação especificado pelo uri SAS hello.</span><span class="sxs-lookup"><span data-stu-id="275b6-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="275b6-305">tooreboot um cache Redis</span><span class="sxs-lookup"><span data-stu-id="275b6-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="275b6-306">Você pode reinicializar a instância de Cache Redis do Azure usando Olá `Reset-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="275b6-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="275b6-307">A reinicialização está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="275b6-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="275b6-308">Para saber mais sobre a reinicialização de seu cache, confira [Administração de cache - reinicializar](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="275b6-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="275b6-309">toosee uma lista de parâmetros disponíveis e suas descrições para `Reset-AzureRmRedisCache`, execute hello seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="275b6-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="275b6-310">comando a seguir Hello reinicializa ambos os nós de saudação especificado cache.</span><span class="sxs-lookup"><span data-stu-id="275b6-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="275b6-311">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="275b6-311">Next steps</span></span>
<span data-ttu-id="275b6-312">toolearn mais sobre como usar o Windows PowerShell com o Azure, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="275b6-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="275b6-313">Documentação de cmdlet do Cache Redis do Azure no MSDN</span><span class="sxs-lookup"><span data-stu-id="275b6-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="275b6-314">[Cmdlets do Gerenciador de recursos do Azure](http://go.microsoft.com/fwlink/?LinkID=394765): Saiba mais sobre toouse Olá cmdlets no módulo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="275b6-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="275b6-315">[Usando o recurso de grupos de toomanage os recursos do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Saiba como toocreate e gerenciar grupos de recursos da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="275b6-316">[Blog do Azure](http://blogs.msdn.com/windowsazure): obtenha informações sobre os novos recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="275b6-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="275b6-317">[Blog do Windows PowerShell](http://blogs.msdn.com/powershell): obtenha informações sobre os novos recursos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="275b6-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="275b6-318">[Blog "Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): obter reais dicas e truques de saudação da comunidade do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="275b6-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

