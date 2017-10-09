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
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Executar consultas Hive usando o SDK .NET do HDInsight
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Saiba como toosubmit Hive consultas usando o HDInsight .NET SDK. Escrever uma consulta de Hive para listar as tabelas da seção de um toosubmit de programa c# e exibir resultados de saudação.

> [!NOTE]
> etapas de saudação neste artigo devem ser executadas de um cliente do Windows. Para obter informações sobre como usar um Linux, OS X ou Unix cliente toowork com Hive, use o seletor de guia de saudação mostrado na parte superior de saudação do artigo hello.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter Olá itens a seguir:

* **Um cluster Hadoop no HDInsight**. Confira a [Introdução ao uso do Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Enviar consultas do Hive usando o SDK do .NET do HDInsight
Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET. 

**trabalhos de tooSubmit**

1. No Visual Studio, crie um aplicativo de console C#.
2. Olá Nuget Package Manager Console, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Use Olá código a seguir:

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
4. Pressione **F5** aplicativo hello de toorun.

saída de saudação do aplicativo hello deverá ser semelhante a:

![Saída do trabalho do Hive do Hadoop HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu um cluster HDInsight toocreate de várias maneiras. toolearn mais, consulte Olá artigos a seguir:

* [Introdução ao Azure HDInsight][hdinsight-get-started]
* [Criar clusters Hadoop no HDInsight][hdinsight-provision]
* [Gerenciar clusters Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-management-portal.md)
* [Referência de SDK .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Use o Sqoop com o HDInsight](hdinsight-use-sqoop-mac-linux.md)
* [Criar aplicativos .NET HDInsight de autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


