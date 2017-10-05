---
title: "Coletando dados de Log Analytics com um runbook na Automação do Azure | Microsoft Docs"
description: "Tutorial passo a passo que orienta a criação de um runbook na Automação do Azure para coletar dados para o repositório do OMS que serão analisados pelo Log Analytics."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="178c9-103">Coletar dados no Log Analytics com um runbook na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="178c9-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="178c9-104">Você pode coletar uma quantidade significativa de dados no Log Analytics de uma variedade de fontes, inclusive [fontes de dados](../log-analytics/log-analytics-data-sources.md) nos agentes e também os [dados coletados do Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="178c9-105">Porém, há cenários em que você precisa coletar dados que não estão acessíveis por meio dessas fontes padrão.</span><span class="sxs-lookup"><span data-stu-id="178c9-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="178c9-106">Nesses casos, você pode usar a [API do Coletor de Dados HTTP](../log-analytics/log-analytics-data-collector-api.md) para gravar dados ao Log Analytics de qualquer cliente de API REST.</span><span class="sxs-lookup"><span data-stu-id="178c9-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="178c9-107">Um método comum para realizar essa coleta de dados é usar um runbook na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="178c9-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="178c9-108">Este tutorial explica o processo para criar e agendar um runbook na Automação do Azure para gravar os dados no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="178c9-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="178c9-109">Prerequisites</span></span>
<span data-ttu-id="178c9-110">Esse cenário exige os seguintes recursos configurados na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="178c9-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="178c9-111">Ambos podem ser uma conta gratuita.</span><span class="sxs-lookup"><span data-stu-id="178c9-111">Both can be a free account.</span></span>

- <span data-ttu-id="178c9-112">[Espaço de trabalho do Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="178c9-113">[Conta de automação do Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="178c9-114">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="178c9-114">Overview of scenario</span></span>
<span data-ttu-id="178c9-115">Para este tutorial, você escreverá um runbook que coleta informações sobre trabalhos de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="178c9-116">Os runbooks na Automação do Azure são implementados com o PowerShell, portanto, comece gravando e testando um script no editor da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="178c9-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="178c9-117">Depois de confirmar que você está coletando as informações necessárias, você gravará esses dados no Log Analytics e verificará o tipo de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="178c9-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="178c9-118">Por fim, você criará um agendamento para iniciar o runbook em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="178c9-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="178c9-119">Você pode configurar a automação do Azure para enviar informações de trabalho para o Log Analytics sem esse runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="178c9-120">Esse cenário é usado principalmente para oferecer suporte ao tutorial e é recomendável que você envie os dados para um espaço de trabalho de teste.</span><span class="sxs-lookup"><span data-stu-id="178c9-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="178c9-121">1. Instalar o módulo de API do Coletor de Dados</span><span class="sxs-lookup"><span data-stu-id="178c9-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="178c9-122">Cada [solicitação da API do Coletor de Dados HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) deve ser formatado corretamente e inclui um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="178c9-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="178c9-123">Você pode fazer isso em seu runbook, mas pode reduzir a quantidade de código necessária para usar um módulo que simplifica esse processo.</span><span class="sxs-lookup"><span data-stu-id="178c9-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="178c9-124">Um módulo que você pode usar é o [módulo OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="178c9-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="178c9-125">Para usar um [módulo](../automation/automation-integration-modules.md) em um runbook, ele deverá ser instalado na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="178c9-126">Qualquer runbook na mesma conta pode usar as funções no módulo.</span><span class="sxs-lookup"><span data-stu-id="178c9-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="178c9-127">Você pode instalar um novo módulo selecionando **Ativos** > **Módulos** > **Adicionar um módulo** na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="178c9-128">No entanto, a Galeria do PowerShell oferece uma opção rápida para implantar um módulo diretamente em sua conta de automação para que você possa usar essa opção para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="178c9-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="178c9-130">Acesse a [Galeria do PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="178c9-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="178c9-131">Procure **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="178c9-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="178c9-132">Clique no botão **Implantar a Automação do Azure**.</span><span class="sxs-lookup"><span data-stu-id="178c9-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="178c9-133">Selecione sua conta de automação e clique em **OK** para instalar o módulo.</span><span class="sxs-lookup"><span data-stu-id="178c9-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="178c9-134">2. Criar variáveis de Automação</span><span class="sxs-lookup"><span data-stu-id="178c9-134">2. Create Automation variables</span></span>
<span data-ttu-id="178c9-135">As [variáveis de Automação](..\automation\automation-variables.md) contêm valores que podem ser usados por todos os runbooks na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="178c9-136">Eles tornam os runbooks mais flexíveis permitindo que você altere esses valores sem editar o runbook real.</span><span class="sxs-lookup"><span data-stu-id="178c9-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="178c9-137">Todas as solicitações da API do Coletor de Dados HTTP exige a identificação e a chave do espaço de trabalho do OMS e os ativos de variável são ideais para armazenar essas informações.</span><span class="sxs-lookup"><span data-stu-id="178c9-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variáveis](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="178c9-139">No portal do Azure, abra sua Conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="178c9-140">Selecione **Variáveis** em **Recursos Compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="178c9-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="178c9-141">Clique em **Adicionar uma variável** e crie duas variáveis na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="178c9-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="178c9-142">Propriedade</span><span class="sxs-lookup"><span data-stu-id="178c9-142">Property</span></span> | <span data-ttu-id="178c9-143">Valor da ID do Espaço de Trabalho</span><span class="sxs-lookup"><span data-stu-id="178c9-143">Workspace ID Value</span></span> | <span data-ttu-id="178c9-144">Valor da Chave do Espaço de Trabalho</span><span class="sxs-lookup"><span data-stu-id="178c9-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="178c9-145">Nome</span><span class="sxs-lookup"><span data-stu-id="178c9-145">Name</span></span> | <span data-ttu-id="178c9-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="178c9-146">WorkspaceId</span></span> | <span data-ttu-id="178c9-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="178c9-147">WorkspaceKey</span></span> |
| <span data-ttu-id="178c9-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="178c9-148">Type</span></span> | <span data-ttu-id="178c9-149">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="178c9-149">String</span></span> | <span data-ttu-id="178c9-150">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="178c9-150">String</span></span> |
| <span data-ttu-id="178c9-151">Valor</span><span class="sxs-lookup"><span data-stu-id="178c9-151">Value</span></span> | <span data-ttu-id="178c9-152">Cole a ID do espaço de trabalho do seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="178c9-153">Cole com a chave primária ou secundária do seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="178c9-154">Criptografado</span><span class="sxs-lookup"><span data-stu-id="178c9-154">Encrypted</span></span> | <span data-ttu-id="178c9-155">Não</span><span class="sxs-lookup"><span data-stu-id="178c9-155">No</span></span> | <span data-ttu-id="178c9-156">Sim</span><span class="sxs-lookup"><span data-stu-id="178c9-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="178c9-157">3. Criar runbook</span><span class="sxs-lookup"><span data-stu-id="178c9-157">3. Create runbook</span></span>

<span data-ttu-id="178c9-158">A Automação do Azure tem um editor no portal onde você pode editar e testar seu runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="178c9-159">Você tem a opção de usar o editor de scripts para trabalhar com o [PowerShell diretamente](../automation/automation-edit-textual-runbook.md) ou [criar um runbook gráfico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="178c9-160">Para este tutorial, você trabalhará com um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="178c9-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Editar runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="178c9-162">Abra sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="178c9-163">Clique em **Runbooks** > **Adicionar um runbook** > **Criar um novo runbook**.</span><span class="sxs-lookup"><span data-stu-id="178c9-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="178c9-164">Para o nome do runbook, digite **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="178c9-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="178c9-165">Para o tipo de runbook, selecione **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="178c9-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="178c9-166">Clique em **Criar** para criar o runbook e iniciar o editor.</span><span class="sxs-lookup"><span data-stu-id="178c9-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="178c9-167">Copie e cole o seguinte código no runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="178c9-168">Consulte os comentários no script para obter a explicação do código.</span><span class="sxs-lookup"><span data-stu-id="178c9-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="178c9-169">4. Runbook de teste</span><span class="sxs-lookup"><span data-stu-id="178c9-169">4. Test runbook</span></span>
<span data-ttu-id="178c9-170">A Automação do Azure inclui um ambiente de [testar seu runbook](../automation/automation-testing-runbook.md) antes de publicá-lo.</span><span class="sxs-lookup"><span data-stu-id="178c9-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="178c9-171">Você pode inspecionar os dados coletados pelo runbook e verificar se ele grava no Log Analytics conforme o esperado antes de publicá-lo em produção.</span><span class="sxs-lookup"><span data-stu-id="178c9-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Runbook de teste](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="178c9-173">Clique em **Salvar** para salvar o runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="178c9-174">Clique em **Painel de teste** para abrir o runbook no ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="178c9-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="178c9-175">Como o runbook tem parâmetros, você será solicitado a inserir valores para eles.</span><span class="sxs-lookup"><span data-stu-id="178c9-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="178c9-176">Insira o nome do grupo de recursos e a conta de automação da qual você coletará informações do trabalho.</span><span class="sxs-lookup"><span data-stu-id="178c9-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="178c9-177">Clique em **Iniciar** para iniciar o runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="178c9-178">O runbook iniciará com um status de **Em fila** antes da transferência para **Executando**.</span><span class="sxs-lookup"><span data-stu-id="178c9-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="178c9-179">O runbook deve exibir a saída detalhada com os trabalhos coletados no formato json.</span><span class="sxs-lookup"><span data-stu-id="178c9-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="178c9-180">Se nenhum trabalho estiver listado, isso significará que talvez nenhum trabalho tenha sido criado na conta de automação na última hora.</span><span class="sxs-lookup"><span data-stu-id="178c9-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="178c9-181">Tente iniciar qualquer runbook na conta de automação e execute o teste novamente.</span><span class="sxs-lookup"><span data-stu-id="178c9-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="178c9-182">Verifique se a saída não mostra todos os erros no comando post para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="178c9-183">Você deve ver uma página semelhante a esta.</span><span class="sxs-lookup"><span data-stu-id="178c9-183">You should have a message similar to the following.</span></span>

    ![Saída de postagem](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="178c9-185">5. Verificar registros no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="178c9-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="178c9-186">Após o runbook ter sido concluído no teste e você ter verificado que a saída foi recebida com êxito, você poderá verificar se os registros foram criados usando uma [pesquisa de log no Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Saída de log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="178c9-188">No Portal do Azure, selecione o espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="178c9-189">Clique em **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="178c9-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="178c9-190">Digite o seguinte comando `Type=AutomationJob_CL` e clique no botão de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="178c9-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="178c9-191">Observe que o tipo de registro inclui _CL, que não foi especificado no script.</span><span class="sxs-lookup"><span data-stu-id="178c9-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="178c9-192">Esse sufixo é acrescentado automaticamente para o tipo de registro para indicar que ele é um tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="178c9-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="178c9-193">Você deve ver um ou mais registros retornados indicando que o runbook está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="178c9-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="178c9-194">6. Publicar o runbook</span><span class="sxs-lookup"><span data-stu-id="178c9-194">6. Publish the runbook</span></span>
<span data-ttu-id="178c9-195">Depois de verificar se o runbook está funcionando corretamente, você precisará publicá-lo para poder executá-lo em produção.</span><span class="sxs-lookup"><span data-stu-id="178c9-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="178c9-196">Você pode continuar a editar e testar o runbook sem modificar a versão publicada.</span><span class="sxs-lookup"><span data-stu-id="178c9-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Publicar runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="178c9-198">Retorne para sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="178c9-198">Return to your automation account.</span></span>
2. <span data-ttu-id="178c9-199">Clique em **Runbooks** e selecione **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="178c9-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="178c9-200">Clique em **Editar** e **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="178c9-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="178c9-201">Clique em **Sim** quando for solicitado para verificar se deseja substituir a versão anteriormente publicada.</span><span class="sxs-lookup"><span data-stu-id="178c9-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="178c9-202">7. Definir opções de log</span><span class="sxs-lookup"><span data-stu-id="178c9-202">7. Set logging options</span></span> 
<span data-ttu-id="178c9-203">Para teste, você conseguiu exibir [saída detalhada](../automation/automation-runbook-output-and-messages.md#message-streams) porque definiu a variável $VerbosePreference no script.</span><span class="sxs-lookup"><span data-stu-id="178c9-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="178c9-204">Para produção, você precisa definir as propriedades de log para o runbook se deseja exibir a saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="178c9-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="178c9-205">Para o runbook usado neste tutorial, isso exibirá os dados json enviados para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Log e rastreamento](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="178c9-207">Nas propriedades para o seu runbook, selecione **Log e rastreamento** em **Configurações do Runbook**.</span><span class="sxs-lookup"><span data-stu-id="178c9-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="178c9-208">Altere a configuração para **Registros detalhados de Log** para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="178c9-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="178c9-209">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="178c9-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="178c9-210">8. Agendar runbook</span><span class="sxs-lookup"><span data-stu-id="178c9-210">8. Schedule runbook</span></span>
<span data-ttu-id="178c9-211">A maneira mais comum para iniciar um runbook que coleta dados de monitoramento é agendá-lo para ser executado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="178c9-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="178c9-212">Você pode fazer isso criando uma [agenda na Automação do Azure](../automation/automation-schedules.md) e anexá-la ao seu runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Agendar runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="178c9-214">Nas propriedades do seu runbook, selecione **Agendas** em **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="178c9-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="178c9-215">Clique em **Adicionar uma agenda** > **Vincular uma agenda ao runbook** > **Criar uma nova agenda**.</span><span class="sxs-lookup"><span data-stu-id="178c9-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="178c9-216">Digite os seguintes valores para o agendamento e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="178c9-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="178c9-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="178c9-217">Property</span></span> | <span data-ttu-id="178c9-218">Valor</span><span class="sxs-lookup"><span data-stu-id="178c9-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="178c9-219">Nome</span><span class="sxs-lookup"><span data-stu-id="178c9-219">Name</span></span> | <span data-ttu-id="178c9-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="178c9-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="178c9-221">Inicia</span><span class="sxs-lookup"><span data-stu-id="178c9-221">Starts</span></span> | <span data-ttu-id="178c9-222">Selecione qualquer horário pelo menos 5 minutos após a hora atual.</span><span class="sxs-lookup"><span data-stu-id="178c9-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="178c9-223">Recorrência</span><span class="sxs-lookup"><span data-stu-id="178c9-223">Recurrence</span></span> | <span data-ttu-id="178c9-224">Recorrente</span><span class="sxs-lookup"><span data-stu-id="178c9-224">Recurring</span></span> |
| <span data-ttu-id="178c9-225">Repetir a cada</span><span class="sxs-lookup"><span data-stu-id="178c9-225">Recur every</span></span> | <span data-ttu-id="178c9-226">1 hora</span><span class="sxs-lookup"><span data-stu-id="178c9-226">1 hour</span></span> |
| <span data-ttu-id="178c9-227">Definir a validade</span><span class="sxs-lookup"><span data-stu-id="178c9-227">Set expiration</span></span> | <span data-ttu-id="178c9-228">Não</span><span class="sxs-lookup"><span data-stu-id="178c9-228">No</span></span> |

<span data-ttu-id="178c9-229">Depois de criar a agenda, você precisará definir os valores de parâmetro que serão usados sempre que essa agenda iniciar o runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="178c9-230">Clique em **Configurar parâmetros e configurações de execução**.</span><span class="sxs-lookup"><span data-stu-id="178c9-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="178c9-231">Preencha os valores para **ResourceGroupName** e **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="178c9-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="178c9-232">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="178c9-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="178c9-233">9. Verificar se o runbook é iniciado no agendamento</span><span class="sxs-lookup"><span data-stu-id="178c9-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="178c9-234">Toda vez que um runbook é iniciado, [um trabalho é criado](../automation/automation-runbook-execution.md) e qualquer saída é registrada.</span><span class="sxs-lookup"><span data-stu-id="178c9-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="178c9-235">Na verdade, esses são os mesmos trabalhos que o runbook está coletando.</span><span class="sxs-lookup"><span data-stu-id="178c9-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="178c9-236">Você pode verificar se o runbook é iniciado conforme o esperado, verificando os trabalhos para o runbook após a hora de início da agenda.</span><span class="sxs-lookup"><span data-stu-id="178c9-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Trabalhos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="178c9-238">Nas propriedades do seu runbook, selecione **Trabalhos** em **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="178c9-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="178c9-239">Você deverá ver uma lista dos trabalhos para cada vez que o runbook foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="178c9-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="178c9-240">Clique em um dos trabalhos para exibir seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="178c9-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="178c9-241">Clique em **Todos os logs** para exibir os logs e a saída do runbook.</span><span class="sxs-lookup"><span data-stu-id="178c9-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="178c9-242">Role para baixo para localizar uma entrada semelhante à imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="178c9-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Detalhado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="178c9-244">Clique nessa entrada para exibir os dados json detalhados que foram enviados para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="178c9-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="178c9-245">Next steps</span></span>
- <span data-ttu-id="178c9-246">Use [Criador de Modos de Exibição](../log-analytics/log-analytics-view-designer.md) para criar uma exibição exibindo os dados coletados no repositório do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="178c9-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="178c9-247">Empacotar seu runbook em um [solução de gerenciamento](operations-management-suite-solutions-creating.md) para distribuir para os clientes.</span><span class="sxs-lookup"><span data-stu-id="178c9-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="178c9-248">Saiba mais sobre o [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="178c9-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="178c9-249">Saiba mais sobre a [Automação do Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="178c9-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="178c9-250">Saiba mais sobre a [API do Coletor de Dados HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="178c9-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>