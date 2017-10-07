---
title: aaaManage Cache Redis do Azure usando a CLI do Azure | Microsoft Docs
description: "Saiba como tooinstall Olá CLI do Azure em qualquer plataforma, como toouse-tooconnect tooyour conta do Azure e como toocreate e gerenciar um cache Redis da saudação CLI do Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="f8a85-103">Como toocreate e gerenciar o Cache Redis do Azure usando hello Azure Interface de linha de comando (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="f8a85-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8a85-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8a85-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="f8a85-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f8a85-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="f8a85-106">Olá CLI do Azure é uma ótima maneira toomanage sua infraestrutura do Azure de qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="f8a85-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="f8a85-107">Este artigo mostra como toocreate e gerenciar suas instâncias de Cache Redis do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a85-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a85-108">Este artigo se aplica a versão anterior do tooa da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a85-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="f8a85-109">Para scripts de exemplo 2.0 do CLI do Azure mais recentes hello, consulte [exemplos de cache Redis do Azure CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f8a85-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f8a85-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8a85-110">Prerequisites</span></span>
<span data-ttu-id="f8a85-111">toocreate e gerenciar instâncias de Cache Redis do Azure usando a CLI do Azure, você deve concluir Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8a85-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="f8a85-112">Você deve ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a85-112">You must have an Azure account.</span></span> <span data-ttu-id="f8a85-113">Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f8a85-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="f8a85-114">[Instalar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f8a85-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f8a85-115">Conecte-se a instalação da CLI do Azure com uma conta do Azure pessoal ou com um trabalho ou escola conta do Azure e fazer logon em Olá CLI do Azure usando Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="f8a85-116">toounderstand Olá diferenças e escolher, consulte [conectar tooan assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f8a85-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="f8a85-117">Antes de executar qualquer um dos comandos a seguir de saudação, comutador hello CLI do Azure no modo do Gerenciador de recursos executando Olá `azure config mode arm` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="f8a85-118">Para obter mais informações, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f8a85-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="f8a85-119">Propriedades do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-119">Redis Cache properties</span></span>
<span data-ttu-id="f8a85-120">propriedades seguintes Hello são usadas ao criar e atualizar instâncias de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="f8a85-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f8a85-121">Property</span></span> | <span data-ttu-id="f8a85-122">Switch</span><span class="sxs-lookup"><span data-stu-id="f8a85-122">Switch</span></span> | <span data-ttu-id="f8a85-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8a85-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8a85-124">name</span><span class="sxs-lookup"><span data-stu-id="f8a85-124">name</span></span> |<span data-ttu-id="f8a85-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="f8a85-125">-n, --name</span></span> |<span data-ttu-id="f8a85-126">Nome da saudação Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="f8a85-127">grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f8a85-127">resource group</span></span> |<span data-ttu-id="f8a85-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="f8a85-128">-g, --resource-group</span></span> |<span data-ttu-id="f8a85-129">Nome da saudação grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8a85-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="f8a85-130">location</span><span class="sxs-lookup"><span data-stu-id="f8a85-130">location</span></span> |<span data-ttu-id="f8a85-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="f8a85-131">-l, --location</span></span> |<span data-ttu-id="f8a85-132">Cache de toocreate local.</span><span class="sxs-lookup"><span data-stu-id="f8a85-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="f8a85-133">tamanho</span><span class="sxs-lookup"><span data-stu-id="f8a85-133">size</span></span> |<span data-ttu-id="f8a85-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="f8a85-134">-z, --size</span></span> |<span data-ttu-id="f8a85-135">Tamanho do Cache Redis da saudação.</span><span class="sxs-lookup"><span data-stu-id="f8a85-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="f8a85-136">Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="f8a85-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="f8a85-137">sku</span><span class="sxs-lookup"><span data-stu-id="f8a85-137">sku</span></span> |<span data-ttu-id="f8a85-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="f8a85-138">-x, --sku</span></span> |<span data-ttu-id="f8a85-139">SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-139">Redis SKU.</span></span> <span data-ttu-id="f8a85-140">Deve ser um destes: [Básico, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="f8a85-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="f8a85-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="f8a85-141">EnableNonSslPort</span></span> |<span data-ttu-id="f8a85-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="f8a85-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="f8a85-143">Propriedade EnableNonSslPort de saudação Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="f8a85-144">Adicione esse sinalizador se você quiser tooenable Olá não SSL porta para o cache</span><span class="sxs-lookup"><span data-stu-id="f8a85-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="f8a85-145">Configuração do Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-145">Redis Configuration</span></span> |<span data-ttu-id="f8a85-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="f8a85-146">-c, --redis-configuration</span></span> |<span data-ttu-id="f8a85-147">Configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-147">Redis Configuration.</span></span> <span data-ttu-id="f8a85-148">Insira uma cadeia de caracteres JSON formatada de valores e chaves de configuração aqui.</span><span class="sxs-lookup"><span data-stu-id="f8a85-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="f8a85-149">Format:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="f8a85-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="f8a85-150">Configuração do Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-150">Redis Configuration</span></span> |<span data-ttu-id="f8a85-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="f8a85-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="f8a85-152">Configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="f8a85-152">Redis Configuration.</span></span> <span data-ttu-id="f8a85-153">Insira o caminho de saudação de um arquivo que contém as chaves de configuração e os valores aqui.</span><span class="sxs-lookup"><span data-stu-id="f8a85-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="f8a85-154">Formato de entrada do arquivo hello: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="f8a85-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="f8a85-155">Contagem de Fragmento</span><span class="sxs-lookup"><span data-stu-id="f8a85-155">Shard Count</span></span> |<span data-ttu-id="f8a85-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="f8a85-156">-r, --shard-count</span></span> |<span data-ttu-id="f8a85-157">Número de fragmentos toocreate em um Cache de Cluster Premium com o cluster.</span><span class="sxs-lookup"><span data-stu-id="f8a85-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="f8a85-158">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="f8a85-158">Virtual Network</span></span> |<span data-ttu-id="f8a85-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="f8a85-159">-v, --virtual-network</span></span> |<span data-ttu-id="f8a85-160">Quando seu cache em uma rede virtual de hospedagem Especifica Olá exata ARM ID de recurso Olá Olá de toodeploy de rede virtual redis cache no.</span><span class="sxs-lookup"><span data-stu-id="f8a85-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="f8a85-161">Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="f8a85-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="f8a85-162">tipo de chave</span><span class="sxs-lookup"><span data-stu-id="f8a85-162">key type</span></span> |<span data-ttu-id="f8a85-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="f8a85-163">-t, --key-type</span></span> |<span data-ttu-id="f8a85-164">Tipo de chave toorenew.</span><span class="sxs-lookup"><span data-stu-id="f8a85-164">Type of key toorenew.</span></span> <span data-ttu-id="f8a85-165">Valores válidos: [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="f8a85-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="f8a85-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="f8a85-166">StaticIP</span></span> |<span data-ttu-id="f8a85-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="f8a85-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="f8a85-168">Ao hospedar o cache em uma rede virtual, especifica um endereço IP exclusivo na sub-rede Olá para o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8a85-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="f8a85-169">Se não for fornecido, um é escolhido para você de sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="f8a85-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="f8a85-170">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="f8a85-170">Subnet</span></span> |<span data-ttu-id="f8a85-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="f8a85-171">t, --subnet <subnet></span></span> |<span data-ttu-id="f8a85-172">Ao hospedar o cache em uma rede virtual, especifica o nome de saudação de sub-rede de saudação no cache de saudação que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f8a85-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="f8a85-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f8a85-173">VirtualNetwork</span></span> |<span data-ttu-id="f8a85-174">-v, --virtual-network <rede virtual></span><span class="sxs-lookup"><span data-stu-id="f8a85-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="f8a85-175">Quando seu cache em uma rede virtual de hospedagem Especifica Olá exata ARM ID de recurso Olá Olá de toodeploy de rede virtual redis cache no.</span><span class="sxs-lookup"><span data-stu-id="f8a85-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="f8a85-176">Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="f8a85-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="f8a85-177">Assinatura</span><span class="sxs-lookup"><span data-stu-id="f8a85-177">Subscription</span></span> |<span data-ttu-id="f8a85-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="f8a85-178">-s, --subscription</span></span> |<span data-ttu-id="f8a85-179">Identificador de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8a85-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="f8a85-180">Ver todos os comandos do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-180">See all Redis Cache commands</span></span>
<span data-ttu-id="f8a85-181">toosee todos os comandos de Redis Cache e seus parâmetros, use Olá `azure rediscache -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="f8a85-182">Criar um Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-182">Create a Redis Cache</span></span>
<span data-ttu-id="f8a85-183">toocreate um Cache Redis, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="f8a85-184">Para obter mais informações sobre esse comando, execute Olá `azure rediscache create -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="f8a85-185">Excluir um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="f8a85-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="f8a85-186">toodelete um Cache Redis, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="f8a85-187">Para obter mais informações sobre esse comando, execute Olá `azure rediscache delete -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="f8a85-188">Listar todos os Caches Redis em sua Assinatura ou Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="f8a85-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="f8a85-189">toolist todos os Caches Redis dentro de sua assinatura ou grupo de recursos, use Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f8a85-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="f8a85-190">Para obter mais informações sobre esse comando, execute Olá `azure rediscache list -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="f8a85-191">Mostrar as propriedades de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="f8a85-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="f8a85-192">tooshow propriedades de um Cache Redis existente, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="f8a85-193">Para obter mais informações sobre esse comando, execute Olá `azure rediscache show -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="f8a85-194">Alterar as configurações de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="f8a85-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="f8a85-195">toochange configurações de um Cache Redis existente, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="f8a85-196">Para obter mais informações sobre esse comando, execute Olá `azure rediscache set -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="f8a85-197">Renovar a chave de autenticação Olá para um Cache existente Redis</span><span class="sxs-lookup"><span data-stu-id="f8a85-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="f8a85-198">chave de autenticação toorenew Olá para um Redis Cache existente, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="f8a85-199">Especifique `Primary` ou `Secondary` como `key-type`.</span><span class="sxs-lookup"><span data-stu-id="f8a85-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="f8a85-200">Para obter mais informações sobre esse comando, execute Olá `azure rediscache renew-key -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="f8a85-201">Listar as chaves Primária e Secundária de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="f8a85-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="f8a85-202">as chaves primária e secundária toolist de um Cache Redis existente, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8a85-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="f8a85-203">Para obter mais informações sobre esse comando, execute Olá `azure rediscache list-keys -h` comando.</span><span class="sxs-lookup"><span data-stu-id="f8a85-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
