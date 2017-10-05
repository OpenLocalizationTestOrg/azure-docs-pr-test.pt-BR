---
title: "Usar a Automação do Azure para disparar um trabalho | Microsoft Docs"
description: "Saiba como usar a Automação do Azure para disparar trabalhos do StorSimple Data Manager (versão prévia particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="16680-103">Usar a Automação do Azure para disparar um trabalho (Versão prévia particular)</span><span class="sxs-lookup"><span data-stu-id="16680-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="16680-104">Este artigo descreve como usar a Automação do Azure para disparar um trabalho do StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="16680-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16680-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="16680-105">Prerequisites</span></span>

<span data-ttu-id="16680-106">Antes de começar, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="16680-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="16680-107">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="16680-107">Azure Powershell installed.</span></span> <span data-ttu-id="16680-108">[Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="16680-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="16680-109">Definições de configuração para inicializar o trabalho de Transformação de Dados (as instruções para obter essas configurações estão incluídas aqui).</span><span class="sxs-lookup"><span data-stu-id="16680-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="16680-110">Uma definição de trabalho que foi configurada corretamente em um Recurso de Dados Híbridos dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="16680-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="16680-111">Baixe o arquivo [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) `DataTransformationApp.zip` no repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="16680-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="16680-112">Baixe o [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) `Get-ConfigurationParams.ps1` no repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="16680-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="16680-113">Baixe o [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) `Trigger-DataTransformation-Job.ps1` no repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="16680-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="16680-114">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="16680-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="16680-115">Obter permissões do Azure Active Directory para que o trabalho de automação execute a definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="16680-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="16680-116">Para recuperar os parâmetros de configuração do Active Directory, realize as seguintes as etapas:</span><span class="sxs-lookup"><span data-stu-id="16680-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="16680-117">Abra o Windows PowerShell no computador local.</span><span class="sxs-lookup"><span data-stu-id="16680-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="16680-118">Verifique se o [Azure PowerShell](https://azure.microsoft.com/downloads/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="16680-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="16680-119">Execute o script `Get-ConfigurationParams.ps1` (na pasta baixada acima).</span><span class="sxs-lookup"><span data-stu-id="16680-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="16680-120">Digite o seguinte comando na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="16680-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="16680-121">A ActiveDirectoryKey é uma senha que será usada mais tarde.</span><span class="sxs-lookup"><span data-stu-id="16680-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="16680-122">Insira uma senha de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="16680-122">Enter a password of your choice.</span></span> <span data-ttu-id="16680-123">AppName pode ser qualquer cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="16680-123">AppName can be any string.</span></span>

2. <span data-ttu-id="16680-124">Esse script gera os valores a seguir, que devem ser usados ao disparar o runbook de automação.</span><span class="sxs-lookup"><span data-stu-id="16680-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="16680-125">Anote esses valores.</span><span class="sxs-lookup"><span data-stu-id="16680-125">Make a note of these values.</span></span>

    - <span data-ttu-id="16680-126">Id do Cliente</span><span class="sxs-lookup"><span data-stu-id="16680-126">Client ID</span></span>
    - <span data-ttu-id="16680-127">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="16680-127">Tenant ID</span></span>
    - <span data-ttu-id="16680-128">Chave do Active Directory (a mesma inserida acima)</span><span class="sxs-lookup"><span data-stu-id="16680-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="16680-129">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="16680-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="16680-130">Configurar a conta de automação</span><span class="sxs-lookup"><span data-stu-id="16680-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="16680-131">Faça logon no Azure e abra sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="16680-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="16680-132">Clique no bloco **Ativos** para abrir a lista de ativos.</span><span class="sxs-lookup"><span data-stu-id="16680-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="16680-133">Clique no bloco **Módulos** para abrir a lista de módulos.</span><span class="sxs-lookup"><span data-stu-id="16680-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="16680-134">Clique no botão **+ Adicionar um módulo** e a folha Adicionar módulo é iniciada.</span><span class="sxs-lookup"><span data-stu-id="16680-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="16680-136">Depois de selecionar o arquivo `DataTransformationApp.zip` no computador local, clique em **OK** para importar o módulo.</span><span class="sxs-lookup"><span data-stu-id="16680-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="16680-137">Quando a Automação do Azure importa um módulo para sua conta, ele extrai os metadados sobre o módulo.</span><span class="sxs-lookup"><span data-stu-id="16680-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="16680-138">Essa operação pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="16680-138">This operation may take a couple of minutes.</span></span>

   ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="16680-140">Você recebe uma notificação informando que o módulo está sendo implantado e outra notificação quando o processo é concluído.</span><span class="sxs-lookup"><span data-stu-id="16680-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="16680-141">Você também pode verificar o status no bloco **Módulos**.</span><span class="sxs-lookup"><span data-stu-id="16680-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="16680-142">Para importar o runbook que dispara a definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="16680-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="16680-143">No portal do Azure, abra sua conta da Automação.</span><span class="sxs-lookup"><span data-stu-id="16680-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="16680-144">Clique no bloco **Runbooks** para abrir a lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="16680-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="16680-145">Clique em **+ Adicionar um runbook** e, em seguida, em **Importar um runbook existente**.</span><span class="sxs-lookup"><span data-stu-id="16680-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importar um runbook existente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="16680-147">Clique em **Arquivo de runbook** para selecionar o arquivo para importar `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="16680-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="16680-148">Clique em **Criar** para importar o runbook.</span><span class="sxs-lookup"><span data-stu-id="16680-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="16680-149">O novo runbook é exibido na lista de runbooks da conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="16680-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="16680-150">Clique no runbook **Trigger-DataTransformation-Job** e, em seguida, em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="16680-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="16680-151">Clique em **Publicar** e em **Sim** quando solicitado para confirmação.</span><span class="sxs-lookup"><span data-stu-id="16680-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="16680-152">Para executar o runbook:</span><span class="sxs-lookup"><span data-stu-id="16680-152">To run the runbook:</span></span>
1. <span data-ttu-id="16680-153">No portal do Azure, abra sua conta da Automação.</span><span class="sxs-lookup"><span data-stu-id="16680-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="16680-154">Clique no bloco **Runbooks** para abrir a lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="16680-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="16680-155">Clique em **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="16680-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="16680-156">Clique em **Iniciar** para iniciar o runbook.</span><span class="sxs-lookup"><span data-stu-id="16680-156">Click **Start** to start the runbook.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="16680-158">Na folha **Iniciar runbook**, insira todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="16680-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="16680-159">Clique em **OK** para enviar o trabalho de Transformação de Dados.</span><span class="sxs-lookup"><span data-stu-id="16680-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="16680-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16680-161">Next steps</span></span>

<span data-ttu-id="16680-162">[Use a interface do usuário do Gerenciador de Dados StorSimple para transformar seus dados](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="16680-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>