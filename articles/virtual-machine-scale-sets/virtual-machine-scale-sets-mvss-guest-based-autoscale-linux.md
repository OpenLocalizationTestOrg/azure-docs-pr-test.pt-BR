---
title: "Usar o dimensionamento automático do Azure com métricas de convidado em um modelo de conjunto de dimensionamento do Linux | Microsoft Docs"
description: "Saiba como tooautoscale usando métricas de convidado em um modelo de conjunto de escala de máquinas virtuais do Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Dimensionamento automático usando métricas de convidado em um modelo de conjunto de dimensionamento do Linux

Há dois tipos de métricas no Azure que são coletadas de VMs e conjuntos de escala: algumas vêm da saudação host VM e outros vêm de convidado Olá VM. Métricas de host não exigem configuração adicional porque eles são coletados pelo host Olá VM, enquanto as métricas de convidado requerem tooinstall Olá [extensão de diagnóstico do Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) ou hello [diagnóstico do Azure Linux extensão](../virtual-machines/linux/diagnostic-extension.md) em Olá VM convidada. Um motivo toouse convidado métricas mais comuns em vez de métricas de host é que as métricas de convidado fornecem uma seleção maior de métricas de métricas de host. Um exemplo disso são as métricas de consumo de memória, que só estão disponíveis por meio de métricas de convidado. métricas de host Olá com suporte são listadas [aqui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e métricas usadas convidado são listadas [aqui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toouse regras de dimensionamento automático com base nas métricas de convidado para conjuntos de escala do Linux.

## <a name="change-hello-template-definition"></a>Alterar a definição de modelo de saudação

Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala de Linux Olá definido com o dimensionamento automático com base no convidado pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:

Primeiro, adicionamos parâmetros para `storageAccountName` e `storageAccountSasToken`. Agente de diagnóstico Olá armazenará dados de métrica em uma [tabela](../cosmos-db/table-storage-how-to-use-dotnet.md) nesta conta de armazenamento. A partir de Olá agente de diagnóstico do Linux versão 3.0, usando uma chave de acesso de armazenamento não é mais suportada. É necessário usar um [Token SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

Em seguida, podemos modificar o conjunto de escala Olá `extensionProfile` tooinclude extensão de diagnóstico de saudação. Nessa configuração, podemos especificar recursos Olá ID de escala Olá definida toocollect métricas de, bem como Olá conta de armazenamento e métricas de saudação do SAS token toouse toostore. Nós também especificar com que frequência as métricas de saudação são agregadas (no caso a cada minuto) e tootrack quais métricas (por este caso memória usada por cento). Para obter informações mais detalhadas sobre essa configuração e métricas diferentes da porcentagem de memória usada, consulte [esta documentação](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Por fim, adicionamos uma `autoscaleSettings` recurso tooconfigure AutoEscala com base nessas métricas. Este recurso tem um `dependsOn` cláusula que faz referência a escala Olá definida tooensure conjunto de escala Olá existe antes de tentar tooautoscale-lo. Se, escolhemos uma tooautoscale de métrica diferente no, usaríamos Olá `counterSpecifier` de configuração de extensão de diagnóstico hello como Olá `metricName` na configuração de AutoEscala hello. Para obter mais informações sobre configuração de dimensionamento automático, consulte Olá [práticas recomendadas de dimensionamento automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) e hello [documentação de referência da API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
