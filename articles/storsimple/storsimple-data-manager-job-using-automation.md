---
title: "tootrigger de automação do Azure aaaUse um trabalho | Microsoft Docs"
description: "Saiba como toouse automação do Azure para o disparo de trabalhos do Gerenciador de dados do StorSimple (visualização particular)"
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="09de9-103">Usar a automação do Azure tootrigger um trabalho (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="09de9-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="09de9-104">Este artigo descreve como tootrigger de automação do Azure toouse um trabalho de Data do StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="09de9-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09de9-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="09de9-105">Prerequisites</span></span>

<span data-ttu-id="09de9-106">Antes de começar, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="09de9-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="09de9-107">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="09de9-107">Azure Powershell installed.</span></span> <span data-ttu-id="09de9-108">[Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="09de9-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="09de9-109">Configuração tooinitialize Olá transformação de dados trabalho de configurações (instruções tooobtain essas configurações são incluídas aqui).</span><span class="sxs-lookup"><span data-stu-id="09de9-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="09de9-110">Uma definição de trabalho que foi configurada corretamente em um Recurso de Dados Híbridos dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09de9-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="09de9-111">Baixar `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) arquivo de repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="09de9-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="09de9-112">Baixar `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) do repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="09de9-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="09de9-113">Baixar `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) do repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="09de9-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="09de9-114">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="09de9-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="09de9-115">Obter as permissões do Active Directory do Azure de definição de trabalho de Olá Olá automação trabalho toorun</span><span class="sxs-lookup"><span data-stu-id="09de9-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="09de9-116">parâmetros de configuração de saudação tooretrieve para Active Directory, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="09de9-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="09de9-117">Abra o Windows PowerShell no computador local.</span><span class="sxs-lookup"><span data-stu-id="09de9-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="09de9-118">Verifique se o [Azure PowerShell](https://azure.microsoft.com/downloads/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="09de9-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="09de9-119">Executar Olá `Get-ConfigurationParams.ps1` script (na pasta Olá baixado anteriormente).</span><span class="sxs-lookup"><span data-stu-id="09de9-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="09de9-120">Digite hello comando na janela do PowerShell Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="09de9-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="09de9-121">Olá ActiveDirectoryKey é uma senha que você pode usar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="09de9-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="09de9-122">Insira uma senha de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="09de9-122">Enter a password of your choice.</span></span> <span data-ttu-id="09de9-123">AppName pode ser qualquer cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="09de9-123">AppName can be any string.</span></span>

2. <span data-ttu-id="09de9-124">Esse script gera Olá valores que devem ser usados ao disparar Olá runbook de automação a seguir.</span><span class="sxs-lookup"><span data-stu-id="09de9-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="09de9-125">Anote esses valores.</span><span class="sxs-lookup"><span data-stu-id="09de9-125">Make a note of these values.</span></span>

    - <span data-ttu-id="09de9-126">Id do Cliente</span><span class="sxs-lookup"><span data-stu-id="09de9-126">Client ID</span></span>
    - <span data-ttu-id="09de9-127">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="09de9-127">Tenant ID</span></span>
    - <span data-ttu-id="09de9-128">Chave de diretório ativo (mesmo que Olá fornecido acima)</span><span class="sxs-lookup"><span data-stu-id="09de9-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="09de9-129">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="09de9-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="09de9-130">Configurar a conta de automação de saudação</span><span class="sxs-lookup"><span data-stu-id="09de9-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="09de9-131">Faça logon em tooAzure e abra sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="09de9-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="09de9-132">Clique em **ativos** bloco tooopen Olá lista de ativos.</span><span class="sxs-lookup"><span data-stu-id="09de9-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="09de9-133">Clique em **módulos** bloco tooopen Olá lista de módulos.</span><span class="sxs-lookup"><span data-stu-id="09de9-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="09de9-134">Clique em **+ adicionar um módulo** botão e hello folha de módulo de adicionar é iniciada.</span><span class="sxs-lookup"><span data-stu-id="09de9-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="09de9-136">Depois que você selecionou Olá `DataTransformationApp.zip` de arquivos do computador local, clique em **Okey** tooimport módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09de9-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="09de9-137">Quando a automação do Azure importa uma conta de tooyour do módulo, ele extrai metadados sobre o módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09de9-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="09de9-138">Essa operação pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="09de9-138">This operation may take a couple of minutes.</span></span>

   ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="09de9-140">Você receberá uma notificação que o módulo hello está sendo implantado e outra notificação quando Olá processo for concluído.</span><span class="sxs-lookup"><span data-stu-id="09de9-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="09de9-141">Você também pode verificar o status de saudação **módulos** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="09de9-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="09de9-142">tooimport Olá runbook que dispara a definição de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="09de9-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="09de9-143">No portal do Azure de Olá, abra sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="09de9-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="09de9-144">Clique em **Runbooks** bloco tooopen Olá lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="09de9-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="09de9-145">Clique em **+ Adicionar um runbook** e, em seguida, em **Importar um runbook existente**.</span><span class="sxs-lookup"><span data-stu-id="09de9-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importar um runbook existente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="09de9-147">Clique em **arquivo de Runbook** e selecione Olá arquivo tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="09de9-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="09de9-148">Clique em **criar** tooimport Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="09de9-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="09de9-149">Olá novo runbook será exibido na lista Olá runbooks para Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="09de9-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="09de9-150">Clique no runbook **Trigger-DataTransformation-Job** e, em seguida, em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="09de9-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="09de9-151">Clique em **Publicar** e em **Sim** quando solicitado para confirmação.</span><span class="sxs-lookup"><span data-stu-id="09de9-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="09de9-152">toorun Olá runbook:</span><span class="sxs-lookup"><span data-stu-id="09de9-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="09de9-153">No portal do Azure de Olá, abra sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="09de9-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="09de9-154">Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="09de9-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="09de9-155">Clique em **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="09de9-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="09de9-156">Clique em **iniciar** toostart Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="09de9-156">Click **Start** toostart hello runbook.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="09de9-158">Em Olá **iniciar runbook** folha, insira todos os parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="09de9-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="09de9-159">Clique em **Okey** toosubmit trabalho de transformação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="09de9-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="09de9-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09de9-161">Next steps</span></span>

<span data-ttu-id="09de9-162">[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="09de9-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
