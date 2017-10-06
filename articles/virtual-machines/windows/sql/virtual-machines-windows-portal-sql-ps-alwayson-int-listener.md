---
title: "aaaConfigure sempre em ouvintes de disponibilidade – Microsoft Azure | Microsoft Docs"
description: "Configure os ouvintes de grupo de disponibilidade no modelo do Azure Resource Manager hello, usando um balanceador de carga interno com um ou mais endereços IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Configurar um ou mais ouvintes de grupo de disponibilidade AlwaysOn – Resource Manager
Este tópico mostra como:

* Criar um balanceador de carga interno para grupos de disponibilidade do SQL Server usando cmdlets do PowerShell.
* Adicione adicionais IP endereços tooa balanceador de carga para mais de um grupo de disponibilidade. 

Um ouvinte de grupo de disponibilidade é um nome de rede virtual que os clientes se conectem toofor acesso de banco de dados. Em máquinas virtuais do Azure, um balanceador de carga contém o endereço IP hello ouvinte Olá. rotas de Balanceador de carga Olá toohello instância do SQL Server está escutando na porta de investigação de saudação do tráfego. Normalmente, um grupo de disponibilidade usa um balanceador de carga interno. Um balanceador de carga interno do Azure pode hospedar um ou vários endereços IP. Cada endereço IP usa uma porta de investigação específica. Este documento mostra como toouse PowerShell toocreate um balanceador de carga ou adicione endereços de IP tooan balanceador de carga existente para grupos de disponibilidade do SQL Server. 

Olá capacidade tooassign vários balanceador de carga interno de tooan para endereços IP é tooAzure novo e está disponível apenas no modelo do Gerenciador de recursos. toocomplete nesta tarefa, você precisa toohave implantado de um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure no modelo do Gerenciador de recursos. Máquinas virtuais do SQL Server deve pertencer toohello mesmo conjunto de disponibilidade. Você pode usar o hello [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically criar grupo de disponibilidade de saudação no Gerenciador de recursos do Azure. Este modelo cria automaticamente o grupo de disponibilidade hello, incluindo o balanceador de carga interno Olá para você. Se preferir, você poderá [configurar manualmente um grupo de disponibilidade AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Este tópico exige que os grupos de disponibilidade já estejam configurados.  

Os tópicos relacionados incluem:

* [Configurar os Grupos de Disponibilidade AlwaysOn na VM do Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurar uma conexão de rede virtual com rede virtual usando o PowerShell e o Azure Resource Manager](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Configurar Olá Firewall do Windows
Configure o acesso ao SQL Server tooallow Firewall do Windows hello. as regras de firewall Olá permitem o usam de portas de toohello conexões TCP por instância do SQL Server hello e investigação do ouvinte hello. Para obter instruções detalhadas, confira [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Crie uma regra de entrada para Olá porta do SQL Server e para a porta de investigação de saudação.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Script de exemplo: criar um balanceador de carga interno usando o PowerShell
> [!NOTE]
> Se você criou o grupo de disponibilidade com hello [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), o balanceador de carga interno Olá já foi criado. 
> 
> 

Olá seguinte script do PowerShell cria um balanceador de carga interno, configura regras de balanceamento de carga de saudação e define um endereço IP hello balanceador de carga. script de saudação toorun, abra o Windows PowerShell ISE e cole o script hello no painel de Script hello. Use `Login-AzureRMAccount` toolog em tooPowerShell. Se você tiver várias assinaturas do Azure, use `Select-AzureRmSubscription ` tooset assinatura de saudação. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Script de exemplo: adicionar um IP endereço tooan balanceador de carga com o PowerShell
toouse mais de um grupo de disponibilidade, adicione um balanceador de carga adicional toohello de endereço IP. Cada endereço IP requer sua própria regra de balanceamento de carga, porta de investigação e porta de front-end.

Olá front-end porta é Olá que aplicativos usam a instância do SQL Server toohello tooconnect. Endereços IP para diferentes grupos de disponibilidade podem use Olá a mesma porta de front-end.

> [!NOTE]
> Para grupos de disponibilidade do SQL Server, cada endereço IP exige uma porta de investigação específica. Por exemplo, se um endereço IP em um balanceador de carga usa a porta de investigação 59999, nenhum outro endereço IP nesse balanceador de carga pode usar essa porta de investigação.

* Para saber mais sobre os limites do balanceador de carga, confira **IP privado front-end por balanceador de carga** em [Limites de Rede – Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Para saber mais sobre os limites de grupo de disponibilidade, confira [Restrições (Grupos de Disponibilidade)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Olá, script a seguir adiciona um novo IP endereço tooan balanceador de carga. Olá ILB usa a porta de escuta Olá Olá balanceamento de carga porta de front-end. Essa porta pode ser Olá que o SQL Server está escutando. Para instâncias padrão do SQL Server, a porta de saudação é 1433. regra para um grupo de disponibilidade de balanceamento de carga de saudação requer um IP flutuante (retorno de servidor direto) para a porta de back-end de saudação é Olá mesmo como portas de front-end de saudação. Atualize as variáveis de saudação para seu ambiente. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Configurar ouvinte Olá

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Defina a porta do ouvinte Olá no SQL Server Management Studio

1. Inicie o SQL Server Management Studio e conecte-se a réplica primária toohello.

1. Navegue muito**alta disponibilidade AlwaysOn** | **grupos de disponibilidade** | **ouvintes do grupo de disponibilidade**. 

1. Agora você deve ver o nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover. Nome do ouvinte de saudação de mouse e clique em **propriedades**.

1. Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade Olá usando Olá $EndpointPort utilizado antes (1433 foi padrão Olá), em seguida, clique em **Okey**.

## <a name="test-hello-connection-toohello-listener"></a>Ouvinte de toohello de conexão de saudação do teste

conexão de saudação tootest:

1. RDP tooa SQL Server que está em Olá mesmo virtual de rede, mas não não réplica Olá próprio. Isso pode ser Olá outros SQL Server em cluster hello.

1. Use **sqlcmd** conexão de saudação do utilitário tootest. Por exemplo, a saudação script a seguir estabelece uma **sqlcmd** réplica primária de toohello de conexão por meio do ouvinte Olá com autenticação do Windows:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Se o ouvinte Olá estiver usando uma porta diferente de Olá padrão (1433) de porta, especifique a porta Olá na cadeia de caracteres de conexão de saudação. Por exemplo, hello seguinte comando sqlcmd conecta tooa escuta na porta 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Olá conexão SQLCMD conecta-se automaticamente toowhichever instância do SQL Server hospeda Olá a réplica primária. 

> [!NOTE]
> Certifique-se de que a porta de Olá especificado é aberta no firewall Olá de ambos os servidores SQL. Ambos os servidores exigem uma regra de entrada para Olá a porta TCP que você usa. Veja [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx) para obter mais informações. 
> 
> 

## <a name="guidelines-and-limitations"></a>Diretrizes e limitações
Observe Olá diretrizes no ouvinte do grupo de disponibilidade no Azure usando o balanceador de carga interno a seguir:

* Com um balanceador de carga interno, apenas acesso ouvinte Olá de dentro de saudação mesma rede virtual.


## <a name="for-more-information"></a>Para obter mais informações
Para saber mais, confira [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md) (Configurar grupo de disponibilidade Always On na VM do Azure manualmente).

## <a name="powershell-cmdlets"></a>Cmdlets do PowerShell
Use Olá toocreate de cmdlets do PowerShell um balanceador de carga interno para máquinas virtuais do Azure a seguir.

* [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) cria um balanceador de carga. 
* [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) cria uma configuração de IP de front-end para um balanceador de carga. 
* [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) cria uma configuração de regra para um balanceador de carga. 
* [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) cria uma configuração de pool de endereços de back-end para um balanceador de carga. 
* [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) cria uma configuração de investigação para um balanceador de carga.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) remove um balanceador de carga de um grupo de recursos do Azure.
