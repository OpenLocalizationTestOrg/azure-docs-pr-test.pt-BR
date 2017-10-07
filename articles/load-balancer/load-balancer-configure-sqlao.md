---
title: aaaConfigure balanceador de carga para o SQL AlwaysOn | Microsoft Docs
description: "Configurar toowork do balanceador de carga com SQL sempre no e como tooleverage powershell toocreate balanceador de carga para implementação de SQL Olá"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Configurar o balanceador de carga para SQL sempre ativo

Grupos de Disponibilidade AlwaysOn do SQL Server agora podem ser executados com ILB. O Grupo de Disponibilidade é uma solução fundamental do SQL Server para alta disponibilidade e recuperação de desastres. Olá ouvinte do grupo de disponibilidade permite que aplicativos cliente tooseamlessly conectar-se a réplica primária toohello, independentemente do número de saudação de réplicas de saudação na configuração de saudação.

nome do ouvinte (DNS) do Hello é o endereço IP de tooa mapeadas com balanceamento de carga e balanceador de carga do Azure direciona o servidor primário de Olá entrada tráfego tooonly Olá Olá conjunto de réplicas.

Você pode usar o suporte do ILB para pontos de extremidade AlwaysOn do SQL Server (ouvinte). Agora você tem controle sobre acessibilidade de saudação do ouvinte hello e pode escolher o endereço IP de balanceamento de carga de saudação de uma sub-rede específica em sua rede Virtual (VNet).

Usando o ILB no ouvinte hello, Olá ponto de extremidade do SQL server (por exemplo, Server = tcp:ListenerName, 1433; banco de dados = DatabaseName) é acessível somente por:

* Olá a serviços e máquinas virtuais na mesma rede Virtual
* Serviços e VMs da rede local conectada
* Serviços e VMs de VNets interconectadas

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Figura 1 – SQL AlwaysOn configurado com o balanceador de carga para a Internet

## <a name="add-internal-load-balancer-toohello-service"></a>Adicionar serviço de toohello do balanceador de carga interno

1. Olá exemplo a seguir, estamos vai configurar uma rede Virtual que contém uma sub-rede denominada 'Subnet-1':

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Adicionar pontos de extremidade de balanceamento de carga ao ILB em cada VM

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    O exemplo hello acima, você tem 2 da VM chamado "sqlsvc1" e "sqlsvc2" execução na nuvem hello "Sqlsvc" de serviço. Depois de criar hello ILB com `DirectServerReturn` alternar, adicionar pontos de extremidade com balanceamento toohello ILB tooallow SQL tooconfigure Olá ouvintes de grupos de disponibilidade de saudação de carga.

Para obter mais informações sobre o SQL AlwaysOn, consulte [Configure an internal load balancer for an AlwaysOn availability group in Azure (Configurar um balanceador de carga interno para um grupo de disponibilidade do AlwaysOn no Azure)](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Consulte também
[Introdução à configuração de um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
