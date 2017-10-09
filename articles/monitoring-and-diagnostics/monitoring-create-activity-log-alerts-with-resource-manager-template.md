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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Criar um alerta do log de atividades com um modelo do Resource Manager
Este artigo mostra como toouse uma [modelo do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure alertas de log de atividade. Usando modelos, você pode facilmente configurar vários alertas que são ativados com base em condições específicas de evento de log de atividades como parte do processo de implantação automática.

etapas básicas de saudação são:

1. Crie um modelo como um arquivo JSON que descreve como a atividade de saudação toocreate log alerta.

2. Implantar o modelo de saudação usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Modelo do Resource Manager para um alerta do log de atividades
toocreate um alerta do log de atividade usando um modelo do Gerenciador de recursos, você cria um recurso do tipo hello `microsoft.insights/activityLogAlerts`. Em seguida, você preencherá todas as propriedades relacionadas. Veja abaixo um modelo que cria um alerta do log de atividades.

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

Visite nossa [Galeria de Início Rápido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para obter alguns exemplos de modelos de alerta do log de atividades.

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre [alertas](monitoring-overview-alerts.md).
- Saiba como tooadd [grupos de ação usando um modelo do Gerenciador de recursos](monitoring-create-action-group-with-resource-manager-template.md).
- Saiba como muito[criar um toomonitor alerta do log de atividade de todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Saiba como muito[criar um toomonitor alerta do log de atividade de todas as operações de escala-em/expansão de dimensionamento automático com falha em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
