---
title: "dados de aaaCopy entre repositório Data Lake e banco de dados do SQL Azure usando o Sqoop | Microsoft Docs"
description: "Usar Sqoop toocopy dados entre o banco de dados do SQL Azure e o repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Copiar dados entre o Repositório Data Lake e o banco de dados SQL do Azure usando o Sqoop
Saiba como toouse Apache Sqoop tooimport e exportação de dados entre o banco de dados do SQL Azure e o repositório Data Lake.

## <a name="what-is-sqoop"></a>O que é o Sqoop?
Os aplicativos de big data são uma opção natural para o processamento de dados semi-estruturados e não estruturados, como logs e arquivos. No entanto, também pode haver uma necessidade de dados tooprocess estruturados armazenados em bancos de dados relacionais.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) é uma ferramenta desenvolvida tootransfer dados entre bancos de dados relacionais e um repositório de dados grande, como repositório Data Lake. Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como o banco de dados do SQL Azure no repositório Data Lake. Você pode, em seguida, transformar e analisar dados hello usando dados de grandes cargas de trabalho e, em seguida, exportar dados de saudação volta para um RDBMS. Neste tutorial, você pode usar um banco de dados do SQL Azure como seu banco de dados relacional tooimport/exportação do.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Este artigo pressupõe que você tenha um cluster HDInsight Linux com acesso ao Repositório Data Lake.
* **Banco de dados SQL do Azure**. Para obter instruções sobre como um, ver toocreate [criar um banco de dados do SQL Azure](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Você aprende rapidamente com vídeos?
[Assista a este vídeo](https://mix.office.com/watch/1butcdjxmu114) sobre como os dados de toocopy entre Blobs de armazenamento do Azure e o repositório Data Lake usando DistCp.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Criar tabelas de exemplo no hello Azure SQL Database
1. toostart, crie duas tabelas de exemplo no hello Azure SQL Database. Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello banco de dados do SQL Azure e, em seguida, execute Olá seguindo consultas.

    **Criar Tabela1**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **Criar Tabela2**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. Na **Tabela1**, adicione alguns dados de exemplo. Deixe a **Tabela2** vazia. Importaremos dados da **Tabela1** para o Repositório Data Lake. Em seguida, exportaremos dados do Repositório Data Lake Store para a **Tabela2**. Execute Olá trecho de código a seguir.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Sqoop de uso de um cluster de HDInsight com acesso tooData Lake repositório
Um cluster HDInsight já tem pacotes de Sqoop Olá disponíveis. Se você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello como um armazenamento adicional, você pode usar o Sqoop (sem alterações de configuração) tooimport/exportar dados entre um banco de dados relacional (por exemplo, banco de dados do SQL Azure) e um repositório Data Lake conta.

1. Para este tutorial, vamos supor que você criou um cluster do Linux, então você deve usar SSH tooconnect toohello cluster. Consulte [conectar tooa HDInsight baseados em Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Verifique se você pode acessar Olá conta do repositório Data Lake do cluster hello. Execute Olá comando a seguir no prompt SSH hello:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Isso deve fornecer uma lista de arquivos/pastas Olá conta do repositório Data Lake.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Importar dados do Banco de Dados SQL do Azure para o Repositório Data Lake
1. Navegue toohello diretório onde os pacotes de Sqoop estão disponíveis. Normalmente, será `/usr/hdp/<version>/sqoop/bin`.
2. Importar dados de saudação do **Table1** em Olá conta do repositório Data Lake. Use Olá sintaxe a seguir:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Observe que **-banco de dados--nome do sql server** espaço reservado representa o nome de saudação do servidor de saudação onde o banco de dados do SQL Azure hello está sendo executado. **nome de banco de dados SQL** espaço reservado representa o nome do banco de dados real hello.

    Por exemplo,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Verifique se esse Olá dados foram transferidos toohello conta de repositório Data Lake. Execute Olá comando a seguir:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Você deve ver Olá saída a seguir.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Cada **parte-m -*** arquivo corresponde tooa linha na tabela de origem hello, **Table1**. Você pode exibir o conteúdo de saudação da parte Olá - m-* arquivos tooverify.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Exportar dados do Repositório Data Lake para o Banco de Dados SQL do Azure
1. Exportar dados de saudação do repositório Data Lake conta toohello tabela vazia **Table2**, em hello Azure SQL Database. Use Olá sintaxe a seguir.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Por exemplo,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Verifique se esse Olá dados foram carregada toohello tabela de banco de dados SQL. Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello banco de dados do SQL Azure e, em seguida, execute Olá seguindo a consulta.

        SELECT * FROM TABLE2

    Isso deve ter Olá saída a seguir.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Considerações de desempenho ao usar o Sqoop

Para o Sqoop de ajuste de desempenho de trabalho repositório toocopy data tooData Lake, consulte [documento de desempenho de Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Consulte também
* [Copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
