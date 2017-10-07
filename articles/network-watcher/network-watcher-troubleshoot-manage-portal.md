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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="ae3b8-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="ae3b8-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ae3b8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ae3b8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="ae3b8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae3b8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="ae3b8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ae3b8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="ae3b8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ae3b8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="ae3b8-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ae3b8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="ae3b8-109">Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="ae3b8-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="ae3b8-111">Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ae3b8-112">Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae3b8-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ae3b8-113">Before you begin</span></span>

<span data-ttu-id="ae3b8-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="ae3b8-115">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="ae3b8-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="ae3b8-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ae3b8-116">Overview</span></span>

<span data-ttu-id="ae3b8-117">Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="ae3b8-118">Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="ae3b8-119">Quando inspeção estiver concluída, os resultados de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="ae3b8-120">Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="ae3b8-121">logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="ae3b8-122">Solucionar problemas de um gateway ou conexão</span><span class="sxs-lookup"><span data-stu-id="ae3b8-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="ae3b8-123">Navegue toohello [portal do Azure](https://portal.azure.com) e clique em **rede** > **observador de rede** > **diagnóstico de VPN**</span><span class="sxs-lookup"><span data-stu-id="ae3b8-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="ae3b8-124">Selecione uma **Assinatura**, **Grupo de Recursos** e **Local**.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="ae3b8-125">Solução de problemas de recurso retorna dados sobre a integridade de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="ae3b8-126">Ele também salva a conta de armazenamento tooa logs relevantes toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="ae3b8-127">Clique em **conta de armazenamento** tooselect uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="ae3b8-128">Em Olá **contas de armazenamento** folha, selecione uma conta de armazenamento existente ou clique em **+ conta de armazenamento** toocreate um novo.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="ae3b8-129">Em Olá **contêineres** folha, escolha um contêiner existente ou clique em **+ contêiner** toocreate um novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="ae3b8-130">Quando concluído, clique em **Selecionar**</span><span class="sxs-lookup"><span data-stu-id="ae3b8-130">When complete click **Select**</span></span>
6. <span data-ttu-id="ae3b8-131">Selecione Olá tootroubleshoot de recursos de Gateway e de Conexão e clique em **Iniciar de solução de problemas**</span><span class="sxs-lookup"><span data-stu-id="ae3b8-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="ae3b8-132">Se vários recursos forem selecionados, a solução de problemas será executada simultaneamente em recursos de gateway.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="ae3b8-133">Não pode ser executada em uma conexão e o gateway em Olá associado simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="ae3b8-134">É recomendável tootroubleshoot gateways primeiro a solução de problemas de conexão é um processo mais longo.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="ae3b8-135">Enquanto o diagnóstico de VPN está em execução em uma saudação do recurso **TROUBLESHOOTING STATUS** coluna mostrará um status de **em execução**</span><span class="sxs-lookup"><span data-stu-id="ae3b8-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="ae3b8-136">Ao concluir, Olá alterações de coluna de status muito**Íntegro** ou **Unhealthy**.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![Solução de problemas concluída][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="ae3b8-138">Entendendo os resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="ae3b8-138">Understanding hello results</span></span>

<span data-ttu-id="ae3b8-139">Em Olá **detalhes** seção da janela de Olá Olá **Status** guia mostra o status de saudação de solução de problemas de última Olá execução no recurso de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="ae3b8-140">Resultados do diagnóstico mais recente Olá são mostrados xx minutos após o hello executado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="ae3b8-141">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ae3b8-141">Property</span></span>  |<span data-ttu-id="ae3b8-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae3b8-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="ae3b8-143">Recurso</span><span class="sxs-lookup"><span data-stu-id="ae3b8-143">Resource</span></span>     | <span data-ttu-id="ae3b8-144">Um recurso de toohello de link.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="ae3b8-145">Caminho de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ae3b8-145">Storage path</span></span>     |  <span data-ttu-id="ae3b8-146">Conta de armazenamento do caminho toohello e contêiner que contêm logs hello (se qualquer produzidas durante a saudação executar).</span><span class="sxs-lookup"><span data-stu-id="ae3b8-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="ae3b8-147">Essa configuração não persiste após sair do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="ae3b8-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="ae3b8-148">Summary</span></span>     | <span data-ttu-id="ae3b8-149">Resumo de integridade de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="ae3b8-150">Detalhes</span><span class="sxs-lookup"><span data-stu-id="ae3b8-150">Detail</span></span>     | <span data-ttu-id="ae3b8-151">Informações detalhadas sobre a integridade de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="ae3b8-152">Última execução</span><span class="sxs-lookup"><span data-stu-id="ae3b8-152">Last run</span></span>     | <span data-ttu-id="ae3b8-153">Olá Olá tempo última solução de problemas de tempo foi executado.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="ae3b8-154">Olá **ação** guia fornece diretrizes gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="ae3b8-155">Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="ae3b8-156">No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="ae3b8-157">Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ae3b8-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="ae3b8-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae3b8-158">Next steps</span></span>

<span data-ttu-id="ae3b8-159">Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="ae3b8-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
