---
title: aaaSet os alertas para consultas no Stream Analytics | Microsoft Docs
description: "Noções básicas sobre alertas do Stream Analytics"
keywords: configurar alertas
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="8a084-104">Configurar alertas para trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="8a084-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="8a084-105">Introdução: Página do monitor</span><span class="sxs-lookup"><span data-stu-id="8a084-105">Introduction: Monitor page</span></span>
<span data-ttu-id="8a084-106">Você pode configurar alertas tootrigger um alerta quando uma métrica atinge uma condição que você especificar.</span><span class="sxs-lookup"><span data-stu-id="8a084-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="8a084-107">Por exemplo, você pode configurar um alerta para uma condição semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="8a084-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="8a084-108">Regras podem ser definidas em métricas por meio do portal hello, ou pode ser configuradas [programaticamente](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sobre dados de Logs de operação.</span><span class="sxs-lookup"><span data-stu-id="8a084-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="8a084-109">Configurar alertas em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8a084-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="8a084-110">No Olá portal do Azure, abra o trabalho do Stream Analytics Olá para que deseja toocreate um alerta.</span><span class="sxs-lookup"><span data-stu-id="8a084-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="8a084-111">Em Olá **trabalho** folha, clique em Olá **monitoramento** seção.</span><span class="sxs-lookup"><span data-stu-id="8a084-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="8a084-112">Em Olá **métrica** folha, clique em Olá **adicionar alerta** comando.</span><span class="sxs-lookup"><span data-stu-id="8a084-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Configuração do portal do Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="8a084-114">Insira um nome e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="8a084-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="8a084-115">Use Olá seletores toodefine Olá condição sob a qual Olá alerta será enviado.</span><span class="sxs-lookup"><span data-stu-id="8a084-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="8a084-116">Fornece informações sobre onde o alerta Olá deve ir.</span><span class="sxs-lookup"><span data-stu-id="8a084-116">Provide information about where hello alert should go.</span></span>

      ![Configurar um alerta para um trabalho do Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="8a084-118">Para obter mais detalhes sobre como configurar alertas em Olá portal do Azure, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="8a084-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="8a084-119">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="8a084-119">Get help</span></span>
<span data-ttu-id="8a084-120">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="8a084-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a084-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a084-121">Next steps</span></span>
* [<span data-ttu-id="8a084-122">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8a084-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8a084-123">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="8a084-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="8a084-124">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="8a084-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8a084-125">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="8a084-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8a084-126">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8a084-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

