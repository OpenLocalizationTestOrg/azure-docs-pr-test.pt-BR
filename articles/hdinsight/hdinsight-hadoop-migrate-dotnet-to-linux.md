---
title: "Use .NET com Hadoop MapReduce no HDInsight baseado em Linux – Azure | Microsoft Docs"
description: Saiba como usar aplicativos .NET para streaming de MapReduce no HDInsight baseado em Linux.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="c5380-103">Migrar soluções .NET do HDInsight baseado em Windows para o HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="c5380-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="c5380-104">Clusters do HDInsight baseado em Linux usam [Mono (https://mono-project.com)](https://mono-project.com) para executar aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="c5380-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="c5380-105">Mono permite que você use componentes .NET como aplicativos MapReduce com HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="c5380-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="c5380-106">Neste documento, saiba como migrar soluções .NET criadas para clusters de HDInsight baseados no Windows para funcionar com Mono no HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="c5380-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="c5380-107">Compatibilidade de Mono com .NET</span><span class="sxs-lookup"><span data-stu-id="c5380-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="c5380-108">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="c5380-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="c5380-109">Para obter mais informações sobre a versão de Mono incluída com o HDInsight, consulte [Versão de componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c5380-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="c5380-110">Para instalar uma versão específica do Mono, consulte o documento [Instalar ou atualizar](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="c5380-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="c5380-111">Para obter informações detalhadas sobre a compatibilidade entre Mono e .NET, consulte o documento [Compatibilidade do Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="c5380-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5380-112">A estrutura SCP.NET é compatível com Mono.</span><span class="sxs-lookup"><span data-stu-id="c5380-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="c5380-113">Para obter mais informações sobre como usar SCP.NET com Mono, consulte [Usar o Visual Studio para desenvolver topologias C# para Apache Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c5380-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="c5380-114">Análise automatizada de portabilidade</span><span class="sxs-lookup"><span data-stu-id="c5380-114">Automated portability analysis</span></span>

<span data-ttu-id="c5380-115">O [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) pode ser usado para gerar um relatório de incompatibilidades entre seu aplicativo e Mono.</span><span class="sxs-lookup"><span data-stu-id="c5380-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="c5380-116">Use as etapas a seguir para configurar o analisador para verificar seu aplicativo para portabilidade Mono:</span><span class="sxs-lookup"><span data-stu-id="c5380-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="c5380-117">Instalar o [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="c5380-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="c5380-118">Durante a instalação, selecione a versão do Visual Studio a ser usada.</span><span class="sxs-lookup"><span data-stu-id="c5380-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="c5380-119">No Visual Studio 2015, selecione __Analisar__ > __Configurações do Portability Analyzer__e verifique se __4.5__ está marcado na seção __Mono__.</span><span class="sxs-lookup"><span data-stu-id="c5380-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 marcado na seção Mono para as configurações do analisador](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="c5380-121">Clique em __OK__ para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c5380-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="c5380-122">Selecione __Analisar__ > __Analisar portabilidade do Assembly__.</span><span class="sxs-lookup"><span data-stu-id="c5380-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="c5380-123">Selecione o assembly que contém sua solução e selecione __Abrir__ para iniciar a análise.</span><span class="sxs-lookup"><span data-stu-id="c5380-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="c5380-124">Quando a análise for concluída, selecione __Analisar__ > __Exibir relatórios de análise__.</span><span class="sxs-lookup"><span data-stu-id="c5380-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="c5380-125">Em __Resultados da análise de portabilidade__, selecione __Abrir relatório__ para abrir um relatório.</span><span class="sxs-lookup"><span data-stu-id="c5380-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Caixa de diálogo de resultados do analisador de portabilidade](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="c5380-127">O analisador não pode capturar todos os problemas com sua solução.</span><span class="sxs-lookup"><span data-stu-id="c5380-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="c5380-128">Por exemplo, um caminho de arquivo de `c:\temp\file.txt` é considerado OK porque o Mono é executado no Windows e o caminho é válido nesse contexto.</span><span class="sxs-lookup"><span data-stu-id="c5380-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="c5380-129">No entanto, o caminho não é válido em uma plataforma Linux.</span><span class="sxs-lookup"><span data-stu-id="c5380-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="c5380-130">Análise de portabilidade manual</span><span class="sxs-lookup"><span data-stu-id="c5380-130">Manual portability analysis</span></span>

<span data-ttu-id="c5380-131">Realizar uma auditoria manual do seu código usando as informações no documento [Portabilidade do aplicativo (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/).</span><span class="sxs-lookup"><span data-stu-id="c5380-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="c5380-132">Modificar e criar</span><span class="sxs-lookup"><span data-stu-id="c5380-132">Modify and build</span></span>

<span data-ttu-id="c5380-133">Você pode continuar a usar o Visual Studio para criar soluções .NET para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c5380-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="c5380-134">No entanto, você deve garantir que o projeto esteja configurado para usar o .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c5380-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="c5380-135">Implantar e testar</span><span class="sxs-lookup"><span data-stu-id="c5380-135">Deploy and test</span></span>

<span data-ttu-id="c5380-136">Depois de modificar a solução usando as recomendações do .NET Portability Analyzer ou de uma análise manual, teste-o com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c5380-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="c5380-137">O teste da solução em um cluster HDInsight baseado em Linux pode revelar problemas sutis que precisam ser corrigidos.</span><span class="sxs-lookup"><span data-stu-id="c5380-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="c5380-138">Recomendamos que você habilite o registro em log adicional no seu aplicativo ao testá-lo.</span><span class="sxs-lookup"><span data-stu-id="c5380-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="c5380-139">Para obter mais informações sobre como acessar logs, veja os documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5380-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="c5380-140">Acessar logs do aplicativo YARN no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="c5380-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="c5380-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5380-141">Next steps</span></span>

* [<span data-ttu-id="c5380-142">Usar C# com MapReduce no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5380-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="c5380-143">Usar funções definidas pelo usuário do C# com Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="c5380-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="c5380-144">Desenvolver topologias C# para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5380-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)