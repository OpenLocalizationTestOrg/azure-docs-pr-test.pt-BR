---
title: "Testar e depurar trabalhos do U-SQL usando execução local e o SDK para U-SQL do Azure Data Lake | Microsoft Docs"
description: "Saiba como usar as Ferramentas do Azure Data Lake para Visual Studio e o SDK para U-SQL do Azure Data Lake a fim de testar e depurar trabalhos do U-SQL em sua estação de trabalho local."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="16d47-103">Testar e depurar trabalhos do U-SQL usando execução local e o SDK para U-SQL do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="16d47-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="16d47-104">Você pode usar as Ferramentas do Azure Data Lake para Visual Studio e SDK para U-SQL do Azure Data Lake a fim de executar trabalhos de U-SQL na sua estação de trabalho da mesma forma que faz no serviço Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="16d47-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="16d47-105">Esses dois recursos de execução local economizam tempo no teste e na depuração de seus trabalhos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="16d47-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="16d47-106">Compreender a pasta raiz de dados e o caminho do arquivo</span><span class="sxs-lookup"><span data-stu-id="16d47-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="16d47-107">Tanto a execução local quanto o SDK para U-SQL exigem uma pasta raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="16d47-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="16d47-108">A pasta raiz de dados é um "repositório local" para a conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="16d47-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="16d47-109">Ela equivale à conta do Azure Data Lake Store de uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="16d47-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="16d47-110">Alternar para uma pasta raiz de dados diferente é como alternar para uma conta de repositório diferente.</span><span class="sxs-lookup"><span data-stu-id="16d47-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="16d47-111">Se você quiser acessar dados compartilhados normalmente com pastas raiz de dados diferentes, deverá usar caminhos absolutos em seus scripts.</span><span class="sxs-lookup"><span data-stu-id="16d47-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="16d47-112">Ou criar links simbólicos de sistema de arquivo (por exemplo, **mklink** em NTFS) na pasta raiz de dados para apontar para os dados compartilhados.</span><span class="sxs-lookup"><span data-stu-id="16d47-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="16d47-113">A pasta raiz de dados é usada para:</span><span class="sxs-lookup"><span data-stu-id="16d47-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="16d47-114">Armazenar metadados, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.</span><span class="sxs-lookup"><span data-stu-id="16d47-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="16d47-115">Pesquisar os caminhos de entrada e saída que são definidos como caminhos relativos no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="16d47-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="16d47-116">Usar caminhos relativos facilita a implantação dos projetos U-SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="16d47-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="16d47-117">Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="16d47-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="16d47-118">O caminho relativo é relativo ao caminho da pasta raiz de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="16d47-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="16d47-119">Recomendamos que você use "/" como o separador de caminho para tornar seus scripts compatíveis com o lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="16d47-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="16d47-120">A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="16d47-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="16d47-121">Nesses exemplos, C:\LocalRunDataRoot é a pasta raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="16d47-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="16d47-122">Caminho relativo</span><span class="sxs-lookup"><span data-stu-id="16d47-122">Relative path</span></span>|<span data-ttu-id="16d47-123">Caminho absoluto</span><span class="sxs-lookup"><span data-stu-id="16d47-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="16d47-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-124">/abc/def/input.csv</span></span> |<span data-ttu-id="16d47-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="16d47-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-126">abc/def/input.csv</span></span>  |<span data-ttu-id="16d47-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="16d47-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="16d47-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="16d47-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="16d47-130">Usar execução local no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16d47-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="16d47-131">As Ferramentas do Data Lake para Visual Studio proporcionam experiência de execução local do U-SQL no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16d47-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="16d47-132">Usando esse recurso, você pode:</span><span class="sxs-lookup"><span data-stu-id="16d47-132">By using this feature, you can:</span></span>

- <span data-ttu-id="16d47-133">Executar um script U-SQL localmente com os assemblies de C#.</span><span class="sxs-lookup"><span data-stu-id="16d47-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="16d47-134">Depurar um assembly de C# localmente.</span><span class="sxs-lookup"><span data-stu-id="16d47-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="16d47-135">Criar, exibir e excluir catálogos do U-SQL (bancos de dados locais, assemblies, esquemas e tabelas) no Gerenciador de servidores.</span><span class="sxs-lookup"><span data-stu-id="16d47-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="16d47-136">Você também pode encontrar o catálogo local no Gerenciador de Servidores.</span><span class="sxs-lookup"><span data-stu-id="16d47-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Catálogo local da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="16d47-138">O instalador das Ferramentas do Data Lake cria uma pasta C:\LocalRunRoot para ser usada como a pasta raiz de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="16d47-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="16d47-139">O paralelismo da execução local padrão é 1.</span><span class="sxs-lookup"><span data-stu-id="16d47-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="16d47-140">Para configurar a execução local no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16d47-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="16d47-141">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16d47-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="16d47-142">Abra o **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="16d47-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="16d47-143">Expanda **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="16d47-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="16d47-144">Clique no menu **Data Lake** e, em seguida, em **Opções e Configurações**.</span><span class="sxs-lookup"><span data-stu-id="16d47-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="16d47-145">Na árvore à esquerda, expanda **Azure Data Lake** e, em seguida, **Geral**.</span><span class="sxs-lookup"><span data-stu-id="16d47-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Definir configurações de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="16d47-147">É necessário um projeto U-SQL do Visual Studio para realizar a execução local.</span><span class="sxs-lookup"><span data-stu-id="16d47-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="16d47-148">Essa parte é diferente de executar scripts U-SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="16d47-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="16d47-149">Para executar um script U-SQL localmente</span><span class="sxs-lookup"><span data-stu-id="16d47-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="16d47-150">No Visual Studio, abra o projeto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="16d47-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="16d47-151">Clique com o botão direito do mouse em um script U-SQL no Gerenciador de Soluções e clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="16d47-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="16d47-152">Selecione **(Local)** como a conta do Analytics para executar o script localmente.</span><span class="sxs-lookup"><span data-stu-id="16d47-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="16d47-153">Você pode também clicar na conta **(Local)** na parte superior da janela do script e clicar em **Enviar** (ou usar as teclas de acesso CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="16d47-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Enviar trabalhos de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="16d47-155">Depurar scripts e assemblies do C# localmente</span><span class="sxs-lookup"><span data-stu-id="16d47-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="16d47-156">É possível depurar assemblies do C# sem os enviar nem os registrar para o Serviço Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="16d47-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="16d47-157">Você pode definir pontos de interrupção no arquivo code-behind e em um projeto do C# referenciado.</span><span class="sxs-lookup"><span data-stu-id="16d47-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="16d47-158">Para depurar o código local no arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="16d47-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="16d47-159">Definir pontos de interrupção no arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="16d47-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="16d47-160">Pressione F5 para depurar o script localmente.</span><span class="sxs-lookup"><span data-stu-id="16d47-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="16d47-161">O procedimento a seguir só funciona no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="16d47-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="16d47-162">No Visual Studio mais antigo, talvez seja necessário adicionar manualmente os arquivos pdb.</span><span class="sxs-lookup"><span data-stu-id="16d47-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="16d47-163">Para depurar o código local em um projeto do C# referenciado</span><span class="sxs-lookup"><span data-stu-id="16d47-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="16d47-164">Crie um projeto de Assembly do C# e compile-o para gerar o dll de saída.</span><span class="sxs-lookup"><span data-stu-id="16d47-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="16d47-165">Registre o dll usando uma instrução U-SQL:</span><span class="sxs-lookup"><span data-stu-id="16d47-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="16d47-166">Definir pontos de interrupção no código C#.</span><span class="sxs-lookup"><span data-stu-id="16d47-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="16d47-167">Pressione F5 para depurar o script referenciando a dll do C# localmente.</span><span class="sxs-lookup"><span data-stu-id="16d47-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="16d47-168">Usar execução local no SDK para U-SQL do Data Lake</span><span class="sxs-lookup"><span data-stu-id="16d47-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="16d47-169">Além de executar scripts U-SQL localmente usando o Visual Studio, você pode usar o SDK para U-SQL do Azure Data Lake para executá-los localmente com interfaces de programação e linha de comando.</span><span class="sxs-lookup"><span data-stu-id="16d47-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="16d47-170">Você pode dimensionar seu teste local U-SQL com eles.</span><span class="sxs-lookup"><span data-stu-id="16d47-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="16d47-171">Saiba mais sobre o [SDK do U-SQL do Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="16d47-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="16d47-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16d47-172">Next steps</span></span>

* <span data-ttu-id="16d47-173">Para ver uma consulta mais complexa, consulte [Analisar logs de site usando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="16d47-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="16d47-174">Para ver detalhes do trabalho, confira [Usar o Navegador de Trabalhos e o Modo de Exibição de Trabalho para trabalhos do Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="16d47-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="16d47-175">Para usar o modo de exibição de execução de vértice, veja [Usar o Modo de Exibição de Execução de Vértice nas Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="16d47-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
