---
title: "Execute runbooks no Hybrid Runbook Workers da Automação do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre a execução de runbooks em computadores em seu datacenter local ou provedor de nuvem com a função de Hybrid Runbook Worker."
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
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="33ee7-103">Executar runbooks em um Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="33ee7-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="33ee7-104">Não há nenhuma diferença na estrutura de runbooks executados na Automação do Azure e daqueles que executam em um Runbook Worker Híbrido.</span><span class="sxs-lookup"><span data-stu-id="33ee7-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="33ee7-105">Os runbooks que você usar com cada um provavelmente serão bem diferentes uns dos outros, já que os runbooks direcionados a um Hybrid Runbook Worker normalmente gerenciam recursos no próprio computador local ou em recursos no ambiente local onde é implantado, enquanto runbooks na Automação do Azure normalmente gerenciam recursos na nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ee7-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="33ee7-106">Você pode editar um runbook para Runbook Worker Híbrido na Automação do Azure, mas pode ter problemas se tentar testá-lo no editor.</span><span class="sxs-lookup"><span data-stu-id="33ee7-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="33ee7-107">Os módulos do PowerShell que acessam os recursos locais podem não estar instalados em seu ambiente de Automação do Azure. Nesse caso, o teste falhará.</span><span class="sxs-lookup"><span data-stu-id="33ee7-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="33ee7-108">Se você instalar os módulos necessários, o runbook será executado, mas não será capaz de acessar recursos locais para um teste completo.</span><span class="sxs-lookup"><span data-stu-id="33ee7-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="33ee7-109">Iniciar um runbook no Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="33ee7-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="33ee7-110">[Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md) descreve métodos diferentes para se iniciar um runbook.</span><span class="sxs-lookup"><span data-stu-id="33ee7-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="33ee7-111">O Runbook Worker Híbrido adiciona uma opção **RunOn** em que você pode especificar o nome de um Grupo de Runbook Worker Híbrido.</span><span class="sxs-lookup"><span data-stu-id="33ee7-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="33ee7-112">Se um grupo for especificado, o runbook é recuperado e executado pelos trabalhadores nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="33ee7-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="33ee7-113">Se essa opção não for especificada, ele é executado na Automação do Azure como de costume.</span><span class="sxs-lookup"><span data-stu-id="33ee7-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="33ee7-114">Ao iniciar um runbook no portal do Azure, a opção **Executar em** ficará disponível e você poderá selecionar **Azure** ou **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="33ee7-115">Se você selecionar **Worker Híbrido**, pode selecionar o grupo de uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="33ee7-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="33ee7-116">Use o parâmetro **RunOn**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="33ee7-117">Você pode usar o comando a seguir para iniciar um runbook denominado Runbook de Teste em um Grupo Hybrid Runbook Worker chamado MyHybridGroup usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ee7-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="33ee7-118">O parâmetro **RunOn** foi adicionado ao cmdlet **Start-AzureAutomationRunbook** na versão 0.9.1 do Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ee7-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="33ee7-119">Você deve [baixar a versão mais recente](https://azure.microsoft.com/downloads/) se tiver uma anterior instalada.</span><span class="sxs-lookup"><span data-stu-id="33ee7-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="33ee7-120">Você só precisa instalar essa versão em uma estação de trabalho em que vá iniciar o runbook do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ee7-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="33ee7-121">Você não precisa instalá-lo no computador de trabalho, a menos que pretenda iniciar runbooks desse computador.</span><span class="sxs-lookup"><span data-stu-id="33ee7-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="33ee7-122">Atualmente, você não pode iniciar um runbook em um Runbook Worker Híbrido de outro runbook, pois isso exigiria que a versão mais recente do Powershell do Azure estivesse instalada em sua Conta de automação.</span><span class="sxs-lookup"><span data-stu-id="33ee7-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="33ee7-123">A versão mais recente será automaticamente atualizada na Automação do Azure e enviada aos trabalhadores em breve.</span><span class="sxs-lookup"><span data-stu-id="33ee7-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="33ee7-124">Permissões de runbook</span><span class="sxs-lookup"><span data-stu-id="33ee7-124">Runbook permissions</span></span>
<span data-ttu-id="33ee7-125">Os runbooks em execução em um Hybrid Runbook Worker não podem usar o mesmo método que é normalmente usado para autenticação de runbooks nos recursos do Azure, já que eles acessarão recursos fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ee7-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="33ee7-126">O runbook pode fornecer sua própria autenticação aos recursos locais, ou você pode especificar uma conta RunAs para fornecer um contexto de usuário a todos os runbooks.</span><span class="sxs-lookup"><span data-stu-id="33ee7-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="33ee7-127">Autenticação de runbook</span><span class="sxs-lookup"><span data-stu-id="33ee7-127">Runbook authentication</span></span>
<span data-ttu-id="33ee7-128">Por padrão, os runbooks serão executados no contexto da conta de Sistema local no computador local; portanto, eles devem fornecer sua própria autenticação aos recursos que acessarão.</span><span class="sxs-lookup"><span data-stu-id="33ee7-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="33ee7-129">Você pode usar ativos de [Credencial](http://msdn.microsoft.com/library/dn940015.aspx) e [Certificado](http://msdn.microsoft.com/library/dn940013.aspx) no runbook com cmdlets que permitem a especificação das credenciais para autenticar com recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="33ee7-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="33ee7-130">O exemplo a seguir mostra uma parte de um runbook que reinicia um computador.</span><span class="sxs-lookup"><span data-stu-id="33ee7-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="33ee7-131">Ele recupera as credenciais de um ativo de credencial e o nome do computador de um ativo variável, para então usar esses valores com o cmdlet Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="33ee7-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="33ee7-132">Você também pode aproveitar o [InlineScript](automation-powershell-workflow.md#inlinescript), que permitirá a execução de blocos de código em outro computador com as credenciais especificadas pelo [parâmetro comum PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="33ee7-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="33ee7-133">Conta RunAs</span><span class="sxs-lookup"><span data-stu-id="33ee7-133">RunAs account</span></span>
<span data-ttu-id="33ee7-134">Em vez de os runbooks fornecerem sua própria autenticação aos recursos locais, você pode especificar uma conta **RunAs** para um grupo Hybrid Worker.</span><span class="sxs-lookup"><span data-stu-id="33ee7-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="33ee7-135">Você especifica um [ativo de credencial](automation-credentials.md) que tenha acesso aos recursos locais e todos os runbooks serão executados sob essas credenciais ao serem executados em um Hybrid Runbook Worker no grupo.</span><span class="sxs-lookup"><span data-stu-id="33ee7-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="33ee7-136">O nome de usuário da credencial deve estar em um dos seguintes formatos:</span><span class="sxs-lookup"><span data-stu-id="33ee7-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="33ee7-137">domínio\nome de usuário</span><span class="sxs-lookup"><span data-stu-id="33ee7-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="33ee7-138">nome de usuário (para contas locais do computador local)</span><span class="sxs-lookup"><span data-stu-id="33ee7-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="33ee7-139">Use o procedimento a seguir para especificar uma conta RunAs para um grupo do Hybrid Worker:</span><span class="sxs-lookup"><span data-stu-id="33ee7-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="33ee7-140">Crie um [ativo de credencial](automation-credentials.md) com acesso a recursos locais.</span><span class="sxs-lookup"><span data-stu-id="33ee7-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="33ee7-141">Abra a conta de Automação no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33ee7-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="33ee7-142">Escolha o bloco **Grupos do Hybrid Worker** e selecione o grupo.</span><span class="sxs-lookup"><span data-stu-id="33ee7-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="33ee7-143">Escolha **Todas as configurações** e **Configurações do grupo do Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="33ee7-144">Altere **Executar como** de **Padrão** para **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="33ee7-145">Escolha a credencial e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="33ee7-146">Conta de automação Executar como</span><span class="sxs-lookup"><span data-stu-id="33ee7-146">Automation Run As account</span></span>
<span data-ttu-id="33ee7-147">Como parte do processo de compilação automatizado para a implantação de recursos no Azure, você talvez precise acessar os sistemas no local para dar suporte a uma tarefa ou um conjunto de etapas na sequência de implantação.</span><span class="sxs-lookup"><span data-stu-id="33ee7-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="33ee7-148">Para dar suporte à autenticação no Azure usando a conta Executar como, você precisa instalar o certificado da conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="33ee7-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="33ee7-149">O runbook do PowerShell a seguir, *Export-RunAsCertificateToHybridWorker*, exporta o certificado de Executar como de sua conta de Automação do Azure e baixa e importa para o repositório de certificados do computador local em um Hybrid Worker conectado à mesma conta.</span><span class="sxs-lookup"><span data-stu-id="33ee7-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="33ee7-150">Quando essa etapa for concluída, ele verificará que o Worker pode ser autenticado com sucesso no Azure usando a conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="33ee7-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

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
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="33ee7-151">Salve o runbook *Export-RunAsCertificateToHybridWorker* no seu computador com uma extensão `.ps1`.</span><span class="sxs-lookup"><span data-stu-id="33ee7-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="33ee7-152">Importe-o para sua conta de Automação e edite o runbook, alterando o valor da variável `$Password` pela sua própria senha.</span><span class="sxs-lookup"><span data-stu-id="33ee7-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="33ee7-153">Publique e, em seguida, execute o runbook direcionando o grupo Hybrid Worker que executa e autentica runbooks usando a conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="33ee7-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="33ee7-154">O fluxo de trabalho informa a tentativa de importar o certificado para o armazenamento do computador local e vem com várias linhas, dependendo de quantas contas de Automação são definidas em sua assinatura e se a autenticação tiver sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="33ee7-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="33ee7-155">Solucionando problemas de runbooks no Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="33ee7-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="33ee7-156">Os logs são armazenados localmente em cada hybrid worker, em C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="33ee7-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="33ee7-157">O Hybrid Worker também registra erros e eventos no log de eventos do Windows em **Logs de Aplicativos e Serviços\Microsoft-SMA\Operacional**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="33ee7-158">Eventos relacionados a runbooks executados no worker são gravados em **Logs de Aplicativos e Serviços\Microsoft-Automation\Operacional**.</span><span class="sxs-lookup"><span data-stu-id="33ee7-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="33ee7-159">O log **Microsoft SMA** inclui muitos outros eventos relacionados ao trabalho de runbook enviado por push para o worker e ao processamento do runbook.</span><span class="sxs-lookup"><span data-stu-id="33ee7-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="33ee7-160">Embora o log de eventos de **Microsoft-Automation** não tenha muitos eventos com detalhes para ajudar na solução de problemas de execução de runbooks, você pelo menos encontrará os resultados do trabalho de runbook.</span><span class="sxs-lookup"><span data-stu-id="33ee7-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="33ee7-161">[A saída e as mensagens do runbook](automation-runbook-output-and-messages.md) são enviadas à Automação do Azure do Hybrid Workers assim como os trabalhos do runbook são executados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="33ee7-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="33ee7-162">Também é possível habilitar os fluxos Verbose e Progress da mesma forma que você faria para outros runbooks.</span><span class="sxs-lookup"><span data-stu-id="33ee7-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="33ee7-163">Se seus runbooks não forem concluídos com êxito e o resumo do trabalho mostrar um status **Suspenso**, leia o artigo de solução de problemas [Hybrid Runbook Worker: um trabalho de runbook termina com o status Suspenso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="33ee7-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="33ee7-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33ee7-164">Next steps</span></span>
* <span data-ttu-id="33ee7-165">Para saber mais sobre os diferentes métodos que podem ser usados para iniciar um runbook, confira [Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="33ee7-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="33ee7-166">Para entender os diferentes procedimentos para trabalhar com runbooks do PowerShell e de Fluxo de Trabalho do PowerShell na Automação do Azure usando o editor de texto, confira [Editar um Runbook na Automação do Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="33ee7-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>