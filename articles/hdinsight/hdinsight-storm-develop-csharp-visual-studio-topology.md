---
title: "topologias de profusão de aaaApache com Visual Studio e c# - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toocreate as topologias Storm em c#. Crie uma topologia de contagem de palavras simples no Visual Studio usando ferramentas Hadoop de saudação do Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="fb5c3-104">Desenvolver topologias c# para o Apache Storm usando ferramentas de Data Lake Olá para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb5c3-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="fb5c3-105">Saiba como toocreate uma topologia c# Storm usando hello Azure Data Lake (Hadoop) ferramentas para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="fb5c3-106">Este documento orienta pelo processo de saudação de criar um projeto Storm no Visual Studio, testá-lo localmente e implantá-la tooan Apache Storm no cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="fb5c3-107">Você também aprenderá como topologias híbridas toocreate que usam componentes c# e Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5c3-108">Enquanto etapas Olá neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio, o projeto compilado Olá pode ser tooeither enviado um cluster Linux ou HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="fb5c3-109">Somente os clusters baseados em Linux criados depois de 28 de outubro de 2016 são compatíveis com as topologias do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="fb5c3-110">topologia toouse c# com um cluster baseado em Linux, você deve atualizar Olá Microsoft.SCP.Net.SDK NuGet pacote usado pelo seu projeto tooversion 0.10.0.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="fb5c3-111">versão de saudação do pacote de saudação também deve corresponder a versão principal de saudação do Storm instalado no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="fb5c3-112">Versão do HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-112">HDInsight version</span></span> | <span data-ttu-id="fb5c3-113">Versão do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-113">Storm version</span></span> | <span data-ttu-id="fb5c3-114">Versão do SCP.NET</span><span class="sxs-lookup"><span data-stu-id="fb5c3-114">SCP.NET version</span></span> | <span data-ttu-id="fb5c3-115">Versão Mono padrão</span><span class="sxs-lookup"><span data-stu-id="fb5c3-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="fb5c3-116">3.3</span><span class="sxs-lookup"><span data-stu-id="fb5c3-116">3.3</span></span> |<span data-ttu-id="fb5c3-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-117">0.10.x</span></span> |<span data-ttu-id="fb5c3-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-118">0.10.x.x</span></span></br><span data-ttu-id="fb5c3-119">(somente em HDInsight baseado no Windows)</span><span class="sxs-lookup"><span data-stu-id="fb5c3-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="fb5c3-120">ND</span><span class="sxs-lookup"><span data-stu-id="fb5c3-120">NA</span></span> |
| <span data-ttu-id="fb5c3-121">3.4</span><span class="sxs-lookup"><span data-stu-id="fb5c3-121">3.4</span></span> | <span data-ttu-id="fb5c3-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-122">0.10.0.x</span></span> | <span data-ttu-id="fb5c3-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-123">0.10.0.x</span></span> | <span data-ttu-id="fb5c3-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="fb5c3-124">3.2.8</span></span> |
| <span data-ttu-id="fb5c3-125">3,5</span><span class="sxs-lookup"><span data-stu-id="fb5c3-125">3.5</span></span> | <span data-ttu-id="fb5c3-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-126">1.0.2.x</span></span> | <span data-ttu-id="fb5c3-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-127">1.0.0.x</span></span> | <span data-ttu-id="fb5c3-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="fb5c3-128">4.2.1</span></span> |
| <span data-ttu-id="fb5c3-129">3.6</span><span class="sxs-lookup"><span data-stu-id="fb5c3-129">3.6</span></span> | <span data-ttu-id="fb5c3-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-130">1.1.0.x</span></span> | <span data-ttu-id="fb5c3-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="fb5c3-131">1.0.0.x</span></span> | <span data-ttu-id="fb5c3-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="fb5c3-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="fb5c3-133">C# topologias em clusters baseados em Linux devem usar o .NET 4.5 e use toorun Mono no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="fb5c3-134">Verificar [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para possíveis incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="fb5c3-135">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb5c3-135">Install Visual Studio</span></span>

<span data-ttu-id="fb5c3-136">Você pode desenvolver c# topologias com SCP.NET usando uma saudação seguintes versões do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="fb5c3-137">Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="fb5c3-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="fb5c3-138">Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="fb5c3-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="fb5c3-139">Visual Studio 2015 ou [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="fb5c3-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="fb5c3-140">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="fb5c3-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="fb5c3-141">Instalar ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb5c3-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="fb5c3-142">ferramentas de Data Lake tooinstall para Visual Studio, siga as etapas de saudação em [começar a usar as ferramentas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="fb5c3-143">Instalar o Java</span><span class="sxs-lookup"><span data-stu-id="fb5c3-143">Install Java</span></span>

<span data-ttu-id="fb5c3-144">Quando você enviar uma topologia Storm do Visual Studio, SCP.NET gera um arquivo zip que contém as dependências e topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="fb5c3-145">Java é usado toocreate esses arquivos, zip, porque ele usa um formato que é mais compatível com clusters baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="fb5c3-146">Instale Olá Java Developer Kit (JDK) 7 ou posterior em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="fb5c3-147">Você pode obter Olá Oracle JDK [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="fb5c3-148">Você também pode usar [outras distribuições do Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="fb5c3-149">Olá `JAVA_HOME` diretório de toohello de ponto de deve variável de ambiente que contém Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="fb5c3-150">Olá `PATH` variável de ambiente deve incluir Olá `%JAVA_HOME%\bin` directory.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="fb5c3-151">Você pode usar o hello c# console aplicativo tooverify Java e hello JDK estão corretamente instalados a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="fb5c3-152">Modelos do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-152">Storm templates</span></span>

<span data-ttu-id="fb5c3-153">ferramentas de Data Lake Olá para Visual Studio fornecem Olá modelos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="fb5c3-154">Tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="fb5c3-154">Project type</span></span> | <span data-ttu-id="fb5c3-155">Demonstra</span><span class="sxs-lookup"><span data-stu-id="fb5c3-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="fb5c3-156">Aplicativo Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-156">Storm Application</span></span> |<span data-ttu-id="fb5c3-157">Um projeto de topologia Storm vazio.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="fb5c3-158">Amostra de gravador do SQL Azure Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="fb5c3-159">Como toowrite tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="fb5c3-160">Amostra de leitor do Azure Cosmos DB do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="fb5c3-161">Como tooread do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="fb5c3-162">Amostra do gravador do Azure Cosmos DB do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="fb5c3-163">Como toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="fb5c3-164">Amostra de leitor de Hub de Eventos do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="fb5c3-165">Como tooread de Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="fb5c3-166">Amostra do gravador de Hub de Eventos do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="fb5c3-167">Como toowrite tooAzure Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="fb5c3-168">Amostra de leitor HBase do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="fb5c3-169">Como clusters de tooread do HBase em HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="fb5c3-170">Amostra de gravador HBase do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="fb5c3-171">Como clusters de tooHBase toowrite no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="fb5c3-172">Amostra híbrida do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="fb5c3-173">Como toouse um componente de Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="fb5c3-174">Amostra do Storm</span><span class="sxs-lookup"><span data-stu-id="fb5c3-174">Storm Sample</span></span> |<span data-ttu-id="fb5c3-175">Uma topologia básica de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="fb5c3-176">Nem todos os modelos funcionarão com o HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="fb5c3-177">Pacotes NuGet usados pelos modelos de saudação podem não ser compatíveis com Mono.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="fb5c3-178">Verificar Olá [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) de documento e usar o hello [.NET portabilidade analisador](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="fb5c3-179">Etapas Olá neste documento, você usa Olá básica Storm aplicativo projeto tipo toocreate uma topologia.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="fb5c3-180">Notas de modelos de HBase</span><span class="sxs-lookup"><span data-stu-id="fb5c3-180">HBase templates notes</span></span>

<span data-ttu-id="fb5c3-181">Olá HBase leitor e modelos de gravador usam Olá API REST do HBase, não Olá HBase API do Java, toocommunicate com um HBase no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="fb5c3-182">Notas de modelos do EventHub</span><span class="sxs-lookup"><span data-stu-id="fb5c3-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb5c3-183">Olá baseados em Java EventHub spout componente incluído com hello modelo EventHub leitor pode não funcionar com Storm no HDInsight versão 3.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="fb5c3-184">Uma versão atualizada deste componente está disponível em [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="fb5c3-185">Para uma topologia de exemplo que usa esse componente e funciona com Storm no HDInsight 3.5, consulte [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="fb5c3-186">Criar uma topologia C#</span><span class="sxs-lookup"><span data-stu-id="fb5c3-186">Create a C# topology</span></span>

1. <span data-ttu-id="fb5c3-187">Abra o Visual Studio, selecione **Arquivo** > **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="fb5c3-188">De saudação **novo projeto** janela, expanda **instalado** > **modelos**e selecione **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="fb5c3-189">Saudação de modelos, selecione lista **profusão de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="fb5c3-190">Na parte inferior de saudação da tela hello, digite **WordCount** como nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Captura de tela da janela Novo Projeto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="fb5c3-192">Depois que você criou o projeto hello, você deve ter Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="fb5c3-193">**Program.CS**: este arquivo define topologia Olá para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="fb5c3-194">Uma topologia padrão consistindo em um spout e um bolt é criada por padrão.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="fb5c3-195">**Spout.cs**: um spout de exemplo que emite números aleatórios.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="fb5c3-196">**Bolt.CS**: um raio de exemplo que mantém uma contagem de números emitidos pelo spout hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="fb5c3-197">Quando você cria o projeto hello, downloads do NuGet hello mais recente [SCP.NET pacote](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="fb5c3-198">Spout de saudação implementar</span><span class="sxs-lookup"><span data-stu-id="fb5c3-198">Implement hello spout</span></span>

1. <span data-ttu-id="fb5c3-199">Abra **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-199">Open **Spout.cs**.</span></span> <span data-ttu-id="fb5c3-200">Spouts são dados tooread usado em uma topologia de uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="fb5c3-201">Olá principais componentes para uma spout são:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="fb5c3-202">**NextTuple**: chamado como uma tempestade quando spout Olá é permitido tooemit novas tuplas.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="fb5c3-203">**ACK** (topologia transacional somente): trata confirmações iniciadas por outros componentes na topologia de saudação de tuplas enviadas do spout hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="fb5c3-204">Confirmar uma tupla avisa spout Olá que ele foi processado com êxito por componentes downstream.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="fb5c3-205">**Falha** (topologia transacional somente): trata tuplas que são falha processamento de outros componentes na topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="fb5c3-206">Implementando um método Fail permite toore-emitir tupla Olá para que possa ser processado novamente.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="fb5c3-207">Substitua o conteúdo de saudação do hello **Spout** classe com hello texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="fb5c3-208">Este spout aleatoriamente emite uma frase em topologia hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="fb5c3-209">Implementar Olá parafusos</span><span class="sxs-lookup"><span data-stu-id="fb5c3-209">Implement hello bolts</span></span>

1. <span data-ttu-id="fb5c3-210">Excluir Olá **Bolt.cs** arquivo de projeto do hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="fb5c3-211">Em **Solution Explorer**, clique com botão direito hello e selecione **adicionar** > **novo item**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="fb5c3-212">Olá, selecione lista **profusão de raio**e digite **Splitter.cs** como nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="fb5c3-213">Repita este toocreate processo chamada de uma segunda brilhante **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="fb5c3-214">**Splitter.cs**: implementa um bolt que divide as frases em palavras individuais e emite um novo fluxo de palavras.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="fb5c3-215">**Counter.CS**: implementa um raio contagens de cada palavra e emite um novo fluxo de palavras e contagem de saudação para cada palavra.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="fb5c3-216">Esses parafusos de leitura e gravação toostreams, mas você também pode usar um raio toocommunicate com fontes, como um banco de dados ou o serviço.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="fb5c3-217">Abra **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="fb5c3-218">Ele tem apenas um método por padrão: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="fb5c3-219">Olá método Execute é chamado quando o raio Olá recebe uma tupla para o processamento.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="fb5c3-220">Aqui, você pode ler e processar tuplas de entradas e emitir tuplas de saída.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="fb5c3-221">Substitua o conteúdo de saudação do hello **divisor** classe com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="fb5c3-222">Abra **Counter.cs**e substitua o conteúdo de classe de saudação com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="fb5c3-223">Definir a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="fb5c3-223">Define hello topology</span></span>

<span data-ttu-id="fb5c3-224">Spouts e parafusos são organizados em um gráfico, que define como os dados de saudação fluem entre os componentes.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="fb5c3-225">Para esta topologia, o gráfico de saudação é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-225">For this topology, hello graph is as follows:</span></span>

![Diagrama de como os componentes são organizados](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="fb5c3-227">Sentenças são emitidas pelos spout hello e são distribuídas tooinstances de raio do divisor de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="fb5c3-228">raio de separador de saudação quebra sentenças Olá em palavras, que são distribuídas toohello raio de contador.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="fb5c3-229">Porque a contagem de palavras é mantida localmente na instância do contador hello, queremos toomake-se de que palavras específicas fluem toohello mesma instância do contador de raio.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="fb5c3-230">Cada instância controla palavras específicas.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="fb5c3-231">Como o raio do divisor Olá mantém sem estado, realmente não importa qual instância do divisor Olá recebe quais sentença.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="fb5c3-232">Abra **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-232">Open **Program.cs**.</span></span> <span data-ttu-id="fb5c3-233">método importante Olá é **GetTopologyBuilder**, que é usado toodefine Olá topologia enviada tooStorm.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="fb5c3-234">Substitua o conteúdo de saudação do **GetTopologyBuilder** com hello topologia de saudação do código tooimplement descrita anteriormente a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="fb5c3-235">Enviar Olá topologia</span><span class="sxs-lookup"><span data-stu-id="fb5c3-235">Submit hello topology</span></span>

1. <span data-ttu-id="fb5c3-236">Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb5c3-237">Se solicitado, insira as credenciais de saudação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="fb5c3-238">Se você tiver mais de uma assinatura, entre toohello que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="fb5c3-239">Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="fb5c3-240">Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="fb5c3-241">Quando a topologia de saudação foi enviada com êxito, Olá **Storm topologias** para cluster Olá deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="fb5c3-242">Selecione Olá **WordCount** topologia de saudação listar tooview informações sobre Olá executando topologia.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb5c3-243">Você também pode exibir **topologias Storm** do **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="fb5c3-244">Expanda **Azure** > **HDInsight**, clique com o botão direito do mouse em cluster do Storm no HDInsight e selecione **Exibir Topologias do Storm**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="fb5c3-245">informações de tooview sobre os componentes de saudação na topologia hello, clique duas vezes no componente Olá no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="fb5c3-246">De saudação **Resumo da topologia** exibir, clique em **Kill** toostop topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb5c3-247">Topologias Storm continuam toorun até que eles são desativados ou Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="fb5c3-248">Topologia transacional</span><span class="sxs-lookup"><span data-stu-id="fb5c3-248">Transactional topology</span></span>

<span data-ttu-id="fb5c3-249">topologia de saudação anterior não é transacional.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="fb5c3-250">componentes de saudação na topologia de saudação não implementam mensagens tooreplaying de funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="fb5c3-251">Para obter um exemplo de uma topologia de transacional, criar um projeto e selecione **profusão de exemplo** como o tipo de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="fb5c3-252">Topologias transacionais implementam Olá toosupport reprodução de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="fb5c3-253">**Cache de metadados**: spout Olá deve armazenar metadados sobre dados Olá emitidos, para que os dados de saudação podem ser recuperados e emitidos novamente se ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="fb5c3-254">Como dados de saudação emitidos pelo exemplo hello são pequenos, dados brutos de saudação para cada tupla são armazenados em um dicionário para reprodução.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="fb5c3-255">**ACK**: cada raio na topologia Olá pode chamar `this.ctx.Ack(tuple)` tooacknowledge que ele processou com êxito uma tupla.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="fb5c3-256">Quando todos os parafusos controladas Olá tupla, Olá `Ack` método spout Olá é invocado.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="fb5c3-257">Olá `Ack` método permite que os dados de tooremove de spout Olá que foi armazenado em cache para reprodução.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="fb5c3-258">**Falha**: cada raio pode chamar `this.ctx.Fail(tuple)` tooindicate que o processamento falhou para uma coleção de itens.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="fb5c3-259">Falha de saudação propaga toohello `Fail` método spout hello, onde pode ser reproduzida Olá tupla usando armazenado em cache de metadados.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="fb5c3-260">**ID de Sequência**: ao emitir uma tupla, uma ID de sequência exclusiva poderá ser especificada.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="fb5c3-261">Esse valor identifica tupla Olá para processamento de reprodução (Ack e falhas).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="fb5c3-262">Por exemplo, Olá spout em Olá **profusão de exemplo** projeto usa a seguinte Olá ao emitir dados:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="fb5c3-263">Esse código emite uma tupla que contém um fluxo de padrão de toohello frase, com valor de ID de sequência de saudação contido em **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="fb5c3-264">Neste exemplo, **lastSeqId** é incrementado para todas as tuplas emitidas.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="fb5c3-265">Conforme demonstrado no hello **profusão de exemplo** do projeto, se um componente é transacional pode ser definido em tempo de execução, com base na configuração.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="fb5c3-266">Topologia híbrida com C# e Java</span><span class="sxs-lookup"><span data-stu-id="fb5c3-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="fb5c3-267">Você também pode usar ferramentas de Data Lake para topologias Visual Studio toocreate híbrida, em que alguns componentes são c# e outros são Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="fb5c3-268">Para um exemplo de topologia híbrida, crie um projeto e selecione **Amostra Híbrida do Storm**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="fb5c3-269">Esse tipo de exemplo demonstra Olá conceitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="fb5c3-270">**Spout Java** e **bolt C#**: definidos em **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="fb5c3-271">Uma versão transacional é definida em **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="fb5c3-272">**Spout C#** e **bolt Java**: definidos em **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="fb5c3-273">Uma versão transacional é definida em **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fb5c3-274">Esta versão também demonstra como toouse Clojure código de um arquivo de texto como um componente de Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="fb5c3-275">topologia de saudação tooswitch que é usada quando o projeto de saudação é enviado, simplesmente mover Olá `[Active(true)]` instrução toohello topologia que toouse, antes de enviá-lo toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5c3-276">Todos os arquivos de Java Olá necessárias são fornecidos como parte deste projeto em Olá **JavaDependency** pasta.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="fb5c3-277">Considere o seguinte hello quando você está criando e enviando uma topologia híbrida:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="fb5c3-278">Você deve usar **JavaComponentConstructor** toocreate uma instância da classe Java para um spout ou um raio de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="fb5c3-279">Você deve usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON os objetos de dados de tooserialize ou de componentes de Java do Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="fb5c3-280">Ao enviar o servidor de toohello Olá topologia, você deve usar o hello **configurações adicionais** Olá de toospecify opção **caminhos de arquivo Java**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="fb5c3-281">caminho de saudação especificado deve ser o diretório de saudação que contém arquivos JAR Olá que contêm classes Java.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="fb5c3-282">Hubs de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="fb5c3-282">Azure Event Hubs</span></span>

<span data-ttu-id="fb5c3-283">A versão SCP.NET 0.9.4.203 introduz uma nova classe e o método especificamente para trabalhar com spout de Hub de eventos da saudação (um spout de Java que lê de Hubs de eventos).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="fb5c3-284">Quando você cria uma topologia que utiliza spout um Hub de eventos, use Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="fb5c3-285">**EventHubSpoutConfig** classe: cria um objeto que contém a configuração de saudação de componente de spout hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="fb5c3-286">**TopologyBuilder.SetEventHubSpout** método: adiciona a topologia de toohello Olá Hub de eventos spout componente.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5c3-287">Você ainda deve usar Olá **CustomizedInteropJSONSerializer** tooserialize dados produzidos por spout hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="fb5c3-288"><a id="configurationmanager"></a>Usar o ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="fb5c3-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="fb5c3-289">Não use **ConfigurationManager** tooretrieve configuração valores de parafuso e spout componentes.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="fb5c3-290">Isso pode causar uma exceção de ponteiro nulo.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="fb5c3-291">Em vez disso, configuração de saudação para seu projeto é passada para topologia de profusão de saudação como um par de chave e valor no contexto de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="fb5c3-292">Cada componente que se baseia em valores de configuração deve recuperá-los do contexto de saudação durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="fb5c3-293">Olá código a seguir demonstra como tooretrieve estes valores:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="fb5c3-294">Se você usar um `Get` método tooreturn uma instância do seu componente, você deve garantir que ele passa dois Olá `Context` e `Dictionary<string, Object>` construtor de toohello de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="fb5c3-295">Olá é um exemplo básico `Get` método corretamente passa esses valores:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="fb5c3-296">Como tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="fb5c3-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="fb5c3-297">As versões recentes do SCP.NET oferecem suporte à atualização de pacote por meio do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="fb5c3-298">Quando uma nova atualização estiver disponível, você receberá uma notificação de atualização.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="fb5c3-299">seleção de toomanually para uma atualização, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="fb5c3-300">Em **Solution Explorer**, clique com botão direito hello e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="fb5c3-301">No Gerenciador de pacotes de saudação, selecione **atualizações**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="fb5c3-302">Se uma atualização estiver disponível, ela será listada.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-302">If an update is available, it is listed.</span></span> <span data-ttu-id="fb5c3-303">Clique em **atualização** para Olá pacote tooinstall-lo.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb5c3-304">Se seu projeto foi criado com uma versão anterior do SCP.NET que não usou o NuGet, você deve executar Olá versão mais recente de tooa de tooupdate de etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="fb5c3-305">Em **Solution Explorer**, clique com botão direito hello e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="fb5c3-306">Usando Olá **pesquisa** campo, pesquisar e, em seguida, adicionar, **Microsoft.SCP.Net.SDK** toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="fb5c3-307">Solucionar problemas comuns com topologias</span><span class="sxs-lookup"><span data-stu-id="fb5c3-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="fb5c3-308">Exceções de ponteiro nulo</span><span class="sxs-lookup"><span data-stu-id="fb5c3-308">Null pointer exceptions</span></span>

<span data-ttu-id="fb5c3-309">Quando você estiver usando uma topologia c# com um cluster HDInsight baseados em Linux, parafuso e spout componentes que usam **ConfigurationManager** tooread definições de configuração em tempo de execução podem retornar exceções de ponteiro nulo.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="fb5c3-310">configuração Olá para seu projeto é passada para a topologia de profusão de saudação como um par de chave e valor no contexto de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="fb5c3-311">Ele pode ser recuperado do objeto de dicionário de saudação que é passado tooyour componentes quando eles são iniciados.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="fb5c3-312">Para obter mais informações, consulte Olá [ConfigurationManager](#configurationmanager) seção deste documento.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="fb5c3-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="fb5c3-313">System.TypeLoadException</span></span>

<span data-ttu-id="fb5c3-314">Quando você estiver usando uma topologia c# com um cluster HDInsight baseados em Linux, você pode encontrar hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="fb5c3-315">Esse erro ocorre quando você usa um binário que não é compatível com a versão de saudação do .NET que oferece suporte a Mono.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="fb5c3-316">Para clusters HDInsight baseados em Linux, verifique se o projeto usa binários compilados para o .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="fb5c3-317">Testar uma topologia localmente</span><span class="sxs-lookup"><span data-stu-id="fb5c3-317">Test a topology locally</span></span>

<span data-ttu-id="fb5c3-318">Embora seja fácil toodeploy um cluster de tooa de topologia, em alguns casos, talvez seja necessário tootest uma topologia localmente.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="fb5c3-319">Use Olá toorun as etapas a seguir e testar a topologia de exemplo hello neste tutorial localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="fb5c3-320">Testes locais funcionam somente para topologias básicas exclusivamente em C#.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="fb5c3-321">Você não pode usar o teste local para topologias híbridas ou topologias que usam vários fluxos.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="fb5c3-322">Em **Solution Explorer**, clique com botão direito hello e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="fb5c3-323">Nas propriedades do projeto hello, alterar Olá **tipo de saída** muito**aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Captura de tela de propriedades do projeto, com Tipo de saída realçado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="fb5c3-325">Lembre-se de saudação toochange **tipo de saída** fazer muito**biblioteca de classes** antes de implantar o cluster de tooa topologia hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="fb5c3-326">Em **Solution Explorer**, clique com botão direito hello e, em seguida, selecione **adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="fb5c3-327">Selecione **classe**e digite **LocalTest.cs** como o nome da classe hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="fb5c3-328">Por fim, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="fb5c3-329">Abra **LocalTest.cs**e adicione o seguinte Olá **usando** instrução na parte superior da saudação:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="fb5c3-330">De código a seguir de saudação de uso como conteúdo de saudação do hello **LocalTest** classe:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="fb5c3-331">Tirar um tooread momento por meio de comentários de código hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="fb5c3-332">Esse código usa **LocalContext** toorun componentes de saudação no ambiente de desenvolvimento hello e persistir TDS Olá entre arquivos de componentes de tootext na unidade local hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="fb5c3-333">Abra **Program.cs**e adicione Olá após toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="fb5c3-334">Salvar alterações de saudação e, em seguida, clique em **F5** ou selecione **depurar** > **iniciar depuração** toostart projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="fb5c3-335">Uma janela do console deve aparecer e registrar o status como progresso de testes de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="fb5c3-336">Quando **testes terminado** for exibida, pressione qualquer janela de saudação tooclose chave.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="fb5c3-337">Use **Windows Explorer** diretório de saudação toolocate que contém seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="fb5c3-338">Por exemplo: **C:\Users\<seu_nome_de_usuário>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="fb5c3-339">Nesse diretório, abra **Bin** e clique em **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="fb5c3-340">Você deve ver os arquivos de texto de saudação que foram produzidos quando Olá testes executados: sentences.txt, counter.txt e splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="fb5c3-341">Abra cada arquivo de texto e inspecionar dados hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb5c3-342">Os dados da cadeia de caracteres persistem como uma matriz de valores decimais nesses arquivos.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="fb5c3-343">Por exemplo, \[[97,103,111]] em Olá **splitter.txt** arquivo é palavra hello *e*.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5c3-344">Ser Olá-se de tooset **tipo de projeto** fazer muito**biblioteca de classes** antes de implantar tooa Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="fb5c3-345">Registrando informações no log</span><span class="sxs-lookup"><span data-stu-id="fb5c3-345">Log information</span></span>

<span data-ttu-id="fb5c3-346">É possível registrar em log com facilidade informações de seus componentes de topologia usando o `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="fb5c3-347">Por exemplo, o seguinte Olá cria uma entrada de log informativa:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="fb5c3-348">Informações registradas podem ser exibidas de saudação **Log do serviço de Hadoop**, que se encontra no **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="fb5c3-349">Expanda a entrada de saudação para seu Storm no cluster HDInsight e, em seguida, expanda **Log do serviço de Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="fb5c3-350">Por fim, selecione Olá tooview de arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5c3-351">Olá logs são armazenados no hello conta de armazenamento do Azure que é usada pelo cluster.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="fb5c3-352">logs de saudação tooview no Visual Studio, você deve entrar no toohello assinatura do Azure que possui a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="fb5c3-353">Exibir informações de erro</span><span class="sxs-lookup"><span data-stu-id="fb5c3-353">View error information</span></span>

<span data-ttu-id="fb5c3-354">tooview erros que ocorreram em uma topologia em execução, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="fb5c3-355">De **Server Explorer**, Olá Storm no cluster HDInsight e selecione **topologias profusão de exibição**.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="fb5c3-356">Para Olá **Spout** e **Bolts**, Olá **último erro** coluna contém informações sobre o último erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="fb5c3-357">Selecione Olá **Spout Id** ou **raio Id** para o componente de saudação que tem um erro listado.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="fb5c3-358">Na página de detalhes de saudação que é exibido, adicional erro informações estão listadas no hello **erros** seção final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="fb5c3-359">tooobtain obter mais informações, selecionadas um **porta** de saudação **executores** seção da página hello, toosee Olá Storm trabalho log Olá últimos minutos.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="fb5c3-360">Erros durante o envio de topologias</span><span class="sxs-lookup"><span data-stu-id="fb5c3-360">Errors submitting topologies</span></span>

<span data-ttu-id="fb5c3-361">Se você encontrar erros ao enviar uma topologia tooHDInsight, você pode encontrar registros para componentes do servidor de saudação que manipulam o envio de topologia no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="fb5c3-362">tooretrieve esses logs, use Olá comando a seguir em uma linha de comando:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="fb5c3-363">Substituir __sshuser__ com hello SSH a conta de usuário para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="fb5c3-364">Substituir __clustername__ com o nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="fb5c3-365">Para saber mais sobre como usar o `scp` e o `ssh` com o HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="fb5c3-366">Envios podem falhar por vários motivos:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="fb5c3-367">JDK não está instalado ou não está no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="fb5c3-368">Dependências de Java necessárias não são incluídas no envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="fb5c3-369">Dependências incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="fb5c3-370">Nomes de topologia duplicados.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-370">Duplicate topology names.</span></span>

<span data-ttu-id="fb5c3-371">Se hello `hdinsight-scpwebapi.out` log contém um `FileNotFoundException`, isso pode ser causado por Olá condições a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="fb5c3-372">Olá JDK não está no caminho de saudação no ambiente de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="fb5c3-373">Verifique se esse Olá JDK está instalado no ambiente de desenvolvimento hello e que `%JAVA_HOME%/bin` está no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="fb5c3-374">Uma dependência de Java está ausente.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-374">You are missing a Java dependency.</span></span> <span data-ttu-id="fb5c3-375">Verifique se que você está incluindo todos os arquivos JAR necessários como parte do envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb5c3-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb5c3-376">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb5c3-376">Next steps</span></span>

<span data-ttu-id="fb5c3-377">Para obter um exemplo de processamento de dados de Hubs de eventos, consulte [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="fb5c3-378">Para obter um exemplo de uma topologia de C# que divide os dados de fluxo em vários fluxos, consulte [Exemplo de Storm C#](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="fb5c3-379">toodiscover obter mais informações sobre como criar c# topologias, consulte [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="fb5c3-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="fb5c3-380">Para mais toowork maneiras com HDInsight e mais Storm em amostras de HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb5c3-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="fb5c3-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="fb5c3-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="fb5c3-382">Guia de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="fb5c3-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="fb5c3-383">**Apache Storm no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="fb5c3-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="fb5c3-384">Implantar e monitorar topologias com o Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="fb5c3-385">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="fb5c3-386">**Apache Hadoop no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="fb5c3-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="fb5c3-387">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fb5c3-388">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fb5c3-389">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="fb5c3-390">**Apache HBase no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="fb5c3-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="fb5c3-391">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb5c3-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
