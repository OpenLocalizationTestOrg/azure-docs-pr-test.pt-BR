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
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="98fa6-103">Criar um grupo de ações com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98fa6-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="98fa6-104">Este artigo mostra como toouse uma [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupos de ação.</span><span class="sxs-lookup"><span data-stu-id="98fa6-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="98fa6-105">Usando modelos, você pode configurar automaticamente os grupos de ações que podem ser reutilizados em determinados tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="98fa6-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="98fa6-106">Esses grupos de ação Certifique-se de que todos os Olá correto partes são notificadas quando um alerta é disparado.</span><span class="sxs-lookup"><span data-stu-id="98fa6-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="98fa6-107">etapas básicas de saudação são:</span><span class="sxs-lookup"><span data-stu-id="98fa6-107">hello basic steps are:</span></span>

1. <span data-ttu-id="98fa6-108">Crie um modelo como um arquivo JSON que descreve como toocreate Olá grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="98fa6-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="98fa6-109">Implantar o modelo de saudação usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="98fa6-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="98fa6-110">Primeiro, descreveremos como um modelo do Gerenciador de recursos para uma ação de toocreate grupo onde as definições de ação de saudação são embutidos em código no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fa6-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="98fa6-111">Em seguida, descreveremos como toocreate um modelo que usa as informações de configuração de webhook hello como parâmetros de entrada quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="98fa6-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="98fa6-112">Modelos do Resource Manager para um grupo de ações</span><span class="sxs-lookup"><span data-stu-id="98fa6-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="98fa6-113">toocreate um grupo de ação usando um modelo do Gerenciador de recursos, você cria um recurso do tipo hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="98fa6-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="98fa6-114">Em seguida, você preencherá todas as propriedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="98fa6-114">Then you fill in all related properties.</span></span> <span data-ttu-id="98fa6-115">Aqui estão dois modelos de exemplo que criam um grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="98fa6-115">Here are two sample templates that create an action group.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="98fa6-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98fa6-116">Next steps</span></span>
* <span data-ttu-id="98fa6-117">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="98fa6-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="98fa6-118">Saiba mais sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="98fa6-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="98fa6-119">Saiba como tooadd [alertas usando um modelo do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="98fa6-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
