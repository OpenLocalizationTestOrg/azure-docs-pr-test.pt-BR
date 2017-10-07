---
title: "aaaCollecting dados de análise de Log com um runbook na automação do Azure | Microsoft Docs"
description: "Tutorial passo a passo que explica como criar um runbook em dados de toocollect de automação do Azure no repositório do OMS Olá para análise pela análise de Log."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="9ecb5-103">Coletar dados no Log Analytics com um runbook na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb5-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="9ecb5-104">Você pode coletar uma quantidade significativa de dados no Log Analytics de uma variedade de fontes, inclusive [fontes de dados](../log-analytics/log-analytics-data-sources.md) nos agentes e também os [dados coletados do Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="9ecb5-105">Há um cenários que onde você precisa toocollect dados que não está acessível por meio dessas fontes padrão.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="9ecb5-106">Nesses casos, você pode usar o hello [API do coletor de dados de HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite dados tooLog análise de qualquer cliente de API REST.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="9ecb5-107">Um tooperform método comuns coleta de dados está usando um runbook na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="9ecb5-108">Este tutorial orienta pelo processo de saudação para criar e agendar um runbook na automação do Azure toowrite dados tooLog análise.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9ecb5-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ecb5-109">Prerequisites</span></span>
<span data-ttu-id="9ecb5-110">Esse cenário requer Olá seguindo os recursos configurados em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="9ecb5-111">Ambos podem ser uma conta gratuita.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-111">Both can be a free account.</span></span>

- <span data-ttu-id="9ecb5-112">[Espaço de trabalho do Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="9ecb5-113">[Conta de automação do Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="9ecb5-114">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="9ecb5-114">Overview of scenario</span></span>
<span data-ttu-id="9ecb5-115">Para este tutorial, você escreverá um runbook que coleta informações sobre trabalhos de Automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="9ecb5-116">Runbooks na automação do Azure são implementados com o PowerShell, portanto, comece por escrever e testar um script no editor de automação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="9ecb5-117">Depois de confirmar que você está coletando informações de saudação necessárias, você gravar que tooLog dados análise e verifique se o tipo de dados personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="9ecb5-118">Por fim, você criará um runbook de saudação do agendamento toostart em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="9ecb5-119">Você pode configurar a automação do Azure toosend trabalho informações tooLog análise sem este runbook.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="9ecb5-120">Este cenário é principalmente tutorial de saudação toosupport usado e é recomendável que você envie o espaço de trabalho de teste do hello dados tooa.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="9ecb5-121">1. Instalar o módulo de API do Coletor de Dados</span><span class="sxs-lookup"><span data-stu-id="9ecb5-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="9ecb5-122">Cada [solicitação de saudação API de coletor de dados HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) devem ser formatados adequadamente e incluir um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="9ecb5-123">Você pode fazer isso no seu runbook, mas você pode reduzir a quantidade de saudação do código necessário usando um módulo que simplifica esse processo.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="9ecb5-124">É um módulo que você pode usar [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) no hello Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="9ecb5-125">toouse um [módulo](../automation/automation-integration-modules.md) em um runbook, ele deve ser instalado em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="9ecb5-126">Qualquer runbook no Olá a mesma conta pode usar Olá funções no módulo hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="9ecb5-127">Você pode instalar um novo módulo selecionando **Ativos** > **Módulos** > **Adicionar um módulo** na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="9ecb5-128">Olá Galeria do PowerShell que lhe toodeploy uma opção rapidamente um módulo diretamente a conta de automação tooyour, portanto você pode usar essa opção para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="9ecb5-130">Vá muito[Galeria do PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="9ecb5-131">Procure **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="9ecb5-132">Clique em Olá **implantar tooAzure automação** botão.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="9ecb5-133">Selecione sua conta de automação e clique em **Okey** tooinstall módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="9ecb5-134">2. Criar variáveis de Automação</span><span class="sxs-lookup"><span data-stu-id="9ecb5-134">2. Create Automation variables</span></span>
<span data-ttu-id="9ecb5-135">As [variáveis de Automação](..\automation\automation-variables.md) contêm valores que podem ser usados por todos os runbooks na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="9ecb5-136">Eles tornarem runbooks mais flexível, permitindo que você toochange esses valores sem editar Olá runbook real.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="9ecb5-137">Todas as solicitações de saudação API do coletor de dados de HTTP requer Olá ID e a chave do espaço de trabalho do OMS hello e ativos de variável são toostore ideal essas informações.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![variáveis](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="9ecb5-139">No portal do Azure de Olá, navegue tooyour conta de automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="9ecb5-140">Selecione **Variáveis** em **Recursos Compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="9ecb5-141">Clique em **adicionar uma variável** e criar hello duas variáveis no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="9ecb5-142">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9ecb5-142">Property</span></span> | <span data-ttu-id="9ecb5-143">Valor da ID do Espaço de Trabalho</span><span class="sxs-lookup"><span data-stu-id="9ecb5-143">Workspace ID Value</span></span> | <span data-ttu-id="9ecb5-144">Valor da Chave do Espaço de Trabalho</span><span class="sxs-lookup"><span data-stu-id="9ecb5-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="9ecb5-145">Nome</span><span class="sxs-lookup"><span data-stu-id="9ecb5-145">Name</span></span> | <span data-ttu-id="9ecb5-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="9ecb5-146">WorkspaceId</span></span> | <span data-ttu-id="9ecb5-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="9ecb5-147">WorkspaceKey</span></span> |
| <span data-ttu-id="9ecb5-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="9ecb5-148">Type</span></span> | <span data-ttu-id="9ecb5-149">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9ecb5-149">String</span></span> | <span data-ttu-id="9ecb5-150">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9ecb5-150">String</span></span> |
| <span data-ttu-id="9ecb5-151">Valor</span><span class="sxs-lookup"><span data-stu-id="9ecb5-151">Value</span></span> | <span data-ttu-id="9ecb5-152">Cole Olá ID do espaço de trabalho do seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="9ecb5-153">Colar com hello primário ou secundário chave de seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="9ecb5-154">Criptografado</span><span class="sxs-lookup"><span data-stu-id="9ecb5-154">Encrypted</span></span> | <span data-ttu-id="9ecb5-155">Não</span><span class="sxs-lookup"><span data-stu-id="9ecb5-155">No</span></span> | <span data-ttu-id="9ecb5-156">Sim</span><span class="sxs-lookup"><span data-stu-id="9ecb5-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="9ecb5-157">3. Criar runbook</span><span class="sxs-lookup"><span data-stu-id="9ecb5-157">3. Create runbook</span></span>

<span data-ttu-id="9ecb5-158">Automação do Azure tem um editor no portal de saudação onde você pode editar e testar seu runbook.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="9ecb5-159">Você tem Olá opção toouse Olá script editor toowork com [PowerShell diretamente](../automation/automation-edit-textual-runbook.md) ou [criar um runbook gráfico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="9ecb5-160">Para este tutorial, você trabalhará com um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Editar runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="9ecb5-162">Navegue tooyour conta de automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="9ecb5-163">Clique em **Runbooks** > **Adicionar um runbook** > **Criar um novo runbook**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="9ecb5-164">Nome de runbook hello, digite **trabalhos de automação de coletar**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="9ecb5-165">Para o tipo de runbook hello, selecione **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="9ecb5-166">Clique em **criar** toocreate Olá runbook e início saudação do editor.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="9ecb5-167">Copie e cole a saudação de código a seguir no runbook hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="9ecb5-168">Consulte toohello comentários no script hello explicação do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="9ecb5-169">4. Runbook de teste</span><span class="sxs-lookup"><span data-stu-id="9ecb5-169">4. Test runbook</span></span>
<span data-ttu-id="9ecb5-170">Automação do Azure inclui um ambiente muito[testar seu runbook](../automation/automation-testing-runbook.md) antes de publicá-lo.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="9ecb5-171">Você pode inspecionar dados Olá coletados pelo runbook hello e verificar que ele grava tooLog análise conforme o esperado antes de publicá-la tooproduction.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Runbook de teste](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="9ecb5-173">Clique em **salvar** toosave Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="9ecb5-174">Clique em **painel teste** tooopen Olá runbook no ambiente de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="9ecb5-175">Desde que o runbook tiver parâmetros, você está tooenter solicitadas valores para eles.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="9ecb5-176">Digite nome Olá Olá do grupo de recursos e automação Olá que seu andamento toocollect trabalho informações de conta.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="9ecb5-177">Clique em **iniciar** toohello iniciar runbook hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="9ecb5-178">Olá runbook iniciará com um status de **em fila** antes que ele fique muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="9ecb5-179">Olá runbook deve exibir a saída detalhada com trabalhos Olá coletados no formato json.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="9ecb5-180">Se nenhum trabalho estiver listado, em seguida, não pode ter havido nenhuma trabalhos criados na conta de automação de saudação em Olá última hora.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="9ecb5-181">Tente iniciar qualquer runbook na conta de automação hello e execute novamente o teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="9ecb5-182">Certifique-se de que o saída Olá não mostra que erros Olá lançar tooLog comando análise.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="9ecb5-183">Você deve ter uma mensagem semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-183">You should have a message similar toohello following.</span></span>

    ![Saída de postagem](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="9ecb5-185">5. Verificar registros no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9ecb5-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="9ecb5-186">Depois de runbook Olá foi concluída no teste e verificar a saída de hello foi recebida com êxito, você pode verificar se os registros de saudação foram criados usando um [pesquisa de log de análise de Log](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Saída de log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="9ecb5-188">No portal do Azure de Olá, selecione seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="9ecb5-189">Clique em **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="9ecb5-190">Saudação de tipo comando a seguir `Type=AutomationJob_CL` e clique em botão de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="9ecb5-191">Observe que o tipo de registro de saudação inclui _CL que não está especificado no script hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="9ecb5-192">Esse sufixo é acrescentada automaticamente toohello log tipo tooindicate que é um tipo de log personalizado.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="9ecb5-193">Você deve ver um ou mais registros retornados indicando que esse runbook hello está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="9ecb5-194">6. Publicar o runbook Olá</span><span class="sxs-lookup"><span data-stu-id="9ecb5-194">6. Publish hello runbook</span></span>
<span data-ttu-id="9ecb5-195">Depois de ter verificado que Olá runbook está funcionando corretamente, é necessário toopublish isso, você pode executá-lo em produção.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="9ecb5-196">Você pode continuar tooedit e testar o runbook Olá sem modificar a versão publicada hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Publicar runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="9ecb5-198">Retorne tooyour conta de automação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="9ecb5-199">Clique em **Runbooks** e selecione **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="9ecb5-200">Clique em **Editar** e **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="9ecb5-201">Clique em **Sim** quando tooverify frequentes que você deseja toooverwrite Olá anteriormente publicada versão.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="9ecb5-202">7. Definir opções de log</span><span class="sxs-lookup"><span data-stu-id="9ecb5-202">7. Set logging options</span></span> 
<span data-ttu-id="9ecb5-203">Para teste, você fosse capaz de tooview [saída detalhada](../automation/automation-runbook-output-and-messages.md#message-streams) porque você definir a variável de saudação $VerbosePreference no script hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="9ecb5-204">Para a produção, você precisa propriedades de log de saudação do tooset do runbook Olá se desejar que a saída detalhada tooview.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="9ecb5-205">Para o runbook Olá usado neste tutorial, será exibido envio tooLog análise de dados json hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Log e rastreamento](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="9ecb5-207">Nas propriedades de saudação do seu runbook selecione **registro em log e rastreamento** em **as configurações de Runbook**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="9ecb5-208">Alterar configuração Olá **registros detalhados de Log** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="9ecb5-209">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="9ecb5-210">8. Agendar runbook</span><span class="sxs-lookup"><span data-stu-id="9ecb5-210">8. Schedule runbook</span></span>
<span data-ttu-id="9ecb5-211">Olá, toostart de maneira mais comum um runbook que coleta dados de monitoramento é tooschedule-toorun automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="9ecb5-212">Você pode fazer isso criando um [agenda na automação do Azure](../automation/automation-schedules.md) e anexá-lo tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Agendar runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="9ecb5-214">Nas propriedades de saudação do seu runbook, selecione **agendas** em **recursos**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="9ecb5-215">Clique em **adicionar uma agenda** > **vincula um runbook do agendamento tooyour** > **criar uma nova agenda**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="9ecb5-216">Tipo de saudação seguintes valores para o agendamento de saudação e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="9ecb5-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9ecb5-217">Property</span></span> | <span data-ttu-id="9ecb5-218">Valor</span><span class="sxs-lookup"><span data-stu-id="9ecb5-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="9ecb5-219">Nome</span><span class="sxs-lookup"><span data-stu-id="9ecb5-219">Name</span></span> | <span data-ttu-id="9ecb5-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="9ecb5-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="9ecb5-221">Inicia</span><span class="sxs-lookup"><span data-stu-id="9ecb5-221">Starts</span></span> | <span data-ttu-id="9ecb5-222">Selecione a qualquer momento pelo menos 5 minutos anterior Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="9ecb5-223">Recorrência</span><span class="sxs-lookup"><span data-stu-id="9ecb5-223">Recurrence</span></span> | <span data-ttu-id="9ecb5-224">Recorrente</span><span class="sxs-lookup"><span data-stu-id="9ecb5-224">Recurring</span></span> |
| <span data-ttu-id="9ecb5-225">Repetir a cada</span><span class="sxs-lookup"><span data-stu-id="9ecb5-225">Recur every</span></span> | <span data-ttu-id="9ecb5-226">1 hora</span><span class="sxs-lookup"><span data-stu-id="9ecb5-226">1 hour</span></span> |
| <span data-ttu-id="9ecb5-227">Definir a validade</span><span class="sxs-lookup"><span data-stu-id="9ecb5-227">Set expiration</span></span> | <span data-ttu-id="9ecb5-228">Não</span><span class="sxs-lookup"><span data-stu-id="9ecb5-228">No</span></span> |

<span data-ttu-id="9ecb5-229">Após Olá cronograma é criado, você precisará tooset valores de parâmetro de saudação que serão usados toda vez que essa agenda inicia o runbook de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="9ecb5-230">Clique em **Configurar parâmetros e configurações de execução**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="9ecb5-231">Preencha os valores para **ResourceGroupName** e **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="9ecb5-232">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="9ecb5-233">9. Verificar se o runbook é iniciado no agendamento</span><span class="sxs-lookup"><span data-stu-id="9ecb5-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="9ecb5-234">Toda vez que um runbook é iniciado, [um trabalho é criado](../automation/automation-runbook-execution.md) e qualquer saída é registrada.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="9ecb5-235">Na verdade, esses são Olá mesmo trabalhos Olá runbook está coletando.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="9ecb5-236">Você pode verificar que esse runbook Olá iniciado como esperado por verificações trabalhos Olá Olá runbook após a hora de início de saudação de agenda Olá passou.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Trabalhos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="9ecb5-238">Nas propriedades de saudação do seu runbook, selecione **trabalhos** em **recursos**.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="9ecb5-239">Você deve ver que uma lista de trabalhos para cada runbook de saudação do tempo foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="9ecb5-240">Clique em uma saudação trabalhos tooview seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="9ecb5-241">Clique em **todos os logs** tooview Olá logs e saída de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="9ecb5-242">Role toohello inferior toofind uma entrada semelhante toohello imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Detalhado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="9ecb5-244">Clique nesta entrada hello tooview json dados detalhados que foi enviados tooLog análise.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9ecb5-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ecb5-245">Next steps</span></span>
- <span data-ttu-id="9ecb5-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate exibir um modo de exibição Olá dados que você coletou toohello repositório de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="9ecb5-247">Empacotar seu runbook em um [solução de gerenciamento de](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="9ecb5-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="9ecb5-248">Saiba mais sobre o [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="9ecb5-249">Saiba mais sobre a [Automação do Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="9ecb5-250">Saiba mais sobre Olá [API do coletor de dados de HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb5-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
