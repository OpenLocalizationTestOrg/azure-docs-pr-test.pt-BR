---
title: "aaaRun runbooks no Hybrid Runbook Worker de automação do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre runbooks em execução em computadores em seu datacenter local ou o provedor de nuvem com a função de operador de Runbook híbrido hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="8f3eb-103">Executar runbooks em um Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="8f3eb-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="8f3eb-104">Não há nenhuma diferença na estrutura de saudação de runbooks que são executados na automação do Azure e aqueles que são executados em um trabalho de Runbook híbrido.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="8f3eb-105">Runbooks que você pode usar com cada provavelmente diferem significativamente embora como runbooks direcionando um Hybrid Runbook Worker normalmente gerenciar recursos no computador local de saudação em si ou a recursos no ambiente local hello, onde ele é implantado, enquanto runbooks na automação do Azure normalmente gerencie recursos em Olá nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="8f3eb-106">Você pode editar um runbook para Hybrid Runbook Worker na automação do Azure, mas você pode ter problemas se você tentar tootest Olá runbook no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="8f3eb-107">módulos do PowerShell Olá que acessam recursos locais Olá talvez não esteja instalados em seu ambiente de automação do Azure nesse caso, o teste de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="8f3eb-108">Se você instalar Olá necessário módulos, em seguida, Olá runbook será executado, mas não será capaz de tooaccess recursos locais para um teste completo.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="8f3eb-109">Iniciar um runbook no Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="8f3eb-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="8f3eb-110">[Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md) descreve métodos diferentes para se iniciar um runbook.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="8f3eb-111">Hybrid Runbook Worker adiciona um **RunOn** opção onde você pode especificar o nome de saudação de um grupo de trabalho de Runbook híbrido.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="8f3eb-112">Se um grupo for especificado, Olá runbook é recuperado e executando de trabalhadores Olá nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="8f3eb-113">Se essa opção não for especificada, ele é executado na Automação do Azure como de costume.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="8f3eb-114">Quando você iniciar um runbook no hello portal do Azure, você verá um **executados em** opção onde você pode selecionar **Azure** ou **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="8f3eb-115">Se você selecionar **Hybrid Worker**, em seguida, você pode selecionar o grupo de saudação em uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="8f3eb-116">Saudação de uso **RunOn** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="8f3eb-117">Você pode usar o hello comando toostart um runbook chamado Test-Runbook em um grupo do Hybrid Runbook Worker denominado MyHybridGroup usando o Windows PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="8f3eb-118">Olá **RunOn** parâmetro foi adicionado toohello **Start-AzureAutomationRunbook** cmdlet na versão 0.9.1 do Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="8f3eb-119">Você deve [baixar a versão mais recente do hello](https://azure.microsoft.com/downloads/) se você tiver uma anterior instalada.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="8f3eb-120">Você só precisa tooinstall esta versão em uma estação de trabalho onde você está iniciando o runbook de saudação do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="8f3eb-121">Não é necessário tooinstall-lo no computador de trabalho hello, a menos que você pretende runbooks toostart desse computador.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="8f3eb-122">Atualmente você não pode iniciar um runbook em um trabalho de Runbook híbrido de outro runbook, pois isso exigiria a versão mais recente de saudação do Azure Powershell toobe instalado na sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="8f3eb-123">versão mais recente da saudação é atualizado automaticamente na automação do Azure e automaticamente propagada toohello trabalhadores em breve.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="8f3eb-124">Permissões de runbook</span><span class="sxs-lookup"><span data-stu-id="8f3eb-124">Runbook permissions</span></span>
<span data-ttu-id="8f3eb-125">Runbooks em execução em um trabalho de Runbook híbrido não é possível usar Olá mesmo método que é normalmente usado para runbooks autenticando tooAzure recursos, desde que eles acessam recursos fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="8f3eb-126">Olá runbook pode fornecer sua própria autenticação toolocal recursos, ou você pode especificar uma conta de RunAs tooprovide um contexto de usuário para todos os runbooks.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="8f3eb-127">Autenticação de runbook</span><span class="sxs-lookup"><span data-stu-id="8f3eb-127">Runbook authentication</span></span>
<span data-ttu-id="8f3eb-128">Por padrão, os runbooks serão executados no contexto Olá Olá conta de sistema local no computador do local de hello, para que eles devem fornecer suas próprias tooresources de autenticação que eles acessarão.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="8f3eb-129">Você pode usar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) e [certificado](http://msdn.microsoft.com/library/dn940013.aspx) ativos no seu runbook com os cmdlets que permitem que você toospecify credenciais para autenticar o toodifferent recursos.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="8f3eb-130">Olá, exemplo a seguir mostra uma parte de um runbook que reinicia um computador.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="8f3eb-131">Ele recupera as credenciais de um nome de ativo e hello de credencial do computador de saudação de um ativo de variável e, em seguida, usa esses valores com hello Restart-Computer cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="8f3eb-132">Você também pode aproveitar [InlineScript](automation-powershell-workflow.md#inlinescript), que permite que você toorun blocos de código em outro computador com as credenciais especificadas pelo Olá [parâmetro comum PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f3eb-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="8f3eb-133">Conta RunAs</span><span class="sxs-lookup"><span data-stu-id="8f3eb-133">RunAs account</span></span>
<span data-ttu-id="8f3eb-134">Em vez de ter runbooks fornecer sua própria autenticação toolocal recursos, você pode especificar um **RunAs** conta para um grupo do Hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="8f3eb-135">Você especifica um [ativo de credencial](automation-credentials.md) que tenha acesso toolocal recursos, e todos os runbooks são executados sob essas credenciais ao executar em um trabalho de Runbook híbrido em grupo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="8f3eb-136">nome de usuário Olá credencial Olá deve ter uma saudação formatos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f3eb-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="8f3eb-137">domínio\nome de usuário</span><span class="sxs-lookup"><span data-stu-id="8f3eb-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="8f3eb-138">nome de usuário (para contas locais toohello, computador local)</span><span class="sxs-lookup"><span data-stu-id="8f3eb-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="8f3eb-139">Use Olá seguindo o procedimento toospecify uma conta executar como para um grupo do Hybrid worker:</span><span class="sxs-lookup"><span data-stu-id="8f3eb-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="8f3eb-140">Criar um [ativo de credencial](automation-credentials.md) com toolocal acessar os recursos.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="8f3eb-141">Abra conta de automação Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="8f3eb-142">Selecione Olá **grupos de trabalho híbrida** lado a lado e, em seguida, selecione o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="8f3eb-143">Escolha **Todas as configurações** e **Configurações do grupo do Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="8f3eb-144">Alterar **executar como** de **padrão** muito**personalizado**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="8f3eb-145">Selecione a credencial hello e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="8f3eb-146">Conta de automação Executar como</span><span class="sxs-lookup"><span data-stu-id="8f3eb-146">Automation Run As account</span></span>
<span data-ttu-id="8f3eb-147">Como parte do processo de compilação automatizado para implantação de recursos no Azure, você pode exigir acesso local tooon sistemas toosupport uma tarefa ou um conjunto de etapas na sequência de implantação.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="8f3eb-148">autenticação toosupport no Azure usando a conta executar como do hello, é necessário tooinstall Olá executar como certificado de conta.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="8f3eb-149">Olá runbook do PowerShell a seguir *RunAsCertificateToHybridWorker de exportação*, exporta Olá executar como certificado de sua conta de automação do Azure e downloads e importa-o para o repositório de certificados do computador local Olá em um Operador híbrido conectado toohello mesma conta.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="8f3eb-150">Após essa etapa é concluída, ela verifica trabalho Olá pode autenticar com êxito tooAzure usando Olá a conta executar como.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="8f3eb-151">Salvar Olá *RunAsCertificateToHybridWorker de exportação* runbook tooyour computador com um `.ps1` extensão.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="8f3eb-152">Importe-o para sua conta de automação e editar runbook hello, alterar valor variável Olá Olá `$Password` com sua própria senha.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="8f3eb-153">Publicar e, em seguida, executar runbook Olá direcionando o grupo do Hybrid Worker Olá que executam o e autenticar usando a conta executar como da saudação de runbooks.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="8f3eb-154">Olá trabalho fluxo relatórios Olá tentativa tooimport Olá certificado no repositório de computador local hello e segue com várias linhas, dependendo do número de contas de automação é definido em sua assinatura e se a autenticação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="8f3eb-155">Solucionando problemas de runbooks no Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="8f3eb-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="8f3eb-156">Os logs são armazenados localmente em cada hybrid worker, em C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="8f3eb-157">Operador híbrido também registra erros e eventos no log de eventos do Windows hello em **aplicativos e serviços Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="8f3eb-158">Eventos relacionados toorunbooks executados no trabalho de saudação são gravados muito**aplicativos e serviços Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="8f3eb-159">Olá **Microsoft SMA** log inclui muitos mais eventos relacionados toohello runbook trabalho toohello enviadas por push hello e trabalho processamento de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="8f3eb-160">Durante a saudação **automação do Microsoft** log de eventos não tem muitos eventos com detalhes para ajudar com a saudação de solução de problemas de execução de runbook, pelo menos, você encontrará resultados Olá Olá do trabalho de runbook.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="8f3eb-161">[Mensagens e saída de runbook](automation-runbook-output-and-messages.md) são enviadas tooAzure automação de operadores híbrido apenas como trabalhos de runbook executados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="8f3eb-162">Você também pode habilitar Olá detalhado e fluxos de andamento Olá mesma maneira que faria para outros runbooks.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="8f3eb-163">Se seus runbooks não são concluídas com êxito e o resumo do trabalho de saudação mostra um status de **suspenso**, examine o artigo de solução de problemas de saudação [Hybrid Runbook Worker: um trabalho de runbook termina com um status de Suspenso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="8f3eb-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="8f3eb-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f3eb-164">Next steps</span></span>
* <span data-ttu-id="8f3eb-165">toolearn mais sobre métodos diferentes de saudação que pode ser usado toostart um runbook, consulte [iniciando um Runbook na automação do Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="8f3eb-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="8f3eb-166">toounderstand Olá diferentes procedimentos para trabalhar com runbooks do PowerShell e fluxo de trabalho do PowerShell na automação do Azure usando o editor de texto hello, consulte [editando um Runbook na automação do Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="8f3eb-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
