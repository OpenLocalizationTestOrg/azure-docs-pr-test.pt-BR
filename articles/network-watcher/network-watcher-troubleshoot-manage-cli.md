---
title: "aaaTroubleshoot conexões - 2.0 do CLI do Azure e o Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como solucionar problemas de toouse Olá observador de rede do Azure 2.0 do CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="81465-103">Como solucionar problemas de conexões e gateway de rede virtual do usando a CLI do Azure 2.0 do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="81465-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="81465-104">Portal</span><span class="sxs-lookup"><span data-stu-id="81465-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="81465-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81465-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="81465-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81465-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="81465-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81465-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="81465-108">API REST</span><span class="sxs-lookup"><span data-stu-id="81465-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="81465-109">Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="81465-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="81465-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="81465-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="81465-111">Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="81465-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="81465-112">Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="81465-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="81465-113">Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="81465-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="81465-114">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="81465-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="81465-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="81465-115">Before you begin</span></span>

<span data-ttu-id="81465-116">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="81465-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="81465-117">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="81465-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="81465-118">Visão geral</span><span class="sxs-lookup"><span data-stu-id="81465-118">Overview</span></span>

<span data-ttu-id="81465-119">Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões.</span><span class="sxs-lookup"><span data-stu-id="81465-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="81465-120">Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado.</span><span class="sxs-lookup"><span data-stu-id="81465-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="81465-121">Quando inspeção estiver concluída, os resultados de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="81465-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="81465-122">Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado.</span><span class="sxs-lookup"><span data-stu-id="81465-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="81465-123">logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.</span><span class="sxs-lookup"><span data-stu-id="81465-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="81465-124">Como recuperar uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="81465-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="81465-125">Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="81465-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="81465-126">Você também pode passá-lo por um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="81465-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="81465-127">Olá cmdlet a seguir lista Olá-conexões vpn em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="81465-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="81465-128">Depois que você tem o nome de saudação do conexão Olá, você pode executar esse comando tooget sua Id de recurso:</span><span class="sxs-lookup"><span data-stu-id="81465-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="81465-129">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="81465-129">Create a storage account</span></span>

<span data-ttu-id="81465-130">Solução de problemas de recurso retorna dados sobre integridade de saudação do recurso hello, ele também salva logs tooa armazenamento conta toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="81465-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="81465-131">Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.</span><span class="sxs-lookup"><span data-stu-id="81465-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="81465-132">Criar conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="81465-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="81465-133">Obter chaves de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="81465-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="81465-134">Criar contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="81465-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="81465-135">Como executar a solução de problemas de recursos do Observador de rede</span><span class="sxs-lookup"><span data-stu-id="81465-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="81465-136">Solucionar problemas de recursos com hello `az network watcher troubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="81465-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="81465-137">Passamos o grupo de recursos de Olá Olá cmdlet, nome da saudação observador de rede, Olá Id de conexão de saudação Olá Olá Id da conta de armazenamento hello e Olá toostore do hello caminho toohello blob solucionar resulta em.</span><span class="sxs-lookup"><span data-stu-id="81465-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="81465-138">Depois de executar o cmdlet Olá, observador de rede revisa a integridade de Olá Olá recursos tooverify.</span><span class="sxs-lookup"><span data-stu-id="81465-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="81465-139">Ele retorna resultados de saudação toohello shell e armazena logs de resultados Olá Olá conta de armazenamento especificado.</span><span class="sxs-lookup"><span data-stu-id="81465-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="81465-140">Entendendo os resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="81465-140">Understanding hello results</span></span>

<span data-ttu-id="81465-141">texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="81465-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="81465-142">Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais.</span><span class="sxs-lookup"><span data-stu-id="81465-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="81465-143">No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="81465-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="81465-144">Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="81465-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="81465-145">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="81465-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="81465-146">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="81465-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="81465-147">Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="81465-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="81465-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81465-148">Next steps</span></span>

<span data-ttu-id="81465-149">Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="81465-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
