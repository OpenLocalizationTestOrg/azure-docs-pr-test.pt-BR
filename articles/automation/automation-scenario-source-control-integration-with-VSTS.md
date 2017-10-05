---
title: "Integrar a automação do Azure com o controle do código-fonte do Visual Studio Team Services | Microsoft Docs"
description: "O cenário guia você pela configuração de integração com uma conta de Automação do Azure e o controle do código-fonte do Visual Studio Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "Azure PowerShell, VSTS, controle do código-fonte, automação"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="6bbf1-104">Cenário da Automação do Azure – Integração de controle do código-fonte da Automação com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6bbf1-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="6bbf1-105">Nesse cenário, você tem um projeto do Visual Studio Team Services que você está usando para gerenciar runbooks da Automação do Azure ou configurações do DSC sob o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="6bbf1-106">Este artigo descreve como integrar o VSTS em seu ambiente de Automação do Azure para que ocorra a integração contínua ocorra para cada check-in.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="6bbf1-107">Obtendo o cenário</span><span class="sxs-lookup"><span data-stu-id="6bbf1-107">Getting the scenario</span></span>

<span data-ttu-id="6bbf1-108">Este cenário é composto por dois runbooks do PowerShell que você pode importar diretamente da [Galeria de Runbooks](automation-runbook-gallery.md) no Portal do Azure, ou baixar da [Galeria do PowerShell](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="6bbf1-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="6bbf1-109">Runbooks</span><span class="sxs-lookup"><span data-stu-id="6bbf1-109">Runbooks</span></span>

<span data-ttu-id="6bbf1-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="6bbf1-110">Runbook</span></span> | <span data-ttu-id="6bbf1-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bbf1-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="6bbf1-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="6bbf1-112">Sync-VSTS</span></span> | <span data-ttu-id="6bbf1-113">Importar runbooks ou configurações do controle do código-fonte do VSTS quando é feito um check-in.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="6bbf1-114">Se executado manualmente, ele importará e publicará todos os runbooks ou configurações para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="6bbf1-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="6bbf1-115">Sync-VSTSGit</span></span> | <span data-ttu-id="6bbf1-116">Importar runbooks ou configurações do controle do código-fonte do VSTS sob o Git quando é feito um check-in.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="6bbf1-117">Se executado manualmente, ele importará e publicará todos os runbooks ou configurações para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="6bbf1-118">variáveis</span><span class="sxs-lookup"><span data-stu-id="6bbf1-118">Variables</span></span>

<span data-ttu-id="6bbf1-119">Variável</span><span class="sxs-lookup"><span data-stu-id="6bbf1-119">Variable</span></span> | <span data-ttu-id="6bbf1-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bbf1-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="6bbf1-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="6bbf1-121">VSToken</span></span> | <span data-ttu-id="6bbf1-122">Ativo de variável segura que você criará e que contém o token de acesso pessoal do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="6bbf1-123">Você pode aprender como criar um token de acesso pessoal do VSTS na [página de autenticação do VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span><span class="sxs-lookup"><span data-stu-id="6bbf1-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="6bbf1-124">Instalando e configurando esse cenário</span><span class="sxs-lookup"><span data-stu-id="6bbf1-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="6bbf1-125">Criar um [token de acesso pessoal](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) no VSTS que será usado para sincronizar runbooks ou configurações em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="6bbf1-126">Criar uma [variável segura](automation-variables.md) na sua conta de automação para armazenar o token de acesso pessoal para que o runbook possa autenticar o VSTS e sincronizar os runbooks ou configurações na conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="6bbf1-127">Você pode nomear esse VSToken.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="6bbf1-128">Importe o runbook que sincronizará seus runbooks ou configurações para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="6bbf1-129">Você pode usar o [runbook de exemplo do VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) ou o [runbook de exemplo do VSTS com Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com dependendo de você usar o controle do código-fonte do VSTS ou VSTS com Git e implantar a sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="6bbf1-130">Agora você pode [publicar](automation-creating-importing-runbook.md#publishing-a-runbook) esse runbook para que você possa criar um webhook.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="6bbf1-131">Criar um [webhook](automation-webhooks.md) para este runbook Sync-VSTS e preencha os parâmetros conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="6bbf1-132">Certifique-se de copiar a URL do webhook, pois você precisará dela para um gancho de serviço no VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="6bbf1-133">O VSAccessTokenVariableName é o nome (VSToken) da variável segura que você criou anteriormente para conter o token de acesso pessoal.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="6bbf1-134">A integração com o VSTS (Sync-VSTS.ps1) utilizará os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="6bbf1-135">Parâmetros do Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="6bbf1-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="6bbf1-136">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6bbf1-136">Parameter</span></span> | <span data-ttu-id="6bbf1-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bbf1-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="6bbf1-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="6bbf1-138">WebhookData</span></span> | <span data-ttu-id="6bbf1-139">Isso conterá as informações de check-in enviadas do gancho de serviço do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="6bbf1-140">Você deve deixar esse parâmetro em branco.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="6bbf1-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6bbf1-141">ResourceGroup</span></span> | <span data-ttu-id="6bbf1-142">Esse é o nome do grupo de recursos em que a conta de automação está contida.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="6bbf1-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="6bbf1-143">AutomationAccountName</span></span> | <span data-ttu-id="6bbf1-144">O nome da conta de automação que será sincronizada com o VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="6bbf1-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="6bbf1-145">VSFolder</span></span> | <span data-ttu-id="6bbf1-146">O nome da pasta do VSTS em que os runbooks e as configurações existem.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="6bbf1-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="6bbf1-147">VSAccount</span></span> | <span data-ttu-id="6bbf1-148">O nome da conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="6bbf1-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="6bbf1-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="6bbf1-150">O nome da variável segura (VSToken) que contém o token de acesso pessoal do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="6bbf1-151">Se você estiver usando o VSTS com GIT (Sync-VSTSGit.ps1), ele utilizará os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="6bbf1-152">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6bbf1-152">Parameter</span></span> | <span data-ttu-id="6bbf1-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bbf1-153">Description</span></span>|
--------|------------|
<span data-ttu-id="6bbf1-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="6bbf1-154">WebhookData</span></span> | <span data-ttu-id="6bbf1-155">Isso conterá as informações de check-in enviadas do gancho de serviço do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="6bbf1-156">Você deve deixar esse parâmetro em branco.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="6bbf1-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6bbf1-157">ResourceGroup</span></span> | <span data-ttu-id="6bbf1-158">Esse é o nome do grupo de recursos em que a conta de automação está contida.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="6bbf1-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="6bbf1-159">AutomationAccountName</span></span> | <span data-ttu-id="6bbf1-160">O nome da conta de automação que será sincronizada com o VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="6bbf1-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="6bbf1-161">VSAccount</span></span> | <span data-ttu-id="6bbf1-162">O nome da conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="6bbf1-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="6bbf1-163">VSProject</span></span> | <span data-ttu-id="6bbf1-164">O nome do projeto no VSTS em que os runbooks e as configurações existem.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="6bbf1-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="6bbf1-165">GitRepo</span></span> | <span data-ttu-id="6bbf1-166">O nome do repositório Git.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-166">The name of the Git repository.</span></span>|
<span data-ttu-id="6bbf1-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="6bbf1-167">GitBranch</span></span> | <span data-ttu-id="6bbf1-168">O nome da ramificação no repositório Git do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="6bbf1-169">Pasta</span><span class="sxs-lookup"><span data-stu-id="6bbf1-169">Folder</span></span> | <span data-ttu-id="6bbf1-170">O nome da pasta na ramificação Git do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="6bbf1-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="6bbf1-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="6bbf1-172">O nome da variável segura (VSToken) que contém o token de acesso pessoal do VSTS.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="6bbf1-173">Crie um gancho de serviço no VSTS para check-ins para a pasta que dispara esse webhook no check-in de código.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="6bbf1-174">Selecione WebHooks como o serviço com o qual se integrar ao criar uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="6bbf1-175">Você pode aprender mais sobre os ganchos de serviço na [documentação de ganchos de serviço do VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span><span class="sxs-lookup"><span data-stu-id="6bbf1-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="6bbf1-176">Agora você deve ser capaz de fazer todos os check-ins de runbooks e configurações no VSTS e sincronizá-los automaticamente em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="6bbf1-177">Se você executar esse runbook manualmente sem ser disparado pelo VSTS, você poderá deixar o parâmetro webhookdata vazio e ele fará uma sincronização completa da pasta do VSTS especificada.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="6bbf1-178">Se você deseja desinstalar o cenário, remova o gancho de serviço do VSTS, exclua o runbook e a variável VSToken.</span><span class="sxs-lookup"><span data-stu-id="6bbf1-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>
