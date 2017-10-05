---
title: Migrar alertas sobre eventos de gerenciamento para Alertas do Log de Atividades | Microsoft Docs
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
ms.openlocfilehash: 08a457029d3721f5c38dbcd2d2aab7d09a241d8f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="1fd7e-104">Migrar alertas do Azure em eventos de gerenciamento para alertas do Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="1fd7e-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="1fd7e-105">Os alertas em eventos de gerenciamento serão desativados a partir do dia 1º de outubro.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="1fd7e-106">Use as instruções abaixo para entender se você tem esses alertas e migrá-los em caso positivo.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="1fd7e-107">O que está mudando</span><span class="sxs-lookup"><span data-stu-id="1fd7e-107">What is changing</span></span>

<span data-ttu-id="1fd7e-108">O Azure Monitor (antigo Azure Insights) oferecia a capacidade de criar um alerta que disparava eventos de gerenciamento e gerava notificações para a URL de um webhook ou endereços de email.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="1fd7e-109">Você pode ter criado um desses alertas usando uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="1fd7e-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="1fd7e-110">No Portal do Azure de certos tipos de recursos, em Monitoramento -> Alertas -> Adicionar Alerta, em que "Alertar sobre" está definido como "Eventos"</span><span class="sxs-lookup"><span data-stu-id="1fd7e-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="1fd7e-111">Executando o cmdlet do PowerShell, Add-AzureRmLogAlertRule</span><span class="sxs-lookup"><span data-stu-id="1fd7e-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="1fd7e-112">Usando diretamente a [API REST do alerta](http://docs.microsoft.com/rest/api/monitor/alertrules) com odata.type = “ManagementEventRuleCondition” e dataSource.odata.type = “RuleManagementEventDataSource”</span><span class="sxs-lookup"><span data-stu-id="1fd7e-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="1fd7e-113">O script do PowerShell a seguir retorna uma lista de todos os alertas sobre eventos de gerenciamento em sua assinatura, bem como as condições definidas em cada alerta.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

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

<span data-ttu-id="1fd7e-114">Se você não tiver alertas em eventos de gerenciamento, o cmdlet do PowerShell acima produzirá uma série de mensagens de aviso como esta:</span><span class="sxs-lookup"><span data-stu-id="1fd7e-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="1fd7e-115">Essas mensagens de aviso podem ser ignoradas.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-115">These warning messages can be ignored.</span></span> <span data-ttu-id="1fd7e-116">Se você tiver alertas sobre eventos de gerenciamento, a saída desse cmdlet do PowerShell será esta:</span><span class="sxs-lookup"><span data-stu-id="1fd7e-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="1fd7e-117">Cada alerta é separado por uma linha tracejada, e os detalhes incluem a ID de recurso do alerta e a regra específica que está sendo monitorada.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="1fd7e-118">Essa funcionalidade foi transferida para [Alertas do Log de Atividades do Azure Monitor](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1fd7e-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="1fd7e-119">Esses novos alertas permitem que você defina uma condição em eventos do Log de Atividades e receba uma notificação quando um novo evento corresponder à condição.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="1fd7e-120">Eles também oferecem vários aprimoramentos de alertas sobre eventos de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="1fd7e-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="1fd7e-121">Você pode reutilizar seu grupo de destinatários de notificação ("ações") em vários alertas usando [Grupos de Ação](monitoring-action-groups.md), reduzindo a complexidade que é alterar quem deve receber um alerta.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="1fd7e-122">Você poderá receber uma notificação diretamente em seu telefone usando SMS com Grupos de Ação.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="1fd7e-123">Você pode [criar alertas do Log de Atividades com modelos do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="1fd7e-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="1fd7e-124">Você pode criar condições com maior flexibilidade e complexidade a fim de atender às suas necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="1fd7e-125">As notificações são entregues mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="1fd7e-126">Como migrar</span><span class="sxs-lookup"><span data-stu-id="1fd7e-126">How to migrate</span></span>
 
<span data-ttu-id="1fd7e-127">Para criar um novo Alerta do Log de Atividades, você pode:</span><span class="sxs-lookup"><span data-stu-id="1fd7e-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="1fd7e-128">Seguir [nosso guia sobre como criar um alerta no Portal do Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="1fd7e-129">Saiba como [Criar um alerta usando um modelo do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="1fd7e-130">Os alertas em eventos de gerenciamento que você criou anteriormente não serão migrados automaticamente para os Alertas do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="1fd7e-131">Você precisa usar o script do PowerShell anterior para listar os alertas sobre eventos de gerenciamento configurados atualmente, e recriá-los manualmente como Alertas do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="1fd7e-132">Isso deve ser feito antes de 1º de outubro, pois após essa data os alertas em eventos de gerenciamento não serão mais visíveis em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="1fd7e-133">Outros tipos de alertas do Azure, incluindo alertas de métrica do Azure Monitor, alertas do Application Insights e alertas do Log Analytics não são afetados por essa alteração.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="1fd7e-134">Se você tiver dúvidas, poste nos comentários abaixo.</span><span class="sxs-lookup"><span data-stu-id="1fd7e-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1fd7e-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fd7e-135">Next steps</span></span>

* <span data-ttu-id="1fd7e-136">Saiba mais sobre o [Log de Atividades](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="1fd7e-137">Configurar [alertas do Log de Atividades por meio do Portal do Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="1fd7e-138">Configurar [alertas do Log de Atividades por meio do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="1fd7e-139">Examine o [esquema do webhook de alertas do Log de Atividade](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="1fd7e-140">Saiba mais sobre as [Notificações de Serviço](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="1fd7e-141">Saiba mais sobre [Grupos de Ação](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="1fd7e-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
