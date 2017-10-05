---
title: "Criar uma configuração multi-SID do SAP no Azure | Microsoft Docs"
description: "Guia para configuração multi-SID do SAP NetWeaver de alta disponibilidade em máquinas virtuais do Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="3665a-103">Criar uma configuração multi-SID do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3665a-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="3665a-104">Em setembro de 2016, a Microsoft lançou um recurso com o qual é possível gerenciar vários endereços IP virtual usando um balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3665a-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="3665a-105">Essa funcionalidade já existe no balanceador externo de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="3665a-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="3665a-106">Se você tiver uma implantação do SAP, será possível usar um balanceador de carga interno para criar uma configuração de cluster do Windows para SAP ASCS/SCS, conforme documentado no [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="3665a-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="3665a-107">Este artigo aborda como mudar de uma instalação ASCS/SCS única para uma configuração Multi-SID do SAP com a instalação de instâncias em cluster do SAP ASCS/SCS adicionais em um cluster WSFC (Windows Server Failover Clustering) existente.</span><span class="sxs-lookup"><span data-stu-id="3665a-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="3665a-108">Quando esse processo for concluído, você já terá um cluster multi-SID do SAP configurado.</span><span class="sxs-lookup"><span data-stu-id="3665a-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3665a-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3665a-109">Prerequisites</span></span>
<span data-ttu-id="3665a-110">Você já configurou um cluster WSFC usado para uma instância SAP ASCS/SCS, conforme discutido no [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide] e conforme mostrado neste diagrama.</span><span class="sxs-lookup"><span data-stu-id="3665a-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instância do SAP ASCS/SCS de alta disponibilidade][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="3665a-112">Arquitetura de destino</span><span class="sxs-lookup"><span data-stu-id="3665a-112">Target architecture</span></span>

<span data-ttu-id="3665a-113">A meta é instalar várias instâncias clusterizadas do SAP ABAP ASCS ou do SAP Java SCS no mesmo cluster WSFC, conforme ilustrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3665a-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Várias instâncias clusterizadas do SAP ASCS/SCS no Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="3665a-115">Há um limite no número de IPs de front-end privado para cada balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3665a-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="3665a-116">O número máximo de instâncias do SAP ASCS/SCS em um cluster WSFC é igual ao número máximo de IPs de front-end privado para cada balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3665a-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="3665a-117">Para obter mais informações sobre limites do balanceador de carga, consulte “IP de front-end privado por balanceador de carga” em [Limites de Rede: Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="3665a-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="3665a-118">O cenário completo com dois sistemas SAP de alta disponibilidade seria assim:</span><span class="sxs-lookup"><span data-stu-id="3665a-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![Instalação multi-SID de alta disponibilidade do SAP com dois SIDs do sistema SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="3665a-120">A instalação deve atender às seguintes condições:</span><span class="sxs-lookup"><span data-stu-id="3665a-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="3665a-121">As instâncias do SAP ASCS/SCS deverão compartilhar o mesmo cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="3665a-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="3665a-122">Cada DBMS SID deverá ter seu próprio cluster WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="3665a-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="3665a-123">Os servidores de aplicativos SAP que pertencem a um SID do sistema SAP deverão ter suas próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="3665a-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="3665a-124">Preparar a infraestrutura</span><span class="sxs-lookup"><span data-stu-id="3665a-124">Prepare the infrastructure</span></span>
<span data-ttu-id="3665a-125">Para preparar sua infra-estrutura, é possível instalar uma instância do SAP ASCS/SCS adicional com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3665a-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="3665a-126">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="3665a-126">Parameter name</span></span> | <span data-ttu-id="3665a-127">Valor</span><span class="sxs-lookup"><span data-stu-id="3665a-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3665a-128">SID do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3665a-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="3665a-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="3665a-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="3665a-130">Balanceador de carga interno de DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="3665a-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="3665a-131">PR5</span><span class="sxs-lookup"><span data-stu-id="3665a-131">PR5</span></span> |
| <span data-ttu-id="3665a-132">Nome do host virtual do SAP</span><span class="sxs-lookup"><span data-stu-id="3665a-132">SAP virtual host name</span></span> | <span data-ttu-id="3665a-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3665a-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="3665a-134">Endereço IP do host virtual do SAP ASCS/SCS (endereço IP adicional do Azure Load Balancer)</span><span class="sxs-lookup"><span data-stu-id="3665a-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="3665a-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3665a-135">10.0.0.50</span></span> |
| <span data-ttu-id="3665a-136">Número da instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3665a-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="3665a-137">50</span><span class="sxs-lookup"><span data-stu-id="3665a-137">50</span></span> |
| <span data-ttu-id="3665a-138">Porta de investigação ILB para uma instância do SAP ASCS/SCS adicional</span><span class="sxs-lookup"><span data-stu-id="3665a-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="3665a-139">62350</span><span class="sxs-lookup"><span data-stu-id="3665a-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="3665a-140">Para instâncias de cluster SAP ASCS/SCS, cada endereço IP exige uma porta de investigação única.</span><span class="sxs-lookup"><span data-stu-id="3665a-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="3665a-141">Por exemplo, se um endereço IP em um balanceador de carga interno do Azure usar a porta de investigação 62300, nenhum outro endereço IP nesse balanceador de carga poderá usar a porta de investigação 62300.</span><span class="sxs-lookup"><span data-stu-id="3665a-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="3665a-142">Para nosso fim, como a porta de investigação 62300 já está reservada, estamos usando a porta de investigação 62350.</span><span class="sxs-lookup"><span data-stu-id="3665a-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="3665a-143">É possível instalar instâncias do SAP ASCS/SCS adicionais no cluster WSFC existente com dois nós:</span><span class="sxs-lookup"><span data-stu-id="3665a-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="3665a-144">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3665a-144">Virtual machine role</span></span> | <span data-ttu-id="3665a-145">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3665a-145">Virtual machine host name</span></span> | <span data-ttu-id="3665a-146">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="3665a-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3665a-147">1º nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3665a-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3665a-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="3665a-148">pr1-ascs-0</span></span> |<span data-ttu-id="3665a-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="3665a-149">10.0.0.10</span></span> |
| <span data-ttu-id="3665a-150">2º nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3665a-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3665a-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="3665a-151">pr1-ascs-1</span></span> |<span data-ttu-id="3665a-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="3665a-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="3665a-153">Criar um nome de host virtual para a instância do SAP ASCS/SCS clusterizada no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="3665a-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="3665a-154">É possível criar uma entrada DNS para o nome de host virtual da instância do ASCS/SCS usando os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3665a-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="3665a-155">Novo nome de host virtual do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3665a-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="3665a-156">Endereço IP associado</span><span class="sxs-lookup"><span data-stu-id="3665a-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="3665a-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3665a-157">pr5-sap-cl</span></span> |<span data-ttu-id="3665a-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3665a-158">10.0.0.50</span></span> |

<span data-ttu-id="3665a-159">O novo nome de host e endereço IP são exibidos no Gerenciador DNS, conforme mostrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="3665a-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![Lista do Gerenciador DNS que destaca a entrada DNS definida para o nome virtual do novo cluster SAP ASCS/SCS e para o endereço TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="3665a-161">O procedimento para criar uma entrada DNS também é descrito em detalhes no principal [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="3665a-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="3665a-162">O novo endereço IP atribuído ao nome de host virtual da instância do ASCS/SCS adicional deve ser igual ao novo endereço IP atribuído ao Azure Load Balancer do SAP.</span><span class="sxs-lookup"><span data-stu-id="3665a-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="3665a-163">Em nosso cenário, o endereço IP é 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="3665a-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="3665a-164">Adicionar um endereço IP a um balanceador de carga interno do Azure existente usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3665a-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="3665a-165">Para criar mais de uma instância do SAP ASCS/SCS no mesmo cluster WSFC, use o PowerShell para adicionar um endereço IP a um balanceador de carga interno do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="3665a-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="3665a-166">Cada endereço IP requer suas próprias regras de balanceamento de carga, porta de investigação, pool IP de front-end e pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3665a-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="3665a-167">O script a seguir adiciona um novo endereço IP a um balanceador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="3665a-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="3665a-168">Atualize as variáveis do PowerShell para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3665a-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="3665a-169">O script criará todas as regras de balanceamento de carga necessárias para todas as portas do SAP ASCS /SCS.</span><span class="sxs-lookup"><span data-stu-id="3665a-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get the Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="3665a-170">Depois que o script tiver sido executado, os resultados serão exibidos no portal do Azure, conforme mostrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="3665a-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Novo pool IP front-end no portal do Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="3665a-172">Adicionar discos a máquinas de cluster e configurar o disco de compartilhamento do cluster SIOS</span><span class="sxs-lookup"><span data-stu-id="3665a-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="3665a-173">É necessário adicionar um novo disco de compartilhamento de cluster para cada nova instância do SAP ASCS/SCS adicional.</span><span class="sxs-lookup"><span data-stu-id="3665a-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="3665a-174">Para o Windows Server 2012 R2, o disco de compartilhamento do cluster WSFC atualmente em uso é a solução de software SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="3665a-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="3665a-175">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3665a-175">Do the following:</span></span>
1. <span data-ttu-id="3665a-176">Inclua discos adicionais com o mesmo tamanho (que você precisa distribuir) para cada um dos nós de cluster e formate-os.</span><span class="sxs-lookup"><span data-stu-id="3665a-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="3665a-177">Configure a replicação de armazenamento com SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="3665a-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="3665a-178">Este procedimento pressupõe que você já tenha instalado o SIOS DataKeeper em computadores do cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="3665a-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="3665a-179">Se você o tiver instalado, agora será necessário configurar a replicação entre os computadores.</span><span class="sxs-lookup"><span data-stu-id="3665a-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="3665a-180">O processo é descrito em detalhes no principal [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="3665a-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Espelhamento síncrono do DataKeeper para o novo disco de compartilhamento do SAP ASCS/SCS][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="3665a-182">Implantar VMs em servidores de aplicativos SAP e cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="3665a-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="3665a-183">Para concluir a preparação da infraestrutura para o segundo sistema SAP, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3665a-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="3665a-184">Implante VMs dedicadas para servidores de aplicativos SAP e coloque-as no seu próprio grupo de disponibilidade dedicado.</span><span class="sxs-lookup"><span data-stu-id="3665a-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="3665a-185">Implante VMs dedicadas para o cluster DBMS e coloque-as no seu próprio grupo de disponibilidade dedicado.</span><span class="sxs-lookup"><span data-stu-id="3665a-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="3665a-186">Instalar o segundo sistema SAP SID2 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3665a-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="3665a-187">O processo completo de instalação de um segundo sistema SAP SID2 é descrito no principal [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="3665a-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="3665a-188">O procedimento de alto nível é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3665a-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="3665a-189">[ Instalar o primeiro nó do cluster do SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="3665a-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="3665a-190">Nesta etapa, instale o SAP com uma instância do ASCS/SCS de alta disponibilidade no **nó de cluster WSFC EXISTENTE 1**.</span><span class="sxs-lookup"><span data-stu-id="3665a-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="3665a-191">[Modificar o perfil SAP da instância do ASCS/SCS][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="3665a-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="3665a-192">[Configurar uma investigação][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="3665a-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="3665a-193">Nesta etapa, você configurará uma porta de investigação SAP-SID2-IP do recurso do cluster SAP usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3665a-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="3665a-194">Execute essa configuração em um dos nós do cluster SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3665a-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="3665a-195">[Instale a instância do banco de dados][sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="3665a-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="3665a-196">Nesta etapa, você instalará o DBMS em um cluster WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="3665a-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="3665a-197">[Instale o segundo nó de cluster][sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="3665a-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="3665a-198">Nesta etapa, instale o SAP com uma instância do ASCS/SCS de alta disponibilidade no nó de cluster WSFC existente 2.</span><span class="sxs-lookup"><span data-stu-id="3665a-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="3665a-199">Abra portas do Firewall do Windows para a instância do SAP ASCS /SCS e ProbePort.</span><span class="sxs-lookup"><span data-stu-id="3665a-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="3665a-200">Em ambos os nós de cluster usados para as instâncias do SAP ASCS/SCS, abra todas as portas do Firewall do Windows usadas pelo SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3665a-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="3665a-201">Essas portas estão listadas no principal [guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="3665a-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="3665a-202">Além disso, abra a porta de investigação do balanceador de carga interno do Azure, que, neste cenário, é 62350.</span><span class="sxs-lookup"><span data-stu-id="3665a-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="3665a-203">[Alterar o tipo de início da instância do serviço Windows ERS do SAP][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="3665a-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="3665a-204">[Instale o servidor de aplicativos SAP principal][sap-ha-guide-9.5] na nova VM dedicada.</span><span class="sxs-lookup"><span data-stu-id="3665a-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="3665a-205">[Instale o servidor de aplicativos SAP adicional][sap-ha-guide-9.6] na nova VM dedicada.</span><span class="sxs-lookup"><span data-stu-id="3665a-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="3665a-206">[Testar o failover da instância do SAP ASCS/SCS e a replicação do SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="3665a-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3665a-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3665a-207">Next steps</span></span>

- <span data-ttu-id="3665a-208">[Limites de rede: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="3665a-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="3665a-209">[Múltiplos VIPs para o Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="3665a-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="3665a-210">[Guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="3665a-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
