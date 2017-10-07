---
title: "aaaCreate uma VM (clássico) com várias placas de rede usando o PowerShell | Microsoft Docs"
description: "Saiba como toocreate e configurar máquinas virtuais com várias placas de rede usando o PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Criar uma VM (Clássica) com diversas NICs
Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais. Várias NICs são um requisito para muitos aplicativos virtuais de rede, como soluções de distribuição de aplicativos e de otimização de WAN. Várias NICs também fornecem isolamento do tráfego entre NICs.

![Várias NICs da VM](./media/virtual-networks-multiple-nics/IC757773.png)

Olá figura mostra uma VM com três NICs, cada um conectado tooa outra sub-rede.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que a maioria das implantações novas use o Gerenciador de Recursos.

* Só há suporte para o VIP da Internet (implantações clássicas) em uma NIC hello "padrão". Há apenas um VIP toohello IP da NIC saudação padrão.
* Neste momento, não há suporte para endereços LPIP (PI público no nível da instância) (implantações clássicas) para VMs com várias NICs.
* Olá a ordem das NICs de saudação do dentro Olá VM será aleatória e também pode mudar entre atualizações de infraestrutura do Azure. No entanto, Olá endereços IP e Olá correspondente ethernet MAC permanecerão endereços Olá mesmo. Por exemplo, suponha que **Eth1** tem o endereço IP 10.1.0.100 e o endereço MAC 00-0D-3A-B0-39-0D; após uma atualização de infraestrutura do Azure e a reinicialização, ela pode ser alterada muito**Eth2**, mas Olá IP e MAC emparelhamento será permanecem Olá mesmo. Quando uma reinicialização for iniciada pelo cliente, Olá ordem da NIC permanecerá Olá mesmo.
* Olá endereço para cada NIC em cada VM deve estar localizado em uma sub-rede, várias NICs em uma única VM pode cada ter Olá de endereços que estão na mesma sub-rede.
* Olá tamanho da VM determina o número de saudação de NICS que você pode criar para uma máquina virtual. Saudação de referência [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tamanhos de VM toodetermine artigos de quantos NICS dá suporte a cada tamanho VM. 

## <a name="network-security-groups-nsgs"></a>Grupos de segurança de rede (NSG)
Em uma implantação do Gerenciador de recursos, qualquer NIC em uma máquina virtual pode estar associada com um NSG (grupo de segurança de rede), incluindo todas as NICs em uma VM que tenha várias NICs habilitadas. Se uma NIC é atribuída um endereço de sub-rede onde a sub-rede de saudação é associada um NSG, em seguida, hello regras NSG da sub-rede Olá também se aplicam NIC toothat. Em sub-redes tooassociating de adição com NSGs, você também pode associar uma NIC com um NSG.

Se uma sub-rede é associada a um NSG e uma NIC dentro dessa sub-rede individualmente associada a um NSG, Olá associado NSG regras são aplicadas em **fluxo ordem** toohello direção do tráfego de saudação sendo passado dentro ou fora de acordo com Olá NIC:

* **Tráfego de entrada** cujo destino é hello NIC em questão flui do primeiro sub-rede hello, disparar regras NSG da sub-rede hello, antes de passar para Olá NIC e disparar regras NSG de saudação do NIC.
* **Tráfego de saída** cuja origem é hello NIC em questão flui primeiro a sair de saudação NIC, disparar regras NSG da NIC hello, antes de passar por sub-rede hello e disparar regras do NSG da sub-rede hello.

Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como elas são aplicadas com base nas associações toosubnets, VMs e NICs.

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Como tooConfigure uma várias VMs de NIC em uma implantação clássica
instruções de saudação abaixo ajudará você a criar uma várias VMs de NIC contendo 3 NICs: uma NIC padrão e duas NICs adicionais. etapas de configuração de saudação criará uma VM que será configurada de acordo com o fragmento configuração de arquivo do serviço toohello abaixo:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Você precisa de saudação pré-requisitos a seguir antes de tentar toorun Olá comandos do PowerShell exemplo hello.

* Uma assinatura do Azure.
* Uma rede virtual configurada. Confira a [Visão geral da Rede Virtual](virtual-networks-overview.md) para saber mais sobre VNets.
* versão mais recente de saudação do Azure PowerShell baixada e instalada. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

toocreate uma VM com várias NICs, Olá concluir etapas a seguir, inserindo cada comando em uma única sessão do PowerShell:

1. Selecione uma imagem de VM na galeria de imagens de VMs do Azure. Observe que as imagens são alteradas frequentemente e estão disponíveis por região. Olá imagem especificada no exemplo hello abaixo pode alterar ou pode não estar em sua região, portanto, imagem Olá toospecify que você precisa.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Crie a configuração da VM.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Crie logon de administrador saudação padrão.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Adicione configuração da VM toohello NICs adicional.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Especifique uma sub-rede de saudação e endereço IP para a NIC saudação padrão.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Crie hello VM em sua rede virtual.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Olá VNet que você especificar aqui já deve existir (conforme mencionado nos pré-requisitos Olá). exemplo Hello abaixo especifica uma rede virtual denominada **MultiNIC-VNet**.
    >

## <a name="limitations"></a>Limitações
Olá limitações a seguir é aplicável ao usar várias NICs:

* VMs com várias NICs devem ser criadas nas redes virtuais do Azure (VNets). As VMs que não sejam Redes Virtuais não podem ser configuradas com várias NICs.
* Todas as VMs em um disponibilidade definido necessidade toouse várias NICs ou uma única placa de rede. Não é possível haver uma combinação de VMs com várias NICs e VMs com uma única NIC em um conjunto de disponibilidade. As mesmas regras se aplicam a VMs em um serviço de nuvem. Para várias VMs de NIC, eles não são necessários toohave Olá mesmo número de NICs, desde que cada um deles tem pelo menos dois.
* Uma VM com uma única NIC não pode ser configurada com várias NICs (e vice-versa) depois de implantada, sem sua exclusão e recriação.

## <a name="secondary-nics-access-tooother-subnets"></a>Secundário NICs acesso tooother sub-redes
Por padrão NICs secundárias não serão configuradas com um gateway padrão, devido o fluxo de tráfego de saudação toowhich em Olá NICs secundárias será limitado toobe dentro Olá mesma sub-rede. Se quiserem que os usuários de saudação tooenable secundário NICs tootalk fora da sua própria sub-rede, será necessário tooadd uma entrada na Olá tabela tooconfigure Olá gateway de roteamento como descrita abaixo.

> [!NOTE]
> VMs criadas antes de julho de 2015 poderão ter um gateway padrão configurado para todas as NICs. gateway padrão Olá NICs secundárias não será removido até que essas VMs são reiniciados. Em sistemas operacionais que usam o modelo roteamento de saudação host fraco, como o Linux, a conectividade com a Internet pode quebrar se o tráfego de entrada e saída hello usar NICs diferentes.
> 

### <a name="configure-windows-vms"></a>Configurar máquinas virtuais do Windows
Suponha que você tenha uma VM do Windows com duas NICs da seguinte maneira:

* Endereço IP primário da NIC: 192.168.1.4
* Endereço IP secundário da NIC: 192.168.2.5

tabela de rotas do IPv4 Olá para essa VM deve ter esta aparência:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Observe a que rota padrão (0.0.0.0) hello está apenas disponível toohello principal placa de rede. Você não será capaz de tooaccess recursos fora da sub-rede Olá Olá secundário NIC, conforme mostrado abaixo:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd uma rota padrão em Olá NIC secundário, siga Olá etapas abaixo:

1. Em um prompt de comando, execute o comando de saudação abaixo tooidentify Olá número de índice para Olá NIC secundário:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Observe que a segunda entrada hello na tabela hello, com um índice de 27 (no exemplo).
3. Saudação prompt de comando, execute Olá **Adicionar rota** comando conforme mostrado abaixo. Neste exemplo, você está especificando 192.168.2.1 como gateway padrão Olá Olá NIC secundário:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. conectividade de tootest voltar toohello prompt de comando e tente tooping uma sub-rede diferente do hello NIC secundário como int mostrado eh exemplo abaixo:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Você também pode verificar que a saudação de toocheck de tabela de rota recém-adicionado rota, conforme mostrado abaixo:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Configurar máquinas virtuais Linux
Para VMs do Linux, como o comportamento padrão de saudação usa host fraco roteamento, recomendamos que Olá secundárias NICs são fluxos de tootraffic restrito apenas em Olá mesma sub-rede. No entanto, se determinados cenários exigem conectividade fora da sub-rede hello, os usuários devem habilitar tooensure de roteamento baseado em política que Olá ingresso e usos de tráfego de saída Olá NIC mesmo.

## <a name="next-steps"></a>Próximas etapas
* Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação do Gerenciador de Recursos](virtual-network-deploy-multinic-arm-template.md).
* Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação clássica](virtual-network-deploy-multinic-classic-ps.md).

