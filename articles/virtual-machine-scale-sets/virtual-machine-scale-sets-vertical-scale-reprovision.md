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
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Dimensionamento vertical automático com conjuntos de Dimensionamento de Máquina Virtual
Este artigo descreve como a escala do Azure toovertically [conjuntos de escala de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/) com ou sem reprovisionamento. Para o escalonamento vertical de VMs que não estão em conjuntos de escala, consulte muito[escalar verticalmente a máquina virtual do Azure na automação do Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Dimensionamento vertical, também conhecido como *expandir* e *reduzir*, significa aumentando ou diminuindo a tamanhos de máquina virtual (VM) na carga de trabalho de tooa de resposta. Compare isso com [escalonamento horizontal](virtual-machine-scale-sets-autoscale-overview.md), também chamado tooas *expansão* e *ampliar*onde o número de saudação de VMs é alterada dependendo da carga de trabalho de saudação.

Reprovisionamento significa remover uma VM existente e substituí-la por uma nova. Quando você aumentar ou diminuir o tamanho de saudação de VMs em um conjunto de escala de VM, em alguns casos você deseja tooresize existente VMs e manter seus dados, enquanto em outros casos, você precisa toodeploy novas VMs de tamanho novo hello. Este documento aborda ambos os casos.

O dimensionamento vertical pode ser útil quando:

* Um serviço baseado em máquinas virtuais é subutilizados (por exemplo, aos finais de semana). Reduzir o tamanho da VM Olá pode reduzir os custos mensais.
* O aumento toocope de tamanho VM com maior demanda sem criar VMs adicionais.

Você pode configurar vertical dimensionamento toobe disparado com base na métricas alertas com base do seu conjunto de escala de VM. Quando Olá alerta for ativado ele acionar um webhook que aciona um runbook que pode dimensionar sua escala é definido para cima ou para baixo. É possível configurar o dimensionamento vertical seguindo estas etapas:

1. Crie uma conta de Automação do Azure com a funcionalidade executar como.
2. Importe os Runbooks de Escala Vertical da Automação do Azure para os Conjuntos de Escala de VM na sua assinatura.
3. Adicione um runbook de tooyour webhook.
4. Adicione um alerta tooyour conjunto de escala de VM usando uma notificação de webhook.

> [!NOTE]
> O dimensionamento automático vertical só pode ocorrer em determinadas faixas de tamanhos de VM. Comparar as especificações de saudação do tamanho de cada antes de decidir tooscale de um tooanother (número mais alto não sempre indica o tamanho de VM maior). Você pode escolher tooscale entre hello pares de tamanhos a seguir:
> 
> | Par de dimensionamento de tamanhos de VM |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Criar uma Conta de Automação do Azure com a funcionalidade executar como
Olá primeira coisa toodo é criar uma conta de automação do Azure que hospedará Olá runbooks usado tooscale Olá conjunto de escala de VM instâncias. Recentemente [automação do Azure](https://azure.microsoft.com/services/automation/) introduziu o recurso "Executar como conta" hello que torna a configuração Olá entidade de serviço para execução automática Olá runbooks em um nome de usuário muito fácil. Você pode ler mais sobre isso em um artigo de saudação abaixo:

* [Autenticar Runbooks com uma conta Executar como do Azure](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importar os Runbooks de Escala Vertical da Automação do Azure para sua assinatura
Olá runbooks necessário escala toovertically que seus conjuntos de escala de VM já estão publicados em Olá Galeria de Runbook de automação do Azure. tooimport-los em sua assinatura siga Olá as etapas neste artigo:

* [Galerias de runbook e de módulos para a Automação do Azure](../automation/automation-runbook-gallery.md)

Escolha a opção de procurar Galeria de saudação menu Runbooks hello:

![Toobe runbooks importado][runbooks]

Olá runbooks que precisam toobe importado são exibidos. Selecione o runbook Olá com base em se você quer vertical de dimensionamento com ou sem reprovisionamento:

![Galeria de Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Adicionar um runbook de tooyour do webhook
Depois de importar runbooks Olá precisará tooadd um runbook de toohello webhook para que ele pode ser acionado por um alerta de um conjunto de escala de VM. detalhes de saudação da criação de um webhook para seu Runbook são descritos neste artigo:

* [Webhooks da Automação do Azure](../automation/automation-webhooks.md)

> [!NOTE]
> Certifique-se de que copiar Olá webhook URI antes de fechar a caixa de diálogo de webhook hello como ele será necessário na próxima seção, Olá.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Adicionar um alerta tooyour conjunto de escala de VM
Abaixo está um PowerShell script que mostra como tooadd um alerta tooa conjunto de escala de VM. Consulte toohello após o nome do artigo tooget Olá de alerta de saudação do hello toofire métrica: [métricas comuns de dimensionamento automático de Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

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
> É recomendável tooconfigure uma janela de tempo razoável de alerta de saudação em ordem tooavoid acionar o escalonamento vertical e houver associados à interrupção do serviço, com muita frequência. Considere uma janela de pelo menos 20 a 30 minutos ou mais. Considere horizontal escala se precisar tooavoid qualquer interrupção.
> 
> 

Para obter mais informações sobre como toocreate alertas Consulte toohello artigos a seguir:

* [Exemplos de início rápido do Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Exemplos de início rápido da CLI entre plataformas do Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Resumo
Este artigo mostrou exemplos simples de dimensionamento vertical. Com essa base (conta de Automação, Runbooks, webhooks e alertas) você pode conectar uma grande variedade de eventos com um conjunto personalizado de ações.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
