---
title: clusters de pronto no Azure HDInsight Linux aaaInstall | Microsoft Docs
description: "Saiba como tooinstall pronto e Airpal no Hadoop de HDInsight baseados em Linux clusters usando ações de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Instalar e usar Presto em clusters Hadoop do HDInsight

Neste tópico, você aprenderá como tooinstall pronto no Hadoop de HDInsight clusters usando a ação de Script. Você também aprenderá como tooinstall Airpal em um cluster HDInsight Presto existente.

> [!IMPORTANT]
> Olá etapas neste documento exigem um **cluster HDInsight Hadoop de 3.5** que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, consulte [Versões do HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>O que é o Presto?
[Presto](https://prestodb.io/overview.html) é um mecanismo de consulta SQL distribuído rápido para big data. O Presto é ideal para consultas interativas de petabytes de dados. Para obter mais informações sobre componentes de saudação pronto e como eles funcionam juntos, consulte [conceitos Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.
> 
> Componentes personalizados, como pronto, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Instalar o Presto usando a ação de script

Esta seção fornece instruções sobre como o script de exemplo de hello toouse ao criar um novo cluster usando Olá portal do Azure. 

1. Iniciar o provisionamento de um cluster usando as etapas de saudação em [clusters HDInsight baseados em Linux provisionar](hdinsight-hadoop-create-linux-clusters-portal.md). Certifique-se de criar cluster hello usando Olá **personalizado** fluxo de criação de cluster. Certifique-se de cluster Olá que criar atende Olá requisitos a seguir.

    a. Ele deve ser um cluster Hadoop com o HDInsight versão 3.5.

    b. Ele deve usar o armazenamento do Azure como armazenamento de dados de saudação. Usando Presto em um cluster que usa o repositório Azure Data Lake como opção de armazenamento Olá ainda não é suportado. 

    ![Criação do cluster HDInsight usando opções personalizadas](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. Em Olá **configurações avançadas** folha, selecione **ações de Script**e forneça as informações de saudação abaixo:
   
   * **NOME**: insira um nome amigável para a ação de script hello.
   * **URI do script Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **CABEÇALHO**: marque esta opção
   * **TRABALHO**: marque esta opção
   * **ZOOKEEPER**: desmarque essa caixa de seleção
   * **PARÂMETROS**: deixe este campo em branco


3. Na parte inferior de saudação do hello **ações de Script** folha, clique em Olá **selecione** configuração de saudação do botão toosave. Por fim, clique em hello **selecione** botão na parte inferior de saudação do hello **configurações avançadas** informações de configuração de saudação de toosave de folha.

4. Continuar o provisionamento de cluster Olá conforme descrito em [clusters HDInsight baseados em Linux provisionar](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > PowerShell do Azure, Olá CLI do Azure, Olá HDInsight .NET SDK ou modelos do Azure Resource Manager também podem ser usado tooapply ações de script. Você também pode aplicar o script ações tooalready clusters em execução. Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Usar o Presto com o HDInsight

Execute Olá etapas toouse pronto em um cluster do HDInsight a seguir depois que ele foi instalado usando Olá etapas descritas acima.

1. Conecte o cluster do HDInsight toohello usando SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Inicie o shell Presto hello, usando o comando a seguir de saudação.
   
        presto --schema default

3. Execute uma consulta em uma tabela de exemplo, **hivesampletable**, que está disponível em todos os clusters do HDInsight por padrão.
   
        select count (*) from hivesampletable;
   
    Por padrão, os conectores [Hive](https://prestodb.io/docs/current/connector/hive.html) e [TPCH](https://prestodb.io/docs/current/connector/tpch.html) já vêm configurados. Conector de hive é configurado toouse saudação padrão instalado Hive instalação, para que todas as tabelas de saudação do Hive serão automaticamente visíveis no pronto.

    Para obter uma descrição detalhada de como você pode usar o Presto, confira a [documentação do Presto](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Usar o Airpal com o Presto

O [Airpal](https://github.com/airbnb/airpal#airpal) é uma interface de consulta baseada na Web de código-fonte aberto para o Presto. Para saber mais sobre o Airpal, confira a [documentação do Airpal](https://github.com/airbnb/airpal#airpal).

Nesta seção, vamos examinar etapas Olá muito**instalar Airpal em Olá edgenode** de um cluster HDInsight Hadoop, que já tem pronto instalado. Isso garante que essa interface de consulta Olá Airpal web está disponível por Olá da Internet.

1. Usando SSH, conecte-se toohello um nó principal do cluster HDInsight Olá Presto instalados:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Quando você estiver conectado, execute Olá comando a seguir.

        sudo slider registry  --name presto1 --getexp presto 
   
    Você verá uma saída semelhante Olá seguinte:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Da saída de hello, observe o valor de saudação para Olá **valor** propriedade. Você precisará dela durante a instalação Airpal no hello edgenode de cluster. Da saída de hello acima, o valor de saudação que você precisará **10.0.0.12:9090**.

4. Usar o modelo de saudação  **[aqui](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate um HDInsight edgenode do cluster e forneça valores hello, conforme mostrado na Olá captura de tela a seguir.

    ![Instalação do Airpal no cluster Presto pelo HDInsight](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Clique em **Comprar**.

6. Assim que as alterações de saudação forem aplicadas toohello configuração de cluster, você pode acessar a interface Olá Airpal da web usando Olá etapas a seguir.

    a. Na folha de cluster hello, clique em **aplicativos**.

    ![O HDInsight inicia o Airpal no cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. De saudação **aplicativos instalados** folha, clique em **Portal** contra airpal.

    ![O HDInsight inicia o Airpal no cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Quando solicitado, insira as credenciais de administrador de saudação que você especificou ao criar o cluster HDInsight Hadoop de saudação.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Personalizar uma instalação do Presto no cluster HDInsight

Depois que você instalou uma pronto em um cluster HDInsight Hadoop, você pode personalizar toomake alterações na instalação da saudação como atualizar as configurações de memória, alterar conectores, etc. Execute Olá toodo as etapas a seguir assim.

1. Usando SSH, conecte-se toohello um nó principal do cluster HDInsight Olá Presto instalados:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Faça as alterações de configuração no arquivo hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Para saber mais sobre a configuração do Presto, confira [Configuração do Presto para clusters baseados em YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).

3. Parar e interrompa a instância de execução atual de saudação do pronto.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Inicie uma nova instância de pronto com a personalização de saudação.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Aguarde Olá nova instância toobe pronto e observe o endereço do coordenador presto.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Gerar dados de avaliação de desempenho para clusters do HDInsight que executam o Presto

DS TPC é saudação padrão da indústria para medir o desempenho de saudação de muitos sistemas de suporte de decisão, incluindo sistemas grandes de dados. Você pode usar Presto nos dados de toogenerate clusters HDInsight e avaliar como ele se compara com seus próprios dados de referência do HDInsight. Para saber mais, clique [aqui](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Consulte também
* [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md). O matiz é uma interface que torna mais fácil toocreate, executar da web e salvar os trabalhos de Pig e Hive, bem como procurar saudação padrão armazenamento para seu cluster HDInsight.

* [Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Use cluster personalização tooinstall que giraph no Hadoop de HDInsight clusters. Giraph permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.

* [Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). Use cluster personalização tooinstall que solr no Hadoop de HDInsight clusters. Solr permite operações de pesquisa poderoso tooperform nos dados armazenados.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
