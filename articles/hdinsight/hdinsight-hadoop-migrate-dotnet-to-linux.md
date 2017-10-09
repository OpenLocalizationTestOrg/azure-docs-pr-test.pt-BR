---
title: aaaUse .NET com Hadoop MapReduce no HDInsight baseados em Linux - Azure | Microsoft Docs
description: Saiba como aplicativos de .NET toouse para streaming MapReduce no HDInsight baseados em Linux.
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="82e96-103">Migrar soluções .NET para HDInsight baseados em Windows com base em tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="82e96-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="82e96-104">Uso de clusters HDInsight baseados em Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET.</span><span class="sxs-lookup"><span data-stu-id="82e96-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="82e96-105">Mono permite toouse componentes do .NET, como aplicativos de MapReduce com HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="82e96-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="82e96-106">Neste documento, saiba como soluções de .NET toomigrate criado para toowork de clusters HDInsight baseados em Windows com Mono no HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="82e96-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="82e96-107">Compatibilidade de Mono com .NET</span><span class="sxs-lookup"><span data-stu-id="82e96-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="82e96-108">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="82e96-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="82e96-109">Para obter mais informações sobre a versão de saudação do Mono incluído no HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="82e96-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="82e96-110">tooinstall uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="82e96-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="82e96-111">Para obter informações detalhadas sobre a compatibilidade entre Mono e .NET, consulte Olá [compatibilidade Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.</span><span class="sxs-lookup"><span data-stu-id="82e96-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82e96-112">estrutura SCP.NET Olá é compatível com Mono.</span><span class="sxs-lookup"><span data-stu-id="82e96-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="82e96-113">Para obter mais informações sobre como usar SCP.NET com Mono, consulte [topologias de toodevelop c# Use o Visual Studio para Apache Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="82e96-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="82e96-114">Análise automatizada de portabilidade</span><span class="sxs-lookup"><span data-stu-id="82e96-114">Automated portability analysis</span></span>

<span data-ttu-id="82e96-115">Olá [.NET portabilidade analisador](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) pode ser usado toogenerate um relatório de incompatibilidades entre seu aplicativo e Mono.</span><span class="sxs-lookup"><span data-stu-id="82e96-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="82e96-116">Use Olá seguindo as etapas tooconfigure Olá analisador toocheck seu aplicativo para a portabilidade Mono:</span><span class="sxs-lookup"><span data-stu-id="82e96-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="82e96-117">Instalar Olá [.NET portabilidade analisador](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="82e96-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="82e96-118">Durante a instalação, selecione a versão de saudação do toouse do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82e96-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="82e96-119">No Visual Studio 2015, selecione __analisar__ > __configurações do analisador de portabilidade__e certifique-se de que __4.5__ check-in Olá __Mono__  seção.</span><span class="sxs-lookup"><span data-stu-id="82e96-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5 verificados na seção Mono para configurações de analisador Olá](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="82e96-121">Selecione __Okey__ toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="82e96-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="82e96-122">Selecione __Analisar__ > __Analisar portabilidade do Assembly__.</span><span class="sxs-lookup"><span data-stu-id="82e96-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="82e96-123">Selecione Olá assembly que contém sua solução e, em seguida, selecione __abrir__ toobegin analysis.</span><span class="sxs-lookup"><span data-stu-id="82e96-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="82e96-124">Quando a análise for concluída, selecione __Analisar__ > __Exibir relatórios de análise__.</span><span class="sxs-lookup"><span data-stu-id="82e96-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="82e96-125">Em __resultados da análise de portabilidade__, selecione __abrir relatório__ tooopen um relatório.</span><span class="sxs-lookup"><span data-stu-id="82e96-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Caixa de diálogo de resultados do analisador de portabilidade](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="82e96-127">Analisador de saudação não pode capturar todos os problemas com sua solução.</span><span class="sxs-lookup"><span data-stu-id="82e96-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="82e96-128">Por exemplo, um caminho de arquivo de `c:\temp\file.txt` é considerado Okey porque Mono é executado no Windows e o caminho de saudação é válido nesse contexto.</span><span class="sxs-lookup"><span data-stu-id="82e96-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="82e96-129">No entanto, o caminho de saudação não é válido em uma plataforma Linux.</span><span class="sxs-lookup"><span data-stu-id="82e96-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="82e96-130">Análise de portabilidade manual</span><span class="sxs-lookup"><span data-stu-id="82e96-130">Manual portability analysis</span></span>

<span data-ttu-id="82e96-131">Realizar uma auditoria manual do seu código usando as informações de Olá Olá [portabilidade do aplicativo (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.</span><span class="sxs-lookup"><span data-stu-id="82e96-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="82e96-132">Modificar e criar</span><span class="sxs-lookup"><span data-stu-id="82e96-132">Modify and build</span></span>

<span data-ttu-id="82e96-133">Você pode continuar toouse Visual Studio toobuild suas soluções .NET para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82e96-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="82e96-134">No entanto, você deve garantir que esse projeto Olá é configurado toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="82e96-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="82e96-135">Implantar e testar</span><span class="sxs-lookup"><span data-stu-id="82e96-135">Deploy and test</span></span>

<span data-ttu-id="82e96-136">Depois de modificar sua solução usando Olá recomendações de saudação analisador de portabilidade de .NET ou de uma análise manual, você deve testá-lo com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82e96-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="82e96-137">Testando a solução Olá em um cluster HDInsight baseados em Linux pode revelar problemas sutis que precisam ser toobe corrigido.</span><span class="sxs-lookup"><span data-stu-id="82e96-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="82e96-138">Recomendamos que você habilite o registro em log adicional no seu aplicativo ao testá-lo.</span><span class="sxs-lookup"><span data-stu-id="82e96-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="82e96-139">Para obter mais informações sobre como acessar os logs, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e96-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="82e96-140">Acessar logs do aplicativo YARN no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="82e96-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="82e96-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82e96-141">Next steps</span></span>

* [<span data-ttu-id="82e96-142">Usar C# com MapReduce no HDInsight</span><span class="sxs-lookup"><span data-stu-id="82e96-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="82e96-143">Usar funções definidas pelo usuário do C# com Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="82e96-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="82e96-144">Desenvolver topologias C# para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="82e96-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)