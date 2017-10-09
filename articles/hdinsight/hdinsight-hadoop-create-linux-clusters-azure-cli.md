---
title: "clusters de Hadoop aaaCreate usando a linha de comando - Olá HDInsight do Azure | Microsoft Docs"
description: "Saiba como clusters de HDInsight toocreate usando Olá 1.0 de CLI do Azure de plataforma cruzada."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Criar clusters HDInsight usando Olá CLI do Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Olá etapas para este passo a passo documento criando um cluster HDInsight 3.5 usando Olá 1.0 da CLI do Azure.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **CLI do Azure**. etapas Olá neste documento foram testadas última CLI do Azure versão 0.10.14.

    > [!IMPORTANT]
    > Olá etapas neste documento não funcionam com o Azure CLI 2.0. A CLI do Azure 2.0 não dá suporte à criação de um cluster HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Faça logon no tooyour assinatura do Azure

Execute as etapas de saudação documentadas em [conectar tooan assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure)](../xplat-cli-connect.md) e conecte-se a assinatura de tooyour usando Olá **login** método.

## <a name="create-a-cluster"></a>Criar um cluster

Olá, as etapas a seguir deve ser executada em uma linha de comando, como o PowerShell ou Bash.

1. Use Olá comando tooauthenticate tooyour assinatura do Azure a seguir:

        azure login

    Você está tooprovide solicitado seu nome e senha. Se você tiver várias assinaturas do Azure, use `azure account set <subscriptionname>` uso de comandos de assinatura Olá tooset Olá CLI do Azure.

2. Alternar o modo de Gerenciador de recursos de tooAzure usando Olá comando a seguir:

        azure config mode arm

3. Crie um grupos de recursos. Este grupo de recursos contém o cluster do HDInsight hello e conta de armazenamento associada.

        azure group create groupname location

    * Substituir `groupname` com um nome exclusivo para o grupo de saudação.

    * Substituir `location` com região Olá que deseja toocreate grupo de saudação.

       Para obter uma lista de locais válidos, use Olá `azure location list` de comando e, em seguida, use um dos locais de saudação do hello `Name` coluna.

4. Criar uma conta de armazenamento. Esta conta de armazenamento é usada como o armazenamento padrão da saudação para cluster de HDInsight hello.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Substituir `groupname` com nome Olá Olá grupo criado na etapa anterior hello.

    * Substituir `location` com hello mesmo local usado na etapa anterior hello.

    * Substituir `storagename` com um nome exclusivo para a conta de armazenamento hello.

        > [!NOTE]
        > Para obter mais informações sobre parâmetros de saudação usado neste comando, use `azure storage account create -h` tooview ajuda para este comando.

5. Recupere a conta de armazenamento de Olá Olá chave tooaccess usado.

        azure storage account keys list -g groupname storagename

    * Substituir `groupname` com o nome do grupo de recursos de saudação.
    * Substituir `storagename` com nome Olá Olá da conta de armazenamento.

     Em dados de saudação que são retornados, salvar Olá `key` valor para `key1`.

6. Crie um cluster HDInsight.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Substituir `groupname` com o nome do grupo de recursos de saudação.

    * Substituir `Hadoop` com o tipo de cluster Olá que você deseja toocreate. Por exemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.

     > [!IMPORTANT]
     > HDInsight clusters são fornecidos em vários tipos, que correspondem a carga de trabalho toohello ou tecnologia que Olá cluster é ajustada para. Não há nenhum método com suporte toocreate um cluster que combina vários tipos, como Storm e HBase em um cluster.

    * Substituir `location` com hello mesmo local usado nas etapas anteriores.

    * Substituir `storagename` com o nome de conta de armazenamento hello.

    * Substituir `storagekey` com chave Olá obtido na etapa anterior hello.

    * Para Olá `--defaultStorageContainer` parâmetro, use Olá mesmo nome que você está usando para o cluster de saudação.

    * Substituir `admin` e `httppassword` com hello nome e senha você deseja toouse ao acessar o cluster Olá através de HTTPS.

    * Substituir `sshuser` e `sshuserpassword` com hello nome de usuário e senha você deseja toouse ao acessar o cluster hello usando SSH

    > [!IMPORTANT]
    > Este exemplo cria um cluster com duas anotações de trabalho. Você também pode alterar o número de saudação de nós de trabalho após a criação do cluster realizando operações de dimensionamento. Se você planeja usar mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos oito núcleos e 14 GB de RAM. Você pode definir o tamanho de nó principal do hello usando Olá `--headNodeSize` parâmetro durante a criação do cluster.
    >
    > Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Ele pode levar vários minutos para Olá toofinish de processo de criação de cluster. Geralmente, cerca de 15 minutos.

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas

Agora que você criou com êxito um cluster HDInsight usando Olá CLI do Azure, use Olá toolearn a seguir como toowork com o cluster:

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
