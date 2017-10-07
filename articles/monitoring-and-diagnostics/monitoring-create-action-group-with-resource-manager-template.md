---
title: "grupos de ação de aaaCreate com modelos do Gerenciador de recursos | Microsoft Docs"
description: "Saiba como toocreate uma ação de grupo usando um modelo do Gerenciador de recursos do Azure."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>Criar um grupo de ações com um modelo do Resource Manager
Este artigo mostra como toouse uma [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupos de ação. Usando modelos, você pode configurar automaticamente os grupos de ações que podem ser reutilizados em determinados tipos de alertas. Esses grupos de ação Certifique-se de que todos os Olá correto partes são notificadas quando um alerta é disparado.

etapas básicas de saudação são:

1. Crie um modelo como um arquivo JSON que descreve como toocreate Olá grupo de ações.

2. Implantar o modelo de saudação usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

Primeiro, descreveremos como um modelo do Gerenciador de recursos para uma ação de toocreate grupo onde as definições de ação de saudação são embutidos em código no modelo de saudação. Em seguida, descreveremos como toocreate um modelo que usa as informações de configuração de webhook hello como parâmetros de entrada quando Olá modelo é implantado.

## <a name="resource-manager-templates-for-an-action-group"></a>Modelos do Resource Manager para um grupo de ações

toocreate um grupo de ação usando um modelo do Gerenciador de recursos, você cria um recurso do tipo hello `Microsoft.Insights/actionGroups`. Em seguida, você preencherá todas as propriedades relacionadas. Aqui estão dois modelos de exemplo que criam um grupo de ações.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [grupos de ação](monitoring-action-groups.md).
* Saiba mais sobre [alertas](monitoring-overview-alerts.md).
* Saiba como tooadd [alertas usando um modelo do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
