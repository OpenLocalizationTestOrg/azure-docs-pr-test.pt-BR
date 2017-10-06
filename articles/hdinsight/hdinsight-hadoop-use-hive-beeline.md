---
title: aaaUse Beeline com o Apache Hive - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Olá Beeline cliente toorun Hive consultas com Hadoop no HDInsight. Beeline é um utilitário para trabalhar com HiveServer2 sobre JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Usar o cliente de Beeline Olá com o Apache Hive

Saiba como toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consultas toorun Hive no HDInsight.

Beeline é um cliente de Hive que está incluído em nós de cabeçalho de saudação do seu cluster HDInsight. Beeline usa JDBC tooconnect tooHiveServer2, um serviço hospedado em seu cluster HDInsight. Você também pode usar Beeline tooaccess Hive no HDInsight remotamente em Olá da internet. Olá, a tabela a seguir fornece cadeias de caracteres de conexão para uso com Beeline:

| De que local você executa o Beeline | parâmetros |
| --- | --- | --- |
| Um nó de um nó principal ou de borda de tooa do conexão SSH | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Cluster de saudação externa | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Substituir `admin` com a conta de logon de cluster Olá para seu cluster.
>
> Substituir `password` com senha Olá Olá cluster conta de logon.
>
> Substituir `clustername` com nome de saudação do cluster HDInsight.

## <a id="prereq"></a>Pré-requisitos

* Um cluster do Hadoop no HDInsight baseado em Linux.

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um cliente SSH ou um cliente Beeline local. A maioria das etapas neste documento hello presumem que você está usando Beeline de um cluster de toohello sessão SSH. Para obter informações sobre a execução Beeline do cluster de saudação externa, consulte Olá [usar Beeline remotamente](#remote) seção.

    Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Usar o Beeline

1. Ao iniciar o Beeline, você deve fornecer uma cadeia de conexão para HiveServer2 em seu cluster HDInsight. comando de Olá toorun do cluster fora do hello, você deve fornecer nome de conta de logon de cluster de saudação (padrão `admin`) e a senha. Use Olá tabela toofind Olá conexão cadeia de caracteres formato e os parâmetros toouse a seguir:

    | De que local você executa o Beeline | parâmetros |
    | --- | --- | --- |
    | Um nó de um nó principal ou de borda de tooa do conexão SSH | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Cluster de saudação externa | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Por exemplo, Olá comando a seguir pode ser usado toostart Beeline de um cluster de toohello sessão SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Esse comando inicia o cliente de Beeline hello e conecta tooHiveServer2 no nó principal do cluster hello. Após a conclusão do comando hello, você chegar a um `jdbc:hive2://headnodehost:10001/>` prompt.

2. Os comandos Beeline normalmente começam com um caractere `!`, por exemplo, `!help` exibe a ajuda. No entanto Olá `!` pode ser omitido para alguns comandos. Por exemplo, `help` também funciona.

    Há um `!sql`, que é usado tooexecute HiveQL instruções. No entanto, HiveQL é usado muito comum que você pode omitir Olá anterior `!sql`. Olá duas instruções a seguir é equivalente:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    Em um novo cluster, somente uma tabela é listada: **hivesampletable**.

3. Use Olá comando toodisplay Olá esquema Olá hivesampletable a seguir:

    ```hiveql
    describe hivesampletable;
    ```

    Esse comando retorna Olá informações a seguir:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Essas informações descrevem colunas Olá na tabela de saudação. Enquanto estamos pode executar algumas consultas em relação a esses dados, vamos em vez disso, crie um novo toodemonstrate de tabela como dados tooload Hive e aplicar um esquema.

4. Digite hello seguindo as instruções toocreate uma tabela chamada **log4jLogs** usando dados de exemplo fornecidos com o cluster do HDInsight hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Essas instruções executam Olá ações a seguir:

    * `DROP TABLE`-Se Olá tabela existir, ele será excluído.

    * `CREATE EXTERNAL TABLE` – Cria uma tabela **externa** no Hive. Tabelas externas apenas armazenam a definição de tabela Olá no Hive. dados de saudação são deixados no local original hello.

    * `ROW FORMAT`-Como dados de saudação são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.

    * `STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e em qual formato de arquivo.

    * `SELECT`-Seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**. Essa consulta deve retornar um valor de **3**, já que existem três linhas que contêm esse valor.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive tentativas tooapply Olá esquema tooall arquivos Olá diretório. Nesse caso, o diretório de saudação contém arquivos que não correspondem ao esquema de saudação. dados de lixo tooprevent nos resultados de hello, essa instrução informa Hive que só deve retornar dados de arquivos que terminam em. log.

  > [!NOTE]
  > Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa. Por exemplo, um processo de upload de dados automatizado ou uma operação MapReduce.
  >
  > Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.

    saudação de saída desse comando é semelhante toohello seguinte texto:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. tooexit Beeline, use `!exit`.

## <a id="file"></a>Use Beeline toorun um arquivo de estilo

Use Olá etapas toocreate um arquivo, em seguida, executá-lo usando Beeline a seguir.

1. Comando de uso a seguir de saudação toocreate um arquivo chamado **query.hql**:

    ```bash
    nano query.hql
    ```

2. Use Olá depois do texto como conteúdo de saudação do arquivo hello. Essa consulta cria uma nova tabela 'interna' chamada **errorLogs**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Essas instruções executam Olá ações a seguir:

    * **Criar tabela IF NOT EXISTS** -se a tabela de saudação ainda não existir, ele será criado. Desde Olá **externo** palavra-chave não for usada, essa instrução cria uma tabela interna. Tabelas internas são armazenadas no data warehouse do hello Hive e são totalmente gerenciadas pelo Hive.
    * **ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC). O formato ORC é altamente otimizado e eficiente para o armazenamento de dados do Hive.
    * **INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.

    > [!NOTE]
    > Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.

3. arquivo de saudação toosave, use **Ctrl**+**x**, em seguida, digite **Y**e, finalmente, **Enter**.

4. Olá usar arquivo de saudação toorun usando Beeline a seguir:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Olá `-i` parâmetro Beeline é iniciado, executa Olá instruções no arquivo de query.hql hello. Após a conclusão da consulta hello, chegam Olá `jdbc:hive2://headnodehost:10001/>` prompt. Você também pode executar um arquivo usando Olá `-f` parâmetro, que será encerrado Beeline após a conclusão da consulta de saudação.

5. tooverify Olá **em decorrência** tabela foi criada, use Olá após a instrução tooreturn todos Olá linhas de **em decorrência**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4:

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Usar o Beeline remotamente

Se você tiver Beeline instalado localmente, ou são usá-lo por meio de uma imagem do Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), você deve usar o hello parâmetros a seguir:

* __Cadeia de conexão__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nome de logon do cluster__: `-n admin`

* __Senha de logon do cluster__ `-p 'password'`

Substituir saudação `clustername` na cadeia de caracteres de conexão de saudação com nome de saudação do cluster HDInsight.

Substituir `admin` com o nome de saudação do logon de cluster e substituir `password` com senha Olá para o seu logon de cluster.

## <a id="sparksql"></a>Usar Beeline com Spark

Spark fornece sua própria implementação de HiveServer2, que frequentemente mencionado como tooas Olá Spark Thrift servidor. Esse serviço usa consultas de tooresolve Spark SQL em vez de Hive e pode fornecer melhor desempenho, dependendo da consulta.

servidor de Spark Thrift toohello tooconnect de um Spark no HDInsight cluster, use porta `10002` em vez de `10001`. Por exemplo: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> servidor do Spark Thrift Olá é não diretamente acessível via Olá da internet. Somente pode se conectar a tooit de uma sessão SSH ou dentro Olá mesma rede Virtual do Azure como Olá cluster HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Próximas etapas

Para obter mais informações sobre o Hive no HDInsight, consulte Olá documento a seguir:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter mais informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight, consulte Olá documentos a seguir:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Se você estiver usando Tez com Hive, consulte Olá documentos a seguir:

* [Use Olá Tez UI no HDInsight baseados no Windows](hdinsight-debug-tez-ui.md)
* [Use Olá exibição Ambari Tez no HDInsight baseados em Linux](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
