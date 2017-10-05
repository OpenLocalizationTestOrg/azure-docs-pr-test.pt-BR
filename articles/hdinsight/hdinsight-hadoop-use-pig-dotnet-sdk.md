---
title: "Executar trabalhos de Pig do Apache com o SDK do .NET para Hadoop – Azure HDInsight | Microsoft Docs"
description: Aprenda a usar o SDK do .NET do Hadoop para enviar trabalhos do Pig para Hadoop no HDInsight.
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
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="802b4-103">Executar trabalhos do Pig usando o SDK do .NET para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="802b4-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="802b4-104">Aprenda a usar o SDK do .NET do Hadoop para enviar trabalhos do Pig Apache para Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802b4-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="802b4-105">O SDK do .NET do HDInsight fornece bibliotecas de cliente .NET que facilitam o trabalho com clusters HDInsight no .NET.</span><span class="sxs-lookup"><span data-stu-id="802b4-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="802b4-106">O Pig permite que você crie operações MapReduce ao modelar uma série de transformações de dados.</span><span class="sxs-lookup"><span data-stu-id="802b4-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="802b4-107">Neste documento, você aprenderá como usar um aplicativo C# básico para enviar um trabalho do Pig para um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802b4-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="802b4-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="802b4-108">Prerequisites</span></span>

<span data-ttu-id="802b4-109">Para concluir as etapas deste artigo, você precisa do seguinte.</span><span class="sxs-lookup"><span data-stu-id="802b4-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="802b4-110">Um cluster do Azure HDInsight (Hadoop no HDInsight) (Windows ou Linux).</span><span class="sxs-lookup"><span data-stu-id="802b4-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="802b4-111">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="802b4-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="802b4-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="802b4-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="802b4-113">Visual Studio 2012, 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="802b4-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="802b4-114">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="802b4-114">Create the application</span></span>

<span data-ttu-id="802b4-115">O SDK do .NET do HDInsight fornece bibliotecas de cliente .NET que facilitam o trabalho com clusters HDInsight do .NET.</span><span class="sxs-lookup"><span data-stu-id="802b4-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="802b4-116">No Visual Studio, no menu **Arquivo**, selecione **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="802b4-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="802b4-117">Para o novo projeto, digite ou selecione os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="802b4-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="802b4-118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="802b4-118">Property</span></span> | <span data-ttu-id="802b4-119">Valor</span><span class="sxs-lookup"><span data-stu-id="802b4-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="802b4-120">Categoria</span><span class="sxs-lookup"><span data-stu-id="802b4-120">Category</span></span> | <span data-ttu-id="802b4-121">Modelos/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="802b4-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="802b4-122">Modelo</span><span class="sxs-lookup"><span data-stu-id="802b4-122">Template</span></span> | <span data-ttu-id="802b4-123">Aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="802b4-123">Console Application</span></span> |
   | <span data-ttu-id="802b4-124">Nome</span><span class="sxs-lookup"><span data-stu-id="802b4-124">Name</span></span> | <span data-ttu-id="802b4-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="802b4-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="802b4-126">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="802b4-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="802b4-127">No menu **Ferramentas**, selecione **Gerenciador de Pacotes da Biblioteca** ou **Gerenciador de Pacotes Nuget** e depois selecione **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="802b4-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="802b4-128">Execute o seguinte comando para instalar os pacotes do SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="802b4-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="802b4-129">No Gerenciador de Soluções, clique duas vezes em **Program.cs** para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="802b4-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="802b4-130">Substitua o código existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="802b4-130">Replace the existing code with the following.</span></span>

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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
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

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="802b4-131">Pressione **F5** para iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="802b4-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="802b4-132">Pressione **ENTER** para sair do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="802b4-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="802b4-133">Resumo</span><span class="sxs-lookup"><span data-stu-id="802b4-133">Summary</span></span>

<span data-ttu-id="802b4-134">Como você pode ver, o SDK para .NET do Hadoop permite criar aplicativos .NET que enviam trabalhos do Pig para um cluster HDInsight e monitorar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="802b4-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="802b4-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="802b4-135">Next steps</span></span>

<span data-ttu-id="802b4-136">Para obter informações sobre o Pig no HDInsight, consulte [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="802b4-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="802b4-137">Para saber mais sobre como usar o Hadoop no HDInsight, veja os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="802b4-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="802b4-138">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="802b4-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="802b4-139">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="802b4-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
