---
title: "Executar trabalhos Sqoop usando o .NET e o HDInsight – Azure | Microsoft Docs"
description: "Aprenda como usar o SDK .NET do HDInsight para executar a importação e a exportação do Sqoop entre um cluster do Hadoop e um banco de dados SQL do Azure."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="5a388-104">Executar trabalhos do Sqoop usando o SDK do .NET para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a388-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="5a388-105">Saiba como usar o SDK .NET do HDInsight para executar trabalhos do Sqoop no HDInsight a fim de importar e exportar entre um cluster HDInsight e um banco de dados SQL do Azure ou um banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a388-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="5a388-106">As etapas neste artigo podem ser usadas com qualquer cluster HDInsight baseado em Linux ou Windows. No entanto, essas etapas só funcionam em um cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="5a388-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="5a388-107">Use o seletor de tabulação na parte superior deste artigo para escolher outros métodos.</span><span class="sxs-lookup"><span data-stu-id="5a388-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="5a388-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5a388-108">Prerequisites</span></span>
<span data-ttu-id="5a388-109">Antes de começar este tutorial, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5a388-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="5a388-110">**Um cluster Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5a388-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="5a388-111">Confira [Criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="5a388-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="5a388-112">Usar o Sqoop em clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="5a388-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="5a388-113">O SDK do .NET do HDInsight fornece bibliotecas de cliente .NET que facilitam o trabalho com clusters HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="5a388-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="5a388-114">Nesta seção, você cria um aplicativo de console em C# a fim de exportar o hivesampletable para a tabela Banco de Dados SQL criada por você neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5a388-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="5a388-115">Enviar um trabalho de Sqoop</span><span class="sxs-lookup"><span data-stu-id="5a388-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="5a388-116">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="5a388-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="5a388-117">No Console do Gerenciador de Pacotes do Visual Studio, execute o seguinte comando do Nuget para importar o pacote.</span><span class="sxs-lookup"><span data-stu-id="5a388-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="5a388-118">Use o seguinte código no arquivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5a388-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="5a388-119">Pressione **F5** para executar o programa.</span><span class="sxs-lookup"><span data-stu-id="5a388-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="5a388-120">Limitações</span><span class="sxs-lookup"><span data-stu-id="5a388-120">Limitations</span></span>
* <span data-ttu-id="5a388-121">Exportação em massa — com HDInsight baseado em Linux, o conector Sqoop usado para exportar dados no Microsoft SQL Server ou no Banco de Dados SQL do Azure, atualmente, não permite inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="5a388-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="5a388-122">Envio em lote — Com HDInsight baseado em Linux, ao usar o comutador `-batch` ao executar inserções, o Sqoop realizará várias inserções em vez de operações de inserção em lotes.</span><span class="sxs-lookup"><span data-stu-id="5a388-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a388-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a388-123">Next steps</span></span>
<span data-ttu-id="5a388-124">Você aprendeu como usar Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5a388-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="5a388-125">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="5a388-125">To learn more, see:</span></span>

* <span data-ttu-id="5a388-126">[Usar o Oozie com o HDInsight](hdinsight-use-oozie.md): use a ação do Sqoop no fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="5a388-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="5a388-127">[Analisar dados de atraso de voos usando o HDInsight](hdinsight-analyze-flight-delay-data.md): use o Hive para analisar dados de atraso de voos e o Sqoop para exportar dados para o banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a388-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="5a388-128">[Carregar dados no HDInsight](hdinsight-upload-data.md): localize outros métodos de carregamento de dados no HDInsight/Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a388-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

