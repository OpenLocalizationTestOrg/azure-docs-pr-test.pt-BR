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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Habilitar automaticamente as Configurações de Diagnóstico na criação do recurso usando um modelo do Resource Manager
Neste artigo, vamos mostrar como você pode usar um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure configurações de diagnóstico em um recurso quando ele é criado. Isso permite que você tooautomatically iniciar streaming seu Logs de diagnóstico e métricas tooEvent Hubs, arquivá-los em uma conta de armazenamento ou enviá-los tooLog análise quando um recurso é criado.

método Hello para habilitar Logs de diagnóstico usando um modelo do Gerenciador de recursos depende do tipo de recurso de saudação.

* **Não Computação** (por exemplo, Grupos de Segurança de Rede, Aplicativos Lógicos, Automação) usam as [Configurações de Diagnóstico descritas neste artigo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Computação** (WAD/LAD base) recursos usam Olá [arquivo de configuração do WAD/LAD descrito neste artigo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

Neste artigo, descreveremos como tooconfigure diagnóstico usando um método.

etapas básicas de saudação são da seguinte maneira:

1. Crie um modelo como um arquivo JSON que descreve como toocreate Olá recursos e habilitar o diagnóstico.
2. [Implante o modelo hello usando qualquer método de implantação](../azure-resource-manager/resource-group-template-deploy.md).

A seguir, fornecemos um exemplo de modelo Olá arquivo JSON necessário toogenerate de não-computação e recursos de computação.

## <a name="non-compute-resource-template"></a>Modelo de recursos de Não Computação
Para recursos de computação não, você precisará toodo duas coisas:

1. Adicione o blob de parâmetros de toohello de parâmetros para o nome de conta de armazenamento hello, ID de regra de barramento de serviço e/ou ID do espaço de trabalho de análise de logs do OMS (Habilitar arquivamento de Logs de diagnóstico em uma conta de armazenamento, fluxo de logs tooEvent Hubs e/ou envio de logs tooLog análise).
   
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
2. Na matriz de recursos de saudação do recurso de saudação do qual você deseja que os Logs de diagnóstico tooenable, adicionar um recurso do tipo `[resource namespace]/providers/diagnosticSettings`.
   
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

Olá blob de propriedades para configuração de diagnóstico de saudação segue [formato Olá descrito neste artigo](https://msdn.microsoft.com/library/azure/dn931931.aspx). Olá adicionando `metrics` propriedade permitirá que você mesmo saídas, contanto que toothese de métricas tooalso envio recurso [métricas do Monitor do Azure oferece suporte a recursos de saudação](monitoring-supported-metrics.md).

Aqui está um exemplo completo que cria um aplicativo lógico e ativa streaming tooEvent Hubs e armazenamento em uma conta de armazenamento.

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

## <a name="compute-resource-template"></a>Modelo de recursos de computação
Diagnóstico de tooenable em um recurso de computação, por exemplo, uma máquina Virtual ou cluster do Service Fabric, você precisa:

1. Adicione definição de recurso VM extensão toohello do hello diagnóstico do Azure.
2. Especificar uma conta de armazenamento e/ou hub de eventos como um parâmetro.
3. Adicione conteúdo de saudação do arquivo WADCfg XML na propriedade de XMLCfg hello, ignorando todos os caracteres XML corretamente.

> [!WARNING]
> Nesta última etapa pode ser difícil tooget direita. [Consulte este artigo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obter um exemplo que divisões Olá esquema de configuração de diagnóstico em variáveis são ignoradas e formatados corretamente.
> 
> 

Olá todo o processo, incluindo exemplos, é descrito [neste documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os Logs de Diagnóstico do Azure](monitoring-overview-of-diagnostic-logs.md)
* [Fluxo de Logs de diagnóstico do Azure tooEvent Hubs](monitoring-stream-diagnostic-logs-to-event-hubs.md)

