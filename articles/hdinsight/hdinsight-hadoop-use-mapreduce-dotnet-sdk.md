---
title: trabalhos de MapReduce aaaSubmit usando o HDInsight .NET SDK - Azure | Microsoft Docs
description: Saiba como toosubmit MapReduce trabalhos tooAzure HDInsight Hadoop usando o HDInsight .NET SDK.
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
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Executar trabalhos MapReduce usando o SDK do .NET do HDInsight
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Saiba como toosubmit MapReduce trabalhos usando o HDInsight .NET SDK. Os clusters HDInsight vêm com um arquivo jar com alguns exemplos de MapReduce. Olá jar arquivo é */example/jars/hadoop-mapreduce-examples.jar*.  Um dos exemplos de saudação é *wordcount*. Desenvolver um c# console aplicativo toosubmit um trabalho de wordcount.  trabalho de saudação lê Olá */example/data/gutenberg/davinci.txt* arquivo e as saídas Olá resultados muito*/example/data/davinciwordcount*.  Se você quiser toorerun Olá aplicativo, você deve limpar Olá pasta de saída.

> [!NOTE]
> etapas de saudação neste artigo devem ser executadas de um cliente do Windows. Para obter informações sobre como usar um Linux, OS X ou Unix cliente toowork com Hive, use o seletor de guia de saudação mostrado na parte superior de saudação do artigo hello.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter Olá itens a seguir:

* **Um cluster Hadoop no HDInsight**. Confira a [Introdução ao uso do Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Enviar trabalhos MapReduce usando o SDK do .NET do HDInsight
Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET. 

**trabalhos de tooSubmit**

1. No Visual Studio, crie um aplicativo de console C#.
2. Olá Nuget Package Manager Console, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Use Olá código a seguir:
   
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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
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
4. Pressione **F5** aplicativo hello de toorun.

trabalho de saudação toorun novamente, você deve alterar Olá trabalho saída nome de pasta, no exemplo hello, é "/ dados/exemplo/davinciwordcount".

Quando Olá for concluído com êxito, o aplicativo hello imprime conteúdo Olá Olá do arquivo de saída "parte-r-00000".

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu um cluster HDInsight toocreate de várias maneiras. toolearn mais, consulte Olá artigos a seguir:

* Para enviar um trabalho de Hive, consulte [Executar consultas Hive usando o SDK do .NET HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Para criar clusters HDInsight, confira [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Criar clusters Hadoop baseados em Linux no HDInsight).
* Para gerenciar clusters HDInsight, consulte [Gerenciar clusters Hadoop no HDInsight](hdinsight-administer-use-portal-linux.md).
* Para aprender Olá HDInsight .NET SDK, consulte [referência do HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).
* Para não interativo autenticar tooAzure, consulte [criar aplicativos .NET HDInsight de autenticação não interativo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

