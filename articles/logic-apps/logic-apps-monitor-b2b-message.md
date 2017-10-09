---
title: "transações aaaMonitor B2B e configurar o log - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar mensagens AS2, X12 e EDIFACT e iniciar o log de diagnósticos da conta de integração"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="5ce18-103">Monitorar e configurar o log de diagnósticos para a comunicação B2B nas contas de integração</span><span class="sxs-lookup"><span data-stu-id="5ce18-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="5ce18-104">Depois de configurar a comunicação B2B entre dois processos ou aplicativos de negócios em execução por meio de sua conta de integração, essas entidades poderão trocar mensagens entre si.</span><span class="sxs-lookup"><span data-stu-id="5ce18-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="5ce18-105">tooconfirm essa comunicação funciona conforme o esperado, você pode configurar o monitoramento de AS2, X12, EDIFACT mensagens e, juntamente com o log de diagnóstico para sua conta de integração por meio de saudação [Azure Log Analytics](../log-analytics/log-analytics-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="5ce18-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="5ce18-106">Esse serviço do [OMS (Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md) monitora os ambientes locais e de nuvem, ajudando você a manter a disponibilidade e o desempenho deles e também coleta detalhes e eventos de tempo de execução para uma depuração mais avançada.</span><span class="sxs-lookup"><span data-stu-id="5ce18-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="5ce18-107">Use também [os dados de diagnóstico com outros serviços](#extend-diagnostic-data), como o Armazenamento do Azure e os Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ce18-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="5ce18-108">Requisitos</span><span class="sxs-lookup"><span data-stu-id="5ce18-108">Requirements</span></span>

* <span data-ttu-id="5ce18-109">Um aplicativo lógico configurado com o log de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="5ce18-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="5ce18-110">Saiba [como tooset o registro em log para esse aplicativo lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="5ce18-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="5ce18-111">Depois de atender esse requisito, você deve ter um espaço de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="5ce18-112">Você deve usar Olá mesmo espaço de trabalho do OMS ao configurar o registro em log para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="5ce18-113">Se você não tiver um espaço de trabalho do OMS, saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="5ce18-114">Uma conta de integração que foi vinculada tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ce18-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="5ce18-115">Saiba [como a conta toocreate uma integração com um aplicativo de lógica de tooyour link](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="5ce18-116">Ativar o log de diagnósticos da conta de integração</span><span class="sxs-lookup"><span data-stu-id="5ce18-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="5ce18-117">Você pode ativar registro em log diretamente de sua conta de integração ou [por meio de hello Azure Monitor service](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="5ce18-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="5ce18-118">O Azure Monitor fornece monitoramento básico com os dados no nível de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="5ce18-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="5ce18-119">Saiba mais sobre o [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="5ce18-120">Ativar o log de diagnósticos diretamente na conta de integração</span><span class="sxs-lookup"><span data-stu-id="5ce18-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="5ce18-121">Em Olá [portal do Azure](https://portal.azure.com), localize e selecione sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="5ce18-122">Em **Monitoramento**, escolha **Logs de diagnóstico**, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="5ce18-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Encontrar e selecionar a conta de integração e escolher “Logs de diagnóstico”](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="5ce18-124">Depois de selecionar a conta de integração, Olá valores a seguir é selecionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5ce18-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="5ce18-125">Se esses valores estiverem corretos, escolha **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="5ce18-126">Caso contrário, selecione os valores hello que você deseja:</span><span class="sxs-lookup"><span data-stu-id="5ce18-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="5ce18-127">Em **assinatura**, selecione Olá assinatura do Azure que você usa com sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="5ce18-128">Em **grupo de recursos**, selecione grupo de recursos de saudação que você usa com sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="5ce18-129">Em **Tipo de recurso**, selecione **Contas de integração**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="5ce18-130">Em **Recurso**, selecione a conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="5ce18-131">Escolha **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-131">Choose **Turn on diagnostics**.</span></span>

   ![Configurar o diagnóstico para sua conta de integração](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="5ce18-133">Em **Configurações de diagnóstico** e, em seguida, **Status**, escolha **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Ativar o Diagnóstico do Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="5ce18-135">Agora selecione toouse de espaço de trabalho e dados OMS de saudação para registro em log conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="5ce18-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="5ce18-136">Selecione **enviar tooLog análise**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="5ce18-137">Em **Log Analytics**, escolha **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="5ce18-138">Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.</span><span class="sxs-lookup"><span data-stu-id="5ce18-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="5ce18-139">Em **Log**, selecione Olá **IntegrationAccountTrackingEvents** categoria.</span><span class="sxs-lookup"><span data-stu-id="5ce18-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="5ce18-140">Escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-140">Choose **Save**.</span></span>

   ![Configurar a análise de Log para enviar o log de tooa de dados de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="5ce18-142">Agora, [configure o acompanhamento das mensagens B2B no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="5ce18-143">Ativar o log de diagnósticos por meio do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="5ce18-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="5ce18-144">Em Olá [portal do Azure](https://portal.azure.com), em Olá menu principal do Azure, escolha **Monitor**, **logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="5ce18-145">Depois, selecione sua conta de integração, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="5ce18-145">Then select your integration account as shown here:</span></span>

   ![Escolher “Monitorar”, “Logs de diagnóstico” e selecionar a conta de integração](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="5ce18-147">Depois de selecionar a conta de integração, Olá valores a seguir é selecionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5ce18-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="5ce18-148">Se esses valores estiverem corretos, escolha **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="5ce18-149">Caso contrário, selecione os valores hello que você deseja:</span><span class="sxs-lookup"><span data-stu-id="5ce18-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="5ce18-150">Em **assinatura**, selecione Olá assinatura do Azure que você usa com sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="5ce18-151">Em **grupo de recursos**, selecione grupo de recursos de saudação que você usa com sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="5ce18-152">Em **Tipo de recurso**, selecione **Contas de integração**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="5ce18-153">Em **Recurso**, selecione a conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5ce18-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="5ce18-154">Escolha **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-154">Choose **Turn on diagnostics**.</span></span>

   ![Configurar o diagnóstico para sua conta de integração](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="5ce18-156">Em **Configurações de diagnóstico**, escolha **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Ativar o Diagnóstico do Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="5ce18-158">Agora selecione categoria de evento e o espaço de trabalho OMS de saudação para registro em log conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="5ce18-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="5ce18-159">Selecione **enviar tooLog análise**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="5ce18-160">Em **Log Analytics**, escolha **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="5ce18-161">Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.</span><span class="sxs-lookup"><span data-stu-id="5ce18-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="5ce18-162">Em **Log**, selecione Olá **IntegrationAccountTrackingEvents** categoria.</span><span class="sxs-lookup"><span data-stu-id="5ce18-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="5ce18-163">Quando terminar, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ce18-163">When you're done, choose **Save**.</span></span>

   ![Configurar a análise de Log para enviar o log de tooa de dados de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="5ce18-165">Agora, [configure o acompanhamento das mensagens B2B no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="5ce18-166">Estender como e onde usar os dados de diagnóstico com outros serviços</span><span class="sxs-lookup"><span data-stu-id="5ce18-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="5ce18-167">Junto com o Azure Log Analytics, você pode estender a maneira de usar os dados de diagnóstico do aplicativo lógico com outros serviços do Azure, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5ce18-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="5ce18-168">Arquivar logs do Diagnóstico do Azure no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5ce18-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="5ce18-169">Fluxo de Logs de diagnóstico do Azure tooAzure Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="5ce18-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="5ce18-170">Depois, obtenha o monitoramento em tempo real usando a telemetria e a análise de outros serviços, como o [Stream Analytics do Azure](../stream-analytics/stream-analytics-introduction.md) e o [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="5ce18-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5ce18-171">For example:</span></span>

* [<span data-ttu-id="5ce18-172">Dados de fluxo de Hubs de eventos tooStream análise</span><span class="sxs-lookup"><span data-stu-id="5ce18-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="5ce18-173">Analisar dados de streaming com o Stream Analytics e criar um painel de análise em tempo real no Power BI</span><span class="sxs-lookup"><span data-stu-id="5ce18-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="5ce18-174">Com base nas opções de saudação que você deseja configurar, certifique-se de que você primeiro [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) ou [criar um hub de eventos do Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="5ce18-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="5ce18-175">Selecione as opções de saudação para onde você deseja que os dados de diagnóstico toosend:</span><span class="sxs-lookup"><span data-stu-id="5ce18-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Enviar dados tooAzure armazenamento conta ou evento de hub](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="5ce18-177">Períodos de retenção se aplicam somente quando você escolher toouse uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ce18-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="5ce18-178">Esquemas de acompanhamento com suporte</span><span class="sxs-lookup"><span data-stu-id="5ce18-178">Supported tracking schemas</span></span>

<span data-ttu-id="5ce18-179">Azure oferece suporte a esses tipos de esquema que têm fixos esquemas exceto Olá tipo personalizado de controle.</span><span class="sxs-lookup"><span data-stu-id="5ce18-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="5ce18-180">Esquema de acompanhamento do AS2</span><span class="sxs-lookup"><span data-stu-id="5ce18-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="5ce18-181">Esquema de acompanhamento do X12</span><span class="sxs-lookup"><span data-stu-id="5ce18-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="5ce18-182">Esquema de acompanhamento personalizado</span><span class="sxs-lookup"><span data-stu-id="5ce18-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="5ce18-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ce18-183">Next steps</span></span>

* [<span data-ttu-id="5ce18-184">Acompanhar mensagens B2B no OMS</span><span class="sxs-lookup"><span data-stu-id="5ce18-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Acompanhar mensagens B2B no OMS")
* [<span data-ttu-id="5ce18-185">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5ce18-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")

