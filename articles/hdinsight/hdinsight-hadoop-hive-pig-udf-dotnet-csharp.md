---
title: aaaUse c# com Hive e Pig no Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse c# definida pelo usuário (UDF) de funções com Hive e Pig no HDInsight do Azure de streaming."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="496a4-103">Usar funções definidas pelo usuário do C# com streaming de Hive e Pig no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="496a4-104">Saiba como toouse c# funções definidas pelo usuário (UDF) com o Apache Hive e Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="496a4-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="496a4-105">etapas de saudação neste documento funcionam com clusters de HDInsight com base em Linux e em Windows.</span><span class="sxs-lookup"><span data-stu-id="496a4-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="496a4-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="496a4-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="496a4-107">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="496a4-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="496a4-108">Ambos Hive e Pig pode transmitir aplicativos de tooexternal de dados para processamento.</span><span class="sxs-lookup"><span data-stu-id="496a4-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="496a4-109">Este processo é conhecido como _streaming_.</span><span class="sxs-lookup"><span data-stu-id="496a4-109">This process is known as _streaming_.</span></span> <span data-ttu-id="496a4-110">Ao usar um aplicativo .NET, Olá transferência dos dados toohello aplicativo STDIN e aplicativo hello retorna resultados de saudação em STDOUT.</span><span class="sxs-lookup"><span data-stu-id="496a4-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="496a4-111">tooread e gravação de STDIN e STDOUT, você pode usar `Console.ReadLine()` e `Console.WriteLine()` de um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="496a4-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="496a4-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="496a4-112">Prerequisites</span></span>

* <span data-ttu-id="496a4-113">Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="496a4-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="496a4-114">Use o IDE que preferir.</span><span class="sxs-lookup"><span data-stu-id="496a4-114">Use whatever IDE you want.</span></span> <span data-ttu-id="496a4-115">Recomendamos o [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 ou o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="496a4-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="496a4-116">Olá as etapas neste documento utilizarem 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="496a4-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="496a4-117">Uma maneira tooupload .exe arquivos toohello cluster e executados trabalhos de Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="496a4-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="496a4-118">É recomendável Olá Data Lake Tools para Visual Studio, o Azure PowerShell e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="496a4-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="496a4-119">Hello etapas deste documento usam Olá Data Lake Tools para arquivos do Visual Studio tooupload hello e execute a consulta de Hive do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="496a4-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="496a4-120">Para obter informações sobre outros trabalhos de Pig e consultas de Hive toorun maneiras, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="496a4-121">Usar o Apache Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="496a4-122">Usar o Apache Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="496a4-123">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="496a4-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="496a4-124">Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="496a4-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="496a4-125">.NET no HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-125">.NET on HDInsight</span></span>

* <span data-ttu-id="496a4-126">__HDInsight baseados em Linux__ clusters usando [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET.</span><span class="sxs-lookup"><span data-stu-id="496a4-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="496a4-127">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="496a4-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="496a4-128">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="496a4-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="496a4-129">toouse uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="496a4-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="496a4-130">__HDInsight baseados em Windows__ clusters usam aplicativos de .NET Olá Microsoft .NET CLR toorun.</span><span class="sxs-lookup"><span data-stu-id="496a4-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="496a4-131">Para obter mais informações sobre a versão de saudação do hello .NET framework e Mono incluídos com versões de HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="496a4-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="496a4-132">Criar hello C\# projetos</span><span class="sxs-lookup"><span data-stu-id="496a4-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="496a4-133">UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="496a4-133">Hive UDF</span></span>

1. <span data-ttu-id="496a4-134">Abra o Visual Studio e crie uma solução.</span><span class="sxs-lookup"><span data-stu-id="496a4-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="496a4-135">Para o tipo de projeto hello, selecione **aplicativo de Console (.NET Framework)**e o novo projeto do nome hello **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="496a4-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="496a4-136">Selecione __.NET Framework 4.5__ se estiver usando um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="496a4-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="496a4-137">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="496a4-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="496a4-138">Substitua o conteúdo de saudação do **Program.cs** com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="496a4-138">Replace hello contents of **Program.cs** with hello following:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="496a4-139">Compile o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="496a4-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="496a4-140">UDF do Pig</span><span class="sxs-lookup"><span data-stu-id="496a4-140">Pig UDF</span></span>

1. <span data-ttu-id="496a4-141">Abra o Visual Studio e crie uma solução.</span><span class="sxs-lookup"><span data-stu-id="496a4-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="496a4-142">Para o tipo de projeto hello, selecione **aplicativo de Console**e o novo projeto do nome hello **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="496a4-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="496a4-143">Substitua o conteúdo de saudação do hello **Program.cs** arquivo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="496a4-144">Este aplicativo analisa linhas Olá enviadas do Pig e reformatar linhas que começam com `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="496a4-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="496a4-145">Salvar **Program.cs**e, em seguida, compilar o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="496a4-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="496a4-146">Carregar toostorage</span><span class="sxs-lookup"><span data-stu-id="496a4-146">Upload toostorage</span></span>

1. <span data-ttu-id="496a4-147">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="496a4-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="496a4-148">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="496a4-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="496a4-149">Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="496a4-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="496a4-150">Expanda o cluster de HDInsight de saudação que você deseja toodeploy este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="496a4-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="496a4-151">Uma entrada com o texto de saudação __(conta de armazenamento padrão)__ está listado.</span><span class="sxs-lookup"><span data-stu-id="496a4-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Mostrando conta de armazenamento Olá para cluster de saudação do Gerenciador de servidores](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="496a4-153">Se essa entrada pode ser expandida, você está usando um __conta de armazenamento do Azure__ como armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="496a4-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="496a4-154">arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, expanda a entrada hello e clique duas vezes Olá __(contêiner padrão)__.</span><span class="sxs-lookup"><span data-stu-id="496a4-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="496a4-155">Se essa entrada não pode ser expandida, você está usando __repositório Azure Data Lake__ como armazenamento de padrão de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="496a4-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="496a4-156">arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, clique duas vezes em Olá __(conta de armazenamento padrão)__ entrada.</span><span class="sxs-lookup"><span data-stu-id="496a4-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="496a4-157">arquivos de .exe do tooupload Olá, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="496a4-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="496a4-158">Se usar um __conta de armazenamento do Azure__, clique ícone de carregamento Olá e, em seguida, procure toohello **bin\debug** pasta Olá **HiveCSharp** projeto.</span><span class="sxs-lookup"><span data-stu-id="496a4-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="496a4-159">Por fim, selecione Olá **HiveCSharp.exe** de arquivo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="496a4-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="496a4-161">Se usar __repositório Azure Data Lake__, uma área vazia na listagem de arquivo hello e, em seguida, selecione __carregar__.</span><span class="sxs-lookup"><span data-stu-id="496a4-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="496a4-162">Por fim, selecione Olá **HiveCSharp.exe** de arquivo e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="496a4-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="496a4-163">Uma vez Olá __HiveCSharp.exe__ carregamento for concluída, o processo de carregamento de repetição Olá para Olá __PigUDF.exe__ arquivo.</span><span class="sxs-lookup"><span data-stu-id="496a4-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="496a4-164">Executar um trabalho do Hive</span><span class="sxs-lookup"><span data-stu-id="496a4-164">Run a Hive query</span></span>

1. <span data-ttu-id="496a4-165">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="496a4-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="496a4-166">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="496a4-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="496a4-167">Cluster de Olá atalho que você implantou Olá **HiveCSharp** aplicativo e, em seguida, selecione **escrever uma consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="496a4-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="496a4-168">Use Olá texto de consulta de Hive Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-168">Use hello following text for hello Hive query:</span></span>

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="496a4-169">Remova os comentários Olá `add file` instrução que corresponde ao tipo de saudação de armazenamento padrão usado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="496a4-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="496a4-170">Essa consulta seleciona Olá `clientid`, `devicemake`, e `devicemodel` os campos do `hivesampletable`e passa campos Olá toohello HiveCSharp.exe aplicativo.</span><span class="sxs-lookup"><span data-stu-id="496a4-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="496a4-171">espera de consulta Olá Olá tooreturn três campos de aplicativo, que são armazenados como `clientid`, `phoneLabel`, e `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="496a4-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="496a4-172">consulta de saudação também espera toofind HiveCSharp.exe na raiz de Olá Olá padrão do contêiner de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="496a4-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="496a4-173">Clique em **enviar** cluster HDInsight do toosubmit Olá trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="496a4-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="496a4-174">Olá **resumo do trabalho de Hive** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="496a4-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="496a4-175">Clique em **atualizar** toorefresh Olá resumo até **Status do trabalho** muda muito**concluído**.</span><span class="sxs-lookup"><span data-stu-id="496a4-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="496a4-176">trabalho de saudação tooview de saída, clique em **saída de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="496a4-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="496a4-177">Executar um trabalho Pig</span><span class="sxs-lookup"><span data-stu-id="496a4-177">Run a Pig job</span></span>

1. <span data-ttu-id="496a4-178">Use uma saudação cluster do HDInsight métodos tooconnect tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="496a4-179">Se você estiver usando um cluster HDInsight __baseado em Linux__, use SSH.</span><span class="sxs-lookup"><span data-stu-id="496a4-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="496a4-180">Por exemplo: `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="496a4-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="496a4-181">Para obter mais informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="496a4-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="496a4-182">Se você estiver usando um __baseados no Windows__ cluster HDInsight, [conectar toohello cluster usando a área de trabalho remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="496a4-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="496a4-183">Use uma saudação seguinte linha de comando do comando toostart Olá Pig:</span><span class="sxs-lookup"><span data-stu-id="496a4-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="496a4-184">Se você estiver usando um cluster baseado no Windows, use Olá comandos a seguir em vez disso:</span><span class="sxs-lookup"><span data-stu-id="496a4-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="496a4-185">Um prompt de `grunt>` é exibido.</span><span class="sxs-lookup"><span data-stu-id="496a4-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="496a4-186">Digite hello toorun um trabalho de Pig que usa o aplicativo do .NET Framework hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="496a4-187">Olá `DEFINE` instrução cria um alias de `streamer` para aplicativos de pigudf.exe Olá, e `CACHE` carrega do armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="496a4-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="496a4-188">Posteriormente, `streamer` é usado com hello `STREAM` tooprocess operador Olá único linhas contidas no LOG e dados de retorno hello como uma série de colunas.</span><span class="sxs-lookup"><span data-stu-id="496a4-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="496a4-189">nome do aplicativo Hello que é usado para streaming deve estar entre Olá \` (apóstrofo) de caractere quando um alias, e ' (aspa simples) quando usado com `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="496a4-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="496a4-190">Depois de inserir a última linha do hello, trabalho Olá deve começar.</span><span class="sxs-lookup"><span data-stu-id="496a4-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="496a4-191">Ele retorna a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="496a4-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="496a4-192">Next steps</span></span>

<span data-ttu-id="496a4-193">Neste documento, você aprendeu como toouse um aplicativo do .NET Framework do Hive e Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="496a4-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="496a4-194">Se você quiser toolearn como toouse Python com Hive e Pig, consulte [uso Python com Hive e Pig no HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="496a4-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="496a4-195">Para outras maneiras toouse Pig e Hive e toolearn sobre o uso de MapReduce, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="496a4-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="496a4-196">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="496a4-197">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="496a4-198">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="496a4-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
