---
title: "Conector de Gerenciamento de Serviço de TI no OMS | Microsoft Docs"
description: "Use o Conector de Gerenciamento de Serviço de TI para monitorar e gerenciar os itens de trabalho de ITSM no OMS de forma centralizada e resolver problemas rapidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="ab53f-103">Gerenciar itens de trabalho de ITSM de forma centralizada usando o Conector de Gerenciamento de Serviço de TI (Visualização)</span><span class="sxs-lookup"><span data-stu-id="ab53f-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Símbolo do Conector de Gerenciamento do Serviço de TI](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="ab53f-105">Você pode usar o ITSMC (Conector de Gerenciamento de Serviço de TI) no Log Analytics do OMS para monitorar e gerenciar itens de trabalho em todos os produtos e serviços de ITSM de forma centralizada.</span><span class="sxs-lookup"><span data-stu-id="ab53f-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="ab53f-106">O Conector de Gerenciamento do Serviço de TI é integrado aos produtos e serviços de ITSM (Gerenciamento do Serviço de TI) com o Log Analytics do OMS.</span><span class="sxs-lookup"><span data-stu-id="ab53f-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="ab53f-107">A solução tem uma integração bidirecional com produtos/serviços de ITSM, que fornece aos usuários do OMS uma opção para criar incidentes, alertas ou eventos na solução de ITSM.</span><span class="sxs-lookup"><span data-stu-id="ab53f-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="ab53f-108">O conector também importa dados, como incidentes e solicitações de alteração, da solução de ITSM para o Log Analytics do OMS.</span><span class="sxs-lookup"><span data-stu-id="ab53f-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="ab53f-109">Com o Conector de Gerenciamento de Serviço de TI, você pode:</span><span class="sxs-lookup"><span data-stu-id="ab53f-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="ab53f-110">Monitorar e gerenciar itens de trabalho para produtos/serviços de ITSM usados em sua organização de forma centralizada.</span><span class="sxs-lookup"><span data-stu-id="ab53f-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="ab53f-111">Criar itens de trabalho de ITSM (como alerta, evento e incidente) no ITSM com base em alertas do OMS e por meio da pesquisa de logs.</span><span class="sxs-lookup"><span data-stu-id="ab53f-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="ab53f-112">Ler incidentes e solicitações de alteração na solução de ITSM e correlacioná-los com os dados de logs relevantes no espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab53f-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="ab53f-113">Localizar eventos inesperados e incomuns e resolvê-los, mesmo antes de os usuários finais entrarem em contato e relatá-los para a assistência técnica.</span><span class="sxs-lookup"><span data-stu-id="ab53f-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="ab53f-114">Importar dados de itens de trabalho para o Log Analytics e criar relatórios de KPI (indicador chave de desempenho).</span><span class="sxs-lookup"><span data-stu-id="ab53f-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="ab53f-115">Com esses relatórios, você pode identificar, avaliar e tomar decisões em relação a vários itens importantes, como avaliação de malware.</span><span class="sxs-lookup"><span data-stu-id="ab53f-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="ab53f-116">Exibir painéis estruturados para obter informações mais profundas sobre incidentes, solicitações de alteração e sistemas afetados.</span><span class="sxs-lookup"><span data-stu-id="ab53f-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="ab53f-117">Resolver problemas mais rapidamente correlacionando-os com outras soluções de gerenciamento do espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab53f-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ab53f-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab53f-118">Prerequisites</span></span>

<span data-ttu-id="ab53f-119">Para importar itens de trabalho de ITSM para o Log Analytics do OMS, a solução precisa de uma conexão entre o Conector de Gerenciamento de Serviço de TI no OMS e o produto/serviço de IT SM do qual os itens de trabalho são importados.</span><span class="sxs-lookup"><span data-stu-id="ab53f-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="ab53f-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="ab53f-120">Configuration</span></span>

<span data-ttu-id="ab53f-121">Adicione a solução Conector de Gerenciamento de Serviço de TI ao espaço de trabalho do OMS usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ab53f-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="ab53f-122">O bloco Conector de Gerenciamento de Serviço de TI como visto na Galeria de soluções:</span><span class="sxs-lookup"><span data-stu-id="ab53f-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![bloco do conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="ab53f-124">Após a adição bem-sucedida, você verá o Conector de Gerenciamento de Serviço de TI em **OMS** > **Configurações** > **Fontes Conectadas.**</span><span class="sxs-lookup"><span data-stu-id="ab53f-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="ab53f-126">Por padrão, o Conector de Gerenciamento do Serviço de TI atualiza os dados da conexão uma vez em cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ab53f-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="ab53f-127">Para atualizar os dados da conexão instantaneamente para as edições ou atualizações do modelo que você fizer, clique no botão Atualizar exibido ao lado de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="ab53f-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Atualização do ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="ab53f-129">Pacotes de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-129">Management packs</span></span>
<span data-ttu-id="ab53f-130">Essa solução não exige nenhum pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ab53f-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="ab53f-131">Fontes conectadas</span><span class="sxs-lookup"><span data-stu-id="ab53f-131">Connected sources</span></span>

<span data-ttu-id="ab53f-132">Os seguintes produtos/serviços de ITSM têm suporte no Conector de Gerenciamento de Serviço de TI:</span><span class="sxs-lookup"><span data-stu-id="ab53f-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="ab53f-133">SCSM (System Center Service Manager)</span><span class="sxs-lookup"><span data-stu-id="ab53f-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="ab53f-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ab53f-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="ab53f-135">Provance</span><span class="sxs-lookup"><span data-stu-id="ab53f-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="ab53f-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="ab53f-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="ab53f-137">Usando a solução</span><span class="sxs-lookup"><span data-stu-id="ab53f-137">Using the solution</span></span>

<span data-ttu-id="ab53f-138">Depois de conectar o Conector de Gerenciamento do Serviço de TI do OMS com o serviço de ITSM, os serviços do Log Analytics começam a coletar os dados dos produtos/serviço do ITMS conectado.</span><span class="sxs-lookup"><span data-stu-id="ab53f-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="ab53f-139">Os dados importados pelo Conector de Gerenciamento do Serviço de TI são exibidos no Log Analytics como eventos chamados **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="ab53f-140">O evento contém um campo chamado **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="ab53f-141">que pode usar seu valor como um incidente ou uma solicitação de alteração, dependendo dos dados de item de trabalho contidos no evento **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="ab53f-142">Dados de entrada</span><span class="sxs-lookup"><span data-stu-id="ab53f-142">Input data</span></span>
<span data-ttu-id="ab53f-143">Itens de trabalho importados dos produtos/serviços do ITSM.</span><span class="sxs-lookup"><span data-stu-id="ab53f-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="ab53f-144">As seguintes informações mostram exemplos de dados coletados pelo conector de Gerenciamento de Serviço de TI:</span><span class="sxs-lookup"><span data-stu-id="ab53f-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="ab53f-145">Dependendo do tipo de item de trabalho importado para o Log Analytics, **ServiceDesk_CL** contém os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="ab53f-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="ab53f-146">**Item de trabalho:** **Incidentes**</span><span class="sxs-lookup"><span data-stu-id="ab53f-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="ab53f-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="ab53f-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="ab53f-148">**Campos**</span><span class="sxs-lookup"><span data-stu-id="ab53f-148">**Fields**</span></span>

- <span data-ttu-id="ab53f-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="ab53f-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="ab53f-150">ID da Central de Serviços</span><span class="sxs-lookup"><span data-stu-id="ab53f-150">Service Desk ID</span></span>
- <span data-ttu-id="ab53f-151">Estado</span><span class="sxs-lookup"><span data-stu-id="ab53f-151">State</span></span>
- <span data-ttu-id="ab53f-152">Urgência</span><span class="sxs-lookup"><span data-stu-id="ab53f-152">Urgency</span></span>
- <span data-ttu-id="ab53f-153">Impacto</span><span class="sxs-lookup"><span data-stu-id="ab53f-153">Impact</span></span>
- <span data-ttu-id="ab53f-154">Prioridade</span><span class="sxs-lookup"><span data-stu-id="ab53f-154">Priority</span></span>
- <span data-ttu-id="ab53f-155">Escalonamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-155">Escalation</span></span>
- <span data-ttu-id="ab53f-156">Criado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-156">Created By</span></span>
- <span data-ttu-id="ab53f-157">Resolvido por</span><span class="sxs-lookup"><span data-stu-id="ab53f-157">Resolved By</span></span>
- <span data-ttu-id="ab53f-158">Fechado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-158">Closed By</span></span>
- <span data-ttu-id="ab53f-159">Fonte</span><span class="sxs-lookup"><span data-stu-id="ab53f-159">Source</span></span>
- <span data-ttu-id="ab53f-160">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="ab53f-160">Assigned To</span></span>
- <span data-ttu-id="ab53f-161">Categoria</span><span class="sxs-lookup"><span data-stu-id="ab53f-161">Category</span></span>
- <span data-ttu-id="ab53f-162">Title</span><span class="sxs-lookup"><span data-stu-id="ab53f-162">Title</span></span>
- <span data-ttu-id="ab53f-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="ab53f-163">Description</span></span>
- <span data-ttu-id="ab53f-164">Data de criação</span><span class="sxs-lookup"><span data-stu-id="ab53f-164">Created Date</span></span>
- <span data-ttu-id="ab53f-165">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-165">Closed Date</span></span>
- <span data-ttu-id="ab53f-166">Data de resolução</span><span class="sxs-lookup"><span data-stu-id="ab53f-166">Resolved Date</span></span>
- <span data-ttu-id="ab53f-167">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="ab53f-167">Last Modified Date</span></span>
- <span data-ttu-id="ab53f-168">Computador</span><span class="sxs-lookup"><span data-stu-id="ab53f-168">Computer</span></span>


<span data-ttu-id="ab53f-169">**Item de trabalho:** **Solicitações de alteração**</span><span class="sxs-lookup"><span data-stu-id="ab53f-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="ab53f-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="ab53f-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="ab53f-171">**Campos**</span><span class="sxs-lookup"><span data-stu-id="ab53f-171">**Fields**</span></span>
- <span data-ttu-id="ab53f-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="ab53f-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="ab53f-173">ID da Central de Serviços</span><span class="sxs-lookup"><span data-stu-id="ab53f-173">Service Desk ID</span></span>
- <span data-ttu-id="ab53f-174">Criado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-174">Created By</span></span>
- <span data-ttu-id="ab53f-175">Fechado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-175">Closed By</span></span>
- <span data-ttu-id="ab53f-176">Fonte</span><span class="sxs-lookup"><span data-stu-id="ab53f-176">Source</span></span>
- <span data-ttu-id="ab53f-177">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="ab53f-177">Assigned To</span></span>
- <span data-ttu-id="ab53f-178">Title</span><span class="sxs-lookup"><span data-stu-id="ab53f-178">Title</span></span>
- <span data-ttu-id="ab53f-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="ab53f-179">Type</span></span>
- <span data-ttu-id="ab53f-180">Categoria</span><span class="sxs-lookup"><span data-stu-id="ab53f-180">Category</span></span>
- <span data-ttu-id="ab53f-181">Estado</span><span class="sxs-lookup"><span data-stu-id="ab53f-181">State</span></span>
- <span data-ttu-id="ab53f-182">Escalonamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-182">Escalation</span></span>
- <span data-ttu-id="ab53f-183">Status do conflito</span><span class="sxs-lookup"><span data-stu-id="ab53f-183">Conflict Status</span></span>
- <span data-ttu-id="ab53f-184">Urgência</span><span class="sxs-lookup"><span data-stu-id="ab53f-184">Urgency</span></span>
- <span data-ttu-id="ab53f-185">Prioridade</span><span class="sxs-lookup"><span data-stu-id="ab53f-185">Priority</span></span>
- <span data-ttu-id="ab53f-186">Risco</span><span class="sxs-lookup"><span data-stu-id="ab53f-186">Risk</span></span>
- <span data-ttu-id="ab53f-187">Impacto</span><span class="sxs-lookup"><span data-stu-id="ab53f-187">Impact</span></span>
- <span data-ttu-id="ab53f-188">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="ab53f-188">Assigned To</span></span>
- <span data-ttu-id="ab53f-189">Data de criação</span><span class="sxs-lookup"><span data-stu-id="ab53f-189">Created Date</span></span>
- <span data-ttu-id="ab53f-190">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-190">Closed Date</span></span>
- <span data-ttu-id="ab53f-191">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="ab53f-191">Last Modified Date</span></span>
- <span data-ttu-id="ab53f-192">Data de solicitação</span><span class="sxs-lookup"><span data-stu-id="ab53f-192">Requested Date</span></span>
- <span data-ttu-id="ab53f-193">Data de início prevista</span><span class="sxs-lookup"><span data-stu-id="ab53f-193">Planned Start Date</span></span>
- <span data-ttu-id="ab53f-194">Data de término prevista</span><span class="sxs-lookup"><span data-stu-id="ab53f-194">Planned End Date</span></span>
- <span data-ttu-id="ab53f-195">Data de início do trabalho</span><span class="sxs-lookup"><span data-stu-id="ab53f-195">Work Start Date</span></span>
- <span data-ttu-id="ab53f-196">Data de término do trabalho</span><span class="sxs-lookup"><span data-stu-id="ab53f-196">Work End Date</span></span>
- <span data-ttu-id="ab53f-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="ab53f-197">Description</span></span>
- <span data-ttu-id="ab53f-198">Computador</span><span class="sxs-lookup"><span data-stu-id="ab53f-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="ab53f-199">Dados de saída de um incidente do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ab53f-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="ab53f-200">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-200">OMS field</span></span> | <span data-ttu-id="ab53f-201">Campo do ITSM</span><span class="sxs-lookup"><span data-stu-id="ab53f-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab53f-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-202">ServiceDeskId_s</span></span>| <span data-ttu-id="ab53f-203">Número</span><span class="sxs-lookup"><span data-stu-id="ab53f-203">Number</span></span> |
| <span data-ttu-id="ab53f-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-204">IncidentState_s</span></span> | <span data-ttu-id="ab53f-205">Estado</span><span class="sxs-lookup"><span data-stu-id="ab53f-205">State</span></span> |
| <span data-ttu-id="ab53f-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-206">Urgency_s</span></span> |<span data-ttu-id="ab53f-207">Urgência</span><span class="sxs-lookup"><span data-stu-id="ab53f-207">Urgency</span></span> |
| <span data-ttu-id="ab53f-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-208">Impact_s</span></span> |<span data-ttu-id="ab53f-209">Impacto</span><span class="sxs-lookup"><span data-stu-id="ab53f-209">Impact</span></span>|
| <span data-ttu-id="ab53f-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-210">Priority_s</span></span> | <span data-ttu-id="ab53f-211">Prioridade</span><span class="sxs-lookup"><span data-stu-id="ab53f-211">Priority</span></span> |
| <span data-ttu-id="ab53f-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-212">CreatedBy_s</span></span> | <span data-ttu-id="ab53f-213">Aberto por</span><span class="sxs-lookup"><span data-stu-id="ab53f-213">Opened by</span></span> |
| <span data-ttu-id="ab53f-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-214">ResolvedBy_s</span></span> | <span data-ttu-id="ab53f-215">Resolvido por</span><span class="sxs-lookup"><span data-stu-id="ab53f-215">Resolved by</span></span>|
| <span data-ttu-id="ab53f-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-216">ClosedBy_s</span></span>  | <span data-ttu-id="ab53f-217">Fechado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-217">Closed by</span></span> |
| <span data-ttu-id="ab53f-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-218">Source_s</span></span>| <span data-ttu-id="ab53f-219">Tipo de contato</span><span class="sxs-lookup"><span data-stu-id="ab53f-219">Contact type</span></span> |
| <span data-ttu-id="ab53f-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-220">AssignedTo_s</span></span> | <span data-ttu-id="ab53f-221">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="ab53f-221">Assigned to</span></span>  |
| <span data-ttu-id="ab53f-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-222">Category_s</span></span> | <span data-ttu-id="ab53f-223">Categoria</span><span class="sxs-lookup"><span data-stu-id="ab53f-223">Category</span></span> |
| <span data-ttu-id="ab53f-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-224">Title_s</span></span>|  <span data-ttu-id="ab53f-225">Descrição breve</span><span class="sxs-lookup"><span data-stu-id="ab53f-225">Short description</span></span> |
| <span data-ttu-id="ab53f-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-226">Description_s</span></span>|  <span data-ttu-id="ab53f-227">Observações</span><span class="sxs-lookup"><span data-stu-id="ab53f-227">Notes</span></span> |
| <span data-ttu-id="ab53f-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-228">CreatedDate_t</span></span>|  <span data-ttu-id="ab53f-229">Aberto</span><span class="sxs-lookup"><span data-stu-id="ab53f-229">Opened</span></span> |
| <span data-ttu-id="ab53f-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-230">ClosedDate_t</span></span>| <span data-ttu-id="ab53f-231">closed</span><span class="sxs-lookup"><span data-stu-id="ab53f-231">closed</span></span>|
| <span data-ttu-id="ab53f-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-232">ResolvedDate_t</span></span>|<span data-ttu-id="ab53f-233">Resolvido</span><span class="sxs-lookup"><span data-stu-id="ab53f-233">Resolved</span></span>|
| <span data-ttu-id="ab53f-234">Computador</span><span class="sxs-lookup"><span data-stu-id="ab53f-234">Computer</span></span>  | <span data-ttu-id="ab53f-235">Item de configuração</span><span class="sxs-lookup"><span data-stu-id="ab53f-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="ab53f-236">Dados de saída para uma solicitação de alteração do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ab53f-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="ab53f-237">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-237">OMS field</span></span> | <span data-ttu-id="ab53f-238">Campo do ITSM</span><span class="sxs-lookup"><span data-stu-id="ab53f-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab53f-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-239">ServiceDeskId_s</span></span>| <span data-ttu-id="ab53f-240">Número</span><span class="sxs-lookup"><span data-stu-id="ab53f-240">Number</span></span> |
| <span data-ttu-id="ab53f-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-241">CreatedBy_s</span></span> | <span data-ttu-id="ab53f-242">Solicitado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-242">Requested by</span></span> |
| <span data-ttu-id="ab53f-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-243">ClosedBy_s</span></span> | <span data-ttu-id="ab53f-244">Fechado por</span><span class="sxs-lookup"><span data-stu-id="ab53f-244">Closed by</span></span> |
| <span data-ttu-id="ab53f-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-245">AssignedTo_s</span></span> | <span data-ttu-id="ab53f-246">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="ab53f-246">Assigned to</span></span>  |
| <span data-ttu-id="ab53f-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-247">Title_s</span></span>|  <span data-ttu-id="ab53f-248">Descrição breve</span><span class="sxs-lookup"><span data-stu-id="ab53f-248">Short description</span></span> |
| <span data-ttu-id="ab53f-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-249">Type_s</span></span>|  <span data-ttu-id="ab53f-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="ab53f-250">Type</span></span> |
| <span data-ttu-id="ab53f-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-251">Category_s</span></span>|  <span data-ttu-id="ab53f-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="ab53f-252">Catgory</span></span> |
| <span data-ttu-id="ab53f-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-253">CRState_s</span></span>|  <span data-ttu-id="ab53f-254">Estado</span><span class="sxs-lookup"><span data-stu-id="ab53f-254">State</span></span>|
| <span data-ttu-id="ab53f-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-255">Urgency_s</span></span>|  <span data-ttu-id="ab53f-256">Urgência</span><span class="sxs-lookup"><span data-stu-id="ab53f-256">Urgency</span></span> |
| <span data-ttu-id="ab53f-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-257">Priority_s</span></span>| <span data-ttu-id="ab53f-258">Prioridade</span><span class="sxs-lookup"><span data-stu-id="ab53f-258">Priority</span></span>|
| <span data-ttu-id="ab53f-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-259">Risk_s</span></span>| <span data-ttu-id="ab53f-260">Risco</span><span class="sxs-lookup"><span data-stu-id="ab53f-260">Risk</span></span>|
| <span data-ttu-id="ab53f-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-261">Impact_s</span></span>| <span data-ttu-id="ab53f-262">Impacto</span><span class="sxs-lookup"><span data-stu-id="ab53f-262">Impact</span></span>|
| <span data-ttu-id="ab53f-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-263">RequestedDate_t</span></span>  | <span data-ttu-id="ab53f-264">Solicitado por data</span><span class="sxs-lookup"><span data-stu-id="ab53f-264">Requested by date</span></span> |
| <span data-ttu-id="ab53f-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-265">ClosedDate_t</span></span> | <span data-ttu-id="ab53f-266">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="ab53f-266">Closed date</span></span> |
| <span data-ttu-id="ab53f-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="ab53f-268">Data de início planejada</span><span class="sxs-lookup"><span data-stu-id="ab53f-268">Planned start date</span></span> |
| <span data-ttu-id="ab53f-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="ab53f-270">Data de término planejada</span><span class="sxs-lookup"><span data-stu-id="ab53f-270">Planned end date</span></span> |
| <span data-ttu-id="ab53f-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-271">WorkStartDate_t</span></span>  | <span data-ttu-id="ab53f-272">Data de início real</span><span class="sxs-lookup"><span data-stu-id="ab53f-272">Actual start date</span></span> |
| <span data-ttu-id="ab53f-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="ab53f-273">WorkEndDate_t</span></span> | <span data-ttu-id="ab53f-274">Data de término real</span><span class="sxs-lookup"><span data-stu-id="ab53f-274">Actual end date</span></span>|
| <span data-ttu-id="ab53f-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="ab53f-275">Description_s</span></span> | <span data-ttu-id="ab53f-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="ab53f-276">Description</span></span> |
| <span data-ttu-id="ab53f-277">Computador</span><span class="sxs-lookup"><span data-stu-id="ab53f-277">Computer</span></span>  | <span data-ttu-id="ab53f-278">Item de Configuração</span><span class="sxs-lookup"><span data-stu-id="ab53f-278">Configuration Item</span></span> |

<span data-ttu-id="ab53f-279">**Tela de exemplo do Log Analytics para dados de ITSM:**</span><span class="sxs-lookup"><span data-stu-id="ab53f-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="ab53f-281">Conector de Gerenciamento de Serviço de TI – integração com outras soluções do OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="ab53f-282">Atualmente, o Conector de Gerenciamento de Serviço de TI dá suporte à integração com a solução Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="ab53f-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="ab53f-283">O Mapa do Serviço descobre automaticamente os componentes de aplicativos em sistemas Windows e Linux e mapeia a comunicação entre os serviços.</span><span class="sxs-lookup"><span data-stu-id="ab53f-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="ab53f-284">Ele permite que você exiba os seus servidores da maneira como pensa neles – como sistemas interconectados que fornecem serviços essenciais.</span><span class="sxs-lookup"><span data-stu-id="ab53f-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="ab53f-285">O Mapa do Serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectada a TCP sem nenhuma configuração necessária além da instalação de um agente.</span><span class="sxs-lookup"><span data-stu-id="ab53f-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="ab53f-286">Mais informações: [Mapa do Serviço](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="ab53f-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="ab53f-287">Com essa integração, é possível exibir os itens da central de serviços criados nas soluções de ITSM, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="ab53f-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="ab53f-288">Solução integrada</span><span class="sxs-lookup"><span data-stu-id="ab53f-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="ab53f-289">Criar itens de trabalho de ITSM para alertas do OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="ab53f-290">Para os alertas do OMS, é possível criar itens de trabalho associados nas fontes de ITSM conectadas.</span><span class="sxs-lookup"><span data-stu-id="ab53f-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="ab53f-291">Para fazer isso, use o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="ab53f-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="ab53f-292">Na janela **Pesquisa de Logs**, execute uma consulta da pesquisa de logs para exibir os dados.</span><span class="sxs-lookup"><span data-stu-id="ab53f-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="ab53f-293">Os resultados da consulta são a fonte de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab53f-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="ab53f-294">Em **Pesquisa de Logs**, clique em **Alerta** para abrir a página **Adicionar Regra de Alerta**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="ab53f-296">Na janela **Adicionar Regra de Alerta**, forneça os detalhes necessários para **Nome**, **Gravidade**, **Consulta de pesquisa** e **Critérios de alerta** (medição Janela de Tempo/Métrica).</span><span class="sxs-lookup"><span data-stu-id="ab53f-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="ab53f-297">Selecione **Sim** para **Ações de ITSM**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="ab53f-298">Selecione a conexão de ITSM na lista **Selecionar Conexão**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="ab53f-299">Forneça os detalhes conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="ab53f-299">Provide the details as required.</span></span>
7. <span data-ttu-id="ab53f-300">Para criar um item de trabalho separado para cada entrada de log desse alerta, marque a caixa de seleção **Criar itens de trabalho individuais para cada entrada de log**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="ab53f-301">Ou</span><span class="sxs-lookup"><span data-stu-id="ab53f-301">Or</span></span>

    <span data-ttu-id="ab53f-302">deixe essa caixa de seleção desmarcada para criar apenas um item de trabalho para qualquer quantidade de entradas de log nesse alerta.</span><span class="sxs-lookup"><span data-stu-id="ab53f-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="ab53f-303">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-303">Click **Save**.</span></span>

<span data-ttu-id="ab53f-304">O alerta do OMS será criado em **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="ab53f-305">Os itens de trabalho da conexão de ITSM correspondentes são criados quando o critério do alerta especificado é atendido.</span><span class="sxs-lookup"><span data-stu-id="ab53f-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="ab53f-306">Criar itens de trabalho de ITSM com base em logs do OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="ab53f-307">É possível criar itens de trabalho nas fontes de ITSM conectadas usando a Pesquisa de Logs do OMS.</span><span class="sxs-lookup"><span data-stu-id="ab53f-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="ab53f-308">Para fazer isso, use o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="ab53f-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="ab53f-309">Na **Pesquisa de Logs**, pesquise os dados necessários, selecione os detalhes e clique em **Criar item de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="ab53f-310">A janela **Criar item de trabalho de ITSM** é exibida:</span><span class="sxs-lookup"><span data-stu-id="ab53f-310">The **Create ITSM Work item** window appears:</span></span>

    ![Tela do Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="ab53f-312">Adicione os seguintes detalhes:</span><span class="sxs-lookup"><span data-stu-id="ab53f-312">Add the following details:</span></span>

  - <span data-ttu-id="ab53f-313">**Título do Item de trabalho**: título do item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab53f-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="ab53f-314">**Descrição do Item de trabalho**: descrição do novo item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab53f-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="ab53f-315">**Computador Afetado**: nome do computador no qual esses dados de logs foram encontrados.</span><span class="sxs-lookup"><span data-stu-id="ab53f-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="ab53f-316">**Selecionar Conexão**: conexão de ITSM na qual você deseja criar esse item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab53f-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="ab53f-317">**Item de trabalho**: tipo de item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab53f-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="ab53f-318">Para usar um modelo de item de trabalho existente para um incidente, clique em **Sim** na opção **Gerar item de trabalho com base no modelo** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="ab53f-319">Ou,</span><span class="sxs-lookup"><span data-stu-id="ab53f-319">Or,</span></span>

    <span data-ttu-id="ab53f-320">Clique em **Não** se desejar fornecer valores personalizados.</span><span class="sxs-lookup"><span data-stu-id="ab53f-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="ab53f-321">Forneça os valores apropriados nas caixas de texto **Tipo de Contato**, **Impacto**, **Urgência**, **Categoria** e **Subcategoria** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="ab53f-322">O item de trabalho será criado no ITSM, que também pode ser exibido no OMS.</span><span class="sxs-lookup"><span data-stu-id="ab53f-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="ab53f-323">Solucionar problemas de conexões de ITSM no OMS</span><span class="sxs-lookup"><span data-stu-id="ab53f-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="ab53f-324">Se houver falha da conexão da interface do usuário da fonte conectada e você receber a mensagem **Erro ao salvar a conexão**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab53f-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="ab53f-325">No caso de conexões do ServiceNow, do Cherwell e do Provance, verifique se você digitou corretamente o nome de usuário/senha e ID do cliente/segredo do cliente para cada uma das conexões.</span><span class="sxs-lookup"><span data-stu-id="ab53f-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="ab53f-326">Se o erro persistir, verifique se você tem privilégios suficientes no produto ITSM correspondente para fazer a conexão.</span><span class="sxs-lookup"><span data-stu-id="ab53f-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="ab53f-327">No caso do Service Manager, certifique-se de que o aplicativo Web está implantado com êxito e conexão híbrida está criada.</span><span class="sxs-lookup"><span data-stu-id="ab53f-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="ab53f-328">Para verificar se a conexão está estabelecida com êxito com o computador do Service Manager local, visite a URL do aplicativo Web conforme detalhado na documentação para fazer a [conexão híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="ab53f-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="ab53f-329">Se os dados do ServiceNow não estiverem sendo sincronizados no OMS, certifique-se de que a instância do ServiceNow não está em suspensão.</span><span class="sxs-lookup"><span data-stu-id="ab53f-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="ab53f-330">Isso pode acontecer em algum momento nas instâncias de desenvolvimento do ServiceNow, quando estão ociosas.</span><span class="sxs-lookup"><span data-stu-id="ab53f-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="ab53f-331">Caso contrário, relate o problema.</span><span class="sxs-lookup"><span data-stu-id="ab53f-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="ab53f-332">Se os alertas estiverem sendo disparados do OMS, mas os itens de trabalho não estiverem sendo criados no produto ITSM ou os itens de configuração não estiverem sendo criados/vinculados aos itens de trabalho ou para qualquer informação genérica, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab53f-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="ab53f-333">A solução do Conector de Gerenciamento do Serviço de TI no portal do OMS poderia ser usada para obter um resumo das conexões/itens de trabalho/computadores etc. Clique na mensagem de erro na folha de status, navegue até **Pesquisa de Logs** e exiba a conexão com o erro usando os detalhes na mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="ab53f-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="ab53f-334">você pode exibir diretamente os erros/informações relacionadas na página **Pesquisa de Logs** usando *Type=ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="ab53f-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="ab53f-335">Solucionar problemas de implantação do aplicativo Web do Service Manager</span><span class="sxs-lookup"><span data-stu-id="ab53f-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="ab53f-336">No caso de problemas com a implantação do aplicativo Web, verifique se que você tem permissões suficientes na assinatura mencionada para criar/implantar recursos.</span><span class="sxs-lookup"><span data-stu-id="ab53f-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="ab53f-337">Se a mensagem de erro **Object reference not set to instance of an object (Referência do objeto não definida para a instância de um objeto)** aparecer ao executar o [script](log-analytics-itsmc-service-manager-script.md), certifique-se de ter inserido valores válidos na seção **Configuração do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ab53f-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="ab53f-338">Se você não conseguir criar o namespace de retransmissão do barramento de serviço, certifique-se de que o provedor de recursos necessário está registrado na assinatura.</span><span class="sxs-lookup"><span data-stu-id="ab53f-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="ab53f-339">Se não estiver registrado, crie-o manualmente no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab53f-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="ab53f-340">Você também pode criá-lo ao [criar a conexão híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab53f-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="ab53f-341">Fale conosco</span><span class="sxs-lookup"><span data-stu-id="ab53f-341">Contact us</span></span>

<span data-ttu-id="ab53f-342">Em caso de dúvidas ou comentários sobre o Conector de Gerenciamento de Serviço de TI, entre em contato conosco pelo email [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ab53f-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab53f-343">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab53f-343">Next steps</span></span>
<span data-ttu-id="ab53f-344">[Adicionar produtos/serviços de ITSM ao Conector de Gerenciamento de Serviço de TI](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="ab53f-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
