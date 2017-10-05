---
title: "Conectar-se ao Kafka usando redes virtuais – Azure HDInsight | Microsoft Docs"
description: "Saiba como conectar-se diretamente ao Kafka no HDInsight por meio de uma Rede Virtual do Azure. Saiba como se conectar ao Kafka de clientes de desenvolvimento usando um gateway de VPN ou então de clientes em sua rede local usando um dispositivo de gateway de VPN."
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="0a6fb-104">Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0a6fb-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="0a6fb-105">Saiba como se conectar diretamente ao Kafka no HDInsight usando Redes Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="0a6fb-106">Este documento fornece informações sobre como se conectar ao Kafka usando as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="0a6fb-107">De recursos em uma rede local.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-107">From resources in an on-premises network.</span></span> <span data-ttu-id="0a6fb-108">Essa conexão é estabelecida usando um dispositivo VPN (software ou hardware) em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="0a6fb-109">De um ambiente de desenvolvimento usando um cliente de software VPN.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="0a6fb-110">Arquitetura e planejamento</span><span class="sxs-lookup"><span data-stu-id="0a6fb-110">Architecture and planning</span></span>

<span data-ttu-id="0a6fb-111">O HDInsight não permite a conexão direta ao Kafka pela Internet pública.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="0a6fb-112">Em vez disso, os clientes Kafka (produtores e consumidores) devem usar um dos seguintes métodos de conexão:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="0a6fb-113">Execute o cliente na mesma rede virtual que o Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="0a6fb-114">Essa configuração é usada no documento [Introdução ao Apache Kafka (versão prévia) no HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="0a6fb-115">O cliente é executado diretamente em nós do cluster HDInsight ou em outra máquina virtual na mesma rede.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="0a6fb-116">Conecte uma rede privada, como a sua rede local, à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="0a6fb-117">Essa configuração permite que os clientes na rede local trabalhem diretamente com o Kafka.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="0a6fb-118">Para habilitar essa configuração, execute as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="0a6fb-119">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="0a6fb-120">Crie um gateway de VPN que use uma configuração de site a site.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="0a6fb-121">A configuração usada neste documento se conecta a um dispositivo de gateway de VPN na rede local.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="0a6fb-122">Crie um servidor DNS na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="0a6fb-123">Configure o encaminhamento entre o servidor DNS em cada rede.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="0a6fb-124">Instale o Kafka no HDInsight na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="0a6fb-125">Para obter mais informações, consulte a seção [Conectar-se ao Kafka de uma rede local](#on-premises).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="0a6fb-126">Conecte computadores individuais à rede virtual usando um gateway de VPN e um cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="0a6fb-127">Para habilitar essa configuração, execute as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="0a6fb-128">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="0a6fb-129">Crie um gateway de VPN que use uma configuração de ponto a site.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="0a6fb-130">Essa configuração fornece um cliente VPN que pode ser instalado em clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="0a6fb-131">Instale o Kafka no HDInsight na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="0a6fb-132">Configure o Kafka para anúncio de IP.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="0a6fb-133">Essa configuração permite ao cliente conectar-se usando o endereçamento IP em vez de nomes de domínio.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="0a6fb-134">Baixe e use o cliente VPN no sistema de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="0a6fb-135">Para obter mais informações, consulte a seção [Conectar-se ao Kafka com um cliente VPN](#vpnclient).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0a6fb-136">Essa configuração é recomendada apenas para fins de desenvolvimento devido às seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="0a6fb-137">Cada cliente deve se conectar usando um cliente de software VPN.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="0a6fb-138">O Azure fornece apenas um cliente baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="0a6fb-139">O cliente não passar solicitações de resolução de nome para a rede virtual, então você deve usar endereçamento IP para se comunicar com o Kafka.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="0a6fb-140">A comunicação de IP requer configuração adicional no cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="0a6fb-141">Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="0a6fb-142"><a id="on-premises"></a> Conectar-se ao Kafka de uma rede local</span><span class="sxs-lookup"><span data-stu-id="0a6fb-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="0a6fb-143">Para criar um cluster Kafka que se comunique com a rede local, siga as etapas no documento [Conectar o HDInsight à rede local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a6fb-144">Ao criar o cluster HDInsight, selecione o tipo de cluster __Kafka__.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="0a6fb-145">Essas etapas criam a configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="0a6fb-146">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0a6fb-146">Azure Virtual Network</span></span>
* <span data-ttu-id="0a6fb-147">Gateway de VPN site a site</span><span class="sxs-lookup"><span data-stu-id="0a6fb-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="0a6fb-148">Conta de Armazenamento do Azure (usada pelo HDInsight)</span><span class="sxs-lookup"><span data-stu-id="0a6fb-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="0a6fb-149">Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a6fb-149">Kafka on HDInsight</span></span>

<span data-ttu-id="0a6fb-150">Para verificar se um cliente Kafka pode se conectar ao cluster local, use as etapas na seção [Exemplo: cliente do Python](#python-client).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="0a6fb-151"><a id="vpnclient"></a> Conectar-se ao Kafka com um cliente VPN</span><span class="sxs-lookup"><span data-stu-id="0a6fb-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="0a6fb-152">Use as etapas nesta seção para criar a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="0a6fb-153">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0a6fb-153">Azure Virtual Network</span></span>
* <span data-ttu-id="0a6fb-154">Gateway de VPN ponto a site</span><span class="sxs-lookup"><span data-stu-id="0a6fb-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="0a6fb-155">Conta de Armazenamento do Azure (usada pelo HDInsight)</span><span class="sxs-lookup"><span data-stu-id="0a6fb-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="0a6fb-156">Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a6fb-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="0a6fb-157">Siga as etapas no documento [Trabalhando com certificados autoassinados para conexões de ponto a site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="0a6fb-158">Esse documento cria os certificados necessários para o gateway.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="0a6fb-159">Abra um prompt do PowerShell e use o seguinte código para fazer logon em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="0a6fb-160">Use o seguinte código para criar variáveis que contenham informações de configuração:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="0a6fb-161">Use o seguinte código para criar o grupo de recursos do Azure e a rede virtual:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="0a6fb-162">Esse processo pode demorar para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="0a6fb-163">Use o seguinte código para criar a Conta de Armazenamento do Azure e o contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="0a6fb-164">Use o seguinte código para criar o cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="0a6fb-165">Esse processo leva cerca de 20 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="0a6fb-166">Use o seguinte cmdlet para recuperar a URL do cliente VPN do Windows para a rede virtual:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="0a6fb-167">Para baixar o cliente VPN do Windows, use o URI retornado no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="0a6fb-168">Configurar Kafka para anúncio de IP</span><span class="sxs-lookup"><span data-stu-id="0a6fb-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="0a6fb-169">Por padrão, o Zookeeper retorna o nome de domínio dos agentes do Kafka aos clientes.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="0a6fb-170">Essa configuração não funciona com o cliente de software VPN, pois não é possível usar a resolução de nomes para entidades na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="0a6fb-171">Para essa configuração, use as seguintes etapas para configurar o Kafka a fim de anunciar endereços IP no lugar de nomes de domínio:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="0a6fb-172">Usando um navegador da Web, acesse https://NOMEDOCLUSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0a6fb-173">Substitua __NOMEDOCLUSTER__ pelo nome do Kafka no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="0a6fb-174">Quando solicitado, use o nome de usuário e a senha HTTPS para o cluster.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="0a6fb-175">A Interface de Usuário Ambari Web para o cluster é exibida.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="0a6fb-176">Para exibir informações sobre o Kafka, selecione __Kafka__ na lista à esquerda.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Lista de serviços com Kafka realçado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="0a6fb-178">Para exibir a configuração do Kafka, selecione __Configurações__ na parte central superior.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Links de Configurações para Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="0a6fb-180">Para localizar a configuração __kafka-env__, digite `kafka-env` no campo __Filtro__ na parte superior direita.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Configuração do Kafka, para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="0a6fb-182">Para configurar o Kafka para anunciar endereços IP, adicione o seguinte texto à parte inferior do campo __kafka-env-template__:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="0a6fb-183">Para configurar a interface na qual o Kafka escuta, digite `listeners` no campo __Filtro__ na parte superior direita.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="0a6fb-184">Para configurar o Kafka para escutar em todas as interfaces de rede, altere o valor no campo __ouvintes__ para `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="0a6fb-185">Para salvar as alterações de configuração, use o botão __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="0a6fb-186">Digite uma mensagem de texto que descreva as alterações.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="0a6fb-187">Selecione __OK__ assim que as alterações tiverem sido salvas.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-187">Select __OK__ once the changes have been saved.</span></span>

    ![Botão Salvar configuração](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="0a6fb-189">Para evitar erros ao reiniciar o Kafka, use o botão __Ações de Serviço__ e selecione __Ativar o Modo de Manutenção__.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="0a6fb-190">Selecione OK para concluir essa operação.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-190">Select OK to complete this operation.</span></span>

    ![Ações de serviço, com ativar manutenção realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="0a6fb-192">Para reiniciar o Kafka, use o botão __Reiniciar__ e selecione __Reiniciar Todos os Afetados__.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="0a6fb-193">Confirme a reinicialização e, em seguida, use o botão __OK__ depois que a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Botão Reiniciar com reiniciar todos os afetados realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="0a6fb-195">Para desabilitar o modo de manutenção, use o botão __Ações de Serviço__ e selecione __Ativar o Modo de Manutenção__.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="0a6fb-196">Selecione **OK** para concluir essa operação.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="0a6fb-197">Conectar-se ao gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="0a6fb-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="0a6fb-198">Para se conectar ao gateway de VPN usando um __cliente Windows__, use a seção __Conectar ao Azure__ do documento [Configurar uma conexão Ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="0a6fb-199"><a id="python-client"></a> Exemplo: cliente do Python</span><span class="sxs-lookup"><span data-stu-id="0a6fb-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="0a6fb-200">Para validar a conectividade com o Kafka, use as etapas a seguir para criar e executar um produtor e consumidor de Python:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="0a6fb-201">Use um dos seguintes métodos para recuperar o FQDN (nome de domínio totalmente qualificado) e os endereços IP dos nós no cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="0a6fb-202">Esse script supõe que `$resourceGroupName` seja o nome do grupo de recursos do Azure que contém a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="0a6fb-203">Salve as informações retornadas para uso nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="0a6fb-204">Use o seguinte para instalar o cliente [kafka-python](http://kafka-python.readthedocs.io/):</span><span class="sxs-lookup"><span data-stu-id="0a6fb-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="0a6fb-205">Para enviar dados ao Kafka, use o seguinte código Python:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="0a6fb-206">Substitua as entradas `'kafka_broker'` pelos endereços retornados da etapa 1 nesta seção:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="0a6fb-207">Se você estiver usando um __cliente VPN de software__, substitua as entradas `kafka_broker` pelo endereço IP de seus nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="0a6fb-208">Se você tiver __habilitado a resolução de nomes por meio de um servidor DNS personalizado__, substitua as entradas `kafka_broker` pelo FQDN dos nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0a6fb-209">Esse código envia a cadeia de caracteres `test message` para o tópico `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="0a6fb-210">A configuração padrão do Kafka no HDInsight é criar o tópico se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="0a6fb-211">Para recuperar as mensagens do Kafka, use o seguinte código Python:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="0a6fb-212">Substitua as entradas `'kafka_broker'` pelos endereços retornados da etapa 1 nesta seção:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="0a6fb-213">Se você estiver usando um __cliente VPN de software__, substitua as entradas `kafka_broker` pelo endereço IP de seus nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="0a6fb-214">Se você tiver __habilitado a resolução de nomes por meio de um servidor DNS personalizado__, substitua as entradas `kafka_broker` pelo FQDN dos nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a6fb-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a6fb-215">Next steps</span></span>

<span data-ttu-id="0a6fb-216">Para obter mais informações sobre como usar o HDInsight com uma redes virtual, veja o documento [Estender o Azure HDInsight usando uma Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="0a6fb-217">Para saber mais sobre como criar uma Rede Virtual do Azure com o gateway de VPN Ponto a Site, confira os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="0a6fb-218">Configurar uma conexão Ponto a Site usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a6fb-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="0a6fb-219">Configurar uma conexão Ponto a Site usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a6fb-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="0a6fb-220">Para saber mais sobre como trabalhar com o Kafka no HDInsight, veja os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="0a6fb-221">Introdução ao Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a6fb-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="0a6fb-222">Usar o espelhamento com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a6fb-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
