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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="47172-103">Executar trabalhos de Pig usando Olá SDK .NET para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="47172-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="47172-104">Saiba como toouse Olá SDK .NET para Hadoop toosubmit Apache Pig trabalhos tooHadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47172-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="47172-105">Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET que torna mais fácil toowork com clusters de HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="47172-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="47172-106">Pig permite operações de MapReduce toocreate por uma série de transformações de dados de modelagem.</span><span class="sxs-lookup"><span data-stu-id="47172-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="47172-107">Neste documento, você aprenderá como toouse básica c# aplicativo toosubmit um Pig trabalho tooan HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="47172-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47172-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47172-108">Prerequisites</span></span>

<span data-ttu-id="47172-109">toocomplete Olá etapas neste artigo, você precisa seguir hello.</span><span class="sxs-lookup"><span data-stu-id="47172-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="47172-110">Um cluster do Azure HDInsight (Hadoop no HDInsight) (Windows ou Linux).</span><span class="sxs-lookup"><span data-stu-id="47172-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="47172-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="47172-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47172-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="47172-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="47172-113">Visual Studio 2012, 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="47172-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="47172-114">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="47172-114">Create hello application</span></span>

<span data-ttu-id="47172-115">Olá HDInsight .NET SDK fornece bibliotecas de cliente .NET, o que torna mais fácil toowork com clusters de HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="47172-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="47172-116">De saudação **arquivo** menu do Visual Studio, selecione **novo** e, em seguida, selecione **projeto**.</span><span class="sxs-lookup"><span data-stu-id="47172-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="47172-117">Para o novo projeto de hello, tipo ou hello select a seguir valores:</span><span class="sxs-lookup"><span data-stu-id="47172-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="47172-118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47172-118">Property</span></span> | <span data-ttu-id="47172-119">Valor</span><span class="sxs-lookup"><span data-stu-id="47172-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="47172-120">Categoria</span><span class="sxs-lookup"><span data-stu-id="47172-120">Category</span></span> | <span data-ttu-id="47172-121">Modelos/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="47172-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="47172-122">Modelo</span><span class="sxs-lookup"><span data-stu-id="47172-122">Template</span></span> | <span data-ttu-id="47172-123">Aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="47172-123">Console Application</span></span> |
   | <span data-ttu-id="47172-124">Nome</span><span class="sxs-lookup"><span data-stu-id="47172-124">Name</span></span> | <span data-ttu-id="47172-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="47172-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="47172-126">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="47172-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="47172-127">De saudação **ferramentas** menu, selecione **Gerenciador de biblioteca de pacote** ou **Nuget Package Manager**e, em seguida, selecione **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="47172-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="47172-128">pacotes de SDK .NET de saudação tooinstall, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="47172-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="47172-129">No Gerenciador de soluções, clique duas vezes em **Program.cs** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="47172-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="47172-130">Substitua código existente Olá seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="47172-130">Replace hello existing code with hello following.</span></span>

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

7. <span data-ttu-id="47172-131">aplicativo de hello toostart, pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="47172-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="47172-132">aplicativo de hello tooexit, pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="47172-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="47172-133">Resumo</span><span class="sxs-lookup"><span data-stu-id="47172-133">Summary</span></span>

<span data-ttu-id="47172-134">Como você pode ver, o hello SDK .NET para Hadoop permite que aplicativos de .NET toocreate envie o cluster HDInsight do Pig trabalhos tooan e monitoram o status do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="47172-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47172-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47172-135">Next steps</span></span>

<span data-ttu-id="47172-136">Para obter informações sobre o Pig no HDInsight, consulte [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="47172-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="47172-137">Para obter mais informações sobre como usar o Hadoop no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="47172-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="47172-138">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="47172-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="47172-139">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="47172-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
