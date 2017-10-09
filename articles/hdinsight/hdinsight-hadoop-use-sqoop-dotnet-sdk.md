---
title: aaaRun Sqoop trabalhos usando o .NET e HDInsight - Azure | Microsoft Docs
description: Saiba como toouse HDInsight .NET SDK toorun Sqoop importar e exportar entre um cluster de Hadoop e um banco de dados do SQL Azure.
keywords: trabalho de sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Executar trabalhos do Sqoop usando o SDK do .NET para Hadoop no HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como toouse HDInsight .NET SDK toorun Sqoop trabalhos no HDInsight tooimport e exportar entre o cluster HDInsight e o banco de dados do SQL Azure ou o banco de dados do SQL Server.

> [!NOTE]
> etapas de saudação neste artigo podem ser usadas com qualquer um com base em Linux ou Windows cluster HDInsight; No entanto, essas etapas funcionam apenas de um cliente do Windows. Use o seletor de guia de saudação na parte superior de saudação do toochoose artigo outros métodos.
> 
> 

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter Olá itens a seguir:

* **Um cluster Hadoop no HDInsight**. Confira [Criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Usar o Sqoop em clusters HDInsight usando o SDK do .NET
Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET. Nesta seção, você cria uma c# console aplicativo tooexport Olá hivesampletable toohello banco de dados SQL tabela criada anteriormente neste tutorial.

## <a name="submit-a-sqoop-job"></a>Enviar um trabalho de Sqoop

1. No Visual Studio, crie um aplicativo de console C#.
2. Olá Visual Studio Package Manager Console, execute Olá pacote do Nuget comando tooimport Olá a seguir.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Use Olá código no arquivo Program.cs de saudação a seguir:
   
        using System.Collections.Generic;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. Pressione **F5** toorun programa de saudação. 

## <a name="limitations"></a>Limitações
* A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.
* Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executa várias inserções em vez de envio em lote as operações de inserção hello.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como toouse Sqoop. toolearn mais, consulte:

* [Usar o Oozie com o HDInsight](hdinsight-use-oozie.md): use a ação do Sqoop no fluxo de trabalho do Oozie.
* [Analisar dados de atraso de voo usando HDInsight](hdinsight-analyze-flight-delay-data.md): usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.
* [Carregar dados tooHDInsight](hdinsight-upload-data.md): encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.

