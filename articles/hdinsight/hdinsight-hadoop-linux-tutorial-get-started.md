---
title: aaaGet iniciado com Hadoop e Hive no HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate HDInsight clusters e consultar dados com Hive.
keywords: "introdução ao hadoop, hadoop linux, início rápido do hadoop, introdução ao hive, início rápido do hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Tutorial do Hadoop: Introdução ao uso do Hadoop no HDInsight

Saiba como toocreate [Hadoop](http://hadoop.apache.org/) clusters HDInsight e como trabalhos de toorun Hive no HDInsight. [O Apache Hive](https://hive.apache.org/) é mais popular componente Olá ecossistema de Hadoop hello. Atualmente, o HDInsight vem com [sete tipos diferentes de cluster](hdinsight-hadoop-introduction.md#overview). Cada tipo de cluster dá suporte a um conjunto diferente de componentes. Todos os tipos de cluster dão suporte ao Hive. Para obter uma lista de componentes com suporte no HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deverá ter o seguinte:

* **Assinatura do Azure**: toocreate uma conta de avaliação de um mês livre, procurar muito[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Criar cluster

A maioria dos trabalhos de Hadoop consiste em trabalhos em lotes. Criar um cluster, executar algumas tarefas e, em seguida, excluir o cluster de saudação. Nesta seção, você criará um cluster Hadoop no HDInsight usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Não é necessário ter experiência com o modelo do Resource Manager para seguir este tutorial. Para outros métodos de criação de cluster e Noções básicas sobre propriedades de saudação usadas neste tutorial, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md). Use o seletor de saudação na parte superior de saudação do hello página toochoose suas opções de criação de cluster.

modelo do Gerenciador de recursos de saudação usado neste tutorial está localizado em [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Clique em Olá toosign de imagem no tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Insira ou selecione Olá valores a seguir:
   
    ![HDInsight Linux get iniciado o modelo do Gerenciador de recursos no portal](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "cluster Hadoop implantar usando HDInsigut Olá portal do Azure e um modelo de Gerenciador de grupo de recursos").
   
    * **Assinatura**: selecione sua assinatura do Azure.
    * **Grupo de recursos**: Crie um novo grupo de recursos ou escolha um grupo de recursos existente.  Um grupo de recursos é um contêiner de componentes do Azure.  Nesse caso, o grupo de recursos de saudação contém cluster do HDInsight hello e conta de armazenamento do Azure dependente hello. 
    * **Local**: selecione um local do Azure onde deseja toocreate seu cluster.  Escolha um tooyou mais próximo do local para um melhor desempenho. 
    * **Tipo de cluster**: selecione **hadoop** para este tutorial.
    * **Nome do cluster**: insira um nome para o cluster de Hadoop hello.
    * **Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.
    * **SSH username e password**: nome de usuário saudação padrão é **sshuser**.  Você pode renomeá-lo. 
     
    Algumas propriedades foram codificados no modelo de saudação.  Você pode configurar esses valores do modelo de saudação.

    * **Local**: Olá local do cluster hello e compartilhamento de conta de armazenamento dependentes Olá Olá mesmo local que o grupo de recursos de saudação.
    * **Versão do cluster**: 3.5
    * **Tipo de SO**: Linux
    * **Número de nós de trabalho**: 2

     Cada cluster tem uma dependência na [conta de Armazenamento do Azure](hdinsight-hadoop-use-blob-storage.md) ou [conta do Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Ele é conhecido como conta de armazenamento saudação padrão. Cluster HDInsight e sua conta de armazenamento padrão devem ser colocalizados em Olá mesma região do Azure. Excluir clusters não excluir a conta de armazenamento hello. 
     
     Para obter mais explicação sobre essas propriedades, confira [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Selecione **concordo toohello termos e condições declaradas acima** e **Pin toodashboard**e, em seguida, clique em **compra**. Você verá um novo bloco intitulado **implantação de modelo de implantação** no painel do portal hello. Demora cerca de aproximadamente 20 minutos toocreate um cluster. Depois de criar o cluster hello, legenda de saudação do bloco de saudação é alterado toohello nome do grupo de recursos especificado. E o portal de saudação abre automaticamente o grupo de recursos de saudação em uma nova folha. Você pode ver o cluster hello e o armazenamento padrão da saudação listados.
   
    ![Grupo de recursos de introdução ao HDInsight para Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Grupo de recursos de cluster do Azure HDInsight").

4. Clique em Olá cluster nome tooopen saudação do cluster em uma nova folha.

   ![Configurações de cluster de introdução do HDInsight para Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Propriedades do cluster do HDInsight")


## <a name="run-hive-queries"></a>Execute consultas Hive
[O Apache Hive](hdinsight-use-hive.md) é Olá componente mais popular usado no HDInsight. Há muitas maneiras toorun trabalhos de Hive no HDInsight. Neste tutorial, você deve usar Olá exibição Ambari Hive do portal de saudação. Para obter outros métodos para enviar trabalhos do Hive, confira [Usar o Hive no HDInsight](hdinsight-use-hive.md).

1. Na captura de tela anterior hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**.  Você também pode procurar muito **https://&lt;ClusterName >. cluster>.azurehdinsight.NET**, onde &lt;ClusterName > é Olá cluster criado em Olá tooopen anterior da seção Ambari.
2. Digite hello Hadoop nome do usuário e senha que você especificou na seção anterior hello. é o nome de usuário do saudação padrão **admin**.
3. Abra **exibição Hive** conforme Olá captura de tela a seguir:
   
    ![Selecionar modos de exibição do Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Menu do Visualizador do Hive no HDInsight").
4. Em Olá **Editor de consultas** seção da página hello, Olá colar HiveQL instruções a seguir na planilha de saudação:
   
        SHOW TABLES;
   
   > [!NOTE]
   > O ponto-e-vírgula é obrigatório para o Hive.       
   > 
   > 
5. Clique em **Executar**. Um **resultados do processo de consulta** seção deve aparecer abaixo Olá Editor de consultas e exibir informações sobre o trabalho de saudação. 
   
    Quando tiver terminado de consulta hello, Olá **resultados do processo de consulta** seção exibe os resultados de saudação da operação de saudação. Você deverá ver uma tabela chamada **hivesampletable**. Essa tabela de Hive de exemplo é fornecido com todos os clusters de HDInsight hello.
   
    ![Modos de exibição de Hive do HDInsight](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Editor de consulta de modo de exibição de Hive do HDInsight").
6. Repita a etapa 4 e saudação de toorun etapa 5 consulta a seguir:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Saudação de Observação **salvar resultados** suspensa no hello superior esquerdo da saudação **resultados do processo de consulta** seção; você pode usar este resultados de saudação do download tooeither ou salvá-los tooHDInsight armazenamento como um arquivo CSV.
   > 
   > 
7. Clique em **histórico** tooget uma lista de trabalhos de saudação.

Depois de concluir um trabalho de Hive, você poderá [exportar o banco de dados do hello resultados tooAzure SQL ou banco de dados do SQL Server](hdinsight-use-sqoop-mac-linux.md), você também pode [visualizar os resultados de saudação usando o Excel](hdinsight-connect-excel-power-query.md). Para obter mais informações sobre como usar o Hive no HDInsight, consulte [Use Hive e HiveQL com Hadoop no HDInsight tooanalyze um exemplo de arquivo Apache log4j](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Limpar tutorial Olá
Depois de concluir o tutorial hello, talvez você queira toodelete cluster de saudação. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso. Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso. 

> [!NOTE]
> Usando [do Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), você pode criar clusters HDInsight sob demanda e configurar um TimeToLive configuração muito exclui clusters Olá automaticamente. 
> 
> 

**toodelete Olá cluster e/ou Olá conta de armazenamento padrão**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Do painel do portal hello, clique em lado a lado com nome de grupo de recursos Olá que você usou quando criou o cluster Olá Olá.
3. Clique em **excluir** na Olá folha toodelete Olá recurso grupo de recursos, que contém o cluster hello e conta de armazenamento padrão Olá; ou clique no nome do cluster de saudação no hello **recursos** lado a lado e, em seguida, clique em **Excluir** na folha de cluster hello. Observação ao excluir o grupo de recursos de saudação exclui a conta de armazenamento de saudação. Se desejar que a conta de armazenamento tookeep hello, escolha toodelete Olá cluster apenas.

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate uma HDInsight baseados em Linux usando um modelo do Gerenciador de recursos de cluster e consultas de Hive tooperform básicas.

toolearn mais sobre a análise de dados com o HDInsight, consulte Olá artigos a seguir:

* toolearn mais sobre como usar o Hive com HDInsight, incluindo como tooperform Hive as consultas do Visual Studio, consulte [uso de Hive do HDInsight][hdinsight-use-hive].
* toolearn sobre Pig, uma linguagem usada tootransform dados, consulte [usar o Pig com HDInsight][hdinsight-use-pig].
* toolearn sobre MapReduce, programas de toowrite uma maneira que processam dados no Hadoop, consulte [Use MapReduce com HDInsight][hdinsight-use-mapreduce].
* toolearn sobre como usar ferramentas do HDInsight Olá para dados do Visual Studio tooanalyze no HDInsight, consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Se você estiver pronto toostart trabalhar com seus próprios dados e precisa tooknow mais sobre como HDInsight armazena dados ou como dados tooget em HDInsight, consulte o seguinte hello:

* Para saber mais sobre como o HDInsight usa o Armazenamento do Azure, veja [Usar Armazenamento do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Para obter informações sobre como tooupload tooHDInsight de dados, consulte [carregar dados tooHDInsight][hdinsight-upload-data].

Se você quiser toolearn mais sobre como criar ou gerenciar um cluster HDInsight, consulte a seguir hello:

* toolearn sobre como gerenciar seu cluster HDInsight baseados em Linux, consulte [HDInsight gerenciar clusters usando o Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn mais sobre opções de saudação, você pode selecionar ao criar um cluster HDInsight, consulte [criando HDInsight no Linux usando opções personalizadas](hdinsight-hadoop-provision-linux-clusters.md).
* Se você estiver familiarizado com Linux e Hadoop, mas desejar tooknow obter as informações específicas sobre o Hadoop Olá HDInsight, consulte [trabalhando com HDInsight no Linux](hdinsight-hadoop-linux-information.md). Este artigo oferece informações como:
  
  * URLs para serviços hospedados no cluster hello, como Ambari e WebHCat
  * local de saudação de arquivos Hadoop e exemplos no sistema de arquivos local Olá
  * uso de saudação do Azure Storage (WASB) em vez de HDFS como armazenamento de dados padrão de saudação

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


