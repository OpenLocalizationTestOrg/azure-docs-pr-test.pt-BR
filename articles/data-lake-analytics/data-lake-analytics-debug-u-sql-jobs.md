---
title: trabalhos aaaDebug U-SQL | Microsoft Docs
description: "Saiba como toodebug um U-SQL falha vértice usando o Visual Studio."
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="b65f4-103">Depurar um código C# definido pelo usuário em trabalhos com falha do U-SQL</span><span class="sxs-lookup"><span data-stu-id="b65f4-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="b65f4-104">U-SQL fornece um modelo de extensibilidade usando c#, portanto você pode escrever sua funcionalidade de tooadd código como um extrator personalizado ou Redutor.</span><span class="sxs-lookup"><span data-stu-id="b65f4-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="b65f4-105">mais, consulte toolearn [guia de programação de U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="b65f4-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="b65f4-106">Na prática, qualquer código pode precisar de depuração e sistemas de Big Data podem fornecer apenas informações limitadas de depuração em tempo de execução como arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="b65f4-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="b65f4-107">Azure Data Lake Tools para Visual Studio fornece um recurso chamado **Falha na depuração de vértice**, que permite que você clonar um trabalho com falha do computador local do hello nuvem tooyour para depuração.</span><span class="sxs-lookup"><span data-stu-id="b65f4-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="b65f4-108">clone local Olá captura o ambiente de nuvem inteira hello, incluindo quaisquer dados de entrada e o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="b65f4-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="b65f4-109">Olá vídeo a seguir demonstra falha vértice depurar no Azure Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b65f4-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="b65f4-110">O Visual Studio requer Olá após duas atualizações, se eles não ainda estiverem instalados: [Microsoft Visual C++ 2015 Redistributable atualização 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Universal em tempo de execução do C para Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="b65f4-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="b65f4-111">Falha no download do vértice toolocal máquina</span><span class="sxs-lookup"><span data-stu-id="b65f4-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="b65f4-112">Quando você abre um trabalho com falha no Azure Data Lake Tools para Visual Studio, verá uma barra amarela de alerta com mensagens de erro detalhadas na guia erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="b65f4-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="b65f4-113">Clique em **baixar** toodownload todos Olá necessários recursos e fluxos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b65f4-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="b65f4-114">Se o download de saudação não for concluída, clique em **novamente**.</span><span class="sxs-lookup"><span data-stu-id="b65f4-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="b65f4-115">Clique em **abrir** após o download de saudação toogenerate um ambiente de depuração local.</span><span class="sxs-lookup"><span data-stu-id="b65f4-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="b65f4-116">Uma nova instância do Visual Studio com uma solução de depuração é criada e aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b65f4-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Vértice para download do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="b65f4-118">Os trabalhos podem incluir arquivos de origem code-behind ou assemblies registrados e esses dois tipos têm diferentes cenários de depuração.</span><span class="sxs-lookup"><span data-stu-id="b65f4-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="b65f4-119">Depurar um trabalho com falha com code-behind</span><span class="sxs-lookup"><span data-stu-id="b65f4-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="b65f4-120">Depurar um trabalho com falha com assemblies</span><span class="sxs-lookup"><span data-stu-id="b65f4-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="b65f4-121">Depurar um trabalho com falha com code-behind</span><span class="sxs-lookup"><span data-stu-id="b65f4-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="b65f4-122">Se um trabalho de U-SQL falha e o trabalho de saudação inclui o código do usuário (geralmente denominado `Script.usql.cs` em um projeto de U-SQL), que o código-fonte é importado para Olá depuração solução.</span><span class="sxs-lookup"><span data-stu-id="b65f4-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="b65f4-123">Lá você pode usar Olá Olá Visual Studio depuração ferramentas (Observação, variáveis, etc.) tootroubleshoot problema.</span><span class="sxs-lookup"><span data-stu-id="b65f4-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b65f4-124">Antes de depurar, ser toocheck se **exceções do Common Language Runtime** na janela de configurações de exceção de saudação (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="b65f4-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Configuração do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="b65f4-126">Pressione **F5** toorun código de code-behind de saudação.</span><span class="sxs-lookup"><span data-stu-id="b65f4-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="b65f4-127">Ele será executado até que seja interrompido por uma exceção.</span><span class="sxs-lookup"><span data-stu-id="b65f4-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="b65f4-128">Olá abrir `ADLTool_Codebehind.usql.cs` arquivo e defina pontos de interrupção, em seguida, pressione **F5** código de saudação toodebug passo a passo.</span><span class="sxs-lookup"><span data-stu-id="b65f4-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Exceção de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="b65f4-130">Depurar trabalho em falha com assemblies</span><span class="sxs-lookup"><span data-stu-id="b65f4-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="b65f4-131">Se você usar assemblies registrados em seu script U-SQL, o sistema de saudação não é possível obter código-fonte Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b65f4-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="b65f4-132">Nesse caso, adicione manualmente fonte código arquivos toohello solução os assemblies da saudação.</span><span class="sxs-lookup"><span data-stu-id="b65f4-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="b65f4-133">Configurar a solução de saudação</span><span class="sxs-lookup"><span data-stu-id="b65f4-133">Configure hello solution</span></span>

1. <span data-ttu-id="b65f4-134">Clique com botão direito **solução 'VertexDebug' > Adicionar > projeto existente...**  toofind Olá código-fonte dos assemblies e adicione Olá projeto toohello solução de depuração.</span><span class="sxs-lookup"><span data-stu-id="b65f4-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Adicionar projeto de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="b65f4-136">Clique com botão direito **LocalVertexHost > propriedades** em Olá Olá solução e cópia **Working Directory** caminho.</span><span class="sxs-lookup"><span data-stu-id="b65f4-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="b65f4-137">Clique com botão direito **projeto de código de origem do assembly > propriedades**, selecione Olá **criar** guia à esquerda e, em seguida, cole o caminho de saudação copiado como **saída > caminho de saída**.</span><span class="sxs-lookup"><span data-stu-id="b65f4-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Definir caminho pdb da depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="b65f4-139">Pressione **Ctrl+Alt+E** e marque **Exceções de Common Language Runtime** na janela Configurações de exceção.</span><span class="sxs-lookup"><span data-stu-id="b65f4-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="b65f4-140">Iniciar depuração</span><span class="sxs-lookup"><span data-stu-id="b65f4-140">Start debug</span></span>

1. <span data-ttu-id="b65f4-141">Clique com botão direito **projeto de código de origem do assembly > recriar** toohello de arquivos. PDB de toooutput `LocalVertexHost` diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b65f4-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="b65f4-142">Pressione **F5** e projeto Olá será executado até que ele seja interrompido por uma exceção.</span><span class="sxs-lookup"><span data-stu-id="b65f4-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="b65f4-143">Você pode ver Olá mensagem de aviso, você pode ignorar com segurança a seguir.</span><span class="sxs-lookup"><span data-stu-id="b65f4-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="b65f4-144">Pode demorar até a tela de depuração de toohello tooa tooget minutos.</span><span class="sxs-lookup"><span data-stu-id="b65f4-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Aviso do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="b65f4-146">Abra o seu código-fonte e definir pontos de interrupção, em seguida, pressione **F5** código de saudação toodebug passo a passo.</span><span class="sxs-lookup"><span data-stu-id="b65f4-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="b65f4-147">Você também pode usar Olá Visual Studio depuração ferramentas (Observação, variáveis, etc.) tootroubleshoot Olá problema.</span><span class="sxs-lookup"><span data-stu-id="b65f4-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b65f4-148">Recompile o projeto de código de origem do assembly hello cada vez depois de modificar arquivos. PDB do hello código toogenerate atualizado.</span><span class="sxs-lookup"><span data-stu-id="b65f4-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="b65f4-149">Após a depuração, se o projeto de saudação for concluído com êxito Olá a janela de saída mostra Olá a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="b65f4-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Depuração do U-SQL do Azure Data Lake Analytics bem sucedida](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="b65f4-151">Envie novamente o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="b65f4-151">Resubmit hello job</span></span>

<span data-ttu-id="b65f4-152">Depois de concluir a depuração, reenvie o trabalho com falha hello.</span><span class="sxs-lookup"><span data-stu-id="b65f4-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="b65f4-153">Para trabalhos com as soluções de lógica, copie seu código c# em um arquivo de origem do code-behind de saudação (geralmente `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="b65f4-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="b65f4-154">Para trabalhos com assemblies, registre Olá atualizado. dll assemblies no banco de dados ADLA:</span><span class="sxs-lookup"><span data-stu-id="b65f4-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="b65f4-155">No Gerenciador de servidores ou Cloud Explorer, expanda Olá **conta ADLA > bancos de dados** nó.</span><span class="sxs-lookup"><span data-stu-id="b65f4-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="b65f4-156">Clique com botão direito **Assemblies** e registrar seus novos assemblies. dll com o banco de dados do hello ADLA: ![depuração da análise Azure Data Lake U-SQL registrar o assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="b65f4-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="b65f4-157">Reenvie o trabalho.</span><span class="sxs-lookup"><span data-stu-id="b65f4-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b65f4-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b65f4-158">Next steps</span></span>

- [<span data-ttu-id="b65f4-159">Guia de programação do U-SQL</span><span class="sxs-lookup"><span data-stu-id="b65f4-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="b65f4-160">Desenvolver operadores do U-SQL definidos pelo usuário para trabalhos do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b65f4-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="b65f4-161">Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b65f4-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
