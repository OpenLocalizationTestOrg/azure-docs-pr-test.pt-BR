---
title: "conjuntos de escala aaaAutomatic dimensionamento e a máquina virtual | Microsoft Docs"
description: "Saiba mais sobre como usar o diagnóstico e máquinas virtuais do dimensionamento automático recursos tooautomatically escala em um conjunto de escala."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Como o dimensionamento automático toouse e conjuntos de escala de máquinas virtuais
O dimensionamento automático de máquinas virtuais em um conjunto de escala é a criação de saudação ou exclusão de máquinas em Olá definido como necessário toomatch requisitos de desempenho. Como aumentos de volume de saudação do trabalho, um aplicativo pode exigir recursos adicionais tooenable-tooeffectively executar tarefas.

O dimensionamento automático é um processo automatizado que ajuda a facilitar o gerenciamento da sobrecarga. Reduzindo a sobrecarga, você não precise toocontinually monitorar o desempenho de sistema ou decidir como toomanage recursos. O dimensionamento é um processo elástico. Mais recursos podem ser adicionados como Olá carga aumenta. E como a demanda diminui, recursos podem ser removidos toominimize custos e manter os níveis de desempenho.

Configure o dimensionamento automático em uma escala definida por meio de um modelo do Azure Resource Manager, do Azure PowerShell, CLI do Azure ou Olá portal do Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Configure o dimensionamento usando modelos do Resource Manager
Em vez de implantar e gerenciar cada recurso do seu aplicativo separadamente, use um modelo que implanta todos os recursos em uma única operação coordenada. No modelo de hello, os recursos de aplicativo são definidos e implantação são especificados para ambientes diferentes. Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação. toolearn mais, examinar [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

No modelo de saudação, você especificar o elemento de capacidade de saudação:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Capacidade identifica o número de saudação de máquinas virtuais no conjunto de saudação. Você pode alterar manualmente a capacidade de saudação Implantando um modelo com um valor diferente. Se você estiver implantando uma capacidade de saudação do modelo tooonly alteração, você pode incluir apenas o elemento de SKU de saudação com capacidade de saudação atualizada.

Olá capacidade de seu conjunto de escala pode ser ajustada automaticamente usando uma combinação de saudação **autoscaleSettings** hello e recursos de extensão de diagnóstico.

### <a name="configure-hello-azure-diagnostics-extension"></a>Configurar a extensão de diagnóstico do Azure Olá
O dimensionamento automático só pode ser feito se a coleção de métricas for bem-sucedida em cada máquina virtual no conjunto de escala de saudação. Olá extensão de diagnóstico do Azure fornece recursos de monitoramento e diagnóstico de saudação que atenda às necessidades de coleta de métricas Olá do recurso de AutoEscala hello. Você pode instalar a extensão de saudação como parte do modelo do Gerenciador de recursos de saudação.

Este exemplo mostra as variáveis de saudação que são usadas na extensão de diagnóstico Olá modelo tooconfigure hello:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Parâmetros são fornecidos ao modelo de saudação é implantado. Neste exemplo, o nome Olá Olá da conta de armazenamento (em que dados são armazenados) e a saudação nome do conjunto de escalas da saudação (onde os dados são coletados) são fornecidos. Também neste exemplo do Windows Server, somente Olá a contagem de threads contador de desempenho é coletado. Olá a todos os contadores de desempenho disponíveis no Windows ou Linux pode ser usados toocollect informações de diagnóstico e pode ser incluído na configuração de extensão de saudação.

Este exemplo mostra a definição de saudação da extensão de saudação no modelo de saudação:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Quando a extensão de diagnóstico de saudação é executado, os dados de saudação são armazenados e coletados em uma tabela, na conta de armazenamento Olá que você especificar. Em Olá **WADPerformanceCounters** tabela, você pode encontrar dados coletado de saudação:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Configurar o recurso de autoScaleSettings Olá
recursos de autoscaleSettings Olá usa as informações de saudação do hello toodecide de extensão de diagnóstico se tooincrease ou diminuir o número de saudação de máquinas virtuais em escala de saudação definido.

Este exemplo mostra a configuração de saudação do recurso Olá no modelo de saudação:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

O exemplo hello acima, as duas regras são criadas para definir ações de dimensionamento automático hello. primeira regra de saudação define a ação de expansão hello e regra segundo Olá define Olá escala em ação. Esses valores são fornecidos nas regras de saudação:

| Regra | Descrição |
| ---- | ----------- |
| metricName        | Esse valor é Olá mesmo que o contador de desempenho de saudação definido na variável de wadperfcounter Olá para extensão de diagnóstico de saudação. No exemplo hello acima, o contador de contagem de threads de saudação é usado.    |
| metricResourceUri | Esse valor é o identificador de recurso de saudação do conjunto de escala de máquinas virtuais de saudação. Esse identificador contém nome Olá Olá do grupo de recursos, o nome de saudação do provedor de recursos de saudação e o nome de saudação do Olá tooscale de conjunto de escala. |
| timeGrain         | Esse valor é a granularidade de saudação de métricas de saudação que são coletadas. Em Olá anterior de exemplo, os dados são coletados em um intervalo de um minuto. Esse valor é usado em conjunto com timeWindow. |
| statistic         | Esse valor determina como as métricas de saudação são combinados tooaccommodate Olá automática de ação de dimensionamento. Olá os valores possíveis são: média, Mín, máx. |
| timeWindow        | Esse valor é Olá intervalo de tempo no qual os dados de instância são coletados. Deve estar entre 5 minutos e 12 horas. |
| timeAggregation   | Esse valor determina como os dados de saudação que são coletados devem ser combinados ao longo do tempo. valor padrão de saudação é média. Olá os valores possíveis são: média, mínimo, máximo, último, Total, contagem. |
| operator          | Esse valor é o operador Olá toocompare usado Olá métrica dados e hello limite. Olá os valores possíveis são: igual a, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| threshold         | Esse valor será Olá que dispara a ação de escala de saudação. Ser tooprovide-se de que a diferença suficiente entre os valores de limite de Olá para Olá **expansão** e **em escala** ações. Se você definir Olá mesmos valores para as duas ações, o sistema Olá prevê alteração constante, o que impede a implementação de uma ação de escala. Por exemplo, definir ambos os threads too600 em Olá anterior exemplo não funciona. |
| direction         | Esse valor determina a ação de saudação que é obtida quando o valor de limite de saudação é obtida. Olá possíveis valores são aumento ou diminuição. |
| type              | Esse valor é o tipo de saudação de ação que deve ocorrer e deve ser definido como tooChangeCount. |
| valor             | Esse valor é o número de saudação de máquinas virtuais que são adicionados tooor removido do conjunto de escala de saudação. Este valor deve ser 1 ou maior. |
| cooldown          | Esse valor é Olá toowait tempo desde a última ação de escala Olá antes da próxima ação de saudação. Esse valor deve estar entre um minuto e uma semana. |

Dependendo do contador de desempenho hello, você está usando, alguns dos elementos de saudação na configuração de modelo de saudação são usados de forma diferente. No hello anterior de exemplo, o contador de desempenho Olá é a contagem de threads, valor de limite de saudação é 650 para uma ação de expansão e valor de limite de saudação é 550 para ação de escala em hello. Se você usar um contador, como % tempo do processador, o valor de limite de saudação é definido toohello porcentagem de uso da CPU que determina a ação de escala.

Quando uma ação de escala é acionada, como uma carga de alta capacidade de saudação do conjunto de saudação é aumentada com base no valor de saudação no modelo de saudação. Por exemplo, em uma escala de definir onde capacidade Olá é definida too3 e valor de ação de escala de saudação é definido too1:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Quando Olá atual carga causas Olá thread médio contagem toogo acima do limite de saudação de 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

Um **expansão** ação é disparada causas Olá capacidade de saudação conjunto toobe acrescido de um:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

saudação de resultados é que uma máquina virtual é adicionada toohello conjunto de escala:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Após um período de cooldown de cinco minutos, se o número médio de saudação de threads em máquinas de saudação permanece em 600, outro computador será adicionado toohello conjunto. Se a contagem de threads de média de saudação permanecer abaixo 550, capacidade de saudação do conjunto de escala de saudação é reduzida por um e um computador é removido do conjunto de saudação.

## <a name="set-up-scaling-using-azure-powershell"></a>Configurar o dimensionamento usando o Azure PowerShell

toosee exemplos de como usar o PowerShell tooset o dimensionamento automático, examinar [rápido do PowerShell do Azure Monitor iniciar exemplos](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Configurar o dimensionamento usando a CLI do Azure

exemplos de toosee de uso tooset CLI do Azure o dimensionamento automático, examine [CLI de plataforma cruzada do Monitor do Azure rápido iniciar exemplos](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Configurar o dimensionamento usando Olá portal do Azure

Olá toosee um exemplo do uso do Azure tooset portal o dimensionamento automático, procure em [criar um conjunto de escala de máquinas virtuais usando o portal do Azure de saudação](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Investigar ações de dimensionamento

* **Portal do Azure**  
No momento, você pode obter uma quantidade limitada de informações usando o portal de saudação.

* **Gerenciador de Recursos do Azure**  
Essa ferramenta é hello melhor para explorar o estado atual de saudação do seu conjunto de escala. Siga este caminho e você deverá ver a exibição de instância de saudação de escala Olá definido que você criou:  
**Assinaturas > {sua assinatura} > resourceGroups {seu grupo de recursos} > provedores > Microsoft.Compute > virtualMachineScaleSets > {seu conjunto de dimensionamento} > virtualMachines**

* **PowerShell do Azure**  
Use este comando tooget algumas informações:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Conecte máquina de virtual jumpbox toohello exatamente como faria com qualquer outro computador e, em seguida, você pode acessar remotamente máquinas virtuais Olá Olá escala conjunto toomonitor individuais processos.

## <a name="next-steps"></a>Próximas etapas
* Examinar [dimensionar automaticamente máquinas em um conjunto de escala de máquinas virtuais](virtual-machine-scale-sets-windows-autoscale.md) toosee um exemplo de como toocreate uma conjunto de escala com o dimensionamento automático configurado.

* Encontre exemplos de recursos de monitoramento do Azure Monitor nos [Exemplos de início rápido do Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)

* Saiba mais sobre os recursos de notificação em [usar AutoEscala ações toosend email e webhook notificações de alerta no Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Saiba mais sobre como muito[notificações de alerta de e-mail e webhook toosend os logs de auditoria de uso no Monitor do Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Saiba mais sobre [Cenários de dimensionamento automático avançado](virtual-machine-scale-sets-advanced-autoscale.md).
