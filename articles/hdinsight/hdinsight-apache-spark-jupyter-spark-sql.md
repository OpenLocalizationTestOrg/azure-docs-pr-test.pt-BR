---
title: cluster de aaaCreate um Apache Spark no HDInsight do Azure | Microsoft Docs
description: "Início rápido do HDInsight Spark no como cluster de toocreate um Apache Spark no HDInsight."
keywords: "início rápido do spark,spark interativo,consulta interativa,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Criar um cluster do Apache Spark no Azure HDInsight

Neste artigo, você aprenderá como cluster de toocreate um Apache Spark no HDInsight do Azure. Para obter informações sobre o Spark no HDInsight, confira [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md).

   ![Diagrama de início rápido que descreve as etapas toocreate um cluster do Apache Spark no Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "início rápido do Spark usando o Apache Spark no HDInsight. Etapas ilustradas: criar um cluster; executar consulta interativa do Spark")

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Antes de começar este tutorial, você deverá ter uma assinatura do Azure. Consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Criar cluster do Azure HDInsight Spark

Nesta seção, você criará um cluster Spark do HDInsight usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Para obter outros métodos de criação de cluster, confira [Criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Digite hello valores a seguir:

    ![Criar um cluster Spark do HDInsight usando um modelo do Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Criar um cluster Spark no HDInsight usando um modelo do Azure Resource Manager")

    * **Assinatura**: selecione sua assinatura do Azure para esse cluster.
    * No **Grupo de recursos**: crie um grupo de recursos ou selecione um existente. Grupo de recursos é usado toomanage recursos do Azure para seus projetos.
    * **Local**: selecione um local para o grupo de recursos de saudação. modelo Olá usa esse local para a criação de cluster Olá bem como para o armazenamento de cluster saudação padrão.
    * **ClusterName**: insira um nome para o cluster do HDInsight Olá que você deseja toocreate.
    * **Versão do Spark**: selecione **2.0** como versão Olá que você deseja tooinstall no cluster hello.
    * **Nome de logon e senha do cluster**: nome de logon do saudação padrão é Admin.
    * **Nome de usuário e senha de SSH**.

   Anote esses valores.  Você precisa-los mais tarde no tutorial de saudação.

3. Selecione **concordo toohello termos e condições declaradas acima**, selecione **Pin toodashboard**e, em seguida, clique em **compra**. Você poderá ver um novo bloco intitulado Como enviar a implantação para a implantação do modelo. Ele usa um cluster de saudação toocreate cerca de 20 minutos.

Se você tiver um problema com a criação de clusters HDInsight, é possível que você não tem Olá permissões corretas toodo assim. Confira [requisitos do controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters) para obter mais informações.

> [!NOTE]
> Este artigo cria um cluster Spark usa [armazenamento de Blobs de armazenamento do Azure como Olá cluster](hdinsight-hadoop-use-blob-storage.md). Você também pode criar um cluster Spark que usa [repositório Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) como armazenamento de padrão de saudação. Para obter instruções, confira [Criar um cluster HDInsight com o Repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Executar uma consulta de Hive usando o Spark SQL

Quando você usa um bloco de anotações do Jupyter configurado para o cluster HDInsight Spark, você obtém uma predefinição `sqlContext` que você pode usar consultas de Hive toorun usando Spark SQL. Nesta seção, você aprenderá como toostart um bloco de anotações do Jupyter e, em seguida, execute uma consulta de Hive básica.

1. Olá abrir [portal do Azure](https://portal.azure.com/).

2. Se você optou por painel de toohello toopin Olá cluster, clique em Olá cluster lado a lado na folha de cluster Olá painel toolaunch hello.

    Se você não fixar Olá cluster toohello painel de controle, no painel esquerdo do hello, clique em **clusters HDInsight**e, em seguida, clique em cluster Olá que você criou.

3. Em **Links rápidos**, clique em **Painéis de cluster**e, em seguida, clique em **Anotações do Jupyter**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   ![Abra Jupyter notebook toorun Spark SQL consulta interativo](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "consulta toorun Spark SQL interativo notebook Jupyter aberto")

   > [!NOTE]
   > Você também pode acessar as anotações do Jupyter Olá para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Crie um notebook. Clique em **Novo** e em **PySpark**.

   ![Criar uma consulta SQL Spark interativa Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "criar uma consulta Jupyter notebook toorun interativa Spark SQL")

   Um novo bloco de anotações é criado e aberto com o nome hello Untitled(Untitled.pynb).

4. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável, se desejar.

    ![Forneça um nome para Olá Jupter notebook toorun Spark consulta interativo de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "forneça um nome para Olá Jupter notebook toorun Spark consulta interativa do")

5.  Colar Olá seguinte código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER** toorun código de saudação. Código de saudação abaixo `%%sql` (mágico de sql chamado hello) informa a predefinição Olá de toouse de notebook Jupyter `sqlContext` consulta de Hive toorun hello. consulta de saudação recupera Olá 10 primeiras linhas de uma tabela de Hive (**hivesampletable**) que está disponível por padrão em todos os clusters de HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Consulta de Hive no HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Consulta de Hive no HDInsight Spark")

    Para obter mais informações sobre Olá `%%sql` mágico e hello predefinição contextos, consulte [Jupyter kernels disponíveis para um cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Sempre que você executa uma consulta em Jupyter, o título da janela navegador web mostra um **(ocupada)** status junto com o título do bloco de anotações de saudação. Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação. Após o trabalho hello, ele altera o círculo vazio tooa.
    >
    >
    
6. tela Hello deve atualizar a saída da consulta tooshow hello.

    ![Saída da consulta de Hive no HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Saída da consulta de Hive no HDInsight Spark")

7. Desliga os recursos de cluster de saudação do hello notebook toorelease depois de terminar de executar o aplicativo hello. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.

8. Se você planejar as próximas etapas do toocomplete hello mais tarde, certifique-se de que excluir o cluster do HDInsight Olá criado neste artigo. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Próxima etapa 

Neste artigo, você aprendeu como toocreate uma HDInsight Spark cluster e execute um Spark SQL básica de consulta. Avança toohello próximo artigo toolearn como toouse uma HDInsight Spark cluster consultas interativas toorun em dados de exemplo.

> [!div class="nextstepaction"]
>[Executar consultas interativas em um cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md)



