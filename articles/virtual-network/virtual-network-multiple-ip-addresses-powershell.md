---
title: "aaaMultiple endereços IP para máquinas virtuais do Azure - PowerShell | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa virtual máquina usando o PowerShell | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Atribuir vários endereços IP máquinas toovirtual usando o PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artigo explica como toocreate uma máquina virtual (VM) por meio da implantação do Azure Resource Manager Olá modelo usando o PowerShell. Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP. toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Criar uma VM com vários endereços IP

etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação. Altere os valores da variável conforme exigido por sua implementação.

1. Abra um prompt de comando do PowerShell e as etapas de saudação completa restantes nesta seção dentro de uma única sessão do PowerShell. Se você ainda não tiver o PowerShell instalado e configurado, Olá concluir etapas no hello [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Conta de logon do tooyour com hello `login-azurermaccount` comando.
3. Substitua *myResourceGroup* e *westus* por um nome e local de sua escolha. Crie um grupos de recursos. Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Criar uma rede virtual (VNet) e a sub-rede no hello mesmo local que o grupo de recursos de saudação:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Crie um NSG (grupo de segurança de rede) e uma regra. Olá NSG protege Olá VM usando regras de entrada e saídas. Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Definir a configuração de IP primária Olá para Olá NIC. Alteração 10.0.0.4 tooa válido na sub-rede Olá criado, se você não usou o valor de saudação definido anteriormente. Antes de atribuir um endereço IP estático, é recomendável que você primeiro confirme que ele ainda não está em uso. Digite o comando Olá `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Se o endereço Olá estiver disponível, Olá saída retorna *True*. Se não estiver disponível, Olá saída retorna *False* e uma lista de endereços que estão disponíveis. 

    Em Olá comandos a seguir **substitua < substituir-com-seu-exclusivo-name > toouse de nome DNS exclusivo hello.** nome da saudação deve ser exclusivo entre todos os endereços IP públicos em uma região do Azure. Este é um parâmetro opcional. Ele pode ser removido se você quiser apenas tooconnect toohello VM usando o endereço IP público de saudação.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Quando você atribui vários tooa de configurações de IP NIC, uma configuração deve ser atribuída como Olá *-primário*.

    > [!NOTE]
    > Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.

7. Definir as configurações de IP secundárias Olá para Olá NIC. Você pode adicionar, remover ou alterar as configurações conforme necessário. Cada configuração de IP deve ter um endereço IP privado atribuído. Cada configuração pode, opcionalmente, ter um endereço IP público atribuído.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Criar hello NIC e associar Olá três tooit de configurações de IP:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Embora todas as configurações são atribuídas tooone NIC neste artigo, você pode atribuir várias IP configurações tooevery NIC conectada toohello VM. toolearn como toocreate uma VM com várias NICs, ler Olá [criar uma VM com várias NICs](virtual-network-deploy-multinic-arm-ps.md) artigo.

9. Crie hello VM inserindo Olá comandos a seguir:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

## <a name="add"></a>Adicionar endereços IP tooa VM

Você pode adicionar pública e privada tooa de endereços IP NIC completando as etapas de saudação que seguem. Olá exemplos Olá seções a seguir pressupõem que você já tem uma máquina virtual com configurações de IP hello três descritas em hello [cenário](#Scenario) neste artigo, mas ele não é necessário que você faça.

1. Abra um prompt de comando do PowerShell e as etapas de saudação completa restantes nesta seção dentro de uma única sessão do PowerShell. Se você ainda não tiver o PowerShell instalado e configurado, Olá concluir etapas no hello [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Alterar hello "valores" dos Olá após $Variables toohello nome da saudação NIC que você deseja tooadd IP endereço tooand Olá recurso grupo e local Olá em que NIC existe:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Se você não souber o nome de saudação do hello NIC que você deseja toochange, digite Olá comandos a seguir, altere os valores hello variáveis anteriores hello:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Crie uma variável e defina-a como toohello existente NIC digitando Olá comando a seguir:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Olá comandos a seguir, alterar *MyVNet* e *MySubnet* toohello nomes de Olá Olá rede virtual e sub-rede NIC está conectada ao. Digite hello comandos tooretrieve Olá rede virtual e sub-rede objetos Olá A que NIC está conectada:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Se você não souber Olá redes ou sub-redes nome hello que NIC está conectada ao, digite Olá comando a seguir:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Na saída de hello, procure texto toohello semelhante a saída de exemplo a seguir:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    Na saída, *MyVnet* é hello VNet e *MySubnet* é Olá sub-rede hello NIC está conectada ao.

5. Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:

    **Adicionar um endereço IP privado**

    tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP. Olá comando a seguir cria uma configuração com um endereço IP estático de 10.0.0.7. Ao especificar um endereço IP estático, ele deve ser um endereço não usado para a sub-rede de saudação. É recomendável que você primeiro teste Olá endereço tooensure está disponível digitando Olá `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando. Se o endereço IP hello estiver disponível, Olá saída retorna *True*. Se não estiver disponível, Olá saída retorna *False*e uma lista de endereços que estão disponíveis.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).

    Adicionar Olá privada IP endereço toohello VM sistema operacional concluindo as etapas de saudação para seu sistema operacional no hello [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.

    **Adicionar um endereço IP público**

    Um endereço IP público é adicionado ao associar um tooeither de recurso de endereço IP público, uma nova configuração de IP ou uma configuração de IP existente. Conclua as etapas de saudação em uma saudação próximas seções, você precisa.

    > [!NOTE]
    > Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.
    >

    - **Associar Olá pública recurso tooa novo IP configuração de endereço IP**
    
        Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado. Você pode adicionar um recurso de endereço IP público existente ou criar um novo. toocreate uma nova, digite Olá comando a seguir:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIp3* IP público recurso de endereço, digite Olá comando a seguir:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Associar Olá pública recurso tooan existente IP configuração de endereço IP**

        Um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado. Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Consulte o seguinte de toohello semelhante de saída:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Desde Olá **PublicIpAddress** coluna para *IpConfig 3* está em branco, nenhum recurso de endereço IP público é tooit atualmente associado. Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IpConfig*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Defina Olá NIC com a nova configuração de IP hello inserindo Olá comando a seguir:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Exibir endereços IP privados de saudação e Olá pública IP endereço recursos atribuído toohello NIC inserindo Olá o comando a seguir:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Adicionar Olá privada IP endereço toohello VM sistema operacional concluindo as etapas de saudação para seu sistema operacional no hello [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereço toohello sistema operacional.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
