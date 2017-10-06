---
title: aaaMigrate Azure alertas em eventos de gerenciamento tooActivity alertas de Log | Microsoft Docs
description: "Os alertas em eventos de gerenciamento serão removidos em 1º de outubro. Prepare-se migrando os alertas de migração existentes."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Migrar do Azure alertas em alertas de Log de eventos tooActivity de gerenciamento


> [!WARNING]
> Os alertas em eventos de gerenciamento serão desativados a partir do dia 1º de outubro. Use instruções Olá abaixo toounderstand se você tiver esses alertas e migrá-los nesse caso.
>
> 

## <a name="what-is-changing"></a>O que está mudando

Monitor do Azure (anteriormente Azure Insights) oferecidos toocreate um recurso um alerta acionado de eventos de gerenciamento e gerado notificações tooa endereços de email ou URL do webhook. Você pode ter criado um desses alertas usando uma das seguintes maneiras:
* Olá portal do Azure para certos tipos de recursos, em monitoramento -> alertas -> Adicionar alerta, onde "Alerta de" está definida muito "Eventos"
* Cmdlet de PowerShell Add-AzureRmLogAlertRule Olá em execução
* Usando diretamente [Olá API REST do alerta](http://docs.microsoft.com/rest/api/monitor/alertrules) com OData. Type = "ManagementEventRuleCondition" e dataSource.odata.type = "RuleManagementEventDataSource"
 
Olá script PowerShell a seguir retorna uma lista de todos os alertas em eventos de gerenciamento que você tem em sua assinatura, bem como as condições de saudação definidas em cada alerta.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

Se você não tem alertas em eventos de gerenciamento, o cmdlet do PowerShell Olá acima produzirá uma série de mensagens de aviso como esta:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Essas mensagens de aviso podem ser ignoradas. Se você tem alertas em eventos de gerenciamento, Olá saída deste cmdlet do PowerShell será assim:

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Cada alerta é separada por uma linha tracejada e detalhes incluem a ID de recurso de saudação do alerta hello e regras específicas de hello está sendo monitorado.

Essa funcionalidade passou por transição muito[alertas de Log de atividade do Monitor](monitoring-activity-log-alerts.md). Esses novos alertas permitem que você tooset uma condição em eventos de Log de atividades e recebem uma notificação quando um novo evento corresponde a condição de saudação. Eles também oferecem vários aprimoramentos de alertas sobre eventos de gerenciamento:
* Você pode reutilizar o grupo de destinatários de notificação ("ações") em vários alertas usando [grupos de ação](monitoring-action-groups.md), reduzindo a complexidade de saudação da alteração que deve receber um alerta.
* Você poderá receber uma notificação diretamente em seu telefone usando SMS com Grupos de Ação.
* Você pode [criar alertas do Log de Atividades com modelos do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Você pode criar condições com maior toomeet flexibilidade e a complexidade suas necessidades específicas.
* As notificações são entregues mais rapidamente.
 
## <a name="how-toomigrate"></a>Como toomigrate
 
toocreate um novo alerta de atividade de Log, você pode:
* Execute [nosso guia em como toocreate um alerta no hello portal do Azure](monitoring-activity-log-alerts.md)
* Saiba como muito[criar um alerta usando um modelo do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Alertas em eventos de gerenciamento que você criou anteriormente não serão automaticamente migrado tooActivity Log de alertas. É necessário toouse Olá anterior alertas de saudação do PowerShell script toolist em eventos de gerenciamento que você configurou atualmente e recriá-los manualmente como alertas de Log de atividade. Isso deve ser feito antes de 1º de outubro, pois após essa data os alertas em eventos de gerenciamento não serão mais visíveis em sua assinatura do Azure. Outros tipos de alertas do Azure, incluindo alertas de métrica do Azure Monitor, alertas do Application Insights e alertas do Log Analytics não são afetados por essa alteração. Se você tiver dúvidas, poste nos comentários de saudação abaixo.


## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre o [Log de Atividades](monitoring-overview-activity-logs.md)
* Configurar [alertas do Log de Atividades por meio do Portal do Azure](monitoring-activity-log-alerts.md)
* Configurar [alertas do Log de Atividades por meio do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Saudação de revisão [esquema webhook alerta do log de atividade](monitoring-activity-log-alerts-webhook.md)
* Saiba mais sobre as [Notificações de Serviço](monitoring-service-notifications.md)
* Saiba mais sobre [Grupos de Ação](monitoring-action-groups.md)
