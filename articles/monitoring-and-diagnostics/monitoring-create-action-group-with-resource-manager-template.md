---
title: "Criar grupos de ações com modelos do Resource Manager | Microsoft Docs"
description: "Saiba como criar um grupo de ações usando um modelo do Azure Resource Manager."
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
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="d29d7-103">Criar um grupo de ações com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d29d7-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="d29d7-104">Este artigo mostra como você pode usar um [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) para configurar grupos de ações.</span><span class="sxs-lookup"><span data-stu-id="d29d7-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="d29d7-105">Usando modelos, você pode configurar automaticamente os grupos de ações que podem ser reutilizados em determinados tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="d29d7-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="d29d7-106">Esses grupos de ações garantem que todas as partes corretas serão notificadas quando um alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="d29d7-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="d29d7-107">As etapas básicas são:</span><span class="sxs-lookup"><span data-stu-id="d29d7-107">The basic steps are:</span></span>

1. <span data-ttu-id="d29d7-108">Crie um modelo como um arquivo JSON que descreve como criar o grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="d29d7-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="d29d7-109">Implantar o modelo usando [qualquer método de implantação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="d29d7-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="d29d7-110">Primeiro, descreveremos como criar um modelo do Resource Manager para um grupo em que as definições de ação são codificadas no modelo.</span><span class="sxs-lookup"><span data-stu-id="d29d7-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="d29d7-111">Em seguida, descreveremos como criar um modelo que usa as informações de configuração de webhook como parâmetros de entrada quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="d29d7-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="d29d7-112">Modelos do Resource Manager para um grupo de ações</span><span class="sxs-lookup"><span data-stu-id="d29d7-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="d29d7-113">Para criar um grupo de ações usando um modelo do Resource Manager, você cria um recurso do tipo `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="d29d7-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="d29d7-114">Em seguida, você preencherá todas as propriedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="d29d7-114">Then you fill in all related properties.</span></span> <span data-ttu-id="d29d7-115">Aqui estão dois modelos de exemplo que criam um grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="d29d7-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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


## <a name="next-steps"></a><span data-ttu-id="d29d7-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d29d7-116">Next steps</span></span>
* <span data-ttu-id="d29d7-117">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="d29d7-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="d29d7-118">Saiba mais sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d29d7-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="d29d7-119">Saiba como adicionar [Alertas usando um modelo do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d29d7-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
