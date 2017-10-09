---
title: "conjuntos de escala de máquina virtual do Azure de escala de aaaVertically | Microsoft Docs"
description: "Como toovertically dimensionar uma máquina Virtual em alertas de toomonitoring de resposta na automação do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="fef89-103">Dimensionamento vertical automático com conjuntos de Dimensionamento de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="fef89-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="fef89-104">Este artigo descreve como a escala do Azure toovertically [conjuntos de escala de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/) com ou sem reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="fef89-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="fef89-105">Para o escalonamento vertical de VMs que não estão em conjuntos de escala, consulte muito[escalar verticalmente a máquina virtual do Azure na automação do Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fef89-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fef89-106">Dimensionamento vertical, também conhecido como *expandir* e *reduzir*, significa aumentando ou diminuindo a tamanhos de máquina virtual (VM) na carga de trabalho de tooa de resposta.</span><span class="sxs-lookup"><span data-stu-id="fef89-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="fef89-107">Compare isso com [escalonamento horizontal](virtual-machine-scale-sets-autoscale-overview.md), também chamado tooas *expansão* e *ampliar*onde o número de saudação de VMs é alterada dependendo da carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fef89-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="fef89-108">Reprovisionamento significa remover uma VM existente e substituí-la por uma nova.</span><span class="sxs-lookup"><span data-stu-id="fef89-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="fef89-109">Quando você aumentar ou diminuir o tamanho de saudação de VMs em um conjunto de escala de VM, em alguns casos você deseja tooresize existente VMs e manter seus dados, enquanto em outros casos, você precisa toodeploy novas VMs de tamanho novo hello.</span><span class="sxs-lookup"><span data-stu-id="fef89-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="fef89-110">Este documento aborda ambos os casos.</span><span class="sxs-lookup"><span data-stu-id="fef89-110">This document covers both cases.</span></span>

<span data-ttu-id="fef89-111">O dimensionamento vertical pode ser útil quando:</span><span class="sxs-lookup"><span data-stu-id="fef89-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="fef89-112">Um serviço baseado em máquinas virtuais é subutilizados (por exemplo, aos finais de semana).</span><span class="sxs-lookup"><span data-stu-id="fef89-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="fef89-113">Reduzir o tamanho da VM Olá pode reduzir os custos mensais.</span><span class="sxs-lookup"><span data-stu-id="fef89-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="fef89-114">O aumento toocope de tamanho VM com maior demanda sem criar VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="fef89-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="fef89-115">Você pode configurar vertical dimensionamento toobe disparado com base na métricas alertas com base do seu conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="fef89-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="fef89-116">Quando Olá alerta for ativado ele acionar um webhook que aciona um runbook que pode dimensionar sua escala é definido para cima ou para baixo.</span><span class="sxs-lookup"><span data-stu-id="fef89-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="fef89-117">É possível configurar o dimensionamento vertical seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fef89-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="fef89-118">Crie uma conta de Automação do Azure com a funcionalidade executar como.</span><span class="sxs-lookup"><span data-stu-id="fef89-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="fef89-119">Importe os Runbooks de Escala Vertical da Automação do Azure para os Conjuntos de Escala de VM na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="fef89-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="fef89-120">Adicione um runbook de tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="fef89-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="fef89-121">Adicione um alerta tooyour conjunto de escala de VM usando uma notificação de webhook.</span><span class="sxs-lookup"><span data-stu-id="fef89-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="fef89-122">O dimensionamento automático vertical só pode ocorrer em determinadas faixas de tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="fef89-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="fef89-123">Comparar as especificações de saudação do tamanho de cada antes de decidir tooscale de um tooanother (número mais alto não sempre indica o tamanho de VM maior).</span><span class="sxs-lookup"><span data-stu-id="fef89-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="fef89-124">Você pode escolher tooscale entre hello pares de tamanhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fef89-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="fef89-125">Par de dimensionamento de tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="fef89-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="fef89-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="fef89-126">Standard_A0</span></span> |<span data-ttu-id="fef89-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="fef89-127">Standard_A11</span></span> |
> | <span data-ttu-id="fef89-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="fef89-128">Standard_D1</span></span> |<span data-ttu-id="fef89-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="fef89-129">Standard_D14</span></span> |
> | <span data-ttu-id="fef89-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="fef89-130">Standard_DS1</span></span> |<span data-ttu-id="fef89-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="fef89-131">Standard_DS14</span></span> |
> | <span data-ttu-id="fef89-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="fef89-132">Standard_D1v2</span></span> |<span data-ttu-id="fef89-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="fef89-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="fef89-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="fef89-134">Standard_G1</span></span> |<span data-ttu-id="fef89-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="fef89-135">Standard_G5</span></span> |
> | <span data-ttu-id="fef89-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="fef89-136">Standard_GS1</span></span> |<span data-ttu-id="fef89-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="fef89-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="fef89-138">Criar uma Conta de Automação do Azure com a funcionalidade executar como</span><span class="sxs-lookup"><span data-stu-id="fef89-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="fef89-139">Olá primeira coisa toodo é criar uma conta de automação do Azure que hospedará Olá runbooks usado tooscale Olá conjunto de escala de VM instâncias.</span><span class="sxs-lookup"><span data-stu-id="fef89-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="fef89-140">Recentemente [automação do Azure](https://azure.microsoft.com/services/automation/) introduziu o recurso "Executar como conta" hello que torna a configuração Olá entidade de serviço para execução automática Olá runbooks em um nome de usuário muito fácil.</span><span class="sxs-lookup"><span data-stu-id="fef89-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="fef89-141">Você pode ler mais sobre isso em um artigo de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="fef89-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="fef89-142">Autenticar Runbooks com uma conta Executar como do Azure</span><span class="sxs-lookup"><span data-stu-id="fef89-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="fef89-143">Importar os Runbooks de Escala Vertical da Automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="fef89-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="fef89-144">Olá runbooks necessário escala toovertically que seus conjuntos de escala de VM já estão publicados em Olá Galeria de Runbook de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="fef89-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="fef89-145">tooimport-los em sua assinatura siga Olá as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="fef89-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="fef89-146">Galerias de runbook e de módulos para a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="fef89-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="fef89-147">Escolha a opção de procurar Galeria de saudação menu Runbooks hello:</span><span class="sxs-lookup"><span data-stu-id="fef89-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe runbooks importado][runbooks]

<span data-ttu-id="fef89-149">Olá runbooks que precisam toobe importado são exibidos.</span><span class="sxs-lookup"><span data-stu-id="fef89-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="fef89-150">Selecione o runbook Olá com base em se você quer vertical de dimensionamento com ou sem reprovisionamento:</span><span class="sxs-lookup"><span data-stu-id="fef89-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galeria de Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="fef89-152">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="fef89-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="fef89-153">Depois de importar runbooks Olá precisará tooadd um runbook de toohello webhook para que ele pode ser acionado por um alerta de um conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="fef89-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="fef89-154">detalhes de saudação da criação de um webhook para seu Runbook são descritos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="fef89-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="fef89-155">Webhooks da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="fef89-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="fef89-156">Certifique-se de que copiar Olá webhook URI antes de fechar a caixa de diálogo de webhook hello como ele será necessário na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="fef89-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="fef89-157">Adicionar um alerta tooyour conjunto de escala de VM</span><span class="sxs-lookup"><span data-stu-id="fef89-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="fef89-158">Abaixo está um PowerShell script que mostra como tooadd um alerta tooa conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="fef89-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="fef89-159">Consulte toohello após o nome do artigo tooget Olá de alerta de saudação do hello toofire métrica: [métricas comuns de dimensionamento automático de Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fef89-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="fef89-160">É recomendável tooconfigure uma janela de tempo razoável de alerta de saudação em ordem tooavoid acionar o escalonamento vertical e houver associados à interrupção do serviço, com muita frequência.</span><span class="sxs-lookup"><span data-stu-id="fef89-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="fef89-161">Considere uma janela de pelo menos 20 a 30 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="fef89-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="fef89-162">Considere horizontal escala se precisar tooavoid qualquer interrupção.</span><span class="sxs-lookup"><span data-stu-id="fef89-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="fef89-163">Para obter mais informações sobre como toocreate alertas Consulte toohello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fef89-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="fef89-164">Exemplos de início rápido do Azure Monitor PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef89-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="fef89-165">Exemplos de início rápido da CLI entre plataformas do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="fef89-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="fef89-166">Resumo</span><span class="sxs-lookup"><span data-stu-id="fef89-166">Summary</span></span>
<span data-ttu-id="fef89-167">Este artigo mostrou exemplos simples de dimensionamento vertical.</span><span class="sxs-lookup"><span data-stu-id="fef89-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="fef89-168">Com essa base (conta de Automação, Runbooks, webhooks e alertas) você pode conectar uma grande variedade de eventos com um conjunto personalizado de ações.</span><span class="sxs-lookup"><span data-stu-id="fef89-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
