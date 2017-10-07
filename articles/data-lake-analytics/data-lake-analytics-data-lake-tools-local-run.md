---
title: "aaaTest e depuração U-SQL trabalhos usando locais executar e Olá SDK do SQL Azure Data Lake U | Microsoft Docs"
description: "Saiba como toouse Azure Data Lake Tools para Visual Studio e tootest do SDK do Azure Data Lake U-SQL hello e depuração U-SQL trabalhos em sua estação de trabalho local."
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
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="53292-103">Testar e depurar os trabalhos de U-SQL usando local executar e Olá SDK do Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="53292-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="53292-104">Você pode usar o Azure Data Lake Tools para Visual Studio e trabalhos do hello SDK do Azure Data Lake U-SQL toorun U-SQL em sua estação de trabalho, exatamente como é possível no serviço do Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="53292-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="53292-105">Esses dois recursos de execução local economizam tempo no teste e na depuração de seus trabalhos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="53292-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="53292-106">Entender a pasta de dados raiz hello e caminho do arquivo hello</span><span class="sxs-lookup"><span data-stu-id="53292-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="53292-107">Execução local e Olá SDK U-SQL exigem uma pasta raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="53292-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="53292-108">pasta de dados raiz Olá é "armazenamento local" para a conta de computação local hello.</span><span class="sxs-lookup"><span data-stu-id="53292-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="53292-109">É a conta do repositório Azure Data Lake toohello equivalente de uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53292-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="53292-110">Pasta raiz de dados diferentes alternando tooa é como alternar tooa conta de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="53292-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="53292-111">Se você quiser tooaccess normalmente compartilhado dados com pastas raiz de dados diferentes, você deve usar caminhos absolutos em seus scripts.</span><span class="sxs-lookup"><span data-stu-id="53292-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="53292-112">Criar links simbólicos do sistema de arquivo (por exemplo, **mklink** em NTFS) em Olá raiz de dados pasta toopoint toohello dados compartilhados.</span><span class="sxs-lookup"><span data-stu-id="53292-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="53292-113">pasta de dados raiz Olá é usada para:</span><span class="sxs-lookup"><span data-stu-id="53292-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="53292-114">Armazenar metadados, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.</span><span class="sxs-lookup"><span data-stu-id="53292-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="53292-115">Pesquise hello de entrada e os caminhos de saída que são definidos como caminhos relativos no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="53292-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="53292-116">Usar caminhos relativos torna mais fácil toodeploy seu tooAzure de projetos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="53292-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="53292-117">Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="53292-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="53292-118">caminho relativo da saudação é relativo toohello caminho da pasta raiz de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="53292-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="53292-119">É recomendável que você use "/" como Olá toomake do separador de caminho seus scripts compatíveis com do lado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="53292-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="53292-120">A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="53292-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="53292-121">Nestes exemplos, C:\LocalRunDataRoot é a pasta raiz de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="53292-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="53292-122">Caminho relativo</span><span class="sxs-lookup"><span data-stu-id="53292-122">Relative path</span></span>|<span data-ttu-id="53292-123">Caminho absoluto</span><span class="sxs-lookup"><span data-stu-id="53292-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="53292-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-124">/abc/def/input.csv</span></span> |<span data-ttu-id="53292-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="53292-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-126">abc/def/input.csv</span></span>  |<span data-ttu-id="53292-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="53292-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="53292-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="53292-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="53292-130">Usar execução local no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53292-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="53292-131">As Ferramentas do Data Lake para Visual Studio proporcionam experiência de execução local do U-SQL no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53292-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="53292-132">Usando esse recurso, você pode:</span><span class="sxs-lookup"><span data-stu-id="53292-132">By using this feature, you can:</span></span>

- <span data-ttu-id="53292-133">Executar um script U-SQL localmente com os assemblies de C#.</span><span class="sxs-lookup"><span data-stu-id="53292-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="53292-134">Depurar um assembly de C# localmente.</span><span class="sxs-lookup"><span data-stu-id="53292-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="53292-135">Criar, exibir e excluir catálogos do U-SQL (bancos de dados locais, assemblies, esquemas e tabelas) no Gerenciador de servidores.</span><span class="sxs-lookup"><span data-stu-id="53292-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="53292-136">Você também pode encontrar catálogo local Olá também do Gerenciador de servidores.</span><span class="sxs-lookup"><span data-stu-id="53292-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Catálogo local da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="53292-138">instalador do Data Lake Tools Olá cria um toobe de pasta C:\LocalRunRoot usado como pasta raiz de dados padrão, Olá.</span><span class="sxs-lookup"><span data-stu-id="53292-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="53292-139">paralelismo de execução local saudação padrão é 1.</span><span class="sxs-lookup"><span data-stu-id="53292-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="53292-140">tooconfigure local executar no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53292-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="53292-141">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53292-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="53292-142">Abra o **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="53292-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="53292-143">Expanda **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="53292-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="53292-144">Clique em Olá **Data Lake** menu e clique **opções e configurações**.</span><span class="sxs-lookup"><span data-stu-id="53292-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="53292-145">Na árvore de saudação à esquerda, expanda **Azure Data Lake**e, em seguida, expanda **geral**.</span><span class="sxs-lookup"><span data-stu-id="53292-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Definir configurações de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="53292-147">É necessário um projeto U-SQL do Visual Studio para realizar a execução local.</span><span class="sxs-lookup"><span data-stu-id="53292-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="53292-148">Essa parte é diferente de executar scripts U-SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="53292-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="53292-149">toorun um U-SQL script localmente</span><span class="sxs-lookup"><span data-stu-id="53292-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="53292-150">No Visual Studio, abra o projeto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="53292-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="53292-151">Clique com o botão direito do mouse em um script U-SQL no Gerenciador de Soluções e clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="53292-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="53292-152">Selecione **(Local)** como hello análise conta toorun seu script localmente.</span><span class="sxs-lookup"><span data-stu-id="53292-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="53292-153">Você também pode clicar em Olá **(Local)** conta na parte superior de saudação da janela de script e, em seguida, clique em **enviar** (ou usar Olá Ctrl + teclas de atalho F5).</span><span class="sxs-lookup"><span data-stu-id="53292-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Enviar trabalhos de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="53292-155">Depurar scripts e assemblies do C# localmente</span><span class="sxs-lookup"><span data-stu-id="53292-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="53292-156">Você pode depurar c# assemblies sem enviar e registrando-tooAzure serviço de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53292-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="53292-157">Você pode definir pontos de interrupção em ambos os Olá arquivo code-behind em um projeto c# referenciado.</span><span class="sxs-lookup"><span data-stu-id="53292-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="53292-158">código de toodebug local no arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="53292-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="53292-159">Definir pontos de interrupção Olá arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="53292-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="53292-160">Pressione o script de saudação de toodebug F5 localmente.</span><span class="sxs-lookup"><span data-stu-id="53292-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="53292-161">Olá seguindo o procedimento só funciona no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="53292-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="53292-162">No Visual Studio mais antigos talvez seja necessário toomanually adicionar os arquivos pdb hello.</span><span class="sxs-lookup"><span data-stu-id="53292-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="53292-163">código de toodebug local em um projeto c# referenciado</span><span class="sxs-lookup"><span data-stu-id="53292-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="53292-164">Criar um projeto c# Assembly e compile toogenerate Olá saída dll.</span><span class="sxs-lookup"><span data-stu-id="53292-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="53292-165">Registre a dll de saudação usando uma instrução U-SQL:</span><span class="sxs-lookup"><span data-stu-id="53292-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="53292-166">Definir pontos de interrupção Olá código c#.</span><span class="sxs-lookup"><span data-stu-id="53292-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="53292-167">Pressione F5 toodebug Olá script referenciando a dll de saudação c# localmente.</span><span class="sxs-lookup"><span data-stu-id="53292-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="53292-168">Usar local executar da saudação SDK Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="53292-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="53292-169">Além disso toorunning U-SQL scripts localmente usando o Visual Studio, você pode usar scripts de U-SQL Olá SDK do Azure Data Lake U-SQL toorun localmente com interfaces de programação e de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="53292-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="53292-170">Você pode dimensionar seu teste local U-SQL com eles.</span><span class="sxs-lookup"><span data-stu-id="53292-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="53292-171">Saiba mais sobre o [SDK do U-SQL do Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="53292-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="53292-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53292-172">Next steps</span></span>

* <span data-ttu-id="53292-173">toosee uma consulta mais complexa, consulte [analisar logs de site usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="53292-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="53292-174">detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="53292-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="53292-175">exibição de execuções de vértice de saudação toouse, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="53292-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
