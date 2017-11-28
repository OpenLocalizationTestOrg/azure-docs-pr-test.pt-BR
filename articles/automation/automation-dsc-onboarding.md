---
title: "aaaOnboarding máquinas para o gerenciamento de DSC de automação do Azure | Microsoft Docs"
description: "Como toosetup máquinas para o gerenciamento com DSC de automação do Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="bfeb6-103">Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="bfeb6-104">Por que gerenciar máquinas com o DSC de Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="bfeb6-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="bfeb6-105">Como a [Configuração de Estado Desejado do PowerShell](https://technet.microsoft.com/library/dn249912.aspx), a Configuração de Estado Desejado da Automação do Azure é um serviço de gerenciamento de configuração simples, mas poderoso, para nós DSC (máquinas físicas e virtuais) em qualquer datacenter de nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="bfeb6-106">Ela permite a escalabilidade entre milhares de máquinas rápida e facilmente a partir de um local central e seguro.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="bfeb6-107">Você pode facilmente integradas máquinas, atribuir configurações declarativas, além de exibir relatórios mostrando cada máquina do estado de toohello desejado de conformidade especificado.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="bfeb6-108">camada de gerenciamento de DSC de automação do Azure Olá é tooDSC qual camada de gerenciamento de automação do Azure Olá é tooPowerShell script.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="bfeb6-109">Em outras palavras, Olá mesma forma que a automação do Azure ajuda a gerenciar scripts do PowerShell, ele também ajuda a gerenciar configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="bfeb6-110">toolearn mais sobre os benefícios de saudação do uso de DSC de automação do Azure, consulte [visão geral de DSC de automação do Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfeb6-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="bfeb6-111">DSC de automação do Azure pode ser usado toomanage várias máquinas:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="bfeb6-112">Máquinas virtuais do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="bfeb6-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="bfeb6-113">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-113">Azure virtual machines</span></span>
* <span data-ttu-id="bfeb6-114">Máquinas virtuais do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="bfeb6-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="bfeb6-115">Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="bfeb6-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="bfeb6-116">Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="bfeb6-117">Além disso, se você não estiver pronto toomanage a configuração de máquina da nuvem Olá, DSC de automação do Azure também pode ser usado como um ponto de extremidade somente de relatório.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="bfeb6-118">Isso permite a configuração desejada tooset (push) por meio do local do DSC e exibir detalhes de relatório avançados sobre a conformidade de nó com hello desejado estado na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="bfeb6-119">Olá seções a seguir descrevem como você pode integrar cada tipo de máquina tooAzure DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="bfeb6-120">Máquinas virtuais do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="bfeb6-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="bfeb6-121">Com DSC de automação do Azure, você pode facilmente integradas máquinas virtuais do Azure (clássica) para gerenciamento de configuração usando Olá portal do Azure, ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="bfeb6-122">Bastidores hello e sem um administrador que tem tooremote em Olá VM, Olá extensão de configuração de estado desejado do Azure VM registra Olá VM com DSC de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="bfeb6-123">Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, as etapas tootrack seu progresso ou solucionar problemas ele são fornecidas nos Olá [ **integração de máquina virtual do Azure de solução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="bfeb6-124">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-124">Azure portal</span></span>

<span data-ttu-id="bfeb6-125">Em Olá [portal do Azure](http://portal.azure.com/), clique em **procurar** -> **máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="bfeb6-126">Selecione Olá VM do Windows que você deseja tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="bfeb6-127">Na folha de painel Olá máquina virtual, clique em **todas as configurações** -> **extensões** -> **adicionar**  ->   **DSC de automação do Azure** -> **criar**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="bfeb6-128">Digite hello [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para seu caso de uso, chave de registro da sua conta de automação e URL de registro e, opcionalmente, um toohello de tooassign de configuração do nó VM.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="bfeb6-129">URL de registro toofind hello e chave Olá automação conta tooonboard Olá máquina, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="bfeb6-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfeb6-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="bfeb6-131">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-131">Azure virtual machines</span></span>

<span data-ttu-id="bfeb6-132">DSC de automação do Azure permite integradas facilmente máquinas virtuais do Azure para gerenciamento de configuração, usando Olá portal do Azure, modelos do Azure Resource Manager ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="bfeb6-133">Bastidores hello e sem um administrador que tem tooremote em Olá VM, Olá extensão de configuração de estado desejado do Azure VM registra Olá VM com DSC de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="bfeb6-134">Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, as etapas tootrack seu progresso ou solucionar problemas ele são fornecidas nos Olá [ **integração de máquina virtual do Azure de solução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="bfeb6-135">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-135">Azure portal</span></span>

<span data-ttu-id="bfeb6-136">Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello conta de automação do Azure onde deseja que as máquinas virtuais de tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="bfeb6-137">No painel da conta de automação hello, clique em **nós DSC** -> **adicionar a máquina virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="bfeb6-138">Em **selecionar máquinas virtuais tooonboard**, selecione um ou tooonboard de máquinas virtuais do Azure mais.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="bfeb6-139">Em **configurar dados de registro**, digite Olá [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para seu caso de uso e, opcionalmente, um toohello de tooassign de configuração do nó VM.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="bfeb6-140">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="bfeb6-141">Máquinas virtuais do Azure pode ser implantadas e incorporados tooAzure DSC de automação por meio de modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="bfeb6-142">Consulte [configurar uma VM por meio da extensão de DSC e DSC de automação do Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para um modelo de exemplo que onboards um tooAzure VM existente DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="bfeb6-143">toofind Olá chave e registro de URL de registro feito como entrada nesse modelo, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="bfeb6-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfeb6-144">PowerShell</span></span>

<span data-ttu-id="bfeb6-145">Olá [AzureRmAutomationDscNode registro](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet pode ser usado tooonboard máquinas virtuais Olá portal do Azure por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="bfeb6-146">Máquinas virtuais do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="bfeb6-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="bfeb6-147">Você pode facilmente integradas máquinas virtuais de Amazon Web Services para o gerenciamento de configuração DSC de automação do Azure usando Olá AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="bfeb6-148">Você pode aprender mais sobre o Kit de ferramentas de saudação [aqui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="bfeb6-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="bfeb6-149">Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="bfeb6-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="bfeb6-150">As máquinas do Windows local e máquinas do Windows Azure não nuvens (como Amazon Web Services) também podem ser incorporados tooAzure DSC de automação, desde que eles têm acesso de saída toohello internet, por meio de algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="bfeb6-151">Certifique-se de que versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) está instalado nos computadores de saudação desejado tooonboard tooAzure DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="bfeb6-152">Siga as instruções de saudação na seção [ **gerando DSC metaconfigurações** ](#generating-dsc-metaconfigurations) abaixo toogenerate uma pasta que contém a saudação necessário metaconfigurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="bfeb6-153">Aplica remotamente as máquinas de toohello metaconfiguração PowerShell DSC Olá deseja tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="bfeb6-154">**máquina de saudação este comando é executado no deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado**:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="bfeb6-155">Se você não pode aplicar Olá PowerShell DSC metaconfigurações remotamente, copie a pasta de metaconfigurações de saudação da etapa 2 para cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="bfeb6-156">Em seguida, chame **Set-DscLocalConfigurationManager** localmente em cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="bfeb6-157">Usando Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora são mostrados como nós DSC registrado em sua conta de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="bfeb6-158">Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="bfeb6-159">Linux local máquinas, máquinas Linux no Azure, e máquinas Linux no Azure não nuvens também podem ser incorporados tooAzure DSC de automação, desde que eles têm acesso de saída toohello internet, por meio de algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="bfeb6-160">Certifique-se de que versão mais recente de saudação do [configuração de estado desejado do PowerShell para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado nos computadores de saudação desejado tooonboard tooAzure DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="bfeb6-161">Se hello [padrões do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) diferenciar maiusculas de minúsculas seu uso e você desejar tooonboard máquinas tal que elas **ambos** por pull e relatar tooAzure DSC de automação:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="bfeb6-162">Em cada Linux máquina tooonboard tooAzure DSC de automação, use tooonboard Register.py usando Olá padrões do Gerenciador de configurações de Local de DSC do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="bfeb6-163">toofind Olá chave e registro de URL de registro para sua conta de automação, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="bfeb6-164">Padrões do Gerenciador de configuração Local do PowerShell DSC se hello **fazer** **não** diferenciar maiusculas de minúsculas seu uso, ou se desejar tooonboard máquinas, de modo que eles só tooAzure DSC de automação de relatório, mas não pull configuração ou módulos do PowerShell, execute as etapas 3 a 6.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="bfeb6-165">Caso contrário, vá diretamente toostep 6.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="bfeb6-166">Siga as instruções de Olá Olá [ **gerando DSC metaconfigurações** ](#generating-dsc-metaconfigurations) seção abaixo toogenerate uma pasta que contém a saudação necessário metaconfigurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="bfeb6-167">Aplicam-se remotamente as máquinas de toohello metaconfiguração PowerShell DSC Olá deseja tooonboard:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="bfeb6-168">máquina de saudação este comando é executado no deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="bfeb6-169">Se você não pode aplicar Olá PowerShell DSC metaconfigurações remotamente, para cada tooonboard de máquina do Linux, copie máquina de toothat Olá metaconfiguração correspondente da pasta de saudação na etapa 5 no computador do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="bfeb6-170">Em seguida, chame `SetDscLocalConfigurationManager.py` localmente em cada computador Linux, você deseja tooonboard tooAzure DSC de automação:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="bfeb6-171">Usando Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora são mostrados como nós DSC registrado em sua conta de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="bfeb6-172">Gerando metaconfigurações DSC</span><span class="sxs-lookup"><span data-stu-id="bfeb6-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="bfeb6-173">toogenerically integrar qualquer máquina tooAzure DSC de automação, um [metaconfiguração do DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) pode ser gerado que, quando aplicada, informa ao agente Olá DSC no hello máquina toopull de e/ou reportar tooAzure DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="bfeb6-174">DSC metaconfigurações para DSC de automação do Azure podem ser geradas usando uma configuração de DSC do PowerShell ou cmdlets do PowerShell do Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="bfeb6-175">Metaconfigurações de DSC contêm Olá segredos necessário tooonboard um tooan conta de automação de gerenciamento do computador.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="bfeb6-176">Verifique se tooproperly proteger qualquer metaconfigurações de DSC que você criar ou excluí-los após o uso.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="bfeb6-177">Usando uma Configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="bfeb6-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="bfeb6-178">Abra Olá ISE do PowerShell como administrador em um computador no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="bfeb6-179">máquina de saudação deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="bfeb6-180">Saudação de cópia localmente o script a seguir.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-180">Copy hello following script locally.</span></span> <span data-ttu-id="bfeb6-181">Esse script contém uma configuração de DSC do PowerShell para criar metaconfigurações e tookick um comando desativar a criação de metaconfiguração hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="bfeb6-182">Preencha chave de registro hello e URL para sua conta de automação, bem como os nomes de saudação do hello máquinas tooonboard.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="bfeb6-183">Todos os outros parâmetros são opcionais.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-183">All other parameters are optional.</span></span> <span data-ttu-id="bfeb6-184">toofind Olá chave e registro de URL de registro para sua conta de automação, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="bfeb6-185">Se você quiser Olá máquinas tooreport DSC status informações tooAzure DSC de automação, mas não pull de configuração ou módulos do PowerShell, defina Olá **ReportOnly** tootrue de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="bfeb6-186">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-186">Run hello script.</span></span> <span data-ttu-id="bfeb6-187">Agora você deve ter uma pasta chamada **DscMetaConfigs** no diretório de trabalho, contendo Olá metaconfigurações de DSC do PowerShell para Olá máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="bfeb6-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="bfeb6-188">Usando os cmdlets de automação do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="bfeb6-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="bfeb6-189">Se os padrões do Gerenciador de configuração Local do PowerShell DSC Olá corresponderem seu caso de uso, e você deseja que as máquinas de tooonboard, de modo que eles tanto por pull e relatam tooAzure DSC de automação, Olá cmdlets de automação do Azure fornecem um método simplificado de geração de saudação DSC metaconfigurações necessário:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="bfeb6-190">Abra o console do PowerShell hello ou ISE do PowerShell como administrador em uma máquina no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="bfeb6-191">Conecte-se usando o Gerenciador de recursos tooAzure **AzureRmAccount adicionar**</span><span class="sxs-lookup"><span data-stu-id="bfeb6-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="bfeb6-192">Baixe Olá DSC do PowerShell metaconfigurações para máquinas Olá deseja tooonboard de saudação automação conta toowhich que você deseja que os nós de tooonboard:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="bfeb6-193">Agora você deve ter uma pasta chamada ***DscMetaConfigs***, que contém a saudação metaconfigurações de DSC do PowerShell para Olá máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="bfeb6-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="bfeb6-194">Proteger o registro</span><span class="sxs-lookup"><span data-stu-id="bfeb6-194">Secure registration</span></span>

<span data-ttu-id="bfeb6-195">Máquinas podem tooan com segurança integrada conta de automação do Azure por meio do protocolo de registro do WMF 5 DSC saudação, que permite que um nó tooauthenticate tooa PowerShell DSC V2 Pull ou relatórios servidor DSC (incluindo DSC de automação do Azure).</span><span class="sxs-lookup"><span data-stu-id="bfeb6-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="bfeb6-196">nó Olá registra toohello server em uma **URL de registro**, autenticação usando um **chave de registro**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="bfeb6-197">Durante o registro, o nó Olá DSC e servidor de Pull de DSC/relatórios negociam um certificado exclusivo para este toouse de nó para pós-registro de autenticação toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="bfeb6-198">Esse processo impede que nós integrados representem um ao outro, por exemplo, se um nó for comprometido e estiver se comportando de maneira mal-intencionada.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="bfeb6-199">Após o registro, a chave de registro de saudação não é usado para autenticação novamente e é excluído do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="bfeb6-200">Você pode obter informações de saudação necessárias para o protocolo de registro de saudação DSC da saudação **gerenciar chaves** folha no portal de visualização do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="bfeb6-201">Abrir esta folha clicando ícone chave Olá Olá **Essentials** painel para Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="bfeb6-202">URL de registro é o campo de URL de saudação na folha de gerenciamento de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="bfeb6-203">Chave de registro é Olá chave de acesso primária ou chave de acesso secundária na folha de gerenciamento de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="bfeb6-204">Qualquer chave pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-204">Either key can be used.</span></span>

<span data-ttu-id="bfeb6-205">Para maior segurança, as chaves de acesso primária e secundária saudação de uma conta de automação podem ser regeneradas a qualquer momento (em Olá **gerenciar chaves** folha) tooprevent registros de nó futuro usando chaves anteriores.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="bfeb6-206">Solução de problemas de integração de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="bfeb6-207">O DSC de Automação do Azure permite a fácil integração de VMs do Microsoft Azure ao gerenciamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="bfeb6-208">Bastidores Olá, Olá extensão de configuração de estado desejado do Azure VM é usada tooregister Olá VM com DSC de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="bfeb6-209">Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, controle o progresso e execução de solução de problemas podem ser importantes.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="bfeb6-210">Qualquer método de integração tooAzure uma VM do Windows Azure DSC de automação que usa a extensão de configuração de estado desejado do Azure VM Olá pode levar até tooan horas para Olá nó tooshow backup registrados na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="bfeb6-211">Isso é devido a instalação de toohello do Windows Management Framework 5.0 no hello VM pela extensão de DSC de VM do Azure hello, que é necessário tooonboard Olá VM tooAzure DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="bfeb6-212">status de Olá tootroubleshoot ou modo de exibição de extensão de configuração de estado desejado do Azure VM, no portal do Azure de saudação do hello navegue toohello VM sendo integrados, em seguida, clique em -> **todas as configurações** -> **extensões**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="bfeb6-213">Para obter mais detalhes, você pode clicar em **Exibir status detalhado**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="bfeb6-214">Expiração do certificado e um novo registro</span><span class="sxs-lookup"><span data-stu-id="bfeb6-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="bfeb6-215">Depois de registrar um computador como um nó de DSC no DSC de automação do Azure, há várias razões por que talvez seja necessário tooreregister nesse nó no hello futura:</span><span class="sxs-lookup"><span data-stu-id="bfeb6-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="bfeb6-216">Após o registro, cada nó negocia automaticamente um certificado exclusivo para autenticação, que expira depois de um ano.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="bfeb6-217">Atualmente, Olá protocolo de registro de DSC do PowerShell não é possível renovar automaticamente certificados quando eles estão se aproximando da expiração, portanto, você precisa nós de saudação tooreregister após a hora de um ano.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="bfeb6-218">Antes de registrar novamente, certifique-se de que cada nó está executando o Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="bfeb6-219">Se certificado de autenticação de um nó irá expirar e não for registrado novamente o nó de saudação, nó hello serão toocommunicate não é possível com a automação do Azure e será marcado como 'Sem resposta.'</span><span class="sxs-lookup"><span data-stu-id="bfeb6-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="bfeb6-220">Um novo registro executadas 90 dias ou menos de tempo de expiração do certificado hello, ou a qualquer momento após a hora de expiração do certificado hello, resultará em um novo certificado que está sendo gerado e usado.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="bfeb6-221">toochange qualquer [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que foram definidas durante o registro inicial do nó de saudação, como ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="bfeb6-222">Atualmente, esses valores de agente do DSC só podem ser alterados por meio de um novo registro.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="bfeb6-223">uma exceção de Olá Olá configuração de nó atribuída nó toohello--isso pode ser alterado no DSC de automação do Azure diretamente.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="bfeb6-224">Um novo registro pode ser executado em Olá mesmo maneira registrado nó Olá inicialmente, usando qualquer um dos métodos de integração de saudação descrita neste documento.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="bfeb6-225">Não é necessário toounregister um nó do DSC de automação do Azure antes registrando-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="bfeb6-226">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="bfeb6-226">Related Articles</span></span>

* [<span data-ttu-id="bfeb6-227">Visão geral do DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="bfeb6-228">cmdlets da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="bfeb6-229">preço da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="bfeb6-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
