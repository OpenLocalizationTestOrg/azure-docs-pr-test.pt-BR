---
title: "aaaWhat é o Apache Hive e HiveQL - HDInsight do Azure | Microsoft Docs"
description: "O Apache Hive é um sistema de data warehouse para Hadoop. Você pode consultar os dados armazenados no Hive usando o HiveQL, quais semelhante tooTransact-SQL. Neste documento, saiba como toouse Hive e HiveQL com HDInsight do Azure."
keywords: "o hiveql, o que é o hive, hiveql hadoop, hive, o que é o hive de saber como toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Saiba mais sobre o Apache Hive e o HiveQL no Azure HDInsight?

O [Apache Hive](http://hive.apache.org/) é um sistema de data warehouse para Hadoop. O Hive permite o resumo de dados, consultas e análise de dados. Consultas de hive são gravadas em HiveQL, que é um tooSQL semelhante de linguagem de consulta.

Seção permite que você tooproject estrutura em dados amplamente. Depois de definir a estrutura de saudação, você pode usar dados de saudação do HiveQL tooquery sem o conhecimento do Java ou MapReduce.

O HDInsight fornece vários tipos de cluster, que são ajustados para cargas de trabalho específicas. Olá seguintes tipos de cluster é geralmente usada para consultas de Hive:

* __Hive interativo__: Hadoop de um cluster que fornece [baixa latência analíticos processamento (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) tempos de resposta de tooimprove funcionalidade para consultas interativas. Para obter mais informações, consulte Olá [iniciar com interativo Hive no HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.

* __Hadoop__: um cluster Hadoop que está ajustado para cargas de trabalho de processamento em lotes. Para obter mais informações, consulte Olá [iniciar com Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.

* __Spark__: o Apache Spark tem funcionalidade interna para trabalhar com o Hive. Para obter mais informações, consulte Olá [iniciar com Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.

* __HBase__: HiveQL pode ser usado tooquery dados armazenados em HBase. Para obter mais informações, consulte Olá [iniciar com HBase em HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.

## <a name="how-toouse-hive"></a>Como toouse Hive

Use Olá toodiscover de tabela como toouse Hive com HDInsight a seguir:

| **Use esse método** se você quiser... | ...um shell **interativo** | ...Processamento em**lotes** | ... com esse **sistema operacional de cluster** | ... desse **sistema operacional cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [Exibição de Hive](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |Qualquer um (baseado em navegador) |
| [Cliente de Beeline](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [API REST](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux ou Windows* |Linux, Unix, Mac OS X ou Windows |
| [Ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux ou Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux ou Windows* |Windows |

> [!IMPORTANT]
> \*Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Se você estiver usando um cluster HDInsight baseados no Windows, você pode usar o hello [console de consulta](hdinsight-hadoop-use-hive-query-console.md) do navegador ou [área de trabalho remota](hdinsight-hadoop-use-hive-remote-desktop.md) toorun consultas de Hive.

## <a name="hiveql-language-reference"></a>Referência da linguagem HiveQL

Referência de linguagem HiveQL está disponível no hello [manual do idioma (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive e estrutura de dados

Hive entende como toowork com estruturado e dados estruturados. Por exemplo, arquivos de texto onde os campos de saudação são delimitados por caracteres específicos. Olá HiveQL instrução a seguir cria uma tabela de dados delimitados por espaço:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

O Hive também dá suporte a **serializador/desserializadores (SerDe)** personalizados para dados complexos ou com estrutura irregular. Para obter mais informações, consulte Olá [como toouse uma SerDe JSON personalizado com HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.

Para obter mais informações sobre formatos de arquivo suportados pelo Hive, consulte Olá [manual do idioma (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Tabelas internas Hive vs. tabelas externas

Há dois tipos de tabelas que você pode criar com o Hive:

* __Interno__: dados são armazenados no data warehouse do hello Hive. Olá do data warehouse está localizado em `/hive/warehouse/` no armazenamento de padrão de saudação para cluster hello.

    Use tabelas internas quando:

    * Os dados são temporários.
    * Você deseja Hive toomanage saudação do ciclo de vida de saudação e os dados.

* __Externa__: os dados são armazenados fora do hello data warehouse. dados de saudação podem ser armazenados em qualquer armazenamento acessível pelo cluster hello.

    Use tabelas externas quando:

    * dados de saudação também são usados fora do Hive. Por exemplo, arquivos de dados de saudação são atualizados por outro processo (que não bloqueia arquivos hello.)
    * Dados precisam tooremain em Olá subjacente local, mesmo depois de descartar a tabela hello.
    * Você precisa de um local personalizado, como uma conta de armazenamento não padrão.
    * Um programa diferente do hive gerencia o formato de dados hello, local, etc.

Para obter mais informações, consulte Olá [Hive internos e externos introdução de tabelas] [ cindygross-hive-tables] postagem de blog.

## <a name="user-defined-functions-udf"></a>UDF (Funções definidas pelo usuário)

O Hive também pode ser estendido por meio de **UDF (funções definidas pelo usuário)**. Um UDF permite funcionalidade tooimplement ou lógica que não é modelada facilmente no estilo. Para obter um exemplo do uso de UDFs com Hive, consulte Olá documentos a seguir:

* [Como usar uma função definida pelo usuário do Java com o Hive](hdinsight-hadoop-hive-java-udf.md)

* [Como usar uma função definida pelo usuário do Python com Hive e Pig](hdinsight-python.md)

* [Como usar uma função definidas pelo usuário do C# com Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Como tooadd um Hive personalizado definido pelo usuário função tooHDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Uma exemplo Hive função definida pelo usuário tooconvert data/hora formatos tooHive timestamp](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Dados de exemplo

O Hive no HDInsight vem pré-carregado com uma tabela interna chamada `hivesampletable`. O HDInsight também fornece conjuntos de dados de exemplo que podem ser usados com o Hive. Esses conjuntos de dados são armazenados em Olá `/example/data` e `/HdiSamples` diretórios. Esses diretórios existem no armazenamento padrão da saudação para seu cluster.

## <a id="job"></a>Exemplo de consulta do Hive

Olá após HiveQL instruções projeto colunas Olá `/example/data/sample.log` arquivo:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

No exemplo anterior de saudação, instruções de HiveQL Olá executam Olá ações a seguir:

* `set hive.execution.engine=tez;`: Define Olá toouse do mecanismo de execução Tez. Usar o Tez no lugar do MapReduce pode fornecer um aumento no desempenho da consulta. Para obter mais informações sobre Tez, consulte Olá [Tez do Apache de uso para melhorar o desempenho](#usetez) seção.

    > [!NOTE]
    > Essa instrução só é necessária ao usar um cluster HDInsight baseado em Windows. Tez é o mecanismo de execução padrão Olá para HDInsight baseados em Linux.

* `DROP TABLE`: Se Olá tabela já existir, exclua-o.

* `CREATE EXTERNAL TABLE`: cria uma nova tabela **externa** no Hive. Tabelas externas apenas armazenam a definição de tabela Olá no Hive. dados de saudação são deixados no local original hello e no formato original hello.

* `ROW FORMAT`: Informa ao Hive como Olá dados são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.

* `STORED AS TEXTFILE LOCATION`: Informa ao Hive onde hello os dados são armazenados (Olá `example/data` directory) e que ela é armazenada como texto. dados saudação podem estar em um arquivo ou distribuídos em vários arquivos no diretório de saudação.

* `SELECT`: Seleciona uma contagem de todas as linhas onde hello coluna **t4** contém valor Olá **[Erro]**. Essa instrução retorna um valor de **3**, já que há três linhas que contêm esse valor.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive tentativas tooapply Olá esquema tooall arquivos Olá diretório. Nesse caso, o diretório de saudação contém arquivos que não correspondem ao esquema de saudação. dados de lixo tooprevent nos resultados de hello, essa instrução informa Hive que só deve retornar dados de arquivos que terminam em. log.

> [!NOTE]
> Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa. Por exemplo, um processo de upload de dados automatizado ou uma operação MapReduce.
>
> Descartar uma tabela externa **não** excluir dados hello, exclui somente a definição de tabela hello.

toocreate um **interno** tabela em vez de externo, use Olá HiveQL a seguir:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Essas instruções executam Olá ações a seguir:

* `CREATE TABLE IF NOT EXISTS`: Se a tabela de saudação não existe, criá-lo. Porque Olá **externo** palavra-chave não for usada, essa instrução cria uma tabela interna. tabela de saudação é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.

* `STORED AS ORC`: Armazena dados saudação no formato de linha de otimização Colunar (ORC). Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.

* `INSERT OVERWRITE ... SELECT`: Seleciona linhas Olá **log4jLogs** tabela que contém **[Erro]**, e, em seguida, insere Olá dados em Olá **em decorrência** tabela.

> [!NOTE]
> Ao contrário das tabelas externas, descartar uma tabela interna também exclui dados subjacentes hello.

## <a name="improve-hive-query-performance"></a>Como melhorar o desempenho de consulta de Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) é uma estrutura que permite que aplicativos intensivos de dados, como o Hive, toorun muito mais eficiência em escala. O Tez está habilitado por padrão para clusters HDInsight baseados em Linux.

> [!NOTE]
> Atualmente o Tez está desativado por padrão para clusters baseados no Windows HDInsight e deve ser habilitado. tootake aproveitar Tez, Olá seguinte valor deve ser definida para uma consulta de Hive:
>
> `set hive.execution.engine=tez;`
>
> Tez é o mecanismo padrão de saudação para clusters HDInsight baseados em Linux.

Olá [Hive em documentos de design Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contém detalhes sobre as opções de implementação de saudação e configurações de ajustes.

tooaid na depuração de trabalhos foi executada usando Tez, HDInsight fornece Olá interfaces do usuário da web que permitem que você tooview detalhes dos trabalhos Tez a seguir:

* [Use Olá exibição Ambari Tez no HDInsight baseados em Linux](hdinsight-debug-ambari-tez-view.md)

* [Use Olá Tez UI no HDInsight baseados no Windows](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Processamento analítico de baixa latência (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (também conhecido como vida longa e processo) é um novo recurso no Hive 2.0 que permite armazenar as consultas em cache na memória. LLAP torna muito mais rápido, backup de consultas de Hive muito[26 x mais rápido do que 1. x em alguns casos de Hive](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight fornece LLAP no hello Hive interativo tipo de cluster. Para obter mais informações, consulte Olá [iniciar com Hive interativo](hdinsight-hadoop-use-interactive-hive.md) documento.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Trabalhos do Hive e SQL Server Integration Services

Você pode usar o SQL Server Integration Services (SSIS) toorun um trabalho de Hive. Hello Azure Feature Pack para SSIS fornece Olá componentes que funcionam com os trabalhos de Hive no HDInsight a seguir.

* [Tarefa do Hive do Azure HDInsight][hivetask]

* [Gerenciador de Conexões de Assinatura do Azure][connectionmanager]

Saiba mais sobre hello Azure Feature Pack para SSIS [aqui][ssispack].

## <a id="nextsteps"></a>Próximas etapas

Agora que você aprendeu Hive e como toouse com Hadoop no HDInsight, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.

* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Usar trabalhos do MapReduce com o HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
