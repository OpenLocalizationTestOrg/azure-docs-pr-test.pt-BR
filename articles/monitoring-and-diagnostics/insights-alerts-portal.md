---
title: "alertas de aaaCreate para serviços do Azure - portal do Azure | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Criar alertas de métrica no Azure Monitor para serviços do Azure – Portal do Azure
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Visão geral
Este artigo mostra como tooset alertas de métrica do Azure usando Olá portal do Azure.   

Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.

* **Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção. Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.    
* **Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem. mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)

Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:

* enviar o administrador do serviço de toohello de notificações de email e coadministradores
* Envie email tooadditional emails que você especificar.
* chamar um webhook
* Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure)

Você pode configurar e obter informações sobre regras de alerta de métrica usando

* [Portal do Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [CLI (Interface de linha de comando)](insights-alerts-command-line-interface.md)
* [API REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Criar uma regra de alerta em uma métrica com hello portal do Azure
1. Em Olá [portal](https://portal.azure.com/), localize o recurso Olá você está interessado no monitoramento e selecioná-lo.

2. Selecione **alertas** ou **regras de alerta** em Olá seção monitoramento. ícone e o texto de saudação podem variar um pouco para recursos diferentes.  

    ![Monitoramento](./media/insights-alerts-portal/AlertRulesButton.png)

3. Selecione Olá **adicionar alerta** de comando e preencha os campos de saudação.

    ![Adicionar alerta](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. Dê um **Nome** para o alerta de regra e escolha uma **Descrição**, que também mostre os emails de notificação.

5. Selecione Olá **métrica** você deseja toomonitor, em seguida, escolha um **condição** e **limite** valor de métrica de saudação. Também tiver escolhido Olá **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação. Por exemplo, se você usar o período de hello "PT5M" e a alerta de procura da CPU acima de 80%, alerta Olá dispara quando Olá CPU foi consistentemente acima de 80% por 5 minutos. Depois que o primeiro gatilho de saudação ocorre, ele novamente dispara quando Olá da CPU permanece abaixo de 80% de 5 minutos. Olá medida de CPU ocorre a cada 1 minuto.   

6. Verificar **proprietários de Email...**  se você quiser que os administradores e coadministradores toobe enviado por email quando Olá alerta acionado.

7. Se você quiser emails adicionais tooreceive notificação hello quando o alerta é acionado, adicioná-los em Olá **email(s) administrador adicional** campo. Vários emails separados com ponto e vírgula – *email@contoso.com;email2@contoso.com*

8. Colocar em um URI válido no hello **Webhook** campo se você quiser chamada hello alerta acionado quando.

9. Se você usar a automação do Azure, você pode selecionar um toobe Runbook executado quando Olá alerta será acionado.

10. Selecione **Okey** quando concluído toocreate Olá alerta.   

Em poucos minutos, o alerta de hello está ativa e dispara conforme descrito anteriormente.

## <a name="managing-your-alerts"></a>Gerenciar seus alertas
Depois de criar um alerta, você poderá selecioná-lo e:

* Exiba um gráfico que mostra o limite de métrica hello e os valores reais de Olá Olá dia anterior.
* Editar ou exclui-lo.
* **Desabilitar** ou **habilitar** se deseja tootemporarily parar ou continuar recebendo notificações para o alerta.

## <a name="next-steps"></a>Próximas etapas
* [Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.
* Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).
* Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).
* Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).
* Tenha uma [visão geral dos logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) e colete métricas detalhadas de alta frequência em seu serviço.
* Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
