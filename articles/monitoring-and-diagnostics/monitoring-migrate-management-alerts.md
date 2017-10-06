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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="70f36-104">Migrar do Azure alertas em alertas de Log de eventos tooActivity de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="70f36-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="70f36-105">Os alertas em eventos de gerenciamento serão desativados a partir do dia 1º de outubro.</span><span class="sxs-lookup"><span data-stu-id="70f36-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="70f36-106">Use instruções Olá abaixo toounderstand se você tiver esses alertas e migrá-los nesse caso.</span><span class="sxs-lookup"><span data-stu-id="70f36-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="70f36-107">O que está mudando</span><span class="sxs-lookup"><span data-stu-id="70f36-107">What is changing</span></span>

<span data-ttu-id="70f36-108">Monitor do Azure (anteriormente Azure Insights) oferecidos toocreate um recurso um alerta acionado de eventos de gerenciamento e gerado notificações tooa endereços de email ou URL do webhook.</span><span class="sxs-lookup"><span data-stu-id="70f36-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="70f36-109">Você pode ter criado um desses alertas usando uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="70f36-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="70f36-110">Olá portal do Azure para certos tipos de recursos, em monitoramento -> alertas -> Adicionar alerta, onde "Alerta de" está definida muito "Eventos"</span><span class="sxs-lookup"><span data-stu-id="70f36-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="70f36-111">Cmdlet de PowerShell Add-AzureRmLogAlertRule Olá em execução</span><span class="sxs-lookup"><span data-stu-id="70f36-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="70f36-112">Usando diretamente [Olá API REST do alerta](http://docs.microsoft.com/rest/api/monitor/alertrules) com OData. Type = "ManagementEventRuleCondition" e dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="70f36-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="70f36-113">Olá script PowerShell a seguir retorna uma lista de todos os alertas em eventos de gerenciamento que você tem em sua assinatura, bem como as condições de saudação definidas em cada alerta.</span><span class="sxs-lookup"><span data-stu-id="70f36-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="70f36-114">Se você não tem alertas em eventos de gerenciamento, o cmdlet do PowerShell Olá acima produzirá uma série de mensagens de aviso como esta:</span><span class="sxs-lookup"><span data-stu-id="70f36-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="70f36-115">Essas mensagens de aviso podem ser ignoradas.</span><span class="sxs-lookup"><span data-stu-id="70f36-115">These warning messages can be ignored.</span></span> <span data-ttu-id="70f36-116">Se você tem alertas em eventos de gerenciamento, Olá saída deste cmdlet do PowerShell será assim:</span><span class="sxs-lookup"><span data-stu-id="70f36-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="70f36-117">Cada alerta é separada por uma linha tracejada e detalhes incluem a ID de recurso de saudação do alerta hello e regras específicas de hello está sendo monitorado.</span><span class="sxs-lookup"><span data-stu-id="70f36-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="70f36-118">Essa funcionalidade passou por transição muito[alertas de Log de atividade do Monitor](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="70f36-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="70f36-119">Esses novos alertas permitem que você tooset uma condição em eventos de Log de atividades e recebem uma notificação quando um novo evento corresponde a condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="70f36-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="70f36-120">Eles também oferecem vários aprimoramentos de alertas sobre eventos de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="70f36-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="70f36-121">Você pode reutilizar o grupo de destinatários de notificação ("ações") em vários alertas usando [grupos de ação](monitoring-action-groups.md), reduzindo a complexidade de saudação da alteração que deve receber um alerta.</span><span class="sxs-lookup"><span data-stu-id="70f36-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="70f36-122">Você poderá receber uma notificação diretamente em seu telefone usando SMS com Grupos de Ação.</span><span class="sxs-lookup"><span data-stu-id="70f36-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="70f36-123">Você pode [criar alertas do Log de Atividades com modelos do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="70f36-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="70f36-124">Você pode criar condições com maior toomeet flexibilidade e a complexidade suas necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="70f36-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="70f36-125">As notificações são entregues mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="70f36-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="70f36-126">Como toomigrate</span><span class="sxs-lookup"><span data-stu-id="70f36-126">How toomigrate</span></span>
 
<span data-ttu-id="70f36-127">toocreate um novo alerta de atividade de Log, você pode:</span><span class="sxs-lookup"><span data-stu-id="70f36-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="70f36-128">Execute [nosso guia em como toocreate um alerta no hello portal do Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="70f36-129">Saiba como muito[criar um alerta usando um modelo do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="70f36-130">Alertas em eventos de gerenciamento que você criou anteriormente não serão automaticamente migrado tooActivity Log de alertas.</span><span class="sxs-lookup"><span data-stu-id="70f36-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="70f36-131">É necessário toouse Olá anterior alertas de saudação do PowerShell script toolist em eventos de gerenciamento que você configurou atualmente e recriá-los manualmente como alertas de Log de atividade.</span><span class="sxs-lookup"><span data-stu-id="70f36-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="70f36-132">Isso deve ser feito antes de 1º de outubro, pois após essa data os alertas em eventos de gerenciamento não serão mais visíveis em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f36-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="70f36-133">Outros tipos de alertas do Azure, incluindo alertas de métrica do Azure Monitor, alertas do Application Insights e alertas do Log Analytics não são afetados por essa alteração.</span><span class="sxs-lookup"><span data-stu-id="70f36-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="70f36-134">Se você tiver dúvidas, poste nos comentários de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="70f36-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="70f36-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70f36-135">Next steps</span></span>

* <span data-ttu-id="70f36-136">Saiba mais sobre o [Log de Atividades](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="70f36-137">Configurar [alertas do Log de Atividades por meio do Portal do Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="70f36-138">Configurar [alertas do Log de Atividades por meio do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="70f36-139">Saudação de revisão [esquema webhook alerta do log de atividade](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="70f36-140">Saiba mais sobre as [Notificações de Serviço](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="70f36-141">Saiba mais sobre [Grupos de Ação](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="70f36-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
