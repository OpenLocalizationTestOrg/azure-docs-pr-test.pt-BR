---
title: aaaApache Sqoop com Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse tooimport Sqoop Apache e exportação entre Hadoop no HDInsight e um banco de dados do SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Use Apache Sqoop tooimport e exportar dados entre o banco de dados SQL e o Hadoop no HDInsight

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como cluster de toouse Apache Sqoop tooimport e exportação entre um Hadoop no HDInsight do Azure e banco de dados do banco de dados SQL ou Microsoft SQL Server. Olá etapas Olá de usar este documento `sqoop` comando diretamente da saudação um nó principal do cluster de Hadoop hello. Use o nó principal do SSH tooconnect toohello e executar comandos de saudação neste documento.

> [!IMPORTANT]
> Olá etapas deste documento só funcionam com clusters de HDInsight que usam o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Instalar o FreeTDS

1. Use SSH tooconnect toohello HDInsight cluster. Por exemplo, Olá comando a seguir se conecta a nó principal primário toohello de um cluster denominado `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Use Olá comando tooinstall FreeTDS a seguir:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    FreeTDS é usado em tooSQL tooconnect de várias etapas banco de dados.

## <a name="create-hello-table-in-sql-database"></a>Criar tabela de saudação no banco de dados SQL

> [!IMPORTANT]
> Se você estiver usando o cluster do HDInsight hello e banco de dados SQL criado no [criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md), ignore as etapas de saudação nesta seção. Olá banco de dados e tabela foram criados como parte da saudação etapas nas Olá [criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md) documento.

1. Da sessão SSH hello, use Olá servidor de banco de dados SQL do comando tooconnect toohello a seguir.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Você receberá a saída toohello semelhante texto a seguir:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. Em Olá `1>` prompt, digite Olá consulta a seguir:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas. Primeiro, Olá **mobiledata** tabela é criada e, em seguida, um índice clusterizado é adicionado tooit (exigido pelo banco de dados SQL).

    Saudação de uso tooverify de consulta que Olá a tabela a seguir foi criada:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Você verá a saída toohello semelhante texto a seguir:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.

## <a name="sqoop-export"></a>Exportação do Sqoop

1. De cluster para toohello de conexão do SSH hello, use Olá tooverify de comando que Sqoop pode ver o banco de dados SQL a seguir:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Quando solicitado, insira a senha de saudação para logon de banco de dados SQL hello.

    Esse comando retorna uma lista de bancos de dados, incluindo Olá **sqooptest** banco de dados que você criou anteriormente.

2. dados de tooexport de **hivesampletable** toohello **mobiledata** de tabela, use Olá comando a seguir:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Este comando instrui o Sqoop tooconnect toohello **sqooptest** banco de dados. Sqoop, em seguida, exporta dados de **wasb: / / / hive/warehouse/hivesampletable** toohello **mobiledata** tabela.

    > [!IMPORTANT]
    > Use `wasb:///` se o armazenamento padrão da saudação para seu cluster é uma conta de armazenamento do Azure. Use `adl:///` se for um Azure Data Lake Store.

3. Após a conclusão do comando hello, use Olá comando tooconnect toohello banco de dados usando TSQL a seguir:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Uma vez conectado, use Olá tooverify instruções que Olá dados a seguir foi exportado toohello **mobiledata** tabela:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Você deve ver uma lista dos dados na tabela de saudação. Tipo `exit` utilitário do tooexit Olá tsql.

## <a name="sqoop-import"></a>Importação do Sqoop

1. Dados tooimport de saudação do comando de uso a seguir de saudação **mobiledata** tabela no banco de dados SQL, toohello **wasb: / / / tutoriais/usesqoop/importeddata** do HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    campos de saudação nos dados de saudação são separados por um caractere de tabulação e linhas de saudação são terminadas por um caractere de nova linha.

2. Depois de saudação importação for concluída, use Olá toolist comando dados Olá no novo diretório de saudação a seguir:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Usar o SQL Server

Você também pode usar o Sqoop tooimport e exportar dados do SQL Server, no seu data center ou em uma máquina Virtual hospedada no Azure. Olá diferenças entre usar o banco de dados SQL e SQL Server são:

* HDInsight e o SQL Server deve ser em Olá mesma rede Virtual do Azure.

    Para obter um exemplo, consulte Olá [HDInsight conectar rede de local de tooyour](./connect-on-premises-network.md) documento.

    Para obter mais informações sobre como usar o HDInsight com uma rede Virtual do Azure, consulte Olá [estender HDInsight com a rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento. Para obter mais informações sobre a rede Virtual do Azure, consulte Olá [visão geral da rede Virtual](../virtual-network/virtual-networks-overview.md) documento.

* SQL Server deve ser configurado tooallow a autenticação do SQL. Para obter mais informações, consulte Olá [escolher um modo de autenticação](https://msdn.microsoft.com/ms144284.aspx) documento.

* Você pode ter conexões remotas do tooaccept tooconfigure do SQL Server. Para obter mais informações, consulte Olá [como tootroubleshoot conexão toohello do SQL Server do banco de dados mecanismo](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.

* Criar hello **sqooptest** banco de dados no SQL Server usando um utilitário como **SQL Server Management Studio** ou **tsql**. etapas de saudação para usar o hello CLI do Azure só funcionam para o banco de dados do SQL Azure.

    Olá Use Olá de toocreate de instruções Transact-SQL a seguir **mobiledata** tabela:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* Ao se conectar toohello do SQL Server de HDInsight, você pode ter toouse endereço IP de saudação de saudação do SQL Server. Por exemplo:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Limitações

* A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.

* Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop faz várias inserções em vez de envio em lote as operações de inserção hello.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse Sqoop. toolearn mais, consulte:

* [Usar o Oozie com o HDInsight][hdinsight-use-oozie]: use a ação do Sqoop no fluxo de trabalho do Oozie.
* [Analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.
* [Carregar dados tooHDInsight][hdinsight-upload-data]: encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
