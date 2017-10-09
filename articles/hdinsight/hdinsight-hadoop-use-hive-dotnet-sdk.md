---
title: consultas de Hive aaaRun usando o HDInsight .NET SDK - Azure | Microsoft Docs
description: Saiba como toosubmit Hadoop trabalhos tooAzure HDInsight Hadoop usando o HDInsight .NET SDK.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="29701-103">Executar consultas Hive usando o SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="29701-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="29701-104">Saiba como toosubmit Hive consultas usando o HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="29701-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="29701-105">Escrever uma consulta de Hive para listar as tabelas da seção de um toosubmit de programa c# e exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="29701-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="29701-106">etapas de saudação neste artigo devem ser executadas de um cliente do Windows.</span><span class="sxs-lookup"><span data-stu-id="29701-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="29701-107">Para obter informações sobre como usar um Linux, OS X ou Unix cliente toowork com Hive, use o seletor de guia de saudação mostrado na parte superior de saudação do artigo hello.</span><span class="sxs-lookup"><span data-stu-id="29701-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="29701-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29701-108">Prerequisites</span></span>
<span data-ttu-id="29701-109">Antes de começar este artigo, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="29701-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="29701-110">**Um cluster Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="29701-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="29701-111">Confira a [Introdução ao uso do Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="29701-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="29701-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="29701-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="29701-113">Enviar consultas do Hive usando o SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="29701-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="29701-114">Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="29701-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="29701-115">**trabalhos de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="29701-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="29701-116">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="29701-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="29701-117">Olá Nuget Package Manager Console, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29701-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="29701-118">Use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="29701-118">Use hello following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="29701-119">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="29701-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="29701-120">saída de saudação do aplicativo hello deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="29701-120">hello output of hello application shall be similar to:</span></span>

![Saída do trabalho do Hive do Hadoop HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="29701-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29701-122">Next steps</span></span>
<span data-ttu-id="29701-123">Neste artigo, você aprendeu um cluster HDInsight toocreate de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="29701-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="29701-124">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29701-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="29701-125">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="29701-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="29701-126">[Criar clusters Hadoop no HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="29701-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="29701-127">Gerenciar clusters Hadoop em HDInsight usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="29701-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="29701-128">Referência de SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="29701-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="29701-129">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="29701-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="29701-130">Use o Sqoop com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="29701-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="29701-131">Criar aplicativos .NET HDInsight de autenticação não interativa</span><span class="sxs-lookup"><span data-stu-id="29701-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


