---
title: "Ferramentas do Azure Data Lake: execução local e depuração local do U-SQL com o Visual Studio Code | Microsoft Docs"
description: "Saiba como depurar toouse Azure Data Lake Tools para toolocal de código do Visual Studio, executar e local."
Keywords: "O VScode, ferramentas do Azure Data Lake, execução, depuração Local, locais de depuração, visualizar o arquivo de armazenamento, Local carregar toostorage caminho"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="66241-104">Execução local e depuração local do U-SQL com o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="66241-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66241-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66241-105">Prerequisites</span></span>
<span data-ttu-id="66241-106">Certifique-se de que ter Olá pré-requisitos no local a seguir antes de começar estes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="66241-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="66241-107">Ferramenta do Azure Data Lake para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="66241-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="66241-108">Para obter instruções, veja [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="66241-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="66241-109">C# para o código do Visual Studio (se você deseja depurar local tooperform um U-SQL).</span><span class="sxs-lookup"><span data-stu-id="66241-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Instalar o C# nas Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="66241-111">Olá execução local U-SQL e recursos de depuração atualmente oferecem suporte apenas aos usuários do Windows.</span><span class="sxs-lookup"><span data-stu-id="66241-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="66241-112">Configurar o ambiente de execução local Olá U-SQL</span><span class="sxs-lookup"><span data-stu-id="66241-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="66241-113">Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: baixar LocalRun dependência** pacotes de saudação do toodownload.</span><span class="sxs-lookup"><span data-stu-id="66241-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Baixe os pacotes de dependência de LocalRun publicitário Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="66241-115">Localize os pacotes de dependência de saudação do caminho Olá mostrado no hello **saída** painel e, em seguida, instalar BuildTools e Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="66241-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="66241-116">Aqui está um caminho de exemplo:</span><span class="sxs-lookup"><span data-stu-id="66241-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="66241-117">![Localize os pacotes de dependência Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="66241-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="66241-118">a.</span><span class="sxs-lookup"><span data-stu-id="66241-118">a.</span></span> <span data-ttu-id="66241-119">tooinstall BuildTools, siga as instruções do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="66241-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Instalar BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="66241-121">b.</span><span class="sxs-lookup"><span data-stu-id="66241-121">b.</span></span> <span data-ttu-id="66241-122">tooinstall Win10SDK 10240, siga as instruções do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="66241-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Instalar Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="66241-124">Defina variável de ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="66241-124">Set up hello environment variable.</span></span> <span data-ttu-id="66241-125">Saudação de conjunto **SCOPE_CPP_SDK** variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="66241-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="66241-126">Reinicie Olá SO toomake-se de que as configurações de variável de ambiente de saudação entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="66241-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Certifique-se a variável de ambiente SCOPE_CPP_SDK hello está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="66241-128">Iniciar serviço de execução local hello e enviar a conta local do hello U-SQL trabalho tooa</span><span class="sxs-lookup"><span data-stu-id="66241-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="66241-129">Para o usuário pela primeira vez hello, você está Olá toodownload solicitadas publicitário: dependência de LocalRun baixar pacotes se eles não ainda estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="66241-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="66241-130">Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: Iniciar serviço de execução Local**.</span><span class="sxs-lookup"><span data-stu-id="66241-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="66241-131">Selecione **aceitar** tooaccept Olá Microsoft Software License Terms para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="66241-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Aceitar Olá Microsoft Software License Terms](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="66241-133">Olá cmd console será aberto.</span><span class="sxs-lookup"><span data-stu-id="66241-133">hello cmd console opens.</span></span> <span data-ttu-id="66241-134">Para usuários pela primeira vez, você precisa tooenter **3**e, em seguida, localize o caminho de pasta local Olá para seus dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="66241-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="66241-135">Para outras opções, você pode usar valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="66241-135">For other options, you can use hello default values.</span></span> 

   ![Ferramentas do Data Lake para Visual Studio Code cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="66241-137">Selecione a paleta de comando Ctrl + Shift + P tooopen hello, digite **publicitário: Enviar trabalho**e, em seguida, selecione **Local** conta local do tooyour toosubmit Olá trabalho.</span><span class="sxs-lookup"><span data-stu-id="66241-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Ferramentas do Data Lake para Visual Studio Code selecionar local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="66241-139">Depois de enviar o trabalho de saudação, você pode exibir detalhes de envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="66241-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="66241-140">Selecione de detalhes do envio de saudação tooview **jobUrl** em Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="66241-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="66241-141">Você também pode exibir o status de envio de trabalho de saudação do console de cmd hello.</span><span class="sxs-lookup"><span data-stu-id="66241-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="66241-142">Digite **7** no console de cmd Olá se você quiser tooknow mais detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="66241-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="66241-143">![Ferramentas do Data Lake para Visual Studio Code saída de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Ferramentas do Data Lake para Visual Studio Code status do cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="66241-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="66241-144">Iniciar uma depuração local de trabalho do hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="66241-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="66241-145">Para o usuário pela primeira vez hello, você está Olá toodownload solicitadas publicitário: dependência de LocalRun baixar pacotes se eles não ainda estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="66241-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="66241-146">Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: Iniciar serviço de execução Local**.</span><span class="sxs-lookup"><span data-stu-id="66241-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="66241-147">Olá cmd console será aberto.</span><span class="sxs-lookup"><span data-stu-id="66241-147">hello cmd console opens.</span></span> <span data-ttu-id="66241-148">Certifique-se de que Olá **DataRoot** está definido.</span><span class="sxs-lookup"><span data-stu-id="66241-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="66241-149">Defina um ponto de interrupção no code-behind do C#.</span><span class="sxs-lookup"><span data-stu-id="66241-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="66241-150">No editor de script hello, selecione o console de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **depuração Local** toostart seu serviço de depuração local.</span><span class="sxs-lookup"><span data-stu-id="66241-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Ferramentas do Data Lake para Visual Studio Code resultado da depuração local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="66241-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66241-152">Next steps</span></span>
- <span data-ttu-id="66241-153">Para usar as Ferramentas do Azure Data Lake para Visual Studio Code, confira [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="66241-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="66241-154">Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="66241-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="66241-155">Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66241-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="66241-156">Para obter informações sobre como desenvolver assemblies hello, consulte [assemblies desenvolver U-SQL para trabalhos de análise do Azure Data Lake](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="66241-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
