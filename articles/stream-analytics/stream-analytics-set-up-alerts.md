---
title: Configurar alertas para consultas no Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: 75b1b256eea7295f5a464996e2f34ae301c715fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="63bc7-104">Configurar alertas para trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="63bc7-105">Introdução: Página do monitor</span><span class="sxs-lookup"><span data-stu-id="63bc7-105">Introduction: Monitor page</span></span>
<span data-ttu-id="63bc7-106">Você pode configurar alertas para disparar um alerta quando uma métrica atinge uma condição que você especifica.</span><span class="sxs-lookup"><span data-stu-id="63bc7-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="63bc7-107">Por exemplo, você pode configurar um alerta para uma condição semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="63bc7-107">For example, you might set up an alert for a condition like the following:</span></span>

`If there are zero input events in the last 5 minutes, send email notification to sa-admin@example.com`

<span data-ttu-id="63bc7-108">As regras podem ser configuradas em métricas por meio do portal ou [de modo programático](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) pelos dados dos Logs de Operação.</span><span class="sxs-lookup"><span data-stu-id="63bc7-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-the-azure-portal"></a><span data-ttu-id="63bc7-109">Configurar alertas no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-109">Set up alerts in the Azure portal</span></span>
1. <span data-ttu-id="63bc7-110">No Portal do Azure, abra o trabalho do Stream Analytics para o qual você deseja criar um alerta.</span><span class="sxs-lookup"><span data-stu-id="63bc7-110">In the Azure portal, open the Stream Analytics job you want to create an alert for.</span></span> 

2. <span data-ttu-id="63bc7-111">Na folha **Trabalho**, clique na seção **Monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="63bc7-111">In the **Job** blade, click the **Monitoring** section.</span></span>  

3. <span data-ttu-id="63bc7-112">Na folha **Métrica**, clique no comando **Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="63bc7-112">In the **Metric** blade, click the **Add alert** command.</span></span>

      ![Configuração do portal do Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="63bc7-114">Insira um nome e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="63bc7-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="63bc7-115">Use os seletores para definir a condição sob a qual o alerta será enviado.</span><span class="sxs-lookup"><span data-stu-id="63bc7-115">Use the selectors to define the condition under which the alert will be sent.</span></span>

6. <span data-ttu-id="63bc7-116">Forneça informações sobre qual deve ser o destino do alerta.</span><span class="sxs-lookup"><span data-stu-id="63bc7-116">Provide information about where the alert should go.</span></span>

      ![Configurar um alerta para um trabalho do Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="63bc7-118">Para obter mais detalhes sobre como configurar alertas no portal do Azure, consulte [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="63bc7-118">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="63bc7-119">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="63bc7-119">Get help</span></span>
<span data-ttu-id="63bc7-120">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="63bc7-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="63bc7-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63bc7-121">Next steps</span></span>
* [<span data-ttu-id="63bc7-122">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-122">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="63bc7-123">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="63bc7-124">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="63bc7-125">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="63bc7-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="63bc7-126">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="63bc7-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

