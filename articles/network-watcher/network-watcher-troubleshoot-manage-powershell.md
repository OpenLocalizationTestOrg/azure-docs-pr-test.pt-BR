---
title: "aaaTroubleshoot conexões - PowerShell e o Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como toouse Olá observador de rede do Azure solucionar problemas do cmdlet do PowerShell"
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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="ea380-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="ea380-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ea380-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ea380-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="ea380-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea380-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="ea380-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ea380-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="ea380-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ea380-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="ea380-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ea380-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="ea380-109">Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="ea380-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="ea380-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea380-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="ea380-111">Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="ea380-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ea380-112">Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="ea380-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea380-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ea380-113">Before you begin</span></span>

<span data-ttu-id="ea380-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="ea380-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="ea380-115">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="ea380-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="ea380-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ea380-116">Overview</span></span>

<span data-ttu-id="ea380-117">Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões.</span><span class="sxs-lookup"><span data-stu-id="ea380-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="ea380-118">Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado.</span><span class="sxs-lookup"><span data-stu-id="ea380-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="ea380-119">Quando inspeção estiver concluída, os resultados de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="ea380-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="ea380-120">Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado.</span><span class="sxs-lookup"><span data-stu-id="ea380-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="ea380-121">logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.</span><span class="sxs-lookup"><span data-stu-id="ea380-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="ea380-122">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="ea380-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="ea380-123">Olá primeira etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="ea380-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ea380-124">Olá `$networkWatcher` variável é passada toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="ea380-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="ea380-125">Como recuperar uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="ea380-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="ea380-126">Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="ea380-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="ea380-127">Você também pode passá-lo por um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ea380-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="ea380-128">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ea380-128">Create a storage account</span></span>

<span data-ttu-id="ea380-129">Solução de problemas de recurso retorna dados sobre integridade de saudação do recurso hello, ele também salva logs tooa armazenamento conta toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="ea380-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="ea380-130">Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.</span><span class="sxs-lookup"><span data-stu-id="ea380-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="ea380-131">Como executar a solução de problemas de recursos do Observador de rede</span><span class="sxs-lookup"><span data-stu-id="ea380-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="ea380-132">Solucionar problemas de recursos com hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ea380-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="ea380-133">Passamos Olá cmdlet Olá observador de rede objeto, Olá Id de Conexão de saudação ou Gateway de rede Virtual, id de conta de armazenamento Olá e resultados de Olá Olá caminho toostore.</span><span class="sxs-lookup"><span data-stu-id="ea380-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="ea380-134">Olá `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet é demorado e pode levar toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ea380-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="ea380-135">Depois de executar o cmdlet Olá, observador de rede revisa a integridade de Olá Olá recursos tooverify.</span><span class="sxs-lookup"><span data-stu-id="ea380-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="ea380-136">Ele retorna resultados de saudação toohello shell e armazena logs de resultados Olá Olá conta de armazenamento especificado.</span><span class="sxs-lookup"><span data-stu-id="ea380-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="ea380-137">Entendendo os resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="ea380-137">Understanding hello results</span></span>

<span data-ttu-id="ea380-138">texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="ea380-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="ea380-139">Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais.</span><span class="sxs-lookup"><span data-stu-id="ea380-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="ea380-140">No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="ea380-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="ea380-141">Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ea380-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="ea380-142">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="ea380-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="ea380-143">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea380-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="ea380-144">Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="ea380-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea380-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea380-145">Next steps</span></span>

<span data-ttu-id="ea380-146">Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="ea380-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
