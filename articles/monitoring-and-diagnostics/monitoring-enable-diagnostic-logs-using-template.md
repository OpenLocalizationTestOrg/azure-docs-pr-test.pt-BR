---
title: "Habilitar automaticamente as Configurações de Diagnóstico usando um modelo do Resource Manager | Microsoft Docs"
description: "Saiba como usar um modelo do Resource Manager para criar configurações de diagnóstico que ajudarão a transmitir seus logs de diagnóstico para os Hubs de Eventos ou armazená-los em uma conta de armazenamento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="ea1b4-103">Habilitar automaticamente as Configurações de Diagnóstico na criação do recurso usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ea1b4-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="ea1b4-104">Neste artigo, mostramos como você pode usar um [Modelo do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para definir as Configurações de Diagnóstico em um recurso quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="ea1b4-105">Isso permite iniciar automaticamente o streaming de seus Logs de Diagnóstico e métricas para os Hubs de Eventos, arquivando-os em uma Conta de Armazenamento ou enviando-os para o Log Analytics quando um recurso é criado.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="ea1b4-106">O método para habilitar os Logs de Diagnóstico usando um modelo do Resource Manager depende do tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="ea1b4-107">**Não Computação** (por exemplo, Grupos de Segurança de Rede, Aplicativos Lógicos, Automação) usam as [Configurações de Diagnóstico descritas neste artigo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="ea1b4-108">**De Computação** (baseados no WAD/LAD) usam o [Arquivo de configuração do WAD/LAD descrito neste artigo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="ea1b4-109">Neste artigo, descrevemos como configurar o diagnóstico usando um método.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="ea1b4-110">Estas são as etapas básicas:</span><span class="sxs-lookup"><span data-stu-id="ea1b4-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="ea1b4-111">Crie um modelo como um arquivo JSON que descreve como criar o recurso e habilite o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="ea1b4-112">[Implantar o modelo usando qualquer método de implantação](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="ea1b4-113">Abaixo, damos um exemplo de arquivo JSON do modelo que você precisa gerar para os recursos de Computação e de Não Computação.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="ea1b4-114">Modelo de recursos de Não Computação</span><span class="sxs-lookup"><span data-stu-id="ea1b4-114">Non-Compute resource template</span></span>
<span data-ttu-id="ea1b4-115">Para os recursos de Não Computação, você precisará fazer duas coisas:</span><span class="sxs-lookup"><span data-stu-id="ea1b4-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="ea1b4-116">Adicione parâmetros ao blob de parâmetros para o nome da conta de armazenamento, ID de regra do barramento de serviço e/ou ID do espaço de trabalho do Log Analytics do OMS (permitindo o arquivamento dos Logs de Diagnóstico em uma conta de armazenamento, streaming de logs para os Hubs de Eventos e/ou envio de logs para o Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="ea1b4-117">Na matriz de recursos do recurso para o qual você deseja habilitar os Logs de Diagnóstico, adicione um recurso do tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="ea1b4-118">O blob de propriedades da Configuração de Diagnóstico segue [o formato descrito neste artigo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="ea1b4-119">A adição da propriedade `metrics` permitirá também o envio de métricas de recurso para essas mesmas saídas, desde que [o recurso ofereça suporte para as métricas do Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="ea1b4-120">Aqui temos um exemplo completo que cria um aplicativo lógico e ativa o streaming para Hubs de eventos e o armazenamento em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="ea1b4-121">Modelo de recursos de computação</span><span class="sxs-lookup"><span data-stu-id="ea1b4-121">Compute resource template</span></span>
<span data-ttu-id="ea1b4-122">Para habilitar o diagnóstico em um recurso de Computação, por exemplo uma Máquina Virtual ou cluster do Service Fabric, você precisa:</span><span class="sxs-lookup"><span data-stu-id="ea1b4-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="ea1b4-123">Adicionar a extensão de Diagnóstico do Azure à definição do recurso da VM.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="ea1b4-124">Especificar uma conta de armazenamento e/ou hub de eventos como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="ea1b4-125">Adicionar o conteúdo do arquivo XML WADCfg na propriedade XMLCfg, substituindo todos os caracteres XML corretamente.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="ea1b4-126">Esta última etapa pode ser difícil de fazer.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="ea1b4-127">[Confira este artigo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obter um exemplo que divide o Esquema de Configuração de Diagnóstico em variáveis que são substituídas e formatadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="ea1b4-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="ea1b4-128">O processo inteiro, incluindo os exemplos, é descrito [neste documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea1b4-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea1b4-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea1b4-129">Next Steps</span></span>
* [<span data-ttu-id="ea1b4-130">Saiba mais sobre os Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ea1b4-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="ea1b4-131">Transmitir Logs de Diagnóstico do Azure para os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ea1b4-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

