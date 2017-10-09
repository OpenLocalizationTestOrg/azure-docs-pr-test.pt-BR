---
title: "replicação de cluster HBase aaaConfigure dentro das redes virtuais - Azure | Microsoft Docs"
description: "Saiba como tooconfigure HBase replicação para balanceamento de carga e alta disponibilidade, sem tempo de inatividade migração/atualização de um tooanother de versão do HDInsight e recuperação de desastres."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Configurar a replicação de cluster HBase dentro das redes virtuais

Saiba como tooconfigure HBase replicação em uma rede virtual (VNet) ou entre duas redes virtuais.

A replicação de cluster usa uma metodologia de envio de origem. Um cluster HBase pode ser uma fonte, um destino ou pode atender a ambas as funções de uma vez. A replicação é assíncrona e objetivo de saudação de replicação é consistência eventual. Quando origem Olá recebe uma família de coluna Editar tooa com replicação habilitada, essa edição é propagado tooall clusters de destino. Quando dados são replicados de um tooanother de cluster, cluster de origem hello e todos os clusters que já consumiram dados saudação são controladas tooprevent loops de replicação.

Neste tutorial, você configurará uma replicação de origem/destino. Para obter outras topologias de cluster, consulte o [Guia de referência do Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

Casos de uso de replicação de HBase para uma única rede virtual:

* O balanceamento de carga – por exemplo, executando verificações ou trabalhos MapReduce no cluster de destino hello e ingestão de dados no cluster de origem Olá
* Alta disponibilidade
* Migração de dados de um tooanother de cluster HBase
* Atualizando um cluster Azure HDInsight de um tooanother de versão

Casos de uso de replicação de HBase para duas redes virtuais:

* Recuperação de desastre
* Balanceamento de carga e particionamento aplicativo hello
* Alta disponibilidade

Replicar clusters usando scripts [ação de script](hdinsight-hadoop-customize-cluster-linux.md) localizados no [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deverá ter uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Configurar ambientes de saudação

Há três opções de configuração possíveis:

- Dois clusters de HBase em uma rede virtual do Azure
- Dois clusters HBase em duas redes virtuais diferentes no hello mesma região
- Dois clusters de HBase em duas redes virtuais diferentes em duas regiões diferentes (replicação geográfica)

toomake-ambientes de saudação tooconfigure mais fácil, criamos alguns [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Se você preferir ambientes de saudação tooconfigure usando outros métodos, consulte:

- [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Criar clusters HBase na rede virtual do Azure](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Configurar uma rede virtual

Clique em Olá imagem toocreate dois clusters HBase em Olá a seguir mesma rede virtual. Olá está armazenado na [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Configurar duas redes virtuais no hello mesma região

Clique em Olá imagem toocreate duas redes virtuais com o emparelhamento de rede virtual e dois clusters HBase em Olá a seguir mesma região. Olá está armazenado na [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Esse cenário requer o [emparelhamento VNet](../virtual-network/virtual-network-peering-overview.md). modelo de saudação permite o emparelhamento de rede virtual.   

A replicação do HBase usa endereços IP de saudação ZooKeeper VMs. Você deve configurar endereços IP estáticos para nós de HBase ZooKeeper de destino hello.

**endereços IP estáticos tooconfigure**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **grupos de recursos**.
3. Clique em seu grupo de recursos que contém Olá destino HBase cluster. Este é o grupo de recursos de saudação que você especificou quando você usou o ambiente de saudação toocreate do modelo de Gerenciador de recursos de saudação. Você pode usar o hello toonarrow de filtro para baixo na lista de saudação. Você pode ver uma lista de recursos que contém duas redes virtuais de saudação.
4. Clique em Olá rede virtual que contenha Olá destino HBase cluster. Por exemplo, clique em **xxxx-vnet2**. É possível ver três dispositivos com nomes que começam com **nic-zookeepermode-**. Esses dispositivos são Olá três ZooKeeper VMs.
5. Clique em uma saudação ZooKeeper VMs.
6. Clique em **Configurações de IP**.
7. Clique em **ipConfig1** na lista de saudação.
8. Clique em **estático**e anote o endereço IP real de saudação. Você precisará de endereço IP hello quando você executa a replicação de tooenable de ação de script hello.

  ![IP estático do ZooKeeper para replicação de HBase no HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Repita a etapa 6 tooset Olá endereço IP para Olá outros dois nós ZooKeeper.

Para o cenário de rede entre hello, você deve usar o hello **- ip** alternar ao chamar hello **hdi_enable_replication.sh** ação de script.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Configurar duas redes virtuais em duas regiões diferentes

Clique em Olá seguinte imagem toocreate duas redes virtuais em duas regiões diferentes. Olá modelo é armazenado em um contêiner de Blob do Azure público.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Crie um gateway VPN entre duas redes virtuais de saudação. Para obter instruções, veja [Criar uma VNet com uma conexão site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

A replicação do HBase usa endereços IP de saudação ZooKeeper VMs. Você deve configurar endereços IP estáticos para nós de HBase ZooKeeper de destino hello. tooconfigure IP estático, consulte a seção "configurar duas redes virtuais Olá mesma região" hello neste artigo.

Para o cenário de rede entre hello, você deve usar o hello **- ip** alternar ao chamar hello **hdi_enable_replication.sh** ação de script.

## <a name="load-test-data"></a>Carregar dados de teste

Quando você replica um cluster, você deve especificar Olá tabelas tooreplicate. Nesta seção, você irá carregar alguns dados em cluster de origem de saudação. Na próxima seção, Olá, você habilitará a replicação entre dois clusters de saudação.

Siga as instruções de saudação em [HBase tutorial: começar a usar o Apache HBase com Hadoop baseado em Linux no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate um **contatos** tabela e insira alguns dados na tabela hello.

## <a name="enable-replication"></a>Habilitar a replicação

Olá, as etapas a seguir mostra como toocall Olá script de ação de script de saudação portal do Azure. Para executar uma ação de script usando o PowerShell do Azure e hello interface de linha de comando (CLI) do Azure, consulte [HDInsight baseados em Linux personalizar clusters usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md).

**replicação do HBase tooenable de saudação portal do Azure**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Abra o cluster do hello fonte HBase.
3. No menu de cluster hello, clique em **ações de Script**.
4. Clique em **Enviar nova** da parte superior da saudação da folha de saudação.
5. Selecione ou insira Olá informações a seguir:

  - **Nome**: insira **Habilitar a replicação**.
  - **URL do Script Bash**: insira **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **Cabeçalho**: selecionado. Olá desmarque os outros tipos de nó.
  - **Parâmetros**: seguinte Olá parâmetros habilitar replicação para todas as tabelas existentes de saudação de exemplo e copiar todos os dados de saudação do cluster de destino toohello do cluster de origem hello:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Clique em **Criar**. script Hello pode levar algum tempo, especialmente quando o argumento de copydata - Olá é usado.

Argumentos necessários:

|Nome|Descrição|
|----|-----------|
|-s, --src-cluster | Especifique o nome DNS de saudação do cluster do hello fonte HBase. Por exemplo: -s hbsrccluster, --src-cluster=hbsrccluster |
|-d, --dst-cluster | Especifique o nome DNS de saudação do destino hello (réplica) cluster HBase. Por exemplo: -s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | Especifica senha do administrador Olá para Ambari no cluster do hello origem HBase. |
|-dp, --dst-ambari-password | Especifica senha do administrador Olá para Ambari no cluster do hello destino HBase.|

Argumentos opcionais:

|Nome|Descrição|
|----|-----------|
|-su, --src-ambari-user | Especifique o nome de usuário de administrador de Olá para Ambari no cluster do hello origem HBase. valor padrão de saudação é **admin**. |
|-du, --dst-ambari-user | Especifique o nome de usuário de administrador de Olá para Ambari no cluster do hello destino HBase. valor padrão de saudação é **admin**. |
|-t, --table-list | Especifique Olá toobe de tabelas replicada. Por exemplo: --table-list="table1;table2;table3". Se você não especificar tabelas, todas as tabelas HBase existentes serão replicadas.|
|-m, --machine | Especifique o nó principal Olá onde a ação de script hello será executado. valor de saudação é hn1 ou hn0. Como hn0 geralmente está mais ocupado, é recomendável usar hn1. Você usar essa opção quando você estiver executando o script hello $0 como uma ação de script do portal de HDInsight hello ou o Azure PowerShell.|
|-ip | Esse argumento é necessário quando você estiver habilitando a replicação entre duas redes virtuais. Esse argumento atua como um comutador toouse Olá estático IPs de ZooKeeper nós de clusters de réplica em vez de nomes FQDN. Olá estático IPs necessário toobe pré-configurado antes de habilitar a replicação. |
|-cp, -copydata | Habilite a migração de saudação dos dados existentes nas tabelas de saudação em que a replicação está habilitada. |
|-rpm, -replicate-phoenix-meta | Habilite a replicação nas tabelas do sistema Phoenix. <br><br>*Use esta opção com cuidado.* É recomendável que você recrie tabelas Phoenix em clusters de réplica antes de usar esse script. |
|-h, --help | Exibir informações de uso. |

Olá Olá seção print_usage() [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fornece uma explicação detalhada de parâmetros.

Após a ação de script hello com êxito implantado, você pode usar SSH tooconnect toohello destino HBase cluster e verificar dados saudação foi replicados.

### <a name="replication-scenarios"></a>Cenários de replicação

Olá lista a seguir mostra alguns casos de uso geral e suas configurações de parâmetro:

- **Habilitar a replicação em todas as tabelas entre clusters Olá dois**. Esse cenário não requer Olá/migração com cópia dos dados existentes nas tabelas de saudação e não usa tabelas Phoenix. Use Olá parâmetros a seguir:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Habilitar a replicação em tabelas específicas**. Use Olá seguindo a replicação tooenable parâmetros na table1, table2 e Tabela3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Habilitar a replicação em tabelas específicas e copie os dados existentes Olá**. Use Olá seguindo a replicação tooenable parâmetros na table1, table2 e Tabela3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Habilitar a replicação em todas as tabelas com replicando phoenix metadados de origem toodestination**. A replicação de metadados Phoenix não é ideal e deve ser habilitada com cuidado.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Copiar e migrar dados

Há dois scripts de ação de script separados para copiar/migrar dados após a replicação ser habilitada:

- [Script para tabelas pequenas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (alguns gigabytes de tamanho e geral cópia é toofinish esperado em menos de uma hora)

- [Script para tabelas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (esperado tootake mais de uma hora toocopy)

Você pode seguir Olá mesmo procedimento no [habilitar replicação](#enable-replication) toocall ação de script hello com hello parâmetros a seguir:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Olá Olá seção print_usage() [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fornece uma descrição detalhada dos parâmetros.

### <a name="scenarios"></a>Cenários

- **Copiar tabelas específicas (test1, test2 e test3) para todas as linhas editadas até o momento (carimbo de hora atual)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  ou o

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Copiar tabelas específicas com intervalo de tempo especificado**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Desabilitar a replicação

replicação toodisable, você usa outro script de ação de script localizado em [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Você pode seguir Olá mesmo procedimento no [habilitar replicação](#enable-replication) toocall ação de script hello com hello parâmetros a seguir:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Olá Olá seção print_usage() [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fornece uma explicação detalhada de parâmetros.

### <a name="scenarios"></a>Cenários

- **Desabilitar a replicação em todas as tabelas**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  ou o

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Desabilitar a replicação em tabelas específicas (table1, table2 e table3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como tooconfigure HBase replicação entre dois datacenters. toolearn mais sobre o HDInsight e HBase, consulte:

* [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started]
* [Visão geral do HDInsight HBase][hdinsight-hbase-overview]
* [Criar clusters HBase na rede virtual do Azure][hdinsight-hbase-provision-vnet]
* [Analisar o sentimento do Twitter em tempo real com o HBase][hdinsight-hbase-twitter-sentiment]
* [Analisar dados de sensor com o Storm e o HBase no HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
