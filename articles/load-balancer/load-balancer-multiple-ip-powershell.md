---
title: "aaaLoad balanceamento em várias configurações de IP no Azure | Microsoft Docs"
description: "Balanceamento de carga entre as configurações de IP primárias e secundárias."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>Balanceamento de carga em várias configurações de IP usando o PowerShell

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Este artigo descreve como toouse balanceador de carga do Azure com o IP de vários endereços em uma interface de rede secundária (NIC). Para este cenário, temos duas VMs executando o Windows, cada uma com uma NIC principal e uma secundária. Cada um dos secundários de saudação NICs têm duas configurações de IP. Cada VM hospeda os sites contoso.com e fabrikam.com. Cada site é associado tooone Olá de configurações de IP em uma NIC secundário. Olá Usamos o balanceador de carga do Azure tooexpose dois front-end endereços IP, uma para cada site, toodistribute tráfego toohello respectiva configuração de IP para o site de saudação. Esse cenário usa Olá o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo de tooload etapas em várias configurações de IP

Siga as próximas etapas, Olá cenário de saudação tooachieve descritos neste artigo:

1. Instale o PowerShell do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.
2. Crie um grupo de recursos usando Olá configurações a seguir:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Para saber mais, consulte a Etapa 2 [Criar um grupo de recursos](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Criar um conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain suas VMs. Para este cenário, use Olá comando a seguir:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Siga as instruções as etapas de 3 a 5 [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artigo tooprepare criação de saudação de uma VM com uma única placa de rede. Execute a etapa 6.1 e use o seguinte Olá em vez de etapa 6.2:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Em seguida, conclua as etapas 6.3 a 6.8 [Criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

5. Adicione um segundo tooeach de configuração de IP de saudação VMs. Siga as instruções de saudação em [atribuir vários endereços IP máquinas toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artigo. Use Olá definições de configuração a seguir:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    Não é necessário tooassociate Olá secundário as configurações de IP com IPs públicos para finalidade de saudação deste tutorial. Edite saudação comando tooremove Olá IP associação parte pública.

6. Conclua as etapas 4 a 6 deste artigo novamente para a VM2. Ser tooreplace se Olá VM nome tooVM2 ao fazer isso. Observe que você não precisa toocreate uma rede virtual para Olá segundo VM. Você pode ou não criar uma nova sub-rede com base em seu caso de uso.

7. Crie dois endereços IP públicos e armazená-los em variáveis apropriadas hello, conforme mostrado:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Crie duas configurações de IP de front-end:

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Crie os pools de endereços de back-end, uma investigação e regras de balanceamento de carga:

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Após a criação desses recursos, crie o balanceador de carga:

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Adicione Olá segundo back-end endereço front-end e pool de IP configuration tooyour recém-criado balanceador de carga:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. comandos de saudação abaixo obtém Olá NICs e, em seguida, adicione o que balanceador de carga de ambas as configurações de IP cada secundário NIC toohello back-end do pool de endereços de saudação:

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Por fim, você deve configurar o recurso registros toopoint toohello front-end respectivo endereço IP de DNS Olá balanceador de carga. Você pode hospedar seus domínios no DNS do Azure. Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre como o balanceamento de carga de toocombine serviços no Azure em [usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Saiba como você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de Balanceador de carga no [de análise de Log para o balanceador de carga do Azure](../load-balancer/load-balancer-monitor-log.md).
