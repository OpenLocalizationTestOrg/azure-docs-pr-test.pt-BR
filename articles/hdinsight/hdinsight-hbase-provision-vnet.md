---
title: aaaCreate HBase clusters em uma rede Virtual - Azure | Microsoft Docs
description: "Introdução ao uso do HBase no Azure HDInsight. Saiba como toocreate HDInsight HBase clusters na rede Virtual do Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Criar clusters HBase no HDInsight na Rede Virtual do Azure
Saiba como clusters de toocreate do Azure HDInsight HBase um [rede Virtual do Azure][1].

Com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que aplicativos podem se comunicar com HBase diretamente. Olá benefícios incluem:

* Conectividade direta Olá web toohello de nós de aplicativos de cluster HBase hello, o que permite a comunicação por meio do procedimento remoto HBase Java chamar APIs de (RPC).
* Desempenho aprimorado, evitando que o tráfego percorra diversos gateways e balanceadores de carga.
* Olá capacidade tooprocess informações confidenciais de forma mais segura sem expor um ponto de extremidade público.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter Olá itens a seguir:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Uma estação de trabalho com o PowerShell do Azure**. Consulte [Instalar e usar o PowerShell do Azure](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Criar clusters do HBase na rede virtual
Nesta seção, você criará um cluster HBase baseados em Linux com conta de armazenamento do Azure dependente Olá em uma rede virtual do Azure usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Para outros métodos de criação de cluster e Noções básicas sobre configurações de hello, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md). Para obter mais informações sobre como usar um modelo toocreate Hadoop clusters de HDInsight, consulte [Hadoop criar clusters de HDInsight usando modelos do Gerenciador de recursos do Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Algumas propriedades são embutidos em código no modelo de saudação. Por exemplo:
>
> * **Local**: Leste dos EUA 2
> * **Versão do cluster**: 3.5
> * **Contagem de nós de trabalho do cluster:** 2
> * **Conta de armazenamento padrão**: uma cadeia de caracteres exclusiva
> * **Nome da rede virtual**:&lt; Nome do cluster > -vnet
> * **Espaço de endereço da rede virtual**: 10.0.0.0/16
> * **Nome da sub-rede**: subnet1
> * **Intervalo de endereços da sub-rede**: 10.0.0.0/24
>
> &lt;Nome do cluster > é substituído pelo nome do cluster Olá fornecem ao usar o modelo de saudação.
>
>

1. Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure. Olá modelo está localizado em [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De saudação **implantação personalizada** folha, digite Olá propriedades a seguir:

   * **Assinatura**: selecione um cluster HDInsight do Azure assinatura usada toocreate hello, Olá dependente conta de armazenamento e Olá rede virtual do Azure.
   * **Grupo de recursos**: selecione **Criar novo** e especifique um novo nome do grupo de recursos.
   * **Local**: selecione um local para o grupo de recursos de saudação.
   * **ClusterName**: insira um nome para toobe de cluster de Hadoop Olá criado.
   * **Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.
   * **SSH username e password**: nome de usuário saudação padrão é **sshuser**.  Você pode renomeá-lo.
   * **Eu concordo toohello termos e condições de saudação declaradas acima**: (Selecionar)
3. Clique em **Comprar**. Demora cerca de aproximadamente 20 minutos toocreate um cluster. Depois de criar o cluster hello, você pode clicar em folha de cluster Olá em tooopen portal Olá-lo.

Depois de concluir o tutorial hello, talvez você queira toodelete cluster de saudação. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso. Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso. Para obter instruções de saudação da exclusão de um cluster, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin trabalhando com seu novo cluster HBase, você pode usar os procedimentos de saudação encontrados no [iniciar o uso do HBase com Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Conectar-se o cluster do HBase toohello usando APIs de RPC de Java do HBase
1. Criar uma infraestrutura como serviço (IaaS) máquina virtual em Olá mesma rede virtual do Azure e Olá mesma sub-rede. Para obter instruções sobre como criar uma máquina virtual IaaS, confira [Criar uma máquina virtual executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Ao seguir as etapas de saudação neste documento, você deve usar Olá valores para a configuração de rede Olá a seguir:

   * **Rede virtual**:&lt; Nome do cluster > -vnet
   * **Sub-rede**: subnet1

   > [!IMPORTANT]
   > Substituir &lt;nome do Cluster > com o nome da saudação usados ao criar o cluster do HDInsight Olá nas etapas anteriores.
   >
   >

   Usando esses valores, Olá máquina virtual é colocada no hello mesma rede virtual e a sub-rede do cluster do HDInsight hello. Essa configuração permite que eles toodirectly se comunicar entre si. Há uma maneira toocreate um cluster HDInsight com um nó de borda vazia. nó de borda Olá pode ser o cluster de saudação do toomanage usado.  Para saber mais, confira [Usar nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md).

2. Ao usar um tooHBase de tooconnect de aplicativo Java remotamente, você deve usar o nome de domínio totalmente qualificado da saudação (FQDN). toodetermine isso, você deve obter o sufixo DNS específico da conexão saudação do cluster do HBase hello. toodo que, você pode usar um dos métodos a seguir de saudação:

   * Use um navegador de Web toomake uma chamada de Ambari:

     Procurar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hospeda? minimal_response = true. Na verdade, um arquivo JSON com sufixos DNS hello.
   * Use Olá Ambari site:

     1. Procurar muito https://&lt;ClusterName >. n e t.
     2. Clique em **Hosts** no menu superior hello.
   * Use chamadas REST ondulação toomake:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Em Olá dados JSON JavaScript Object Notation () retornado, localizar a entrada de "host_name" hello. Ele contém Olá FQDN para nós de saudação em cluster hello. Por exemplo:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     parte de saudação do hello domínio nome que começa com o nome do cluster Olá é sufixo DNS hello. Por exemplo, mycluster.b1.cloudapp.net.
   * Usar PowerShell do Azure

     Saudação de uso após a saudação de tooregister de script do PowerShell do Azure **ClusterDetail Get** função, que pode ser o sufixo DNS usado tooreturn hello:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Depois de script do PowerShell do Azure Olá em execução, use Olá comando a seguir sufixo DNS Olá tooreturn usando Olá **ClusterDetail Get** função. Especifique o nome do cluster do HBase do HDInsight, o nome e a senha do administrador ao usar esse comando.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Esse comando retorna o sufixo DNS hello. Por exemplo, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify que Olá máquina virtual pode se comunicar com hello cluster HBase, use o comando Olá `ping headnode0.<dns suffix>` da máquina virtual de saudação. Por exemplo, envie ping a headnode0.mycluster.b1.cloudapp.net.

toouse essas informações em um aplicativo Java, você pode seguir etapas Olá [usar Maven toobuild os aplicativos Java que usa HBase com HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate um aplicativo. aplicativo de hello toohave conectar o servidor remoto de HBase tooa, modifique Olá **hbase-site.XML** Zookeeper no arquivo na saudação de toouse exemplo FQDN. Por exemplo:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Para obter mais informações sobre resolução de nomes em redes virtuais do Azure, incluindo como toouse seu próprio servidor DNS, consulte [resolução de nomes (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate um cluster HBase. toolearn mais, consulte:

* [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Usar nós de borda vazios no HDInsight](hdinsight-apps-use-edge-node.md)
* [Configurar a replicação do HBase no HDInsight](hdinsight-hbase-replication.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Introdução ao uso do HBase com Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Analisar dados de sentimento no Twitter com o HBase no HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Visão geral da Rede Virtual][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalhes de provisionar novo cluster de HBase Olá"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Use a ação de Script toocustomize um cluster HBase"

[azure-preview-portal]: https://portal.azure.com
