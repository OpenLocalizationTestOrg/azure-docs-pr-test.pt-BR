---
title: Criar um alerta do log de atividades com um modelo do Resource Manager | Microsoft Docs
description: Seja notificado quando seus recursos do Azure forem criados.
author: anirudhcavale
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
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="97cb4-103">Criar um alerta do log de atividades com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97cb4-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="97cb4-104">Este artigo mostra como usar um [modelo do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) para configurar alertas do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="97cb4-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="97cb4-105">Usando modelos, você pode facilmente configurar vários alertas que são ativados com base em condições específicas de evento de log de atividades como parte do processo de implantação automática.</span><span class="sxs-lookup"><span data-stu-id="97cb4-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="97cb4-106">As etapas básicas são:</span><span class="sxs-lookup"><span data-stu-id="97cb4-106">The basic steps are:</span></span>

1. <span data-ttu-id="97cb4-107">Crie um modelo como um arquivo JSON que descreve como criar o alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="97cb4-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="97cb4-108">Implantar o modelo usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="97cb4-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="97cb4-109">Modelo do Resource Manager para um alerta do log de atividades</span><span class="sxs-lookup"><span data-stu-id="97cb4-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="97cb4-110">Para criar um alerta do log de atividades usando um modelo do Resource Manager, você cria um recurso do tipo `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="97cb4-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="97cb4-111">Em seguida, você preencherá todas as propriedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="97cb4-111">Then you fill in all related properties.</span></span> <span data-ttu-id="97cb4-112">Veja abaixo um modelo que cria um alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="97cb4-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

<span data-ttu-id="97cb4-113">Visite nossa [Galeria de Início Rápido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para obter alguns exemplos de modelos de alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="97cb4-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97cb4-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97cb4-114">Next steps</span></span>
- <span data-ttu-id="97cb4-115">Saiba mais sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="97cb4-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="97cb4-116">Saiba como adicionar [grupos de ações usando um modelo do Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="97cb4-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="97cb4-117">Saiba como [criar um alerta do log de atividades para monitorar todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="97cb4-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="97cb4-118">Saiba como [criar um alerta do log de atividades para monitorar todas as operações de escalar horizontalmente/reduzir horizontalmente com falha na sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="97cb4-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
