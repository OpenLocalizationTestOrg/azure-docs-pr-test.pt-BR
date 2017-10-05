---
title: "Topologias Apache Storm com Visual Studio e C# – Azure HDInsight | Microsoft Docs"
description: Aprenda como criar topologias Storm em C#. Crie uma topologia de contagem de palavras simples no Visual Studio usando as ferramentas do Hadoop para Visual Studio.
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="f6394-104">Desenvolver topologias C# para Apache Storm usando ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6394-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="f6394-105">Saiba como criar uma topologia Storm C# usando as ferramentas do Azure Data Lake (Hadoop) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6394-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="f6394-106">Este documento orienta o processo de criar um projeto do Storm no Visual Studio, testá-lo localmente e implantá-lo em um Apache Storm no cluster do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="f6394-107">Você também aprende a criar topologias híbridas que usam componentes C# e Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="f6394-108">Embora as etapas neste documento dependam de um ambiente de desenvolvimento do Windows com Visual Studio, o projeto compilado pode ser enviado a um cluster HDInsight baseado em Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="f6394-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="f6394-109">Somente os clusters baseados em Linux criados depois de 28 de outubro de 2016 são compatíveis com as topologias do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="f6394-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="f6394-110">Para usar uma topologia do C# com um cluster baseado em Linux, você deverá atualizar o pacote NuGet Microsoft.SCP.Net.SDK usado pelo seu projeto para a versão 0.10.0.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f6394-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="f6394-111">A versão do pacote também deve coincidir com a versão principal do Storm instalada no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="f6394-112">Versão do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-112">HDInsight version</span></span> | <span data-ttu-id="f6394-113">Versão do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-113">Storm version</span></span> | <span data-ttu-id="f6394-114">Versão do SCP.NET</span><span class="sxs-lookup"><span data-stu-id="f6394-114">SCP.NET version</span></span> | <span data-ttu-id="f6394-115">Versão Mono padrão</span><span class="sxs-lookup"><span data-stu-id="f6394-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="f6394-116">3.3</span><span class="sxs-lookup"><span data-stu-id="f6394-116">3.3</span></span> |<span data-ttu-id="f6394-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="f6394-117">0.10.x</span></span> |<span data-ttu-id="f6394-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="f6394-118">0.10.x.x</span></span></br><span data-ttu-id="f6394-119">(somente em HDInsight baseado no Windows)</span><span class="sxs-lookup"><span data-stu-id="f6394-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="f6394-120">ND</span><span class="sxs-lookup"><span data-stu-id="f6394-120">NA</span></span> |
| <span data-ttu-id="f6394-121">3.4</span><span class="sxs-lookup"><span data-stu-id="f6394-121">3.4</span></span> | <span data-ttu-id="f6394-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="f6394-122">0.10.0.x</span></span> | <span data-ttu-id="f6394-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="f6394-123">0.10.0.x</span></span> | <span data-ttu-id="f6394-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="f6394-124">3.2.8</span></span> |
| <span data-ttu-id="f6394-125">3,5</span><span class="sxs-lookup"><span data-stu-id="f6394-125">3.5</span></span> | <span data-ttu-id="f6394-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="f6394-126">1.0.2.x</span></span> | <span data-ttu-id="f6394-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="f6394-127">1.0.0.x</span></span> | <span data-ttu-id="f6394-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="f6394-128">4.2.1</span></span> |
| <span data-ttu-id="f6394-129">3.6</span><span class="sxs-lookup"><span data-stu-id="f6394-129">3.6</span></span> | <span data-ttu-id="f6394-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="f6394-130">1.1.0.x</span></span> | <span data-ttu-id="f6394-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="f6394-131">1.0.0.x</span></span> | <span data-ttu-id="f6394-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="f6394-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f6394-133">As topologias C# em clusters baseados em Linux devem usar o .NET 4.5 e o Mono para execução no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="f6394-134">Verificar [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para possíveis incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="f6394-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="f6394-135">Instalar Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6394-135">Install Visual Studio</span></span>

<span data-ttu-id="f6394-136">Você pode desenvolver topologias C# com SCP.NET, usando uma das seguintes versões do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f6394-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="f6394-137">Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="f6394-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="f6394-138">Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="f6394-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="f6394-139">Visual Studio 2015 ou [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="f6394-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="f6394-140">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="f6394-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="f6394-141">Instalar ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6394-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="f6394-142">Para instalar as ferramentas do Data Lake para Visual Studio, siga as etapas em [Introdução ao uso das ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f6394-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="f6394-143">Instalar o Java</span><span class="sxs-lookup"><span data-stu-id="f6394-143">Install Java</span></span>

<span data-ttu-id="f6394-144">Quando você envia uma topologia Storm do Visual Studio, o SCP.NET gera um arquivo zip que contém a topologia e as respectivas dependências.</span><span class="sxs-lookup"><span data-stu-id="f6394-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="f6394-145">O Java é usado para criar esses arquivos zip porque ele usa um formato que é mais compatível com clusters baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="f6394-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="f6394-146">Instale o JDK (Java Developer Kit) 7 ou posterior em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f6394-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="f6394-147">Você pode obter o Oracle JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="f6394-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="f6394-148">Você também pode usar [outras distribuições do Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="f6394-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="f6394-149">A variável de ambiente `JAVA_HOME` deve apontar para o diretório que contém o Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="f6394-150">A variável de ambiente `PATH` deve incluir o diretório `%JAVA_HOME%\bin`.</span><span class="sxs-lookup"><span data-stu-id="f6394-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="f6394-151">Você pode usar o seguinte aplicativo de console C# para verificar se Java e JDK estão instalados corretamente:</span><span class="sxs-lookup"><span data-stu-id="f6394-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="f6394-152">Modelos do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-152">Storm templates</span></span>

<span data-ttu-id="f6394-153">As ferramentas do Data Lake para o Visual Studio fornecem os seguintes modelos:</span><span class="sxs-lookup"><span data-stu-id="f6394-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="f6394-154">Tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="f6394-154">Project type</span></span> | <span data-ttu-id="f6394-155">Demonstra</span><span class="sxs-lookup"><span data-stu-id="f6394-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="f6394-156">Aplicativo Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-156">Storm Application</span></span> |<span data-ttu-id="f6394-157">Um projeto de topologia Storm vazio.</span><span class="sxs-lookup"><span data-stu-id="f6394-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="f6394-158">Amostra de gravador do SQL Azure Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="f6394-159">Como gravar em um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6394-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="f6394-160">Amostra de leitor do Azure Cosmos DB do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="f6394-161">Como ler do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f6394-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="f6394-162">Amostra do gravador do Azure Cosmos DB do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="f6394-163">Como gravar no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f6394-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="f6394-164">Amostra de leitor de Hub de Eventos do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="f6394-165">Como ler dos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6394-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="f6394-166">Amostra do gravador de Hub de Eventos do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="f6394-167">Como gravar nos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6394-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="f6394-168">Amostra de leitor HBase do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="f6394-169">Como ler do HBase em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="f6394-170">Amostra de gravador HBase do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="f6394-171">Como gravar no HBase em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="f6394-172">Amostra híbrida do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="f6394-173">Como usar um componente Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-173">How to use a Java component.</span></span> |
| <span data-ttu-id="f6394-174">Amostra do Storm</span><span class="sxs-lookup"><span data-stu-id="f6394-174">Storm Sample</span></span> |<span data-ttu-id="f6394-175">Uma topologia básica de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="f6394-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="f6394-176">Nem todos os modelos funcionarão com o HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="f6394-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="f6394-177">Pacotes NuGet usados pelos modelos podem não ser compatíveis com o Mono.</span><span class="sxs-lookup"><span data-stu-id="f6394-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="f6394-178">Verifique o documento [Compatibilidade com o Mono](http://www.mono-project.com/docs/about-mono/compatibility/) e use o [Analisador de Portabilidade do .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) para identificar problemas em potencial.</span><span class="sxs-lookup"><span data-stu-id="f6394-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="f6394-179">Nas etapas neste documento, você usará o tipo de projeto de aplicativo Storm básico para criar uma topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="f6394-180">Notas de modelos de HBase</span><span class="sxs-lookup"><span data-stu-id="f6394-180">HBase templates notes</span></span>

<span data-ttu-id="f6394-181">Para se comunicar com um HBase no cluster HDInsight, os modelos de leitor e gravador do HBase não usam a API Java do HBase, mas sim a API REST do HBase.</span><span class="sxs-lookup"><span data-stu-id="f6394-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="f6394-182">Notas de modelos do EventHub</span><span class="sxs-lookup"><span data-stu-id="f6394-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6394-183">O componente spout do EventHub baseado em Java incluído com o modelo de Leitor do EventHub pode não funcionar com o Storm no HDInsight versão 3.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f6394-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="f6394-184">Uma versão atualizada deste componente está disponível em [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="f6394-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="f6394-185">Para uma topologia de exemplo que usa esse componente e funciona com Storm no HDInsight 3.5, consulte [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="f6394-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="f6394-186">Criar uma topologia C#</span><span class="sxs-lookup"><span data-stu-id="f6394-186">Create a C# topology</span></span>

1. <span data-ttu-id="f6394-187">Abra o Visual Studio, selecione **Arquivo** > **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f6394-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="f6394-188">Na janela **Novo Projeto**, expanda **Instalados** > **Modelos** e selecione **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="f6394-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="f6394-189">Na lista de modelos, selecione **Aplicativo Storm**.</span><span class="sxs-lookup"><span data-stu-id="f6394-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="f6394-190">Na parte inferior da tela, insira **WordCount** como o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6394-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Captura de tela da janela Novo Projeto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="f6394-192">Após você criar o projeto, você deverá ter os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="f6394-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="f6394-193">**Program.cs**: esse arquivo define a topologia para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="f6394-194">Uma topologia padrão consistindo em um spout e um bolt é criada por padrão.</span><span class="sxs-lookup"><span data-stu-id="f6394-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="f6394-195">**Spout.cs**: um spout de exemplo que emite números aleatórios.</span><span class="sxs-lookup"><span data-stu-id="f6394-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="f6394-196">**Bolt.cs**: um bolt de exemplo que mantém uma contagem de números emitidos pelo spout.</span><span class="sxs-lookup"><span data-stu-id="f6394-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="f6394-197">Quando você cria o projeto, o NuGet baixa a versão mais recente do [pacote SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="f6394-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="f6394-198">Implementar o spout</span><span class="sxs-lookup"><span data-stu-id="f6394-198">Implement the spout</span></span>

1. <span data-ttu-id="f6394-199">Abra **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="f6394-199">Open **Spout.cs**.</span></span> <span data-ttu-id="f6394-200">Os spouts são usados para ler os dados em uma topologia de uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="f6394-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="f6394-201">Os principais componentes de um spout são:</span><span class="sxs-lookup"><span data-stu-id="f6394-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="f6394-202">**NextTuple**: chamado pelo Storm quando o spout pode emitir novas tuplas.</span><span class="sxs-lookup"><span data-stu-id="f6394-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="f6394-203">**Ack** (apenas topologia transacional): lida com confirmações iniciadas por outros componentes na topologia, para cadeias de identificação enviadas do spout.</span><span class="sxs-lookup"><span data-stu-id="f6394-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="f6394-204">Confirmar uma tupla informa ao spout que ele foi processado com êxito por componentes downstream.</span><span class="sxs-lookup"><span data-stu-id="f6394-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="f6394-205">**Falha** : (apenas topologia transacional) - lida com tuplas que falham ao processar outros componentes na topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="f6394-206">A implementação um método Fail permite emitir novamente a tupla para que ela possa ser processada novamente.</span><span class="sxs-lookup"><span data-stu-id="f6394-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="f6394-207">Substitua o conteúdo da classe **Spout** pelo texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6394-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="f6394-208">Esse spout emite uma frase para a topologia aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="f6394-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="f6394-209">Implementar os bolts</span><span class="sxs-lookup"><span data-stu-id="f6394-209">Implement the bolts</span></span>

1. <span data-ttu-id="f6394-210">Exclua o arquivo **Bolt.cs** existente do projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="f6394-211">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Adicionar** > **Novo item**.</span><span class="sxs-lookup"><span data-stu-id="f6394-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="f6394-212">Na lista, selecione **Storm Bolt** e digite **Splitter.cs** como o nome.</span><span class="sxs-lookup"><span data-stu-id="f6394-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="f6394-213">Repita esse processo para criar um segundo bolt chamado **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="f6394-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="f6394-214">**Splitter.cs**: implementa um bolt que divide as frases em palavras individuais e emite um novo fluxo de palavras.</span><span class="sxs-lookup"><span data-stu-id="f6394-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="f6394-215">**Counter.cs**: implementa um bolt que conta cada palavra e emite um novo fluxo de palavras e a contagem de cada palavra.</span><span class="sxs-lookup"><span data-stu-id="f6394-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f6394-216">Esses bolts leem e gravam em fluxos, mas você também pode usar um bolt para se comunicar com um banco de dados ou serviço.</span><span class="sxs-lookup"><span data-stu-id="f6394-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="f6394-217">Abra **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="f6394-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="f6394-218">Ele tem apenas um método por padrão: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="f6394-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="f6394-219">O método Execute é chamado quando o bolt recebe uma tupla para processamento.</span><span class="sxs-lookup"><span data-stu-id="f6394-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="f6394-220">Aqui, você pode ler e processar tuplas de entradas e emitir tuplas de saída.</span><span class="sxs-lookup"><span data-stu-id="f6394-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="f6394-221">Substitua o conteúdo da classe **Splitter** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f6394-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="f6394-222">Abra **Counter.cs** e substitua o conteúdo da classe pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="f6394-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="f6394-223">Definir a topologia</span><span class="sxs-lookup"><span data-stu-id="f6394-223">Define the topology</span></span>

<span data-ttu-id="f6394-224">Spouts e bolts são organizados em um gráfico, que define como os dados fluem entre componentes.</span><span class="sxs-lookup"><span data-stu-id="f6394-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="f6394-225">Para essa topologia, o gráfico é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f6394-225">For this topology, the graph is as follows:</span></span>

![Diagrama de como os componentes são organizados](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="f6394-227">As frases são emitidas do spout e são distribuídas para instâncias do bolt Splitter.</span><span class="sxs-lookup"><span data-stu-id="f6394-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="f6394-228">O bolt Splitter divide as frases em palavras, que são distribuídas para o bolt Contador.</span><span class="sxs-lookup"><span data-stu-id="f6394-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="f6394-229">Como a contagem de palavras é mantida localmente na instância Contador, queremos nos certificar de que palavras específicas sejam transmitidas para a mesma instância do bolt Contador.</span><span class="sxs-lookup"><span data-stu-id="f6394-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="f6394-230">Cada instância controla palavras específicas.</span><span class="sxs-lookup"><span data-stu-id="f6394-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="f6394-231">Uma vez que o bolt Splitter não mantém nenhum estado, não importa qual instância do Splitter recebe qual frase.</span><span class="sxs-lookup"><span data-stu-id="f6394-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="f6394-232">Abra **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f6394-232">Open **Program.cs**.</span></span> <span data-ttu-id="f6394-233">O método importante é **GetTopologyBuilder**, que é usado para definir a topologia enviada ao Storm.</span><span class="sxs-lookup"><span data-stu-id="f6394-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="f6394-234">Substitua o conteúdo de **GetTopologyBuilder** pelo seguinte código para implementar a topologia descrita anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f6394-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="f6394-235">Enviar a topologia</span><span class="sxs-lookup"><span data-stu-id="f6394-235">Submit the topology</span></span>

1. <span data-ttu-id="f6394-236">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Enviar para o Storm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f6394-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6394-237">Se solicitado, insira as credenciais de logon para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6394-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="f6394-238">Se você tiver mais de uma assinatura, entre naquela que contém seu cluster Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="f6394-239">Selecione seu Storm no cluster HDInsight no menu suspenso **Cluster Storm** e selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="f6394-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="f6394-240">Você pode monitorar se o envio obteve êxito ou não usando a janela **Saída** .</span><span class="sxs-lookup"><span data-stu-id="f6394-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="f6394-241">Depois que a topologia tiver sido enviada com êxito, as **Topologias Storm** para o cluster deverão aparecer.</span><span class="sxs-lookup"><span data-stu-id="f6394-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="f6394-242">Selecione a topologia **WordCount** na lista para exibir informações sobre a topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="f6394-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6394-243">Você também pode exibir **topologias Storm** do **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="f6394-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="f6394-244">Expanda **Azure** > **HDInsight**, clique com o botão direito do mouse em cluster do Storm no HDInsight e selecione **Exibir Topologias do Storm**.</span><span class="sxs-lookup"><span data-stu-id="f6394-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="f6394-245">Para exibir informações sobre os componentes na topologia, clique duas vezes no componente no diagrama.</span><span class="sxs-lookup"><span data-stu-id="f6394-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="f6394-246">Na exibição **Resumo da Topologia**, selecione **Eliminar** para parar a topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6394-247">As topologias Storm continuarão em execução até serem paradas ou até que o cluster seja excluído.</span><span class="sxs-lookup"><span data-stu-id="f6394-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="f6394-248">Topologia transacional</span><span class="sxs-lookup"><span data-stu-id="f6394-248">Transactional topology</span></span>

<span data-ttu-id="f6394-249">A topologia anterior não é transacional.</span><span class="sxs-lookup"><span data-stu-id="f6394-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="f6394-250">Os componentes na topologia não implementam a funcionalidade para reproduzir as mensagens.</span><span class="sxs-lookup"><span data-stu-id="f6394-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="f6394-251">Para um exemplo de uma topologia transacional, crie um projeto e selecione **Amostra do Storm** como o tipo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="f6394-252">As topologias transacionais implementam o seguinte para suportar a reprodução de dados:</span><span class="sxs-lookup"><span data-stu-id="f6394-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="f6394-253">**Cache de metadados**: o spout deve armazenar metadados sobre os dados emitidos para que os dados possam ser recuperados e emitidos novamente caso ocorra uma falha.</span><span class="sxs-lookup"><span data-stu-id="f6394-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="f6394-254">Como os dados emitidos pela amostra são pequenos, os dados brutos de cada tupla são armazenados em um dicionário para reprodução.</span><span class="sxs-lookup"><span data-stu-id="f6394-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="f6394-255">**Ack**: cada bolt na topologia pode chamar `this.ctx.Ack(tuple)` para confirmar que processou uma tupla com êxito.</span><span class="sxs-lookup"><span data-stu-id="f6394-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="f6394-256">Quando todos os bolts confirmarem a tupla, o método `Ack` do spout será chamado.</span><span class="sxs-lookup"><span data-stu-id="f6394-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="f6394-257">O método `Ack` permite que o spout remova os dados armazenados em cache para reprodução.</span><span class="sxs-lookup"><span data-stu-id="f6394-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="f6394-258">**Falha**: cada bolt pode chamar `this.ctx.Fail(tuple)` para indicar que o processamento falhou para uma tupla.</span><span class="sxs-lookup"><span data-stu-id="f6394-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="f6394-259">A falha é propagada para o método `Fail` do spout, onde a tupla pode ser reproduzida usando os metadados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="f6394-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="f6394-260">**ID de Sequência**: ao emitir uma tupla, uma ID de sequência exclusiva poderá ser especificada.</span><span class="sxs-lookup"><span data-stu-id="f6394-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="f6394-261">Esse valor identifica a tupla para o processamento da reprodução (Confirmação e Falha).</span><span class="sxs-lookup"><span data-stu-id="f6394-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="f6394-262">Por exemplo, o spout do projeto **Amostra do Storm** usa o seguinte ao emitir dados:</span><span class="sxs-lookup"><span data-stu-id="f6394-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="f6394-263">Esse código emite uma tupla que contém uma frase para o fluxo padrão com o valor da ID de sequência contido em **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="f6394-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="f6394-264">Neste exemplo, **lastSeqId** é incrementado para todas as tuplas emitidas.</span><span class="sxs-lookup"><span data-stu-id="f6394-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="f6394-265">Conforme demonstrado no projeto **Amostra do Storm**, se um componente for transacional, ele poderá ser definido no tempo de execução com base na configuração.</span><span class="sxs-lookup"><span data-stu-id="f6394-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="f6394-266">Topologia híbrida com C# e Java</span><span class="sxs-lookup"><span data-stu-id="f6394-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="f6394-267">Você também pode usar as ferramentas do Data Lake para Visual Studio para criar topologias híbridas, em que alguns componentes são C# e outros são Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="f6394-268">Para um exemplo de topologia híbrida, crie um projeto e selecione **Amostra Híbrida do Storm**.</span><span class="sxs-lookup"><span data-stu-id="f6394-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="f6394-269">Esse tipo de exemplo demonstra os seguintes conceitos:</span><span class="sxs-lookup"><span data-stu-id="f6394-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="f6394-270">**Spout Java** e **bolt C#**: definidos em **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="f6394-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="f6394-271">Uma versão transacional é definida em **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="f6394-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="f6394-272">**Spout C#** e **bolt Java**: definidos em **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="f6394-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="f6394-273">Uma versão transacional é definida em **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="f6394-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f6394-274">Essa versão também demonstra como usar o código Clojure de um arquivo de texto como um componente Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="f6394-275">Para mudar a topologia que é usada quando o projeto é enviado, basta mover a instrução `[Active(true)]` para a topologia que você deseja usar antes de enviá-la para o cluster.</span><span class="sxs-lookup"><span data-stu-id="f6394-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f6394-276">Todos os arquivos Java necessários são fornecidos como parte desse projeto na pasta **JavaDependency** .</span><span class="sxs-lookup"><span data-stu-id="f6394-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="f6394-277">Considere o seguinte ao criar e enviar uma topologia híbrida:</span><span class="sxs-lookup"><span data-stu-id="f6394-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="f6394-278">Você deve usar **JavaComponentConstructor** para criar uma instância da classe Java para um spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="f6394-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="f6394-279">Você deve usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** para serializar dados de entrada ou saída de componentes Java desde objetos Java até o JSON.</span><span class="sxs-lookup"><span data-stu-id="f6394-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="f6394-280">Ao enviar a topologia para o servidor, você deve usar a opção **Configurações adicionais** para especificar **Caminhos de arquivo Java**.</span><span class="sxs-lookup"><span data-stu-id="f6394-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="f6394-281">O caminho especificado deve ser o diretório que contém os arquivos JAR com suas classes Java.</span><span class="sxs-lookup"><span data-stu-id="f6394-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="f6394-282">Hubs de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="f6394-282">Azure Event Hubs</span></span>

<span data-ttu-id="f6394-283">A versão 0.9.4.203 do SCP.NET introduz uma classe e um método novos especificamente para trabalhar com o spout do Hub de Eventos (um spout Java que lê de Hubs de Eventos).</span><span class="sxs-lookup"><span data-stu-id="f6394-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="f6394-284">Ao criar uma topologia que usa um spout de Hub de Eventos, use os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="f6394-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="f6394-285">Classe **EventHubSpoutConfig**: cria um objeto que contém a configuração do componente spout.</span><span class="sxs-lookup"><span data-stu-id="f6394-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="f6394-286">Método **TopologyBuilder.SetEventHubSpout**: adiciona o componente Spout do Hub de Eventos à topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="f6394-287">Você ainda deve usar o **CustomizedInteropJSONSerializer** para serializar os dados produzidos pelo spout.</span><span class="sxs-lookup"><span data-stu-id="f6394-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="f6394-288"><a id="configurationmanager"></a>Usar o ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f6394-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="f6394-289">Não use o **ConfigurationManager** para recuperar valores de configuração dos componentes bolt e spout.</span><span class="sxs-lookup"><span data-stu-id="f6394-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="f6394-290">Isso pode causar uma exceção de ponteiro nulo.</span><span class="sxs-lookup"><span data-stu-id="f6394-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="f6394-291">Em vez disso, a configuração do seu projeto é passada para a topologia Storm como um par de chave/valor no contexto da topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="f6394-292">Cada componente que se baseia em valores de configuração deve recuperá-los no contexto durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="f6394-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="f6394-293">O seguinte código demonstra como recuperar esses valores:</span><span class="sxs-lookup"><span data-stu-id="f6394-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="f6394-294">Se você usar um método `Get` para retornar uma instância do seu componente, será preciso garantir que ele passe os parâmetros `Context` e `Dictionary<string, Object>` ao construtor.</span><span class="sxs-lookup"><span data-stu-id="f6394-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="f6394-295">O seguinte exemplo é um método `Get` básico que passa corretamente esses valores:</span><span class="sxs-lookup"><span data-stu-id="f6394-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="f6394-296">Como atualizar o SCP.NET</span><span class="sxs-lookup"><span data-stu-id="f6394-296">How to update SCP.NET</span></span>

<span data-ttu-id="f6394-297">As versões recentes do SCP.NET oferecem suporte à atualização de pacote por meio do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6394-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="f6394-298">Quando uma nova atualização estiver disponível, você receberá uma notificação de atualização.</span><span class="sxs-lookup"><span data-stu-id="f6394-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="f6394-299">Para verificar manualmente se há uma atualização, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f6394-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="f6394-300">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f6394-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="f6394-301">No Gerenciador de pacotes, selecione **Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="f6394-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="f6394-302">Se uma atualização estiver disponível, ela será listada.</span><span class="sxs-lookup"><span data-stu-id="f6394-302">If an update is available, it is listed.</span></span> <span data-ttu-id="f6394-303">Clique em **Atualização** referente ao pacote para instalá-la.</span><span class="sxs-lookup"><span data-stu-id="f6394-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6394-304">Se o seu projeto foi criado com uma versão anterior do SCP.NET que não usou o NuGet, você deverá executar as seguintes etapas para atualizar para uma versão mais recente:</span><span class="sxs-lookup"><span data-stu-id="f6394-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="f6394-305">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f6394-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="f6394-306">Usando o campo **Pesquisa**, faça a pesquisa e adicione **Microsoft.SCP.Net.SDK** ao projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="f6394-307">Solucionar problemas comuns com topologias</span><span class="sxs-lookup"><span data-stu-id="f6394-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="f6394-308">Exceções de ponteiro nulo</span><span class="sxs-lookup"><span data-stu-id="f6394-308">Null pointer exceptions</span></span>

<span data-ttu-id="f6394-309">Ao usar uma topologia C# com um cluster HDInsight baseado em Linux, os componentes bolt e spout que usam o **ConfigurationManager** para ler configurações em tempo de execução podem retornar exceções de ponteiro nulo.</span><span class="sxs-lookup"><span data-stu-id="f6394-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="f6394-310">A configuração do seu projeto é passada para a topologia Storm como um par de chave/valor no contexto da topologia.</span><span class="sxs-lookup"><span data-stu-id="f6394-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="f6394-311">Ele pode ser recuperado do objeto de dicionário que é passado para os seus componentes quando eles são inicializados.</span><span class="sxs-lookup"><span data-stu-id="f6394-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="f6394-312">Para obter mais informações, consulte a seção [ConfigurationManager](#configurationmanager) deste documento.</span><span class="sxs-lookup"><span data-stu-id="f6394-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="f6394-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="f6394-313">System.TypeLoadException</span></span>

<span data-ttu-id="f6394-314">Ao usar uma topologia C# com um cluster HDInsight baseado em Linux, você pode encontrar o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="f6394-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="f6394-315">Esse erro geralmente ocorre quando você usa um binário que não é compatível com a versão do .NET à qual o Mono dá suporte.</span><span class="sxs-lookup"><span data-stu-id="f6394-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="f6394-316">Para clusters HDInsight baseados em Linux, verifique se o projeto usa binários compilados para o .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="f6394-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="f6394-317">Testar uma topologia localmente</span><span class="sxs-lookup"><span data-stu-id="f6394-317">Test a topology locally</span></span>

<span data-ttu-id="f6394-318">Embora seja fácil implantar uma topologia em um cluster, em alguns casos poderá ser necessário testar uma topologia localmente.</span><span class="sxs-lookup"><span data-stu-id="f6394-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="f6394-319">Use as seguintes etapas para executar e testar a topologia de exemplo nesse tutorial localmente em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f6394-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="f6394-320">Testes locais funcionam somente para topologias básicas exclusivamente em C#.</span><span class="sxs-lookup"><span data-stu-id="f6394-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="f6394-321">Você não pode usar o teste local para topologias híbridas ou topologias que usam vários fluxos.</span><span class="sxs-lookup"><span data-stu-id="f6394-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="f6394-322">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6394-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="f6394-323">Nas propriedades do projeto, altere **Tipo de saída** para **Aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="f6394-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Captura de tela de propriedades do projeto, com Tipo de saída realçado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="f6394-325">Lembre-se de alterar o **Tipo de saída** de volta para **Biblioteca de Classes** antes de implantar a topologia em um cluster.</span><span class="sxs-lookup"><span data-stu-id="f6394-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="f6394-326">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f6394-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="f6394-327">Selecione **Classe** e insira **LocalTest.cs** como o nome de classe.</span><span class="sxs-lookup"><span data-stu-id="f6394-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="f6394-328">Por fim, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6394-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="f6394-329">Abra **LocalTest.cs** e adicione a seguinte instrução **using** na parte superior:</span><span class="sxs-lookup"><span data-stu-id="f6394-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="f6394-330">Use o seguinte código como o conteúdo da classe **LocalTest**:</span><span class="sxs-lookup"><span data-stu-id="f6394-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="f6394-331">Tome um momento para ler os comentários do código.</span><span class="sxs-lookup"><span data-stu-id="f6394-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="f6394-332">Esse código usa **LocalContext** para executar os componentes no ambiente de desenvolvimento, persistindo o fluxo de dados entre componentes para arquivos de texto na unidade local.</span><span class="sxs-lookup"><span data-stu-id="f6394-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="f6394-333">Abra **Program.cs** e adicione o seguinte ao método **Main**:</span><span class="sxs-lookup"><span data-stu-id="f6394-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="f6394-334">Salve as alterações e use **F5** ou selecione **Depurar** > **Iniciar Depuração** para iniciar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="f6394-335">Uma janela de console deve aparecer e o status do log colocado como progresso dos testes.</span><span class="sxs-lookup"><span data-stu-id="f6394-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="f6394-336">Quando **Testes concluídos** aparecer, pressione qualquer tecla para fechar a janela.</span><span class="sxs-lookup"><span data-stu-id="f6394-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="f6394-337">Use **Windows Explorer** para localizar o diretório que contém seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f6394-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="f6394-338">Por exemplo: **C:\Users\<seu_nome_de_usuário>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="f6394-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="f6394-339">Nesse diretório, abra **Bin** e clique em **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="f6394-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="f6394-340">Você deve ver os arquivos de texto produzidos após a execução dos testes: sentences.txt, counter.txt e splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="f6394-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="f6394-341">Abra cada arquivo de texto e inspecione os dados.</span><span class="sxs-lookup"><span data-stu-id="f6394-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6394-342">Os dados da cadeia de caracteres persistem como uma matriz de valores decimais nesses arquivos.</span><span class="sxs-lookup"><span data-stu-id="f6394-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="f6394-343">Por exemplo, \[[97,103,111]] no arquivo **splitter.txt** é a palavra *and*.</span><span class="sxs-lookup"><span data-stu-id="f6394-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="f6394-344">Defina **Tipo de projeto** novamente como **Biblioteca de Classes** antes de implantar em um Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="f6394-345">Registrando informações no log</span><span class="sxs-lookup"><span data-stu-id="f6394-345">Log information</span></span>

<span data-ttu-id="f6394-346">É possível registrar em log com facilidade informações de seus componentes de topologia usando o `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="f6394-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="f6394-347">Por exemplo, o seguinte criará uma entrada do log de informações:</span><span class="sxs-lookup"><span data-stu-id="f6394-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="f6394-348">As informações registradas em log podem ser exibidas no **Log do Serviço do Hadoop**, que é encontrado no **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="f6394-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="f6394-349">Expanda a entrada para o seu Storm no cluster HDInsight e expanda **Log de Serviço do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="f6394-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="f6394-350">Por fim, selecione o arquivo de log para exibir.</span><span class="sxs-lookup"><span data-stu-id="f6394-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="f6394-351">Os logs são armazenados na conta de Armazenamento do Azure usada pelo seu cluster.</span><span class="sxs-lookup"><span data-stu-id="f6394-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="f6394-352">Para exibir os logs no Visual Studio, você deve entrar na assinatura do Azure proprietária da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f6394-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="f6394-353">Exibir informações de erro</span><span class="sxs-lookup"><span data-stu-id="f6394-353">View error information</span></span>

<span data-ttu-id="f6394-354">Para exibir erros ocorridos em uma topologia em execução, use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6394-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="f6394-355">No **Gerenciador de Servidores**, clique com o botão direito do mouse no Storm do cluster HDInsight e selecione **Exibir topologias Storm**.</span><span class="sxs-lookup"><span data-stu-id="f6394-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="f6394-356">Para **Spout** e **Bolts**, a coluna **Último Erro** contém informações sobre o último erro ocorrido.</span><span class="sxs-lookup"><span data-stu-id="f6394-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="f6394-357">Selecione **ID do Spout** ou **ID do Bolt** para o componente com um erro listado.</span><span class="sxs-lookup"><span data-stu-id="f6394-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="f6394-358">Na página de detalhes exibida, as informações adicionais do erro serão listadas na seção **Erros** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="f6394-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="f6394-359">Para obter mais informações, selecione uma **Porta** na seção **Executores** da página para ver o log de trabalho do Storm nos últimos minutos.</span><span class="sxs-lookup"><span data-stu-id="f6394-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="f6394-360">Erros durante o envio de topologias</span><span class="sxs-lookup"><span data-stu-id="f6394-360">Errors submitting topologies</span></span>

<span data-ttu-id="f6394-361">Se você encontrar erros ao enviar uma topologia ao HDInsight, poderá encontrar registros para os componentes do lado do servidor que lidam com o envio de topologia em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="f6394-362">Para recuperar esses logs, use o seguinte comando em uma linha de comando:</span><span class="sxs-lookup"><span data-stu-id="f6394-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="f6394-363">Substitua __sshuser__ pela conta de usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="f6394-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="f6394-364">Substitua __clustername__ pelo nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f6394-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="f6394-365">Para saber mais sobre como usar o `scp` e o `ssh` com o HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f6394-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f6394-366">Envios podem falhar por vários motivos:</span><span class="sxs-lookup"><span data-stu-id="f6394-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="f6394-367">O JDK não está instalado ou não está no caminho.</span><span class="sxs-lookup"><span data-stu-id="f6394-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="f6394-368">Dependências de Java necessárias não são incluídas no envio.</span><span class="sxs-lookup"><span data-stu-id="f6394-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="f6394-369">Dependências incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="f6394-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="f6394-370">Nomes de topologia duplicados.</span><span class="sxs-lookup"><span data-stu-id="f6394-370">Duplicate topology names.</span></span>

<span data-ttu-id="f6394-371">Se o log `hdinsight-scpwebapi.out` contém um `FileNotFoundException`, isso pode ser causado pelas seguintes condições:</span><span class="sxs-lookup"><span data-stu-id="f6394-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="f6394-372">O JDK não está no caminho no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f6394-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="f6394-373">Verifique se o JDK está instalado no ambiente de desenvolvimento e que `%JAVA_HOME%/bin` está no caminho.</span><span class="sxs-lookup"><span data-stu-id="f6394-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="f6394-374">Uma dependência de Java está ausente.</span><span class="sxs-lookup"><span data-stu-id="f6394-374">You are missing a Java dependency.</span></span> <span data-ttu-id="f6394-375">Verifique se você está incluindo todos os arquivos .jar necessários como parte do envio.</span><span class="sxs-lookup"><span data-stu-id="f6394-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6394-376">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6394-376">Next steps</span></span>

<span data-ttu-id="f6394-377">Para obter um exemplo de processamento de dados de Hubs de eventos, consulte [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f6394-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="f6394-378">Para obter um exemplo de uma topologia de C# que divide os dados de fluxo em vários fluxos, consulte [Exemplo de Storm C#](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="f6394-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="f6394-379">Para descobrir mais informações sobre como criar topologias de C#, veja [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="f6394-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="f6394-380">Para obter outras maneiras de trabalhar com o HDInsight e mais amostras do Storm no HDInsight, consulte o seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="f6394-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="f6394-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="f6394-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="f6394-382">Guia de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="f6394-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="f6394-383">**Apache Storm no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f6394-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="f6394-384">Implantar e monitorar topologias com o Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="f6394-385">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="f6394-386">**Apache Hadoop no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f6394-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="f6394-387">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f6394-388">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f6394-389">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f6394-390">**Apache HBase no HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f6394-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="f6394-391">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6394-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
