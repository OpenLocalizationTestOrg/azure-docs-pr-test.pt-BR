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
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="f21d6-103">Configurar um ambiente de nuvem híbrida simulado para testes</span><span class="sxs-lookup"><span data-stu-id="f21d6-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="f21d6-104">Este artigo explica como criar um ambiente simulado de nuvem híbrida com o Microsoft Azure usando duas redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="f21d6-105">Aqui está a configuração resultante hello.</span><span class="sxs-lookup"><span data-stu-id="f21d6-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="f21d6-106">Isso simula um ambiente de produção de nuvem híbrida e consiste em:</span><span class="sxs-lookup"><span data-stu-id="f21d6-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="f21d6-107">Uma rede simulada e simplificada local hospedada em uma rede virtual do Azure (rede virtual da saudação TestLab).</span><span class="sxs-lookup"><span data-stu-id="f21d6-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="f21d6-108">Uma rede virtual simulada entre locais, hospedada no Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="f21d6-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="f21d6-109">Uma conexão de rede virtual a rede entre redes virtuais Olá dois.</span><span class="sxs-lookup"><span data-stu-id="f21d6-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="f21d6-110">Um controlador de domínio secundário na rede virtual do hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="f21d6-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="f21d6-111">Isto proporciona uma base e um ponto de partida comum com os quais é possível:</span><span class="sxs-lookup"><span data-stu-id="f21d6-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="f21d6-112">Desenvolver e testar aplicativos em um ambiente de nuvem híbrida simulado.</span><span class="sxs-lookup"><span data-stu-id="f21d6-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="f21d6-113">Crie configurações de teste de computadores, alguns na rede virtual do hello TestLab e alguns na rede virtual Olá TestVNET, toosimulate híbrido baseado em nuvem IT cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f21d6-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="f21d6-114">Há quatro toosetting principais fases esse ambiente de teste de nuvem híbrida:</span><span class="sxs-lookup"><span data-stu-id="f21d6-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="f21d6-115">Configure a rede virtual do hello TestLab.</span><span class="sxs-lookup"><span data-stu-id="f21d6-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="f21d6-116">Crie rede virtual do hello entre locais.</span><span class="sxs-lookup"><span data-stu-id="f21d6-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="f21d6-117">Crie conexão de VPN Olá VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="f21d6-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="f21d6-118">Configurar o DC2.</span><span class="sxs-lookup"><span data-stu-id="f21d6-118">Configure DC2.</span></span> 

<span data-ttu-id="f21d6-119">Essa configuração exige uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="f21d6-120">Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="f21d6-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="f21d6-121">Máquinas virtuais e gateways de redes virtuais no Azure geram custos monetários contínuos quando estão em execução.</span><span class="sxs-lookup"><span data-stu-id="f21d6-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="f21d6-122">Esse custo é cobrado em sua assinatura paga ou do MSDN.</span><span class="sxs-lookup"><span data-stu-id="f21d6-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="f21d6-123">Um gateway de VPN do Azure é implementado como um conjunto de duas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="f21d6-124">custos de saudação toominimize, criar ambiente de teste de saudação e executar seus testes necessários e a demonstração assim que possível.</span><span class="sxs-lookup"><span data-stu-id="f21d6-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="f21d6-125">Etapa 1: Configurar a rede virtual do hello TestLab</span><span class="sxs-lookup"><span data-stu-id="f21d6-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="f21d6-126">Use instruções Olá Olá [ambiente de teste de configuração de Base](https://technet.microsoft.com/library/mt771177.aspx) tópico tooconfigure Olá DC1, APP1 e CLIENT1 computadores Olá rede virtual do Azure denominado TestLab.</span><span class="sxs-lookup"><span data-stu-id="f21d6-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="f21d6-127">Em seguida, inicie um prompt do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f21d6-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="f21d6-128">Olá conjuntos de comandos a seguir usa o Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="f21d6-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="f21d6-129">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="f21d6-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="f21d6-130">Obter o nome da sua assinatura usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f21d6-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="f21d6-131">Defina sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-131">Set your Azure subscription.</span></span> <span data-ttu-id="f21d6-132">Use Olá a mesma assinatura usada toobuild sua configuração base na fase 1.</span><span class="sxs-lookup"><span data-stu-id="f21d6-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="f21d6-133">Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com o nome correto da saudação.</span><span class="sxs-lookup"><span data-stu-id="f21d6-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="f21d6-134">Em seguida, adicione uma gateway sub-rede toohello TestLab rede virtual da sua configuração de base, que será usado toohost Olá gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="f21d6-135">Em seguida, solicite um público endereço tooassign toohello gateway IP para rede virtual do hello TestLab.</span><span class="sxs-lookup"><span data-stu-id="f21d6-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="f21d6-136">Depois, crie seu gateway.</span><span class="sxs-lookup"><span data-stu-id="f21d6-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="f21d6-137">Tenha em mente que novos gateways podem levar 20 minutos ou mais toocreate.</span><span class="sxs-lookup"><span data-stu-id="f21d6-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="f21d6-138">Em Olá o portal do Azure em seu computador local, conecte-se tooDC1 com as credenciais de CORP\User1 hello.</span><span class="sxs-lookup"><span data-stu-id="f21d6-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="f21d6-139">domínio do tooconfigure Olá CORP para que computadores e usuários usem o seu controlador de domínio local para autenticação, execute esses comandos em um prompt de comando do nível de administrador do Windows PowerShell no DC1.</span><span class="sxs-lookup"><span data-stu-id="f21d6-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="f21d6-140">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="f21d6-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="f21d6-141">Etapa 2: Criar rede virtual do hello TestVNET</span><span class="sxs-lookup"><span data-stu-id="f21d6-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="f21d6-142">Primeiro, crie a rede virtual do hello TestVNET e protegê-lo com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f21d6-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

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

<span data-ttu-id="f21d6-143">Em seguida, a solicitação um toobe de endereço IP público alocado toohello gateway para a rede virtual do hello TestVNET e criar o gateway.</span><span class="sxs-lookup"><span data-stu-id="f21d6-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="f21d6-144">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="f21d6-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="f21d6-145">Etapa 3: Criar conexão Olá VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="f21d6-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="f21d6-146">Primeiro, obtenha uma chave pré-compartilhada aleatória, criptograficamente forte de 32 caracteres do seu administrador de rede ou segurança.</span><span class="sxs-lookup"><span data-stu-id="f21d6-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="f21d6-147">Como alternativa, use informações de saudação em [criar uma cadeia de caracteres aleatória para uma chave pré-compartilhada IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain uma chave pré-compartilhada.</span><span class="sxs-lookup"><span data-stu-id="f21d6-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="f21d6-148">Em seguida, use a conexão de rede virtual a rede VPN esses comandos toocreate hello, que pode levar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f21d6-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="f21d6-149">Depois de alguns minutos, a conexão de saudação deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f21d6-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="f21d6-150">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="f21d6-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="f21d6-151">Fase 4: configurar o DC2</span><span class="sxs-lookup"><span data-stu-id="f21d6-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="f21d6-152">Em primeiro lugar, crie uma máquina virtual para DC2.</span><span class="sxs-lookup"><span data-stu-id="f21d6-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="f21d6-153">Execute esses comandos no prompt de comando do PowerShell do Azure Olá no computador local.</span><span class="sxs-lookup"><span data-stu-id="f21d6-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

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

<span data-ttu-id="f21d6-154">Em seguida, conecte-se a nova máquina de virtual DC2 toohello de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f21d6-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="f21d6-155">Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica.</span><span class="sxs-lookup"><span data-stu-id="f21d6-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="f21d6-156">Em um prompt de comando com nível de administrador do Windows PowerShell no DC2, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="f21d6-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="f21d6-157">comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="f21d6-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="f21d6-158">Este é um teste de tráfego Olá conexão de rede virtual a rede.</span><span class="sxs-lookup"><span data-stu-id="f21d6-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="f21d6-159">Em seguida, adicione Olá disco de dados extra no DC2 como um novo volume com a letra da unidade Olá f:.</span><span class="sxs-lookup"><span data-stu-id="f21d6-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="f21d6-160">No painel esquerdo de saudação do Gerenciador do servidor, clique em **serviços de arquivo e armazenamento**e, em seguida, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="f21d6-161">No painel de conteúdo de saudação em Olá **discos** de grupo, clique em **disco 2** (com hello **partição** definido muito**desconhecido**).</span><span class="sxs-lookup"><span data-stu-id="f21d6-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="f21d6-162">Clique em **Tarefas** e, em seguida, em **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="f21d6-163">Na saudação antes de começar a página do Assistente de novo Volume de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="f21d6-164">Na página de disco e servidor de saudação selecione hello, clique em **disco 2**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="f21d6-165">Quando solicitado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="f21d6-166">No hello especificar tamanho de saudação da página de volume hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="f21d6-167">Na saudação atribuir tooa unidade pasta ou letra da página, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="f21d6-168">Na página de configurações do sistema do arquivo selecione hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="f21d6-169">Na página Olá confirmar seleções, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="f21d6-170">Ao concluir, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-170">When complete, click **Close**.</span></span>

<span data-ttu-id="f21d6-171">Em seguida, configure o DC2 como um controlador de domínio de réplica para o domínio do hello corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f21d6-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="f21d6-172">Execute esses comandos no prompt de comando do Windows PowerShell Olá no DC2.</span><span class="sxs-lookup"><span data-stu-id="f21d6-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="f21d6-173">Observe que são solicitada toosupply ambos Olá corp/User1 senha e uma senha de modo de restauração de serviços de diretório (DSRM) e toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="f21d6-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="f21d6-174">Agora que hello, rede virtual TestVNET tem seu próprio servidor DNS (DC2), você deve configurar Olá TestVNET rede virtual toouse esse servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f21d6-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="f21d6-175">No painel esquerdo de saudação do hello portal do Azure, clique Olá ícone de redes virtuais e, em seguida, clique em **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="f21d6-176">Em Olá **configurações** , clique em **servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="f21d6-177">Em **servidor DNS primário**, tipo **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="f21d6-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="f21d6-178">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f21d6-178">Click **Save**.</span></span>

<span data-ttu-id="f21d6-179">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="f21d6-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="f21d6-180">Seu ambiente de nuvem híbrida simulado agora está pronto para testes.</span><span class="sxs-lookup"><span data-stu-id="f21d6-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="f21d6-181">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="f21d6-181">Next step</span></span>
* <span data-ttu-id="f21d6-182">Configure um [aplicativo de linha de negócios baseado na Web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) nesse ambiente.</span><span class="sxs-lookup"><span data-stu-id="f21d6-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

