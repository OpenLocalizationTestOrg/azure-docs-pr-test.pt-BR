---
title: "ambiente de nuvem híbrida aaaSimulated | Microsoft Docs"
description: "Crie um ambiente de nuvem híbrida simulado para testes profissionais de TI ou testes de desenvolvimento, usando duas redes virtuais do Azure e uma conexão Rede Virtual para Rede Virtual."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Configurar um ambiente de nuvem híbrida simulado para testes
Este artigo explica como criar um ambiente simulado de nuvem híbrida com o Microsoft Azure usando duas redes virtuais do Azure. Aqui está a configuração resultante hello.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Isso simula um ambiente de produção de nuvem híbrida e consiste em:

* Uma rede simulada e simplificada local hospedada em uma rede virtual do Azure (rede virtual da saudação TestLab).
* Uma rede virtual simulada entre locais, hospedada no Azure (TestVNET).
* Uma conexão de rede virtual a rede entre redes virtuais Olá dois.
* Um controlador de domínio secundário na rede virtual do hello TestVNET.

Isto proporciona uma base e um ponto de partida comum com os quais é possível:

* Desenvolver e testar aplicativos em um ambiente de nuvem híbrida simulado.
* Crie configurações de teste de computadores, alguns na rede virtual do hello TestLab e alguns na rede virtual Olá TestVNET, toosimulate híbrido baseado em nuvem IT cargas de trabalho.

Há quatro toosetting principais fases esse ambiente de teste de nuvem híbrida:

1. Configure a rede virtual do hello TestLab.
2. Crie rede virtual do hello entre locais.
3. Crie conexão de VPN Olá VNet para VNet.
4. Configurar o DC2. 

Essa configuração exige uma assinatura do Azure. Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Máquinas virtuais e gateways de redes virtuais no Azure geram custos monetários contínuos quando estão em execução. Esse custo é cobrado em sua assinatura paga ou do MSDN. Um gateway de VPN do Azure é implementado como um conjunto de duas máquinas virtuais do Azure. custos de saudação toominimize, criar ambiente de teste de saudação e executar seus testes necessários e a demonstração assim que possível.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Etapa 1: Configurar a rede virtual do hello TestLab
Use instruções Olá Olá [ambiente de teste de configuração de Base](https://technet.microsoft.com/library/mt771177.aspx) tópico tooconfigure Olá DC1, APP1 e CLIENT1 computadores Olá rede virtual do Azure denominado TestLab. 

Em seguida, inicie um prompt do Azure PowerShell.

> [!NOTE]
> Olá conjuntos de comandos a seguir usa o Azure PowerShell 1.0 e posterior.
> 
> 

Entre na conta de tooyour.

    Login-AzureRMAccount

Obter o nome da sua assinatura usando o comando a seguir de saudação.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Defina sua assinatura do Azure. Use Olá a mesma assinatura usada toobuild sua configuração base na fase 1. Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com o nome correto da saudação.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Em seguida, adicione uma gateway sub-rede toohello TestLab rede virtual da sua configuração de base, que será usado toohost Olá gateway do Azure.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Em seguida, solicite um público endereço tooassign toohello gateway IP para rede virtual do hello TestLab.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Depois, crie seu gateway.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Tenha em mente que novos gateways podem levar 20 minutos ou mais toocreate.

Em Olá o portal do Azure em seu computador local, conecte-se tooDC1 com as credenciais de CORP\User1 hello. domínio do tooconfigure Olá CORP para que computadores e usuários usem o seu controlador de domínio local para autenticação, execute esses comandos em um prompt de comando do nível de administrador do Windows PowerShell no DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Etapa 2: Criar rede virtual do hello TestVNET
Primeiro, crie a rede virtual do hello TestVNET e protegê-lo com um grupo de segurança de rede.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

Em seguida, a solicitação um toobe de endereço IP público alocado toohello gateway para a rede virtual do hello TestVNET e criar o gateway.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Etapa 3: Criar conexão Olá VNet para VNet
Primeiro, obtenha uma chave pré-compartilhada aleatória, criptograficamente forte de 32 caracteres do seu administrador de rede ou segurança. Como alternativa, use informações de saudação em [criar uma cadeia de caracteres aleatória para uma chave pré-compartilhada IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain uma chave pré-compartilhada.

Em seguida, use a conexão de rede virtual a rede VPN esses comandos toocreate hello, que pode levar algum tempo toocomplete.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Depois de alguns minutos, a conexão de saudação deve ser estabelecida.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Fase 4: configurar o DC2
Em primeiro lugar, crie uma máquina virtual para DC2. Execute esses comandos no prompt de comando do PowerShell do Azure Olá no computador local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Em seguida, conecte-se a nova máquina de virtual DC2 toohello de saudação portal do Azure.

Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica. Em um prompt de comando com nível de administrador do Windows PowerShell no DC2, execute estes comandos.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 10.0.0.4. Este é um teste de tráfego Olá conexão de rede virtual a rede.

Em seguida, adicione Olá disco de dados extra no DC2 como um novo volume com a letra da unidade Olá f:.

1. No painel esquerdo de saudação do Gerenciador do servidor, clique em **serviços de arquivo e armazenamento**e, em seguida, clique em **discos**.
2. No painel de conteúdo de saudação em Olá **discos** de grupo, clique em **disco 2** (com hello **partição** definido muito**desconhecido**).
3. Clique em **Tarefas** e, em seguida, em **Novo Volume**.
4. Na saudação antes de começar a página do Assistente de novo Volume de saudação, clique em **próximo**.
5. Na página de disco e servidor de saudação selecione hello, clique em **disco 2**e, em seguida, clique em **próximo**. Quando solicitado, clique em **OK**.
6. No hello especificar tamanho de saudação da página de volume hello, clique em **próximo**.
7. Na saudação atribuir tooa unidade pasta ou letra da página, clique em **próximo**.
8. Na página de configurações do sistema do arquivo selecione hello, clique em **próximo**.
9. Na página Olá confirmar seleções, clique em **criar**.
10. Ao concluir, clique em **Fechar**.

Em seguida, configure o DC2 como um controlador de domínio de réplica para o domínio do hello corp.contoso.com. Execute esses comandos no prompt de comando do Windows PowerShell Olá no DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Observe que são solicitada toosupply ambos Olá corp/User1 senha e uma senha de modo de restauração de serviços de diretório (DSRM) e toorestart DC2.

Agora que hello, rede virtual TestVNET tem seu próprio servidor DNS (DC2), você deve configurar Olá TestVNET rede virtual toouse esse servidor DNS.

1. No painel esquerdo de saudação do hello portal do Azure, clique Olá ícone de redes virtuais e, em seguida, clique em **TestVNET**.
2. Em Olá **configurações** , clique em **servidores DNS**.
3. Em **servidor DNS primário**, tipo **192.168.0.4** tooreplace 10.0.0.4.
4. Clique em **Salvar**.

Esta é a configuração atual. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Seu ambiente de nuvem híbrida simulado agora está pronto para testes.

## <a name="next-step"></a>Próxima etapa
* Configure um [aplicativo de linha de negócios baseado na Web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) nesse ambiente.

