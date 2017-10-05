---
title: "Enviar trabalhos MapReduce usando o SDK do .NET do HDInsight – Azure | Microsoft Docs"
description: Saiba como enviar trabalhos MapReduce para o Hadoop do Azure HDInsight usando o SDK do .NET do HDInsight.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="26647-103">Executar trabalhos MapReduce usando o SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="26647-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="26647-104">Saiba como enviar trabalhos MapReduce usando o SDK do .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26647-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="26647-105">Os clusters HDInsight vêm com um arquivo jar com alguns exemplos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="26647-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="26647-106">O arquivo jar está localizado em */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="26647-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="26647-107">Um dos exemplos é *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="26647-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="26647-108">Você desenvolve um aplicativo do console C# para enviar um trabalho wordcount.</span><span class="sxs-lookup"><span data-stu-id="26647-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="26647-109">O trabalho lê o arquivo */example/data/gutenberg/davinci.txt* e gera os resultados em */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="26647-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="26647-110">Se você desejar executar novamente o aplicativo, você deve limpar a pasta de saída.</span><span class="sxs-lookup"><span data-stu-id="26647-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="26647-111">As etapas neste artigo devem ser executadas em um cliente do Windows.</span><span class="sxs-lookup"><span data-stu-id="26647-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="26647-112">Para obter informações sobre como usar um cliente Linux, OS X ou Unix para trabalhar com o Hive, use o seletor de tabulação mostrado na parte superior do artigo.</span><span class="sxs-lookup"><span data-stu-id="26647-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="26647-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26647-113">Prerequisites</span></span>
<span data-ttu-id="26647-114">Antes de começar este artigo, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="26647-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="26647-115">**Um cluster Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="26647-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="26647-116">Confira a [Introdução ao uso do Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="26647-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="26647-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="26647-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="26647-118">Enviar trabalhos MapReduce usando o SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="26647-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="26647-119">O SDK do .NET do HDInsight fornece bibliotecas de cliente .NET que facilitam o trabalho com clusters HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="26647-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="26647-120">**Para enviar trabalhos**</span><span class="sxs-lookup"><span data-stu-id="26647-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="26647-121">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="26647-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="26647-122">No Console do Gerenciador de Pacotes NuGet, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="26647-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="26647-123">Use o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="26647-123">Use the following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="26647-124">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26647-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="26647-125">Para executar o trabalho novamente, é necessário alterar o nome da pasta de saída do trabalho, no exemplo, "/example/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="26647-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="26647-126">Quando o trabalho for concluído com êxito, o aplicativo imprimirá o conteúdo do arquivo de saída "part-r-00000".</span><span class="sxs-lookup"><span data-stu-id="26647-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="26647-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26647-127">Next steps</span></span>
<span data-ttu-id="26647-128">Neste artigo, você aprendeu várias maneiras de criar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26647-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="26647-129">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="26647-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="26647-130">Para enviar um trabalho de Hive, consulte [Executar consultas Hive usando o SDK do .NET HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="26647-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="26647-131">Para criar clusters HDInsight, confira [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Criar clusters Hadoop baseados em Linux no HDInsight).</span><span class="sxs-lookup"><span data-stu-id="26647-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="26647-132">Para gerenciar clusters HDInsight, consulte [Gerenciar clusters Hadoop no HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="26647-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="26647-133">Para aprender sobre o SDK do .NET do HDInsight, consulte [referência do SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="26647-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="26647-134">Para autenticação não interativa no Azure, confira [Criar aplicativos .NET HDInsight de autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="26647-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

