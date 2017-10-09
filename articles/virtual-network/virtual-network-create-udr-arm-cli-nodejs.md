---
title: "dispositivos de roteamento e virtual de aaaControl usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como dispositivos de roteamento e virtual de toocontrol usando Olá 1.0 da CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>Criar rotas definidas pelo usuário (UDR) usando Olá 1.0 da CLI do Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI do Azure](virtual-network-create-udr-arm-cli.md)
> * [Modelo](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Clássico)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Clássica)](virtual-network-create-udr-classic-cli.md)

Crie roteamento personalizado e dispositivos virtuais usando Olá CLI do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete 

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir: 

- [1.0 de CLI do Azure](#Create-the-UDR-for-the-front-end-subnet) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](virtual-network-create-udr-arm-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Criar hello UDR para sub-rede front-end Olá
tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.

1. Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede front-end hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    Saída:
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    Parâmetros:
   
   * **-g (ou --resource-group)**. Nome do grupo de recursos de saudação onde Olá UDR será criado. Para o nosso cenário, *TestRG*.
   * **-l (ou --location)**. Região do Azure onde hello UDR novo será criado. Para o nosso cenário, *westus*.
   * **-n (or --name)**. Nome para Olá UDR novo. Para nosso cenário, *UDR-FrontEnd*.
2. Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    Saída:
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    Parâmetros:
   
   * **-r (ou --route-table-name)**. Nome da tabela de rota Olá onde rota Olá será adicionada. Para nosso cenário, *UDR-FrontEnd*.
   * **-a (ou --address-prefix)**. Prefixo de endereço de sub-rede Olá onde os pacotes são destinados a. Para nosso cenário, *192.168.2.0/24*.
   * **-y (ou --next-hop-type)**. Tipo de objeto ao qual o tráfego será enviado. Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.
   * **-p (ou --next-hop-ip-address**). Endereço IP do próximo salto. Para o nosso cenário, *192.168.0.4*.
3. Tabela de rotas Olá tooassociate criada acima com hello comando a seguir de execução Olá **front-end** sub-rede:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Saída:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    Parâmetros:
   
   * **-e (ou --vnet-name)**. Nome de rede virtual onde está localizada a sub-rede de saudação do hello. Para o nosso cenário, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Criar hello UDR para a sub-rede de back-end Olá
tabela de rotas de saudação toocreate e rotear necessários para a sub-rede de back-end de saudação com base no cenário de saudação acima, Olá concluir as etapas a seguir:

1. Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Habilite o encaminhamento de IP em FW1
encaminhamento de IP tooenable em Olá NIC usada por **FW1**completa Olá seguintes etapas:

1. Executar comando de saudação que segue e observe o valor de saudação para **encaminhamento IP habilitar**. Ele deve ser definido muito*false*.

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    Saída:
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. Execute Olá encaminhamento de IP de tooenable de comando a seguir:

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    Saída:
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    Parâmetros:
   
   * **-f (ou --enable-ip-forwarding)**. *true* ou *false*.

