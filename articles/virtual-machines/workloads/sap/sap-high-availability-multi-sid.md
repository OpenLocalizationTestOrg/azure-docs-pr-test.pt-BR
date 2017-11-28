---
title: "aaaCreate uma configuração de multi-SID do SAP no Azure | Microsoft Docs"
description: "Configuração de várias SID do guia toohigh disponibilidade SAP NetWeaver em máquinas virtuais do Windows"
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
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="3bbee-103">Criar uma configuração multi-SID do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3bbee-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="3bbee-104">Em setembro de 2016, a Microsoft lançou um recurso com o qual é possível gerenciar vários endereços IP virtual usando um balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="3bbee-105">Essa funcionalidade já existe no balanceador de carga externo do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="3bbee-106">Se você tiver uma implantação do SAP, você pode usar um balanceador de carga interno toocreate uma configuração de cluster do Windows para o SAP ASCS/SCS, conforme documentado no hello [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="3bbee-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="3bbee-107">Este artigo se concentra em como toomove de uma única ASCS/SCS instalação tooan SAP várias SID configuração instalando adicional SAP ASCS/SCS instâncias clusterizadas em um cluster existente do Windows Server Failover Clustering (WSFC).</span><span class="sxs-lookup"><span data-stu-id="3bbee-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="3bbee-108">Quando esse processo for concluído, você já terá um cluster multi-SID do SAP configurado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3bbee-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3bbee-109">Prerequisites</span></span>
<span data-ttu-id="3bbee-110">Você já tiver configurado um cluster WSFC que é usado para uma instância SAP ASCS/SCS, conforme discutido em Olá [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows] [ sap-ha-guide] e conforme mostrado neste diagrama.</span><span class="sxs-lookup"><span data-stu-id="3bbee-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instância do SAP ASCS/SCS de alta disponibilidade][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="3bbee-112">Arquitetura de destino</span><span class="sxs-lookup"><span data-stu-id="3bbee-112">Target architecture</span></span>

<span data-ttu-id="3bbee-113">Olá meta é tooinstall vários SAP ABAP ASCS ou SAP Java SCS clusterizado instâncias Olá mesmo cluster WSFC, conforme ilustrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3bbee-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Várias instâncias clusterizadas do SAP ASCS/SCS no Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="3bbee-115">Há um número de toohello limite de IPs privados de front-end para cada balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="3bbee-116">número máximo de saudação de instâncias SAP ASCS/SCS em um cluster WSFC é igual toohello o número máximo de IPs privados de front-end para cada balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="3bbee-117">Para obter mais informações sobre limites do balanceador de carga, consulte “IP de front-end privado por balanceador de carga” em [Limites de Rede: Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="3bbee-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="3bbee-118">cenário completo de saudação com dois sistemas SAP de alta disponibilidade deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="3bbee-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![Instalação multi-SID de alta disponibilidade do SAP com dois SIDs do sistema SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="3bbee-120">instalação de saudação deve atender aos Olá condições a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="3bbee-121">Olá SAP ASCS/SCS instâncias devem compartilhar Olá mesmo cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="3bbee-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="3bbee-122">Cada DBMS SID deverá ter seu próprio cluster WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="3bbee-123">Servidores de aplicativos SAP que pertencem o sistema SAP de tooone SID devem ter suas próprias VMs dedicados.</span><span class="sxs-lookup"><span data-stu-id="3bbee-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="3bbee-124">Preparar a infraestrutura de saudação</span><span class="sxs-lookup"><span data-stu-id="3bbee-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="3bbee-125">tooprepare sua infra-estrutura, você pode instalar uma instância adicional do SAP ASCS/SCS com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="3bbee-126">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="3bbee-126">Parameter name</span></span> | <span data-ttu-id="3bbee-127">Valor</span><span class="sxs-lookup"><span data-stu-id="3bbee-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3bbee-128">SID do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3bbee-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="3bbee-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="3bbee-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="3bbee-130">Balanceador de carga interno de DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="3bbee-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="3bbee-131">PR5</span><span class="sxs-lookup"><span data-stu-id="3bbee-131">PR5</span></span> |
| <span data-ttu-id="3bbee-132">Nome do host virtual do SAP</span><span class="sxs-lookup"><span data-stu-id="3bbee-132">SAP virtual host name</span></span> | <span data-ttu-id="3bbee-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3bbee-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="3bbee-134">Endereço IP do host virtual do SAP ASCS/SCS (endereço IP adicional do Azure Load Balancer)</span><span class="sxs-lookup"><span data-stu-id="3bbee-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="3bbee-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3bbee-135">10.0.0.50</span></span> |
| <span data-ttu-id="3bbee-136">Número da instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3bbee-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="3bbee-137">50</span><span class="sxs-lookup"><span data-stu-id="3bbee-137">50</span></span> |
| <span data-ttu-id="3bbee-138">Porta de investigação ILB para uma instância do SAP ASCS/SCS adicional</span><span class="sxs-lookup"><span data-stu-id="3bbee-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="3bbee-139">62350</span><span class="sxs-lookup"><span data-stu-id="3bbee-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="3bbee-140">Para instâncias de cluster SAP ASCS/SCS, cada endereço IP exige uma porta de investigação única.</span><span class="sxs-lookup"><span data-stu-id="3bbee-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="3bbee-141">Por exemplo, se um endereço IP em um balanceador de carga interno do Azure usar a porta de investigação 62300, nenhum outro endereço IP nesse balanceador de carga poderá usar a porta de investigação 62300.</span><span class="sxs-lookup"><span data-stu-id="3bbee-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="3bbee-142">Para nosso fim, como a porta de investigação 62300 já está reservada, estamos usando a porta de investigação 62350.</span><span class="sxs-lookup"><span data-stu-id="3bbee-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="3bbee-143">Você pode instalar instâncias adicionais do SAP ASCS/SCS no cluster WSFC existente de saudação com dois nós:</span><span class="sxs-lookup"><span data-stu-id="3bbee-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="3bbee-144">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3bbee-144">Virtual machine role</span></span> | <span data-ttu-id="3bbee-145">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3bbee-145">Virtual machine host name</span></span> | <span data-ttu-id="3bbee-146">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="3bbee-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bbee-147">1º nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3bbee-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3bbee-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="3bbee-148">pr1-ascs-0</span></span> |<span data-ttu-id="3bbee-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="3bbee-149">10.0.0.10</span></span> |
| <span data-ttu-id="3bbee-150">2º nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3bbee-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3bbee-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="3bbee-151">pr1-ascs-1</span></span> |<span data-ttu-id="3bbee-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="3bbee-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="3bbee-153">Criar um nome de host virtual para instância do SAP ASCS/SCS Olá clusterizado no servidor DNS Olá</span><span class="sxs-lookup"><span data-stu-id="3bbee-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="3bbee-154">Você pode criar uma entrada DNS para o nome de host virtual Olá da instância do ASCS/SCS hello usando Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="3bbee-155">Novo nome de host virtual do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3bbee-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="3bbee-156">Endereço IP associado</span><span class="sxs-lookup"><span data-stu-id="3bbee-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="3bbee-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3bbee-157">pr5-sap-cl</span></span> |<span data-ttu-id="3bbee-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3bbee-158">10.0.0.50</span></span> |

<span data-ttu-id="3bbee-159">Olá novo nome de host e endereço IP são exibidos no hello Gerenciador DNS, conforme mostrado no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Lista de Gerenciador de DNS realce Olá definida a entrada DNS Olá novo SAP ASCS/SCS cluster virtual nome e endereço TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="3bbee-161">procedimento de saudação para criar uma entrada de DNS também está descrito detalhadamente no hello principal [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="3bbee-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="3bbee-162">Olá novo endereço IP que você atribuir o nome de host virtual toohello de instância adicional de ASCS/SCS Olá deve ser Olá igual a saudação novo endereço IP que você atribuiu o balanceador de carga do Azure do SAP toohello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="3bbee-163">Em nosso cenário, o endereço IP de saudação é 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="3bbee-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="3bbee-164">Adicionar um balanceador de carga interno do Azure existente do IP endereço tooan usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bbee-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="3bbee-165">toocreate mais de uma instância SAP ASCS/SCS no hello WSFC mesmo cluster, use PowerShell tooadd um tooan de endereço IP existente balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="3bbee-166">Cada endereço IP requer suas próprias regras de balanceamento de carga, porta de investigação, pool IP de front-end e pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3bbee-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="3bbee-167">Olá, script a seguir adiciona um novo IP endereço tooan balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="3bbee-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="3bbee-168">Atualize as variáveis do PowerShell de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3bbee-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="3bbee-169">script Hello criará necessárias todas as regras de balanceamento de carga para todas as portas do SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3bbee-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get hello Azure VNet and subnet
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

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="3bbee-170">Depois que o script hello foi executado, Olá resultados são exibidos no hello portal do Azure, conforme mostrado no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Novo pool IP de front-end no hello portal do Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="3bbee-172">Adicionar discos toocluster máquinas e configurar Olá SIOS cluster compartilhamento de disco</span><span class="sxs-lookup"><span data-stu-id="3bbee-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="3bbee-173">É necessário adicionar um novo disco de compartilhamento de cluster para cada nova instância do SAP ASCS/SCS adicional.</span><span class="sxs-lookup"><span data-stu-id="3bbee-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="3bbee-174">Para Windows Server 2012 R2, o disco de compartilhamento de cluster WSFC de saudação atualmente em uso é a solução de software SIOS DataKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="3bbee-175">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-175">Do hello following:</span></span>
1. <span data-ttu-id="3bbee-176">Adicionar adicional em disco ou discos de Olá mesmo tamanho (que é necessário toostripe) tooeach de saudação nós de cluster e formatá-los.</span><span class="sxs-lookup"><span data-stu-id="3bbee-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="3bbee-177">Configure a replicação de armazenamento com SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="3bbee-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="3bbee-178">Este procedimento pressupõe que você já instalou SIOS DataKeeper em máquinas de cluster WSFC hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="3bbee-179">Se você tiver instalado a ele, agora você deve configurar a replicação entre máquinas hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="3bbee-180">Olá processo é descrito em detalhes no hello principal [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="3bbee-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper para Olá novo SAP ASCS/SCS compartilhamento de disco de espelhamento síncrono][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="3bbee-182">Implantar VMs em servidores de aplicativos SAP e cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="3bbee-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="3bbee-183">preparação da infraestrutura toocomplete Olá para o sistema SAP da segunda hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbee-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="3bbee-184">Implante VMs dedicadas para servidores de aplicativos SAP e coloque-as no seu próprio grupo de disponibilidade dedicado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="3bbee-185">Implante VMs dedicadas para o cluster DBMS e coloque-as no seu próprio grupo de disponibilidade dedicado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="3bbee-186">Instalar o sistema SAP NetWeaver de SID2 da segunda Olá</span><span class="sxs-lookup"><span data-stu-id="3bbee-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="3bbee-187">concluir o processo de instalação de um sistema SAP SID2 segundo Olá Olá principal descrito [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="3bbee-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="3bbee-188">procedimento de alto nível de saudação é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3bbee-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="3bbee-189">[Instalar Olá SAP primeiro nó de cluster][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="3bbee-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="3bbee-190">Nesta etapa, você está instalando o SAP com uma instância do ASCS/SCS de alta disponibilidade em Olá **nó do cluster WSFC existente 1**.</span><span class="sxs-lookup"><span data-stu-id="3bbee-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="3bbee-191">[Modificar Olá SAP perfil da instância do ASCS/SCS Olá][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="3bbee-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="3bbee-192">[Configurar uma investigação][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="3bbee-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="3bbee-193">Nesta etapa, você configurará uma porta de investigação SAP-SID2-IP do recurso do cluster SAP usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bbee-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="3bbee-194">Execute essa configuração em um de nós de cluster Olá SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3bbee-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="3bbee-195">[Instale a instância de banco de dados de saudação] [sap-ha-guia-9.2].</span><span class="sxs-lookup"><span data-stu-id="3bbee-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="3bbee-196">Nesta etapa, você instalará o DBMS em um cluster WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="3bbee-197">[Instalação do segundo nó de cluster Olá] [sap-ha-guia-9.3].</span><span class="sxs-lookup"><span data-stu-id="3bbee-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="3bbee-198">Nesta etapa, você está instalando o SAP com uma instância do ASCS/SCS de alta disponibilidade no nó de cluster WSFC existente do hello 2.</span><span class="sxs-lookup"><span data-stu-id="3bbee-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="3bbee-199">Abrir portas de Firewall do Windows para a instância do SAP ASCS/SCS hello e ProbePort.</span><span class="sxs-lookup"><span data-stu-id="3bbee-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="3bbee-200">Em ambos os nós de cluster usados para as instâncias do SAP ASCS/SCS, abra todas as portas do Firewall do Windows usadas pelo SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3bbee-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="3bbee-201">Essas portas são listadas no hello [guia para alta disponibilidade SAP NetWeaver nas máquinas virtuais do Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="3bbee-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="3bbee-202">Também abra Olá interno de carga do Azure balanceador porta de investigação, que é 62350 em nosso cenário.</span><span class="sxs-lookup"><span data-stu-id="3bbee-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="3bbee-203">[Alterar tipo de inicialização de saudação da instância de serviço do Windows de ES do SAP Olá][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="3bbee-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="3bbee-204">[Instalar o servidor de aplicativo principal SAP Olá] [ sap-ha-guide-9.5] em Olá novo dedicado a VM.</span><span class="sxs-lookup"><span data-stu-id="3bbee-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="3bbee-205">[Instalar o servidor de aplicativos adicionais de SAP Olá] [ sap-ha-guide-9.6] em Olá novo dedicado a VM.</span><span class="sxs-lookup"><span data-stu-id="3bbee-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="3bbee-206">[Testar o failover de instância SAP ASCS/SCS hello e replicação SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="3bbee-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bbee-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3bbee-207">Next steps</span></span>

- <span data-ttu-id="3bbee-208">[Limites de rede: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="3bbee-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="3bbee-209">[Múltiplos VIPs para o Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="3bbee-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="3bbee-210">[Guia para SAP NetWeaver de alta disponibilidade em VMs do Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="3bbee-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
