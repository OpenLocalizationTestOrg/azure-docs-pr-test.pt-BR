---
title: "Exemplo de Script do Azure PowerShell – Abrir porta de aplicativo no balanceador de carga | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell – Abrir uma porta no Azure Load Balancer para um aplicativo do Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: sample
ms.date: 12/08/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: c643fc9e575a8e836a361893d78348bbd627a425
ms.sourcegitcommit: 42ee5ea09d9684ed7a71e7974ceb141d525361c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/09/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a>Abrir uma porta de aplicativo no Azure Load Balancer

Um aplicativo do Service Fabric em execução no Azure fica por trás do Azure Load Balancer. Este exemplo de script abre uma porta em um Azure Load Balancer para que um aplicativo do Service Fabric possa se comunicar com clientes externos. Personalize os parâmetros conforme necessário. Se o cluster estiver em um grupo de segurança de rede, também [adicione uma regra de grupo de segurança de rede de entrada](service-fabric-powershell-add-nsg-rule.md) para permitir o tráfego de entrada.

Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Obtém um recurso do Azure.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Obtém o Azure Load Balancer. |
| [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | Adiciona uma configuração de investigação a um balanceador de carga.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Obtém uma configuração de investigação para um balanceador de carga. |
| [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | Adiciona uma configuração de regra a um balanceador de carga. |
| [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | Define a meta de estado para um balanceador de carga. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).

Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).
