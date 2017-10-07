---
title: "webhooks aaaConfigure em alertas de métrica do Azure | Microsoft Docs"
description: "Redirecionar sistemas de não Azure tooother alertas do Azure."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configurar um webhook em um alerta do métrica do Azure
Webhooks permitir tooroute um Azure alerta sistemas de notificação de tooother para ações de pós-processamento ou personalizados. Você pode usar um webhook em um alerta tooroute-tooservices que enviar SMS, bugs de log, notificar uma equipe por meio de serviços de chat/mensagens ou fazer várias outras ações. Este artigo descreve como tooset um webhook em um alerta de métrica do Azure e quais carga Olá Olá HTTP POST tooa webhook é semelhante. Para obter informações sobre a instalação de saudação e esquema de um alerta de Log de atividades do Azure (alerta em eventos), [consulte esta página em vez disso,](insights-auditlog-to-webhook-email.md).

Azure alertas conteúdo do alerta Olá HTTP POST no formato JSON, o esquema definido abaixo, tooa webhook URI que você fornece durante a criação de alerta de saudação. O URI deve ser um ponto de extremidade HTTP ou HTTPS válido. O Azure posta uma entrada por solicitação quando um alerta é ativado.

## <a name="configuring-webhooks-via-hello-portal"></a>Como configurar webhooks por meio do portal de saudação
Você pode adicionar ou atualizar Olá webhook URI na tela de alertas de Create/Update Olá Olá [portal](https://portal.azure.com/).

![Adicionar uma Regra de alerta](./media/insights-webhooks-alerts/Alertwebhook.png)

Você também pode configurar um webhook de tooa toopost alerta URI usando Olá [Cmdlets do PowerShell do Azure](insights-powershell-samples.md#create-metric-alerts), [CLI de plataforma cruzada](insights-cli-samples.md#work-with-alerts), ou [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Autenticando Olá webhook
Olá webhook pode autenticar usando a autorização baseada em token. Olá webhook URI é salvo com uma ID do token, por exemplo. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Esquema de conteúdo
Olá operação POST contém Olá carga JSON e o esquema para todas as métrica de alertas a seguir.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Campo | Obrigatório | Conjunto fixo de valores | Observações |
|:--- |:--- |:--- |:--- |
| status |S |“Activated”, “Resolved” |Status de saudação de alerta com base nas condições de saudação você definiu. |
| context |S | |contexto de alerta de saudação. |
| timestamp |S | |tempo de saudação no qual Olá alerta foi disparado. |
| ID |S | |Cada regra de alerta tem uma ID exclusiva. |
| name |S | |nome do alerta Hello. |
| description |S | |Descrição do alerta de saudação. |
| conditionType |S |“Metric”, “Event” |Há suporte para dois tipos de alertas. Um com base em uma condição de métrica e hello outros com base em um evento em Olá Log de atividades. Use toocheck esse valor se o alerta Olá baseia-se na métrica ou evento. |
| condition |S | |Olá toocheck campos específicos para com base em conditionType hello. |
| metricName |para alertas de Métrica | |nome Hello da métrica de saudação que define quais regra Olá monitora. |
| metricUnit |para alertas de Métrica |"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percent", "Seconds" |unidade de saudação permitida na métrica hello. [Os valores permitidos estão listados aqui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |para alertas de Métrica | |valor real de saudação da métrica Olá que causou o alerta de saudação. |
| threshold |para alertas de Métrica | |valor de limite de saudação no qual Olá alerta for ativado. |
| windowSize |para alertas de Métrica | |Olá período de tempo que é usado toomonitor atividade de alerta com base no limite de saudação. Deve estar entre 5 minutos e 1 dia. Formato de duração ISO 8601. |
| timeAggregation |para alertas de Métrica |"Average", "Last", "Maximum", "Minimum", "None", "Total" |Como os dados de saudação que são coletados devem ser combinados ao longo do tempo. valor padrão de saudação é média. [Os valores permitidos estão listados aqui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |para alertas de Métrica | |operador de saudação usado toocompare Olá atual dados da métrica toohello limite definido. |
| subscriptionId |S | |Id de assinatura do Azure. |
| resourceGroupName |S | |Nome do grupo de recursos de saudação para Olá afetados recursos. |
| resourceName |S | |Nome do recurso de saudação afetados recursos. |
| resourceType |S | |Tipo de recurso de saudação afetados recursos. |
| resourceId |S | |ID do recurso da saudação afetados recursos. |
| resourceRegion |S | |Região ou o local da saudação afetados recursos. |
| portalLink |S | |Página Resumo do recurso do portal do toohello de vínculo direto. |
| propriedades |N |Opcional |Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento hello. Olá propriedades campo é opcional. Em um interface do usuário ou lógica com base no aplicativo fluxo de trabalho personalizado, os usuários podem inserir chave/valores que podem ser transmitidos por meio de carga hello. Olá maneira alternativa toopass propriedades personalizadas back toohello webhook é por meio do uri de webhook de saudação em si (como parâmetros de consulta) |

> [!NOTE]
> campo de propriedades Olá só pode ser definido usando Olá [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre alertas do Azure e webhooks vídeo Olá [integrar o Azure alertas com PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Exemplos de scripts da Automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Use o aplicativo lógico toosend um SMS por meio do Twilio em um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Use o aplicativo lógico toosend uma mensagem de margem de atraso de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Use o aplicativo lógico toosend tooan uma mensagem fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
