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
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="5332b-103">Como o dimensionamento automático toouse e conjuntos de escala de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5332b-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5332b-104">O dimensionamento automático de máquinas virtuais em um conjunto de escala é a criação de saudação ou exclusão de máquinas em Olá definido como necessário toomatch requisitos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5332b-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="5332b-105">Como aumentos de volume de saudação do trabalho, um aplicativo pode exigir recursos adicionais tooenable-tooeffectively executar tarefas.</span><span class="sxs-lookup"><span data-stu-id="5332b-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="5332b-106">O dimensionamento automático é um processo automatizado que ajuda a facilitar o gerenciamento da sobrecarga.</span><span class="sxs-lookup"><span data-stu-id="5332b-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="5332b-107">Reduzindo a sobrecarga, você não precise toocontinually monitorar o desempenho de sistema ou decidir como toomanage recursos.</span><span class="sxs-lookup"><span data-stu-id="5332b-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="5332b-108">O dimensionamento é um processo elástico.</span><span class="sxs-lookup"><span data-stu-id="5332b-108">Scaling is an elastic process.</span></span> <span data-ttu-id="5332b-109">Mais recursos podem ser adicionados como Olá carga aumenta.</span><span class="sxs-lookup"><span data-stu-id="5332b-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="5332b-110">E como a demanda diminui, recursos podem ser removidos toominimize custos e manter os níveis de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5332b-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="5332b-111">Configure o dimensionamento automático em uma escala definida por meio de um modelo do Azure Resource Manager, do Azure PowerShell, CLI do Azure ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5332b-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="5332b-112">Configure o dimensionamento usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5332b-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="5332b-113">Em vez de implantar e gerenciar cada recurso do seu aplicativo separadamente, use um modelo que implanta todos os recursos em uma única operação coordenada.</span><span class="sxs-lookup"><span data-stu-id="5332b-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="5332b-114">No modelo de hello, os recursos de aplicativo são definidos e implantação são especificados para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="5332b-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="5332b-115">Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="5332b-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="5332b-116">toolearn mais, examinar [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5332b-117">No modelo de saudação, você especificar o elemento de capacidade de saudação:</span><span class="sxs-lookup"><span data-stu-id="5332b-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="5332b-118">Capacidade identifica o número de saudação de máquinas virtuais no conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="5332b-119">Você pode alterar manualmente a capacidade de saudação Implantando um modelo com um valor diferente.</span><span class="sxs-lookup"><span data-stu-id="5332b-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="5332b-120">Se você estiver implantando uma capacidade de saudação do modelo tooonly alteração, você pode incluir apenas o elemento de SKU de saudação com capacidade de saudação atualizada.</span><span class="sxs-lookup"><span data-stu-id="5332b-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="5332b-121">Olá capacidade de seu conjunto de escala pode ser ajustada automaticamente usando uma combinação de saudação **autoscaleSettings** hello e recursos de extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5332b-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="5332b-122">Configurar a extensão de diagnóstico do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="5332b-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="5332b-123">O dimensionamento automático só pode ser feito se a coleção de métricas for bem-sucedida em cada máquina virtual no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="5332b-124">Olá extensão de diagnóstico do Azure fornece recursos de monitoramento e diagnóstico de saudação que atenda às necessidades de coleta de métricas Olá do recurso de AutoEscala hello.</span><span class="sxs-lookup"><span data-stu-id="5332b-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="5332b-125">Você pode instalar a extensão de saudação como parte do modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="5332b-126">Este exemplo mostra as variáveis de saudação que são usadas na extensão de diagnóstico Olá modelo tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="5332b-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="5332b-127">Parâmetros são fornecidos ao modelo de saudação é implantado.</span><span class="sxs-lookup"><span data-stu-id="5332b-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="5332b-128">Neste exemplo, o nome Olá Olá da conta de armazenamento (em que dados são armazenados) e a saudação nome do conjunto de escalas da saudação (onde os dados são coletados) são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="5332b-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="5332b-129">Também neste exemplo do Windows Server, somente Olá a contagem de threads contador de desempenho é coletado.</span><span class="sxs-lookup"><span data-stu-id="5332b-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="5332b-130">Olá a todos os contadores de desempenho disponíveis no Windows ou Linux pode ser usados toocollect informações de diagnóstico e pode ser incluído na configuração de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="5332b-131">Este exemplo mostra a definição de saudação da extensão de saudação no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="5332b-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="5332b-132">Quando a extensão de diagnóstico de saudação é executado, os dados de saudação são armazenados e coletados em uma tabela, na conta de armazenamento Olá que você especificar.</span><span class="sxs-lookup"><span data-stu-id="5332b-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="5332b-133">Em Olá **WADPerformanceCounters** tabela, você pode encontrar dados coletado de saudação:</span><span class="sxs-lookup"><span data-stu-id="5332b-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="5332b-134">Configurar o recurso de autoScaleSettings Olá</span><span class="sxs-lookup"><span data-stu-id="5332b-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="5332b-135">recursos de autoscaleSettings Olá usa as informações de saudação do hello toodecide de extensão de diagnóstico se tooincrease ou diminuir o número de saudação de máquinas virtuais em escala de saudação definido.</span><span class="sxs-lookup"><span data-stu-id="5332b-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="5332b-136">Este exemplo mostra a configuração de saudação do recurso Olá no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="5332b-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="5332b-137">O exemplo hello acima, as duas regras são criadas para definir ações de dimensionamento automático hello.</span><span class="sxs-lookup"><span data-stu-id="5332b-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="5332b-138">primeira regra de saudação define a ação de expansão hello e regra segundo Olá define Olá escala em ação.</span><span class="sxs-lookup"><span data-stu-id="5332b-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="5332b-139">Esses valores são fornecidos nas regras de saudação:</span><span class="sxs-lookup"><span data-stu-id="5332b-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="5332b-140">Regra</span><span class="sxs-lookup"><span data-stu-id="5332b-140">Rule</span></span> | <span data-ttu-id="5332b-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="5332b-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="5332b-142">metricName</span><span class="sxs-lookup"><span data-stu-id="5332b-142">metricName</span></span>        | <span data-ttu-id="5332b-143">Esse valor é Olá mesmo que o contador de desempenho de saudação definido na variável de wadperfcounter Olá para extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="5332b-144">No exemplo hello acima, o contador de contagem de threads de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="5332b-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="5332b-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="5332b-145">metricResourceUri</span></span> | <span data-ttu-id="5332b-146">Esse valor é o identificador de recurso de saudação do conjunto de escala de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="5332b-147">Esse identificador contém nome Olá Olá do grupo de recursos, o nome de saudação do provedor de recursos de saudação e o nome de saudação do Olá tooscale de conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="5332b-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="5332b-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="5332b-148">timeGrain</span></span>         | <span data-ttu-id="5332b-149">Esse valor é a granularidade de saudação de métricas de saudação que são coletadas.</span><span class="sxs-lookup"><span data-stu-id="5332b-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="5332b-150">Em Olá anterior de exemplo, os dados são coletados em um intervalo de um minuto.</span><span class="sxs-lookup"><span data-stu-id="5332b-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="5332b-151">Esse valor é usado em conjunto com timeWindow.</span><span class="sxs-lookup"><span data-stu-id="5332b-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="5332b-152">statistic</span><span class="sxs-lookup"><span data-stu-id="5332b-152">statistic</span></span>         | <span data-ttu-id="5332b-153">Esse valor determina como as métricas de saudação são combinados tooaccommodate Olá automática de ação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="5332b-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="5332b-154">Olá os valores possíveis são: média, Mín, máx.</span><span class="sxs-lookup"><span data-stu-id="5332b-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="5332b-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="5332b-155">timeWindow</span></span>        | <span data-ttu-id="5332b-156">Esse valor é Olá intervalo de tempo no qual os dados de instância são coletados.</span><span class="sxs-lookup"><span data-stu-id="5332b-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="5332b-157">Deve estar entre 5 minutos e 12 horas.</span><span class="sxs-lookup"><span data-stu-id="5332b-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="5332b-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="5332b-158">timeAggregation</span></span>   | <span data-ttu-id="5332b-159">Esse valor determina como os dados de saudação que são coletados devem ser combinados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="5332b-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="5332b-160">valor padrão de saudação é média.</span><span class="sxs-lookup"><span data-stu-id="5332b-160">hello default value is Average.</span></span> <span data-ttu-id="5332b-161">Olá os valores possíveis são: média, mínimo, máximo, último, Total, contagem.</span><span class="sxs-lookup"><span data-stu-id="5332b-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="5332b-162">operator</span><span class="sxs-lookup"><span data-stu-id="5332b-162">operator</span></span>          | <span data-ttu-id="5332b-163">Esse valor é o operador Olá toocompare usado Olá métrica dados e hello limite.</span><span class="sxs-lookup"><span data-stu-id="5332b-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="5332b-164">Olá os valores possíveis são: igual a, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="5332b-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="5332b-165">threshold</span><span class="sxs-lookup"><span data-stu-id="5332b-165">threshold</span></span>         | <span data-ttu-id="5332b-166">Esse valor será Olá que dispara a ação de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="5332b-167">Ser tooprovide-se de que a diferença suficiente entre os valores de limite de Olá para Olá **expansão** e **em escala** ações.</span><span class="sxs-lookup"><span data-stu-id="5332b-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="5332b-168">Se você definir Olá mesmos valores para as duas ações, o sistema Olá prevê alteração constante, o que impede a implementação de uma ação de escala.</span><span class="sxs-lookup"><span data-stu-id="5332b-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="5332b-169">Por exemplo, definir ambos os threads too600 em Olá anterior exemplo não funciona.</span><span class="sxs-lookup"><span data-stu-id="5332b-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="5332b-170">direction</span><span class="sxs-lookup"><span data-stu-id="5332b-170">direction</span></span>         | <span data-ttu-id="5332b-171">Esse valor determina a ação de saudação que é obtida quando o valor de limite de saudação é obtida.</span><span class="sxs-lookup"><span data-stu-id="5332b-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="5332b-172">Olá possíveis valores são aumento ou diminuição.</span><span class="sxs-lookup"><span data-stu-id="5332b-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="5332b-173">type</span><span class="sxs-lookup"><span data-stu-id="5332b-173">type</span></span>              | <span data-ttu-id="5332b-174">Esse valor é o tipo de saudação de ação que deve ocorrer e deve ser definido como tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="5332b-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="5332b-175">valor</span><span class="sxs-lookup"><span data-stu-id="5332b-175">value</span></span>             | <span data-ttu-id="5332b-176">Esse valor é o número de saudação de máquinas virtuais que são adicionados tooor removido do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="5332b-177">Este valor deve ser 1 ou maior.</span><span class="sxs-lookup"><span data-stu-id="5332b-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="5332b-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="5332b-178">cooldown</span></span>          | <span data-ttu-id="5332b-179">Esse valor é Olá toowait tempo desde a última ação de escala Olá antes da próxima ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="5332b-180">Esse valor deve estar entre um minuto e uma semana.</span><span class="sxs-lookup"><span data-stu-id="5332b-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="5332b-181">Dependendo do contador de desempenho hello, você está usando, alguns dos elementos de saudação na configuração de modelo de saudação são usados de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="5332b-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="5332b-182">No hello anterior de exemplo, o contador de desempenho Olá é a contagem de threads, valor de limite de saudação é 650 para uma ação de expansão e valor de limite de saudação é 550 para ação de escala em hello.</span><span class="sxs-lookup"><span data-stu-id="5332b-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="5332b-183">Se você usar um contador, como % tempo do processador, o valor de limite de saudação é definido toohello porcentagem de uso da CPU que determina a ação de escala.</span><span class="sxs-lookup"><span data-stu-id="5332b-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="5332b-184">Quando uma ação de escala é acionada, como uma carga de alta capacidade de saudação do conjunto de saudação é aumentada com base no valor de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="5332b-185">Por exemplo, em uma escala de definir onde capacidade Olá é definida too3 e valor de ação de escala de saudação é definido too1:</span><span class="sxs-lookup"><span data-stu-id="5332b-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="5332b-186">Quando Olá atual carga causas Olá thread médio contagem toogo acima do limite de saudação de 650:</span><span class="sxs-lookup"><span data-stu-id="5332b-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="5332b-187">Um **expansão** ação é disparada causas Olá capacidade de saudação conjunto toobe acrescido de um:</span><span class="sxs-lookup"><span data-stu-id="5332b-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="5332b-188">saudação de resultados é que uma máquina virtual é adicionada toohello conjunto de escala:</span><span class="sxs-lookup"><span data-stu-id="5332b-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="5332b-189">Após um período de cooldown de cinco minutos, se o número médio de saudação de threads em máquinas de saudação permanece em 600, outro computador será adicionado toohello conjunto.</span><span class="sxs-lookup"><span data-stu-id="5332b-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="5332b-190">Se a contagem de threads de média de saudação permanecer abaixo 550, capacidade de saudação do conjunto de escala de saudação é reduzida por um e um computador é removido do conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="5332b-191">Configurar o dimensionamento usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5332b-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="5332b-192">toosee exemplos de como usar o PowerShell tooset o dimensionamento automático, examinar [rápido do PowerShell do Azure Monitor iniciar exemplos](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="5332b-193">Configurar o dimensionamento usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5332b-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="5332b-194">exemplos de toosee de uso tooset CLI do Azure o dimensionamento automático, examine [CLI de plataforma cruzada do Monitor do Azure rápido iniciar exemplos](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="5332b-195">Configurar o dimensionamento usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5332b-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="5332b-196">Olá toosee um exemplo do uso do Azure tooset portal o dimensionamento automático, procure em [criar um conjunto de escala de máquinas virtuais usando o portal do Azure de saudação](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="5332b-197">Investigar ações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="5332b-197">Investigate scaling actions</span></span>

* <span data-ttu-id="5332b-198">**Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="5332b-198">**Azure portal**</span></span>  
<span data-ttu-id="5332b-199">No momento, você pode obter uma quantidade limitada de informações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="5332b-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="5332b-200">**Gerenciador de Recursos do Azure**</span><span class="sxs-lookup"><span data-stu-id="5332b-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="5332b-201">Essa ferramenta é hello melhor para explorar o estado atual de saudação do seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="5332b-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="5332b-202">Siga este caminho e você deverá ver a exibição de instância de saudação de escala Olá definido que você criou:</span><span class="sxs-lookup"><span data-stu-id="5332b-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="5332b-203">**Assinaturas > {sua assinatura} > resourceGroups {seu grupo de recursos} > provedores > Microsoft.Compute > virtualMachineScaleSets > {seu conjunto de dimensionamento} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="5332b-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="5332b-204">**PowerShell do Azure**</span><span class="sxs-lookup"><span data-stu-id="5332b-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="5332b-205">Use este comando tooget algumas informações:</span><span class="sxs-lookup"><span data-stu-id="5332b-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="5332b-206">Conecte máquina de virtual jumpbox toohello exatamente como faria com qualquer outro computador e, em seguida, você pode acessar remotamente máquinas virtuais Olá Olá escala conjunto toomonitor individuais processos.</span><span class="sxs-lookup"><span data-stu-id="5332b-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5332b-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5332b-207">Next Steps</span></span>
* <span data-ttu-id="5332b-208">Examinar [dimensionar automaticamente máquinas em um conjunto de escala de máquinas virtuais](virtual-machine-scale-sets-windows-autoscale.md) toosee um exemplo de como toocreate uma conjunto de escala com o dimensionamento automático configurado.</span><span class="sxs-lookup"><span data-stu-id="5332b-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="5332b-209">Encontre exemplos de recursos de monitoramento do Azure Monitor nos [Exemplos de início rápido do Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="5332b-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="5332b-210">Saiba mais sobre os recursos de notificação em [usar AutoEscala ações toosend email e webhook notificações de alerta no Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="5332b-211">Saiba mais sobre como muito[notificações de alerta de e-mail e webhook toosend os logs de auditoria de uso no Monitor do Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="5332b-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="5332b-212">Saiba mais sobre [Cenários de dimensionamento automático avançado](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="5332b-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
