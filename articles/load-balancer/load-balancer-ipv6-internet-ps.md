---
title: "Balanceador de carga aaaCreate um Azure voltados à Internet com o IPv6 - PowerShell | Microsoft Docs"
description: "Saiba como toocreate um voltados à Internet carregar balanceador com IPv6 usando o PowerShell para o Gerenciador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a>Introdução à criação de um balanceador de carga para a Internet com IPv6 usando o PowerShell para Resource Manager

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI do Azure](load-balancer-ipv6-internet-cli.md)
> * [Modelo](load-balancer-ipv6-internet-template.md)

Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP). o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga. O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.

## <a name="example-deployment-scenario"></a>Exemplo de cenário de implantação

Olá diagrama a seguir ilustra Olá solução balanceamento de carga que está sendo implantada neste artigo.

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

Nesse cenário, você criará hello Azure recursos a seguir:

* um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6
* dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos de extremidade públicos
* um conjunto de disponibilidade toothat contém Olá duas VMs
* duas VMs (máquinas virtuais)
* uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a>Implantar solução hello usando hello Azure PowerShell

Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com o PowerShell. No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente, em seguida, juntar toocreate um recurso.

toodeploy um balanceador de carga, que você crie e configure Olá seguintes objetos:

* Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.
* Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.
* Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.
* Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.
* Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.

Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configurar o PowerShell toouse Gerenciador de recursos

Verifique se que você tem a versão mais recente de produção saudação do módulo do Azure Resource Manager Olá para o PowerShell.

1. Entrar no Azure

    ```powershell
    Login-AzureRmAccount
    ```

    Insira suas credenciais quando solicitado.

2. Verificar as assinaturas de saudação conta Olá

    ```powershell
    Get-AzureRmSubscription
    ```

3. Escolha qual toouse suas assinaturas do Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Crie um grupo de recursos (pule esta etapa se você estiver usando um grupo de recursos existente)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação

1. Criar uma rede virtual com uma sub-rede.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Crie endereço IP público do Azure recursos (PIP) para o pool de endereços IP front-end hello.

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > Balanceador de carga de saudação usa o rótulo de domínio de saudação do IP público hello como prefixo para o FQDN. Neste exemplo, Olá FQDNs são *lbnrpipv4.westus.cloudapp.azure.com* e *lbnrpipv6.westus.cloudapp.azure.com*.

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a>Criar configurações de IP de front-end e um pool de endereços de back-end

1. Crie configuração de endereço front-end que usa endereços IP públicos de saudação criado por você.

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. Crie um pool de endereços de back-end.

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a>Criar regras de LB, regras NAT, um teste e um balanceador de carga

Este exemplo cria Olá itens a seguir:

* regra de NAT tootranslate todo o tráfego de entrada na porta 443 tooport 4443
* um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.
* uma carga balanceador regra tooallow RDP conexão toohello VMs na porta 3389.
* um status de integridade de saudação do teste regra toocheck em uma página chamada *HealthProbe.aspx* ou um serviço na porta 8080
* um balanceador de carga que usa todos esses objetos

1. Crie regras NAT de saudação.

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. Crie um teste de integridade. Há dois tooconfigure de maneiras uma investigação:

    Investigação HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    ou Investigação TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Neste exemplo, vamos toouse Olá que sondas de TCP.

3. Crie uma regra de balanceador de carga.

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. Crie o balanceador de carga hello usando objetos Olá criado anteriormente.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a>Criar NICs para Olá VMs de back-end

1. Obter Olá rede Virtual e a sub-rede de rede Virtual, onde Olá NICs necessário toobe criado.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Crie NICs e as configurações de IP para VMs de saudação.

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a>Criar máquinas virtuais e atribuir Olá recém-criado NICs

Para obter mais informações sobre como criar uma VM, consulte [Criar e pré-configurar uma máquina virtual do Windows com o Gerenciador de Recursos e o Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Criar um conjunto de disponibilidade e a conta de armazenamento

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. Criar cada VM e atribuir Olá anterior criada NICs

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
