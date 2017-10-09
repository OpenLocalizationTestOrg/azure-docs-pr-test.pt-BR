---
title: aaaRun Pig Apache trabalhos com o SDK .NET para Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Olá SDK .NET para tooHadoop de trabalhos do Hadoop toosubmit Pig no HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Executar trabalhos de Pig usando Olá SDK .NET para Hadoop no HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Saiba como toouse Olá SDK .NET para Hadoop toosubmit Apache Pig trabalhos tooHadoop no Azure HDInsight.

Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET que torna mais fácil toowork com clusters de HDInsight do .NET. Pig permite operações de MapReduce toocreate por uma série de transformações de dados de modelagem. Neste documento, você aprenderá como toouse básica c# aplicativo toosubmit um Pig trabalho tooan HDInsight cluster.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete Olá etapas neste artigo, você precisa seguir hello.

* Um cluster do Azure HDInsight (Hadoop no HDInsight) (Windows ou Linux).

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 ou 2017.

## <a name="create-hello-application"></a>Criar um aplicativo hello

Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET.

1. De saudação **arquivo** menu do Visual Studio, selecione **novo** e, em seguida, selecione **projeto**.

2. Para o novo projeto de hello, tipo ou hello select a seguir valores:

   | Propriedade | Valor |
   | ------ | ------ |
   | Categoria | Modelos/Visual C#/Windows |
   | Modelo | Aplicativo de console |
   | Nome | SubmitPigJob |

3. Clique em **Okey** toocreate projeto de saudação.

4. De saudação **ferramentas** menu, selecione **Gerenciador de biblioteca de pacote** ou **Nuget Package Manager**e, em seguida, selecione **Package Manager Console**.

5. pacotes de SDK .NET de saudação tooinstall, use Olá comando a seguir:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. No Gerenciador de soluções, clique duas vezes em **Program.cs** tooopen-lo. Substitua código existente Olá seguinte hello.

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. aplicativo de hello toostart, pressione **F5**.

8. aplicativo de hello tooexit, pressione **ENTER**.

## <a name="summary"></a>Resumo

Como você pode ver, o hello SDK .NET para Hadoop permite que aplicativos de .NET toocreate envie o cluster HDInsight do Pig trabalhos tooan e monitoram o status do trabalho hello.

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre o Pig no HDInsight, consulte [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).

Para obter mais informações sobre como usar o Hadoop no HDInsight, consulte Olá documentos a seguir:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
