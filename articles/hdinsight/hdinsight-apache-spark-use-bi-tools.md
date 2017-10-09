---
title: "aaaSpark BI usando ferramentas de visualização de dados no Azure HDInsight | Microsoft Docs"
description: "Usar ferramentas de visualização de dados para análise usando Apache Spark BI em clusters HDInsight"
keywords: "apache spark bi, spark bi, visualização de dados spark, spark business intelligence"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI usando ferramentas de visualização de dados com o Azure HDInsight

Saiba como visualização de dados toouse ferramentas como o Power BI e Tableau tooanalyze um conjunto de dados brutos de exemplo usando o Apache Spark BI em clusters de HDInsight.

> [!NOTE]
> A conectividade com as ferramentas BI descritas neste artigo não tem suporte no Spark 2.1 no modo Preview do Azure HDInsight 3.6. Somente as versões 1.6 e 2.0 do Spark (HDInsight 3.4 e 3.5, respectivamente) têm suporte.
>

Este tutorial também está disponível como um notebook Jupyter em um cluster do Spark HDInsight. experiência de notebook Olá permite executar trechos de Python de saudação do bloco de anotações de saudação em si. tutorial de saudação tooperform de dentro de um bloco de anotações, criar um cluster Spark, inicie um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), e, em seguida, execute notebook Olá **usar ferramentas de BI com o Apache Spark no HDInsight.ipynb** em Olá **Python**  pasta.

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Preparar dados para visualização de dados o Spark

Nesta seção, usamos Olá [Jupyter](https://jupyter.org) bloco de anotações de um trabalhos de toorun de cluster HDInsight Spark que processam os dados brutos de exemplo e salvá-lo como uma tabela. dados de exemplo Hello são um arquivo. csv (hvac.csv) disponível em todos os clusters por padrão. Quando seus dados é salvo como uma tabela, na próxima seção, Olá, use a tabela de toohello de tooconnect de ferramentas de BI e executar visualizações de dados.

> [!NOTE]
> Se você estiver executando Olá as etapas neste artigo após a conclusão de instruções Olá [executar consultas interativas em um cluster do HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), você pode ignorar tooStep 8 abaixo.
>

1. De saudação [portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   

2. Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   > [!NOTE]
   > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Crie um notebook. Clique em **Novo** e em **PySpark**.

    ![Criar um notebook Jupyter para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Criar um notebook Jupyter para o Apache Spark BI")

4. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.

    ![Forneça um nome para o bloco de anotações Olá para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "forneça um nome para o bloco de anotações Olá para o Apache Spark BI")

5. Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. Olá Spark e Hive contextos são criados automaticamente para você quando você executar a primeira célula de código hello. Você pode começar importando tipos de saudação necessários para este cenário. toodo, portanto, coloque o cursor de saudação na célula hello e pressione **SHIFT + ENTER**.

        from pyspark.sql import *

6. Carregar dados de exemplo em uma tabela temporária. Quando você cria um cluster Spark no HDInsight, arquivo de dados de exemplo hello, **hvac.csv**, é copiado toohello associado a conta de armazenamento em **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    Em uma célula vazia, cole o seguinte Olá trecho e pressione **SHIFT + ENTER**. Este trecho de código registra dados saudação em uma tabela chamada **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Verifique se que essa tabela Olá foi criada com êxito. Você pode usar o hello `%%sql` magic consultas de Hive toorun diretamente. Para obter mais informações sobre Olá `%%sql` mágico e outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Você vê uma saída como a mostrada abaixo:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Olá somente tabelas que têm falso em Olá **isTemporary** coluna são tabelas de hive que são armazenadas em metastore hello e podem ser acessadas de ferramentas de BI hello. Neste tutorial, nós nos conectamos toohello **hvac** tabela são criadas.

8. Verifique se que essa tabela Olá contém dados saudação que se destina. Em uma célula vazia no bloco de anotações hello, copie o seguinte de saudação trecho e pressione **SHIFT + ENTER**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Desligar os recursos de Olá Olá notebook toorelease. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.

## <a name="powerbi"></a>Usar o Power BI para visualização de dados do Spark

> [!NOTE]
> Esta seção é aplicável somente ao Spark 1.6 no HDInsight 3.4 e ao Spark 2.0 no HDInsight 3.5.
>
>

Depois de salvar dados saudação como uma tabela, você pode usar dados do Power BI tooconnect toohello e visualizá-la toocreate relatórios, painéis, etc.

1. Verifique se que você tem acesso tooPower BI. Você pode obter uma assinatura gratuita de visualização do Power BI em [http://www.powerbi.com/](http://www.powerbi.com/).

2. Entrar muito[Power BI](http://www.powerbi.com/).

3. Da parte inferior de saudação do painel esquerdo do hello, clique em **obter dados**.

4. Em Olá **obter dados** página em **importar ou conectar tooData**, para **bancos de dados**, clique em **obter**.

    ![Colocar dados no Power BI para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Colocar dados no Power BI para o Apache Spark BI")

5. Na próxima tela de saudação, clique em **Spark no Azure HDInsight** e, em seguida, clique em **conectar**. Quando solicitado, insira a URL do cluster hello (`mysparkcluster.azurehdinsight.net`) e Olá credenciais tooconnect toohello cluster.

    ![Conecte-se tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "conectar tooApache Spark BI")

    Depois de estabelecer conexão hello, Power BI inicia a importação de dados do cluster do hello Spark no HDInsight.

6. Power BI importa dados hello e adiciona um **Spark** dataset sob Olá **conjuntos de dados** título. Clique em Olá tooopen de conjunto de dados novos dados de planilha toovisualize hello. Você também pode salvar a planilha hello como um relatório. toosave uma planilha, Olá **arquivo** menu, clique em **salvar**.

    ![Bloco do Apache Spark BI no painel do Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Bloco do Apache Spark BI no painel do Power BI")
7. Observe que Olá **campos** lista Olá direita lista Olá **hvac** tabela criada anteriormente. Expanda Olá tabela toosee Olá campos Olá tabela, conforme definido anteriormente no bloco de anotações.

      ![Listar tabelas no painel do Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Listar tabelas no painel do Apache Spark BI")

8. Crie uma visualização tooshow Olá a variação entre temperatura de destino e temperatura real para cada compilação. dados de suas toovisualize, selecione **gráfico de área** (mostrado na caixa vermelha). eixo toodefine Olá Olá de arrastar e soltar **BuildingID** campo em **eixo**, e **ActualTemp**/**TargetTemp** os campos em **valor**.

    ![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Criar visualizações de dados Spark usando o Apache Spark BI")

9. Por padrão, visualização de saudação mostra soma Olá para **ActualTemp** e **TargetTemp**. Para ambos Olá campos de saudação lista suspensa, selecione **médio** tooget média real e temperaturas de destino para as duas construções.

    ![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Criar visualizações de dados Spark usando o Apache Spark BI")

10. A visualização de dados deve ser semelhante toohello uma captura de tela de saudação. Mova o cursor sobre dicas de ferramenta do hello visualização tooget com dados relevantes.

    ![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Criar visualizações de dados Spark usando o Apache Spark BI")

11. Clique em **salvar** de saudação principais de menu e forneça um nome de relatório. Você também pode fixar Olá visual. Quando você fixa uma visualização, ele é armazenado no seu painel para que você pode controlar o valor mais recente de saudação em um relance.

   Você pode adicionar visualizações quantas desejar para Olá mesmo conjunto de dados e fixá-los toohello painel para um instantâneo dos dados. Além disso, clusters Spark no HDInsight são conectado tooPower BI com o direct se conectar. Isso garante que Power BI sempre terá Olá a maioria dos dados atualizados do cluster para que não é necessário tooschedule atualizações para o conjunto de dados de saudação.

## <a name="tableau"></a>Usar o Tableau Desktop para visualização de dados do Spark

> [!NOTE]
> Esta seção é aplicável somente para clusters do Spark 1.5.2 criados no Azure HDInsight.
>
>

1. Instalar [Tableau Desktop](http://www.tableau.com/products/desktop) no computador Olá onde você está executando este tutorial do Apache Spark BI.

2. Verifique se o computador também tem o driver ODBC do Microsoft Spark instalado. Você pode instalar o driver de saudação do [aqui](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Inicie o Tableau Desktop. No painel esquerdo do hello, na lista de saudação do servidor tooconnect, clique em **Spark SQL**. Se Spark SQL não estiver listado por padrão no painel esquerdo do hello, você pode localizá-la clique **mais servidores**.
2. Na caixa de diálogo de conexão do hello Spark SQL, forneça valores hello conforme mostrado na captura de tela hello e, em seguida, clique em **Okey**.

    ![Conectar tooa cluster para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "conectar tooa cluster para o Apache Spark BI")

    Olá listas suspensas de autenticação **Microsoft Azure HDInsight Service** como uma opção, somente se você instalou Olá [Driver de ODBC do Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) no computador de saudação.
3. Na tela seguinte hello, de saudação **esquema** lista suspensa, clique em Olá **localizar** ícone e clique **padrão**.

    ![Localizar o esquema para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Localizar o esquema para o Apache Spark BI")
4. Para Olá **tabela** , clique em Olá **localizar** ícone novamente toolist todos Olá Hive tabelas disponíveis no cluster hello. Você deve ver Olá **hvac** criado anteriormente usando o bloco de anotações de saudação de tabela.

    ![Localizar tabela para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Localizar a tabela para o Apache Spark BI")
5. Arraste e solte a caixa superior do hello tabela toohello em saudação à direita. Tableau importa dados hello e exibe o esquema de saudação como destacado pela caixa Olá vermelho.

    ![Adicionar tabelas tooTableau para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "adicionar tooTableau de tabelas para o Apache Spark BI")
6. Clique em Olá **Planilha1** guia na parte inferior de saudação à esquerda. Faça uma visualização que mostra o destino médio hello e temperaturas reais para todas as construções para cada data. Arraste **data** e **ID da construção** muito**colunas** e **Temp real**/**Temp destino**muito**linhas**. Em **marcas**, selecione **área** toouse um mapa de área de visualização de dados do Spark.

     ![Adicionar campos para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Adicionar campos para visualização de dados do Spark")
7. Por padrão, os campos de temperatura Olá são mostrados como agregação. Se você quiser temperaturas médio de saudação tooshow em vez disso, você pode fazer isso na lista suspensa Olá conforme mostrado abaixo.

    ![Obter a temperatura média para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Obter a temperatura média para visualização de dados do Spark")

8. Você também pode superimpor um mapa de temperatura Olá em outros tooget uma noção melhor de diferença entre temperaturas reais e de destino. Mova Olá mouse toohello de canto do mapa de área inferior Olá até ver Olá alça de forma realçada em um círculo vermelho. Arraste Olá mapa toohello outros mapa Olá superior e versão saudação do mouse quando você vir a forma de saudação realçada no retângulo vermelho.

    ![Mesclar mapas para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Mesclar mapas para visualização de dados do Spark")

     A visualização de dados deve alterar conforme mostrado na captura de tela de saudação:

    ![Saída do Tableau para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Saída do Tableau para visualização de dados do Spark")
9. Clique em **salvar** toosave planilha de saudação. Você pode criar painéis e adicionar um ou mais tooit de folhas.

## <a name="next-steps"></a>Próximas etapas

Até agora, você aprendeu como criar Spark quadros tooquery dados toocreate um cluster e acessar os dados de ferramentas de BI. Agora você pode ver instruções sobre como toomanage Olá recursos de cluster e depurar os trabalhos que são executados em um cluster HDInsight Spark.

* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

