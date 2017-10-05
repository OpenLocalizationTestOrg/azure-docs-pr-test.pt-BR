---
title: "Ambiente de teste de nuvem híbrida simulado | Microsoft Docs"
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
ms.openlocfilehash: 4ec6f079b762a25894d822bfc098ea5442a1f7e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="1391f-103">Configurar um ambiente de nuvem híbrida simulado para testes</span><span class="sxs-lookup"><span data-stu-id="1391f-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="1391f-104">Este artigo explica como criar um ambiente simulado de nuvem híbrida com o Microsoft Azure usando duas redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="1391f-105">Veja abaixo a configuração resultante.</span><span class="sxs-lookup"><span data-stu-id="1391f-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="1391f-106">Isso simula um ambiente de produção de nuvem híbrida e consiste em:</span><span class="sxs-lookup"><span data-stu-id="1391f-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="1391f-107">Uma rede simulada e simplificada local, hospedada em uma rede virtual do Azure (a rede virtual TestLab).</span><span class="sxs-lookup"><span data-stu-id="1391f-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
* <span data-ttu-id="1391f-108">Uma rede virtual simulada entre locais, hospedada no Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="1391f-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="1391f-109">Uma conexão VNet para VNet entre as duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="1391f-109">A VNet-to-VNet connection between the two virtual networks.</span></span>
* <span data-ttu-id="1391f-110">Um controlador de domínio secundário na rede virtual TestVNET.</span><span class="sxs-lookup"><span data-stu-id="1391f-110">A secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="1391f-111">Isto proporciona uma base e um ponto de partida comum com os quais é possível:</span><span class="sxs-lookup"><span data-stu-id="1391f-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="1391f-112">Desenvolver e testar aplicativos em um ambiente de nuvem híbrida simulado.</span><span class="sxs-lookup"><span data-stu-id="1391f-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="1391f-113">Criar configurações de teste de computadores, alguns dentro da rede virtual TestLab e outros na rede virtual TestVNET, para simular cargas de TI baseadas em nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="1391f-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="1391f-114">Há quatro fases principais para configurar esse ambiente de teste de nuvem híbrida:</span><span class="sxs-lookup"><span data-stu-id="1391f-114">There are four major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="1391f-115">Configurar a rede virtual TestLab.</span><span class="sxs-lookup"><span data-stu-id="1391f-115">Configure the TestLab virtual network.</span></span>
2. <span data-ttu-id="1391f-116">Criar a rede virtual entre locais.</span><span class="sxs-lookup"><span data-stu-id="1391f-116">Create the cross-premises virtual network.</span></span>
3. <span data-ttu-id="1391f-117">Criar a conexão VPN de VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="1391f-117">Create the VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="1391f-118">Configurar o DC2.</span><span class="sxs-lookup"><span data-stu-id="1391f-118">Configure DC2.</span></span> 

<span data-ttu-id="1391f-119">Essa configuração exige uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="1391f-120">Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="1391f-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="1391f-121">Máquinas virtuais e gateways de redes virtuais no Azure geram custos monetários contínuos quando estão em execução.</span><span class="sxs-lookup"><span data-stu-id="1391f-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="1391f-122">Esse custo é cobrado em sua assinatura paga ou do MSDN.</span><span class="sxs-lookup"><span data-stu-id="1391f-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="1391f-123">Um gateway de VPN do Azure é implementado como um conjunto de duas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="1391f-124">Para minimizar os custos, crie o ambiente de teste e execute seus testes e demonstrações necessários o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="1391f-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="1391f-125">Fase 1: Configurar a rede virtual TestLab</span><span class="sxs-lookup"><span data-stu-id="1391f-125">Phase 1: Configure the TestLab virtual network</span></span>
<span data-ttu-id="1391f-126">Use as instruções no tópico [Base Configuration test environment (Ambiente de teste da Configuração de Base)](https://technet.microsoft.com/library/mt771177.aspx) para configurar os computadores DC1, APP1 e CLIENT1 na rede virtual do Azure chamada TestLab.</span><span class="sxs-lookup"><span data-stu-id="1391f-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="1391f-127">Em seguida, inicie um prompt do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1391f-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="1391f-128">O comando a seguir define o uso do Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="1391f-128">The following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="1391f-129">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="1391f-129">Sign in to your account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="1391f-130">Obtenha o nome da sua assinatura usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="1391f-130">Get your subscription name using the following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="1391f-131">Defina sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-131">Set your Azure subscription.</span></span> <span data-ttu-id="1391f-132">Use a mesma assinatura que você usou para compilar a configuração de base na Fase 1.</span><span class="sxs-lookup"><span data-stu-id="1391f-132">Use the same subscription that you used to build your base configuration in Phase 1.</span></span> <span data-ttu-id="1391f-133">Substitua tudo que estiver entre aspas, incluindo os caracteres < e >, pelo nome correto.</span><span class="sxs-lookup"><span data-stu-id="1391f-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="1391f-134">Em seguida, adicione uma sub-rede de gateway à rede virtual TestLab de sua configuração de base, que será usada para hospedar o gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="1391f-135">Em seguida, solicite um endereço IP público para atribuir o gateway à rede virtual TestLab.</span><span class="sxs-lookup"><span data-stu-id="1391f-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="1391f-136">Depois, crie seu gateway.</span><span class="sxs-lookup"><span data-stu-id="1391f-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="1391f-137">Lembre-se de que a criação de novos gateways pode levar 20 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="1391f-137">Keep in mind that new gateways can take 20 minutes or more to create.</span></span>

<span data-ttu-id="1391f-138">No portal do Azure em seu computador local, conecte-se ao DC1 com as credenciais CORP\User1.</span><span class="sxs-lookup"><span data-stu-id="1391f-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span></span> <span data-ttu-id="1391f-139">Para configurar o domínio CORP para que computadores e usuários utilizem seu controlador de domínio local para autenticação, execute estes comandos em um prompt de comando no nível de administrador do Windows PowerShell no DC1.</span><span class="sxs-lookup"><span data-stu-id="1391f-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="1391f-140">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="1391f-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a><span data-ttu-id="1391f-141">Fase 2: Criar a rede virtual TestVNET</span><span class="sxs-lookup"><span data-stu-id="1391f-141">Phase 2: Create the TestVNET virtual network</span></span>
<span data-ttu-id="1391f-142">Primeiro, crie a rede virtual TestVNET e proteja-a com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="1391f-142">First, create the TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of the resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="1391f-143">Em seguida, solicite um endereço IP público para ser alocado para o gateway para a rede virtual TestVNET e crie seu gateway.</span><span class="sxs-lookup"><span data-stu-id="1391f-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="1391f-144">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="1391f-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a><span data-ttu-id="1391f-145">Fase 3: Criar a conexão de VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="1391f-145">Phase 3: Create the VNet-to-VNet connection</span></span>
<span data-ttu-id="1391f-146">Primeiro, obtenha uma chave pré-compartilhada aleatória, criptograficamente forte de 32 caracteres do seu administrador de rede ou segurança.</span><span class="sxs-lookup"><span data-stu-id="1391f-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="1391f-147">Você também pode usar as informações em [Create a random string for an IPsec preshared key (Criar uma cadeia de caracteres aleatória para uma chave pré-compartilhada IPsec)](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) para obter uma chave pré-compartilhada.</span><span class="sxs-lookup"><span data-stu-id="1391f-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span></span>

<span data-ttu-id="1391f-148">Em seguida, use estes comandos para criar a conexão VPN VNet para VNet, que pode levar algum tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="1391f-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="1391f-149">Depois de alguns minutos, a conexão deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1391f-149">After a few minutes, the connection should be established.</span></span>

<span data-ttu-id="1391f-150">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="1391f-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="1391f-151">Fase 4: configurar o DC2</span><span class="sxs-lookup"><span data-stu-id="1391f-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="1391f-152">Em primeiro lugar, crie uma máquina virtual para DC2.</span><span class="sxs-lookup"><span data-stu-id="1391f-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="1391f-153">Execute estes comandos no prompt de comando do Azure PowerShell em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="1391f-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<the storage account name for the base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="1391f-154">Em seguida, conecte-se à nova máquina virtual DC2 do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1391f-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span></span>

<span data-ttu-id="1391f-155">Em seguida, configure uma regra do Firewall do Windows para permitir o tráfego e testar a conectividade básica.</span><span class="sxs-lookup"><span data-stu-id="1391f-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="1391f-156">Em um prompt de comando com nível de administrador do Windows PowerShell no DC2, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="1391f-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="1391f-157">O comando ping deve resultar em quatro respostas bem-sucedidas do endereço IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="1391f-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="1391f-158">Este é um teste de tráfego pela conexão de Rede Virtual para Rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="1391f-158">This is a test of traffic across the VNet-to-VNet connection.</span></span>

<span data-ttu-id="1391f-159">Em seguida, adicione o disco de dados extra no DC2 como um novo volume com a letra de unidade F:.</span><span class="sxs-lookup"><span data-stu-id="1391f-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="1391f-160">No painel esquerdo do Gerenciador do Servidor, clique em **Serviços de Arquivo e Armazenamento** e, em seguida, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="1391f-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="1391f-161">No painel de conteúdo, no grupo **Discos**, clique em **disco 2** (com a **Partição** definida como **Desconhecida**).</span><span class="sxs-lookup"><span data-stu-id="1391f-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="1391f-162">Clique em **Tarefas** e, em seguida, em **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="1391f-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="1391f-163">Na página Antes de começar do Assistente de Novo Volume, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="1391f-164">Na página Selecione o servidor e o disco, clique em **Disco 2** e, em seguida, em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="1391f-165">Quando solicitado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1391f-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="1391f-166">Na página Especifique o tamanho do volume, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-166">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="1391f-167">Na página Atribuir a uma letra da unidade ou pasta, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-167">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="1391f-168">Na página Selecionar configurações do sistema de arquivos, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-168">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="1391f-169">Na página Confirmar seleções, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-169">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="1391f-170">Ao concluir, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-170">When complete, click **Close**.</span></span>

<span data-ttu-id="1391f-171">Em seguida, configure o DC2 como um controlador de domínio de réplica para o domínio corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1391f-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span></span> <span data-ttu-id="1391f-172">Execute estes comandos no prompt de comando do Windows PowerShell no DC2.</span><span class="sxs-lookup"><span data-stu-id="1391f-172">Run these commands from the Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="1391f-173">Observe que você será solicitado a fornecer a senha de CORP\User1 e uma senha do Modo de Restauração dos Serviços de Diretório (DSRM) e reiniciar o DC2.</span><span class="sxs-lookup"><span data-stu-id="1391f-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span>

<span data-ttu-id="1391f-174">Agora que a rede virtual TestVNET tem seu próprio servidor DNS (DC2), você deve configurar a rede virtual TestVNET para usar esse servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="1391f-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span></span>

1. <span data-ttu-id="1391f-175">No painel esquerdo do portal do Azure, clique no ícone das redes virtuais e em **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="1391f-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="1391f-176">Na guia **Configurações**, clique em **Servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="1391f-176">On the **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="1391f-177">Em **Servidor DNS primário**, digite **192.168.0.4** para substituir 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="1391f-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span></span>
4. <span data-ttu-id="1391f-178">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1391f-178">Click **Save**.</span></span>

<span data-ttu-id="1391f-179">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="1391f-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="1391f-180">Seu ambiente de nuvem híbrida simulado agora está pronto para testes.</span><span class="sxs-lookup"><span data-stu-id="1391f-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="1391f-181">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="1391f-181">Next step</span></span>
* <span data-ttu-id="1391f-182">Configure um [aplicativo de linha de negócios baseado na Web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) nesse ambiente.</span><span class="sxs-lookup"><span data-stu-id="1391f-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

