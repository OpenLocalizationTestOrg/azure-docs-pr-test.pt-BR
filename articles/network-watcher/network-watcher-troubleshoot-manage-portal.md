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
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="c9e03-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e03-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c9e03-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c9e03-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="c9e03-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9e03-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="c9e03-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c9e03-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="c9e03-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c9e03-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="c9e03-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c9e03-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="c9e03-109">O observador de rede oferece muitos recursos que dizem respeito às noções básicas sobre os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e03-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="c9e03-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9e03-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="c9e03-111">A solução de problemas de recursos pode ser chamada pelo Portal, pelo PowerShell, pela CLI ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="c9e03-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c9e03-112">Quando chamado, o Observador de rede inspeciona a integridade de uma conexão ou um gateway de rede virtual e faz um relatório sobre suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="c9e03-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c9e03-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c9e03-113">Before you begin</span></span>

<span data-ttu-id="c9e03-114">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="c9e03-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="c9e03-115">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="c9e03-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="c9e03-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c9e03-116">Overview</span></span>

<span data-ttu-id="c9e03-117">A solução de problemas de recursos fornece a capacidade de solucionar problemas que podem surgir com as conexões e o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c9e03-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c9e03-118">Quando uma solução de problemas de recursos recebe uma solicitação, os logs são consultados e inspecionadas.</span><span class="sxs-lookup"><span data-stu-id="c9e03-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="c9e03-119">Quando a inspeção estiver concluída, você receberá um relatório com os resultados.</span><span class="sxs-lookup"><span data-stu-id="c9e03-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="c9e03-120">As solicitações da solução de problemas de recursos são solicitações de execução longa e podem demorar para gerar um relatório.</span><span class="sxs-lookup"><span data-stu-id="c9e03-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="c9e03-121">Os logs de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="c9e03-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="c9e03-122">Solucionar problemas de um gateway ou conexão</span><span class="sxs-lookup"><span data-stu-id="c9e03-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="c9e03-123">Navegue até o [Portal do Azure](https://portal.azure.com) e clique em **Rede** > **Observador de Rede** > **Diagnósticos de VPN**</span><span class="sxs-lookup"><span data-stu-id="c9e03-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="c9e03-124">Selecione uma **Assinatura**, **Grupo de Recursos** e **Local**.</span><span class="sxs-lookup"><span data-stu-id="c9e03-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="c9e03-125">A solução de problemas de recurso retorna dados sobre a integridade do recurso.</span><span class="sxs-lookup"><span data-stu-id="c9e03-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="c9e03-126">Ela também salva os logs relevantes para uma conta de armazenamento a ser examinada.</span><span class="sxs-lookup"><span data-stu-id="c9e03-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="c9e03-127">Clique em **Conta de Armazenamento** para selecionar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c9e03-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="c9e03-128">Na folha **Configurações da conta**, selecione uma conta de armazenamento existente ou clique em **+ Conta de armazenamento** para criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="c9e03-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="c9e03-129">Na folha **Contêineres**, escolha um contêiner existente ou clique em **+ Contêiner** para criar um novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="c9e03-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="c9e03-130">Quando concluído, clique em **Selecionar**</span><span class="sxs-lookup"><span data-stu-id="c9e03-130">When complete click **Select**</span></span>
6. <span data-ttu-id="c9e03-131">Selecione os recursos de Gateway e de Conexão para solucionar problemas e clique em **Iniciar Solução de Problemas**</span><span class="sxs-lookup"><span data-stu-id="c9e03-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="c9e03-132">Se vários recursos forem selecionados, a solução de problemas será executada simultaneamente em recursos de gateway.</span><span class="sxs-lookup"><span data-stu-id="c9e03-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="c9e03-133">Ela não pode ser executada em uma conexão e no respectivo gateway associado simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c9e03-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="c9e03-134">É recomendável solucionar problemas de gateways primeiro, pois a solução de problemas de conexão é um processo mais longo.</span><span class="sxs-lookup"><span data-stu-id="c9e03-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="c9e03-135">Enquanto o diagnóstico de VPN estiver em execução em um recurso, a coluna **STATUS DE SOLUÇÃO DE PROBLEMAS** mostrará um status de **Em execução**</span><span class="sxs-lookup"><span data-stu-id="c9e03-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="c9e03-136">Quando concluído, a coluna de status é alterada para **Íntegro** ou **Não íntegro**.</span><span class="sxs-lookup"><span data-stu-id="c9e03-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![Solução de problemas concluída][2]

## <a name="understanding-the-results"></a><span data-ttu-id="c9e03-138">Como entender os resultados</span><span class="sxs-lookup"><span data-stu-id="c9e03-138">Understanding the results</span></span>

<span data-ttu-id="c9e03-139">Na seção **Detalhes** da janela, a guia **Status** mostra o status da última solução de problemas executada no recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="c9e03-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="c9e03-140">Os resultados do diagnóstico mais recente são mostrados xx minutos após a última execução.</span><span class="sxs-lookup"><span data-stu-id="c9e03-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="c9e03-141">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c9e03-141">Property</span></span>  |<span data-ttu-id="c9e03-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="c9e03-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="c9e03-143">Recurso</span><span class="sxs-lookup"><span data-stu-id="c9e03-143">Resource</span></span>     | <span data-ttu-id="c9e03-144">Um link para o recurso.</span><span class="sxs-lookup"><span data-stu-id="c9e03-144">A link to the resource.</span></span>        |
|<span data-ttu-id="c9e03-145">Caminho de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c9e03-145">Storage path</span></span>     |  <span data-ttu-id="c9e03-146">Caminho para a conta de armazenamento e o contêiner que contêm os logs (se algum foi produzido durante a execução).</span><span class="sxs-lookup"><span data-stu-id="c9e03-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="c9e03-147">Essa configuração não persiste depois de você sair do portal.</span><span class="sxs-lookup"><span data-stu-id="c9e03-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="c9e03-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="c9e03-148">Summary</span></span>     | <span data-ttu-id="c9e03-149">Resumo da integridade do recurso.</span><span class="sxs-lookup"><span data-stu-id="c9e03-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="c9e03-150">Detalhes</span><span class="sxs-lookup"><span data-stu-id="c9e03-150">Detail</span></span>     | <span data-ttu-id="c9e03-151">Informações detalhadas sobre a integridade do recurso.</span><span class="sxs-lookup"><span data-stu-id="c9e03-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="c9e03-152">Última execução</span><span class="sxs-lookup"><span data-stu-id="c9e03-152">Last run</span></span>     | <span data-ttu-id="c9e03-153">A hora em que a solução de problemas foi executada pela última vez.</span><span class="sxs-lookup"><span data-stu-id="c9e03-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="c9e03-154">A guia **Ação** fornece diretrizes gerais sobre como resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="c9e03-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="c9e03-155">Se for possível executar uma ação para solucionar o problema, você receberá um link com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="c9e03-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="c9e03-156">Nos casos em que não há orientações adicionais, a resposta fornecerá a url para abrir um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="c9e03-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="c9e03-157">Para obter mais informações sobre as propriedades da resposta e o do que está incluído, acesse [Visão geral da solução de problemas do observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c9e03-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="c9e03-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9e03-158">Next steps</span></span>

<span data-ttu-id="c9e03-159">Se as configurações para a conectividade VPN foram alteradas, confira [Gerenciamento de grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para acompanhar quais são as regras de segurança e o grupo de segurança de rede envolvidos na questão.</span><span class="sxs-lookup"><span data-stu-id="c9e03-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
