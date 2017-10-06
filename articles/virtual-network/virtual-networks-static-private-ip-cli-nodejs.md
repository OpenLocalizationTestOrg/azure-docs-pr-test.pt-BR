---
title: "endereços IP privados de aaaConfigure para VMs - 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando hello Azure interface de linha de comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a>Configurar endereços IP para uma máquina virtual usando Olá 1.0 da CLI do Azure


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete 

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir: 

- [1.0 de CLI do Azure](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](virtual-networks-static-private-ip-arm-cli.md) -nosso CLI de última geração para o modelo de implantação do gerenciamento de recursos de saudação 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Como toospecify um particular de endereços IP estáticos ao criar uma VM
toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.
   
        azure config mode arm
   
    Saída esperada:
   
        info:    New mode is arm
3. Executar Olá **public-ip de rede do azure criar** toocreate um IP público para Olá VM. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    Saída esperada:
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * **-g (ou --resource-group)**. Nome do IP público do Olá Olá recurso grupo será criado no.
   * **-n (or --name)**. Nome do IP público hello.
   * **-l (ou --location)**. Região do Azure onde IP público Olá será criado. Para o nosso cenário, *centralus*.
4. Executar Olá **nic de rede do azure criar** comando toocreate uma NIC com um endereço IP privado estático. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    Saída esperada:
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * **- a (ou --private-ip-address)**. Endereço IP privado estático para Olá NIC.
   * **-m (ou --subnet-vnet-name)**. Nome da saudação redes onde Olá NIC será criada.
   * **-k (ou --subnet-name)**. Nome da sub-rede Olá onde Olá NIC será criada.
5. Executar Olá **criar vm do azure** saudação do comando toocreate VM usando o IP público hello e NIC criado acima. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    Saída esperada:
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * **-y (ou --os-type)**. Tipo de operando sistema Olá VM, ou *Windows* ou *Linux*.
   * **-f (ou --nic-name)**. Nome da saudação NIC Olá VM usará.
   * **-i (ou --public-ip-name)**. Nome da saudação IP pública Olá VM usará.
   * **-F (ou --vnet-name)**. Nome da saudação redes onde Olá VM será criado.
   * **-j (ou --vnet-subnet-name)**. Nome da sub-rede Olá onde Olá VM será criado.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como informações de uma VM de endereço de IP privado estático de tooretrieve
tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá após o comando CLI do Azure e observar os valores de saudação para *método de alocação de IP privado* e *endereço IP privado*:

    azure vm show -g TestRG -n DNS01

Saída esperada:

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um particular de endereços IP estáticos de uma VM
Você não pode remover um endereço IP privado estático de uma NIC no CLI do Azure para o Gerenciador de Recursos. Você deve criar uma nova NIC que usa um IP dinâmico, remova Olá NIC anterior de saudação VM e depois adicione toohello NIC Olá nova VM. toochange hello NIC para Olá VM usado int eh comandos acima, siga as etapas de saudação abaixo.

1. Executar Olá **nic de rede do azure criar** comando toocreate uma nova NIC usando a alocação de IP dinâmico. Observe como você não precisa toospecify Olá endereço IP neste momento.
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    Saída esperada:
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. Executar Olá **conjunto de vm do azure** saudação do comando toochange NIC usada por Olá VM.
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    Saída esperada:
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. Se quiser, execute Olá **nic de rede do azure excluir** comando toodelete Olá antigo placa de rede.
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    Saída esperada:
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Como tooadd um endereço IP privado estático endereço tooan existente VM
tooadd um toohello de endereço IP de privado estático NIC usada para a máquina virtual criada usando o script de saudação acima, execute Olá comando a seguir:

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

Saída esperada:

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .
* Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .
* Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

