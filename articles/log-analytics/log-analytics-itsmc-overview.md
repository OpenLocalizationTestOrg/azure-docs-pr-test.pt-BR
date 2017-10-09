---
title: "aaaIT conector de gerenciamento de serviço do OMS | Microsoft Docs"
description: "Use o monitor de toocentrally Olá conector de gerenciamento de serviço de TI e gerenciar itens de trabalho ITSM Olá no OMS e resolver problemas rapidamente."
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="cb970-103">Gerenciar itens de trabalho de ITSM de forma centralizada usando o Conector de Gerenciamento de Serviço de TI (Visualização)</span><span class="sxs-lookup"><span data-stu-id="cb970-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Símbolo do Conector de Gerenciamento do Serviço de TI](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="cb970-105">Você pode usar o hello conector de gerenciamento de serviço de TI (ITSMC) no monitor de toocentrally de análise de logs do OMS e gerenciar itens de trabalho entre seus produtos/serviços ITSM.</span><span class="sxs-lookup"><span data-stu-id="cb970-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="cb970-106">Olá conector de gerenciamento de serviço de TI se integra a seus serviços e produtos de gerenciamento de serviço de TI (ITSM) existentes com análise de logs do OMS.</span><span class="sxs-lookup"><span data-stu-id="cb970-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="cb970-107">solução de saudação tem integração bidirecional com ITSM produtos/serviços, onde ele fornece Olá incidentes opção toocreate os usuários do OMS, alertas ou eventos em solução ITSM.</span><span class="sxs-lookup"><span data-stu-id="cb970-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="cb970-108">conector de saudação também importa dados, como incidentes e solicitações de alteração de solução ITSM em análise de logs do OMS.</span><span class="sxs-lookup"><span data-stu-id="cb970-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="cb970-109">Com o Conector de Gerenciamento de Serviço de TI, você pode:</span><span class="sxs-lookup"><span data-stu-id="cb970-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="cb970-110">Monitorar e gerenciar itens de trabalho para produtos/serviços de ITSM usados em sua organização de forma centralizada.</span><span class="sxs-lookup"><span data-stu-id="cb970-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="cb970-111">Criar itens de trabalho de ITSM (como alerta, evento e incidente) no ITSM com base em alertas do OMS e por meio da pesquisa de logs.</span><span class="sxs-lookup"><span data-stu-id="cb970-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="cb970-112">Ler incidentes e solicitações de alteração na solução de ITSM e correlacioná-los com os dados de logs relevantes no espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cb970-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="cb970-113">Localizar qualquer evento inesperado e incomuns e resolvê-los, mesmo para que os usuários finais de saudação chamar e relatá-los toohello helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cb970-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="cb970-114">Importar dados de itens de trabalho para o Log Analytics e criar relatórios de KPI (indicador chave de desempenho).</span><span class="sxs-lookup"><span data-stu-id="cb970-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="cb970-115">Com esses relatórios, você pode identificar, avaliar e tomar decisões em relação a vários itens importantes, como avaliação de malware.</span><span class="sxs-lookup"><span data-stu-id="cb970-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="cb970-116">Exibir painéis estruturados para obter informações mais profundas sobre incidentes, solicitações de alteração e sistemas afetados.</span><span class="sxs-lookup"><span data-stu-id="cb970-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="cb970-117">Solucionar problemas mais rapidamente, correlacionando com outras soluções de gerenciamento no espaço de trabalho de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb970-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cb970-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb970-118">Prerequisites</span></span>

<span data-ttu-id="cb970-119">itens de trabalho tooimport Olá ITSM em análise de logs do OMS, Olá solução exige que uma conexão entre hello conector de gerenciamento de serviço de TI no hello OMS e Olá TI SM produto/serviço do qual você importa os itens de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="cb970-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="cb970-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="cb970-120">Configuration</span></span>

<span data-ttu-id="cb970-121">Saudação de adicionar espaço de trabalho do OMS conector de gerenciamento de serviço de TI solução tooyour, usando Olá processo descrito na [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="cb970-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="cb970-122">Conector de gerenciamento de serviço IT bloco que você vê na Galeria de soluções de saudação:</span><span class="sxs-lookup"><span data-stu-id="cb970-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![bloco do conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="cb970-124">Após a adição bem-sucedida, você verá Olá conector de gerenciamento de serviço de TI em **OMS** > **configurações** > **fontes conectadas.**</span><span class="sxs-lookup"><span data-stu-id="cb970-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="cb970-126">Por padrão, o Olá conector de gerenciamento de serviço de TI atualiza os dados da conexão Olá uma vez em cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cb970-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="cb970-127">toorefresh instantaneamente para as edições ou modelo as da conexão atualizações de dados que você fizer, clique em conexão botão exibido tooyour próxima atualização hello.</span><span class="sxs-lookup"><span data-stu-id="cb970-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Atualização do ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="cb970-129">Pacotes de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cb970-129">Management packs</span></span>
<span data-ttu-id="cb970-130">Essa solução não exige nenhum pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="cb970-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="cb970-131">Fontes conectadas</span><span class="sxs-lookup"><span data-stu-id="cb970-131">Connected sources</span></span>

<span data-ttu-id="cb970-132">Olá ITSM seguintes produtos/serviços são suportados pelo Olá conector de gerenciamento de serviço de TI:</span><span class="sxs-lookup"><span data-stu-id="cb970-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="cb970-133">SCSM (System Center Service Manager)</span><span class="sxs-lookup"><span data-stu-id="cb970-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="cb970-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cb970-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="cb970-135">Provance</span><span class="sxs-lookup"><span data-stu-id="cb970-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="cb970-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="cb970-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="cb970-137">Usando a solução de saudação</span><span class="sxs-lookup"><span data-stu-id="cb970-137">Using hello solution</span></span>

<span data-ttu-id="cb970-138">Quando você conecta Olá conector de gerenciamento de serviço de TI de OMS com seu serviço ITSM, serviços de análise de Log Olá inicia a coleta de dados Olá Olá conectado ITSM produtos/serviço.</span><span class="sxs-lookup"><span data-stu-id="cb970-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="cb970-139">Os dados importados pelo Conector de Gerenciamento do Serviço de TI são exibidos no Log Analytics como eventos chamados **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="cb970-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="cb970-140">O evento contém um campo chamado **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="cb970-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="cb970-141">que pode ter seu valor como um incidente, ou solicitação de alteração, dependendo de saudação do item de trabalho dados contidos em Olá **ServiceDesk_CL** eventos.</span><span class="sxs-lookup"><span data-stu-id="cb970-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="cb970-142">Dados de entrada</span><span class="sxs-lookup"><span data-stu-id="cb970-142">Input data</span></span>
<span data-ttu-id="cb970-143">Itens de trabalho importados de saudação ITSM produtos/serviços.</span><span class="sxs-lookup"><span data-stu-id="cb970-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="cb970-144">Olá informações a seguir mostram exemplos de dados coletados pelo conector de gerenciamento de serviços de saudação:</span><span class="sxs-lookup"><span data-stu-id="cb970-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="cb970-145">Dependendo de saudação do item de trabalho tipo importado para a análise de Log, **ServiceDesk_CL** contém Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="cb970-146">**Item de trabalho:** **Incidentes**</span><span class="sxs-lookup"><span data-stu-id="cb970-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="cb970-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="cb970-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="cb970-148">**Campos**</span><span class="sxs-lookup"><span data-stu-id="cb970-148">**Fields**</span></span>

- <span data-ttu-id="cb970-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="cb970-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="cb970-150">ID da Central de Serviços</span><span class="sxs-lookup"><span data-stu-id="cb970-150">Service Desk ID</span></span>
- <span data-ttu-id="cb970-151">Estado</span><span class="sxs-lookup"><span data-stu-id="cb970-151">State</span></span>
- <span data-ttu-id="cb970-152">Urgência</span><span class="sxs-lookup"><span data-stu-id="cb970-152">Urgency</span></span>
- <span data-ttu-id="cb970-153">Impacto</span><span class="sxs-lookup"><span data-stu-id="cb970-153">Impact</span></span>
- <span data-ttu-id="cb970-154">Prioridade</span><span class="sxs-lookup"><span data-stu-id="cb970-154">Priority</span></span>
- <span data-ttu-id="cb970-155">Escalonamento</span><span class="sxs-lookup"><span data-stu-id="cb970-155">Escalation</span></span>
- <span data-ttu-id="cb970-156">Criado por</span><span class="sxs-lookup"><span data-stu-id="cb970-156">Created By</span></span>
- <span data-ttu-id="cb970-157">Resolvido por</span><span class="sxs-lookup"><span data-stu-id="cb970-157">Resolved By</span></span>
- <span data-ttu-id="cb970-158">Fechado por</span><span class="sxs-lookup"><span data-stu-id="cb970-158">Closed By</span></span>
- <span data-ttu-id="cb970-159">Fonte</span><span class="sxs-lookup"><span data-stu-id="cb970-159">Source</span></span>
- <span data-ttu-id="cb970-160">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="cb970-160">Assigned To</span></span>
- <span data-ttu-id="cb970-161">Categoria</span><span class="sxs-lookup"><span data-stu-id="cb970-161">Category</span></span>
- <span data-ttu-id="cb970-162">Title</span><span class="sxs-lookup"><span data-stu-id="cb970-162">Title</span></span>
- <span data-ttu-id="cb970-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb970-163">Description</span></span>
- <span data-ttu-id="cb970-164">Data de criação</span><span class="sxs-lookup"><span data-stu-id="cb970-164">Created Date</span></span>
- <span data-ttu-id="cb970-165">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="cb970-165">Closed Date</span></span>
- <span data-ttu-id="cb970-166">Data de resolução</span><span class="sxs-lookup"><span data-stu-id="cb970-166">Resolved Date</span></span>
- <span data-ttu-id="cb970-167">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="cb970-167">Last Modified Date</span></span>
- <span data-ttu-id="cb970-168">Computador</span><span class="sxs-lookup"><span data-stu-id="cb970-168">Computer</span></span>


<span data-ttu-id="cb970-169">**Item de trabalho:** **Solicitações de alteração**</span><span class="sxs-lookup"><span data-stu-id="cb970-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="cb970-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="cb970-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="cb970-171">**Campos**</span><span class="sxs-lookup"><span data-stu-id="cb970-171">**Fields**</span></span>
- <span data-ttu-id="cb970-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="cb970-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="cb970-173">ID da Central de Serviços</span><span class="sxs-lookup"><span data-stu-id="cb970-173">Service Desk ID</span></span>
- <span data-ttu-id="cb970-174">Criado por</span><span class="sxs-lookup"><span data-stu-id="cb970-174">Created By</span></span>
- <span data-ttu-id="cb970-175">Fechado por</span><span class="sxs-lookup"><span data-stu-id="cb970-175">Closed By</span></span>
- <span data-ttu-id="cb970-176">Fonte</span><span class="sxs-lookup"><span data-stu-id="cb970-176">Source</span></span>
- <span data-ttu-id="cb970-177">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="cb970-177">Assigned To</span></span>
- <span data-ttu-id="cb970-178">Title</span><span class="sxs-lookup"><span data-stu-id="cb970-178">Title</span></span>
- <span data-ttu-id="cb970-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="cb970-179">Type</span></span>
- <span data-ttu-id="cb970-180">Categoria</span><span class="sxs-lookup"><span data-stu-id="cb970-180">Category</span></span>
- <span data-ttu-id="cb970-181">Estado</span><span class="sxs-lookup"><span data-stu-id="cb970-181">State</span></span>
- <span data-ttu-id="cb970-182">Escalonamento</span><span class="sxs-lookup"><span data-stu-id="cb970-182">Escalation</span></span>
- <span data-ttu-id="cb970-183">Status do conflito</span><span class="sxs-lookup"><span data-stu-id="cb970-183">Conflict Status</span></span>
- <span data-ttu-id="cb970-184">Urgência</span><span class="sxs-lookup"><span data-stu-id="cb970-184">Urgency</span></span>
- <span data-ttu-id="cb970-185">Prioridade</span><span class="sxs-lookup"><span data-stu-id="cb970-185">Priority</span></span>
- <span data-ttu-id="cb970-186">Risco</span><span class="sxs-lookup"><span data-stu-id="cb970-186">Risk</span></span>
- <span data-ttu-id="cb970-187">Impacto</span><span class="sxs-lookup"><span data-stu-id="cb970-187">Impact</span></span>
- <span data-ttu-id="cb970-188">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="cb970-188">Assigned To</span></span>
- <span data-ttu-id="cb970-189">Data de criação</span><span class="sxs-lookup"><span data-stu-id="cb970-189">Created Date</span></span>
- <span data-ttu-id="cb970-190">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="cb970-190">Closed Date</span></span>
- <span data-ttu-id="cb970-191">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="cb970-191">Last Modified Date</span></span>
- <span data-ttu-id="cb970-192">Data de solicitação</span><span class="sxs-lookup"><span data-stu-id="cb970-192">Requested Date</span></span>
- <span data-ttu-id="cb970-193">Data de início prevista</span><span class="sxs-lookup"><span data-stu-id="cb970-193">Planned Start Date</span></span>
- <span data-ttu-id="cb970-194">Data de término prevista</span><span class="sxs-lookup"><span data-stu-id="cb970-194">Planned End Date</span></span>
- <span data-ttu-id="cb970-195">Data de início do trabalho</span><span class="sxs-lookup"><span data-stu-id="cb970-195">Work Start Date</span></span>
- <span data-ttu-id="cb970-196">Data de término do trabalho</span><span class="sxs-lookup"><span data-stu-id="cb970-196">Work End Date</span></span>
- <span data-ttu-id="cb970-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb970-197">Description</span></span>
- <span data-ttu-id="cb970-198">Computador</span><span class="sxs-lookup"><span data-stu-id="cb970-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="cb970-199">Dados de saída de um incidente do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cb970-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="cb970-200">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-200">OMS field</span></span> | <span data-ttu-id="cb970-201">Campo do ITSM</span><span class="sxs-lookup"><span data-stu-id="cb970-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="cb970-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="cb970-202">ServiceDeskId_s</span></span>| <span data-ttu-id="cb970-203">Número</span><span class="sxs-lookup"><span data-stu-id="cb970-203">Number</span></span> |
| <span data-ttu-id="cb970-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="cb970-204">IncidentState_s</span></span> | <span data-ttu-id="cb970-205">Estado</span><span class="sxs-lookup"><span data-stu-id="cb970-205">State</span></span> |
| <span data-ttu-id="cb970-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="cb970-206">Urgency_s</span></span> |<span data-ttu-id="cb970-207">Urgência</span><span class="sxs-lookup"><span data-stu-id="cb970-207">Urgency</span></span> |
| <span data-ttu-id="cb970-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="cb970-208">Impact_s</span></span> |<span data-ttu-id="cb970-209">Impacto</span><span class="sxs-lookup"><span data-stu-id="cb970-209">Impact</span></span>|
| <span data-ttu-id="cb970-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="cb970-210">Priority_s</span></span> | <span data-ttu-id="cb970-211">Prioridade</span><span class="sxs-lookup"><span data-stu-id="cb970-211">Priority</span></span> |
| <span data-ttu-id="cb970-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="cb970-212">CreatedBy_s</span></span> | <span data-ttu-id="cb970-213">Aberto por</span><span class="sxs-lookup"><span data-stu-id="cb970-213">Opened by</span></span> |
| <span data-ttu-id="cb970-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="cb970-214">ResolvedBy_s</span></span> | <span data-ttu-id="cb970-215">Resolvido por</span><span class="sxs-lookup"><span data-stu-id="cb970-215">Resolved by</span></span>|
| <span data-ttu-id="cb970-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="cb970-216">ClosedBy_s</span></span>  | <span data-ttu-id="cb970-217">Fechado por</span><span class="sxs-lookup"><span data-stu-id="cb970-217">Closed by</span></span> |
| <span data-ttu-id="cb970-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="cb970-218">Source_s</span></span>| <span data-ttu-id="cb970-219">Tipo de contato</span><span class="sxs-lookup"><span data-stu-id="cb970-219">Contact type</span></span> |
| <span data-ttu-id="cb970-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="cb970-220">AssignedTo_s</span></span> | <span data-ttu-id="cb970-221">Atribuído muito</span><span class="sxs-lookup"><span data-stu-id="cb970-221">Assigned too</span></span> |
| <span data-ttu-id="cb970-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="cb970-222">Category_s</span></span> | <span data-ttu-id="cb970-223">Categoria</span><span class="sxs-lookup"><span data-stu-id="cb970-223">Category</span></span> |
| <span data-ttu-id="cb970-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="cb970-224">Title_s</span></span>|  <span data-ttu-id="cb970-225">Descrição breve</span><span class="sxs-lookup"><span data-stu-id="cb970-225">Short description</span></span> |
| <span data-ttu-id="cb970-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="cb970-226">Description_s</span></span>|  <span data-ttu-id="cb970-227">Observações</span><span class="sxs-lookup"><span data-stu-id="cb970-227">Notes</span></span> |
| <span data-ttu-id="cb970-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-228">CreatedDate_t</span></span>|  <span data-ttu-id="cb970-229">Aberto</span><span class="sxs-lookup"><span data-stu-id="cb970-229">Opened</span></span> |
| <span data-ttu-id="cb970-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-230">ClosedDate_t</span></span>| <span data-ttu-id="cb970-231">closed</span><span class="sxs-lookup"><span data-stu-id="cb970-231">closed</span></span>|
| <span data-ttu-id="cb970-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-232">ResolvedDate_t</span></span>|<span data-ttu-id="cb970-233">Resolvido</span><span class="sxs-lookup"><span data-stu-id="cb970-233">Resolved</span></span>|
| <span data-ttu-id="cb970-234">Computador</span><span class="sxs-lookup"><span data-stu-id="cb970-234">Computer</span></span>  | <span data-ttu-id="cb970-235">Item de configuração</span><span class="sxs-lookup"><span data-stu-id="cb970-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="cb970-236">Dados de saída para uma solicitação de alteração do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cb970-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="cb970-237">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-237">OMS field</span></span> | <span data-ttu-id="cb970-238">Campo do ITSM</span><span class="sxs-lookup"><span data-stu-id="cb970-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="cb970-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="cb970-239">ServiceDeskId_s</span></span>| <span data-ttu-id="cb970-240">Número</span><span class="sxs-lookup"><span data-stu-id="cb970-240">Number</span></span> |
| <span data-ttu-id="cb970-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="cb970-241">CreatedBy_s</span></span> | <span data-ttu-id="cb970-242">Solicitado por</span><span class="sxs-lookup"><span data-stu-id="cb970-242">Requested by</span></span> |
| <span data-ttu-id="cb970-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="cb970-243">ClosedBy_s</span></span> | <span data-ttu-id="cb970-244">Fechado por</span><span class="sxs-lookup"><span data-stu-id="cb970-244">Closed by</span></span> |
| <span data-ttu-id="cb970-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="cb970-245">AssignedTo_s</span></span> | <span data-ttu-id="cb970-246">Atribuído muito</span><span class="sxs-lookup"><span data-stu-id="cb970-246">Assigned too</span></span> |
| <span data-ttu-id="cb970-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="cb970-247">Title_s</span></span>|  <span data-ttu-id="cb970-248">Descrição breve</span><span class="sxs-lookup"><span data-stu-id="cb970-248">Short description</span></span> |
| <span data-ttu-id="cb970-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="cb970-249">Type_s</span></span>|  <span data-ttu-id="cb970-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="cb970-250">Type</span></span> |
| <span data-ttu-id="cb970-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="cb970-251">Category_s</span></span>|  <span data-ttu-id="cb970-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="cb970-252">Catgory</span></span> |
| <span data-ttu-id="cb970-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="cb970-253">CRState_s</span></span>|  <span data-ttu-id="cb970-254">Estado</span><span class="sxs-lookup"><span data-stu-id="cb970-254">State</span></span>|
| <span data-ttu-id="cb970-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="cb970-255">Urgency_s</span></span>|  <span data-ttu-id="cb970-256">Urgência</span><span class="sxs-lookup"><span data-stu-id="cb970-256">Urgency</span></span> |
| <span data-ttu-id="cb970-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="cb970-257">Priority_s</span></span>| <span data-ttu-id="cb970-258">Prioridade</span><span class="sxs-lookup"><span data-stu-id="cb970-258">Priority</span></span>|
| <span data-ttu-id="cb970-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="cb970-259">Risk_s</span></span>| <span data-ttu-id="cb970-260">Risco</span><span class="sxs-lookup"><span data-stu-id="cb970-260">Risk</span></span>|
| <span data-ttu-id="cb970-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="cb970-261">Impact_s</span></span>| <span data-ttu-id="cb970-262">Impacto</span><span class="sxs-lookup"><span data-stu-id="cb970-262">Impact</span></span>|
| <span data-ttu-id="cb970-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-263">RequestedDate_t</span></span>  | <span data-ttu-id="cb970-264">Solicitado por data</span><span class="sxs-lookup"><span data-stu-id="cb970-264">Requested by date</span></span> |
| <span data-ttu-id="cb970-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-265">ClosedDate_t</span></span> | <span data-ttu-id="cb970-266">Data de fechamento</span><span class="sxs-lookup"><span data-stu-id="cb970-266">Closed date</span></span> |
| <span data-ttu-id="cb970-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="cb970-268">Data de início planejada</span><span class="sxs-lookup"><span data-stu-id="cb970-268">Planned start date</span></span> |
| <span data-ttu-id="cb970-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="cb970-270">Data de término planejada</span><span class="sxs-lookup"><span data-stu-id="cb970-270">Planned end date</span></span> |
| <span data-ttu-id="cb970-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-271">WorkStartDate_t</span></span>  | <span data-ttu-id="cb970-272">Data de início real</span><span class="sxs-lookup"><span data-stu-id="cb970-272">Actual start date</span></span> |
| <span data-ttu-id="cb970-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="cb970-273">WorkEndDate_t</span></span> | <span data-ttu-id="cb970-274">Data de término real</span><span class="sxs-lookup"><span data-stu-id="cb970-274">Actual end date</span></span>|
| <span data-ttu-id="cb970-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="cb970-275">Description_s</span></span> | <span data-ttu-id="cb970-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb970-276">Description</span></span> |
| <span data-ttu-id="cb970-277">Computador</span><span class="sxs-lookup"><span data-stu-id="cb970-277">Computer</span></span>  | <span data-ttu-id="cb970-278">Item de Configuração</span><span class="sxs-lookup"><span data-stu-id="cb970-278">Configuration Item</span></span> |

<span data-ttu-id="cb970-279">**Tela de exemplo do Log Analytics para dados de ITSM:**</span><span class="sxs-lookup"><span data-stu-id="cb970-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="cb970-281">Conector de Gerenciamento de Serviço de TI – integração com outras soluções do OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="cb970-282">Conector de gerenciamento de serviço IT, atualmente oferece suporte à integração com hello solução Mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="cb970-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="cb970-283">Mapa de serviço detecta automaticamente Olá componentes de aplicativos no Windows e mapas e sistemas Linux Olá comunicação entre serviços.</span><span class="sxs-lookup"><span data-stu-id="cb970-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="cb970-284">Ele permite que você tooview os servidores que você imagina – como sistemas interconectados que fornecem serviços essenciais.</span><span class="sxs-lookup"><span data-stu-id="cb970-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="cb970-285">O Mapa do Serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectada a TCP sem nenhuma configuração necessária além da instalação de um agente.</span><span class="sxs-lookup"><span data-stu-id="cb970-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="cb970-286">Mais informações: [Mapa do Serviço](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="cb970-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="cb970-287">Com essa integração, você pode exibir itens de suporte técnico de serviço Olá criados em soluções ITSM hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="cb970-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="cb970-288">Solução integrada</span><span class="sxs-lookup"><span data-stu-id="cb970-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="cb970-289">Criar itens de trabalho de ITSM para alertas do OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="cb970-290">Para alertas do OMS hello, você pode criar itens de trabalho associados em fontes de ITSM Olá conectado.</span><span class="sxs-lookup"><span data-stu-id="cb970-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="cb970-291">toodo, Olá use procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="cb970-292">De **pesquisa de Log** janela, execute um dados tooview de consulta de pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="cb970-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="cb970-293">Resultados da consulta são fonte Olá para itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cb970-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="cb970-294">Em **pesquisa de Log**, clique em **alerta** tooopen Olá **Adicionar regra de alerta** página.</span><span class="sxs-lookup"><span data-stu-id="cb970-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="cb970-296">Em Olá **Adicionar regra de alerta** janela, forneça detalhes Olá necessária para **nome**, **severidade**, **consulta de pesquisa**, e  **Critérios de alerta** (medida da métrica/janela de tempo).</span><span class="sxs-lookup"><span data-stu-id="cb970-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="cb970-297">Selecione **Sim** para **Ações de ITSM**.</span><span class="sxs-lookup"><span data-stu-id="cb970-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="cb970-298">Selecione sua conexão ITSM da saudação **Selecionar Conexão** lista.</span><span class="sxs-lookup"><span data-stu-id="cb970-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="cb970-299">Forneça detalhes Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="cb970-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="cb970-300">toocreate um item de trabalho separada para cada entrada de log de saudação esse alerta, selecione **criar itens de trabalho individuais para cada entrada de log** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="cb970-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="cb970-301">Ou</span><span class="sxs-lookup"><span data-stu-id="cb970-301">Or</span></span>

    <span data-ttu-id="cb970-302">Deixe essa caixa de seleção toocreate não selecionado apenas um item de trabalho para qualquer número de entradas de log sob esse alerta.</span><span class="sxs-lookup"><span data-stu-id="cb970-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="cb970-303">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cb970-303">Click **Save**.</span></span>

<span data-ttu-id="cb970-304">alerta OMS Hello será criada sob **alertas**.</span><span class="sxs-lookup"><span data-stu-id="cb970-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="cb970-305">Olá trabalho da conexão ITSM correspondente itens são criados quando a condição do alerta Olá especificada for atendida.</span><span class="sxs-lookup"><span data-stu-id="cb970-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="cb970-306">Criar itens de trabalho de ITSM com base em logs do OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="cb970-307">Você pode criar itens de trabalho em fontes de ITSM Olá conectado usando a pesquisa de Log do OMS.</span><span class="sxs-lookup"><span data-stu-id="cb970-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="cb970-308">toodo, Olá use procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="cb970-309">De **pesquisa de Log**, pesquisar dados Olá necessário, selecione os detalhes de saudação e clique em **criar item de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="cb970-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="cb970-310">Olá **item de trabalho de ITSM criar** janela é exibida:</span><span class="sxs-lookup"><span data-stu-id="cb970-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Tela do Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="cb970-312">Adicione Olá detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-312">Add hello following details:</span></span>

  - <span data-ttu-id="cb970-313">**Título do item de trabalho**: título Olá item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cb970-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="cb970-314">**Descrição do item de trabalho**: descrição Olá novo item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cb970-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="cb970-315">**Afetou o computador**: nome do computador Olá onde esses dados de log foi encontrados.</span><span class="sxs-lookup"><span data-stu-id="cb970-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="cb970-316">**Selecione a Conexão**: conexão ITSM no qual você deseja toocreate este item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cb970-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="cb970-317">**Item de trabalho**: tipo de item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cb970-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="cb970-318">toouse um modelo de item de trabalho existente de um incidente, clique em **Sim** em **gerar item de trabalho com base no modelo de saudação** opção e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="cb970-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="cb970-319">Ou,</span><span class="sxs-lookup"><span data-stu-id="cb970-319">Or,</span></span>

    <span data-ttu-id="cb970-320">Clique em **não** se você quiser tooprovide seus valores personalizados.</span><span class="sxs-lookup"><span data-stu-id="cb970-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="cb970-321">Forneça os valores adequados no Olá Olá **tipo de contato**, **impacto**, **urgência**, **categoria**, e **subcategoria**  caixas de texto e clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="cb970-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="cb970-322">item de trabalho Olá será criado no hello ITSM, que você também pode exibir no OMS.</span><span class="sxs-lookup"><span data-stu-id="cb970-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="cb970-323">Solucionar problemas de conexões de ITSM no OMS</span><span class="sxs-lookup"><span data-stu-id="cb970-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="cb970-324">Se a falha de conexão de interface de usuário da fonte conectada e obter Olá **erro ao salvar a conexão** mensagem, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="cb970-325">No caso de conexões de ServiceNow, Cherwell e Provance, certifique-se você segredo de ID e cliente cliente e o nome de usuário/senha Olá inseridos corretamente para cada uma das conexões de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb970-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="cb970-326">Se Olá erro persistir, verifique se você tem privilégios suficientes em conexão Olá correspondente ITSM produto toomake hello.</span><span class="sxs-lookup"><span data-stu-id="cb970-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="cb970-327">No caso do Service Manager, certifique-se de que Olá Web aplicativo é implantado com êxito e conexão híbrida é criada.</span><span class="sxs-lookup"><span data-stu-id="cb970-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="cb970-328">conexão de saudação tooverify é estabelecida com êxito com hello na Service Manager máquina local, visite a URL do aplicativo Web hello conforme detalhado na documentação de saudação para fazer Olá [conexão híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="cb970-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="cb970-329">Se não estiver obtendo sincronizados dados do ServiceNow do OMS, certifique-se de que essa instância do ServiceNow Olá não está em suspensão.</span><span class="sxs-lookup"><span data-stu-id="cb970-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="cb970-330">Isso pouco e pode ocorrer em Olá ServiceNow Dev instâncias, quando estão ociosos.</span><span class="sxs-lookup"><span data-stu-id="cb970-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="cb970-331">Else, problema de saudação de relatório.</span><span class="sxs-lookup"><span data-stu-id="cb970-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="cb970-332">Se estiverem obtendo acionados alertas do OMS, mas itens de trabalho não estão obtendo criados no produto ITSM ou itens de configuração não estão recebendo itens toowork criado/vinculado ou para todas as informações genéricas, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb970-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="cb970-333">Solução de conector do serviço de gerenciamento de TI no portal do OMS pode ser usado tooget um resumo de itens de trabalho/conexões/computadores etc. Clique em mensagem de erro de saudação na folha de status hello, navegue muito**pesquisa de Log** e exibir conexão Olá com erro hello usando detalhes da saudação na mensagem de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb970-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="cb970-334">diretamente você pode exibir informações de erros/relacionados Olá no hello **pesquisa de Log** página usando *tipo = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="cb970-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="cb970-335">Solucionar problemas de implantação do aplicativo Web do Service Manager</span><span class="sxs-lookup"><span data-stu-id="cb970-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="cb970-336">No caso de problemas com a implantação de aplicativo web, certifique-se de ter permissões suficientes na assinatura de saudação mencionado toocreate/implantar recursos.</span><span class="sxs-lookup"><span data-stu-id="cb970-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="cb970-337">Se **referência de objeto não definida tooinstance de um objeto** mensagem de erro é exibida durante a execução Olá [script](log-analytics-itsmc-service-manager-script.md) Certifique-se de que você inseriu valores válidos em **configuração do usuário**seção.</span><span class="sxs-lookup"><span data-stu-id="cb970-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="cb970-338">Se você não toocreate namespace de retransmissão de barramento de serviço, certifique-se de que Olá exigido de provedor de recursos está registrado na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb970-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="cb970-339">Se não estiver registrado, manualmente criá-la de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb970-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="cb970-340">Você também pode criá-lo ao [criar conexão de híbrida Olá](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb970-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="cb970-341">Fale conosco</span><span class="sxs-lookup"><span data-stu-id="cb970-341">Contact us</span></span>

<span data-ttu-id="cb970-342">Para todas as consultas ou comentários em Olá conector de gerenciamento de serviço de TI, entre em contato conosco em [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cb970-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb970-343">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb970-343">Next steps</span></span>
<span data-ttu-id="cb970-344">[Adicionar ITSM produtos/serviços tooIT conector de gerenciamento de serviço](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="cb970-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
