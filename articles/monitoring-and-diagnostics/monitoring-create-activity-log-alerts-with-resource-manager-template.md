---
title: um alerta de log de atividade com um modelo do Gerenciador de recursos de aaaCreate | Microsoft Docs
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
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="9d202-103">Criar um alerta do log de atividades com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9d202-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="9d202-104">Este artigo mostra como toouse uma [modelo do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure alertas de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="9d202-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="9d202-105">Usando modelos, você pode facilmente configurar vários alertas que são ativados com base em condições específicas de evento de log de atividades como parte do processo de implantação automática.</span><span class="sxs-lookup"><span data-stu-id="9d202-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="9d202-106">etapas básicas de saudação são:</span><span class="sxs-lookup"><span data-stu-id="9d202-106">hello basic steps are:</span></span>

1. <span data-ttu-id="9d202-107">Crie um modelo como um arquivo JSON que descreve como a atividade de saudação toocreate log alerta.</span><span class="sxs-lookup"><span data-stu-id="9d202-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="9d202-108">Implantar o modelo de saudação usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="9d202-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="9d202-109">Modelo do Resource Manager para um alerta do log de atividades</span><span class="sxs-lookup"><span data-stu-id="9d202-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="9d202-110">toocreate um alerta do log de atividade usando um modelo do Gerenciador de recursos, você cria um recurso do tipo hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="9d202-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="9d202-111">Em seguida, você preencherá todas as propriedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="9d202-111">Then you fill in all related properties.</span></span> <span data-ttu-id="9d202-112">Veja abaixo um modelo que cria um alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="9d202-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
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

<span data-ttu-id="9d202-113">Visite nossa [Galeria de Início Rápido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para obter alguns exemplos de modelos de alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="9d202-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d202-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d202-114">Next steps</span></span>
- <span data-ttu-id="9d202-115">Saiba mais sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9d202-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="9d202-116">Saiba como tooadd [grupos de ação usando um modelo do Gerenciador de recursos](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="9d202-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="9d202-117">Saiba como muito[criar um toomonitor alerta do log de atividade de todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="9d202-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="9d202-118">Saiba como muito[criar um toomonitor alerta do log de atividade de todas as operações de escala-em/expansão de dimensionamento automático com falha em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="9d202-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
