---
title: aaaCreate um Azure voltados para Internet carregar balanceador - PowerShell | Microsoft Docs
description: Saiba como toocreate um voltados para Internet balanceador de carga no Gerenciador de recursos usando o PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Criar um balanceador de carga para a Internet no Resource Manager usando o PowerShell

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [Saiba como toocreate um voltados para Internet balanceador de carga usando o modelo de implantação clássico Olá](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Implantação de solução de saudação usando o PowerShell do Azure

Olá procedimentos a seguir explica como toocreate um voltados para Internet balanceador de carga usando o Gerenciador de recursos do Azure com o PowerShell. No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um balanceador de carga.

Você deve criar e configurar Olá objetos toodeploy um balanceador de carga a seguir:

* Configuração de IP de front-end: contém PIPs ( endereços IP públicos) para o tráfego de rede de entrada.
* Pool de endereços de back-end: contém as interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.
* Regras de balanceamento de carga: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá no pool de endereços de back-end de saudação.
* Regras NAT de entrada: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.
* Testes: contém integridade investigações usadas toocheck disponibilidade das instâncias de máquina virtual no pool de endereços de back-end de saudação.

Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configurar o PowerShell toouse Gerenciador de recursos

Verifique se que você tem a versão mais recente de produção saudação do módulo do Azure Resource Manager Olá do PowerShell:

1. Entrar tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    Insira suas credenciais quando solicitado.

2. Verificar as assinaturas de saudação para conta de saudação.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Escolha qual toouse suas assinaturas do Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Crie um grupos de recursos. (Ignore esta etapa se está usando um grupo de recursos existente.)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação

1. Criar uma sub-rede e uma rede virtual.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Criar Azure público recurso de endereço IP, denominado **PublicIP**, toobe usado por um pool IP de front-end com o nome DNS Olá **loadbalancernrp.westus.cloudapp.azure.com**. Olá comando a seguir usa Olá tipo de alocação estática.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > Balanceador de carga de saudação usa o rótulo de domínio de saudação do IP público hello como um prefixo para o FQDN. Isso é diferente do modelo de implantação clássico hello, que usa o serviço de nuvem Olá Olá FQDN do balanceador de carga.
   > Neste exemplo, hello FQDN é **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Criar um pool de IPs de front-end e um pool de endereços de back-end

1. Criar um pool IP de front-end denominado **LB Frontend** que usa Olá **PublicIp** recursos.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Crie um pool de endereços de back-end chamado **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Criar regras NAT, uma regra de balanceador de carga, uma investigação e um balanceador de carga

Este exemplo cria Olá itens a seguir:

* Um tootranslate de regra NAT todas as solicitações de tráfego na porta 3441 tooport 3389
* Um tootranslate de regra NAT todas as solicitações de tráfego na porta 3442 tooport 3389
* Um status de integridade de saudação do teste regra toocheck em uma página chamada **HealthProbe.aspx**
* Um toobalance de regra de Balanceador de carga de todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end Olá
* Um balanceador de carga que usa todos esses objetos

Siga estas etapas:

1. Crie regras NAT de saudação.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Crie um teste de integridade. Há dois tooconfigure de maneiras uma investigação:

    Investigação HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Investigação TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Crie uma regra de balanceador de carga.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Crie balanceador de carga hello usando objetos Olá criado anteriormente.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Criar NICs

Criar interfaces de rede (ou modificar as existentes) e, em seguida, associá-los tooNAT regras, regras de Balanceador de carga e investigações:

1. Obter Olá uma rede virtual e uma sub-rede de rede virtual, onde Olá NICs necessário toobe criado.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Criar uma NIC denominada **lb-nic1 ser**e associá-lo a primeira regra NAT hello e pool de endereços de back-end de primeira (e única) do hello.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Criar uma NIC denominada **lb-nic2 ser**e associá-lo a segunda regra NAT hello e pool de endereços de back-end de primeira (e única) do hello.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Verifique as NICs de saudação.

        $backendnic1

    Saída esperada:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Saudação de uso `Add-AzureRmVMNetworkInterface` cmdlet tooassign Olá NICs toodifferent VMs.

## <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Para obter orientação sobre como criar uma máquina virtual e atribuir uma NIC, confira [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Adicionar balanceador de carga Olá rede interface toohello

1. Recupere o balanceador de carga de saudação do Azure.

    Carregar o recurso de Balanceador de carga de saudação em uma variável (se você ainda não tiver feito isso ainda). variável de saudação é chamado **$lb**. Use Olá mesmo nomes de recurso Olá de Balanceador de carga que você criou anteriormente.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Variável de tooa de configuração de back-end de Olá de carga.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Carregar a interface de rede Olá já criado em uma variável. é o nome da variável Olá **$nic**. Olá nome da interface de rede é Olá mesmo da saudação exemplo anterior.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Alterar configuração de back-end de saudação na interface de rede de saudação.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Salve o objeto de interface de rede de saudação.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Depois que uma interface de rede é adicionada toohello pool de back-end do balanceador de carga, ele começa a receber o tráfego de rede com base em regras de balanceamento de carga Olá para esse recurso de Balanceador de carga.

## <a name="update-an-existing-load-balancer"></a>Atualizar um balanceador de carga existente

1. Usando Olá de Balanceador de carga Olá exemplo anterior, atribua uma variável de toohello de objeto de Balanceador de carga **$slb** usando `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. Saudação de exemplo a seguir, você adiciona uma regra NAT de entrada – usando a porta 81 no pool de front-end hello e 8181 a porta para o pool de back-end hello – tooan balanceador de carga existente.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Salvar a nova configuração de saudação usando `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Remover um balanceador de carga

Use o comando Olá `Remove-AzureLoadBalancer` toodelete um balanceador de carga criado anteriormente denominado **NRP LB** em um grupo de recursos chamado **NRP RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Você pode usar a opção Olá **-Force** tooavoid prompt de saudação para exclusão.

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
