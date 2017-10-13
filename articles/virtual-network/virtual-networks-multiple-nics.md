---
title: "Criar uma VM (Clássica) com diversas NICs usando o PowerShell | Microsoft Docs"
description: "Saiba como criar e configurar VMs com várias NICs usando PowerShell."
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
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Criar uma VM (Clássica) com diversas NICs
Você pode criar máquinas virtuais (VMs) no Azure e anexar várias interfaces de rede (NICs) para cada uma de suas VMs. Várias NICs são um requisito para muitos aplicativos virtuais de rede, como soluções de distribuição de aplicativos e de otimização de WAN. Várias NICs também fornecem isolamento do tráfego entre NICs.

![Várias NICs da VM](./media/virtual-networks-multiple-nics/IC757773.png)

A figura mostra uma VM com três NICs, cada uma conectada a uma sub-rede diferente.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda o uso do modelo de implantação clássica. A Microsoft recomenda que a maioria das implantações novas use o Gerenciador de Recursos.

* VIP da Internet (implantações clássicas) têm suporte apenas na NIC "padrão". Há apenas um VIP para o IP da NIC padrão.
* Neste momento, não há suporte para endereços LPIP (PI público no nível da instância) (implantações clássicas) para VMs com várias NICs.
* A ordem das NICs de dentro da VM será aleatória e também pode ser alterada nas atualizações da infraestrutura do Azure. No entanto, os endereços IP e os endereços ethernet MAC correspondentes permanecerão os mesmos. Por exemplo, suponha que **Eth1** tenha o endereço IP 10.1.0.100 e um endereço MAC 00-0D-3A-B0-39-0D; após uma atualização de infraestrutura e reinicialização do Azure, ela pode ser alterada para **Eth2**, mas o emparelhamento entre IP e MAC permanecerá o mesmo. Quando a reinicialização for iniciada pelo cliente, a ordem das NICs permanecerá a mesma.
* O endereço de cada NIC em cada máquina virtual deve estar localizado em uma sub-rede, várias NICs em uma única VM podem, cada uma, receber a atribuição de endereços que estejam na mesma sub-rede.
* O tamanho da VM determina o número de NICS que você pode criar para uma máquina virtual. Consulte os artigos sobre tamanhos de VM do[Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e do [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para determinar a quantas NICS cada tamanho de VM oferece suporte. 

## <a name="network-security-groups-nsgs"></a>Grupos de segurança de rede (NSG)
Em uma implantação do Gerenciador de recursos, qualquer NIC em uma máquina virtual pode estar associada com um NSG (grupo de segurança de rede), incluindo todas as NICs em uma VM que tenha várias NICs habilitadas. Se uma NIC tiver um endereço atribuído em uma sub-rede que esteja associada a um NSG, as regras do NSG da sub-rede também se aplicarão à NIC. Além de associar sub-redes a NSGs, você também pode associar uma NIC a um NSG.

Se uma sub-rede for associada a um NSG e uma NIC dessa sub-rede for associada individualmente a um NSG, as regras do NSG associado serão aplicadas na **ordem de fluxo** de acordo com a direção do tráfego que estiver sendo passado para dentro ou para fora da NIC:

* **tráfego de entrada** cujo destino é a NIC em questão flui primeiro pela sub-rede, disparando as regras do NSG da sub-rede, antes de passar pela NIC, quando serão acionadas as regras do NSG da NIC.
* **tráfego de saída** cujo destino é a NIC em questão flui primeiro para fora da sub-rede, acionando as regras do NSG da NIC, antes de passar pela sub-rede, quando serão acionadas as regras do NSG da sub-rede.

Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como elas são aplicados com base nas associações a sub-redes, VMs e NICs.

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a>Como configurar uma VM de várias NICs em uma implantação clássica
As instruções a seguir o ajudarão a criar uma VM de várias NICs contendo 3 NICs: uma NIC padrão e duas NICs adicionais. As etapas da configuração criarão uma VM que será configurada de acordo com o fragmento do arquivo de configuração de serviços abaixo:

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
    … Skip over the remainder section …
    </VirtualNetworkSite>


É necessário ter os pré-requisitos a seguir antes de tentar executar os comandos do PowerShell no exemplo.

* Uma assinatura do Azure.
* Uma rede virtual configurada. Confira a [Visão geral da Rede Virtual](virtual-networks-overview.md) para saber mais sobre VNets.
* A versão mais recente do Azure PowerShell baixada e instalada. Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).

Para criar uma VM com várias NICs, conclua as etapas a seguir, inserindo cada comando em uma única sessão do PowerShell:

1. Selecione uma imagem de VM na galeria de imagens de VMs do Azure. Observe que as imagens são alteradas frequentemente e estão disponíveis por região. A imagem especificada no exemplo a seguir pode ser alterada ou pode não ser da sua região, portanto certifique-se de especificar a imagem correta.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Crie a configuração da VM.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Crie o logon de administrador padrão.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Adicione outras NICs à configuração da VM.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Especifique a sub-rede e o endereço IP da NIC padrão.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Crie a VM na sua rede virtual.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > A VNet que você especificar aqui já deve existir (conforme mencionado nos pré-requisitos). O exemplo a seguir especifica uma rede virtual chamada **MultiNIC-VNet**.
    >

## <a name="limitations"></a>Limitações
As seguintes limitações são aplicáveis ao usar várias NICs:

* VMs com várias NICs devem ser criadas nas redes virtuais do Azure (VNets). As VMs que não sejam Redes Virtuais não podem ser configuradas com várias NICs.
* Todas as VMs em um conjunto de disponibilidade precisam usar várias NICs ou uma única NIC. Não é possível haver uma combinação de VMs com várias NICs e VMs com uma única NIC em um conjunto de disponibilidade. As mesmas regras se aplicam a VMs em um serviço de nuvem. Para VMs de várias NICs, não é necessário ter o mesmo número de NICs, desde que cada uma delas tenha pelo menos duas.
* Uma VM com uma única NIC não pode ser configurada com várias NICs (e vice-versa) depois de implantada, sem sua exclusão e recriação.

## <a name="secondary-nics-access-to-other-subnets"></a>Acesso a NICs secundárias a outras sub-redes
Por padrão, as NICs secundárias não serão configuradas com um gateway padrão e, devido a isso, o fluxo de tráfego nas NICs secundárias será limitado à mesma sub-rede. Se os usuários desejarem habilitar NICs secundárias para falar fora de suas próprias sub-redes, precisarão adicionar uma entrada à tabela de roteamento para configurar o gateway, conforme descrito abaixo.

> [!NOTE]
> VMs criadas antes de julho de 2015 poderão ter um gateway padrão configurado para todas as NICs. O gateway padrão para NICs secundárias não será removido até que essas VMs sejam reinicializadas. Em sistemas operacionais que usam o modelo de roteamento de host fraco, como o Linux, a conectividade da Internet poderá ser interrompida se o tráfego de entrada e de saída usarem NICs diferentes.
> 

### <a name="configure-windows-vms"></a>Configurar máquinas virtuais do Windows
Suponha que você tenha uma VM do Windows com duas NICs da seguinte maneira:

* Endereço IP primário da NIC: 192.168.1.4
* Endereço IP secundário da NIC: 192.168.2.5

A tabela de rotas do IPv4 para essa VM ficaria assim:

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

Observe que a rota padrão (0.0.0.0) só está disponível para a NIC primária. Você não conseguirá acessar recursos fora da sub-rede para a NIC secundária, conforme mostrado abaixo:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

Para adicionar uma rota padrão à NIC secundária, siga as etapas abaixo:

1. Em um prompt de comando, execute o comando a seguir para identificar o número de índice para a NIC secundária:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Observe a segunda entrada na tabela, com um índice de 27 (no exemplo).
3. No prompt de comando, execute o comando **route add** conforme mostrado abaixo. Neste exemplo, você está especificando 192.168.2.1 como o gateway padrão para a NIC secundária:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. Para testar a conectividade, volte ao prompt de comando e tente executar o ping em uma sub-rede diferente da NIC secundária, como int eh, mostrado no exemplo a seguir:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Você também pode conferir a sua tabela de rotas para verificar a rota recém-adicionada, conforme mostrado abaixo:
   
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
Para VMs do Linux, como o comportamento padrão usa roteamento de host fraco, recomendamos que as NICs secundárias sejam restritas a fluxos de tráfego somente dentro da mesma sub-rede. No entanto, se determinados cenários exigirem conectividade fora da sub-rede, os usuários devem habilitar a política com base em roteamento para garantir que o tráfego de entrada e saída use a mesma NIC.

## <a name="next-steps"></a>Próximas etapas
* Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação do Gerenciador de Recursos](virtual-network-deploy-multinic-arm-template.md).
* Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação clássica](virtual-network-deploy-multinic-classic-ps.md).

