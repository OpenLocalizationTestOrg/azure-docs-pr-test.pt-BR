---
title: "Visão geral de configuração de estado desejado para o Azure | Microsoft Docs"
description: "Visão geral para usar o manipulador de extensão do Microsoft Azure para configuração de estado desejado do PowerShell. Incluindo pré-requisitos, arquitetura e cmdlets."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: c05c2d541a5f526f362f9cd72fe6d878374112b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="bfcf5-104">Introdução ao manipulador de extensão de configuração do estado desejado do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcf5-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="bfcf5-105">O agente de VM do Azure e as extensões associadas são parte dos serviços de infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="bfcf5-106">Extensões de VM são componentes de software que estendem a funcionalidade da VM e simplificam várias operações de gerenciamento de VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="bfcf5-107">Por exemplo, a extensão VMAccess pode ser usada para redefinir uma senha de administrador, ou a extensão de Script Personalizado pode ser usada para executar um script na VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="bfcf5-108">Este artigo apresenta a extensão de configuração de estado desejado (DSC) do PowerShell para VMs do Azure como parte do SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="bfcf5-109">Você pode usar os novos cmdlets para carregar e aplicar uma DSC do PowerShell em uma VM do Azure habilitada com a extensão de DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="bfcf5-110">A extensão de DSC do PowerShell chama a DSC do PowerShell para aplicar a configuração DSC recebida na VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="bfcf5-111">Essa funcionalidade também está disponível por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfcf5-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bfcf5-112">Prerequisites</span></span>
<span data-ttu-id="bfcf5-113">**Máquina local** Para interagir com a extensão de VM do Azure, você precisa usar o Portal do Azure ou o SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="bfcf5-114">**Agente convidado** A VM do Azure a configurar pela configuração do DSC precisa ter um sistema operacional compatível com Windows Management Framework (WMF) 4.0 ou 5.0.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="bfcf5-115">A lista completa de versões com suporte do sistema operacional pode ser encontrada no [Histórico de versões da extensão de DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="bfcf5-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="bfcf5-116">Termos e conceitos</span><span class="sxs-lookup"><span data-stu-id="bfcf5-116">Terms and concepts</span></span>
<span data-ttu-id="bfcf5-117">Este guia presume familiaridade com os seguintes conceitos:</span><span class="sxs-lookup"><span data-stu-id="bfcf5-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="bfcf5-118">Configuração - um documento de configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="bfcf5-119">Nó - um destino para uma configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="bfcf5-120">Neste documento, "nó" sempre faz referência a uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="bfcf5-121">Dados de configuração - um arquivo .psd1 contendo dados ambientais para uma configuração</span><span class="sxs-lookup"><span data-stu-id="bfcf5-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="bfcf5-122">Visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="bfcf5-122">Architectural overview</span></span>
<span data-ttu-id="bfcf5-123">A extensão de DSC do Azure usa a estrutura do Agente de VM do Azure para entregar, aplicar e gerar relatórios sobre configurações da DSC executadas em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="bfcf5-124">A extensão de DSC espera um arquivo .zip contendo pelo menos um documento de configuração e um conjunto de parâmetros fornecidos por meio do SDK do Azure PowerShell ou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="bfcf5-125">Quando a extensão é chamada pela primeira vez, executa um processo de instalação.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="bfcf5-126">Esse processo instala uma versão do Windows Management Framework (WMF) usando a lógica a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfcf5-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="bfcf5-127">Se o sistema operacional da VM do Azure for o Windows Server 2016, nenhuma ação é executada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="bfcf5-128">O Windows Server 2016 já possui a versão mais recente do PowerShell instalada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="bfcf5-129">Se a propriedade `wmfVersion` for especificada, essa versão do WMF é instalada, a menos que ele não seja compatível com o sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="bfcf5-130">Se nenhuma propriedade `wmfVersion` for especificada, a versão mais recente do WMF aplicável é instalada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="bfcf5-131">A instalação do WMF requer uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="bfcf5-132">Após a reinicialização, a extensão baixa o arquivo .zip especificado na propriedade `modulesUrl` .</span><span class="sxs-lookup"><span data-stu-id="bfcf5-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="bfcf5-133">Se esse local estiver no armazenamento de blobs do Azure, um token SAS pode ser especificado na propriedade `sasToken` para acessar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="bfcf5-134">Depois que o arquivo .zip for baixado e descompactado, a função de configuração definida em `configurationFunction` é executada para gerar o arquivo .MOF.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="bfcf5-135">Em seguida, a extensão executa `Start-DscConfiguration -Force` no arquivo MOF gerado.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="bfcf5-136">A extensão captura a saída e grava de volta para no canal de status do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="bfcf5-137">Desse ponto em diante, o LCM de DSC lida com o monitoramento e correção da maneira normal.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="bfcf5-138">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfcf5-138">PowerShell cmdlets</span></span>
<span data-ttu-id="bfcf5-139">Os cmdlets do PowerShell podem ser usados com o Azure Resource Manager ou o modelo clássico de implementação para empacotar, publicar e monitorar implantações de extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="bfcf5-140">Os cmdlets listados a seguir são os módulos de implantação clássicos, mas "Azure" pode ser substituído por "AzureRm" para usar o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="bfcf5-141">Por exemplo, `Publish-AzureVMDscConfiguration` usa o modelo de implantação clássico, mas `Publish-AzureRmVMDscConfiguration` usa o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="bfcf5-142">`Publish-AzureVMDscConfiguration` recebe um arquivo de configuração, verifica a existência de recursos dependentes de DSC e cria um arquivo .zip contendo a configuração e os recursos de DSC necessários para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="bfcf5-143">Também pode criar o pacote localmente usando o parâmetro `-ConfigurationArchivePath` .</span><span class="sxs-lookup"><span data-stu-id="bfcf5-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="bfcf5-144">Caso contrário, ele publicará o arquivo .zip no Armazenamento de Blobs do Azure e o protegerá com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="bfcf5-145">O arquivo .zip criado por esse cmdlet possui o script de configuração .ps1 na raiz da pasta de arquivamento.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="bfcf5-146">Os recursos possuem a pasta de módulo colocada na pasta de arquivo morto.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="bfcf5-147">`Set-AzureVMDscExtension` injeta as configurações necessárias pela extensão de DSC do PowerShell em um objeto de configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="bfcf5-148">No modelo de implantação clássico, as alterações da VM devem ser aplicadas a uma VM do Azure com `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="bfcf5-149">O `Get-AzureVMDscExtension` recupera o status da extensão de DSC de uma VM específica.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="bfcf5-150">`Get-AzureVMDscExtensionStatus` recupera o status da configuração DSC imposta pelo manipulador de extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="bfcf5-151">Essa ação pode ser executada em uma única VM ou em um grupo de VMs.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="bfcf5-152">`Remove-AzureVMDscExtension` remove o manipulador de extensão de uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="bfcf5-153">Esse cmdlet **não** remove a configuração, desinstala o WMF ou altera as configurações aplicadas na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="bfcf5-154">Apenas remove o manipulador de extensão.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="bfcf5-155">**Principais diferenças nos cmdlets do ASM e do Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="bfcf5-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="bfcf5-156">Os cmdlets do Azure Resource Manager são síncronos.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="bfcf5-157">Os cmdlets do ASM são assíncronos.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="bfcf5-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version e Location são todos parâmetros obrigatórios no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="bfcf5-159">ArchiveResourceGroupName é um novo parâmetro opcional para o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="bfcf5-160">Você pode especificar esse parâmetro quando sua conta de armazenamento pertencer a um grupo de recursos diferente daquele no qual a máquina virtual foi criada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="bfcf5-161">ConfigurationArchive é chamado de ArchiveBlobName no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfcf5-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="bfcf5-162">ContainerName é chamado de ArchiveContainerName no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfcf5-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="bfcf5-163">StorageEndpointSuffix é chamado de ArchiveStorageEndpointSuffix no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfcf5-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="bfcf5-164">A opção AutoUpdate foi adicionada ao Azure Resource Manager para habilitar a atualização automática do manipulador de extensão na versão mais recente e quando estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="bfcf5-165">Observe que esse parâmetro tem o potencial de causar reinicializações na VM quando uma nova versão do WMF for lançada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="bfcf5-166">Funcionalidade do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcf5-166">Azure portal functionality</span></span>
<span data-ttu-id="bfcf5-167">Navegue até uma VM.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-167">Browse to a VM.</span></span> <span data-ttu-id="bfcf5-168">Em Configurações -> Geral, clique em "Extensões".</span><span class="sxs-lookup"><span data-stu-id="bfcf5-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="bfcf5-169">Um novo painel é criado.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-169">A new pane is created.</span></span> <span data-ttu-id="bfcf5-170">Clique em "Adicionar" e selecione DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="bfcf5-171">O portal precisa de entrada.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-171">The portal needs input.</span></span>
<span data-ttu-id="bfcf5-172">**Script ou módulos de configuração**: esse campo é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="bfcf5-173">Requer um arquivo. ps1 contendo um script de configuração ou um arquivo .zip com um script de configuração .ps1 na raiz e todos os recursos dependentes em pastas de módulo dentro do .zip.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="bfcf5-174">Ele pode ser criado com o cmdlet `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` incluído no SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="bfcf5-175">O arquivo .zip será carregado em seu armazenamento de blobs de usuário protegido por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="bfcf5-176">**Arquivo de configuração PSD1 de dados**: esse campo é opcional.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="bfcf5-177">Se sua configuração exigir um arquivo de dados de configuração em .psd1, use este campo para selecioná-lo e carregá-lo no armazenamento de blobs de usuário, onde eles serão protegidos por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="bfcf5-178">**Nome de configuração qualificado por módulo**: os arquivos .ps1 podem ter várias funções de configuração.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="bfcf5-179">Insira o nome do script .ps1 de configuração seguido por um '\'' e o nome da função de configuração.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="bfcf5-180">Por exemplo, se o seu script .ps1 tiver o nome "configuration.ps1" e se a configuração for "IisInstall", insira: `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="bfcf5-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="bfcf5-181">**Argumentos de configuração**: se a função de configuração leva argumentos, insira-os aqui no formato `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="bfcf5-182">Observe que esse formato é diferente daquele como argumentos de configuração são aceitos por meio de cmdlets do PowerShell ou modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="bfcf5-183">Introdução</span><span class="sxs-lookup"><span data-stu-id="bfcf5-183">Getting started</span></span>
<span data-ttu-id="bfcf5-184">A extensão de DSC do Azure usa documentos de configuração DSC e impõe os mesmos em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="bfcf5-185">A seguir está um exemplo simples de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="bfcf5-186">Salve localmente como "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="bfcf5-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="bfcf5-187">As etapas a seguir colocam o script IisInstall.ps1 na VM especificada, executam a configuração e relatam o status.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="bfcf5-188">Modelo clássico</span><span class="sxs-lookup"><span data-stu-id="bfcf5-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="bfcf5-189">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfcf5-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="bfcf5-190">Registro em log</span><span class="sxs-lookup"><span data-stu-id="bfcf5-190">Logging</span></span>
<span data-ttu-id="bfcf5-191">Os logs são colocados em:</span><span class="sxs-lookup"><span data-stu-id="bfcf5-191">Logs are placed in:</span></span>

<span data-ttu-id="bfcf5-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Número de versão]</span><span class="sxs-lookup"><span data-stu-id="bfcf5-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfcf5-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfcf5-193">Next steps</span></span>
<span data-ttu-id="bfcf5-194">Para saber mais sobre a DSC do PowerShell, [visite o centro de documentação do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="bfcf5-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="bfcf5-195">Examine o [modelo do Azure Resource Manager para a extensão de DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfcf5-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="bfcf5-196">Para encontrar a funcionalidade adicional que você pode gerenciar com a DSC do PowerShell, [navegue na galeria do PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para conhecer mais recursos da DSC.</span><span class="sxs-lookup"><span data-stu-id="bfcf5-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="bfcf5-197">Para obter detalhes sobre como passar parâmetros confidenciais em configurações, consulte [Gerenciar credenciais com segurança com o manipulador de extensão de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfcf5-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

