---
title: aaaInstall e usar Giraph no HDInsight (Hadoop) - Azure | Microsoft Docs
description: "Saiba como tooinstall Giraph no HDInsight baseados em Linux clusters usando ações de Script. Ações de script permite que você toocustomize Olá cluster durante a criação, alteração de configuração de cluster ou instalando serviços e utilitários."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Instalar Giraph em clusters de HDInsight Hadoop e usar gráficos em grande escala do Giraph tooprocess

Saiba como tooinstall Giraph Apache em um cluster HDInsight. recurso de ação de script de saudação do HDInsight permite que você toocustomize o cluster executando um script de bash. Scripts podem ser usados toocustomize clusters durante e após a criação do cluster.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>O que é Giraph

[Apache Giraph](http://giraph.apache.org/) permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight. Gráficos moldam as relações entre objetos. Por exemplo, conexões de saudação entre roteadores em uma rede grande como Olá Internet ou relações entre as pessoas em redes sociais. Processamento de gráfico permite que você tooreason sobre relações de saudação entre objetos em um gráfico, como:

* Identificar possíveis amigos com base em suas relações atuais.

* Identificando a rota mais curta Olá entre dois computadores em uma rede.

* Calculando a classificação de página Olá das páginas da Web.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados - Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.
>
> Componentes personalizados, como Giraph, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. Microsoft Support pode ser capaz de tooresolving problema de saudação. Caso contrário, você deve consultar comunidades de software livre em que é possível encontrar conhecimento aprofundado sobre essa tecnologia. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>O script hello faz

Esse script executa Olá ações a seguir:

* Instala Giraph muito`/usr/hdp/current/giraph`

* Olá cópias `giraph-examples.jar` armazenamento de arquivos toodefault (WASB) para o cluster:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Instalar o Giraph usando Ações de Script

Tooinstall um script de exemplo Giraph em um cluster HDInsight está disponível em Olá local a seguir:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Esta seção fornece instruções sobre como toouse Olá script de exemplo durante a criação de cluster hello usando Olá portal do Azure.

> [!NOTE]
> Uma ação de script pode ser aplicada usando qualquer um dos métodos a seguir de saudação:
> * Azure PowerShell
> * Olá CLI do Azure
> * Olá HDInsight .NET SDK
> * Modelos do Gerenciador de Recursos do Azure
> 
> Você também pode aplicar o script ações tooalready clusters em execução. Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).

1. Começar a criar um cluster usando as etapas de saudação em [clusters HDInsight baseados em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md), mas não conclua o processo de criação.

2. Em Olá **configuração opcional** folha, selecione **ações de Script**e fornecer Olá informações a seguir:

   * **NOME**: insira um nome amigável para a ação de script hello.

   * **URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **CABEÇALHO**: marque esta entrada

   * **TRABALHO**: deixe esta entrada desmarcada

   * **ZOOKEEPER**: deixe esta entrada desmarcada

   * **PARÂMETROS**: deixe este campo em branco

3. Na parte inferior de saudação do hello **ações de Script**, use Olá **selecione** configuração de saudação do botão toosave. Por fim, use Olá **selecione** botão na parte inferior de saudação do hello **configuração opcional** informações de configuração opcional de saudação de toosave de folha.

4. Continuar a criar o cluster Olá conforme descrito em [clusters HDInsight baseados em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Como usar o Giraph no HDInsight?

Depois que o cluster Olá tiver sido criado, use Olá etapas toorun Olá SimpleShortestPathsComputation exemplo incluído com Giraph a seguir. Este exemplo usa Olá basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementação para localizar o caminho mais curto de saudação entre objetos em um gráfico.

1. Conecte o cluster do HDInsight toohello usando SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Comando de uso a seguir de saudação toocreate um arquivo chamado **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Use Olá depois do texto como o conteúdo deste arquivo hello:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Esses dados descrevem uma relação entre objetos em um gráfico direcionado, usando o formato de saudação `[source_id, source_value,[[dest_id], [edge_value],...]]`. Cada linha representa uma relação entre um objeto `source_id` e um ou mais objetos `dest_id`. Olá `edge_value` pode ser pensada como intensidade hello ou distância de conexão Olá entre `source_id` e `dest\_id`.

    Desenhado, e usando o valor de hello (ou peso) como a distância Olá entre objetos, dados saudação podem parecer com hello diagrama a seguir:

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. arquivo de saudação toosave, use **Ctrl + X**, em seguida, **Y**e, finalmente, **Enter** nome de arquivo hello tooaccept.

4. Use Olá seguintes dados de saudação do toostore no armazenamento primário para seu cluster HDInsight:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Execute o exemplo de SimpleShortestPathsComputation hello usando o comando a seguir de saudação:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    parâmetros de saudação usados com este comando são descritos na Olá a tabela a seguir:

   | Parâmetro | O que faz |
   | --- | --- |
   | `jar` |arquivo jar do Hello que contém exemplos de saudação. |
   | `org.apache.giraph.GiraphRunner` |classe de saudação usada toostart exemplos de saudação. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |exemplo Hello que é usado. Neste exemplo, ele computa o caminho mais curto de saudação entre ID 1 e todos os outros IDs no gráfico de saudação. |
   | `-ca mapred.job.tracker` |Olá um nó principal para o cluster de saudação. |
   | `-vif` |Olá toouse de formato de entrada para os dados de entrada hello. |
   | `-vip` |arquivo de dados de entrada Hello. |
   | `-vof` |saudação de formato de saída. Nesse exemplo, a ID e o valor como texto sem formatação. |
   | `-op` |saudação de local de saída. |
   | `-w 2` |número de saudação de trabalhadores toouse. Neste exemplo, 2. |

    Para obter mais informações sobre esses e outros parâmetros usados com Giraph exemplos, consulte Olá [Giraph quickstart](http://giraph.apache.org/quick_start.html).

6. Quando tiver terminado de trabalho hello, resultados de saudação são armazenados em Olá **/example/out/shotestpaths** directory. Olá nomes de arquivo de saída começam com **parte-m -** e terminar com um número indicando Olá primeiro, segundo, arquivo etc. Use Olá saída do comando tooview Olá a seguir:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    saída de Hello deve aparecer semelhante toohello texto a seguir:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    exemplo de SimpleShortestPathComputation Hello é toostart codificado com o objeto ID 1 e localizar Olá shortest path tooother objetos. saída de Hello está no formato de saudação do `destination_id` e `distance`. Olá `distance` é Olá valor (ou peso) das bordas Olá percorridas entre o objeto ID 1 e ID de destino hello.

    Visualizar esses dados, você pode verificar os resultados de saudação percorrerem caminhos mais curto Olá ID 1 e todos os outros objetos. caminho mais curto de saudação entre ID 1 e 4 ID é 5. Esse valor é a distância total Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Próximas etapas

* [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).

* [Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).
