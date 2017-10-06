---
title: "alertas de aaaCreate para serviços do Azure - PowerShell | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Criar alertas de métrica no Azure Monitor para serviços do Azure – PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Visão geral
Este artigo mostra como tooset a métrica do Azure alertas usando o PowerShell.  

Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.

* **Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção. Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.    
* **Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem. mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)

Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:

* enviar o administrador do serviço de toohello de notificações de email e coadministradores
* Envie email tooadditional emails que você especificar.
* chamar um webhook
* Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure)

Você pode configurar e obter informações sobre o uso de regras de alerta

* [Portal do Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [CLI (Interface de linha de comando)](insights-alerts-command-line-interface.md)
* [API REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Para obter informações adicionais, você pode digitar sempre ```Get-Help``` e, em seguida, Olá comando do PowerShell que você deseja obter ajuda.

## <a name="create-alert-rules-in-powershell"></a>Criar regras de alerta no PowerShell
1. Faça logon em tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Obter uma lista de assinaturas de saudação que estão disponíveis. Verifique se que você está trabalhando com assinatura de saudação à direita. Se não, defina-o à direita de toohello um usando a saída de saudação do `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. as regras existentes em um grupo de recursos, toolist use Olá comando a seguir:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate uma regra, você precisa toohave várias partes importantes de informações pela primeira vez.

  * Olá **ID de recurso** para os recursos de saudação deseja tooset um alerta para
  * Olá **definições de métrica** disponíveis para esse recurso

     Olá unidirecional tooget ID de recurso é toouse Olá portal do Azure. Supondo que o recurso de saudação já foi criada, selecione-o no portal de saudação. Na folha da próxima hello, selecione *propriedades* em Olá *configurações* seção. **ID do recurso** é um campo na folha de saudação Avançar. Outra maneira é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com/).

     Um exemplo de ID de Recurso para um aplicativo Web é

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Você pode usar `Get-AzureRmMetricDefinition` tooview lista de saudação de todas as definições de métrica para um recurso específico.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Olá exemplo a seguir gera uma tabela com o nome de métrica de saudação e hello unidade para métrica.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Uma lista completa das opções disponíveis para Get-AzureRmMetricDefinition está disponível executando Get-MetricDefinitions.
5. Olá exemplo configura um alerta a seguir em um recurso de site da web. Olá alerta gatilhos sempre que ele recebe consistentemente qualquer tráfego de 5 minutos e, novamente, quando ele recebe nenhum tráfego de 5 minutos.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook ou enviar email quando dispara um alerta, primeiro crie email hello e/ou webhooks. Criar regra Olá posteriormente com imediatamente Olá - marca de ações e, conforme mostrado no exemplo a seguir de saudação. Você não pode associar o webhook ou emails a regras já criadas usando o PowerShell.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify que os alertas foram criados corretamente examinando regras individuais hello.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Excluir seus alertas. Esses comandos excluem regras Olá criadas anteriormente neste artigo.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Próximas etapas
* [Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.
* Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).
* Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).
* Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).
* Obter um [visão geral de coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência em seu serviço.
* Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
