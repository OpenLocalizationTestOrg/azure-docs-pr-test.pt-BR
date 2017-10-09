---
title: tooKafka aaaConnect usando redes virtuais - HDInsight do Azure | Microsoft Docs
description: Saiba como toodirectly conectar tooKafka no HDInsight por meio de uma rede Virtual do Azure. Saiba como tooconnect tooKafka de clientes de desenvolvimento usando um gateway VPN ou de clientes em seu local de rede usando um dispositivo de gateway VPN.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="b45c2-104">Conecte-se tooKafka no HDInsight (visualização) por meio de uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b45c2-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="b45c2-105">Saiba como toodirectly conectar tooKafka no HDInsight usando redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="b45c2-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="b45c2-106">Este documento fornece informações sobre como conectar tooKafka usando Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="b45c2-107">De recursos em uma rede local.</span><span class="sxs-lookup"><span data-stu-id="b45c2-107">From resources in an on-premises network.</span></span> <span data-ttu-id="b45c2-108">Essa conexão é estabelecida usando um dispositivo VPN (software ou hardware) em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="b45c2-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="b45c2-109">De um ambiente de desenvolvimento usando um cliente de software VPN.</span><span class="sxs-lookup"><span data-stu-id="b45c2-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="b45c2-110">Arquitetura e planejamento</span><span class="sxs-lookup"><span data-stu-id="b45c2-110">Architecture and planning</span></span>

<span data-ttu-id="b45c2-111">HDInsight não permite a conexão direta tooKafka sobre Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="b45c2-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="b45c2-112">Em vez disso, os clientes Kafka (produtores e consumidores) devem usar um dos Olá métodos de conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="b45c2-113">Execute o cliente de saudação em Olá mesma rede virtual Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b45c2-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="b45c2-114">Essa configuração é usada em Olá [iniciar com o Apache Kafka (visualização) no HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b45c2-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="b45c2-115">Hello cliente é executado diretamente em Olá HDInsight nós de cluster ou em outra máquina virtual no hello mesma rede.</span><span class="sxs-lookup"><span data-stu-id="b45c2-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="b45c2-116">Conecte-se a uma rede privada, como a sua rede local, rede virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="b45c2-117">Essa configuração permite que os clientes em seu trabalho de toodirectly de rede local com Kafka.</span><span class="sxs-lookup"><span data-stu-id="b45c2-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="b45c2-118">tooenable essa configuração, execute Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="b45c2-119">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b45c2-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="b45c2-120">Crie um gateway de VPN que use uma configuração de site a site.</span><span class="sxs-lookup"><span data-stu-id="b45c2-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="b45c2-121">configuração de saudação usada neste documento se conecta tooa dispositivo de gateway VPN na sua rede local.</span><span class="sxs-lookup"><span data-stu-id="b45c2-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="b45c2-122">Crie um servidor DNS na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="b45c2-123">Configure o encaminhamento entre o servidor DNS de saudação em cada rede.</span><span class="sxs-lookup"><span data-stu-id="b45c2-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="b45c2-124">Instale Kafka no HDInsight em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="b45c2-125">Para obter mais informações, consulte Olá [conectar tooKafka de uma rede local](#on-premises) seção.</span><span class="sxs-lookup"><span data-stu-id="b45c2-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="b45c2-126">Conecte-se a rede virtual do toohello máquinas individuais usando um gateway de VPN e o cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="b45c2-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="b45c2-127">tooenable essa configuração, execute Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="b45c2-128">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b45c2-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="b45c2-129">Crie um gateway de VPN que use uma configuração de ponto a site.</span><span class="sxs-lookup"><span data-stu-id="b45c2-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="b45c2-130">Essa configuração fornece um cliente VPN que pode ser instalado em clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="b45c2-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="b45c2-131">Instale Kafka no HDInsight em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="b45c2-132">Configure o Kafka para anúncio de IP.</span><span class="sxs-lookup"><span data-stu-id="b45c2-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="b45c2-133">Essa configuração permite Olá cliente tooconnect usando em vez de nomes de domínio de endereçamento IP.</span><span class="sxs-lookup"><span data-stu-id="b45c2-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="b45c2-134">Baixar e usar o cliente VPN Olá no sistema de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="b45c2-135">Para obter mais informações, consulte Olá [conectar tooKafka com um cliente VPN](#vpnclient) seção.</span><span class="sxs-lookup"><span data-stu-id="b45c2-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b45c2-136">Essa configuração é recomendada apenas para fins de desenvolvimento devido a saudação seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="b45c2-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="b45c2-137">Cada cliente deve se conectar usando um cliente de software VPN.</span><span class="sxs-lookup"><span data-stu-id="b45c2-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="b45c2-138">O Azure fornece apenas um cliente baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="b45c2-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="b45c2-139">cliente de saudação não passar nome resolução solicitações toohello rede virtual, você deve usar toocommunicate com Kafka de endereçamento IP.</span><span class="sxs-lookup"><span data-stu-id="b45c2-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="b45c2-140">Comunicação de IP requer configuração adicional no cluster Kafka de saudação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="b45c2-141">Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="b45c2-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="b45c2-142"><a id="on-premises"></a>Conecte-se tooKafka de uma rede local</span><span class="sxs-lookup"><span data-stu-id="b45c2-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="b45c2-143">toocreate um cluster Kafka que se comunica com a sua rede local, siga as etapas de Olá Olá [HDInsight conectar rede de local de tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b45c2-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b45c2-144">Ao criar o cluster do HDInsight hello, selecione Olá __Kafka__ tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="b45c2-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="b45c2-145">Essas etapas para criar Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="b45c2-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="b45c2-146">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b45c2-146">Azure Virtual Network</span></span>
* <span data-ttu-id="b45c2-147">Gateway de VPN site a site</span><span class="sxs-lookup"><span data-stu-id="b45c2-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="b45c2-148">Conta de Armazenamento do Azure (usada pelo HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b45c2-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="b45c2-149">Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b45c2-149">Kafka on HDInsight</span></span>

<span data-ttu-id="b45c2-150">tooverify que um cliente Kafka pode se conectar a cluster toohello do local, use etapas Olá Olá [exemplo: cliente Python](#python-client) seção.</span><span class="sxs-lookup"><span data-stu-id="b45c2-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="b45c2-151"><a id="vpnclient"></a>Conecte-se tooKafka com um cliente VPN</span><span class="sxs-lookup"><span data-stu-id="b45c2-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="b45c2-152">Use as etapas de Olá Olá de toocreate essa seção seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="b45c2-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="b45c2-153">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b45c2-153">Azure Virtual Network</span></span>
* <span data-ttu-id="b45c2-154">Gateway de VPN ponto a site</span><span class="sxs-lookup"><span data-stu-id="b45c2-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="b45c2-155">Conta de Armazenamento do Azure (usada pelo HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b45c2-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="b45c2-156">Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b45c2-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="b45c2-157">Siga as etapas de Olá Olá [trabalhar com certificados autoassinados para conexões ponto a site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b45c2-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="b45c2-158">Este documento cria certificados de saudação necessários para o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="b45c2-159">Abra um prompt do PowerShell e use Olá toolog de código em tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="b45c2-160">Olá Use variáveis de toocreate de código que contêm informações de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-160">Use hello following code toocreate variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="b45c2-161">Grupo de recursos do Azure Olá toocreate e rede virtual de código a seguir de Olá de uso:</span><span class="sxs-lookup"><span data-stu-id="b45c2-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > <span data-ttu-id="b45c2-162">Pode levar vários minutos para que esse processo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b45c2-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="b45c2-163">Use Olá contêiner de blob e conta de armazenamento do Azure de saudação de toocreate do código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="b45c2-164">Use Olá cluster do HDInsight de saudação de toocreate de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="b45c2-165">Esse processo leva cerca de 20 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b45c2-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="b45c2-166">Use Olá cmdlet tooretrieve Olá URL para o cliente de VPN do Windows hello para rede virtual Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="b45c2-167">cliente de VPN do Windows hello toodownload, use Olá retornado URI no navegador da web.</span><span class="sxs-lookup"><span data-stu-id="b45c2-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="b45c2-168">Configurar Kafka para anúncio de IP</span><span class="sxs-lookup"><span data-stu-id="b45c2-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="b45c2-169">Por padrão, Zookeeper retorna o nome de domínio de saudação do hello Kafka tooclients de agentes.</span><span class="sxs-lookup"><span data-stu-id="b45c2-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="b45c2-170">Essa configuração não funciona com hello cliente VPN de software, pois ele não pode usar a resolução de nomes de entidades de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="b45c2-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="b45c2-171">Para essa configuração, use o seguinte Olá tooconfigure etapas de endereços IP de tooadvertise Kafka em vez de nomes de domínio:</span><span class="sxs-lookup"><span data-stu-id="b45c2-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="b45c2-172">Usando um navegador da web, visite toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="b45c2-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b45c2-173">Substituir __CLUSTERNAME__ com nome Olá Olá Kafka no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b45c2-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="b45c2-174">Quando solicitado, use HTTPS Olá nome e uma senha para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="b45c2-175">Olá Ambari Web UI para cluster Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="b45c2-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="b45c2-176">informações de tooview em Kafka, selecione __Kafka__ Olá na lista de saudação esquerda.</span><span class="sxs-lookup"><span data-stu-id="b45c2-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Lista de serviços com Kafka realçado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="b45c2-178">Selecione tooview configuração Kafka, __configurações__ de intermediária superior hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Links de Configurações para Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="b45c2-180">Olá toofind __kafka env__ configuração, digite `kafka-env` em Olá __filtro__ campo na parte superior direita do hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Configuração do Kafka, para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="b45c2-182">endereços de IP de tooadvertise Kafka tooconfigure, adicione Olá após o fim do texto toohello de saudação __kafka-env-modelo__ campo:</span><span class="sxs-lookup"><span data-stu-id="b45c2-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="b45c2-183">interface de saudação de tooconfigure Kafka escuta em, digite `listeners` em Olá __filtro__ campo na parte superior direita do hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="b45c2-184">tooconfigure toolisten Kafka em todas as interfaces de rede, alterar o valor de saudação em Olá __ouvintes__ campo muito`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="b45c2-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="b45c2-185">alterações de configuração do toosave hello, use Olá __salvar__ botão.</span><span class="sxs-lookup"><span data-stu-id="b45c2-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="b45c2-186">Digite uma mensagem de texto que descreve as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="b45c2-187">Selecione __Okey__ depois Olá alterações foram salvas.</span><span class="sxs-lookup"><span data-stu-id="b45c2-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Botão Salvar configuração](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="b45c2-189">erros tooprevent ao reiniciar Kafka, use Olá __ações de serviço__ botão e selecione __ativar no modo de manutenção__.</span><span class="sxs-lookup"><span data-stu-id="b45c2-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="b45c2-190">Selecione toocomplete Okey esta operação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-190">Select OK toocomplete this operation.</span></span>

    ![Ações de serviço, com ativar manutenção realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="b45c2-192">toorestart Kafka, use Olá __reiniciar__ botão e selecione __reiniciar todos os afetados__.</span><span class="sxs-lookup"><span data-stu-id="b45c2-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="b45c2-193">Confirmar reinicialização hello e use Olá __Okey__ botão Olá operação concluída.</span><span class="sxs-lookup"><span data-stu-id="b45c2-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Botão Reiniciar com reiniciar todos os afetados realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="b45c2-195">toodisable modo de manutenção, use Olá __ações de serviço__ botão e selecione __ativar desativar o modo de manutenção__.</span><span class="sxs-lookup"><span data-stu-id="b45c2-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="b45c2-196">Selecione **Okey** toocomplete esta operação.</span><span class="sxs-lookup"><span data-stu-id="b45c2-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="b45c2-197">Conecte-se o gateway VPN toohello</span><span class="sxs-lookup"><span data-stu-id="b45c2-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="b45c2-198">tooconnect toohello gateway VPN de um __cliente Windows__, use Olá __conectar tooAzure__ seção Olá [configurar uma conexão ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.</span><span class="sxs-lookup"><span data-stu-id="b45c2-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="b45c2-199"><a id="python-client"></a> Exemplo: cliente do Python</span><span class="sxs-lookup"><span data-stu-id="b45c2-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="b45c2-200">toovalidate tooKafka de conectividade, use Olá toocreate as etapas a seguir e execute um produtor de Python e consumidor:</span><span class="sxs-lookup"><span data-stu-id="b45c2-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="b45c2-201">Usar um dos Olá Olá de tooretrieve métodos a seguir totalmente qualificado (FQDN) do nome de domínio e endereços IP de nós Olá Olá cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="b45c2-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="b45c2-202">Esse script presume que `$resourceGroupName` é nome Olá Olá do Azure do grupo de recursos que contém a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="b45c2-203">Salve Olá retornada informações para uso nas próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="b45c2-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="b45c2-204">Olá Use tooinstall Olá a seguir [kafka python](http://kafka-python.readthedocs.io/) cliente:</span><span class="sxs-lookup"><span data-stu-id="b45c2-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="b45c2-205">toosend dados tooKafka, use Olá código Python a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="b45c2-206">Substituir saudação `'kafka_broker'` entradas com endereços hello retornadas da etapa 1 nesta seção:</span><span class="sxs-lookup"><span data-stu-id="b45c2-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="b45c2-207">Se você estiver usando um __cliente VPN de Software__, substitua Olá `kafka_broker` entradas com o endereço IP de saudação de seus nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b45c2-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="b45c2-208">Se você tiver __habilitada a resolução de nomes por meio de um servidor DNS personalizado__, substitua Olá `kafka_broker` entradas com hello FQDN Olá de nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b45c2-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b45c2-209">Esse código envia a cadeia de caracteres de saudação `test message` toohello tópico `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="b45c2-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="b45c2-210">configuração de padrão de saudação do Kafka no HDInsight é tópico de saudação toocreate se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="b45c2-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="b45c2-211">mensagens de saudação do tooretrieve de Kafka, use Olá código Python a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="b45c2-212">Substituir saudação `'kafka_broker'` entradas com endereços hello retornadas da etapa 1 nesta seção:</span><span class="sxs-lookup"><span data-stu-id="b45c2-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="b45c2-213">Se você estiver usando um __cliente VPN de Software__, substitua Olá `kafka_broker` entradas com o endereço IP de saudação de seus nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b45c2-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="b45c2-214">Se você tiver __habilitada a resolução de nomes por meio de um servidor DNS personalizado__, substitua Olá `kafka_broker` entradas com hello FQDN Olá de nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b45c2-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b45c2-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b45c2-215">Next steps</span></span>

<span data-ttu-id="b45c2-216">Para obter mais informações sobre como usar o HDInsight com uma rede virtual, consulte Olá [estender o Azure HDInsight usando uma rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b45c2-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="b45c2-217">Para obter mais informações sobre como criar uma rede Virtual do Azure com o gateway VPN ponto a Site, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="b45c2-218">Configurar uma conexão ponto a Site usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b45c2-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="b45c2-219">Configurar uma conexão Ponto a Site usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b45c2-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="b45c2-220">Para obter mais informações sobre como trabalhar com Kafka no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b45c2-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b45c2-221">Introdução ao Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b45c2-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="b45c2-222">Usar o espelhamento com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b45c2-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
