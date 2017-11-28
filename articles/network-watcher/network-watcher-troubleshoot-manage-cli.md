---
title: "Solução de problemas de Conexões e do Gateway de Rede Virtual do Azure – CLI do Azure 2.0 | Microsoft Docs"
description: "Esta página explica como usar a solução de problemas da CLI do Azure 2.0 do Observador de Rede do Azure"
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
ms.openlocfilehash: e1d56317b10fa738a3d7089f6c4f357159fe2c2b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="40d5c-103">Como solucionar problemas de conexões e gateway de rede virtual do usando a CLI do Azure 2.0 do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="40d5c-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="40d5c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="40d5c-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="40d5c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40d5c-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="40d5c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="40d5c-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="40d5c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40d5c-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="40d5c-108">API REST</span><span class="sxs-lookup"><span data-stu-id="40d5c-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="40d5c-109">O observador de rede oferece muitos recursos que dizem respeito às noções básicas sobre os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="40d5c-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="40d5c-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="40d5c-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="40d5c-111">A solução de problemas de recursos pode ser chamada pelo Portal, pelo PowerShell, pela CLI ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="40d5c-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="40d5c-112">Quando chamado, o Observador de rede inspeciona a integridade de uma conexão ou um gateway de rede virtual e faz um relatório sobre suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="40d5c-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="40d5c-113">Este artigo usa nossa CLI de próxima geração para o modelo de implantação do gerenciamento de recursos, CLI do Azure 2.0, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="40d5c-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="40d5c-114">Para executar as etapas deste artigo, será necessário [instalar a Interface de Linha de Comando do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="40d5c-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="40d5c-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="40d5c-115">Before you begin</span></span>

<span data-ttu-id="40d5c-116">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="40d5c-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="40d5c-117">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="40d5c-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="40d5c-118">Visão geral</span><span class="sxs-lookup"><span data-stu-id="40d5c-118">Overview</span></span>

<span data-ttu-id="40d5c-119">A solução de problemas de recursos fornece a capacidade de solucionar problemas que podem surgir com as conexões e o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="40d5c-119">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="40d5c-120">Quando uma solução de problemas de recursos recebe uma solicitação, os logs são consultados e inspecionadas.</span><span class="sxs-lookup"><span data-stu-id="40d5c-120">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="40d5c-121">Quando a inspeção estiver concluída, você receberá um relatório com os resultados.</span><span class="sxs-lookup"><span data-stu-id="40d5c-121">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="40d5c-122">As solicitações da solução de problemas de recursos são solicitações de execução longa e podem demorar para gerar um relatório.</span><span class="sxs-lookup"><span data-stu-id="40d5c-122">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="40d5c-123">Os logs de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="40d5c-123">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="40d5c-124">Como recuperar uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="40d5c-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="40d5c-125">Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="40d5c-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="40d5c-126">Você também pode passá-lo por um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="40d5c-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="40d5c-127">O cmdlet a seguir lista as conexões vpn em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="40d5c-127">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="40d5c-128">Assim que você tiver o nome da conexão, poderá executar esse comando para obter sua ID de recurso:</span><span class="sxs-lookup"><span data-stu-id="40d5c-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="40d5c-129">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40d5c-129">Create a storage account</span></span>

<span data-ttu-id="40d5c-130">A solução de problemas de recursos produz relatório de dados sobre a integridade do recurso, ela também salva os logs em uma conta de armazenamento a ser revisada.</span><span class="sxs-lookup"><span data-stu-id="40d5c-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="40d5c-131">Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.</span><span class="sxs-lookup"><span data-stu-id="40d5c-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="40d5c-132">Criar a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40d5c-132">Create the storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="40d5c-133">Obter as chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40d5c-133">Get the storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="40d5c-134">Criar o contêiner</span><span class="sxs-lookup"><span data-stu-id="40d5c-134">Create the container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="40d5c-135">Como executar a solução de problemas de recursos do Observador de rede</span><span class="sxs-lookup"><span data-stu-id="40d5c-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="40d5c-136">Você usa o cmdlet `az network watcher troubleshooting` para solucionar problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="40d5c-136">You troubleshoot resources with the `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="40d5c-137">Aprovamos o cmdlet no grupo de recursos, no nome do Observador de rede, no ID da conexão, no ID da conta de armazenamento e no caminho para o blob para armazenar o resultado da solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="40d5c-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="40d5c-138">Depois que você executar o cmdlet, o Observador de rede revisará o recurso para verificar a integridade.</span><span class="sxs-lookup"><span data-stu-id="40d5c-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="40d5c-139">Ele envia um relatório com os resultados para o shell e armazena os logs dos resultados na conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="40d5c-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="40d5c-140">Como entender os resultados</span><span class="sxs-lookup"><span data-stu-id="40d5c-140">Understanding the results</span></span>

<span data-ttu-id="40d5c-141">O texto de ação fornece orientação geral sobre como resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="40d5c-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="40d5c-142">Se for possível executar uma ação para solucionar o problema, você receberá um link com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="40d5c-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="40d5c-143">Nos casos em que não há orientações adicionais, a resposta fornecerá a url para abrir um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="40d5c-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="40d5c-144">Para obter mais informações sobre as propriedades da resposta e o do que está incluído, acesse [Visão geral da solução de problemas do observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="40d5c-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="40d5c-145">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do Azure, confira [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="40d5c-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="40d5c-146">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="40d5c-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="40d5c-147">Para obter mais informações sobre o Gerenciador de armazenamento acesse o link: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="40d5c-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="40d5c-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40d5c-148">Next steps</span></span>

<span data-ttu-id="40d5c-149">Se as configurações para a conectividade VPN foram alteradas, confira [Gerenciamento de grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para acompanhar quais são as regras de segurança e o grupo de segurança de rede envolvidos na questão.</span><span class="sxs-lookup"><span data-stu-id="40d5c-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
