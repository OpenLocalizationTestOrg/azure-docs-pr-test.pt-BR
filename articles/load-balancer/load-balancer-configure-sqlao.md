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
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="1039e-103">Configurar o balanceador de carga para SQL sempre ativo</span><span class="sxs-lookup"><span data-stu-id="1039e-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="1039e-104">Grupos de Disponibilidade AlwaysOn do SQL Server agora podem ser executados com ILB.</span><span class="sxs-lookup"><span data-stu-id="1039e-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="1039e-105">O Grupo de Disponibilidade é uma solução fundamental do SQL Server para alta disponibilidade e recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="1039e-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="1039e-106">Olá ouvinte do grupo de disponibilidade permite que aplicativos cliente tooseamlessly conectar-se a réplica primária toohello, independentemente do número de saudação de réplicas de saudação na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="1039e-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="1039e-107">nome do ouvinte (DNS) do Hello é o endereço IP de tooa mapeadas com balanceamento de carga e balanceador de carga do Azure direciona o servidor primário de Olá entrada tráfego tooonly Olá Olá conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="1039e-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="1039e-108">Você pode usar o suporte do ILB para pontos de extremidade AlwaysOn do SQL Server (ouvinte).</span><span class="sxs-lookup"><span data-stu-id="1039e-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="1039e-109">Agora você tem controle sobre acessibilidade de saudação do ouvinte hello e pode escolher o endereço IP de balanceamento de carga de saudação de uma sub-rede específica em sua rede Virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="1039e-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="1039e-110">Usando o ILB no ouvinte hello, Olá ponto de extremidade do SQL server (por exemplo, Server = tcp:ListenerName, 1433; banco de dados = DatabaseName) é acessível somente por:</span><span class="sxs-lookup"><span data-stu-id="1039e-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="1039e-111">Olá a serviços e máquinas virtuais na mesma rede Virtual</span><span class="sxs-lookup"><span data-stu-id="1039e-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="1039e-112">Serviços e VMs da rede local conectada</span><span class="sxs-lookup"><span data-stu-id="1039e-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="1039e-113">Serviços e VMs de VNets interconectadas</span><span class="sxs-lookup"><span data-stu-id="1039e-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="1039e-115">Figura 1 – SQL AlwaysOn configurado com o balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="1039e-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="1039e-116">Adicionar serviço de toohello do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="1039e-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="1039e-117">Olá exemplo a seguir, estamos vai configurar uma rede Virtual que contém uma sub-rede denominada 'Subnet-1':</span><span class="sxs-lookup"><span data-stu-id="1039e-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="1039e-118">Adicionar pontos de extremidade de balanceamento de carga ao ILB em cada VM</span><span class="sxs-lookup"><span data-stu-id="1039e-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="1039e-119">O exemplo hello acima, você tem 2 da VM chamado "sqlsvc1" e "sqlsvc2" execução na nuvem hello "Sqlsvc" de serviço.</span><span class="sxs-lookup"><span data-stu-id="1039e-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="1039e-120">Depois de criar hello ILB com `DirectServerReturn` alternar, adicionar pontos de extremidade com balanceamento toohello ILB tooallow SQL tooconfigure Olá ouvintes de grupos de disponibilidade de saudação de carga.</span><span class="sxs-lookup"><span data-stu-id="1039e-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="1039e-121">Para obter mais informações sobre o SQL AlwaysOn, consulte [Configure an internal load balancer for an AlwaysOn availability group in Azure (Configurar um balanceador de carga interno para um grupo de disponibilidade do AlwaysOn no Azure)](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="1039e-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1039e-122">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1039e-122">See Also</span></span>
[<span data-ttu-id="1039e-123">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="1039e-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="1039e-124">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="1039e-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="1039e-125">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="1039e-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1039e-126">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="1039e-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
