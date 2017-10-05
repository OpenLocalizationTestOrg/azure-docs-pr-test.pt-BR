---
title: Gerenciar o Cache Redis do Azure usando a CLI do Azure | Microsoft Docs
description: "Saiba como instalar a CLI do Azure em qualquer plataforma, como usá-la para se conectar à sua conta do Azure e como criar e gerenciar um cache Redis da CLI do Azure."
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
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="1d047-103">Como criar e gerenciar o Cache Redis do Azure usando a Interface de Linha de Comando do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="1d047-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d047-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d047-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="1d047-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1d047-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="1d047-106">A CLI do Azure é uma ótima maneira de gerenciar sua infraestrutura do Azure de qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="1d047-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="1d047-107">Este artigo mostra como criar e gerenciar suas instâncias do Cache Redis do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d047-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="1d047-108">Este artigo se aplica a uma versão anterior da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d047-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="1d047-109">Para os scripts de exemplo da CLI do Azure 2.0 mais recentes, consulte [Exemplos de Cache Redis da CLI do Azure](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d047-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1d047-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d047-110">Prerequisites</span></span>
<span data-ttu-id="1d047-111">Para criar e gerenciar as instâncias do Cache Redis do Azure usando a CLI do Azure, você deverá concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1d047-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="1d047-112">Você deve ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d047-112">You must have an Azure account.</span></span> <span data-ttu-id="1d047-113">Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1d047-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="1d047-114">[Instale a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1d047-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1d047-115">Conecte sua instalação da CLI do Azure a uma conta do Azure pessoal, ou a uma conta corporativa ou de estudante do Azure, e faça logon na CLI do Azure usando o comando `azure login` .</span><span class="sxs-lookup"><span data-stu-id="1d047-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="1d047-116">Para entender as diferenças e escolher entre elas, veja [Conectar-se a uma assinatura do Azure a partir da interface de linha de comando do Azure (CLI do Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1d047-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="1d047-117">Antes de executar um dos comandos a seguir, alterne a CLI do Azure para o modo Gerenciador de Recursos executando o comando `azure config mode arm` .</span><span class="sxs-lookup"><span data-stu-id="1d047-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="1d047-118">Para obter mais informações, consulte [Use a CLI do Azure para gerenciar recursos e grupos de recursos do Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1d047-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="1d047-119">Propriedades do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="1d047-119">Redis Cache properties</span></span>
<span data-ttu-id="1d047-120">As propriedades a seguir são usadas durante a criação e a atualização de instâncias do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="1d047-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1d047-121">Property</span></span> | <span data-ttu-id="1d047-122">Switch</span><span class="sxs-lookup"><span data-stu-id="1d047-122">Switch</span></span> | <span data-ttu-id="1d047-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="1d047-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1d047-124">name</span><span class="sxs-lookup"><span data-stu-id="1d047-124">name</span></span> |<span data-ttu-id="1d047-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="1d047-125">-n, --name</span></span> |<span data-ttu-id="1d047-126">Nome do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="1d047-127">grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1d047-127">resource group</span></span> |<span data-ttu-id="1d047-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="1d047-128">-g, --resource-group</span></span> |<span data-ttu-id="1d047-129">Nome do Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="1d047-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="1d047-130">location</span><span class="sxs-lookup"><span data-stu-id="1d047-130">location</span></span> |<span data-ttu-id="1d047-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="1d047-131">-l, --location</span></span> |<span data-ttu-id="1d047-132">Local para criar o cache.</span><span class="sxs-lookup"><span data-stu-id="1d047-132">Location to create cache.</span></span> |
| <span data-ttu-id="1d047-133">tamanho</span><span class="sxs-lookup"><span data-stu-id="1d047-133">size</span></span> |<span data-ttu-id="1d047-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="1d047-134">-z, --size</span></span> |<span data-ttu-id="1d047-135">Tamanho do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-135">Size of the Redis Cache.</span></span> <span data-ttu-id="1d047-136">Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="1d047-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="1d047-137">sku</span><span class="sxs-lookup"><span data-stu-id="1d047-137">sku</span></span> |<span data-ttu-id="1d047-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="1d047-138">-x, --sku</span></span> |<span data-ttu-id="1d047-139">SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-139">Redis SKU.</span></span> <span data-ttu-id="1d047-140">Deve ser um destes: [Básico, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="1d047-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="1d047-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="1d047-141">EnableNonSslPort</span></span> |<span data-ttu-id="1d047-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="1d047-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="1d047-143">Propriedade EnableNonSslPort do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="1d047-144">Adicione este sinalizador se quiser habilitar a Porta Não SSL para o cache</span><span class="sxs-lookup"><span data-stu-id="1d047-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="1d047-145">Configuração do Redis</span><span class="sxs-lookup"><span data-stu-id="1d047-145">Redis Configuration</span></span> |<span data-ttu-id="1d047-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="1d047-146">-c, --redis-configuration</span></span> |<span data-ttu-id="1d047-147">Configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-147">Redis Configuration.</span></span> <span data-ttu-id="1d047-148">Insira uma cadeia de caracteres JSON formatada de valores e chaves de configuração aqui.</span><span class="sxs-lookup"><span data-stu-id="1d047-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="1d047-149">Format:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="1d047-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="1d047-150">Configuração do Redis</span><span class="sxs-lookup"><span data-stu-id="1d047-150">Redis Configuration</span></span> |<span data-ttu-id="1d047-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="1d047-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="1d047-152">Configuração do Redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-152">Redis Configuration.</span></span> <span data-ttu-id="1d047-153">Insira o caminho de um arquivo que contenha os valores e as chaves de configuração aqui.</span><span class="sxs-lookup"><span data-stu-id="1d047-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="1d047-154">Formato da entrada do arquivo: {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="1d047-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="1d047-155">Contagem de Fragmento</span><span class="sxs-lookup"><span data-stu-id="1d047-155">Shard Count</span></span> |<span data-ttu-id="1d047-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="1d047-156">-r, --shard-count</span></span> |<span data-ttu-id="1d047-157">Número de Fragmentos para criar um cache de Cluster Premium com clustering.</span><span class="sxs-lookup"><span data-stu-id="1d047-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="1d047-158">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="1d047-158">Virtual Network</span></span> |<span data-ttu-id="1d047-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="1d047-159">-v, --virtual-network</span></span> |<span data-ttu-id="1d047-160">Ao hospedar o cache em uma VNET, especifica a ID de recurso ARM exata da rede virtual para implantar o cache redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="1d047-161">Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="1d047-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="1d047-162">tipo de chave</span><span class="sxs-lookup"><span data-stu-id="1d047-162">key type</span></span> |<span data-ttu-id="1d047-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="1d047-163">-t, --key-type</span></span> |<span data-ttu-id="1d047-164">Tipo de chave a ser renovada.</span><span class="sxs-lookup"><span data-stu-id="1d047-164">Type of key to renew.</span></span> <span data-ttu-id="1d047-165">Valores válidos: [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="1d047-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="1d047-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="1d047-166">StaticIP</span></span> |<span data-ttu-id="1d047-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="1d047-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="1d047-168">Ao hospedar o cache em uma VNET, especifica um endereço IP exclusivo na sub-rede do cache.</span><span class="sxs-lookup"><span data-stu-id="1d047-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="1d047-169">Se ele não for fornecido, um será escolhido para você na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="1d047-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="1d047-170">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="1d047-170">Subnet</span></span> |<span data-ttu-id="1d047-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="1d047-171">t, --subnet <subnet></span></span> |<span data-ttu-id="1d047-172">Ao hospedar o cache em uma VNET, especifica o nome da sub-rede na qual implantar o cache.</span><span class="sxs-lookup"><span data-stu-id="1d047-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="1d047-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1d047-173">VirtualNetwork</span></span> |<span data-ttu-id="1d047-174">-v, --virtual-network <rede virtual></span><span class="sxs-lookup"><span data-stu-id="1d047-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="1d047-175">Ao hospedar o cache em uma VNET, especifica a ID de recurso ARM exata da rede virtual para implantar o cache redis.</span><span class="sxs-lookup"><span data-stu-id="1d047-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="1d047-176">Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="1d047-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="1d047-177">Assinatura</span><span class="sxs-lookup"><span data-stu-id="1d047-177">Subscription</span></span> |<span data-ttu-id="1d047-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="1d047-178">-s, --subscription</span></span> |<span data-ttu-id="1d047-179">O identificador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1d047-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="1d047-180">Ver todos os comandos do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="1d047-180">See all Redis Cache commands</span></span>
<span data-ttu-id="1d047-181">Para ver todos os comandos do Cache Redis e seus parâmetros, use o comando `azure rediscache -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
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
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="1d047-182">Criar um Cache Redis</span><span class="sxs-lookup"><span data-stu-id="1d047-182">Create a Redis Cache</span></span>
<span data-ttu-id="1d047-183">Para criar um Cache Redis, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="1d047-184">Para saber mais sobre esse comando, execute o comando `azure rediscache create -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="1d047-185">Excluir um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="1d047-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="1d047-186">Para excluir um Cache Redis, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="1d047-187">Para saber mais sobre esse comando, execute o comando `azure rediscache delete -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="1d047-188">Listar todos os Caches Redis em sua Assinatura ou Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="1d047-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="1d047-189">Para listar todos os Caches Redis em sua Assinatura ou Grupo de Recursos, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="1d047-190">Para saber mais sobre esse comando, execute o comando `azure rediscache list -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="1d047-191">Mostrar as propriedades de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="1d047-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="1d047-192">Para mostrar as propriedades de um Cache Redis existente, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="1d047-193">Para saber mais sobre esse comando, execute o comando `azure rediscache show -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="1d047-194">Alterar as configurações de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="1d047-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="1d047-195">Para alterar as propriedades de um Cache Redis existente, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="1d047-196">Para saber mais sobre esse comando, execute o comando `azure rediscache set -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="1d047-197">Renovar a chave de autenticação para um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="1d047-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="1d047-198">Para renovar a chave de autenticação para um Cache Redis existente, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="1d047-199">Especifique `Primary` ou `Secondary` como `key-type`.</span><span class="sxs-lookup"><span data-stu-id="1d047-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="1d047-200">Para saber mais sobre esse comando, execute o comando `azure rediscache renew-key -h`.</span><span class="sxs-lookup"><span data-stu-id="1d047-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="1d047-201">Listar as chaves Primária e Secundária de um Cache Redis existente</span><span class="sxs-lookup"><span data-stu-id="1d047-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="1d047-202">Para listar as chaves Primária e Secundária de um Cache Redis, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d047-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="1d047-203">Para saber mais sobre esse comando, execute o comando `azure rediscache list-keys -h` .</span><span class="sxs-lookup"><span data-stu-id="1d047-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
