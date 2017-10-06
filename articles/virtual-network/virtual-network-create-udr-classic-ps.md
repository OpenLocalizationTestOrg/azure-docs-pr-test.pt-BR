---
title: "aaaControl roteamento em uma rede Virtual do Azure - PowerShell - clássico | Microsoft Docs"
description: "Saiba como toocontrol roteamento em VNets usando o PowerShell | Clássico"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Controlar o roteamento e usar dispositivos virtuais (clássico) usando o PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI do Azure](virtual-network-create-udr-arm-cli.md)
> * [Modelo](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Clássico)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Clássica)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico. Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabalhar com qualquer recurso do Azure. Você pode exibir a documentação de saudação para diferentes ferramentas selecionando uma opção na parte superior da saudação deste artigo. Este artigo aborda o modelo de implantação clássico hello.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

exemplo Hello Azure PowerShell comandos abaixo esperam um ambiente simples já foi criado com base no cenário de saudação acima. Comandos de saudação toorun conforme elas são exibidas neste documento, criar ambiente Olá mostrado na [criar uma rede virtual (clássica) usando o PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Criar hello UDR para a sub-rede de front-end Olá
tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.

1. Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede front-end hello:

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Execução hello após a tabela de rotas do comando tooassociate Olá com hello **front-end** sub-rede:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Criar hello UDR para a sub-rede de back-end Olá
tabela de rotas toocreate hello e rota necessário para fazer Olá end subrede com base no cenário de saudação, conclua Olá etapas a seguir:

1. Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Habilitar o encaminhamento de IP hello FW1 VM

encaminhamento de IP tooenable em Olá FW1 VM, Olá concluir as etapas a seguir:

1. Execute Olá status do comando toocheck Olá de encaminhamento IP a seguir:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Comando a seguir de execução Olá tooenable encaminhamento de IP para Olá *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
