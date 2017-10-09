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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="ce77a-103">Dimensionamento automático usando métricas de convidado em um modelo de conjunto de dimensionamento do Linux</span><span class="sxs-lookup"><span data-stu-id="ce77a-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="ce77a-104">Há dois tipos de métricas no Azure que são coletadas de VMs e conjuntos de escala: algumas vêm da saudação host VM e outros vêm de convidado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ce77a-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="ce77a-105">Métricas de host não exigem configuração adicional porque eles são coletados pelo host Olá VM, enquanto as métricas de convidado requerem tooinstall Olá [extensão de diagnóstico do Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) ou hello [diagnóstico do Azure Linux extensão](../virtual-machines/linux/diagnostic-extension.md) em Olá VM convidada.</span><span class="sxs-lookup"><span data-stu-id="ce77a-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="ce77a-106">Um motivo toouse convidado métricas mais comuns em vez de métricas de host é que as métricas de convidado fornecem uma seleção maior de métricas de métricas de host.</span><span class="sxs-lookup"><span data-stu-id="ce77a-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="ce77a-107">Um exemplo disso são as métricas de consumo de memória, que só estão disponíveis por meio de métricas de convidado.</span><span class="sxs-lookup"><span data-stu-id="ce77a-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="ce77a-108">métricas de host Olá com suporte são listadas [aqui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e métricas usadas convidado são listadas [aqui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ce77a-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="ce77a-109">Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toouse regras de dimensionamento automático com base nas métricas de convidado para conjuntos de escala do Linux.</span><span class="sxs-lookup"><span data-stu-id="ce77a-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="ce77a-110">Alterar a definição de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="ce77a-110">Change hello template definition</span></span>

<span data-ttu-id="ce77a-111">Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala de Linux Olá definido com o dimensionamento automático com base no convidado pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ce77a-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="ce77a-112">Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:</span><span class="sxs-lookup"><span data-stu-id="ce77a-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="ce77a-113">Primeiro, adicionamos parâmetros para `storageAccountName` e `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="ce77a-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="ce77a-114">Agente de diagnóstico Olá armazenará dados de métrica em uma [tabela](../cosmos-db/table-storage-how-to-use-dotnet.md) nesta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ce77a-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="ce77a-115">A partir de Olá agente de diagnóstico do Linux versão 3.0, usando uma chave de acesso de armazenamento não é mais suportada.</span><span class="sxs-lookup"><span data-stu-id="ce77a-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="ce77a-116">É necessário usar um [Token SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ce77a-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="ce77a-117">Em seguida, podemos modificar o conjunto de escala Olá `extensionProfile` tooinclude extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce77a-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="ce77a-118">Nessa configuração, podemos especificar recursos Olá ID de escala Olá definida toocollect métricas de, bem como Olá conta de armazenamento e métricas de saudação do SAS token toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="ce77a-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="ce77a-119">Nós também especificar com que frequência as métricas de saudação são agregadas (no caso a cada minuto) e tootrack quais métricas (por este caso memória usada por cento).</span><span class="sxs-lookup"><span data-stu-id="ce77a-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="ce77a-120">Para obter informações mais detalhadas sobre essa configuração e métricas diferentes da porcentagem de memória usada, consulte [esta documentação](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ce77a-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="ce77a-121">Por fim, adicionamos uma `autoscaleSettings` recurso tooconfigure AutoEscala com base nessas métricas.</span><span class="sxs-lookup"><span data-stu-id="ce77a-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="ce77a-122">Este recurso tem um `dependsOn` cláusula que faz referência a escala Olá definida tooensure conjunto de escala Olá existe antes de tentar tooautoscale-lo.</span><span class="sxs-lookup"><span data-stu-id="ce77a-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="ce77a-123">Se, escolhemos uma tooautoscale de métrica diferente no, usaríamos Olá `counterSpecifier` de configuração de extensão de diagnóstico hello como Olá `metricName` na configuração de AutoEscala hello.</span><span class="sxs-lookup"><span data-stu-id="ce77a-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="ce77a-124">Para obter mais informações sobre configuração de dimensionamento automático, consulte Olá [práticas recomendadas de dimensionamento automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) e hello [documentação de referência da API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce77a-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="ce77a-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce77a-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
