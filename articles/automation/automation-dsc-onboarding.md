---
title: "Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure | Microsoft Docs"
description: "Como configurar computadores para o gerenciamento com o DSC de Automação do Azure"
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="be9ad-103">Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="be9ad-104">Por que gerenciar máquinas com o DSC de Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="be9ad-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="be9ad-105">Como a [Configuração de Estado Desejado do PowerShell](https://technet.microsoft.com/library/dn249912.aspx), a Configuração de Estado Desejado da Automação do Azure é um serviço de gerenciamento de configuração simples, mas poderoso, para nós DSC (máquinas físicas e virtuais) em qualquer datacenter de nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="be9ad-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="be9ad-106">Ela permite a escalabilidade entre milhares de máquinas rápida e facilmente a partir de um local central e seguro.</span><span class="sxs-lookup"><span data-stu-id="be9ad-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="be9ad-107">Você pode, facilmente, integrar máquinas, atribuir a elas configurações declarativas e exibir relatórios que mostram a conformidade de cada computador com o estado desejado especificado.</span><span class="sxs-lookup"><span data-stu-id="be9ad-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="be9ad-108">A camada de gerenciamento do DSC de Automação do Azure é para o DSC o que a camada de gerenciamento de Automação do Azure é para o script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be9ad-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="be9ad-109">Em outras palavras, da mesma forma que a Automação do Azure ajuda você a gerenciar os scripts do PowerShell, ela também ajuda a gerenciar configurações do DSC.</span><span class="sxs-lookup"><span data-stu-id="be9ad-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="be9ad-110">Para saber mais sobre os benefícios do uso do DSC de Automação do Azure, consulte [Visão geral do DSC de Automação do Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be9ad-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="be9ad-111">O DSC de Automação do Azure pode ser usado para gerenciar uma variedade de máquinas:</span><span class="sxs-lookup"><span data-stu-id="be9ad-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="be9ad-112">Máquinas virtuais do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="be9ad-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="be9ad-113">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-113">Azure virtual machines</span></span>
* <span data-ttu-id="be9ad-114">Máquinas virtuais do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="be9ad-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="be9ad-115">Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="be9ad-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="be9ad-116">Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="be9ad-117">Além disso, se você não estiver pronto para gerenciar a configuração da máquina a partir da nuvem, o DSC da Automação do Azure também poderá ser usado como um ponto de extremidade apenas para relatório.</span><span class="sxs-lookup"><span data-stu-id="be9ad-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="be9ad-118">Isso permite que você defina a configuração desejada (push) por meio do DSC local e exiba relatórios detalhados sobre a conformidade de nó com o estado desejado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="be9ad-119">As seções a seguir descrevem como você pode integrar cada tipo de máquina ao DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="be9ad-120">Máquinas virtuais do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="be9ad-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="be9ad-121">Com o DSC de Automação do Azure, você pode facilmente carregar máquinas virtuais do Azure (clássico) para gerenciamento de configuração usando o portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be9ad-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="be9ad-122">Nos bastidores e sem um administrador precisar acessar remotamente a VM, a extensão de Configuração de Estado Desejado da VM do Azure registra a VM com o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="be9ad-123">Como a extensão da Configuração de Estado Desejado da VM do Azure é executada de forma assíncrona, as etapas para acompanhar seu andamento ou para resolver problemas nele são fornecidas na seção [**Solução de problemas de integração de máquina virtual do Azure**](#troubleshooting-azure-virtual-machine-onboarding) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="be9ad-124">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-124">Azure portal</span></span>

<span data-ttu-id="be9ad-125">No [portal do Azure](http://portal.azure.com/), clique em **Procurar** -> **Máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="be9ad-126">Selecione a VM do Windows que você deseja integrar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="be9ad-127">Na folha do painel da máquina virtual, clique em **Todas as configurações** -> **Extensões** -> **Adicionar** -> **DSC de Automação do Azure** -> **Criar**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="be9ad-128">Insira os [Valores do Gerenciador de Configurações Local de DSC do PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o seu caso de uso, a chave de registro e a URL de registro de sua conta da Automação e, opcionalmente, uma configuração de nó para atribuir à VM.</span><span class="sxs-lookup"><span data-stu-id="be9ad-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="be9ad-129">Para encontrar a URL de registro e a chave da conta da Automação a ser integrada ao computador, confira a seção [**Proteger o registro**](#secure-registration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="be9ad-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be9ad-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="be9ad-131">Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-131">Azure virtual machines</span></span>

<span data-ttu-id="be9ad-132">O DSC de Automação do Azure permite que você integre facilmente máquinas virtuais do Azure para o gerenciamento de configuração, usando o portal do Azure, os modelos do Gerenciador de Recursos do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be9ad-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="be9ad-133">Nos bastidores e sem um administrador precisar acessar remotamente a VM, a extensão de Configuração de Estado Desejado da VM do Azure registra a VM com o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="be9ad-134">Como a extensão da Configuração de Estado Desejado da VM do Azure é executada de forma assíncrona, as etapas para acompanhar seu andamento ou para resolver problemas nele são fornecidas na seção [**Solução de problemas de integração de máquina virtual do Azure**](#troubleshooting-azure-virtual-machine-onboarding) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="be9ad-135">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-135">Azure portal</span></span>

<span data-ttu-id="be9ad-136">No [Portal do Azure](https://portal.azure.com/), navegue até a conta da Automação do Azure na qual você deseja carregar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="be9ad-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="be9ad-137">No painel da conta de Automação, clique em **Nós DSC** -> **Adicionar VM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="be9ad-138">Em **Selecionar máquinas virtuais a serem integradas**, selecione uma ou mais máquinas virtuais do Azure para integrar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="be9ad-139">Em **Configurar dados de registro**, digite os [valores do Gerenciador de Configuração Local de DSC do PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o seu caso de uso e, opcionalmente, uma configuração de nó para atribuir à VM.</span><span class="sxs-lookup"><span data-stu-id="be9ad-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="be9ad-140">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="be9ad-141">Máquinas virtuais do Azure podem ser implantadas e integradas ao DSC de Automação do Azure por meio de modelos do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="be9ad-142">Veja [Configurar uma VM por meio da extensão de DSC e da DSC de Automação do Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para obter um modelo de exemplo que integra uma VM existente à DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="be9ad-143">Para encontrar a chave de registro e a URL de registro adotadas como entrada neste modelo, confira a seção [**Proteger o registro**](#secure-registration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="be9ad-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be9ad-144">PowerShell</span></span>

<span data-ttu-id="be9ad-145">O cmdlet [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) pode ser usado para integrar máquinas virtuais ao Portal do Azure por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be9ad-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="be9ad-146">Máquinas virtuais do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="be9ad-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="be9ad-147">Você pode facilmente integrar máquinas virtuais do Amazon Web Services para o gerenciamento de configuração pelo DSC de Automação do Azure usando o Kit de Ferramentas AWS DSC.</span><span class="sxs-lookup"><span data-stu-id="be9ad-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="be9ad-148">Você pode saber mais sobre esse kit de ferramentas [aqui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="be9ad-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="be9ad-149">Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="be9ad-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="be9ad-150">As máquinas do Windows locais e as máquinas do Windows em nuvens que não são do Azure (como o Amazon Web Services) também podem ser integradas ao DSC de Automação do Azure, desde que eles tenham acesso de saída à Internet, através de algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="be9ad-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="be9ad-151">Verifique se a versão mais recente do [WMF 5](http://aka.ms/wmf5latest) está instalada nos computadores que você deseja integrar ao DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="be9ad-152">Siga as instruções na seção [**Gerando metaconfigurações DSC**](#generating-dsc-metaconfigurations) abaixo para gerar uma pasta com as metaconfigurações de DSC necessárias.</span><span class="sxs-lookup"><span data-stu-id="be9ad-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="be9ad-153">Aplique-se remotamente a metaconfiguração do DSC do PowerShell às máquinas que você deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="be9ad-154">**O computador no qual este comando é executado deve ter a versão mais recente do [WMF 5](http://aka.ms/wmf5latest) instalada**:</span><span class="sxs-lookup"><span data-stu-id="be9ad-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="be9ad-155">Se você não pode aplicar as metaconfigurações do DSC do PowerShell remotamente, copie a pasta de metaconfigurações da etapa 2 em cada computador para carregar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="be9ad-156">Ligue para **Set-DscLocalConfigurationManager** localmente em cada computador para carregar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="be9ad-157">Usando o portal do Azure ou os cmdlets, verifique se as máquinas para carregar agora aparecem como nós DSC registrados em sua conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="be9ad-158">Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="be9ad-159">Os computadores com Linux locais, computadores com Linux no Azure e os computadores com Linux em nuvens que não são do Azure também podem ser integrados ao DSC de Automação do Azure, desde que tenham acesso de saída à Internet, por meio de algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="be9ad-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="be9ad-160">Certifique-se de que a versão mais recente da [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalada nos computadores que você deseja integrar à DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="be9ad-161">Se o [padrões do Gerenciador de Configurações Local do DSC do PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corresponde a seu caso de uso e você deseja integrar computadores de modo que como que eles **ambos** efetuem pull e gerem relatório para o DSC de Automação do Azure:</span><span class="sxs-lookup"><span data-stu-id="be9ad-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="be9ad-162">Em cada computador Linux para carregar ao DSC de Automação do Azure, use Register.py para carregar usando os padrões do Gerenciador de Configuração Local do DSC do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="be9ad-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="be9ad-163">Para encontrar a chave de registro e a URL de registro de sua conta da Automação, confira a seção [**Proteger o registro**](#secure-registration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="be9ad-164">Se os padrões do Gerenciador de Configuração Local do DSC do PowerShell **não** **correspondem** a seu caso de uso, ou você deseja carregar computadores, de modo que eles só reportem para o DSC de Automação do Azure, mas não façam configuração pull nem módulos do PowerShell com base nela, siga as etapas 3-6.</span><span class="sxs-lookup"><span data-stu-id="be9ad-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="be9ad-165">Caso contrário, vá diretamente para a etapa 6.</span><span class="sxs-lookup"><span data-stu-id="be9ad-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="be9ad-166">Siga as instruções na seção [**Gerando metaconfigurações DSC**](#generating-dsc-metaconfigurations) abaixo para gerar uma pasta com as metaconfigurações de DSC necessárias.</span><span class="sxs-lookup"><span data-stu-id="be9ad-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="be9ad-167">Aplique remotamente a metaconfiguração do DSC do PowerShell às máquinas que você deseja carrega:</span><span class="sxs-lookup"><span data-stu-id="be9ad-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="be9ad-168">O computador no qual este comando é executado deve ter a versão mais recente do [WMF 5](http://aka.ms/wmf5latest) instalada.</span><span class="sxs-lookup"><span data-stu-id="be9ad-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="be9ad-169">Se você não pode aplicar as metaconfigurações do DSC do PowerShell remotamente, para cada computador Linux para carregar, copie a metaconfiguração correspondente a esse computador a partir da pasta na etapa 5 no computador Linux.</span><span class="sxs-lookup"><span data-stu-id="be9ad-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="be9ad-170">Em seguida, chame `SetDscLocalConfigurationManager.py` localmente em cada computador com Linux que deseja integrar à DSC de Automação do Azure:</span><span class="sxs-lookup"><span data-stu-id="be9ad-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="be9ad-171">Usando o portal do Azure ou os cmdlets, verifique se as máquinas para carregar agora aparecem como nós DSC registrados em sua conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="be9ad-172">Gerando metaconfigurações DSC</span><span class="sxs-lookup"><span data-stu-id="be9ad-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="be9ad-173">Para carregar genericamente qualquer computador ao DSC de Automação do Azure, uma [metaconfiguração de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) pode ser gerada de modo que, quando aplicada, informa o agente do DSC no computador para efetuar pull de e/ou relatar para o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="be9ad-174">As metaconfigurações de DSC para o DSC de Automação do Azure podem ser geradas usando uma configuração de DSC do PowerShell, ou os cmdlets do PowerShell de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="be9ad-175">Metaconfigurações DSC contêm os segredos necessários para carregar um computador em uma conta de Automação para gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="be9ad-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="be9ad-176">Certifique-se de proteger corretamente quaisquer metaconfigurações de DSC que criar, ou exclua-as imediatamente após o uso.</span><span class="sxs-lookup"><span data-stu-id="be9ad-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="be9ad-177">Usando uma Configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="be9ad-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="be9ad-178">Abra o PowerShell ISE como administrador em um computador no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="be9ad-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="be9ad-179">O computador também deve ter a versão mais recente do [WMF 5](http://aka.ms/wmf5latest) instalada.</span><span class="sxs-lookup"><span data-stu-id="be9ad-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="be9ad-180">Compie o script a seguir localmente.</span><span class="sxs-lookup"><span data-stu-id="be9ad-180">Copy the following script locally.</span></span> <span data-ttu-id="be9ad-181">Esse script contém uma configuração DSC do PowerShell para criar metaconfigurações e um comando para dar início à criação de metaconfigurações.</span><span class="sxs-lookup"><span data-stu-id="be9ad-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="be9ad-182">Preencha a chave de registro e a URL para sua conta de Automação, bem como os nomes dos computadores a carregar.</span><span class="sxs-lookup"><span data-stu-id="be9ad-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="be9ad-183">Todos os outros parâmetros são opcionais.</span><span class="sxs-lookup"><span data-stu-id="be9ad-183">All other parameters are optional.</span></span> <span data-ttu-id="be9ad-184">Para encontrar a chave de registro e a URL de registro de sua conta da Automação, confira a seção [**Proteger o registro**](#secure-registration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="be9ad-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="be9ad-185">Se você deseja que as máquinas relatem informações de status de DSC ao DSC de Automação do Azure, mas não efetue pull da configuração de recepção ou módulos do PowerShell, defina o parâmetro **ReportOnly** como verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="be9ad-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="be9ad-186">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="be9ad-186">Run the script.</span></span> <span data-ttu-id="be9ad-187">Agora você deve ter uma pasta chamada **DscMetaConfigs** no diretório de trabalho, que contém as metaconfigurações de DSC do PowerShell para os computadores a carregar (como um administrador):</span><span class="sxs-lookup"><span data-stu-id="be9ad-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="be9ad-188">Usando os cmdlets da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="be9ad-189">Se o padrões do Gerenciador de Configurações Local do DSC do PowerShell correspondem a seu caso de uso e você deseja integrar computadores de modo que eles ambos efetuem pull e gerem relatório para o DSC de Automação do Azure, os cmdlets de Automação do Azure fornecem um método simplificado para gerar as metaconfigurações de DSC necessárias:</span><span class="sxs-lookup"><span data-stu-id="be9ad-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="be9ad-190">Abra o console do PowerShell ou o PowerShell ISE como administrador em uma máquina no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="be9ad-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="be9ad-191">Conecte-se ao Gerenciador de Recursos do Azure usando **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="be9ad-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="be9ad-192">Baixe, da conta de Automação da qual você deseja carregar nós, as metaconfigurações do DSC do PowerShell para as máquinas que você deseja carregar:</span><span class="sxs-lookup"><span data-stu-id="be9ad-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="be9ad-193">Agora você deve ter uma pasta chamada ***DscMetaConfigs***que contém as metaconfigurações de DSC do PowerShell para os computadores a carregar (como um administrador):</span><span class="sxs-lookup"><span data-stu-id="be9ad-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="be9ad-194">Proteger o registro</span><span class="sxs-lookup"><span data-stu-id="be9ad-194">Secure registration</span></span>

<span data-ttu-id="be9ad-195">Os computadores podem ser carregados com segurança a uma conta de Automação do Azure por meio do protocolo de registro de WMF 5 DSC, que permite a um nó DSC se autenticar a um servidor de Recepção ou de Relatórios do DSC V2 do PowerShell (incluindo o DSC de Automação do Azure).</span><span class="sxs-lookup"><span data-stu-id="be9ad-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="be9ad-196">O nó é registrado no servidor em uma **URL de Registro**, autenticando por meio de uma **Chave de registro**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="be9ad-197">Durante o registro, o nó de DSC e o servidor de Recepção/Relatórios DSC negociam um certificado exclusivo para este nó a ser usado para a autenticação do servidor após o registro.</span><span class="sxs-lookup"><span data-stu-id="be9ad-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="be9ad-198">Esse processo impede que nós integrados representem um ao outro, por exemplo, se um nó for comprometido e estiver se comportando de maneira mal-intencionada.</span><span class="sxs-lookup"><span data-stu-id="be9ad-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="be9ad-199">Após o registro, a Chave de registro não é usada para autenticação novamente e é excluída do nó.</span><span class="sxs-lookup"><span data-stu-id="be9ad-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="be9ad-200">Você pode obter as informações necessárias para o protocolo de registro do DSC na folha **Gerenciar chaves** no portal de visualização do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="be9ad-201">Abra a folha clicando no ícone de chave no painel **Noções Básicas** da conta da Automação.</span><span class="sxs-lookup"><span data-stu-id="be9ad-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="be9ad-202">A URL de registro é o campo de URL na folha Gerenciar chaves.</span><span class="sxs-lookup"><span data-stu-id="be9ad-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="be9ad-203">A chave de registro é a Chave de Acesso Primária ou Chave de Acesso Secundária na folha Gerenciar chaves.</span><span class="sxs-lookup"><span data-stu-id="be9ad-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="be9ad-204">Qualquer chave pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="be9ad-204">Either key can be used.</span></span>

<span data-ttu-id="be9ad-205">Para aumentar a segurança, as chaves de acesso primária e secundária de uma conta de Automação podem ser regeneradas a qualquer momento (na folha **Gerenciar chaves** ) para impedir que os registros de nós futuros usem chaves anteriores.</span><span class="sxs-lookup"><span data-stu-id="be9ad-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="be9ad-206">Solução de problemas de integração de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="be9ad-207">O DSC de Automação do Azure permite a fácil integração de VMs do Microsoft Azure ao gerenciamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="be9ad-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="be9ad-208">Nos bastidores, a extensão de Configuração de Estado Desejado da VM do Azure é usada para registrar a VM com o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="be9ad-209">Como a extensão de Configuração de Estado Desejado da VM do Azure é executada de forma assíncrona, acompanhar o seu progresso e solucionar os problemas de sua execução pode ser importante.</span><span class="sxs-lookup"><span data-stu-id="be9ad-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="be9ad-210">Qualquer método de integração de uma VM do Azure ao DSC de Automação do Azure que usa a extensão de Configuração de Estado Desejado da VM do Azure pode levar até uma hora para o nó mostrar como registrado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="be9ad-211">Isso se deve à instalação do Windows Management Framework 5.0 na VM pela extensão DSC da VM do Azure, que precisa integrar a VM ao DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="be9ad-212">Para solucionar problemas ou exibir o status da extensão de Configuração de Estado Desejado da VM do Azure, no portal do Azure, navegue até a VM que está sendo integrada e clique em -> **Todas as configurações** -> **Extensões** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="be9ad-213">Para obter mais detalhes, você pode clicar em **Exibir status detalhado**.</span><span class="sxs-lookup"><span data-stu-id="be9ad-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="be9ad-214">Expiração do certificado e um novo registro</span><span class="sxs-lookup"><span data-stu-id="be9ad-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="be9ad-215">Depois de registrar uma máquina como um nó DSC no DSC de Automação do Azure, há vários motivos para você precisar registrar novamente o nó no futuro:</span><span class="sxs-lookup"><span data-stu-id="be9ad-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="be9ad-216">Após o registro, cada nó negocia automaticamente um certificado exclusivo para autenticação, que expira depois de um ano.</span><span class="sxs-lookup"><span data-stu-id="be9ad-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="be9ad-217">Atualmente, o protocolo de registro DSC do PowerShell não pode renovar automaticamente certificados quando eles estão prestes a expirar, então você precisa registrar novamente os nós após um ano.</span><span class="sxs-lookup"><span data-stu-id="be9ad-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="be9ad-218">Antes de registrar novamente, certifique-se de que cada nó está executando o Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="be9ad-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="be9ad-219">Se o certificado de autenticação de um nó expirar e o nó não for registrado novamente, o nó não será capaz de se comunicar com a Automação do Azure e será marcado como "Sem resposta".</span><span class="sxs-lookup"><span data-stu-id="be9ad-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="be9ad-220">A realização de um novo registro a 90 dias ou menos do tempo de expiração do certificado, ou a qualquer momento após o tempo de expiração do certificado, vai resultar na geração e uso de um novo certificado.</span><span class="sxs-lookup"><span data-stu-id="be9ad-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="be9ad-221">Para alterar quaisquer [valores do Gerenciador de Configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que foram definidos durante o registro inicial do nó, como ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="be9ad-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="be9ad-222">Atualmente, esses valores de agente do DSC só podem ser alterados por meio de um novo registro.</span><span class="sxs-lookup"><span data-stu-id="be9ad-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="be9ad-223">A única exceção é a Configuração de Nó atribuída ao nó, isso pode ser alterado diretamente no DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ad-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="be9ad-224">Um novo registro pode ser executado da mesma maneira que você registrou o nó inicialmente, usando qualquer um dos métodos de integração descritos neste documento.</span><span class="sxs-lookup"><span data-stu-id="be9ad-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="be9ad-225">Você não precisa cancelar o registro de um nó do DSC de Automação do Azure antes de registrá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="be9ad-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="be9ad-226">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="be9ad-226">Related Articles</span></span>

* [<span data-ttu-id="be9ad-227">Visão geral do DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="be9ad-228">cmdlets da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="be9ad-229">preço da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be9ad-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
