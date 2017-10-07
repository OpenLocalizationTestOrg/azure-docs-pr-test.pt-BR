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
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Configurar alertas para trabalhos do Stream Analytics do Azure
## <a name="introduction-monitor-page"></a>Introdução: Página do monitor
Você pode configurar alertas tootrigger um alerta quando uma métrica atinge uma condição que você especificar. Por exemplo, você pode configurar um alerta para uma condição semelhante Olá seguinte:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Regras podem ser definidas em métricas por meio do portal hello, ou pode ser configuradas [programaticamente](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sobre dados de Logs de operação.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Configurar alertas em Olá portal do Azure
1. No Olá portal do Azure, abra o trabalho do Stream Analytics Olá para que deseja toocreate um alerta. 

2. Em Olá **trabalho** folha, clique em Olá **monitoramento** seção.  

3. Em Olá **métrica** folha, clique em Olá **adicionar alerta** comando.

      ![Configuração do portal do Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Insira um nome e uma descrição.

5. Use Olá seletores toodefine Olá condição sob a qual Olá alerta será enviado.

6. Fornece informações sobre onde o alerta Olá deve ir.

      ![Configurar um alerta para um trabalho do Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Para obter mais detalhes sobre como configurar alertas em Olá portal do Azure, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-get-started.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

