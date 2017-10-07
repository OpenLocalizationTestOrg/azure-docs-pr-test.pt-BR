---
title: "aaaCreate um voltados para Internet carregar balanceador - clássico do Azure PowerShell | Microsoft Docs"
description: "Saiba como toocreate voltado para a Internet um balanceador de carga no modo clássico, usando o PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Introdução à criação de um balanceador de carga para a Internet (clássico) no PowerShell

> [!div class="op_single_selector"]
> * [Portal clássico do Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Serviços de Nuvem do Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico. Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure. Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo. Este artigo aborda o modelo de implantação clássico hello. Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Configurar o balanceador de carga usando o PowerShell

tooset backup de um balanceador de carga usando o powershell, execute as etapas de saudação abaixo:

1. Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.
2. Depois de criar uma máquina virtual, você pode usar os cmdlets de PowerShell tooadd uma máquina virtual de tooa de Balanceador de carga dentro Olá mesmo serviço de nuvem.

Olá o exemplo a seguir você irá adicionar um conjunto de Balanceador de carga chamado "webfarm" toocloud máquinas "mytestcloud" (ou myctestcloud.cloudapp.net), a adição de pontos de extremidade Olá Olá toovirtual do balanceador de carga de serviço denominado "web1" e "web2". Balanceador de carga Hello recebe tráfego de rede na porta 80 e o balanceamento de carga entre máquinas virtuais de saudação definidas pelo ponto de extremidade local (no caso, a porta 80) hello usando TCP.

### <a name="step-1"></a>Etapa 1

Criar um ponto de extremidade com balanceamento de carga para web1"hello primeira VM"

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Etapa 2

Crie outro ponto de extremidade para hello segundo VM "web2" usando Olá mesmo carregar nome do balanceador de conjunto

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Remover uma máquina virtual de um balanceador de carga

Você pode usar o Remove-AzureEndpoint tooremove um ponto de extremidade de máquina virtual do balanceador de carga Olá

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Próximas etapas

Você também pode [começar a criar um balanceador de carga interno](load-balancer-get-started-ilb-classic-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.

Se seu aplicativo precisa tookeep conexões ativo para os servidores atrás de um balanceador de carga, você pode saber mais sobre [ocioso configurações de tempo limite TCP para um balanceador de carga](load-balancer-tcp-idle-timeout.md). Ele ajudará toolearn sobre o comportamento de conexão ociosa, quando você estiver usando um balanceador de carga do Azure.
