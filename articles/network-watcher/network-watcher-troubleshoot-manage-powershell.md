---
title: "Solução de problemas de conexões e do gateway de rede virtual do Azure - PowerShell | Microsoft Docs"
description: "Esta página explica como usar o cmdlet do PowerShell para solucionar problemas do Observador de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="94d71-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="94d71-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="94d71-104">Portal</span><span class="sxs-lookup"><span data-stu-id="94d71-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="94d71-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d71-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="94d71-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="94d71-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="94d71-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94d71-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="94d71-108">API REST</span><span class="sxs-lookup"><span data-stu-id="94d71-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="94d71-109">O observador de rede oferece muitos recursos que dizem respeito às noções básicas sobre os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="94d71-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="94d71-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="94d71-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="94d71-111">A solução de problemas de recursos pode ser chamada pelo Portal, pelo PowerShell, pela CLI ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="94d71-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="94d71-112">Quando chamado, o Observador de rede inspeciona a integridade de uma conexão ou um gateway de rede virtual e faz um relatório sobre suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="94d71-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="94d71-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="94d71-113">Before you begin</span></span>

<span data-ttu-id="94d71-114">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="94d71-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="94d71-115">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="94d71-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="94d71-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="94d71-116">Overview</span></span>

<span data-ttu-id="94d71-117">A solução de problemas de recursos fornece a capacidade de solucionar problemas que podem surgir com as conexões e o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="94d71-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="94d71-118">Quando uma solução de problemas de recursos recebe uma solicitação, os logs são consultados e inspecionadas.</span><span class="sxs-lookup"><span data-stu-id="94d71-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="94d71-119">Quando a inspeção estiver concluída, você receberá um relatório com os resultados.</span><span class="sxs-lookup"><span data-stu-id="94d71-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="94d71-120">As solicitações da solução de problemas de recursos são solicitações de execução longa e podem demorar para gerar um relatório.</span><span class="sxs-lookup"><span data-stu-id="94d71-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="94d71-121">Os logs de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="94d71-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="94d71-122">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="94d71-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="94d71-123">A primeira etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="94d71-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="94d71-124">A variável `$networkWatcher` é passada para o cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="94d71-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="94d71-125">Como recuperar uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="94d71-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="94d71-126">Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="94d71-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="94d71-127">Você também pode passá-lo por um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="94d71-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="94d71-128">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="94d71-128">Create a storage account</span></span>

<span data-ttu-id="94d71-129">A solução de problemas de recursos produz relatório de dados sobre a integridade do recurso, ela também salva os logs em uma conta de armazenamento a ser revisada.</span><span class="sxs-lookup"><span data-stu-id="94d71-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="94d71-130">Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.</span><span class="sxs-lookup"><span data-stu-id="94d71-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="94d71-131">Como executar a solução de problemas de recursos do Observador de rede</span><span class="sxs-lookup"><span data-stu-id="94d71-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="94d71-132">Você usa o cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` para solucionar problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="94d71-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="94d71-133">Passamos o cmdlet do objeto do Observador de Rede, a Id da Conexão ou Gateway de Rede Virtual, a id da conta de armazenamento e o caminho para armazenar os resultados.</span><span class="sxs-lookup"><span data-stu-id="94d71-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="94d71-134">O cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` é demorado e pode levar alguns minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="94d71-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="94d71-135">Depois que você executar o cmdlet, o Observador de rede revisará o recurso para verificar a integridade.</span><span class="sxs-lookup"><span data-stu-id="94d71-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="94d71-136">Ele envia um relatório com os resultados para o shell e armazena os logs dos resultados na conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="94d71-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="94d71-137">Como entender os resultados</span><span class="sxs-lookup"><span data-stu-id="94d71-137">Understanding the results</span></span>

<span data-ttu-id="94d71-138">O texto de ação fornece orientação geral sobre como resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="94d71-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="94d71-139">Se for possível executar uma ação para solucionar o problema, você receberá um link com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="94d71-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="94d71-140">Nos casos em que não há orientações adicionais, a resposta fornecerá a url para abrir um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="94d71-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="94d71-141">Para obter mais informações sobre as propriedades da resposta e o do que está incluído, acesse [Visão geral da solução de problemas do observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="94d71-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="94d71-142">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do Azure, confira [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="94d71-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="94d71-143">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="94d71-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="94d71-144">Para obter mais informações sobre o Gerenciador de armazenamento acesse o link: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="94d71-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="94d71-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94d71-145">Next steps</span></span>

<span data-ttu-id="94d71-146">Se as configurações para a conectividade VPN foram alteradas, confira [Gerenciamento de grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para acompanhar quais são as regras de segurança e o grupo de segurança de rede envolvidos na questão.</span><span class="sxs-lookup"><span data-stu-id="94d71-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
