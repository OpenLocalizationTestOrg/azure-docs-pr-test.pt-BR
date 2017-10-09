---
title: "clusters de aaaKernels para anotações do Jupyter no Spark no HDInsight do Azure | Microsoft Docs"
description: "Saiba mais sobre os kernels PySpark, PySpark3 e Spark Olá para anotações do Jupyter com clusters Spark no HDInsight do Azure."
keywords: "bloco de anotações do jupyter no spark, jupyter spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Kernels para o bloco de anotações do Jupyter em clusters do Spark no Azure HDInsight 

Os clusters de HDInsight Spark fornecem kernels que você pode usar anotações do Jupyter Olá no Spark para testar seus aplicativos. Um kernel é um programa que é executado e que interpreta seu código. três kernels Olá são:

- **PySpark** - para aplicativos escritos em Python2
- **PySpark3** - para aplicativos escritos em Python3
- **Spark** - para aplicativos escritos em Scala

Neste artigo, você aprenderá como toouse esses kernels e os benefícios de saudação de usá-los.

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Criar um bloco de anotações do Jupyter no Spark HDInsight

1. De saudação [portal do Azure](https://portal.azure.com/), abra seu cluster.  Consulte [lista e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) para obter instruções de saudação. cluster de saudação é aberto em uma nova folha de portal.

2. De saudação **links rápidos** seção, clique em **Cluster painéis** tooopen Olá **painéis do Cluster** folha.  Se você não vir **Links rápidos**, clique em **visão geral** no menu esquerdo de saudação na folha de saudação.

    ![Bloco de anotações do Jupyter no Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Bloco de anotações do Jupyter no Spark") 

3. Clique em **Notebook Jupyter**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.
   
   > [!NOTE]
   > Você também pode acessar anotações do Jupyter Olá no cluster do Spark por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Clique em **novo**e, em seguida, clique em **Pyspark**, **PySpark3**, ou **Spark** toocreate um bloco de anotações. Use kernel do Spark Olá para aplicativos Scala kernel PySpark para aplicativos Python2 e PySpark3 kernel para aplicativos de Python3.
   
    ![Kernels para bloco de anotações do Jupyter no Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Kernels para bloco de anotações do Jupyter no Spark") 

4. Abre um bloco de anotações com kernel Olá selecionado.

## <a name="benefits-of-using-hello-kernels"></a>Benefícios do uso de kernels Olá

Aqui estão algumas vantagens de usar kernels novo Olá com anotações do Jupyter em clusters de HDInsight Spark.

- **Contextos de predefinição**. Com **PySpark**, **PySpark3**, ou hello **Spark** kernels, você não precisa tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com seus aplicativos. Eles estão disponíveis para você por padrão. Esses contextos são:
   
   * **sc** - para o contexto do Spark
   * **sqlContext** : para o contexto Hive

    Portanto, você não tem instruções toorun como Olá contextos de saudação tooset a seguir:

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    Em vez disso, você pode usar diretamente Olá predefinição contextos em seu aplicativo.

- **A mágica da célula**. Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com `%%` (por exemplo, `%%MAGIC` <args>). comando magic Olá deve ser a primeira palavra hello em uma célula de código e permitir várias linhas de conteúdo. palavra mágica Olá deve ser a primeira palavra hello na célula de saudação. Adicionar qualquer coisa antes magic hello, até mesmo comentários, causa um erro.     Para saber mais sobre palavras mágicas, clique [aqui](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Olá tabela a seguir lista magics diferente da saudação disponíveis por meio de kernels hello.

   | Mágica | Exemplo | Descrição |
   | --- | --- | --- |
   | ajuda |`%%help` |Gera uma tabela de todos os magics de saudação disponíveis com o exemplo e uma descrição |
   | informações |`%%info` |Informações de sessão de saídas para o ponto de extremidade de Livy atual Olá |
   | CONFIGURAR |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Configura os parâmetros de saudação para criar uma sessão. Olá sinalizador force (-f) é obrigatório se uma sessão já foi criada, que garante que essa sessão Olá será descartada e recriada. Veja o [Corpo da Solicitação POST /sessions da Livy](https://github.com/cloudera/livy#request-body) para obter uma lista de parâmetros válidos. Parâmetros devem ser passados como uma cadeia de caracteres JSON e devem estar na próxima linha de saudação após magic Olá, conforme mostrado na coluna de exemplo hello. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |Executa uma consulta de Hive em Olá sqlContext. Se hello `-o` parâmetro for passado, o resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um [Pandas](http://pandas.pydata.org/) dataframe. |
   | local |`%%local`<br>`a=1` |Todo o código Olá linhas subsequentes é executado localmente. Código deve ser o código Python2 válido mesmo independentemente do kernel Olá que você está usando. Portanto, mesmo se você selecionou **PySpark3** ou **Spark** kernels durante a criação de notebook hello, se você usar o hello `%%local` magic em uma célula, essa célula só deve ter código Python2 válido. |
   | logs |`%%logs` |Saídas hello logs para a sessão atual de Livy hello. |
   | excluir |`%%delete -f -s <session number>` |Exclui uma sessão específica do ponto de extremidade de Livy atual hello. Observe que você não pode excluir a sessão Olá iniciado para o kernel Olá em si. |
   | limpeza |`%%cleanup -f` |Exclui todas as sessões de Olá Olá atual Livy ponto de extremidade, incluindo sessão deste bloco de anotações. Olá force sinalizador -f é obrigatório. |

   > [!NOTE]
   > Além disso toohello magics adicionado pelo kernel de PySpark hello, você também pode usar o hello [magics internos do IPython](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), incluindo `%%sh`. Você pode usar o hello `%%sh` magic toorun scripts e blocos de código em um nó de cluster principal hello.
   >
   >
2. **Visualização automática**. Olá **Pyspark** kernel automaticamente visualiza a saída de saudação de consultas de Hive e SQL. Escolha entre vários tipos diferentes de visualização, incluindo Tabela, Pizza, Linha, Área, Barra.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parâmetros de suporte com hello % % mágico do sql
Olá `%%sql` magic dá suporte a parâmetros diferentes que você pode usar o tipo de saudação do toocontrol de saída que você recebe ao executar consultas. Olá a tabela a seguir lista a saída de hello.

| Parâmetro | Exemplo | Descrição |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Use esse resultado parâmetro toopersist Olá Olá consulta, em Olá % % contexto Python local, como um [Pandas](http://pandas.pydata.org/) dataframe. nome de saudação da variável de dataframe de saudação é o nome de variável de saudação que você especificar. |
| -q |`-q` |Use este tooturn desativar visualizações de célula hello. Se você não quiser tooauto-visualizar o conteúdo de saudação de uma célula e deseja apenas toocapture-lo como um dataframe, em seguida, use `-q -o <VARIABLE>`. Se você quiser tooturn desativar visualizações sem capturando Olá resultados (por exemplo, para executar uma consulta SQL, como um `CREATE TABLE` instrução), use `-q` sem especificar um `-o` argumento. |
| -m |`-m <METHOD>` |Onde **METHOD** é **take** ou **sample** (o padrão é **take**). Se o método hello é **levar**, kernel Olá escolhe elementos da parte superior de saudação do conjunto de resultados de saudação especificado pelo MAXROWS (descrito posteriormente nesta tabela). Se o método hello é **exemplo**, kernel Olá aleatoriamente exemplos de elementos de saudação do conjunto de dados de acordo com muito`-r` parâmetro, como descrito a seguir nesta tabela. |
| -r |`-r <FRACTION>` |Aqui **FRACTION** é um número de ponto flutuante entre 0.0 e 1.0. Se o método do exemplo hello para consulta SQL Olá é `sample`, em seguida, o kernel Olá aleatoriamente amostras de fração de saudação especificado de elementos de saudação do hello conjunto de resultados para você. Por exemplo, se você executar uma consulta SQL com argumentos Olá `-m sample -r 0.01`, em seguida, % 1 Olá de linhas de resultado são amostrados aleatoriamente. |
| -n |`-n <MAXROWS>` |**MAXROWS** é um valor inteiro. kernel Olá limita o número de saudação de linhas de saída muito**MAXROWS**. Se **MAXROWS** é um número negativo como **-1**, em seguida, Olá número de linhas no conjunto de resultados de saudação não é limitado. |

**Exemplo:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

instrução de saudação acima Olá a seguir:

* Seleciona todos os registros de **hivesampletable**.
* Como usamos - q, ele desativa a visualização automática.
* Porque usamos `-m sample -r 0.1 -n 500` -amostras de 10% das linhas Olá Olá hivesampletable aleatoriamente e Olá de limites de tamanho de linhas de too500 do conjunto de resultados de saudação.
* Por fim, porque usamos `-o query2` saída Olá também salva em um dataframe chamado **consulta2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Considerações ao usar o hello kernels novo

Seja qual for o kernel usar, deixar notebooks Olá com consome recursos de cluster de saudação.  Com esses kernels, porque os contextos de saudação são predefinidos, simplesmente sair notebooks Olá não kill contexto hello e, portanto, os recursos de cluster Olá continuam toobe em uso. Uma prática recomendada é Olá toouse **fechar e interromper** opção a partir do bloco de anotações Olá **arquivo** menu quando terminar de usar notebook hello, o que elimina o contexto de saudação e, em seguida, sai Olá notebook.     

## <a name="show-me-some-examples"></a>Mostre-me alguns exemplos

Quando você abre um bloco de anotações do Jupyter, verá duas pastas disponíveis no nível raiz de saudação.

* Olá **PySpark** pasta tiver blocos de anotações do exemplo hello que use novo **Python** kernel.
* Olá **Scala** pasta tiver blocos de anotações do exemplo hello que use novo **Spark** kernel.

Você pode abrir Olá **00 - [LEIA-ME primeiro] recursos de Kernel do Spark Magic** notebook de saudação **PySpark** ou **Spark** toolearn pasta sobre magics diferente da saudação disponíveis. Você também pode usar Olá outros blocos de anotações do exemplo disponíveis em Olá duas pastas toolearn como tooachieve diferentes cenários de uso de anotações do Jupyter com clusters de HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>Onde estão armazenados os blocos de anotações Olá?

Blocos de anotações do Jupyter são salvos toohello conta de armazenamento associada Olá cluster em Olá **/HdiNotebooks** pasta.  Blocos de anotações, arquivos de texto e pastas que você criar no Jupyter são acessíveis Olá da conta de armazenamento.  Por exemplo, se você usar uma pasta de toocreate de Jupyter **minhapasta** e um bloco de anotações **myfolder/mynotebook.ipynb**, você pode acessar esse bloco no `/HdiNotebooks/myfolder/mynotebook.ipynb` na conta de armazenamento hello.  Olá inverso também é verdadeiro, ou seja, se você carregar um bloco de anotações diretamente a conta de armazenamento tooyour em `/HdiNotebooks/mynotebook1.ipynb`, notebook Olá também é visível do Jupyter.  Blocos de anotações permanecem na conta de armazenamento Olá mesmo após Olá cluster é excluído.

modo de Olá anotações são salvas toohello conta de armazenamento é compatível com o HDFS. Portanto, se você SSH em cluster Olá que você pode usar comandos de gerenciamento de arquivos conforme Olá trecho de código a seguir:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Caso haja problemas para acessar a conta de armazenamento Olá para cluster hello, notebooks Olá também são salvas em um nó principal do hello `/var/lib/jupyter`.

## <a name="supported-browser"></a>Navegador com suporte

Os blocos de anotações do Jupyter em clusters do Spark HDInsight só têm suporte no Google Chrome.

## <a name="feedback"></a>Comentários
kernels novo Olá estão em evolução estágio e serão amadurecer ao longo do tempo. Isso também pode significar que as APIs podem mudar à medida que esses kernels amadurecem. Agradecemos o envio quaisquer comentários que você tenha ao usar esses novos kernels. Isso é útil na versão final de saudação desses kernels de formatação. Você pode deixar seus comentários/comentários em Olá **comentários** seção Olá final deste artigo.

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
