---
title: "aaaAutomatically Habilitar configurações de diagnóstico usando um modelo do Gerenciador de recursos | Microsoft Docs"
description: "Saiba como toouse um Gerenciador de recursos de modelo toocreate configurações de diagnóstico que permitirão que você toostream o diagnóstico logs tooEvent Hubs ou armazená-las em uma conta de armazenamento."
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="71144-103">Habilitar automaticamente as Configurações de Diagnóstico na criação do recurso usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71144-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="71144-104">Neste artigo, vamos mostrar como você pode usar um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure configurações de diagnóstico em um recurso quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="71144-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="71144-105">Isso permite que você tooautomatically iniciar streaming seu Logs de diagnóstico e métricas tooEvent Hubs, arquivá-los em uma conta de armazenamento ou enviá-los tooLog análise quando um recurso é criado.</span><span class="sxs-lookup"><span data-stu-id="71144-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="71144-106">método Hello para habilitar Logs de diagnóstico usando um modelo do Gerenciador de recursos depende do tipo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="71144-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="71144-107">**Não Computação** (por exemplo, Grupos de Segurança de Rede, Aplicativos Lógicos, Automação) usam as [Configurações de Diagnóstico descritas neste artigo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="71144-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="71144-108">**Computação** (WAD/LAD base) recursos usam Olá [arquivo de configuração do WAD/LAD descrito neste artigo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="71144-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="71144-109">Neste artigo, descreveremos como tooconfigure diagnóstico usando um método.</span><span class="sxs-lookup"><span data-stu-id="71144-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="71144-110">etapas básicas de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="71144-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="71144-111">Crie um modelo como um arquivo JSON que descreve como toocreate Olá recursos e habilitar o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="71144-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="71144-112">[Implante o modelo hello usando qualquer método de implantação](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="71144-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="71144-113">A seguir, fornecemos um exemplo de modelo Olá arquivo JSON necessário toogenerate de não-computação e recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="71144-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="71144-114">Modelo de recursos de Não Computação</span><span class="sxs-lookup"><span data-stu-id="71144-114">Non-Compute resource template</span></span>
<span data-ttu-id="71144-115">Para recursos de computação não, você precisará toodo duas coisas:</span><span class="sxs-lookup"><span data-stu-id="71144-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="71144-116">Adicione o blob de parâmetros de toohello de parâmetros para o nome de conta de armazenamento hello, ID de regra de barramento de serviço e/ou ID do espaço de trabalho de análise de logs do OMS (Habilitar arquivamento de Logs de diagnóstico em uma conta de armazenamento, fluxo de logs tooEvent Hubs e/ou envio de logs tooLog análise).</span><span class="sxs-lookup"><span data-stu-id="71144-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="71144-117">Na matriz de recursos de saudação do recurso de saudação do qual você deseja que os Logs de diagnóstico tooenable, adicionar um recurso do tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="71144-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="71144-118">Olá blob de propriedades para configuração de diagnóstico de saudação segue [formato Olá descrito neste artigo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="71144-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="71144-119">Olá adicionando `metrics` propriedade permitirá que você mesmo saídas, contanto que toothese de métricas tooalso envio recurso [métricas do Monitor do Azure oferece suporte a recursos de saudação](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="71144-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="71144-120">Aqui está um exemplo completo que cria um aplicativo lógico e ativa streaming tooEvent Hubs e armazenamento em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="71144-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="71144-121">Modelo de recursos de computação</span><span class="sxs-lookup"><span data-stu-id="71144-121">Compute resource template</span></span>
<span data-ttu-id="71144-122">Diagnóstico de tooenable em um recurso de computação, por exemplo, uma máquina Virtual ou cluster do Service Fabric, você precisa:</span><span class="sxs-lookup"><span data-stu-id="71144-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="71144-123">Adicione definição de recurso VM extensão toohello do hello diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="71144-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="71144-124">Especificar uma conta de armazenamento e/ou hub de eventos como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="71144-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="71144-125">Adicione conteúdo de saudação do arquivo WADCfg XML na propriedade de XMLCfg hello, ignorando todos os caracteres XML corretamente.</span><span class="sxs-lookup"><span data-stu-id="71144-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="71144-126">Nesta última etapa pode ser difícil tooget direita.</span><span class="sxs-lookup"><span data-stu-id="71144-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="71144-127">[Consulte este artigo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obter um exemplo que divisões Olá esquema de configuração de diagnóstico em variáveis são ignoradas e formatados corretamente.</span><span class="sxs-lookup"><span data-stu-id="71144-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="71144-128">Olá todo o processo, incluindo exemplos, é descrito [neste documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71144-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71144-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71144-129">Next Steps</span></span>
* [<span data-ttu-id="71144-130">Saiba mais sobre os Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="71144-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="71144-131">Fluxo de Logs de diagnóstico do Azure tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="71144-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

