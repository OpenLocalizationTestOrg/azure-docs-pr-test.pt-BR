---
title: "Iniciando e parando máquinas virtuais com a Automação do Azure - Fluxo de Trabalho do PowerShell | Microsoft Docs"
description: "Versão gráfica do cenário da Automação do Azure, incluindo runbooks para iniciar e parar máquinas virtuais clássicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="2dfb7-103">Cenário de Automação do Azure — iniciando e parando máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="2dfb7-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="2dfb7-104">Esse cenário de Automação do Azure inclui runbooks para iniciar e parar máquinas virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="2dfb7-105">Você pode usar esse cenário para qualquer um destes objetivos:</span><span class="sxs-lookup"><span data-stu-id="2dfb7-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="2dfb7-106">Usar os runbooks sem modificação em seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="2dfb7-107">Modificar os runbooks para executar funcionalidade personalizada.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="2dfb7-108">Chamar os runbooks de outro runbook como parte de uma solução geral.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="2dfb7-109">Usar os runbooks como tutoriais para saber sobre os conceitos de criação do runbook.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2dfb7-110">Gráfico</span><span class="sxs-lookup"><span data-stu-id="2dfb7-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="2dfb7-111">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dfb7-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="2dfb7-112">Esta é a versão de runbook do Fluxo de Trabalho do PowerShell desse cenário.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="2dfb7-113">Ela também é disponibilizada usando [runbooks gráficos](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="2dfb7-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="2dfb7-114">Obtendo o cenário</span><span class="sxs-lookup"><span data-stu-id="2dfb7-114">Getting the scenario</span></span>
<span data-ttu-id="2dfb7-115">Esse cenário é formado por dois runbooks de Fluxo de Trabalho do PowerShell, que você pode baixar dos links a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="2dfb7-116">Confira a [versão gráfica](automation-solution-startstopvm-graphical.md) deste cenário para obter os links para os runbooks gráficos.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="2dfb7-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="2dfb7-117">Runbook</span></span> | <span data-ttu-id="2dfb7-118">Link</span><span class="sxs-lookup"><span data-stu-id="2dfb7-118">Link</span></span> | <span data-ttu-id="2dfb7-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="2dfb7-119">Type</span></span> | <span data-ttu-id="2dfb7-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="2dfb7-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2dfb7-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-121">Start-AzureVMs</span></span> |[<span data-ttu-id="2dfb7-122">Iniciar VMs clássicas do Azure</span><span class="sxs-lookup"><span data-stu-id="2dfb7-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="2dfb7-123">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dfb7-123">PowerShell Workflow</span></span> |<span data-ttu-id="2dfb7-124">Inicia todas as máquinas virtuais clássicas em uma assinatura do Azure ou em todas as máquinas virtuais com um nome de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="2dfb7-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="2dfb7-126">Parar VMs clássicas do Azure</span><span class="sxs-lookup"><span data-stu-id="2dfb7-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="2dfb7-127">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dfb7-127">PowerShell Workflow</span></span> |<span data-ttu-id="2dfb7-128">Para todas as máquinas virtuais em uma conta de automação ou todas as máquinas virtuais com um nome de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="2dfb7-129">Instalando e configurando o cenário</span><span class="sxs-lookup"><span data-stu-id="2dfb7-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="2dfb7-130">1. Instalar os runbooks</span><span class="sxs-lookup"><span data-stu-id="2dfb7-130">1. Install the runbooks</span></span>
<span data-ttu-id="2dfb7-131">Depois de baixar os runbooks, você poderá importá-los usando o procedimento em [Importando um runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="2dfb7-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="2dfb7-132">2. Analisar a descrição e os requisitos</span><span class="sxs-lookup"><span data-stu-id="2dfb7-132">2. Review the description and requirements</span></span>
<span data-ttu-id="2dfb7-133">Os runbooks incluem um texto de ajuda comentado que apresenta uma descrição e os ativos necessários.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="2dfb7-134">Também é possível obter as mesmas informações neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="2dfb7-135">3. Configurar ativos</span><span class="sxs-lookup"><span data-stu-id="2dfb7-135">3. Configure assets</span></span>
<span data-ttu-id="2dfb7-136">Os runbooks exigem os ativos a seguir, que você deverá criar e preencher com os valores apropriados.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="2dfb7-137">Tipo de Ativo</span><span class="sxs-lookup"><span data-stu-id="2dfb7-137">Asset Type</span></span> | <span data-ttu-id="2dfb7-138">Nome do ativo</span><span class="sxs-lookup"><span data-stu-id="2dfb7-138">Asset Name</span></span> | <span data-ttu-id="2dfb7-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="2dfb7-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2dfb7-140">Credencial</span><span class="sxs-lookup"><span data-stu-id="2dfb7-140">Credential</span></span> |<span data-ttu-id="2dfb7-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="2dfb7-141">AzureCredential</span></span> |<span data-ttu-id="2dfb7-142">Contém as credenciais de uma conta com autoridade para iniciar e parar máquinas virtuais na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="2dfb7-143">Como alternativa, você pode especificar outro ativo credencial no parâmetro **Credencial** da atividade **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="2dfb7-144">Variável</span><span class="sxs-lookup"><span data-stu-id="2dfb7-144">Variable</span></span> |<span data-ttu-id="2dfb7-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2dfb7-145">AzureSubscriptionId</span></span> |<span data-ttu-id="2dfb7-146">Contém a ID da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="2dfb7-147">Usando o cenário</span><span class="sxs-lookup"><span data-stu-id="2dfb7-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="2dfb7-148">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2dfb7-148">Parameters</span></span>
<span data-ttu-id="2dfb7-149">Cada um dos runbooks tem os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="2dfb7-150">Você deve fornecer valores para todos os parâmetros obrigatórios e pode, se desejar, fornecer valores para outros parâmetros de acordo com os próprios requisitos.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="2dfb7-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="2dfb7-151">Parameter</span></span> | <span data-ttu-id="2dfb7-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="2dfb7-152">Type</span></span> | <span data-ttu-id="2dfb7-153">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2dfb7-153">Mandatory</span></span> | <span data-ttu-id="2dfb7-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="2dfb7-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2dfb7-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="2dfb7-155">ServiceName</span></span> |<span data-ttu-id="2dfb7-156">string</span><span class="sxs-lookup"><span data-stu-id="2dfb7-156">string</span></span> |<span data-ttu-id="2dfb7-157">Não</span><span class="sxs-lookup"><span data-stu-id="2dfb7-157">No</span></span> |<span data-ttu-id="2dfb7-158">Se um valor for fornecido, todas as máquinas virtuais com esse nome de serviço serão iniciadas ou paradas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="2dfb7-159">Se nenhum valor for fornecido, todas as máquinas virtuais clássicas na assinatura do Azure serão iniciadas ou paradas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="2dfb7-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="2dfb7-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="2dfb7-161">string</span><span class="sxs-lookup"><span data-stu-id="2dfb7-161">string</span></span> |<span data-ttu-id="2dfb7-162">Não</span><span class="sxs-lookup"><span data-stu-id="2dfb7-162">No</span></span> |<span data-ttu-id="2dfb7-163">Contém o nome do [ativo variável](#installing-and-configuring-the-scenario) que contém a ID da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="2dfb7-164">Se você não especificar um valor, *AzureSubscriptionId* será usado.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="2dfb7-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="2dfb7-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="2dfb7-166">string</span><span class="sxs-lookup"><span data-stu-id="2dfb7-166">string</span></span> |<span data-ttu-id="2dfb7-167">Não</span><span class="sxs-lookup"><span data-stu-id="2dfb7-167">No</span></span> |<span data-ttu-id="2dfb7-168">Contém o nome do [ativo de credencial](#installing-and-configuring-the-scenario) com as credenciais para o runbook a ser usado.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="2dfb7-169">Se você não especificar um valor, *AzureCredential* será usado.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="2dfb7-170">Iniciando os runbooks</span><span class="sxs-lookup"><span data-stu-id="2dfb7-170">Starting the runbooks</span></span>
<span data-ttu-id="2dfb7-171">Você pode usar qualquer um dos métodos em [Iniciando um runbook na Automação do Azure](automation-starting-a-runbook.md) para iniciar qualquer um dos runbooks neste cenário.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="2dfb7-172">Os comandos de exemplo a seguir usam o Windows PowerShell para executar **StartAzureClassicVM** e iniciar todas as máquinas virtuais com o nome do serviço *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="2dfb7-173">Saída</span><span class="sxs-lookup"><span data-stu-id="2dfb7-173">Output</span></span>
<span data-ttu-id="2dfb7-174">Os runbooks [emitirão uma mensagem](automation-runbook-output-and-messages.md) para cada máquina virtual, indicando se a instrução de inicialização ou interrupção foi enviada com êxito.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="2dfb7-175">Você pode procurar uma cadeia de caracteres específica na saída para determinar o resultado de cada runbook.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="2dfb7-176">As cadeias de caracteres de saída possíveis estão listadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="2dfb7-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="2dfb7-177">Runbook</span></span> | <span data-ttu-id="2dfb7-178">Condição</span><span class="sxs-lookup"><span data-stu-id="2dfb7-178">Condition</span></span> | <span data-ttu-id="2dfb7-179">Mensagem</span><span class="sxs-lookup"><span data-stu-id="2dfb7-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2dfb7-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-180">Start-AzureVMs</span></span> |<span data-ttu-id="2dfb7-181">A máquina virtual já está em execução</span><span class="sxs-lookup"><span data-stu-id="2dfb7-181">Virtual machine is already running</span></span> |<span data-ttu-id="2dfb7-182">MyVM já está em execução</span><span class="sxs-lookup"><span data-stu-id="2dfb7-182">MyVM is already running</span></span> |
| <span data-ttu-id="2dfb7-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-183">Start-AzureVMs</span></span> |<span data-ttu-id="2dfb7-184">Solicitação de inicialização para máquina virtual enviada com êxito</span><span class="sxs-lookup"><span data-stu-id="2dfb7-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="2dfb7-185">MyVM foi iniciada</span><span class="sxs-lookup"><span data-stu-id="2dfb7-185">MyVM has been started</span></span> |
| <span data-ttu-id="2dfb7-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-186">Start-AzureVMs</span></span> |<span data-ttu-id="2dfb7-187">Falha na solicitação de inicialização para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2dfb7-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="2dfb7-188">Falha ao iniciar a MyVM</span><span class="sxs-lookup"><span data-stu-id="2dfb7-188">MyVM failed to start</span></span> |
| <span data-ttu-id="2dfb7-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-189">Stop-AzureVMs</span></span> |<span data-ttu-id="2dfb7-190">A máquina virtual já está parada</span><span class="sxs-lookup"><span data-stu-id="2dfb7-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="2dfb7-191">MyVM já foi parada</span><span class="sxs-lookup"><span data-stu-id="2dfb7-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="2dfb7-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-192">Stop-AzureVMs</span></span> |<span data-ttu-id="2dfb7-193">Solicitação de parada da máquina virtual enviada com êxito</span><span class="sxs-lookup"><span data-stu-id="2dfb7-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="2dfb7-194">MyVM foi parada</span><span class="sxs-lookup"><span data-stu-id="2dfb7-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="2dfb7-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-195">Stop-AzureVMs</span></span> |<span data-ttu-id="2dfb7-196">Falha na solicitação de parada da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2dfb7-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="2dfb7-197">Falha ao para a MyVM</span><span class="sxs-lookup"><span data-stu-id="2dfb7-197">MyVM failed to stop</span></span> |

<span data-ttu-id="2dfb7-198">Por exemplo, o trecho de código a seguir de um runbook tenta iniciar todas as máquinas virtuais com o nome de serviço *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="2dfb7-199">Se algumas das solicitações de inicialização falhar, as ações de erro poderão ser executadas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="2dfb7-200">Divisão detalhada</span><span class="sxs-lookup"><span data-stu-id="2dfb7-200">Detailed breakdown</span></span>
<span data-ttu-id="2dfb7-201">Veja a seguir uma divisão detalhada dos runbooks nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="2dfb7-202">Você pode usar essas informações para personalizar os runbooks ou apenas para aprender a criar seus próprios cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="2dfb7-203">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2dfb7-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="2dfb7-204">O fluxo de trabalho é iniciado obtendo os valores dos [parâmetros de entrada](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="2dfb7-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="2dfb7-205">Se os nomes do ativo não forem fornecidos, os nomes padrão serão usados.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="2dfb7-206">Saída</span><span class="sxs-lookup"><span data-stu-id="2dfb7-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="2dfb7-207">Essa linha declara que a saída do runbook será uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="2dfb7-208">Ela não é obrigatória, mas é uma prática recomendada para quando o runbook for usado como um [runbook filho](automation-child-runbooks.md) , de modo que o runbook pai saiba que tipo de saída esperar.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="2dfb7-209">Autenticação</span><span class="sxs-lookup"><span data-stu-id="2dfb7-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="2dfb7-210">As próximas linhas definem as [credenciais](automation-credentials.md) e a assinatura do Azure que serão usadas para o restante do runbook.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="2dfb7-211">Primeiro, usamos **Get-AutomationPSCredential** para obter o ativo que mantém as credenciais com acesso para iniciar e parar máquinas virtuais na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="2dfb7-212">**Add-AzureAccount** usa esse ativo para definir as credenciais.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="2dfb7-213">A saída é atribuída a uma variável fictícia para que ela não seja incluída na saída do runbook.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="2dfb7-214">O ativo variável com a ID da assinatura é recuperado com **Get-AutomationVariable** e a assinatura definida com **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="2dfb7-215">Obter VMs</span><span class="sxs-lookup"><span data-stu-id="2dfb7-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="2dfb7-216">**Get-AzureVM** é usado para recuperar as máquinas virtuais com as quais o runbook trabalhará.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="2dfb7-217">Se um valor for fornecido na variável de entrada **ServiceName** , apenas as máquinas virtuais com esse nome de serviço serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="2dfb7-218">Se **ServiceName** estiver vazia, todas as máquinas virtuais serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="2dfb7-219">Iniciar/parar as máquinas virtuais e enviar a saída</span><span class="sxs-lookup"><span data-stu-id="2dfb7-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="2dfb7-220">As próximas linhas exploram cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="2dfb7-221">Primeiro o **PowerState** da máquina virtual é verificado para confirmar se ela já está em execução ou está parada, dependendo do runbook.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="2dfb7-222">Se já estiver no estado desejado, uma mensagem será enviada para a saída e o runbook será encerrado.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="2dfb7-223">Caso contrário, **Start-AzureVM** ou **Stop-AzureVM** será usado para tentar iniciar ou parar a máquina virtual com o resultado da solicitação armazenado em uma variável.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="2dfb7-224">Uma mensagem é enviada para a saída especificando se a solicitação para iniciar ou parar foi enviada com êxito.</span><span class="sxs-lookup"><span data-stu-id="2dfb7-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dfb7-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dfb7-225">Next steps</span></span>
* <span data-ttu-id="2dfb7-226">Para saber mais sobre como trabalhar com runbooks filho, consulte [Runbooks filho na Automação do Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="2dfb7-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="2dfb7-227">Para saber mais sobre mensagens de saída durante a execução de runbook e registro em log para ajudar a solucionar problemas, consulte [Saída e mensagens de runbook na Automação do Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="2dfb7-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

