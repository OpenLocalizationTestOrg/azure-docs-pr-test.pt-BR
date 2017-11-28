---
title: "Ferramentas do Azure Data Lake: execução local e depuração local do U-SQL com o Visual Studio Code | Microsoft Docs"
description: "Saiba como usar as Ferramentas do Azure Data Lake para Visual Studio Code na execução local e na depuração local."
Keywords: "VSCode, Ferramentas do Azure Data Lake, Execução local, Depuração local, Depuração Local, visualizar arquivo de armazenamento, carregar no caminho de armazenamento"
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
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="9dd8e-104">Execução local e depuração local do U-SQL com o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9dd8e-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dd8e-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9dd8e-105">Prerequisites</span></span>
<span data-ttu-id="9dd8e-106">Verifique se que você tem os seguintes pré-requisitos em vigor antes de iniciar estes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="9dd8e-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="9dd8e-107">Ferramenta do Azure Data Lake para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="9dd8e-108">Para obter instruções, veja [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="9dd8e-109">C# para Visual Studio Code (se você quiser executar a depuração local do U-SQL).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Instalar o C# nas Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="9dd8e-111">Os recursos de depuração e execução local do U-SQL atualmente dão suporte apenas para usuários do Windows.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="9dd8e-112">Configurar o ambiente de execução local do U-SQL</span><span class="sxs-lookup"><span data-stu-id="9dd8e-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="9dd8e-113">Selecione Ctrl+Shift+P para abrir a paleta de comandos e então insira **ADL: Baixar Dependência LocalRun** para baixar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![Baixar os pacotes de Dependência de LocalRun do ADL](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="9dd8e-115">Localize os pacotes de dependência do caminho mostrado no painel **Saída** abaixo e então instale o BuildTools e o Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="9dd8e-116">Aqui está um caminho de exemplo:</span><span class="sxs-lookup"><span data-stu-id="9dd8e-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="9dd8e-117">![Localizar os pacotes de dependência](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="9dd8e-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="9dd8e-118">a.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-118">a.</span></span> <span data-ttu-id="9dd8e-119">Para instalar BuildTools, siga as instruções do assistente para instalar.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![Instalar BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="9dd8e-121">b.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-121">b.</span></span> <span data-ttu-id="9dd8e-122">Para instalar o Win10SDK 10240, siga as instruções do assistente.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Instalar Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="9dd8e-124">Defina a variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-124">Set up the environment variable.</span></span> <span data-ttu-id="9dd8e-125">Defina a variável de ambiente **SCOPE_CPP_SDK** como:</span><span class="sxs-lookup"><span data-stu-id="9dd8e-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="9dd8e-126">Reinicie o sistema operacional para garantir que as configurações da variável de ambiente entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![Certifique-se de que a variável de ambiente SCOPE_CPP_SDK esteja instalada](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="9dd8e-128">Inicie o serviço de execução local e envie o trabalho U-SQL para uma conta local</span><span class="sxs-lookup"><span data-stu-id="9dd8e-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="9dd8e-129">No primeiro uso, você precisará baixar os pacotes do ADL: Baixar Dependência de LocalRun se eles ainda não estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="9dd8e-130">Pressione Ctrl+Shift+P para abrir a paleta de comandos e digite **ADL: Iniciar Serviço de Execução Local**.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="9dd8e-131">Selecione **Aceito** para aceitar os termos da Licença de Software da Microsoft pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Aceite os Termos de Licença para Software Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="9dd8e-133">O console cmd é aberto.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-133">The cmd console opens.</span></span> <span data-ttu-id="9dd8e-134">Aos usuários de primeira viagem, será necessário inserir **3** e insira um caminho de pasta local para os dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="9dd8e-135">Para outras opções, basta simplesmente usar os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-135">For other options, you can use the default values.</span></span> 

   ![Ferramentas do Data Lake para Visual Studio Code cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="9dd8e-137">Select Ctrl+Shift+P para abrir a paleta de comandos, insira **ADL: Enviar Trabalho** e selecione **Local** para enviar o trabalho para sua conta local.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Ferramentas do Data Lake para Visual Studio Code selecionar local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="9dd8e-139">Depois de enviar o trabalho, você poderá exibir os detalhes de envio.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="9dd8e-140">Para exibir o envio de detalhes, selecione **jobUrl** na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="9dd8e-141">Você também pode exibir o status de envio de trabalho do console do cmd.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="9dd8e-142">Digite **7** no console do cmd se você quiser saber mais detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="9dd8e-143">![Ferramentas do Data Lake para Visual Studio Code saída de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Ferramentas do Data Lake para Visual Studio Code status do cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="9dd8e-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="9dd8e-144">Iniciar uma depuração local para o trabalho de U-SQL</span><span class="sxs-lookup"><span data-stu-id="9dd8e-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="9dd8e-145">No primeiro uso, você precisará baixar os pacotes do ADL: Baixar Dependência de LocalRun se eles ainda não estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="9dd8e-146">Pressione Ctrl+Shift+P para abrir a paleta de comandos e digite **ADL: Iniciar Serviço de Execução Local**.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="9dd8e-147">O console cmd é aberto.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-147">The cmd console opens.</span></span> <span data-ttu-id="9dd8e-148">Verifique se **DataRoot** está definido.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="9dd8e-149">Defina um ponto de interrupção no code-behind do C#.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="9dd8e-150">No editor de script, selecione Ctrl+Shift+P para abrir o console de comando e insira **Depuração Local** para iniciar o serviço de depuração local.</span><span class="sxs-lookup"><span data-stu-id="9dd8e-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Ferramentas do Data Lake para Visual Studio Code resultado da depuração local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="9dd8e-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dd8e-152">Next steps</span></span>
- <span data-ttu-id="9dd8e-153">Para usar as Ferramentas do Azure Data Lake para Visual Studio Code, confira [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="9dd8e-154">Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="9dd8e-155">Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="9dd8e-156">Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="9dd8e-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
