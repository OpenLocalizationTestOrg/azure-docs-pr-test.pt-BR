---
title: "aaaStarting e parar máquinas virtuais com a automação do Azure - fluxo de trabalho do PowerShell | Microsoft Docs"
description: "Versão gráfica do cenário de automação do Azure, incluindo runbooks toostart e parar máquinas virtuais clássicas."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="f4e78-103">Cenário de Automação do Azure — iniciando e parando máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f4e78-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="f4e78-104">Este cenário de automação do Azure inclui runbooks toostart e parar máquinas virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="f4e78-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="f4e78-105">Você pode usar este cenário para qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="f4e78-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="f4e78-106">Use runbooks Olá sem modificação no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f4e78-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="f4e78-107">Modificar a funcionalidade do hello runbooks tooperform personalizado.</span><span class="sxs-lookup"><span data-stu-id="f4e78-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="f4e78-108">Chame hello runbooks de outro runbook como parte de uma solução geral.</span><span class="sxs-lookup"><span data-stu-id="f4e78-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="f4e78-109">Use runbooks hello como tutoriais toolearn runbook conceitos de criação.</span><span class="sxs-lookup"><span data-stu-id="f4e78-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4e78-110">Gráfico</span><span class="sxs-lookup"><span data-stu-id="f4e78-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="f4e78-111">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e78-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="f4e78-112">Isso é hello versão de runbook de fluxo de trabalho do PowerShell deste cenário.</span><span class="sxs-lookup"><span data-stu-id="f4e78-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="f4e78-113">Ela também é disponibilizada usando [runbooks gráficos](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="f4e78-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="f4e78-114">Obtendo o cenário de saudação</span><span class="sxs-lookup"><span data-stu-id="f4e78-114">Getting hello scenario</span></span>
<span data-ttu-id="f4e78-115">Este cenário consiste em dois runbooks de fluxo de trabalho do PowerShell que você pode baixar do hello links a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4e78-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="f4e78-116">Consulte Olá [versão gráfica](automation-solution-startstopvm-graphical.md) deste cenário para links toohello gráfica runbooks.</span><span class="sxs-lookup"><span data-stu-id="f4e78-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="f4e78-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="f4e78-117">Runbook</span></span> | <span data-ttu-id="f4e78-118">Link</span><span class="sxs-lookup"><span data-stu-id="f4e78-118">Link</span></span> | <span data-ttu-id="f4e78-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="f4e78-119">Type</span></span> | <span data-ttu-id="f4e78-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4e78-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4e78-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-121">Start-AzureVMs</span></span> |[<span data-ttu-id="f4e78-122">Iniciar VMs clássicas do Azure</span><span class="sxs-lookup"><span data-stu-id="f4e78-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="f4e78-123">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e78-123">PowerShell Workflow</span></span> |<span data-ttu-id="f4e78-124">Inicia todas as máquinas virtuais clássicas em uma assinatura do Azure ou em todas as máquinas virtuais com um nome de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="f4e78-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="f4e78-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="f4e78-126">Parar VMs clássicas do Azure</span><span class="sxs-lookup"><span data-stu-id="f4e78-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="f4e78-127">Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e78-127">PowerShell Workflow</span></span> |<span data-ttu-id="f4e78-128">Para todas as máquinas virtuais em uma conta de automação ou todas as máquinas virtuais com um nome de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="f4e78-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="f4e78-129">Instalando e configurando o cenário de saudação</span><span class="sxs-lookup"><span data-stu-id="f4e78-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="f4e78-130">1. Instalar Olá runbooks</span><span class="sxs-lookup"><span data-stu-id="f4e78-130">1. Install hello runbooks</span></span>
<span data-ttu-id="f4e78-131">Depois de baixar runbooks hello, você pode importá-los usando o procedimento Olá [importar um Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="f4e78-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="f4e78-132">2. Descrição de saudação de revisão e requisitos</span><span class="sxs-lookup"><span data-stu-id="f4e78-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="f4e78-133">Olá runbooks incluir texto de ajuda comentados que inclui uma descrição e os ativos necessários.</span><span class="sxs-lookup"><span data-stu-id="f4e78-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="f4e78-134">Você também pode obter Olá as mesmas informações deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f4e78-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="f4e78-135">3. Configurar ativos</span><span class="sxs-lookup"><span data-stu-id="f4e78-135">3. Configure assets</span></span>
<span data-ttu-id="f4e78-136">Olá runbooks exigem Olá ativos que você deve criar e popular com os valores apropriados a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4e78-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="f4e78-137">Tipo de Ativo</span><span class="sxs-lookup"><span data-stu-id="f4e78-137">Asset Type</span></span> | <span data-ttu-id="f4e78-138">Nome do ativo</span><span class="sxs-lookup"><span data-stu-id="f4e78-138">Asset Name</span></span> | <span data-ttu-id="f4e78-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4e78-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4e78-140">Credencial</span><span class="sxs-lookup"><span data-stu-id="f4e78-140">Credential</span></span> |<span data-ttu-id="f4e78-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="f4e78-141">AzureCredential</span></span> |<span data-ttu-id="f4e78-142">Contém as credenciais para uma conta que tenha autoridade toostart e parar máquinas de virtuais em Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e78-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="f4e78-143">Como alternativa, você pode especificar outro ativo de credencial em Olá **credencial** parâmetro hello **Add-AzureAccount** atividade.</span><span class="sxs-lookup"><span data-stu-id="f4e78-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="f4e78-144">Variável</span><span class="sxs-lookup"><span data-stu-id="f4e78-144">Variable</span></span> |<span data-ttu-id="f4e78-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f4e78-145">AzureSubscriptionId</span></span> |<span data-ttu-id="f4e78-146">Contém a ID de assinatura de saudação da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e78-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="f4e78-147">Usando o cenário de saudação</span><span class="sxs-lookup"><span data-stu-id="f4e78-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="f4e78-148">parâmetros</span><span class="sxs-lookup"><span data-stu-id="f4e78-148">Parameters</span></span>
<span data-ttu-id="f4e78-149">Olá runbooks cada têm Olá parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4e78-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="f4e78-150">Você deve fornecer valores para todos os parâmetros obrigatórios e pode, se desejar, fornecer valores para outros parâmetros de acordo com os próprios requisitos.</span><span class="sxs-lookup"><span data-stu-id="f4e78-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="f4e78-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f4e78-151">Parameter</span></span> | <span data-ttu-id="f4e78-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="f4e78-152">Type</span></span> | <span data-ttu-id="f4e78-153">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f4e78-153">Mandatory</span></span> | <span data-ttu-id="f4e78-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4e78-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4e78-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="f4e78-155">ServiceName</span></span> |<span data-ttu-id="f4e78-156">string</span><span class="sxs-lookup"><span data-stu-id="f4e78-156">string</span></span> |<span data-ttu-id="f4e78-157">Não</span><span class="sxs-lookup"><span data-stu-id="f4e78-157">No</span></span> |<span data-ttu-id="f4e78-158">Se um valor for fornecido, todas as máquinas virtuais com esse nome de serviço serão iniciadas ou paradas.</span><span class="sxs-lookup"><span data-stu-id="f4e78-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="f4e78-159">Se nenhum valor for fornecido, todas as máquinas virtuais clássicas em Olá assinatura do Azure são iniciadas ou interrompidas.</span><span class="sxs-lookup"><span data-stu-id="f4e78-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="f4e78-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="f4e78-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="f4e78-161">string</span><span class="sxs-lookup"><span data-stu-id="f4e78-161">string</span></span> |<span data-ttu-id="f4e78-162">Não</span><span class="sxs-lookup"><span data-stu-id="f4e78-162">No</span></span> |<span data-ttu-id="f4e78-163">Contém nome de saudação do hello [ativo variável](#installing-and-configuring-the-scenario) que contém a ID de assinatura de saudação da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e78-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="f4e78-164">Se você não especificar um valor, *AzureSubscriptionId* será usado.</span><span class="sxs-lookup"><span data-stu-id="f4e78-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="f4e78-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="f4e78-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="f4e78-166">string</span><span class="sxs-lookup"><span data-stu-id="f4e78-166">string</span></span> |<span data-ttu-id="f4e78-167">Não</span><span class="sxs-lookup"><span data-stu-id="f4e78-167">No</span></span> |<span data-ttu-id="f4e78-168">Contém nome de saudação do hello [ativo de credencial](#installing-and-configuring-the-scenario) que contém credenciais Olá Olá runbook toouse.</span><span class="sxs-lookup"><span data-stu-id="f4e78-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="f4e78-169">Se você não especificar um valor, *AzureCredential* será usado.</span><span class="sxs-lookup"><span data-stu-id="f4e78-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="f4e78-170">Runbooks de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="f4e78-170">Starting hello runbooks</span></span>
<span data-ttu-id="f4e78-171">Você pode usar qualquer um dos métodos de saudação em [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md) toostart qualquer um dos runbooks Olá neste cenário.</span><span class="sxs-lookup"><span data-stu-id="f4e78-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="f4e78-172">Olá comandos de exemplo a seguir usa o Windows PowerShell toorun **StartAzureVMs** toostart todas as máquinas virtuais com o nome do serviço Olá *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="f4e78-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="f4e78-173">Saída</span><span class="sxs-lookup"><span data-stu-id="f4e78-173">Output</span></span>
<span data-ttu-id="f4e78-174">Olá runbooks serão [uma mensagem de saída](automation-runbook-output-and-messages.md) para cada máquina virtual que indica se ou não Olá início ou instrução stop foi enviada com êxito.</span><span class="sxs-lookup"><span data-stu-id="f4e78-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="f4e78-175">Você pode procurar uma cadeia de caracteres específica em Olá toodetermine Olá resultado para cada runbook.</span><span class="sxs-lookup"><span data-stu-id="f4e78-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="f4e78-176">cadeias de caracteres de saída possíveis Olá são listadas na Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4e78-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="f4e78-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="f4e78-177">Runbook</span></span> | <span data-ttu-id="f4e78-178">Condição</span><span class="sxs-lookup"><span data-stu-id="f4e78-178">Condition</span></span> | <span data-ttu-id="f4e78-179">Mensagem</span><span class="sxs-lookup"><span data-stu-id="f4e78-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4e78-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-180">Start-AzureVMs</span></span> |<span data-ttu-id="f4e78-181">A máquina virtual já está em execução</span><span class="sxs-lookup"><span data-stu-id="f4e78-181">Virtual machine is already running</span></span> |<span data-ttu-id="f4e78-182">MyVM já está em execução</span><span class="sxs-lookup"><span data-stu-id="f4e78-182">MyVM is already running</span></span> |
| <span data-ttu-id="f4e78-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-183">Start-AzureVMs</span></span> |<span data-ttu-id="f4e78-184">Solicitação de inicialização para máquina virtual enviada com êxito</span><span class="sxs-lookup"><span data-stu-id="f4e78-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="f4e78-185">MyVM foi iniciada</span><span class="sxs-lookup"><span data-stu-id="f4e78-185">MyVM has been started</span></span> |
| <span data-ttu-id="f4e78-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-186">Start-AzureVMs</span></span> |<span data-ttu-id="f4e78-187">Falha na solicitação de inicialização para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f4e78-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="f4e78-188">Falha de MyVM toostart</span><span class="sxs-lookup"><span data-stu-id="f4e78-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="f4e78-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-189">Stop-AzureVMs</span></span> |<span data-ttu-id="f4e78-190">A máquina virtual já está parada</span><span class="sxs-lookup"><span data-stu-id="f4e78-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="f4e78-191">MyVM já foi parada</span><span class="sxs-lookup"><span data-stu-id="f4e78-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="f4e78-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-192">Stop-AzureVMs</span></span> |<span data-ttu-id="f4e78-193">Solicitação de parada da máquina virtual enviada com êxito</span><span class="sxs-lookup"><span data-stu-id="f4e78-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="f4e78-194">MyVM foi parada</span><span class="sxs-lookup"><span data-stu-id="f4e78-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="f4e78-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-195">Stop-AzureVMs</span></span> |<span data-ttu-id="f4e78-196">Falha na solicitação de parada da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f4e78-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="f4e78-197">Falha de MyVM toostop</span><span class="sxs-lookup"><span data-stu-id="f4e78-197">MyVM failed toostop</span></span> |

<span data-ttu-id="f4e78-198">Por exemplo, Olá trecho de código a seguir de um runbook tentativas toostart todas as máquinas virtuais com o nome do serviço Olá *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="f4e78-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="f4e78-199">Se qualquer Olá iniciar solicitações falhar, as ações de erro podem tomadas.</span><span class="sxs-lookup"><span data-stu-id="f4e78-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="f4e78-200">Divisão detalhada</span><span class="sxs-lookup"><span data-stu-id="f4e78-200">Detailed breakdown</span></span>
<span data-ttu-id="f4e78-201">A seguir está uma análise detalhada dos runbooks Olá neste cenário.</span><span class="sxs-lookup"><span data-stu-id="f4e78-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="f4e78-202">Você pode usar essas informações tooeither personalizar Olá runbooks ou apenas toolearn deles para a criação de seus próprios cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="f4e78-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="f4e78-203">parâmetros</span><span class="sxs-lookup"><span data-stu-id="f4e78-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="f4e78-204">Hello fluxo de trabalho é iniciado por obter valores Olá Olá [parâmetros de entrada](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="f4e78-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="f4e78-205">Se não forem fornecidos nomes de recursos de saudação nomes padrão são usados.</span><span class="sxs-lookup"><span data-stu-id="f4e78-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="f4e78-206">Saída</span><span class="sxs-lookup"><span data-stu-id="f4e78-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="f4e78-207">Essa linha declara que o resultado Olá Olá runbook será uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f4e78-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="f4e78-208">Isso não é necessário, mas é uma prática recomendada para quando o runbook Olá é usada como um [runbook filho](automation-child-runbooks.md) para que um runbook pai saibam saída Olá tooexpect de tipo.</span><span class="sxs-lookup"><span data-stu-id="f4e78-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="f4e78-209">Autenticação</span><span class="sxs-lookup"><span data-stu-id="f4e78-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="f4e78-210">linhas seguintes Olá definem Olá [credenciais](automation-credentials.md) e assinatura do Azure que será usada para o restante de saudação do runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f4e78-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="f4e78-211">Primeiro, usamos **Get-AutomationPSCredential** tooget ativo de saudação que mantém as credenciais de saudação com acesso toostart e parar máquinas virtuais em Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e78-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="f4e78-212">**Adicionar-AzureAccount** , em seguida, usa esse credenciais de saudação tooset ativo.</span><span class="sxs-lookup"><span data-stu-id="f4e78-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="f4e78-213">saída de Hello é atribuída a variável fictício tooa para que ele não está incluído na saída de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f4e78-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="f4e78-214">ativo de variável Olá com assinatura Olá ID, em seguida, é recuperada com **Get-AutomationVariable** e assinatura Olá com **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="f4e78-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="f4e78-215">Obter VMs</span><span class="sxs-lookup"><span data-stu-id="f4e78-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="f4e78-216">**Get-AzureVM** é usado tooretrieve máquinas virtuais de Olá Olá runbook funcionará com.</span><span class="sxs-lookup"><span data-stu-id="f4e78-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="f4e78-217">Se um valor é fornecido no hello **ServiceName** variável, em seguida, somente as máquinas virtuais do hello com esse nome de serviço são recuperadas de entrada.</span><span class="sxs-lookup"><span data-stu-id="f4e78-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="f4e78-218">Se **ServiceName** estiver vazia, todas as máquinas virtuais serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="f4e78-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="f4e78-219">Iniciar/parar as máquinas virtuais e enviar a saída</span><span class="sxs-lookup"><span data-stu-id="f4e78-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="f4e78-220">Olá Avançar linhas percorrer cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4e78-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="f4e78-221">Olá primeiro **PowerState** de saudação a máquina virtual está toosee verificado se ele já está em execução ou parado, dependendo da saudação runbook.</span><span class="sxs-lookup"><span data-stu-id="f4e78-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="f4e78-222">Se ele já está em estado de destino hello, uma mensagem é enviada toooutput e Olá runbook termina.</span><span class="sxs-lookup"><span data-stu-id="f4e78-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="f4e78-223">Se não, em seguida, **Start-AzureVM** ou **Stop-AzureVM** é tooattempt usado toostart ou parar Olá máquina virtual com o resultado da saudação da variável do hello solicitação tooa armazenado.</span><span class="sxs-lookup"><span data-stu-id="f4e78-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="f4e78-224">Uma mensagem é enviada toooutput especificando se Olá solicitação toostart ou parar foi enviada com êxito.</span><span class="sxs-lookup"><span data-stu-id="f4e78-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4e78-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4e78-225">Next steps</span></span>
* <span data-ttu-id="f4e78-226">toolearn mais sobre como trabalhar com runbooks filho, consulte [filho runbooks na automação do Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="f4e78-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="f4e78-227">Saiba mais sobre toolearn mensagens durante a execução de runbook e registro em log toohelp solucionar problemas, consulte [Runbook mensagens na automação do Azure e saída](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="f4e78-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

