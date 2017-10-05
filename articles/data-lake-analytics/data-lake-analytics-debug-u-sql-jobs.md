---
title: Depurar trabalhos do U-SQL | Microsoft Docs
description: "Saiba como depurar um vértice com falha do U-SQL usando o Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="661d1-103">Depurar um código C# definido pelo usuário em trabalhos com falha do U-SQL</span><span class="sxs-lookup"><span data-stu-id="661d1-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="661d1-104">O U-SQL fornece um modelo de extensibilidade usando o C# e, portanto, você pode escrever seu código para adicionar funcionalidade, como um extrator ou redutor personalizado.</span><span class="sxs-lookup"><span data-stu-id="661d1-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="661d1-105">Para saber mais, consulte o [Guia de programação do U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="661d1-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="661d1-106">Na prática, qualquer código pode precisar de depuração e sistemas de Big Data podem fornecer apenas informações limitadas de depuração em tempo de execução como arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="661d1-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="661d1-107">As Ferramentas do Azure Data Lake para Visual Studio fornecem um recurso chamado **Falha na Depuração de Vértice**, que permite clonar um trabalho com falha da nuvem para o computador local para depuração.</span><span class="sxs-lookup"><span data-stu-id="661d1-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="661d1-108">O clone local captura todo o ambiente de nuvem, incluindo dados de entrada e código do usuário.</span><span class="sxs-lookup"><span data-stu-id="661d1-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="661d1-109">O vídeo a seguir demonstra a Falha na Depuração de Vértice nas Ferramentas do Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="661d1-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="661d1-110">O Visual Studio exige as seguintes duas atualizações, caso elas ainda não estejam instaladas: [Microsoft Visual C++ 2015 Redistributable Atualização 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Tempo de Execução C Universal do Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="661d1-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="661d1-111">Baixar o vértice com falha no computador local</span><span class="sxs-lookup"><span data-stu-id="661d1-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="661d1-112">Ao abrir um trabalho com falha nas Ferramentas do Azure Data Lake para Visual Studio, você verá uma barra amarela de alerta com mensagens de erro detalhadas na guia de erros.</span><span class="sxs-lookup"><span data-stu-id="661d1-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="661d1-113">Clique em **Download** para baixar todos os recursos e fluxos de entrada necessários.</span><span class="sxs-lookup"><span data-stu-id="661d1-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="661d1-114">Se o download não for concluído, clique em **Tentar Novamente**.</span><span class="sxs-lookup"><span data-stu-id="661d1-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="661d1-115">Clique em **Abrir** após a conclusão do download para gerar um ambiente de depuração local.</span><span class="sxs-lookup"><span data-stu-id="661d1-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="661d1-116">Uma nova instância do Visual Studio com uma solução de depuração é criada e aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="661d1-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Vértice para download do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="661d1-118">Os trabalhos podem incluir arquivos de origem code-behind ou assemblies registrados e esses dois tipos têm diferentes cenários de depuração.</span><span class="sxs-lookup"><span data-stu-id="661d1-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="661d1-119">Depurar um trabalho com falha com code-behind</span><span class="sxs-lookup"><span data-stu-id="661d1-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="661d1-120">Depurar um trabalho com falha com assemblies</span><span class="sxs-lookup"><span data-stu-id="661d1-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="661d1-121">Depurar um trabalho com falha com code-behind</span><span class="sxs-lookup"><span data-stu-id="661d1-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="661d1-122">Se um trabalho do U-SQL falhar e o trabalho incluir o código do usuário (geralmente chamado `Script.usql.cs` em um projeto do U-SQL), esse código-fonte será importado para a solução de depuração.</span><span class="sxs-lookup"><span data-stu-id="661d1-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="661d1-123">Nela, você pode usar as ferramentas de depuração do Visual Studio (inspeção, variáveis, etc.) para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="661d1-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="661d1-124">Antes da depuração, marque a opção **Exceções do Common Language Runtime** na janela Configurações de Exceção (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="661d1-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Configuração do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="661d1-126">Pressione **F5** para executar o código code-behind.</span><span class="sxs-lookup"><span data-stu-id="661d1-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="661d1-127">Ele será executado até que seja interrompido por uma exceção.</span><span class="sxs-lookup"><span data-stu-id="661d1-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="661d1-128">Abra o arquivo `ADLTool_Codebehind.usql.cs` e defina pontos de interrupção e, em seguida, pressione **F5** para depurar o código passo a passo.</span><span class="sxs-lookup"><span data-stu-id="661d1-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Exceção de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="661d1-130">Depurar trabalho em falha com assemblies</span><span class="sxs-lookup"><span data-stu-id="661d1-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="661d1-131">Se você usar assemblies registrados no script do U-SQL, o sistema não poderá obter o código-fonte automaticamente.</span><span class="sxs-lookup"><span data-stu-id="661d1-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="661d1-132">Nesse caso, adicione manualmente os arquivos do código-fonte dos assemblies à solução.</span><span class="sxs-lookup"><span data-stu-id="661d1-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="661d1-133">Configurar a solução</span><span class="sxs-lookup"><span data-stu-id="661d1-133">Configure the solution</span></span>

1. <span data-ttu-id="661d1-134">Clique com o botão direito do mouse em **Solução “VertexDebug” > Adicionar > Projeto Existente...** para encontrar o código-fonte dos assemblies e adicionar o projeto à solução de depuração.</span><span class="sxs-lookup"><span data-stu-id="661d1-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Adicionar projeto de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="661d1-136">Clique com o botão direito do mouse em **LocalVertexHost > Propriedades** na solução e copie o caminho do **Diretório de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="661d1-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="661d1-137">Clique com o botão direito do mouse em **projeto de código-fonte do assembly > Propriedades**, selecione a guia **Compilar** à esquerda e, em seguida, cole o caminho copiado como **Saída > Caminho de saída**.</span><span class="sxs-lookup"><span data-stu-id="661d1-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Definir caminho pdb da depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="661d1-139">Pressione **Ctrl+Alt+E** e marque **Exceções de Common Language Runtime** na janela Configurações de exceção.</span><span class="sxs-lookup"><span data-stu-id="661d1-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="661d1-140">Iniciar depuração</span><span class="sxs-lookup"><span data-stu-id="661d1-140">Start debug</span></span>

1. <span data-ttu-id="661d1-141">Clique com o botão direito do mouse em **projeto de código-fonte do assembly > Recompilar** para gerar arquivos .pdb no diretório de trabalho `LocalVertexHost`.</span><span class="sxs-lookup"><span data-stu-id="661d1-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="661d1-142">Pressione **F5** e o projeto será executado até que seja interrompido por uma exceção.</span><span class="sxs-lookup"><span data-stu-id="661d1-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="661d1-143">Talvez você veja a seguinte mensagem de aviso, que poderá ser ignorada.</span><span class="sxs-lookup"><span data-stu-id="661d1-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="661d1-144">Pode levar um minuto para que a tela de depuração seja exibida.</span><span class="sxs-lookup"><span data-stu-id="661d1-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Aviso do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="661d1-146">Abra o código-fonte e defina pontos de interrupção e, em seguida, pressione **F5** para depurar o código passo a passo.</span><span class="sxs-lookup"><span data-stu-id="661d1-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="661d1-147">Você também pode usar as ferramentas de depuração do Visual Studio (inspeção, variáveis, etc.) para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="661d1-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="661d1-148">Recompile o projeto de código-fonte do assembly sempre depois de modificar o código para gerar os arquivos .pdb atualizados.</span><span class="sxs-lookup"><span data-stu-id="661d1-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="661d1-149">Após a depuração, se o projeto for concluído com êxito, a janela de saída mostrará a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="661d1-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Depuração do U-SQL do Azure Data Lake Analytics bem sucedida](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="661d1-151">Reenviar o trabalho</span><span class="sxs-lookup"><span data-stu-id="661d1-151">Resubmit the job</span></span>

<span data-ttu-id="661d1-152">Depois de concluir a depuração, reenvie o trabalho com falha.</span><span class="sxs-lookup"><span data-stu-id="661d1-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="661d1-153">Para trabalhos com soluções code-behind, copie o código C# para o arquivo de origem code-behind (geralmente, `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="661d1-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="661d1-154">Para trabalhos com assemblies, registre os assemblies .dll atualizados no banco de dados do ADLA:</span><span class="sxs-lookup"><span data-stu-id="661d1-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="661d1-155">No Gerenciador de Servidores ou no Cloud Explorer, expanda o nó **conta do ADLA > Bancos de dados**.</span><span class="sxs-lookup"><span data-stu-id="661d1-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="661d1-156">Clique com o botão direito do mouse em **Assemblies** e registre os novos assemblies .dll no banco de dados do ADLA: ![assembly de registro de depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="661d1-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="661d1-157">Reenvie o trabalho.</span><span class="sxs-lookup"><span data-stu-id="661d1-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="661d1-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="661d1-158">Next steps</span></span>

- [<span data-ttu-id="661d1-159">Guia de programação do U-SQL</span><span class="sxs-lookup"><span data-stu-id="661d1-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="661d1-160">Desenvolver operadores do U-SQL definidos pelo usuário para trabalhos do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="661d1-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="661d1-161">Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="661d1-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
