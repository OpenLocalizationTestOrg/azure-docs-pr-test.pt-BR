---
title: "configurações de aaaCompiling no DSC de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como as configurações de configuração de estado desejado (DSC) toocompile para automação do Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="e8a6c-103">Compilando configurações no DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="e8a6c-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="e8a6c-104">Você pode compilar configurações de configuração de estado desejado (DSC) de duas maneiras na automação do Azure: no hello portal do Azure e com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="e8a6c-105">Olá tabela a seguir ajudam a determinar quando toouse qual método com base em características de saudação de cada um:</span><span class="sxs-lookup"><span data-stu-id="e8a6c-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e8a6c-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8a6c-106">Azure portal</span></span>

* <span data-ttu-id="e8a6c-107">Método mais simples com interface do usuário interativo</span><span class="sxs-lookup"><span data-stu-id="e8a6c-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="e8a6c-108">Valores de parâmetro simples do formulário tooprovide</span><span class="sxs-lookup"><span data-stu-id="e8a6c-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="e8a6c-109">Acompanhar facilmente o estado do trabalho</span><span class="sxs-lookup"><span data-stu-id="e8a6c-109">Easily track job state</span></span>
* <span data-ttu-id="e8a6c-110">Acesso autenticado com o logon do Azure</span><span class="sxs-lookup"><span data-stu-id="e8a6c-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="e8a6c-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-111">Windows PowerShell</span></span>

* <span data-ttu-id="e8a6c-112">Chame da linha de comando com os cmdlets do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="e8a6c-113">Pode ser incluído em uma solução automatizada com várias etapas</span><span class="sxs-lookup"><span data-stu-id="e8a6c-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="e8a6c-114">Fornece valores de parâmetro simples e complexos.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="e8a6c-115">Acompanha o estado do trabalho</span><span class="sxs-lookup"><span data-stu-id="e8a6c-115">Track job state</span></span>
* <span data-ttu-id="e8a6c-116">Cliente necessário toosupport cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="e8a6c-117">Transmitir ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="e8a6c-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="e8a6c-118">Compilar configurações que usam credenciais</span><span class="sxs-lookup"><span data-stu-id="e8a6c-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="e8a6c-119">Depois de decidir sobre um método de compilação, você pode seguir os procedimentos de respectivos de saudação abaixo toostart compilação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="e8a6c-120">Compilar uma configuração de DSC com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8a6c-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="e8a6c-121">Em sua conta de Automação, clique em **Configurações DSC**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="e8a6c-122">Clique em uma configuração tooopen sua folha.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="e8a6c-123">Clique em **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-123">Click **Compile**.</span></span>
4. <span data-ttu-id="e8a6c-124">Se a configuração de saudação não tiver parâmetros, será tooconfirm solicitada se você deseja toocompile-lo.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="e8a6c-125">Se a configuração de saudação tiver parâmetros, Olá **compilar configuração** folha será aberta para que possa fornecer os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="e8a6c-126">Consulte Olá [ **parâmetros básicos** ](#basic-parameters) seção abaixo para obter mais detalhes sobre os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="e8a6c-127">Olá **trabalho de compilação** folha é aberta para que você pode acompanhar o status do trabalho de compilação hello e hello configurações do nó (documentos MOF de configuração) causou toobe colocada em Olá servidor de Pull de DSC do Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="e8a6c-128">Compilando uma Configuração DSC com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="e8a6c-129">Você pode usar [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compilar com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="e8a6c-130">Olá, código de exemplo a seguir inicia a compilação de uma configuração DSC chamada **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="e8a6c-131">`Start-AzureRmAutomationDscCompilationJob`Retorna uma compilação que você pode usar tootrack seu status de objeto de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="e8a6c-132">Você pode usar esse objeto de trabalho de compilação com [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine status de saudação do trabalho de compilação de saudação e [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview seus fluxos (saída).</span><span class="sxs-lookup"><span data-stu-id="e8a6c-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="e8a6c-133">Olá, código de exemplo a seguir inicia a compilação de saudação **SampleConfig** configuração, aguarda até que ele foi concluído e exibe seus fluxos.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="e8a6c-134">Parâmetros básicos</span><span class="sxs-lookup"><span data-stu-id="e8a6c-134">Basic Parameters</span></span>
<span data-ttu-id="e8a6c-135">Declaração de parâmetro em configurações de DSC, incluindo tipos de parâmetro e propriedades, works Olá mesmo como runbooks de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="e8a6c-136">Consulte [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md) toolearn mais informações sobre parâmetros de runbook.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="e8a6c-137">Olá, exemplo a seguir usa dois parâmetros chamados **FeatureName** e **IsPresent**, valores de saudação toodetermine das propriedades Olá **ParametersExample.sample** nó configuração, gerada durante a compilação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="e8a6c-138">Você pode compilar configurações DSC que usam parâmetros básicos no portal de DSC de automação do Azure hello, ou com o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e8a6c-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="e8a6c-139">Portal</span><span class="sxs-lookup"><span data-stu-id="e8a6c-139">Portal</span></span>

<span data-ttu-id="e8a6c-140">No portal de saudação, você pode inserir valores de parâmetro depois de clicar em **compilar**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![texto alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="e8a6c-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-142">PowerShell</span></span>

<span data-ttu-id="e8a6c-143">PowerShell requer parâmetros em um [hashtable](http://technet.microsoft.com/library/hh847780.aspx) onde chave Olá corresponde o nome do parâmetro hello e Olá valor for igual a valor do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="e8a6c-144">Para obter informações sobre como transmitir PSCredentials como parâmetros, confira <a href="#credential-assets">**Ativos de credencial**</a> abaixo.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="e8a6c-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="e8a6c-145">ConfigurationData</span></span>
<span data-ttu-id="e8a6c-146">**ConfigurationData** permite a configuração estrutural tooseparate de qualquer configuração específica do ambiente durante o uso de DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="e8a6c-147">Consulte [separando "O que" de "Onde" PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn mais sobre **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a6c-148">Você pode usar **ConfigurationData** ao compilar no DSC de automação do Azure usando o PowerShell do Azure, mas não no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="e8a6c-149">Olá exemplo DSC configuração a seguir usa **ConfigurationData** via Olá **$ConfigurationData** e **$AllNodes** palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="e8a6c-150">Você também precisará Olá [ **xWebAdministration** módulo](https://www.powershellgallery.com/packages/xWebAdministration/) para este exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8a6c-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="e8a6c-151">Você pode compilar a configuração de DSC Olá acima com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="e8a6c-152">Olá abaixo do PowerShell adiciona dois toohello de configurações de nó servidor de Pull de DSC do Azure Automation: **ConfigurationDataSample.MyVM1** e **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="e8a6c-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="e8a6c-153">Ativos</span><span class="sxs-lookup"><span data-stu-id="e8a6c-153">Assets</span></span>

<span data-ttu-id="e8a6c-154">Referências de ativos são Olá mesmo em runbooks e as configurações DSC de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="e8a6c-155">Veja a seguir Olá para obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="e8a6c-155">See hello following for more information:</span></span>

* [<span data-ttu-id="e8a6c-156">Certificados</span><span class="sxs-lookup"><span data-stu-id="e8a6c-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="e8a6c-157">Conexões</span><span class="sxs-lookup"><span data-stu-id="e8a6c-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="e8a6c-158">Credenciais</span><span class="sxs-lookup"><span data-stu-id="e8a6c-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="e8a6c-159">Variáveis</span><span class="sxs-lookup"><span data-stu-id="e8a6c-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="e8a6c-160">Ativos de credencial</span><span class="sxs-lookup"><span data-stu-id="e8a6c-160">Credential Assets</span></span>

<span data-ttu-id="e8a6c-161">Embora as Configurações DSC na Automação do Azure possam fazer referência aos ativos de credencial usando **Get-AzureRmAutomationCredential**, os ativos de credencial também podem ser transmitidos por meio de parâmetros, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="e8a6c-162">Se uma configuração aceita um parâmetro de **PSCredential** digite, em seguida, é necessário o nome de cadeia de caracteres de saudação toopass de um ativo de credencial de automação do Azure como valores do parâmetro, em vez de um objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="e8a6c-163">Em segundo plano hello, ativo de credencial de automação do Azure Olá com esse nome será recuperado e passado toohello configuração.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="e8a6c-164">Manter credenciais segura em configurações do nó (documentos MOF de configuração) requer a criptografia de credenciais Olá no arquivo do MOF de configuração de nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="e8a6c-165">Automação do Azure vai ainda mais e criptografa o arquivo MOF inteiro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="e8a6c-166">No entanto, no momento você deve dizer DSC do PowerShell é okey para credenciais toobe enviada em texto sem formatação durante a geração do MOF de configuração de nó, porque DSC do PowerShell não sabe que automação do Azure será criptografar arquivo MOF inteiro de saudação após seu geração por meio de um trabalho de compilação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="e8a6c-167">Você pode informar DSC do PowerShell que é okey para credenciais toobe enviada em texto sem formatação na configuração de nó Olá gerado MOFs usando [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="e8a6c-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="e8a6c-168">Você deve passar `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** para o nome do bloco de cada nó que aparece na configuração de saudação DSC e usa credenciais.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="e8a6c-169">Olá, exemplo a seguir mostra uma configuração de DSC que usa um ativo de credencial de automação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="e8a6c-170">Você pode compilar a configuração de DSC Olá acima com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="e8a6c-171">Olá abaixo do PowerShell adiciona dois toohello de configurações de nó servidor de Pull de DSC do Azure Automation: **CredentialSample.MyVM1** e **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="e8a6c-172">Como importar configurações de nó</span><span class="sxs-lookup"><span data-stu-id="e8a6c-172">Importing node configurations</span></span>

<span data-ttu-id="e8a6c-173">Você também pode importar configurações de nó (MOFs) que você compilou fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="e8a6c-174">Uma das vantagens disso é que as configurações de nó podem ser assinadas.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="e8a6c-175">Uma configuração de nó assinado é verificada localmente em um nó gerenciado por agente Olá DSC, garantindo que a configuração hello está sendo aplicada toohello nó vem de uma origem autorizada.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a6c-176">Você pode importar configurações assinadas em sua conta de Automação do Azure, mas a Automação do Azure não oferece suporte à compilação de configurações assinadas.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a6c-177">Um arquivo de configuração do nó não deve ser maior que 1 MB tooallow-toobe importado para a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="e8a6c-178">Você pode aprender como configurações do nó toosign em https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="e8a6c-179">Importar uma configuração de nó no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8a6c-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="e8a6c-180">Em sua conta de Automação, clique em **Configurações do nó DSC**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configurações de nó DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="e8a6c-182">Em Olá **configurações do nó DSC** folha, clique em **adicionar um NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="e8a6c-183">Em Olá **importação** folha, clique Olá pasta ícone próximo toohello **arquivo de configuração de nó** toobrowse da caixa de texto para um arquivo de configuração de nó (MOF) em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Procurar arquivo local](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="e8a6c-185">Insira um nome no hello **nome da configuração** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="e8a6c-186">Esse nome deve corresponder a saudação nome da configuração de saudação do qual a configuração do nó Olá foi compilada.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="e8a6c-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="e8a6c-188">Importar uma configuração de nó com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a6c-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="e8a6c-189">Você pode usar o hello [AzureRmAutomationDscNodeConfiguration importação](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport uma configuração de nó em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e8a6c-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



