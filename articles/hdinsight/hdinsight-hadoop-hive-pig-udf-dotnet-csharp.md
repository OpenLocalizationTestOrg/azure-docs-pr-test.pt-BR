---
title: "Usar o C# com o Hive e Pig no Hadoop no HDInsight – Azure | Microsoft Docs"
description: "Saiba como usar as UDFs (Funções Definidas pelo Usuário) do C# com streaming do Hive e Pig no Azure HDInsight."
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
ms.openlocfilehash: 58e7af47be71c3e0389e5fb4641e124eb648494e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="30bf9-103">Usar funções definidas pelo usuário do C# com streaming de Hive e Pig no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="30bf9-104">Saiba como usar as UDFs (Funções Definidas pelo Usuário) do C# com o Apache Hive e Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30bf9-104">Learn how to use C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30bf9-105">As etapas neste documento só funcionam com clusters HDInsight baseados no Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="30bf9-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="30bf9-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="30bf9-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="30bf9-107">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="30bf9-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="30bf9-108">Tanto o Hive quanto o Pig podem passar dados para aplicativos externos para processamento.</span><span class="sxs-lookup"><span data-stu-id="30bf9-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="30bf9-109">Este processo é conhecido como _streaming_.</span><span class="sxs-lookup"><span data-stu-id="30bf9-109">This process is known as _streaming_.</span></span> <span data-ttu-id="30bf9-110">Ao usar um aplicativos .NET, os dados são passados para o aplicativo em STDIN e o aplicativo retornará os resultados em STDOUT.</span><span class="sxs-lookup"><span data-stu-id="30bf9-110">When using a .NET applciation, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="30bf9-111">Para ler e gravar por meio de STDIN e STDOUT, use `Console.ReadLine()` e `Console.WriteLine()` de um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="30bf9-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30bf9-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="30bf9-112">Prerequisites</span></span>

* <span data-ttu-id="30bf9-113">Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="30bf9-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="30bf9-114">Use o IDE que preferir.</span><span class="sxs-lookup"><span data-stu-id="30bf9-114">Use whatever IDE you want.</span></span> <span data-ttu-id="30bf9-115">Recomendamos o [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 ou o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="30bf9-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="30bf9-116">As etapas neste tutorial usam o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="30bf9-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="30bf9-117">Uma forma de carregar arquivos .exe para o cluster e executar trabalhos de Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="30bf9-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="30bf9-118">Recomendamos as Ferramentas do Data Lake para Visual Studio, o Azure PowerShell e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="30bf9-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="30bf9-119">As etapas neste documento usam as Ferramentas do Data Lake para Visual Studio para carregar os arquivos e executar o exemplo de consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="30bf9-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="30bf9-120">Para obter informações sobre outras maneiras de executar consultas do Hive e trabalhos do Pig, veja os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="30bf9-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="30bf9-121">Usar o Apache Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="30bf9-122">Usar o Apache Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="30bf9-123">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30bf9-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="30bf9-124">Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="30bf9-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="30bf9-125">.NET no HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-125">.NET on HDInsight</span></span>

* <span data-ttu-id="30bf9-126">Clusters do __HDInsight baseado em Linux__ usam [Mono (https://mono-project.com)](https://mono-project.com) para executar aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="30bf9-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="30bf9-127">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="30bf9-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="30bf9-128">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="30bf9-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="30bf9-129">Para usar uma versão específica do Mono, consulte o documento [Instalar ou atualizar](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="30bf9-129">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="30bf9-130">Clusters do __HDInsight baseado em Windows__ usam CLR do Microsoft .NET para executar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30bf9-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="30bf9-131">Para obter mais informações sobre a versão do .NET Framework e do Mono incluídas no HDInsight, consulte [Versões do componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="30bf9-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="30bf9-132">Criar os projetos em C\#</span><span class="sxs-lookup"><span data-stu-id="30bf9-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="30bf9-133">UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="30bf9-133">Hive UDF</span></span>

1. <span data-ttu-id="30bf9-134">Abra o Visual Studio e crie uma solução.</span><span class="sxs-lookup"><span data-stu-id="30bf9-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="30bf9-135">Para o tipo de projeto, selecione **Aplicativo de Console (.NET Framework)** e nomeie o novo projeto como **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="30bf9-136">Selecione __.NET Framework 4.5__ se estiver usando um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="30bf9-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="30bf9-137">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="30bf9-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="30bf9-138">Substitua os conteúdos de **Program.cs** pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="30bf9-138">Replace the contents of **Program.cs** with the following:</span></span>

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
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
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

3. <span data-ttu-id="30bf9-139">Compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="30bf9-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="30bf9-140">UDF do Pig</span><span class="sxs-lookup"><span data-stu-id="30bf9-140">Pig UDF</span></span>

1. <span data-ttu-id="30bf9-141">Abra o Visual Studio e crie uma solução.</span><span class="sxs-lookup"><span data-stu-id="30bf9-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="30bf9-142">Para o tipo de projeto, selecione **Aplicativo de Console** e nomeie o novo projeto como **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="30bf9-143">Substitua o conteúdo do arquivo **Program.cs** pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="30bf9-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

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
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="30bf9-144">Esse aplicativo analisa as linhas enviadas do Pig e reformata as linhas que começam com `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="30bf9-144">This application parses the lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="30bf9-145">Salve **Program.cs**, e, em seguida, compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="30bf9-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="30bf9-146">Carregar para o armazenamento</span><span class="sxs-lookup"><span data-stu-id="30bf9-146">Upload to storage</span></span>

1. <span data-ttu-id="30bf9-147">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="30bf9-148">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="30bf9-149">Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="30bf9-150">Expanda o cluster HDInsight no qual você deseja implantar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30bf9-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="30bf9-151">Uma entrada com o texto __(Conta de armazenamento padrão)__ é listada.</span><span class="sxs-lookup"><span data-stu-id="30bf9-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Gerenciador de Servidores mostrando a conta de armazenamento para o cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="30bf9-153">Se essa entrada puder ser expandida, você estará usando uma __Conta de Armazenamento do Azure__ como armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="30bf9-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="30bf9-154">Para exibir os arquivos no armazenamento padrão para o cluster, expanda a entrada e clique duas vezes no __(Contêiner Padrão)__.</span><span class="sxs-lookup"><span data-stu-id="30bf9-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="30bf9-155">Se essa entrada não puder ser expandida, você estará usando __Azure Data Lake Store__ como o armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="30bf9-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="30bf9-156">Para exibir os arquivos no armazenamento padrão do cluster, clique duas vezes na entrada __(Conta de Armazenamento Padrão)__.</span><span class="sxs-lookup"><span data-stu-id="30bf9-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="30bf9-157">Para carregar os arquivos .exe, use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="30bf9-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="30bf9-158">Se estiver usando uma __Conta de Armazenamento do Azure__, clique no ícone de upload e, em seguida, navegue até a pasta **bin\debug** do projeto **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="30bf9-159">Por fim, selecione o arquivo **HiveCSharp.exe** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="30bf9-161">Se estiver usando o __Azure Data Lake Store__, clique com o botão direito do mouse em uma área vazia na listagem de arquivos e, em seguida, selecione __Carregar__.</span><span class="sxs-lookup"><span data-stu-id="30bf9-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="30bf9-162">Por fim, selecione o arquivo **HiveCSharp.exe** e clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="30bf9-163">Após o __HiveCSharp.exe__ ser carregado, repita o processo de upload para o arquivo __PigUDF.exe__.</span><span class="sxs-lookup"><span data-stu-id="30bf9-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="30bf9-164">Executar um trabalho do Hive</span><span class="sxs-lookup"><span data-stu-id="30bf9-164">Run a Hive query</span></span>

1. <span data-ttu-id="30bf9-165">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="30bf9-166">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="30bf9-167">Clique com o botão direito do mouse no cluster em que você implantou o aplicativo **HiveCSharp** e, em seguida, selecione **Escrever uma consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="30bf9-168">Use o texto a seguir para a consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="30bf9-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="30bf9-169">Remova a marca de comentário da instrução `add file` que corresponde ao tipo de armazenamento padrão usado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="30bf9-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="30bf9-170">Esta consulta seleciona os campos `clientid`, `devicemake` e `devicemodel` de `hivesampletable`, e passa os campos para o aplicativo HiveCSharp.exe.</span><span class="sxs-lookup"><span data-stu-id="30bf9-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="30bf9-171">A consulta espera que o aplicativo retorne três campos, que são armazenados como `clientid`, `phoneLabel` e `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="30bf9-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="30bf9-172">A consulta também espera encontrar HiveCSharp.exe na raiz do contêiner de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="30bf9-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="30bf9-173">Clique em **Enviar** para enviar o trabalho para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30bf9-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="30bf9-174">A janela **Resumo do trabalho Hive** é aberta.</span><span class="sxs-lookup"><span data-stu-id="30bf9-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="30bf9-175">Clique em **Atualizar** para atualizar o resumo até que **Status do trabalho** mude para **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="30bf9-176">Para exibir a saída do trabalho, clique em **Saída do trabalho**.</span><span class="sxs-lookup"><span data-stu-id="30bf9-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="30bf9-177">Executar um trabalho Pig</span><span class="sxs-lookup"><span data-stu-id="30bf9-177">Run a Pig job</span></span>

1. <span data-ttu-id="30bf9-178">Use um dos seguintes métodos para se conectar ao seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="30bf9-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="30bf9-179">Se você estiver usando um cluster HDInsight __baseado em Linux__, use SSH.</span><span class="sxs-lookup"><span data-stu-id="30bf9-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="30bf9-180">Por exemplo: `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="30bf9-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="30bf9-181">Para obter mais informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="30bf9-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="30bf9-182">Se você estiver usando um cluster HDInsight __baseado em Windows__, [Conecte-se ao cluster usando a Área de Trabalho Remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="30bf9-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="30bf9-183">Use um dos comandos a seguir para iniciar a linha de comando do Pig:</span><span class="sxs-lookup"><span data-stu-id="30bf9-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="30bf9-184">Se você estiver usando um cluster baseado em Windows, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="30bf9-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="30bf9-185">Um prompt de `grunt>` é exibido.</span><span class="sxs-lookup"><span data-stu-id="30bf9-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="30bf9-186">Digite o seguinte para executar um trabalho do Pig que usa o aplicativo do .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="30bf9-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="30bf9-187">A instrução `DEFINE` cria um alias de `streamer` para os aplicativos pigudf.exe, enquanto `CACHE` o carrega do armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="30bf9-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="30bf9-188">Posteriormente, `streamer` é usado com o operador `STREAM` para processar as linhas individuais contidas no LOG e retornar os dados como uma série de colunas.</span><span class="sxs-lookup"><span data-stu-id="30bf9-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30bf9-189">O nome do aplicativo que é usado para streaming deve estar entre o caractere \` (acento grave) quando se tratar de um alias e ' (aspa simples) quando usado com `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="30bf9-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="30bf9-190">Depois de inserir a última linha, o trabalho deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="30bf9-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="30bf9-191">Isso retorna saídas semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="30bf9-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="30bf9-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30bf9-192">Next steps</span></span>

<span data-ttu-id="30bf9-193">Neste documento, você aprendeu a usar um aplicativo do .NET Framework do Hive e do Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30bf9-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="30bf9-194">Se você quiser aprender como usar o Python com Hive e Pig, consulte [Usar o Python com o Hive e o Pig no HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="30bf9-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="30bf9-195">Para obter outras formas de usar o Pig e o Hive e para saber como usar o MapReduce, consulte os documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="30bf9-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="30bf9-196">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="30bf9-197">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="30bf9-198">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="30bf9-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
