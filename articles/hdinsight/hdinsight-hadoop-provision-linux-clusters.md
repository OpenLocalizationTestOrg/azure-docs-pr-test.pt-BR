---
title: "instalação de aaaCluster para Hadoop, Spark, Kafka, HBase ou R Server - HDInsight do Azure | Microsoft Docs"
description: "Configure clusters de Hadoop, Kafka, Spark, HBase, R Server ou Storm para HDInsight de um navegador, Olá CLI do Azure, do PowerShell do Azure, REST ou SDK."
keywords: "instalação de cluster hadoop, instalação de cluster kafka, instalação de cluster spark, o que é um cluster no hadoop"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Configurar clusters no HDInsight com Hadoop, Spark, Kafka e mais

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Saiba como tooset e configurar os clusters de HDInsight com Hadoop, Spark, Kafka, Hive interativo, HBase, R Server ou Storm. Além disso, saiba como toocustomize clusters e adicione segurança unindo-los tooa domínio.

Um cluster Hadoop é composto por várias máquinas virtuais (nós), usadas para processamento distribuído de tarefas. HDInsight do Azure trata os detalhes de implementação de instalação e configuração de nós individuais, para que você tenha apenas informações de configuração geral de tooprovide. 

> [!IMPORTANT]
>A cobrança de cluster HDInsight começa quando um cluster é criado e é interrompido quando o cluster Olá é excluído. A cobrança ocorre por minuto, portanto, sempre exclua o cluster quando ele não estiver mais sendo usado. Saiba como muito[excluir um cluster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Métodos de instalação de cluster
Olá tabela a seguir mostra métodos diferentes de saudação que você pode usar tooset backup de um cluster HDInsight.

| Clusters criados com | Navegador da Web | Linha de comando | API REST | . | 
| --- |:---:|:---:|:---:|:---:|
| [Portal do Azure](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [PowerShell do Azure](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Curl](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [SDK .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Modelos do Gerenciador de Recursos do Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Criação rápida: instalação de cluster Básico
Este artigo o orienta por meio da instalação no hello [portal do Azure](https://portal.azure.com), onde você pode criar um cluster HDInsight usando *criação rápida* ou *personalizado*. 

Siga as instruções em Olá tela toodo uma instalação de cluster básico. Os detalhes são fornecidos abaixo para:

* [Nome do grupo de recursos](#resource-group-name)
* [Tipos de cluster e configuração](#cluster-types) 
* [Logon de cluster e o nome de usuário SSH](#cluster-login-and-ssh-username)
* [Localidade](#location)

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight 3.3).
>

## <a name="resource-group-name"></a>Nome do grupo de recursos 

[Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) ajuda você a trabalhar com recursos de saudação em seu aplicativo como um grupo, chamado tooas um grupo de recursos do Azure. Você pode implantar, atualizar, monitorar ou excluir todos os recursos de saudação para seu aplicativo em uma única operação de coordenada.

## <a name="cluster-types"></a> Tipos de cluster e configuração
HDInsight do Azure atualmente fornece a seguinte Olá certas funcionalidades de tipos, cada um com um conjunto de componentes tooprovide cluster.

> [!IMPORTANT]
> Clusters HDInsight estão disponíveis em vários tipos, cada um para uma carga de trabalho ou tecnologia distinta. Não há nenhum método com suporte toocreate um cluster que combina vários tipos, como Storm e HBase em um cluster. Se sua solução requer tecnologias que são distribuídas entre vários tipos de cluster HDInsight, uma [rede virtual do Azure](https://docs.microsoft.com/azure/virtual-network) pode se conectar a tipos de cluster Olá necessário. 
>
>

| Tipo de cluster | Funcionalidade |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Consulta de Lote e a análise de dados armazenados |
| [HBase](hdinsight-hbase-overview.md) |Processamento de grandes quantidades de dados NoSQL sem esquema |
| [Storm](hdinsight-storm-overview.md) |Processamento de eventos em tempo real |
| [Spark](hdinsight-apache-spark-overview.md) |Processamento na memória, consultas interativas, processamento de transmissão de microlotes |
| [Kafka (Visualização)](hdinsight-apache-kafka-introduction.md) | Uma plataforma de streaming distribuída que pode ser usado toobuild pipelines de dados de streaming em tempo real e aplicativos |
| [Servidor R](hdinsight-hadoop-r-server-overview.md) |Uma variedade de recursos de estatísticas de Big Data, modelagem preditiva e aprendizado de máquina |
| [Hive Interativo (Visualização)](hdinsight-hadoop-use-interactive-hive.md) |Caching na memória para consultas de Hive interativas e mais rápidas |

### <a name="number-of-nodes-for-each-cluster-type"></a>Número de nós para cada tipo de cluster
Cada tipo de cluster tem seu próprio número de nós, terminologia para nós no cluster e tamanho da VM padrão. Olá a tabela a seguir, número de saudação de nós para cada tipo de nó é entre parênteses.

| Tipo | Nós | Diagrama |
| --- | --- | --- |
| O Hadoop |Nó de cabeçalho (2), Nó de dados (1+) |![Nós de cluster Hadoop do HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Servidor de cabeçalho (2), Servidor de região (1 +), Nó mestre/do ZooKeeper (3) |![Nós de cluster HBase do HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nó do Nimbus (2), Servidor do supervisor (1+), Nó do ZooKeeper (3) |![Nós de cluster Storm do HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Nó de cabeçalho (2), nó de trabalho (1+), nó do ZooKeeper (3) (gratuito para tamanho de VM A1 do ZooKeeper) |![Nós de cluster Spark do HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Para obter mais informações, consulte [padrão tamanhos de máquina virtual e a configuração de nó para clusters](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) em "O que são componentes do Hadoop hello e as versões em HDInsight?"

### <a name="hdinsight-version"></a>Versão do HDInsight
Escolha a versão de saudação do HDInsight para este cluster. Para saber mais, confira [Versões do HDInsight com suporte](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Camada do cluster: camadas de serviço do HDInsight

HDInsight do Azure fornece ofertas de nuvem Olá grandes dados em duas camadas de serviço: Standard e Premium.  Para obter mais informações, consulte [HDInsight Standard e HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Olá seguinte captura de tela mostra Olá informações sobre o portal do Azure para escolher os tipos de cluster.

![Configuração do HDInsight premium](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Logon de cluster e o nome de usuário SSH
Com os clusters HDInsight, você pode configurar duas contas de usuário durante a criação de cluster:

* Usuário HTTP: nome de usuário padrão Olá é *admin*. Ele usa a configuração básica da saudação no hello portal do Azure. Às vezes, ele é chamado "Usuário de cluster".
* Usuário SSH (Linux clusters): tooconnect usado toohello cluster por meio do SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Local (regiões) para armazenamento e clusters

Você não precisa local do cluster Olá toospecify explicitamente: Olá cluster está Olá mesmo local de armazenamento padrão da saudação. Para obter uma lista de regiões com suporte, clique em Olá **região** lista suspensa em [preços do HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Pontos de extremidade de armazenamento para clusters

Embora uma instalação local do Hadoop usa Olá sistema de arquivos distribuído da Hadoop (HDFS) para o armazenamento em cluster hello, Olá nuvem usar pontos de extremidade de armazenamento conectados toocluster. Clusters HDInsight usam o [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) ou [blobs no Armazenamento do Azure](hdinsight-hadoop-use-blob-storage.md). Usar o armazenamento do Azure ou repositório Data Lake significa que você pode excluir com segurança os clusters de HDInsight Olá usados para cálculo enquanto ainda retém os dados. 

> [!WARNING]
> Não há suporte para usar uma conta de armazenamento adicional em um local diferente do cluster do HDInsight Olá.

Durante a configuração, ponto de extremidade de armazenamento padrão Olá você especificar um contêiner de blob de uma conta de armazenamento do Azure ou um repositório Data Lake. Olá armazenamento padrão contém aplicativo e sistema de logs. Opcionalmente, você pode especificar contas de armazenamento do Azure vinculadas adicionais e contas do repositório Data Lake Olá cluster podem acessar. Olá a cluster do HDInsight Hello e armazenamento dependentes Olá devem estar no mesmo local do Azure.

![Configurações de armazenamento de cluster: pontos de extremidade de armazenamento compatível com HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Metastores opcionais
Você pode criar metastores Hive ou Oozie opcionais. No entanto, nem todos os tipos de cluster dão suporte a metastores e o SQL Data Warehouse do Azure não é compatível com metastores. 

> [!IMPORTANT]
> Quando você cria um metastore personalizado, não use espaços no nome do banco de dados hello, hífens ou traços. Isso pode causar Olá toofail de processo de criação de cluster.

### <a name="use-hiveoozie-metastore"></a>Metastore do Hive

Se você quiser tooretain suas tabelas de Hive, após a exclusão de um cluster HDInsight, use um metastore personalizado. Em seguida, você pode anexar cluster do HDInsight Olá metastore tooanother.

Um metastore do HDInsight criado para uma versão de cluster do HDInsight não pode ser compartilhado entre diferentes versões de cluster do HDInsight. Para obter uma lista das versões do HDInsight, consulte [Versões do HDInsight com suporte](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Metastore do Oozie

tooincrease desempenho ao usar Oozie, use um metastore personalizado. Um metastore também pode fornecer dados de trabalho do access tooOozie depois de excluir o cluster. 

> [!IMPORTANT]
> Não é possível reutilizar um metastore personalizado do Oozie. toouse um Oozie metastore personalizado, você deve fornecer um banco de dados do SQL Azure vazio durante a criação de cluster do HDInsight hello.

## <a name="configure-cluster-size"></a>Configurar o tamanho do cluster

Você será cobrado por uso de nó para como cluster Olá existe. A cobrança começa quando um cluster é criado e é interrompido quando Olá cluster é excluído. Os clusters não podem ser desalocados ou colocados em espera.

custo de saudação de clusters HDInsight é determinado pelo número de saudação de nós e tamanhos de máquinas virtuais Olá para nós de saudação. 

Diferentes tipos de cluster têm diferentes tipos de nó, números de nós e tamanhos de nós:
* Padrão de tipo de cluster Hadoop: 
    * Dois *nós de cabeçalho*  
    * Quatro *nós de dados*
* Padrão de tipo de cluster Storm: 
    * Dois *nós Nimbus*
    * Três *nós ZooKeeper*
    * Quatro *nós supervisores* 

Se você estiver apenas experimentando o HDInsight, é recomendável usar um nó de dados. Para obter mais informações sobre os preços do HDInsight, confira [Preços do HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> limite de tamanho de cluster Olá varia entre as assinaturas do Azure. Entre em contato com [suporte de cobrança do Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease limite de saudação.
>

Quando você usa um cluster de Olá Olá tooconfigure portal do Azure, o tamanho de nó Olá está disponível por meio de saudação **as camadas de preços do nó** folha. No portal de saudação, você também pode ver Olá custo associado com tamanhos de nó diferente de saudação. 

![Tamanhos de nó de VM do HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Tamanhos de máquina virtual 
Quando você implantar clusters, escolha os recursos de computação com base na solução Olá planejar toodeploy. Olá que VMs seguintes são usadas para clusters de HDInsight:
* VMs A e série D1-4: [Tamanhos de VM Linux de uso geral](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* VM série D11-14: [Tamanhos de VM Linux com otimização de memória](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind out valor você deve usar toospecify um tamanho VM ao criar um cluster usando Olá SDKs diferentes ou ao usar o Azure PowerShell, consulte [toouse para clusters de HDInsight com tamanho de VM](../cloud-services/cloud-services-sizes-specs.md#size-tables). Deste artigo vinculado, use o valor de saudação no hello **tamanho** coluna das tabelas de saudação.

> [!IMPORTANT]
> Se você precisa de mais de 32 nós de trabalho em um cluster, você precisa selecionar um tamanho de nó de cabeçalho com pelo menos 8 núcleos e 14 GB de RAM.
>
>

Para obter mais informações, confira [Tamanhos das máquinas virtuais](../virtual-machines/windows/sizes.md). Para obter informações sobre os preços de saudação vários tamanhos, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Instalação de cluster personalizado
Compilações de instalação de cluster personalizado em Olá rápido criar configurações e adiciona Olá as opções a seguir:
- [Aplicativos HDInsight](#hdinsight-applications)
- [Tamanho do cluster](#cluster-size)
- Configurações avançadas
  - [Ações de script](#customize-clusters-using-script-action)
  - [Rede virtual](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Instalar aplicativos HDInsight em clusters

Um aplicativo do HDInsight é um aplicativo que os usuários podem instalar em um cluster HDInsight baseado em Linux. Você pode usar os aplicativos fornecidos pela Microsoft, a terceiros ou que você desenvolver por conta própria. Para saber mais, confira [Instalar aplicativos de terceiros do Hadoop no Azure HDInsight](hdinsight-apps-install-applications.md).

A maioria dos aplicativos de HDInsight Olá é instalada em um nó de borda vazia.  Um nó de borda vazia é uma máquina virtual de Linux com hello mesmas ferramentas de cliente instalado e configurado como nó principal hello. Você pode usar o nó de borda Olá para acessar o cluster hello, testar seus aplicativos de cliente e hospedagem de aplicativos cliente. Para saber mais, confira [Usar nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Configurações avançadas: ações de Script

Você pode instalar componentes adicionais ou personalizar a configuração de cluster por meio de scripts durante a criação. Esses scripts são invocados por meio de **ação de Script**, que é uma opção de configuração que pode ser usada de saudação portal do Azure, cmdlets do HDInsight Windows PowerShell ou Olá HDInsight .NET SDK. Para obter mais informações, consulte [Personalizar cluster HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

Alguns componentes de Java nativo, como Mahout e em cascata, podem ser executados no cluster hello como arquivos Java Archive (JAR). Esses arquivos JAR podem ser distribuída tooAzure armazenamento e enviada tooHDInsight clusters com mecanismos de envio de trabalho do Hadoop. Para obter mais informações, consulte [Enviar trabalhos do Hadoop de forma programática](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Se você tiver problemas de implantação de clusters de tooHDInsight arquivos JAR ou chamar arquivos JAR em clusters de HDInsight, entre em contato com [Microsoft Support](https://azure.microsoft.com/support/options/).
>
> A cascata não tem suporte do HDInsight e não está qualificada para o Suporte da Microsoft. Para listas de componentes com suporte, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).
>
>

Às vezes, você deseja tooconfigure Olá arquivos de configuração a seguir durante o processo de criação de saudação:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Para saber mais, confira [Personalizar clusters HDInsight usando a Inicialização](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Configurações avançadas: estender clusters com uma rede virtual
Se sua solução requer tecnologias que são distribuídas entre vários tipos de cluster HDInsight, uma [rede virtual do Azure](https://docs.microsoft.com/azure/virtual-network) pode se conectar a tipos de cluster Olá necessário. Essa configuração permite que os clusters hello e qualquer código que você implantar toothem, toodirectly se comunicam entre si.

Para obter mais informações sobre como usar uma rede virtual do Azure com HDInsight, confira [Estender o HDInsight com redes virtuais do Azure](hdinsight-extend-hadoop-virtual-network.md).

Para obter um exemplo de como usar dois tipos de cluster em uma rede virtual do Azure, confira [Analisar dados de sensor com Storm e HBase](hdinsight-storm-sensor-data-analysis.md). Para obter mais informações sobre como usar o HDInsight com uma rede virtual, incluindo requisitos de configuração específicos para a rede virtual do hello, consulte [HDInsight estender recursos usando a rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Solucionar problemas de controle de acesso

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas

- [Quais são HDInsight, ecossistema de Hadoop hello e clusters de Hadoop?](hdinsight-hadoop-introduction.md)
- [Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Trabalhar em Hadoop no HDInsight em um computador com Windows](hdinsight-hadoop-windows-tools.md)
