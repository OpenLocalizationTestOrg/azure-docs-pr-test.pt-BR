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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Conecte-se tooKafka no HDInsight (visualização) por meio de uma rede Virtual do Azure

Saiba como toodirectly conectar tooKafka no HDInsight usando redes virtuais do Azure. Este documento fornece informações sobre como conectar tooKafka usando Olá configurações a seguir:

* De recursos em uma rede local. Essa conexão é estabelecida usando um dispositivo VPN (software ou hardware) em sua rede local.
* De um ambiente de desenvolvimento usando um cliente de software VPN.

## <a name="architecture-and-planning"></a>Arquitetura e planejamento

HDInsight não permite a conexão direta tooKafka sobre Olá internet pública. Em vez disso, os clientes Kafka (produtores e consumidores) devem usar um dos Olá métodos de conexão a seguir:

* Execute o cliente de saudação em Olá mesma rede virtual Kafka no HDInsight. Essa configuração é usada em Olá [iniciar com o Apache Kafka (visualização) no HDInsight](hdinsight-apache-kafka-get-started.md) documento. Hello cliente é executado diretamente em Olá HDInsight nós de cluster ou em outra máquina virtual no hello mesma rede.

* Conecte-se a uma rede privada, como a sua rede local, rede virtual toohello. Essa configuração permite que os clientes em seu trabalho de toodirectly de rede local com Kafka. tooenable essa configuração, execute Olá tarefas a seguir:

    1. Crie uma rede virtual.
    2. Crie um gateway de VPN que use uma configuração de site a site. configuração de saudação usada neste documento se conecta tooa dispositivo de gateway VPN na sua rede local.
    3. Crie um servidor DNS na rede virtual hello.
    4. Configure o encaminhamento entre o servidor DNS de saudação em cada rede.
    5. Instale Kafka no HDInsight em rede virtual hello.

    Para obter mais informações, consulte Olá [conectar tooKafka de uma rede local](#on-premises) seção. 

* Conecte-se a rede virtual do toohello máquinas individuais usando um gateway de VPN e o cliente VPN. tooenable essa configuração, execute Olá tarefas a seguir:

    1. Crie uma rede virtual.
    2. Crie um gateway de VPN que use uma configuração de ponto a site. Essa configuração fornece um cliente VPN que pode ser instalado em clientes do Windows.
    3. Instale Kafka no HDInsight em rede virtual hello.
    4. Configure o Kafka para anúncio de IP. Essa configuração permite Olá cliente tooconnect usando em vez de nomes de domínio de endereçamento IP.
    5. Baixar e usar o cliente VPN Olá no sistema de desenvolvimento de saudação.

    Para obter mais informações, consulte Olá [conectar tooKafka com um cliente VPN](#vpnclient) seção.

    > [!WARNING]
    > Essa configuração é recomendada apenas para fins de desenvolvimento devido a saudação seguintes limitações:
    >
    > * Cada cliente deve se conectar usando um cliente de software VPN. O Azure fornece apenas um cliente baseado em Windows.
    > * cliente de saudação não passar nome resolução solicitações toohello rede virtual, você deve usar toocommunicate com Kafka de endereçamento IP. Comunicação de IP requer configuração adicional no cluster Kafka de saudação.

Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Conecte-se tooKafka de uma rede local

toocreate um cluster Kafka que se comunica com a sua rede local, siga as etapas de Olá Olá [HDInsight conectar rede de local de tooyour](./connect-on-premises-network.md) documento.

> [!IMPORTANT]
> Ao criar o cluster do HDInsight hello, selecione Olá __Kafka__ tipo de cluster.

Essas etapas para criar Olá a seguinte configuração:

* Rede Virtual do Azure
* Gateway de VPN site a site
* Conta de Armazenamento do Azure (usada pelo HDInsight)
* Kafka no HDInsight

tooverify que um cliente Kafka pode se conectar a cluster toohello do local, use etapas Olá Olá [exemplo: cliente Python](#python-client) seção.

## <a id="vpnclient"></a>Conecte-se tooKafka com um cliente VPN

Use as etapas de Olá Olá de toocreate essa seção seguinte configuração:

* Rede Virtual do Azure
* Gateway de VPN ponto a site
* Conta de Armazenamento do Azure (usada pelo HDInsight)
* Kafka no HDInsight

1. Siga as etapas de Olá Olá [trabalhar com certificados autoassinados para conexões ponto a site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento. Este documento cria certificados de saudação necessários para o gateway de saudação.

2. Abra um prompt do PowerShell e use Olá toolog de código em tooyour assinatura do Azure a seguir:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Olá Use variáveis de toocreate de código que contêm informações de configuração a seguir:

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

4. Grupo de recursos do Azure Olá toocreate e rede virtual de código a seguir de Olá de uso:

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
    > Pode levar vários minutos para que esse processo toocomplete.

5. Use Olá contêiner de blob e conta de armazenamento do Azure de saudação de toocreate do código a seguir:

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

6. Use Olá cluster do HDInsight de saudação de toocreate de código a seguir:

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
  > Esse processo leva cerca de 20 minutos toocomplete.

8. Use Olá cmdlet tooretrieve Olá URL para o cliente de VPN do Windows hello para rede virtual Olá a seguir:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    cliente de VPN do Windows hello toodownload, use Olá retornado URI no navegador da web.

### <a name="configure-kafka-for-ip-advertising"></a>Configurar Kafka para anúncio de IP

Por padrão, Zookeeper retorna o nome de domínio de saudação do hello Kafka tooclients de agentes. Essa configuração não funciona com hello cliente VPN de software, pois ele não pode usar a resolução de nomes de entidades de rede virtual Olá. Para essa configuração, use o seguinte Olá tooconfigure etapas de endereços IP de tooadvertise Kafka em vez de nomes de domínio:

1. Usando um navegador da web, visite toohttps://CLUSTERNAME.azurehdinsight.net. Substituir __CLUSTERNAME__ com nome Olá Olá Kafka no cluster HDInsight.

    Quando solicitado, use HTTPS Olá nome e uma senha para cluster hello. Olá Ambari Web UI para cluster Olá é exibida.

2. informações de tooview em Kafka, selecione __Kafka__ Olá na lista de saudação esquerda.

    ![Lista de serviços com Kafka realçado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Selecione tooview configuração Kafka, __configurações__ de intermediária superior hello.

    ![Links de Configurações para Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. Olá toofind __kafka env__ configuração, digite `kafka-env` em Olá __filtro__ campo na parte superior direita do hello.

    ![Configuração do Kafka, para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. endereços de IP de tooadvertise Kafka tooconfigure, adicione Olá após o fim do texto toohello de saudação __kafka-env-modelo__ campo:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. interface de saudação de tooconfigure Kafka escuta em, digite `listeners` em Olá __filtro__ campo na parte superior direita do hello.

7. tooconfigure toolisten Kafka em todas as interfaces de rede, alterar o valor de saudação em Olá __ouvintes__ campo muito`PLAINTEXT://0.0.0.0:9092`.

8. alterações de configuração do toosave hello, use Olá __salvar__ botão. Digite uma mensagem de texto que descreve as alterações de saudação. Selecione __Okey__ depois Olá alterações foram salvas.

    ![Botão Salvar configuração](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. erros tooprevent ao reiniciar Kafka, use Olá __ações de serviço__ botão e selecione __ativar no modo de manutenção__. Selecione toocomplete Okey esta operação.

    ![Ações de serviço, com ativar manutenção realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, use Olá __reiniciar__ botão e selecione __reiniciar todos os afetados__. Confirmar reinicialização hello e use Olá __Okey__ botão Olá operação concluída.

    ![Botão Reiniciar com reiniciar todos os afetados realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. toodisable modo de manutenção, use Olá __ações de serviço__ botão e selecione __ativar desativar o modo de manutenção__. Selecione **Okey** toocomplete esta operação.

### <a name="connect-toohello-vpn-gateway"></a>Conecte-se o gateway VPN toohello

tooconnect toohello gateway VPN de um __cliente Windows__, use Olá __conectar tooAzure__ seção Olá [configurar uma conexão ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.

## <a id="python-client"></a> Exemplo: cliente do Python

toovalidate tooKafka de conectividade, use Olá toocreate as etapas a seguir e execute um produtor de Python e consumidor:

1. Usar um dos Olá Olá de tooretrieve métodos a seguir totalmente qualificado (FQDN) do nome de domínio e endereços IP de nós Olá Olá cluster Kafka:

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

    Esse script presume que `$resourceGroupName` é nome Olá Olá do Azure do grupo de recursos que contém a rede virtual hello.

    Salve Olá retornada informações para uso nas próximas etapas hello.

2. Olá Use tooinstall Olá a seguir [kafka python](http://kafka-python.readthedocs.io/) cliente:

        pip install kafka-python

3. toosend dados tooKafka, use Olá código Python a seguir:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Substituir saudação `'kafka_broker'` entradas com endereços hello retornadas da etapa 1 nesta seção:

    * Se você estiver usando um __cliente VPN de Software__, substitua Olá `kafka_broker` entradas com o endereço IP de saudação de seus nós de trabalho.

    * Se você tiver __habilitada a resolução de nomes por meio de um servidor DNS personalizado__, substitua Olá `kafka_broker` entradas com hello FQDN Olá de nós de trabalho.

    > [!NOTE]
    > Esse código envia a cadeia de caracteres de saudação `test message` toohello tópico `testtopic`. configuração de padrão de saudação do Kafka no HDInsight é tópico de saudação toocreate se ele não existe.

4. mensagens de saudação do tooretrieve de Kafka, use Olá código Python a seguir:

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

    Substituir saudação `'kafka_broker'` entradas com endereços hello retornadas da etapa 1 nesta seção:

    * Se você estiver usando um __cliente VPN de Software__, substitua Olá `kafka_broker` entradas com o endereço IP de saudação de seus nós de trabalho.

    * Se você tiver __habilitada a resolução de nomes por meio de um servidor DNS personalizado__, substitua Olá `kafka_broker` entradas com hello FQDN Olá de nós de trabalho.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o HDInsight com uma rede virtual, consulte Olá [estender o Azure HDInsight usando uma rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

Para obter mais informações sobre como criar uma rede Virtual do Azure com o gateway VPN ponto a Site, consulte Olá documentos a seguir:

* [Configurar uma conexão ponto a Site usando Olá portal do Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configurar uma conexão Ponto a Site usando o Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Para obter mais informações sobre como trabalhar com Kafka no HDInsight, consulte Olá documentos a seguir:

* [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)
* [Usar o espelhamento com o Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)
