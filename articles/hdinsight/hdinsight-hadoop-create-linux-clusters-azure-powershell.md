---
title: clusters de Hadoop aaaCreate usando o PowerShell - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate Hadoop, HBase, tempestade ou Spark clusters no Linux para HDInsight usando o PowerShell do Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

PowerShell do Azure é um ambiente de script poderoso que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Microsoft Azure. Este documento fornece informações sobre como toocreate uma HDInsight baseados em Linux de cluster usando o PowerShell do Azure. Ele também inclui um script de exemplo.

> [!NOTE]
> O Azure PowerShell só está disponível em clientes do Windows. Se você estiver usando um cliente Mac OS X, Unix ou Linux, consulte [criar um cluster HDInsight baseados em Linux usando a CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para obter informações sobre como usar o hello CLI do Azure toocreate um cluster.

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte Olá antes de iniciar este procedimento:

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [PowerShell do Azure](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017. Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.
    >
    > Siga as etapas de saudação em [instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall Olá última versão do PowerShell do Azure. Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.

## <a name="create-cluster"></a>Criar cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate um cluster HDInsight usando o PowerShell do Azure, você deve concluir Olá procedimentos a seguir:

* Criar um grupo de recursos do Azure
* Criar uma conta de Armazenamento do Azure
* Criar um contêiner de Blob do Azure
* Crie um cluster HDInsight

Olá script a seguir demonstra como toocreate um novo cluster:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

os valores de Olá especificado para o logon de cluster Olá são toocreate usado Olá conta de usuário do Hadoop para cluster hello. Use este tooservices de tooconnect conta hospedadas no cluster hello como web interfaces do usuário ou APIs REST.

os valores Hello especificado para o usuário SSH Olá são usuário SSH Olá toocreate usado para o cluster de saudação. Use esta conta toostart uma sessão remota do SSH no cluster hello e executar trabalhos. Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

> [!IMPORTANT]
> Se você planejar toouse mais de 32 nós de trabalho (na criação de cluster ou escala Olá cluster após a criação), você também deve especificar um tamanho de nó principal com pelo menos 8 núcleos e 14 GB de RAM.
>
> Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Pode demorar até too20 minutos toocreate um cluster.

## <a name="create-cluster-configuration-object"></a>Criar cluster: objeto de configuração

Você também pode criar um objeto de configuração de HDInsight usando o cmdlet `New-AzureRmHDInsightClusterConfig`. Você pode modificar essa configuração objeto tooenable outras opções de configuração para o cluster. Por fim, use Olá `-Config` parâmetro hello `New-AzureRmHDInsightCluster` configuração de saudação do cmdlet toouse.

Olá script a seguir cria um tooconfigure do objeto de configuração um servidor de R no tipo de cluster HDInsight. configuração de saudação permite que um nó de borda, RStudio e uma conta de armazenamento adicionais.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente. Ao usar este exemplo, criar a conta de armazenamento adicional de saudação em Olá mesmo local como servidor de saudação.

## <a name="customize-clusters"></a>Personalizar clusters

* Consulte [Personalizar clusters do HDInsight usando a Inicialização](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas

Agora que você criou com êxito um cluster HDInsight, use Olá toolearn recursos a seguir como toowork com o cluster.

### <a name="hadoop-clusters"></a>Clusters do Hadoop

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters do HBase

* [Introdução ao HBase no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desenvolvimento de aplicativos Java para HBase no HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm

* [Desenvolver topologias Java para Storm no HDInsight](hdinsight-storm-develop-java-topology.md)
* [Usar componentes de Python no Storm no HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implantar e monitorar topologias com o Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clusters do Spark

* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)

