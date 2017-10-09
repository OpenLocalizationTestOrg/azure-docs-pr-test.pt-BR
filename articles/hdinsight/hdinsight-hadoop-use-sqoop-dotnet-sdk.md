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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="7fe33-104">Executar trabalhos do Sqoop usando o SDK do .NET para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7fe33-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="7fe33-105">Saiba como toouse HDInsight .NET SDK toorun Sqoop trabalhos no HDInsight tooimport e exportar entre o cluster HDInsight e o banco de dados do SQL Azure ou o banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7fe33-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe33-106">etapas de saudação neste artigo podem ser usadas com qualquer um com base em Linux ou Windows cluster HDInsight; No entanto, essas etapas funcionam apenas de um cliente do Windows.</span><span class="sxs-lookup"><span data-stu-id="7fe33-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="7fe33-107">Use o seletor de guia de saudação na parte superior de saudação do toochoose artigo outros métodos.</span><span class="sxs-lookup"><span data-stu-id="7fe33-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="7fe33-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7fe33-108">Prerequisites</span></span>
<span data-ttu-id="7fe33-109">Antes de começar este tutorial, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7fe33-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="7fe33-110">**Um cluster Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7fe33-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="7fe33-111">Confira [Criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="7fe33-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="7fe33-112">Usar o Sqoop em clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7fe33-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="7fe33-113">Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="7fe33-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="7fe33-114">Nesta seção, você cria uma c# console aplicativo tooexport Olá hivesampletable toohello banco de dados SQL tabela criada anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="7fe33-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="7fe33-115">Enviar um trabalho de Sqoop</span><span class="sxs-lookup"><span data-stu-id="7fe33-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="7fe33-116">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="7fe33-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="7fe33-117">Olá Visual Studio Package Manager Console, execute Olá pacote do Nuget comando tooimport Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7fe33-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="7fe33-118">Use Olá código no arquivo Program.cs de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="7fe33-118">Use hello following code in hello Program.cs file:</span></span>
   
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
4. <span data-ttu-id="7fe33-119">Pressione **F5** toorun programa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7fe33-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="7fe33-120">Limitações</span><span class="sxs-lookup"><span data-stu-id="7fe33-120">Limitations</span></span>
* <span data-ttu-id="7fe33-121">A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="7fe33-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="7fe33-122">Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executa várias inserções em vez de envio em lote as operações de inserção hello.</span><span class="sxs-lookup"><span data-stu-id="7fe33-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe33-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7fe33-123">Next steps</span></span>
<span data-ttu-id="7fe33-124">Agora que você aprendeu como toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="7fe33-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="7fe33-125">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="7fe33-125">toolearn more, see:</span></span>

* <span data-ttu-id="7fe33-126">[Usar o Oozie com o HDInsight](hdinsight-use-oozie.md): use a ação do Sqoop no fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="7fe33-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="7fe33-127">[Analisar dados de atraso de voo usando HDInsight](hdinsight-analyze-flight-delay-data.md): usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7fe33-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="7fe33-128">[Carregar dados tooHDInsight](hdinsight-upload-data.md): encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.</span><span class="sxs-lookup"><span data-stu-id="7fe33-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

