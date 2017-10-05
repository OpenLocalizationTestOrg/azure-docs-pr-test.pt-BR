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
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure

Saiba como se conectar diretamente ao Kafka no HDInsight usando Redes Virtuais do Azure. Este documento fornece informações sobre como se conectar ao Kafka usando as seguintes configurações:

* De recursos em uma rede local. Essa conexão é estabelecida usando um dispositivo VPN (software ou hardware) em sua rede local.
* De um ambiente de desenvolvimento usando um cliente de software VPN.

## <a name="architecture-and-planning"></a>Arquitetura e planejamento

O HDInsight não permite a conexão direta ao Kafka pela Internet pública. Em vez disso, os clientes Kafka (produtores e consumidores) devem usar um dos seguintes métodos de conexão:

* Execute o cliente na mesma rede virtual que o Kafka no HDInsight. Essa configuração é usada no documento [Introdução ao Apache Kafka (versão prévia) no HDInsight](hdinsight-apache-kafka-get-started.md). O cliente é executado diretamente em nós do cluster HDInsight ou em outra máquina virtual na mesma rede.

* Conecte uma rede privada, como a sua rede local, à rede virtual. Essa configuração permite que os clientes na rede local trabalhem diretamente com o Kafka. Para habilitar essa configuração, execute as seguintes tarefas:

    1. Crie uma rede virtual.
    2. Crie um gateway de VPN que use uma configuração de site a site. A configuração usada neste documento se conecta a um dispositivo de gateway de VPN na rede local.
    3. Crie um servidor DNS na rede virtual.
    4. Configure o encaminhamento entre o servidor DNS em cada rede.
    5. Instale o Kafka no HDInsight na rede virtual.

    Para obter mais informações, consulte a seção [Conectar-se ao Kafka de uma rede local](#on-premises). 

* Conecte computadores individuais à rede virtual usando um gateway de VPN e um cliente VPN. Para habilitar essa configuração, execute as seguintes tarefas:

    1. Crie uma rede virtual.
    2. Crie um gateway de VPN que use uma configuração de ponto a site. Essa configuração fornece um cliente VPN que pode ser instalado em clientes do Windows.
    3. Instale o Kafka no HDInsight na rede virtual.
    4. Configure o Kafka para anúncio de IP. Essa configuração permite ao cliente conectar-se usando o endereçamento IP em vez de nomes de domínio.
    5. Baixe e use o cliente VPN no sistema de desenvolvimento.

    Para obter mais informações, consulte a seção [Conectar-se ao Kafka com um cliente VPN](#vpnclient).

    > [!WARNING]
    > Essa configuração é recomendada apenas para fins de desenvolvimento devido às seguintes limitações:
    >
    > * Cada cliente deve se conectar usando um cliente de software VPN. O Azure fornece apenas um cliente baseado em Windows.
    > * O cliente não passar solicitações de resolução de nome para a rede virtual, então você deve usar endereçamento IP para se comunicar com o Kafka. A comunicação de IP requer configuração adicional no cluster Kafka.

Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a> Conectar-se ao Kafka de uma rede local

Para criar um cluster Kafka que se comunique com a rede local, siga as etapas no documento [Conectar o HDInsight à rede local](./connect-on-premises-network.md).

> [!IMPORTANT]
> Ao criar o cluster HDInsight, selecione o tipo de cluster __Kafka__.

Essas etapas criam a configuração a seguir:

* Rede Virtual do Azure
* Gateway de VPN site a site
* Conta de Armazenamento do Azure (usada pelo HDInsight)
* Kafka no HDInsight

Para verificar se um cliente Kafka pode se conectar ao cluster local, use as etapas na seção [Exemplo: cliente do Python](#python-client).

## <a id="vpnclient"></a> Conectar-se ao Kafka com um cliente VPN

Use as etapas nesta seção para criar a seguinte configuração:

* Rede Virtual do Azure
* Gateway de VPN ponto a site
* Conta de Armazenamento do Azure (usada pelo HDInsight)
* Kafka no HDInsight

1. Siga as etapas no documento [Trabalhando com certificados autoassinados para conexões de ponto a site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md). Esse documento cria os certificados necessários para o gateway.

2. Abra um prompt do PowerShell e use o seguinte código para fazer logon em sua assinatura do Azure:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Use o seguinte código para criar variáveis que contenham informações de configuração:

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

4. Use o seguinte código para criar o grupo de recursos do Azure e a rede virtual:

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
    > Esse processo pode demorar para ser concluído.

5. Use o seguinte código para criar a Conta de Armazenamento do Azure e o contêiner de blob:

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

6. Use o seguinte código para criar o cluster HDInsight:

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
  > Esse processo leva cerca de 20 minutos para ser concluído.

8. Use o seguinte cmdlet para recuperar a URL do cliente VPN do Windows para a rede virtual:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    Para baixar o cliente VPN do Windows, use o URI retornado no navegador da Web.

### <a name="configure-kafka-for-ip-advertising"></a>Configurar Kafka para anúncio de IP

Por padrão, o Zookeeper retorna o nome de domínio dos agentes do Kafka aos clientes. Essa configuração não funciona com o cliente de software VPN, pois não é possível usar a resolução de nomes para entidades na rede virtual. Para essa configuração, use as seguintes etapas para configurar o Kafka a fim de anunciar endereços IP no lugar de nomes de domínio:

1. Usando um navegador da Web, acesse https://NOMEDOCLUSTER.azurehdinsight.net. Substitua __NOMEDOCLUSTER__ pelo nome do Kafka no cluster HDInsight.

    Quando solicitado, use o nome de usuário e a senha HTTPS para o cluster. A Interface de Usuário Ambari Web para o cluster é exibida.

2. Para exibir informações sobre o Kafka, selecione __Kafka__ na lista à esquerda.

    ![Lista de serviços com Kafka realçado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Para exibir a configuração do Kafka, selecione __Configurações__ na parte central superior.

    ![Links de Configurações para Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. Para localizar a configuração __kafka-env__, digite `kafka-env` no campo __Filtro__ na parte superior direita.

    ![Configuração do Kafka, para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. Para configurar o Kafka para anunciar endereços IP, adicione o seguinte texto à parte inferior do campo __kafka-env-template__:

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. Para configurar a interface na qual o Kafka escuta, digite `listeners` no campo __Filtro__ na parte superior direita.

7. Para configurar o Kafka para escutar em todas as interfaces de rede, altere o valor no campo __ouvintes__ para `PLAINTEXT://0.0.0.0:9092`.

8. Para salvar as alterações de configuração, use o botão __Salvar__. Digite uma mensagem de texto que descreva as alterações. Selecione __OK__ assim que as alterações tiverem sido salvas.

    ![Botão Salvar configuração](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. Para evitar erros ao reiniciar o Kafka, use o botão __Ações de Serviço__ e selecione __Ativar o Modo de Manutenção__. Selecione OK para concluir essa operação.

    ![Ações de serviço, com ativar manutenção realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. Para reiniciar o Kafka, use o botão __Reiniciar__ e selecione __Reiniciar Todos os Afetados__. Confirme a reinicialização e, em seguida, use o botão __OK__ depois que a operação for concluída.

    ![Botão Reiniciar com reiniciar todos os afetados realçada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. Para desabilitar o modo de manutenção, use o botão __Ações de Serviço__ e selecione __Ativar o Modo de Manutenção__. Selecione **OK** para concluir essa operação.

### <a name="connect-to-the-vpn-gateway"></a>Conectar-se ao gateway de VPN

Para se conectar ao gateway de VPN usando um __cliente Windows__, use a seção __Conectar ao Azure__ do documento [Configurar uma conexão Ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).

## <a id="python-client"></a> Exemplo: cliente do Python

Para validar a conectividade com o Kafka, use as etapas a seguir para criar e executar um produtor e consumidor de Python:

1. Use um dos seguintes métodos para recuperar o FQDN (nome de domínio totalmente qualificado) e os endereços IP dos nós no cluster Kafka:

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

    Esse script supõe que `$resourceGroupName` seja o nome do grupo de recursos do Azure que contém a rede virtual.

    Salve as informações retornadas para uso nas próximas etapas.

2. Use o seguinte para instalar o cliente [kafka-python](http://kafka-python.readthedocs.io/):

        pip install kafka-python

3. Para enviar dados ao Kafka, use o seguinte código Python:

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Substitua as entradas `'kafka_broker'` pelos endereços retornados da etapa 1 nesta seção:

    * Se você estiver usando um __cliente VPN de software__, substitua as entradas `kafka_broker` pelo endereço IP de seus nós de trabalho.

    * Se você tiver __habilitado a resolução de nomes por meio de um servidor DNS personalizado__, substitua as entradas `kafka_broker` pelo FQDN dos nós de trabalho.

    > [!NOTE]
    > Esse código envia a cadeia de caracteres `test message` para o tópico `testtopic`. A configuração padrão do Kafka no HDInsight é criar o tópico se ele não existir.

4. Para recuperar as mensagens do Kafka, use o seguinte código Python:

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

    Substitua as entradas `'kafka_broker'` pelos endereços retornados da etapa 1 nesta seção:

    * Se você estiver usando um __cliente VPN de software__, substitua as entradas `kafka_broker` pelo endereço IP de seus nós de trabalho.

    * Se você tiver __habilitado a resolução de nomes por meio de um servidor DNS personalizado__, substitua as entradas `kafka_broker` pelo FQDN dos nós de trabalho.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o HDInsight com uma redes virtual, veja o documento [Estender o Azure HDInsight usando uma Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).

Para saber mais sobre como criar uma Rede Virtual do Azure com o gateway de VPN Ponto a Site, confira os seguintes documentos:

* [Configurar uma conexão Ponto a Site usando o portal do Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configurar uma conexão Ponto a Site usando o Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Para saber mais sobre como trabalhar com o Kafka no HDInsight, veja os seguintes documentos:

* [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)
* [Usar o espelhamento com o Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)
