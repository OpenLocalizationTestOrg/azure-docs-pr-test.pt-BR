---
title: aaaCreate interno do Azure carregar balanceador - PowerShell | Microsoft Docs
description: Saiba como o toocreate um interno balanceador usando o PowerShell no Gerenciador de recursos de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Criar um balanceador de carga interno usando o PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Olá etapas a seguir explica como toocreate um interno carregar balanceador usando o Gerenciador de recursos do Azure com o PowerShell. No Gerenciador de recursos do Azure, Olá itens toocreate um balanceador de carga interno são configuradas individualmente e, em seguida, combinados toocreate um balanceador de carga.

Você precisa toocreate e configurar Olá objetos toodeploy um balanceador de carga a seguir:

* Configuração de IP de final de front - irá configurar o endereço IP privado de saudação para tráfego de rede
* Pool de endereços de back-end - irá configurar interfaces de rede de saudação que irá receber o tráfego de balanceamento de carga hello proveniente do pool IP de front-end
* Regras de balanceamento de carga - fonte e a configuração de porta local para Olá balanceador de carga.
* Testes - configura a investigação de status de integridade Olá para instâncias de máquina Virtual de saudação.
* Regras NAT de entrada - configura o acesso toodirectly de regras de porta de saudação uma das instâncias de máquina Virtual de saudação.

É possível obter mais informações sobre componentes do balanceador de carga com o gerenciador de recursos do Azure em [Suporte do Gerenciador de Recursos do Azure para balanceador de carga](load-balancer-arm.md).

Olá etapas a seguir explicam como tooconfigure um balanceador de carga entre duas máquinas virtuais.

## <a name="setup-powershell-toouse-resource-manager"></a>Instalação do PowerShell toouse Gerenciador de recursos

Verifique se você possui hello, a última versão de produção do hello módulo do Azure para o PowerShell e ter PowerShell instalação tooaccess corretamente sua assinatura do Azure.

### <a name="step-1"></a>Etapa 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Etapa 2

Verificar as assinaturas de saudação conta Olá

```powershell
Get-AzureRmSubscription
```

Será solicitada tooAuthenticate com suas credenciais.

### <a name="step-3"></a>Etapa 3

Escolha qual toouse suas assinaturas do Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Criar grupo de recursos para o balanceador de carga

Crie um grupo de recursos (pule esta etapa se você estiver usando um grupo de recursos existente)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Isso é usado como o local padrão de saudação para recursos desse grupo de recursos. Verifique se todos os comandos toocreate um balanceador de carga usará Olá mesmo grupo de recursos.

Em Olá exemplo acima é criado um grupo de recursos chamado "NRP-RG" e o local "Oeste US".

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Crie a Rede virtual e um endereço IP privado para o pool de IP front-end

Cria uma sub-rede da rede virtual hello e atribui toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Criar uma rede virtual:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Criar rede virtual hello e adiciona Olá sub-rede toohello lb sub-rede ser virtual rede NRPVNet e atribui toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Criar o pool de IP front-end e pool de endereços de back-end

Configurar um pool IP de front-end para entrada de saudação carregar o tráfego de rede do balanceador e tráfego de balanceamento de carga do back-end endereço pool tooreceive Olá.

### <a name="step-1"></a>Etapa 1

Crie um pool IP de front-end usando o endereço IP privado Olá 10.0.2.5 para Olá sub-rede 10.0.2.0/24 que será endpoint de tráfego de rede de entrada Olá.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Etapa 2

Configurar um pool de endereços de back-end usado tooreceive o tráfego de entrada de pool de IP de front-end:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Criar regras de balanceamento de carga, regras de NAT, teste e balanceador de carga

Depois de criar o pool IP de front-end hello e pool de endereços de back-end Olá, você precisará de regras de saudação toocreate que pertencem o recurso de Balanceador de carga toohello:

### <a name="step-1"></a>Etapa 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

exemplo Hello acima está criando Olá itens a seguir:

* Regra NAT que todo tráfego tooport 3441 irá tooport 3389.
* uma segunda regra NAT que todo tráfego tooport 3442 irá tooport 3389.
* uma regra de Balanceador de carga que será carregado equilibrar todo o tráfego de entrada na porta 80 do toolocal porta pública 80 no pool de endereços de back-end de saudação.
* uma regra de teste que irá verificar o status de integridade de saudação de caminho "HealthProbe.aspx"

### <a name="step-2"></a>Etapa 2

Crie o balanceador de carga Olá somar todos os objetos (regras NAT, regras de Balanceador de carga, configurações de teste):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Criar interfaces de rede

Depois de criar o balanceador de carga interno hello, você precisa definir quais interfaces de rede receberá Olá com balanceamento de carga tráfego de rede, as regras de NAT e investigação. interface de rede Olá nesse caso é configurada individualmente e pode ter tooa VM mais tarde.

### <a name="step-1"></a>Etapa 1

Obter recurso Olá interfaces de rede virtuais de toocreate de rede e sub-rede:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Essa etapa cria uma interface de rede que pertencem a toohello pool de back-end do balanceador de carga e associar a primeira regra NAT Olá para RDP para essa interface de rede:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Etapa 2

Criar uma segunda chamada de interface de rede chamada LB-Nic2-BE:

Essa etapa cria uma segunda interface de rede, atribuindo toohello mesmo balanceador de carga novamente terminar pool e associar a segunda regra NAT Olá criado para RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

resultado final de saudação mostrará o seguinte hello:

    $backendnic1

Saída esperada:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Etapa 3

Use Olá comando Add-AzureRmVMNetworkInterface tooassign Olá NIC tooa máquina virtual.

Você pode encontrar hello instruções passo a passo toocreate uma máquina virtual e atribua tooa NIC documentação Olá a seguir: [criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Adicionar a interface de rede Olá

Se você já tiver uma máquina virtual criada, você pode adicionar a interface de rede de saudação com Olá etapas a seguir:

### <a name="step-1"></a>Etapa 1

Carregar o recurso de Balanceador de carga de saudação em uma variável (se você ainda não tiver feito isso ainda). variável Olá usado é chamado $lb e use Olá mesmos nomes de recurso de Balanceador de carga Olá criados acima.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Etapa 2

Variável de tooa de configuração de back-end de saudação de carga.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Etapa 3

Carregar a interface de rede Olá já criado em uma variável. nome da variável Olá usado é NIC $. nome de interface de rede Olá usado Olá mesmo do exemplo hello acima.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Etapa 4

Alterar configuração de back-end de saudação na interface de rede de saudação.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Etapa 5

Salve o objeto de interface de rede de saudação.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Depois que uma interface de rede é adicionada toohello pool de back-end do balanceador de carga, ele começa a receber o tráfego de rede com base em regras para esse recurso de Balanceador de carga de balanceamento de carga de saudação.

## <a name="update-an-existing-load-balancer"></a>Atualizar um balanceador de carga existente

### <a name="step-1"></a>Etapa 1
Usar o balanceador de carga de saudação do exemplo hello acima, atribuir toovariable de objeto do balanceador de carga $slb usando Get-AzureRmLoadBalancer

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Etapa 2

Em Olá exemplo a seguir, você adicionará uma nova regra de NAT de entrada usando a porta 81 no front-end hello e porta 8181 volta Olá terminar balanceador de carga existente do pool tooan

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Etapa 3

Salve Olá nova configuração usando Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Remover um balanceador de carga

Use Olá comando Remove-AzureRmLoadBalancer toodelete um balanceador de carga criado anteriormente denominado "NRP LB" em um grupo de recursos chamado "RG NRP"

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Você pode usar o hello opcional alternar - Force tooavoid Olá Solicitar exclusão.

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
