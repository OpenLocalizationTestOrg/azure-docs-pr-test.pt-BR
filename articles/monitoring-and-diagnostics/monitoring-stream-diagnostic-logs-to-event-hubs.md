---
title: "Logs de diagnóstico do Azure de aaaStream tooan Namespace de Hubs de evento | Microsoft Docs"
description: "Saiba como toostream diagnóstico do Azure registra tooan namespace de Hubs de eventos."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Fluxo de Logs de diagnóstico do Azure tooan Namespace de Hubs de evento
**[Logs de diagnósticos do Azure](monitoring-overview-of-diagnostic-logs.md)**  pode ser transmitida em quase em tempo real tooany aplicativo usando a opção hello "Exportar tooEvent Hubs" incorporada no Portal de saudação ou habilitando Olá ID de regra de barramento de serviço em uma configuração de diagnóstica por meio de saudação do PowerShell do Azure CLI cmdlets ou do Azure.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>O que você pode fazer com os logs de diagnóstico e os Hubs de Eventos
Aqui estão algumas maneiras que você pode usar o hello capacidade para streaming para Logs de diagnóstico:

* **Fluxo de logs de sistemas de registro em log e telemetria de too3rd** – ao longo do tempo, streaming de Hubs de eventos se tornará Olá mecanismo toopipe os logs de diagnóstico na parte toothird SIEMs e soluções de análise de log.
* **Exibir a integridade do serviço por streaming "afunilamento" dados tooPowerBI** – usando Hubs de eventos, análise de fluxo e Power BI, você pode facilmente transformar os dados de diagnóstico em informações em tempo real toonear em seus serviços do Azure. [Este artigo de documentação fornece uma visão de geral grande como tooset a Hubs de eventos, processar dados com a análise de fluxo e usar o Power BI como uma saída](../stream-analytics/stream-analytics-power-bi-dashboard.md). Aqui estão algumas dicas para configurá-lo com os logs de diagnóstico:
  
  * Um hub de eventos para uma categoria de logs de diagnóstico é criado automaticamente quando você marca a opção Olá no portal de saudação ou habilitá-lo por meio do PowerShell, para que você deseja que o hub de eventos tooselect Olá Olá namespace com o nome da saudação que começa com **insights**.
  * Olá código SQL a seguir está um exemplo de análise de fluxo de consulta que você pode usar tooparse todos os dados de log Olá na tabela do Power BI tooa:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Criar uma plataforma de registro em log e telemetria personalizada** – se você já tem uma plataforma de telemetria personalizada ou estão pensando sobre como criar um, Olá altamente escalonável de publicação / assinatura natureza dos Hubs de eventos permite que você tooflexibly ingestão diagnóstico logs. [Consulte toousing de guia de Dan Rosanova Hubs de eventos em uma plataforma de telemetria de escala global aqui](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Habilitar o streaming de logs de diagnóstico
Você pode habilitar o streaming de logs de diagnóstico programaticamente, por meio do portal hello, ou usando Olá [APIs de REST do Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). De qualquer forma, você cria uma configuração de diagnóstica que você especifica um namespace de Hubs de eventos e categorias de log hello e métricas que você deseja toosend no namespace toohello. Um hub de eventos é criado no namespace Olá para cada categoria de log que você habilitar. Uma **categoria de log** de diagnóstico é um tipo de log que um recurso pode coletar.

> [!WARNING]
> A habilitação e streaming de logs de diagnóstico dos recursos de computação (por exemplo, VMs ou Service Fabric) [exige um conjunto diferente de etapas](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Olá barramento de serviço ou Hubs de evento namespace não tem toobe em Olá mesma assinatura que o recurso Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Logs de diagnóstico de fluxo usando o portal de saudação
1. No portal de hello, navegar tooAzure Monitor e clique em **configurações de diagnóstico**

    ![Seção de monitoramento do Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Se desejar filtrar lista Olá por tipo de recurso ou grupo de recursos, clique no recurso Olá para o qual você gostaria que tooset uma configuração de diagnóstica.

3. Se nenhuma configuração existir no recurso de saudação selecionado, você está toocreate solicitada uma configuração. Clique em “Ativar diagnóstico”.

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Se houver configurações existentes no recurso hello, você verá uma lista de configurações já configurado nesse recurso. Clique em "Adicionar configuração de diagnóstico".

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Dê sua configuração para um nome e marque a caixa de saudação para **hub de eventos do fluxo tooan**, em seguida, selecione um namespace de Hubs de eventos.
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Olá namespace selecionado será onde o hub de eventos de saudação é criado (se esta for a primeira vez em que os logs de diagnósticos de streaming) ou transmitido muito (se já houver recursos que são de streaming log categoria toothis namespace), e política de saudação define Olá permissões de mecanismo de fluxo de saudação. Atualmente, o hub de eventos streaming tooan requer permissões de escuta, envio e gerenciar. Você pode criar ou modificar políticas de acesso compartilhado de namespace Hubs de eventos no portal de saudação na guia Configurar de saudação para seu namespace. tooupdate uma destas configurações de diagnósticas, o cliente Olá deve ter permissão de ListKey de Olá na regra de autorização de Hubs de eventos de saudação.

4. Clique em **Salvar**.

Após alguns instantes, nova configuração de saudação aparece na lista de configurações para esse recurso e logs de diagnóstico são transmitidos a conta de armazenamento toothat assim que novos dados de evento são gerados.

### <a name="via-powershell-cmdlets"></a>Via Cmdlets do PowerShell
tooenable streaming por meio do hello [Cmdlets do PowerShell do Azure](insights-powershell-samples.md), você pode usar o hello `Set-AzureRmDiagnosticSetting` cmdlet com estes parâmetros:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`, por exemplo, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Via CLI do Azure
tooenable streaming por meio do hello [CLI do Azure](insights-cli-samples.md), você pode usar o hello `insights diagnostic set` comando como este:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Use Olá mesmo formato para ID de regra de barramento de serviço, conforme explicado para Olá Cmdlet do PowerShell.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Como consomem a dados de log de saudação dos Hubs de eventos?
Aqui está um exemplo de dados de saída dos Hubs de Eventos:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Nome do elemento | Descrição |
| --- | --- |
| records |Uma matriz de todos os eventos de log nessa carga. |
| tempo real |Hora em que hello evento ocorreu. |
| categoria |Categoria do log desse evento. |
| resourceId |ID de recurso do recurso de saudação que gerou este evento. |
| operationName |Nome da operação de saudação. |
| level |Opcional. Indica o nível de log de eventos de saudação. |
| propriedades |Propriedades de evento de saudação. |

Você pode exibir uma lista de todos os provedores de recursos que oferecem suporte a streaming Hubs tooEvent [aqui](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Transmitir dados de recursos de Computação
Você também pode transmitir os logs de diagnóstico dos recursos de computação usando o agente de diagnóstico do Windows Azure hello. [Consulte este artigo](../event-hubs/event-hubs-streaming-azure-diags-data.md) como tooset esse backup.

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os Logs de Diagnóstico do Azure](monitoring-overview-of-diagnostic-logs.md)
* [Introdução aos Hubs de Evento](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

