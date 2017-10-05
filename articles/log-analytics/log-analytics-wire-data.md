---
title: "Solução de Dados de Transmissão no Log Analytics | Microsoft Docs"
description: "Dados de transmissão são dados consolidados de rede e de desempenho recebidos de computadores com agentes do OMS, incluindo agentes do Operations Manager e agentes conectados com o Windows. Os dados de rede são combinados com os dados de log para ajudá-lo a correlacionar dados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="f2c39-104">Solução Wire Data 2.0 (Versão Prévia) no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2c39-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Símbolo do Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="f2c39-106">O Wire Data consiste em dados de desempenho e rede consolidados de computadores com agentes do OMS, incluindo agentes Operations Manager, conectados ao Windows e aos agentes do Linux.</span><span class="sxs-lookup"><span data-stu-id="f2c39-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="f2c39-107">Os dados de rede são combinados a seus outros dados de log para ajudá-lo a correlacionar dados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="f2c39-108">Além dos agentes do OMS, a solução Wire Data usa os agentes de Dependência da Microsoft que você instala em computadores na sua infraestrutura de TI.</span><span class="sxs-lookup"><span data-stu-id="f2c39-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="f2c39-109">Os Agentes de Dependência monitoram dados de rede enviados de e para seus computadores para os níveis de rede 2 e 3 no [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), incluindo os diversos protocolos e portas usados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="f2c39-110">Os dados então são enviados para o Log Analytics usando agentes.</span><span class="sxs-lookup"><span data-stu-id="f2c39-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="f2c39-111">Você não pode adicionar a versão anterior da solução Wire Data a novos espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2c39-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="f2c39-112">Se você tiver a solução Wire Data original habilitada, poderá continuar a usá-la.</span><span class="sxs-lookup"><span data-stu-id="f2c39-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="f2c39-113">No entanto, para usar Wire Data 2.0, você deve primeiro remover a versão original.</span><span class="sxs-lookup"><span data-stu-id="f2c39-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="f2c39-114">Por padrão, o Log Analytics coleta dados registrados para dados de CPU, memória, disco e desempenho de rede dos contadores internos do Windows.</span><span class="sxs-lookup"><span data-stu-id="f2c39-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="f2c39-115">A coleta de dados de rede e de outros dados é feita em tempo real para cada agente, incluindo sub-redes e protocolos no nível de aplicativo usados pelo computador.</span><span class="sxs-lookup"><span data-stu-id="f2c39-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="f2c39-116">É possível adicionar outros contadores de desempenho na página Configurações, na guia Logs.</span><span class="sxs-lookup"><span data-stu-id="f2c39-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="f2c39-117">Se você já tiver usado [sFlow](http://www.sflow.org/) ou outro software com o [protocolo NetFlow da Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), as estatísticas e os dados que você verá do Wire Data já serão conhecidos.</span><span class="sxs-lookup"><span data-stu-id="f2c39-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="f2c39-118">Entre alguns dos tipos de consultas de Pesquisa de log internas estão:</span><span class="sxs-lookup"><span data-stu-id="f2c39-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="f2c39-119">Agentes que fornecem dados de transmissão</span><span class="sxs-lookup"><span data-stu-id="f2c39-119">Agents that provide wire data</span></span>
- <span data-ttu-id="f2c39-120">Endereço IP de agentes que fornecem dados de transmissão</span><span class="sxs-lookup"><span data-stu-id="f2c39-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="f2c39-121">Comunicações de saída por endereços IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="f2c39-122">Número de bytes enviados por protocolos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2c39-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="f2c39-123">Número de bytes enviados por um serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2c39-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="f2c39-124">Bytes recebidos por diferentes protocolos</span><span class="sxs-lookup"><span data-stu-id="f2c39-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="f2c39-125">Total de bytes enviados e recebidos por versão de IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="f2c39-126">Latência média de conexões que foram medidas de forma confiável</span><span class="sxs-lookup"><span data-stu-id="f2c39-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="f2c39-127">Processos de computador que iniciaram ou receberam tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="f2c39-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="f2c39-128">Quantidade de tráfego de rede de um processo</span><span class="sxs-lookup"><span data-stu-id="f2c39-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="f2c39-129">Ao pesquisar com os dados de transmissão, é possível filtrar e agrupar os dados para exibir informações sobre os principais agentes e protocolos.</span><span class="sxs-lookup"><span data-stu-id="f2c39-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="f2c39-130">Ou você pode exibir quando determinados computadores (endereços IP/MAC) comunicaram-se entre si, a duração dessa comunicação e a quantidade de dados enviados – basicamente, são exibidos metadados sobre o tráfego de rede, que são baseados em pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f2c39-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="f2c39-131">No entanto, já que você está exibindo metadados, eles não são necessariamente úteis para solução de problemas detalhada.</span><span class="sxs-lookup"><span data-stu-id="f2c39-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="f2c39-132">Wire Data no Log Analytics não é uma captura completa dos dados da rede.</span><span class="sxs-lookup"><span data-stu-id="f2c39-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="f2c39-133">Portanto, não se destina a uma solução de problemas em profundidade no nível de pacote.</span><span class="sxs-lookup"><span data-stu-id="f2c39-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="f2c39-134">A vantagem de usar o agente, em comparação a outros métodos de coleta, é que você não precisa instalar dispositivos, reconfigurar os comutadores de rede nem realizar configurações complicadas.</span><span class="sxs-lookup"><span data-stu-id="f2c39-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="f2c39-135">O Wire Data é simplesmente baseado em agente – você instala o agente em um computador e ele monitorará seu próprio tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="f2c39-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="f2c39-136">Outra vantagem é quando você deseja monitorar cargas de trabalho em execução em provedores de nuvem, provedor de serviços de hospedagem ou no Microsoft Azure, em que o usuário não tem a camada de malha.</span><span class="sxs-lookup"><span data-stu-id="f2c39-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="f2c39-137">Fontes conectadas</span><span class="sxs-lookup"><span data-stu-id="f2c39-137">Connected sources</span></span>

<span data-ttu-id="f2c39-138">O Wire Data obtém seus dados do Agente de Dependência da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2c39-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="f2c39-139">O Agente de Dependência depende do Agente do OMS para suas conexões ao Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2c39-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="f2c39-140">Isso significa que um servidor deve ter o Agente do OMS instalado e configurado primeiro e, em seguida, você instala o Agente de Dependência.</span><span class="sxs-lookup"><span data-stu-id="f2c39-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="f2c39-141">A tabela a seguir descreve as fontes conectadas às quais a solução Wire Data dá suporte.</span><span class="sxs-lookup"><span data-stu-id="f2c39-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="f2c39-142">**Fonte conectada**</span><span class="sxs-lookup"><span data-stu-id="f2c39-142">**Connected source**</span></span> | <span data-ttu-id="f2c39-143">**Com suporte**</span><span class="sxs-lookup"><span data-stu-id="f2c39-143">**Supported**</span></span> | <span data-ttu-id="f2c39-144">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f2c39-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2c39-145">Agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-145">Windows agents</span></span> | <span data-ttu-id="f2c39-146">Sim</span><span class="sxs-lookup"><span data-stu-id="f2c39-146">Yes</span></span> | <span data-ttu-id="f2c39-147">O Wire Data analisa e coleta dados de computadores de agente do Windows.</span><span class="sxs-lookup"><span data-stu-id="f2c39-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="f2c39-148">Além do [Agente do OMS](log-analytics-windows-agents.md), os agentes do Windows exigem o Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="f2c39-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="f2c39-149">Veja os [sistemas operacionais com suporte](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obter uma lista completa das versões de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f2c39-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="f2c39-150">Agentes do Linux</span><span class="sxs-lookup"><span data-stu-id="f2c39-150">Linux agents</span></span> | <span data-ttu-id="f2c39-151">Sim</span><span class="sxs-lookup"><span data-stu-id="f2c39-151">Yes</span></span> | <span data-ttu-id="f2c39-152">O Wire Data analisa e coleta dados de computadores de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="f2c39-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="f2c39-153">Além do [Agente do OMS](log-analytics-linux-agents.md), os agentes do Linux exigem o Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="f2c39-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="f2c39-154">Veja os [sistemas operacionais com suporte](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obter uma lista completa das versões de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f2c39-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="f2c39-155">Grupo de gerenciamento do System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f2c39-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="f2c39-156">Sim</span><span class="sxs-lookup"><span data-stu-id="f2c39-156">Yes</span></span> | <span data-ttu-id="f2c39-157">O Wire Data analisa e coleta dados de agentes do Windows e do Linux em um [grupo de gerenciamento do System Center Operations Manager](log-analytics-om-agents.md) conectado.</span><span class="sxs-lookup"><span data-stu-id="f2c39-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="f2c39-158">Uma conexão direta do computador do agente do System Center Operations Manager para Log Analytics é necessária.</span><span class="sxs-lookup"><span data-stu-id="f2c39-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="f2c39-159">Os dados são encaminhados do grupo de gerenciamento ao Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2c39-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="f2c39-160">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f2c39-160">Azure storage account</span></span> | <span data-ttu-id="f2c39-161">Não</span><span class="sxs-lookup"><span data-stu-id="f2c39-161">No</span></span> | <span data-ttu-id="f2c39-162">O Wire Data coleta dados de computadores do agente e, portanto, não há nenhum dado dele a ser coletado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c39-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="f2c39-163">No Windows, o MMA (Microsoft Monitoring Agent) é usado pelo System Center Operations Manager e pelo Log Analytics para coletar e enviar dados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="f2c39-164">Dependendo do contexto, esse agente é chamado de Agente do System Center Operations Manager, Agente do OMS, Agente do Log Analytics, MMA ou Agente Direto.</span><span class="sxs-lookup"><span data-stu-id="f2c39-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="f2c39-165">O System Center Operations Manager e o Log Analytics fornecem versões do MMA ligeiramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="f2c39-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="f2c39-166">Essas versões podem relatar para o System Center Operations Manager, para o Log Analytics ou para ambos.</span><span class="sxs-lookup"><span data-stu-id="f2c39-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="f2c39-167">No Linux, o Agente OMS para Linux coleta e envia os dados ao Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2c39-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="f2c39-168">Você pode usar o Wire Data em servidores com Agentes Diretos do OMS ou em servidores anexados ao Log Analytics por meio de grupos de gerenciamento do System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f2c39-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="f2c39-169">Neste artigo, as referências a todos os agentes, sejam Linux ou Windows, sejam conectados a um grupo de gerenciamento do System Center Operations Manager ou diretamente ao Log Analytics são chamados de _agente do OMS_.</span><span class="sxs-lookup"><span data-stu-id="f2c39-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="f2c39-170">Usaremos o nome de implantação específico do agente somente se ele for necessário para o contexto.</span><span class="sxs-lookup"><span data-stu-id="f2c39-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="f2c39-171">O Agente de Dependência não transmite todos os dados em si e não requer alterações a portas ou firewalls.</span><span class="sxs-lookup"><span data-stu-id="f2c39-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="f2c39-172">Os dados no Wire Data sempre são transmitidos pelo agente do OMS ao Log Analytics, seja diretamente ou usando o Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="f2c39-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![diagrama do agente](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="f2c39-174">Se você for um usuário do System Center Operations Manager com um grupo de gerenciamento conectado ao Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="f2c39-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="f2c39-175">Se nenhuma configuração adicional é necessária quando os agentes do System Center Operations Manager podem acessar a Internet para conectarem-se ao Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2c39-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="f2c39-176">Você precisa configurar o Gateway do OMS para operar com o System Center Operations Manager quando os agentes do System Center Operations Manager não puderem acessar o Log Analytics pela Internet.</span><span class="sxs-lookup"><span data-stu-id="f2c39-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="f2c39-177">Se você estiver usando o Direct Agent, precisará configurar o próprio agente do OMS para conexão ao Log Analytics ou ao Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="f2c39-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="f2c39-178">Você pode baixar o Gateway do OMS no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="f2c39-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2c39-179">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f2c39-179">Prerequisites</span></span>

- <span data-ttu-id="f2c39-180">Requer a oferta da solução [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing).</span><span class="sxs-lookup"><span data-stu-id="f2c39-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="f2c39-181">Se você estiver usando a versão anterior da solução Wire Data, deverá primeiro removê-la.</span><span class="sxs-lookup"><span data-stu-id="f2c39-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="f2c39-182">No entanto, todos os dados capturados por meio de solução Wire Data original ainda estão disponível no Wire Data 2.0 e na pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="f2c39-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="f2c39-183">São necessários privilégios de administrador para instalar ou desinstalar o Agente de Dependência.</span><span class="sxs-lookup"><span data-stu-id="f2c39-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="f2c39-184">O Agente de Dependência deve ser instalado em um computador com um sistema operacional de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="f2c39-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="f2c39-185">Sistemas operacionais</span><span class="sxs-lookup"><span data-stu-id="f2c39-185">Operating systems</span></span>

<span data-ttu-id="f2c39-186">As seções a seguir listam os sistemas operacionais com suporte para o Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="f2c39-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="f2c39-187">O Wire Data não dá suporte a arquiteturas de 32 bits de nenhum sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f2c39-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="f2c39-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f2c39-188">Windows Server</span></span>

- <span data-ttu-id="f2c39-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f2c39-189">Windows Server 2016</span></span>
- <span data-ttu-id="f2c39-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f2c39-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="f2c39-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f2c39-191">Windows Server 2012</span></span>
- <span data-ttu-id="f2c39-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f2c39-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="f2c39-193">Área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-193">Windows desktop</span></span>

- <span data-ttu-id="f2c39-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="f2c39-194">Windows 10</span></span>
- <span data-ttu-id="f2c39-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="f2c39-195">Windows 8.1</span></span>
- <span data-ttu-id="f2c39-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="f2c39-196">Windows 8</span></span>
- <span data-ttu-id="f2c39-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="f2c39-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="f2c39-198">Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (com Kernel RHEL)</span><span class="sxs-lookup"><span data-stu-id="f2c39-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="f2c39-199">Somente as versões de kernel padrão e Linux SMP têm suporte.</span><span class="sxs-lookup"><span data-stu-id="f2c39-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="f2c39-200">Nenhuma distribuição do Linux dá suporte às versões de kernel não padrão, como PAE e Xen.</span><span class="sxs-lookup"><span data-stu-id="f2c39-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="f2c39-201">Por exemplo, não há suporte para um sistema com a cadeia de caracteres de versão _2.6.16.21-0.8-xen_.</span><span class="sxs-lookup"><span data-stu-id="f2c39-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="f2c39-202">Não há suporte para kernels personalizados, incluindo recompilações de kernels padrão.</span><span class="sxs-lookup"><span data-stu-id="f2c39-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="f2c39-203">Não há suporte para o kernel CentOSPlus.</span><span class="sxs-lookup"><span data-stu-id="f2c39-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="f2c39-204">O UEK (Unbreakable Enterprise Kernel) da Oracle é abordado em uma seção posterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2c39-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="f2c39-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="f2c39-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="f2c39-206">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-206">**OS version**</span></span> | <span data-ttu-id="f2c39-207">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-208">7.0</span><span class="sxs-lookup"><span data-stu-id="f2c39-208">7.0</span></span> | <span data-ttu-id="f2c39-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="f2c39-209">3.10.0-123</span></span> |
| <span data-ttu-id="f2c39-210">7.1</span><span class="sxs-lookup"><span data-stu-id="f2c39-210">7.1</span></span> | <span data-ttu-id="f2c39-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="f2c39-211">3.10.0-229</span></span> |
| <span data-ttu-id="f2c39-212">7,2</span><span class="sxs-lookup"><span data-stu-id="f2c39-212">7.2</span></span> | <span data-ttu-id="f2c39-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="f2c39-213">3.10.0-327</span></span> |
| <span data-ttu-id="f2c39-214">7.3</span><span class="sxs-lookup"><span data-stu-id="f2c39-214">7.3</span></span> | <span data-ttu-id="f2c39-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="f2c39-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="f2c39-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="f2c39-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="f2c39-217">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-217">**OS version**</span></span> | <span data-ttu-id="f2c39-218">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-219">6,0</span><span class="sxs-lookup"><span data-stu-id="f2c39-219">6.0</span></span> | <span data-ttu-id="f2c39-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="f2c39-220">2.6.32-71</span></span> |
| <span data-ttu-id="f2c39-221">6.1</span><span class="sxs-lookup"><span data-stu-id="f2c39-221">6.1</span></span> | <span data-ttu-id="f2c39-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="f2c39-222">2.6.32-131</span></span> |
| <span data-ttu-id="f2c39-223">6.2</span><span class="sxs-lookup"><span data-stu-id="f2c39-223">6.2</span></span> | <span data-ttu-id="f2c39-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="f2c39-224">2.6.32-220</span></span> |
| <span data-ttu-id="f2c39-225">6.3</span><span class="sxs-lookup"><span data-stu-id="f2c39-225">6.3</span></span> | <span data-ttu-id="f2c39-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="f2c39-226">2.6.32-279</span></span> |
| <span data-ttu-id="f2c39-227">6.4</span><span class="sxs-lookup"><span data-stu-id="f2c39-227">6.4</span></span> | <span data-ttu-id="f2c39-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="f2c39-228">2.6.32-358</span></span> |
| <span data-ttu-id="f2c39-229">6.5</span><span class="sxs-lookup"><span data-stu-id="f2c39-229">6.5</span></span> | <span data-ttu-id="f2c39-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="f2c39-230">2.6.32-431</span></span> |
| <span data-ttu-id="f2c39-231">6.6</span><span class="sxs-lookup"><span data-stu-id="f2c39-231">6.6</span></span> | <span data-ttu-id="f2c39-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="f2c39-232">2.6.32-504</span></span> |
| <span data-ttu-id="f2c39-233">6.7</span><span class="sxs-lookup"><span data-stu-id="f2c39-233">6.7</span></span> | <span data-ttu-id="f2c39-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="f2c39-234">2.6.32-573</span></span> |
| <span data-ttu-id="f2c39-235">6,8</span><span class="sxs-lookup"><span data-stu-id="f2c39-235">6.8</span></span> | <span data-ttu-id="f2c39-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="f2c39-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="f2c39-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="f2c39-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="f2c39-238">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-238">**OS version**</span></span> | <span data-ttu-id="f2c39-239">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-240">5.8</span><span class="sxs-lookup"><span data-stu-id="f2c39-240">5.8</span></span> | <span data-ttu-id="f2c39-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="f2c39-241">2.6.18-308</span></span> |
| <span data-ttu-id="f2c39-242">5.9</span><span class="sxs-lookup"><span data-stu-id="f2c39-242">5.9</span></span> | <span data-ttu-id="f2c39-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="f2c39-243">2.6.18-348</span></span> |
| <span data-ttu-id="f2c39-244">5.10</span><span class="sxs-lookup"><span data-stu-id="f2c39-244">5.10</span></span> | <span data-ttu-id="f2c39-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="f2c39-245">2.6.18-371</span></span> |
| <span data-ttu-id="f2c39-246">5.11</span><span class="sxs-lookup"><span data-stu-id="f2c39-246">5.11</span></span> | <span data-ttu-id="f2c39-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="f2c39-247">2.6.18-398</span></span> <br> <span data-ttu-id="f2c39-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="f2c39-248">2.6.18-400</span></span> <br><span data-ttu-id="f2c39-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="f2c39-249">2.6.18-402</span></span> <br><span data-ttu-id="f2c39-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="f2c39-250">2.6.18-404</span></span> <br><span data-ttu-id="f2c39-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="f2c39-251">2.6.18-406</span></span> <br> <span data-ttu-id="f2c39-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="f2c39-252">2.6.18-407</span></span> <br> <span data-ttu-id="f2c39-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="f2c39-253">2.6.18-408</span></span> <br> <span data-ttu-id="f2c39-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="f2c39-254">2.6.18-409</span></span> <br> <span data-ttu-id="f2c39-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="f2c39-255">2.6.18-410</span></span> <br> <span data-ttu-id="f2c39-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="f2c39-256">2.6.18-411</span></span> <br> <span data-ttu-id="f2c39-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="f2c39-257">2.6.18-412</span></span> <br> <span data-ttu-id="f2c39-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="f2c39-258">2.6.18-416</span></span> <br> <span data-ttu-id="f2c39-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="f2c39-259">2.6.18-417</span></span> <br> <span data-ttu-id="f2c39-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="f2c39-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="f2c39-261">Oracle Enterprise Linux com Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="f2c39-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="f2c39-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="f2c39-262">Oracle Linux 6</span></span>

| <span data-ttu-id="f2c39-263">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-263">**OS version**</span></span> | <span data-ttu-id="f2c39-264">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-265">6.2</span><span class="sxs-lookup"><span data-stu-id="f2c39-265">6.2</span></span> | <span data-ttu-id="f2c39-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="f2c39-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="f2c39-267">6.3</span><span class="sxs-lookup"><span data-stu-id="f2c39-267">6.3</span></span> | <span data-ttu-id="f2c39-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="f2c39-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="f2c39-269">6.4</span><span class="sxs-lookup"><span data-stu-id="f2c39-269">6.4</span></span> | <span data-ttu-id="f2c39-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="f2c39-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="f2c39-271">6.5</span><span class="sxs-lookup"><span data-stu-id="f2c39-271">6.5</span></span> | <span data-ttu-id="f2c39-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="f2c39-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="f2c39-273">6.6</span><span class="sxs-lookup"><span data-stu-id="f2c39-273">6.6</span></span> | <span data-ttu-id="f2c39-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="f2c39-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="f2c39-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="f2c39-275">Oracle Linux 5</span></span>

| <span data-ttu-id="f2c39-276">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-276">**OS version**</span></span> | <span data-ttu-id="f2c39-277">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-278">5.8</span><span class="sxs-lookup"><span data-stu-id="f2c39-278">5.8</span></span> | <span data-ttu-id="f2c39-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="f2c39-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="f2c39-280">5.9</span><span class="sxs-lookup"><span data-stu-id="f2c39-280">5.9</span></span> | <span data-ttu-id="f2c39-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="f2c39-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="f2c39-282">5.10</span><span class="sxs-lookup"><span data-stu-id="f2c39-282">5.10</span></span> | <span data-ttu-id="f2c39-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="f2c39-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="f2c39-284">5.11</span><span class="sxs-lookup"><span data-stu-id="f2c39-284">5.11</span></span> | <span data-ttu-id="f2c39-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="f2c39-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="f2c39-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="f2c39-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="f2c39-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="f2c39-287">SUSE Linux 11</span></span>

| <span data-ttu-id="f2c39-288">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-288">**OS version**</span></span> | <span data-ttu-id="f2c39-289">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-290">11</span><span class="sxs-lookup"><span data-stu-id="f2c39-290">11</span></span> | <span data-ttu-id="f2c39-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="f2c39-291">2.6.27</span></span> |
| <span data-ttu-id="f2c39-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="f2c39-292">11 SP1</span></span> | <span data-ttu-id="f2c39-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="f2c39-293">2.6.32</span></span> |
| <span data-ttu-id="f2c39-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="f2c39-294">11 SP2</span></span> | <span data-ttu-id="f2c39-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="f2c39-295">3.0.13</span></span> |
| <span data-ttu-id="f2c39-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="f2c39-296">11 SP3</span></span> | <span data-ttu-id="f2c39-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="f2c39-297">3.0.76</span></span> |
| <span data-ttu-id="f2c39-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="f2c39-298">11 SP4</span></span> | <span data-ttu-id="f2c39-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="f2c39-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="f2c39-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="f2c39-300">SUSE Linux 10</span></span>

| <span data-ttu-id="f2c39-301">**Versão do SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-301">**OS version**</span></span> | <span data-ttu-id="f2c39-302">**Versão do kernel**</span><span class="sxs-lookup"><span data-stu-id="f2c39-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="f2c39-303">10 SP4</span></span> | <span data-ttu-id="f2c39-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="f2c39-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="f2c39-305">Downloads do Agente de Dependência</span><span class="sxs-lookup"><span data-stu-id="f2c39-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="f2c39-306">**Arquivo**</span><span class="sxs-lookup"><span data-stu-id="f2c39-306">**File**</span></span> | <span data-ttu-id="f2c39-307">**SO**</span><span class="sxs-lookup"><span data-stu-id="f2c39-307">**OS**</span></span> | <span data-ttu-id="f2c39-308">**Versão**</span><span class="sxs-lookup"><span data-stu-id="f2c39-308">**Version**</span></span> | <span data-ttu-id="f2c39-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="f2c39-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="f2c39-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="f2c39-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="f2c39-311">Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-311">Windows</span></span> | <span data-ttu-id="f2c39-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="f2c39-312">9.0.5</span></span> | <span data-ttu-id="f2c39-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="f2c39-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="f2c39-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="f2c39-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="f2c39-315">Linux</span><span class="sxs-lookup"><span data-stu-id="f2c39-315">Linux</span></span> | <span data-ttu-id="f2c39-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="f2c39-316">9.0.5</span></span> | <span data-ttu-id="f2c39-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="f2c39-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="f2c39-318">Configuração</span><span class="sxs-lookup"><span data-stu-id="f2c39-318">Configuration</span></span>

<span data-ttu-id="f2c39-319">Execute as seguintes etapas para configurar a solução Wire Data para seus espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2c39-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="f2c39-320">Habilite a solução Log Analytics da atividade no [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) ou usando o processo descrito em [Adicionar soluções Log Analytics por meio da Galeria de soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="f2c39-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="f2c39-321">Instale o Agente de Dependência em cada computador em que você deseje obter dados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="f2c39-322">O Agente de Dependência pode monitorar conexões a vizinhos imediatos, portanto, talvez não seja necessário ter um agente em cada computador.</span><span class="sxs-lookup"><span data-stu-id="f2c39-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="f2c39-323">Instalar o Agente de Dependência no Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="f2c39-324">São necessários privilégios de administrador para instalar ou desinstalar o agente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="f2c39-325">O Agente de Dependência é instalado em computadores que executam o Windows por meio do InstallDependencyAgent-Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="f2c39-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="f2c39-326">Se você executar o arquivo executável sem opções, ele iniciará um assistente que você poderá seguir para executar a instalação interativamente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="f2c39-327">Use as etapas a seguir para instalar o Agente de Dependência em cada computador com o Windows:</span><span class="sxs-lookup"><span data-stu-id="f2c39-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="f2c39-328">Instalar o Agente OMS usando as instruções em [Conectar computadores Windows ao serviço do Log Analytics no Azure](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="f2c39-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="f2c39-329">Baixe o agente do Windows usando o link na seção anterior e, em seguida, executando-o usando o seguinte comando: InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="f2c39-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="f2c39-330">Acompanhe o assistente para instalar o agente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="f2c39-331">Se o Agente de Dependência não for iniciado, verifique os logs para obter informações de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="f2c39-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="f2c39-332">Em Agentes do Windows, o diretório de log será %Programfiles%\Microsoft Dependency Agent\logs.</span><span class="sxs-lookup"><span data-stu-id="f2c39-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="f2c39-333">Linha de comando do Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-333">Windows command line</span></span>

<span data-ttu-id="f2c39-334">Use as opções da tabela a seguir para instalar a partir de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f2c39-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="f2c39-335">Para ver uma lista dos sinalizadores de instalação, execute o instalador usando o sinalizador /?</span><span class="sxs-lookup"><span data-stu-id="f2c39-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="f2c39-336">da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="f2c39-336">flag as follows.</span></span>

<span data-ttu-id="f2c39-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="f2c39-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="f2c39-338">**Sinalizador**</span><span class="sxs-lookup"><span data-stu-id="f2c39-338">**Flag**</span></span> | <span data-ttu-id="f2c39-339">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f2c39-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="f2c39-340">Obtenha uma lista das opções de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f2c39-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="f2c39-341">Realize uma instalação silenciosa sem solicitações ao usuário.</span><span class="sxs-lookup"><span data-stu-id="f2c39-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="f2c39-342">Os arquivos do Agente de Dependência do Windows são colocados em C:\Program Files\Microsoft Dependency Agent por padrão.</span><span class="sxs-lookup"><span data-stu-id="f2c39-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="f2c39-343">Instalar o Agente de Dependência no Linux</span><span class="sxs-lookup"><span data-stu-id="f2c39-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="f2c39-344">O acesso root é necessário para instalar ou configurar o agente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="f2c39-345">O Agente de Dependência é instalado em computadores com o Linux por meio do InstallDependencyAgent-Linux64.bin, um script de shell com um binário de extração automática.</span><span class="sxs-lookup"><span data-stu-id="f2c39-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="f2c39-346">Você pode executar o arquivo usando _sh_ ou adicionar permissões de execução ao próprio arquivo.</span><span class="sxs-lookup"><span data-stu-id="f2c39-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="f2c39-347">Use as seguintes etapas para instalar o Dependency Agent em cada computador com o Linux:</span><span class="sxs-lookup"><span data-stu-id="f2c39-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="f2c39-348">Instale o Agente OMS usando as instruções em [Coletar e gerenciar dados de computadores com o Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f2c39-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="f2c39-349">Baixe o Agente de Dependência do Linux usando o link na seção anterior e, em seguida, instale-o como raiz usando o seguinte comando: sh InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="f2c39-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="f2c39-350">Se o Agente de Dependência não for iniciado, verifique os logs para obter informações de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="f2c39-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="f2c39-351">Em agentes do Linux, o diretório de log é /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="f2c39-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="f2c39-352">Para ver uma lista dos sinalizadores de instalação, execute o programa de instalação com o sinalizador `-help` conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2c39-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="f2c39-353">**Sinalizador**</span><span class="sxs-lookup"><span data-stu-id="f2c39-353">**Flag**</span></span> | <span data-ttu-id="f2c39-354">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f2c39-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="f2c39-355">Obtenha uma lista das opções de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f2c39-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="f2c39-356">Realize uma instalação silenciosa sem solicitações ao usuário.</span><span class="sxs-lookup"><span data-stu-id="f2c39-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="f2c39-357">Verifica as permissões e o sistema operacional, mas não instala o agente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="f2c39-358">Os arquivos do Dependency Agent são colocados nos diretórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2c39-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="f2c39-359">**Arquivos**</span><span class="sxs-lookup"><span data-stu-id="f2c39-359">**Files**</span></span> | <span data-ttu-id="f2c39-360">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="f2c39-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-361">Arquivos de núcleo</span><span class="sxs-lookup"><span data-stu-id="f2c39-361">Core files</span></span> | <span data-ttu-id="f2c39-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="f2c39-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="f2c39-363">Arquivos de log</span><span class="sxs-lookup"><span data-stu-id="f2c39-363">Log files</span></span> | <span data-ttu-id="f2c39-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="f2c39-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="f2c39-365">Arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="f2c39-365">Config files</span></span> | <span data-ttu-id="f2c39-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="f2c39-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="f2c39-367">Arquivos executáveis de serviço</span><span class="sxs-lookup"><span data-stu-id="f2c39-367">Service executable files</span></span> | <span data-ttu-id="f2c39-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="f2c39-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="f2c39-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="f2c39-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="f2c39-370">Arquivos de armazenamento binário</span><span class="sxs-lookup"><span data-stu-id="f2c39-370">Binary storage files</span></span> | <span data-ttu-id="f2c39-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="f2c39-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="f2c39-372">Exemplos de script de instalação</span><span class="sxs-lookup"><span data-stu-id="f2c39-372">Installation script examples</span></span>

<span data-ttu-id="f2c39-373">Para implantar facilmente o agente de dependência em vários servidores simultaneamente, convém usar um script.</span><span class="sxs-lookup"><span data-stu-id="f2c39-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="f2c39-374">Você pode usar os exemplos de script a seguir para baixar e instalar o agente de dependência no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="f2c39-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="f2c39-375">Script do PowerShell para Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="f2c39-376">Script de Shell para Linux</span><span class="sxs-lookup"><span data-stu-id="f2c39-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="f2c39-377">Configuração de estado desejado</span><span class="sxs-lookup"><span data-stu-id="f2c39-377">Desired State Configuration</span></span>

<span data-ttu-id="f2c39-378">Para implantar o agente de dependência por meio da Desired State Configuration, você pode usar o módulo xPSDesiredStateConfiguration e um pouco de código semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f2c39-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="f2c39-379">Desinstalar o Agente de Dependência</span><span class="sxs-lookup"><span data-stu-id="f2c39-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="f2c39-380">Use as seções a seguir para ajudá-lo a remover o Agente de Dependência.</span><span class="sxs-lookup"><span data-stu-id="f2c39-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="f2c39-381">Desinstalar o Agente de Dependência no Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="f2c39-382">O Agente de Dependência para Windows pode ser desinstalado por um administrador por meio do Painel de Controle.</span><span class="sxs-lookup"><span data-stu-id="f2c39-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="f2c39-383">Um administrador também pode executar %Programfiles%\Microsoft Agent\Uninstall.exe para desinstalar o Agente de Dependência.</span><span class="sxs-lookup"><span data-stu-id="f2c39-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="f2c39-384">Desinstalar o Agente de Dependência no Linux</span><span class="sxs-lookup"><span data-stu-id="f2c39-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="f2c39-385">Para desinstalar completamente o Agente de Dependência do Linux, você deve remover o agente propriamente dito e o conector instalado automaticamente com o agente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="f2c39-386">Você pode desinstalar ambos usando o seguinte comando único:</span><span class="sxs-lookup"><span data-stu-id="f2c39-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="f2c39-387">Pacotes de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="f2c39-387">Management packs</span></span>

<span data-ttu-id="f2c39-388">Quando o Wire Data é ativado em um espaço de trabalho do Log Analytics, um pacote de gerenciamento de 300 KB é enviado a todos os servidores do Windows nesse espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2c39-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="f2c39-389">Se você estiver usando agentes do System Center Operations Manager em um [grupo de gerenciamento conectado](log-analytics-om-agents.md), o pacote de gerenciamento do Monitor de Dependência será implantado do System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f2c39-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="f2c39-390">Se os agentes forem conectados diretamente, o Log Analytics fornecerá o pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f2c39-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="f2c39-391">O pacote de gerenciamento chama-se Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="f2c39-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="f2c39-392">Ele é gravado em: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="f2c39-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="f2c39-393">A fonte de dados usada pelo pacote de gerenciamento é: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="f2c39-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="f2c39-394">Usando a solução</span><span class="sxs-lookup"><span data-stu-id="f2c39-394">Using the solution</span></span>

<span data-ttu-id="f2c39-395">**Instalando e configurando a solução**</span><span class="sxs-lookup"><span data-stu-id="f2c39-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="f2c39-396">Use as informações a seguir para instalar e configurar a solução.</span><span class="sxs-lookup"><span data-stu-id="f2c39-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="f2c39-397">A solução de Dados de Transmissão obtém dados de computadores que executam o Windows Server 2012 R2, Windows 8.1 e sistemas operacionais posteriores.</span><span class="sxs-lookup"><span data-stu-id="f2c39-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="f2c39-398">O Microsoft .NET Framework 4.0 ou posterior é necessário nos computadores dos quais você deseja obter dados de transmissão.</span><span class="sxs-lookup"><span data-stu-id="f2c39-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="f2c39-399">Adicione a solução de Dados de Transmissão ao seu espaço de trabalho do Log Analytics usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="f2c39-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="f2c39-400">Não é necessária nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="f2c39-400">There is no further configuration required.</span></span>
- <span data-ttu-id="f2c39-401">Se você desejar exibir os dados de transmissão de uma solução específica, será necessário ter a solução já adicionada ao seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2c39-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="f2c39-402">Depois de instalar os agentes e instalar a solução, o bloco Wire Data 2.0 aparece no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2c39-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="f2c39-403">No momento, você deve usar o portal do OMS para exibir dados de transmissão.</span><span class="sxs-lookup"><span data-stu-id="f2c39-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="f2c39-404">Você não pode usar o portal do Azure para exibir o Wire Data.</span><span class="sxs-lookup"><span data-stu-id="f2c39-404">You cannot use the Azure portal to view wire data.</span></span>

![Bloco do Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="f2c39-406">Usando a solução Wire Data 2.0</span><span class="sxs-lookup"><span data-stu-id="f2c39-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="f2c39-407">No portal do OMS, clique no bloco **Wire Data 2.0** para abrir o painel Wire Data.</span><span class="sxs-lookup"><span data-stu-id="f2c39-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="f2c39-408">O painel inclui as folhas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2c39-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="f2c39-409">Cada folha lista os 10 principais itens que correspondem aos critérios da folha para o escopo e o intervalo de tempo especificados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="f2c39-410">É possível executar uma pesquisa de logs que retorna todos os registros clicando em **Ver todos** na parte inferior da folha ou clicando no cabeçalho de folha.</span><span class="sxs-lookup"><span data-stu-id="f2c39-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="f2c39-411">**Folha**</span><span class="sxs-lookup"><span data-stu-id="f2c39-411">**Blade**</span></span> | <span data-ttu-id="f2c39-412">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f2c39-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f2c39-413">Agentes capturando tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="f2c39-413">Agents capturing network traffic</span></span> | <span data-ttu-id="f2c39-414">Mostra o número de agentes que estão capturando tráfego de rede e lista os 10 principais computadores que estão capturando tráfego.</span><span class="sxs-lookup"><span data-stu-id="f2c39-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="f2c39-415">Clique no número para executar uma pesquisa de logs para <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="f2c39-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="f2c39-416">Clique em um computador na lista para executar uma pesquisa de logs retornando o número total de bytes capturados.</span><span class="sxs-lookup"><span data-stu-id="f2c39-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="f2c39-417">Sub-redes locais</span><span class="sxs-lookup"><span data-stu-id="f2c39-417">Local Subnets</span></span> | <span data-ttu-id="f2c39-418">Mostra o número de sub-redes locais que os agentes descobriram.</span><span class="sxs-lookup"><span data-stu-id="f2c39-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="f2c39-419">Clique no número para executar uma pesquisa de logs para <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> que liste todas as sub-redes com o número de bytes enviados em cada uma.</span><span class="sxs-lookup"><span data-stu-id="f2c39-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="f2c39-420">Clique em uma sub-rede na lista para executar uma pesquisa de logs retornando o número total de bytes enviados pela sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f2c39-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="f2c39-421">Protocolos no nível do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2c39-421">Application-level Protocols</span></span> | <span data-ttu-id="f2c39-422">Mostra o número de protocolos no nível de aplicativo em uso, conforme detectados pelos agentes.</span><span class="sxs-lookup"><span data-stu-id="f2c39-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="f2c39-423">Clique no número para executar uma pesquisa de logs para <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="f2c39-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="f2c39-424">Clique em um protocolo para executar uma pesquisa de logs retornando o número total de bytes enviados usando o protocolo.</span><span class="sxs-lookup"><span data-stu-id="f2c39-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Painel do Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="f2c39-426">Você pode usar a folha **Agentes capturando tráfego de rede** para determinar quanta largura de banda de rede está sendo consumida pelos computadores.</span><span class="sxs-lookup"><span data-stu-id="f2c39-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="f2c39-427">Essa folha pode ajudá-lo a localizar facilmente o computador _chattiest_ no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f2c39-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="f2c39-428">Esses computadores podem estar sobrecarregados, operando de modo anormal ou usando mais recursos de rede que o normal.</span><span class="sxs-lookup"><span data-stu-id="f2c39-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="f2c39-430">De modo parecido, você pode usar a folha **Sub-Redes Locais** para determinar quanto tráfego de rede está passando pelas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f2c39-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="f2c39-431">Os usuários geralmente definem sub-redes em torno de áreas críticas para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f2c39-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="f2c39-432">Esta folha oferece uma exibição dessas áreas.</span><span class="sxs-lookup"><span data-stu-id="f2c39-432">This blade offers a view into those areas.</span></span>

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="f2c39-434">A folha **Protocolos em Nível de Aplicativo** é interessante porque é útil saber quais protocolos estão em uso.</span><span class="sxs-lookup"><span data-stu-id="f2c39-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="f2c39-435">Por exemplo, você pode esperar que SSH não esteja em uso no seu ambiente de rede.</span><span class="sxs-lookup"><span data-stu-id="f2c39-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="f2c39-436">Exibir informações disponíveis na folha pode rapidamente confirmar ou v. refutar suas expectativas.</span><span class="sxs-lookup"><span data-stu-id="f2c39-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="f2c39-438">Neste exemplo, você pode analisar em detalhes SSH para ver quais computadores estão usando o SSH e muitos outros detalhes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="f2c39-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![resultados da pesquisa sh](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="f2c39-440">Também é útil saber se o tráfego do protocolo está aumentando ou diminuindo ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="f2c39-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="f2c39-441">Por exemplo, se a quantidade de dados que está sendo transmitida por um aplicativo estiver aumentando, isso pode ser algo a que você deve estar atento ou pode considerar importante.</span><span class="sxs-lookup"><span data-stu-id="f2c39-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="f2c39-442">Dados de entrada</span><span class="sxs-lookup"><span data-stu-id="f2c39-442">Input data</span></span>

<span data-ttu-id="f2c39-443">A coleta de dados coleta metadados sobre o tráfego de rede usando os agentes que você habilitou.</span><span class="sxs-lookup"><span data-stu-id="f2c39-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="f2c39-444">Cada agente envia dados aproximadamente a cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="f2c39-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="f2c39-445">Dados de saída</span><span class="sxs-lookup"><span data-stu-id="f2c39-445">Output data</span></span>

<span data-ttu-id="f2c39-446">Um registro com um tipo de _WireData_ é criado para cada tipo de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2c39-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="f2c39-447">Os registros do WireData têm as propriedades mostradas na tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2c39-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="f2c39-448">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2c39-448">Property</span></span> | <span data-ttu-id="f2c39-449">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2c39-449">Description</span></span> |
|---|---|
| <span data-ttu-id="f2c39-450">Computador</span><span class="sxs-lookup"><span data-stu-id="f2c39-450">Computer</span></span> | <span data-ttu-id="f2c39-451">Nome do computador em que os dados foram coletados</span><span class="sxs-lookup"><span data-stu-id="f2c39-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="f2c39-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="f2c39-452">TimeGenerated</span></span> | <span data-ttu-id="f2c39-453">Hora do registro</span><span class="sxs-lookup"><span data-stu-id="f2c39-453">Time of the record</span></span> |
| <span data-ttu-id="f2c39-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="f2c39-454">LocalIP</span></span> | <span data-ttu-id="f2c39-455">Endereço IP do computador local</span><span class="sxs-lookup"><span data-stu-id="f2c39-455">IP address of the local computer</span></span> |
| <span data-ttu-id="f2c39-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="f2c39-456">SessionState</span></span> | <span data-ttu-id="f2c39-457">Conectado ou desconectado</span><span class="sxs-lookup"><span data-stu-id="f2c39-457">Connected or disconnected</span></span> |
| <span data-ttu-id="f2c39-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="f2c39-458">ReceivedBytes</span></span> | <span data-ttu-id="f2c39-459">Quantidade de bytes recebidos</span><span class="sxs-lookup"><span data-stu-id="f2c39-459">Amount of bytes received</span></span> |
| <span data-ttu-id="f2c39-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="f2c39-460">ProtocolName</span></span> | <span data-ttu-id="f2c39-461">Nome do protocolo de rede usado</span><span class="sxs-lookup"><span data-stu-id="f2c39-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="f2c39-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="f2c39-462">IPVersion</span></span> | <span data-ttu-id="f2c39-463">Versão IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-463">IP version</span></span> |
| <span data-ttu-id="f2c39-464">Direção</span><span class="sxs-lookup"><span data-stu-id="f2c39-464">Direction</span></span> | <span data-ttu-id="f2c39-465">Entrada ou saída</span><span class="sxs-lookup"><span data-stu-id="f2c39-465">Inbound or outbound</span></span> |
| <span data-ttu-id="f2c39-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="f2c39-466">MaliciousIP</span></span> | <span data-ttu-id="f2c39-467">Endereço IP de uma fonte mal-intencionada conhecida</span><span class="sxs-lookup"><span data-stu-id="f2c39-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="f2c39-468">Severity</span><span class="sxs-lookup"><span data-stu-id="f2c39-468">Severity</span></span> | <span data-ttu-id="f2c39-469">Gravidade de suspeita de malware</span><span class="sxs-lookup"><span data-stu-id="f2c39-469">Suspected malware severity</span></span> |
| <span data-ttu-id="f2c39-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="f2c39-470">RemoteIPCountry</span></span> | <span data-ttu-id="f2c39-471">País do endereço IP remoto</span><span class="sxs-lookup"><span data-stu-id="f2c39-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="f2c39-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="f2c39-472">ManagementGroupName</span></span> | <span data-ttu-id="f2c39-473">Nome do grupo de gerenciamento do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f2c39-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="f2c39-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="f2c39-474">SourceSystem</span></span> | <span data-ttu-id="f2c39-475">Fonte na qual o dados foram coletados</span><span class="sxs-lookup"><span data-stu-id="f2c39-475">Source where data was collected</span></span> |
| <span data-ttu-id="f2c39-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="f2c39-476">SessionStartTime</span></span> | <span data-ttu-id="f2c39-477">Hora de início da sessão</span><span class="sxs-lookup"><span data-stu-id="f2c39-477">Start time of session</span></span> |
| <span data-ttu-id="f2c39-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="f2c39-478">SessionEndTime</span></span> | <span data-ttu-id="f2c39-479">Hora de término da sessão</span><span class="sxs-lookup"><span data-stu-id="f2c39-479">End time of session</span></span> |
| <span data-ttu-id="f2c39-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="f2c39-480">LocalSubnet</span></span> | <span data-ttu-id="f2c39-481">Sub-rede na qual o dados foram coletados</span><span class="sxs-lookup"><span data-stu-id="f2c39-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="f2c39-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="f2c39-482">LocalPortNumber</span></span> | <span data-ttu-id="f2c39-483">Número da porta local</span><span class="sxs-lookup"><span data-stu-id="f2c39-483">Local port number</span></span> |
| <span data-ttu-id="f2c39-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="f2c39-484">RemoteIP</span></span> | <span data-ttu-id="f2c39-485">Endereço IP remoto usado pelo computador remoto</span><span class="sxs-lookup"><span data-stu-id="f2c39-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="f2c39-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="f2c39-486">RemotePortNumber</span></span> | <span data-ttu-id="f2c39-487">Número da porta usada pelo endereço IP remoto</span><span class="sxs-lookup"><span data-stu-id="f2c39-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="f2c39-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="f2c39-488">SessionID</span></span> | <span data-ttu-id="f2c39-489">Um valor exclusivo que identifica a sessão de comunicação entre os dois endereços IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="f2c39-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="f2c39-490">SentBytes</span></span> | <span data-ttu-id="f2c39-491">Número de bytes enviados</span><span class="sxs-lookup"><span data-stu-id="f2c39-491">Number of bytes sent</span></span> |
| <span data-ttu-id="f2c39-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="f2c39-492">TotalBytes</span></span> | <span data-ttu-id="f2c39-493">Número total de bytes enviados durante a sessão</span><span class="sxs-lookup"><span data-stu-id="f2c39-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="f2c39-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="f2c39-494">ApplicationProtocol</span></span> | <span data-ttu-id="f2c39-495">Tipo de protocolo de rede usado</span><span class="sxs-lookup"><span data-stu-id="f2c39-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="f2c39-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="f2c39-496">ProcessID</span></span> | <span data-ttu-id="f2c39-497">ID de processo do Windows</span><span class="sxs-lookup"><span data-stu-id="f2c39-497">Windows process ID</span></span> |
| <span data-ttu-id="f2c39-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="f2c39-498">ProcessName</span></span> | <span data-ttu-id="f2c39-499">Nome de arquivo e caminho do processo</span><span class="sxs-lookup"><span data-stu-id="f2c39-499">Path and file name of the process</span></span> |
| <span data-ttu-id="f2c39-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="f2c39-500">RemoteIPLongitude</span></span> | <span data-ttu-id="f2c39-501">Valor de longitude do IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-501">IP longitude value</span></span> |
| <span data-ttu-id="f2c39-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="f2c39-502">RemoteIPLatitude</span></span> | <span data-ttu-id="f2c39-503">Valor de latitude do IP</span><span class="sxs-lookup"><span data-stu-id="f2c39-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f2c39-504">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2c39-504">Next steps</span></span>

- <span data-ttu-id="f2c39-505">[Pesquise nos logs](log-analytics-log-searches.md) para exibir registros detalhados da pesquisa de dados de transmissão.</span><span class="sxs-lookup"><span data-stu-id="f2c39-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
