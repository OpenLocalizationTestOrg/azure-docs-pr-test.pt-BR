---
title: "aaaDesired configuração de estado para visão geral do Azure | Microsoft Docs"
description: "Visão geral para usar o manipulador de extensão do Microsoft Azure Olá para configuração de estado desejado do PowerShell. Incluindo pré-requisitos, arquitetura e cmdlets."
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
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="45558-104">Manipulador de extensão de configuração de estado desejado do Azure de toohello de Introdução</span><span class="sxs-lookup"><span data-stu-id="45558-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="45558-105">Hello Azure VM Agent e as extensões associadas são parte do hello serviços de infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="45558-106">Extensões de VM são componentes de software que estendem a funcionalidade VM hello e simplificam a várias operações de gerenciamento de VM.</span><span class="sxs-lookup"><span data-stu-id="45558-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="45558-107">Por exemplo, Olá extensão VMAccess pode ser usado tooreset uma senha de administrador ou Olá Script personalizado extensão pode ser usado tooexecute um script em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="45558-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="45558-108">Este artigo apresenta Olá extensão de configuração de estado de desejado (DSC) do PowerShell para VMs do Azure como parte da saudação SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45558-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="45558-109">Você pode usar o novo tooupload de cmdlets e aplicar uma configuração de DSC do PowerShell em uma VM do Azure habilitado com hello extensão de DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45558-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="45558-110">chamadas de extensão de DSC do PowerShell Olá em saudação do PowerShell DSC tooenact recebeu a configuração de DSC em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="45558-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="45558-111">Essa funcionalidade também está disponível por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45558-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45558-112">Prerequisites</span></span>
<span data-ttu-id="45558-113">**Máquina local** toointeract com hello extensão VM do Azure, você precisa toouse ou Olá portal do Azure ou Olá SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45558-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="45558-114">**O agente convidado** Olá VM do Azure que é configurado por configuração Olá DSC precisa toobe um sistema operacional que suporta o Windows Management Framework (WMF) 4.0 ou 5.0.</span><span class="sxs-lookup"><span data-stu-id="45558-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="45558-115">lista completa de Olá das versões de sistema operacional com suporte pode ser encontrada no hello [histórico de versão da extensão DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="45558-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="45558-116">Termos e conceitos</span><span class="sxs-lookup"><span data-stu-id="45558-116">Terms and concepts</span></span>
<span data-ttu-id="45558-117">Este guia presume familiaridade com hello conceitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="45558-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="45558-118">Configuração - um documento de configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="45558-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="45558-119">Nó - um destino para uma configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="45558-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="45558-120">Neste documento, "nó" sempre se refere a tooan VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="45558-121">Dados de configuração - um arquivo .psd1 contendo dados ambientais para uma configuração</span><span class="sxs-lookup"><span data-stu-id="45558-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="45558-122">Visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="45558-122">Architectural overview</span></span>
<span data-ttu-id="45558-123">Olá extensão de DSC do Azure usa hello Azure VM Agent do framework toodeliver, aplicar e relatar as configurações de DSC em execução em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="45558-124">Olá extensão DSC espera um arquivo. zip que contém pelo menos um documento de configuração e um conjunto de parâmetros fornecido por meio de saudação SDK do Azure PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="45558-125">Quando a extensão de saudação é chamado para Olá primeira vez, ele executa um processo de instalação.</span><span class="sxs-lookup"><span data-stu-id="45558-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="45558-126">Esse processo instala a versão de hello Windows Management Framework (WMF) usando Olá lógica a seguir:</span><span class="sxs-lookup"><span data-stu-id="45558-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="45558-127">Se Olá sistema operacional da VM do Azure for Windows Server 2016, nenhuma ação é executada.</span><span class="sxs-lookup"><span data-stu-id="45558-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="45558-128">Windows Server 2016 já tem a versão mais recente de saudação do PowerShell instalado.</span><span class="sxs-lookup"><span data-stu-id="45558-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="45558-129">Se hello `wmfVersion` propriedade for especificada, essa versão do hello WMF é instalado, a menos que é incompatível com o sistema operacional da VM hello.</span><span class="sxs-lookup"><span data-stu-id="45558-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="45558-130">Se nenhum `wmfVersion` propriedade for especificada, hello mais recente versão aplicável do hello WMF está instalado.</span><span class="sxs-lookup"><span data-stu-id="45558-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="45558-131">Instalação do hello WMF requer uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="45558-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="45558-132">Depois da reinicialização, extensão Olá downloads arquivo. zip de saudação especificado no hello `modulesUrl` propriedade.</span><span class="sxs-lookup"><span data-stu-id="45558-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="45558-133">Se este local estiver no armazenamento de BLOBs do Azure, um token SAS pode ser especificado em Olá `sasToken` propriedade tooaccess Olá arquivo.</span><span class="sxs-lookup"><span data-stu-id="45558-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="45558-134">Após Olá ZIP é baixado e desempacotados, Olá função configuração definida no `configurationFunction` é executar o arquivo MOF do toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="45558-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="45558-135">em seguida, executa uma extensão de saudação `Start-DscConfiguration -Force` no arquivo MOF de saudação gerado.</span><span class="sxs-lookup"><span data-stu-id="45558-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="45558-136">extensão de saudação captura a saída e grava-toohello canal de Status do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="45558-137">Desse ponto em hello LCM do DSC trata de monitoramento e correção como normal.</span><span class="sxs-lookup"><span data-stu-id="45558-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="45558-138">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="45558-138">PowerShell cmdlets</span></span>
<span data-ttu-id="45558-139">Cmdlets do PowerShell pode ser usados com o Gerenciador de recursos do Azure ou Olá toopackage do modelo de implantação clássico, publicar e monitorar implantações de extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="45558-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="45558-140">cmdlets a seguir listados Hello são módulos de implantação clássico hello, mas "Azure" pode ser substituída pelo modelo do "AzureRm" toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45558-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="45558-141">Por exemplo, `Publish-AzureVMDscConfiguration` usa Olá modelo de implantação clássico, onde `Publish-AzureRmVMDscConfiguration` usa o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="45558-142">`Publish-AzureVMDscConfiguration`usa um arquivo de configuração, ele procura recursos dependentes da DSC e cria um arquivo. zip que contém a configuração de saudação e configuração de saudação do DSC recursos tooenact necessários.</span><span class="sxs-lookup"><span data-stu-id="45558-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="45558-143">Ele também pode criar pacote hello localmente usando Olá `-ConfigurationArchivePath` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="45558-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="45558-144">Caso contrário, ela publica o armazenamento de BLOBs do hello. ZIP arquivo tooAzure e protege-o com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="45558-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="45558-145">arquivo do Hello. zip criado por esse cmdlet tem script de configuração do hello. ps1 na raiz de saudação da pasta de arquivamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="45558-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="45558-146">Os recursos têm pasta do módulo Olá colocada na pasta de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="45558-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="45558-147">`Set-AzureVMDscExtension`Insere as configurações de saudação necessárias por Olá extensão de DSC do PowerShell em um objeto de configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="45558-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="45558-148">No modelo de implantação clássico hello, alterações VM de saudação devem ser aplicada tooan VM do Azure com `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="45558-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="45558-149">`Get-AzureVMDscExtension`recupera o status da extensão DSC saudação de uma VM específica.</span><span class="sxs-lookup"><span data-stu-id="45558-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="45558-150">`Get-AzureVMDscExtensionStatus`recupera o status de saudação da configuração de DSC Olá imposta pelo manipulador de extensão de DSC hello.</span><span class="sxs-lookup"><span data-stu-id="45558-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="45558-151">Essa ação pode ser executada em uma única VM ou em um grupo de VMs.</span><span class="sxs-lookup"><span data-stu-id="45558-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="45558-152">`Remove-AzureVMDscExtension`Remove o manipulador de extensão de saudação de uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45558-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="45558-153">Este cmdlet não **não** remover configuração hello, desinstalar Olá WMF ou alterar configurações de saudação aplicada na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="45558-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="45558-154">Ela remove somente o manipulador de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="45558-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="45558-155">**Principais diferenças nos cmdlets do ASM e do Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="45558-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="45558-156">Os cmdlets do Azure Resource Manager são síncronos.</span><span class="sxs-lookup"><span data-stu-id="45558-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="45558-157">Os cmdlets do ASM são assíncronos.</span><span class="sxs-lookup"><span data-stu-id="45558-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="45558-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version e Location são todos parâmetros obrigatórios no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45558-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="45558-159">ArchiveResourceGroupName é um novo parâmetro opcional para o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45558-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="45558-160">Você pode especificar esse parâmetro quando sua conta de armazenamento pertence tooa outro grupo de recursos que Olá um onde a máquina virtual de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="45558-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="45558-161">ConfigurationArchive é chamado de ArchiveBlobName no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45558-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="45558-162">ContainerName é chamado de ArchiveContainerName no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45558-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="45558-163">StorageEndpointSuffix é chamado de ArchiveStorageEndpointSuffix no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45558-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="45558-164">opção de atualização automática de Olá foi adicionada tooAzure tooenable do Gerenciador de recursos de saudação manipulador toohello mais recente versão da extensão como e quando ele está disponível a atualização automática.</span><span class="sxs-lookup"><span data-stu-id="45558-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="45558-165">Observe que esse parâmetro tem possíveis reinicializações de toocause Olá Olá VM quando uma nova versão do hello que WMF é liberado.</span><span class="sxs-lookup"><span data-stu-id="45558-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="45558-166">Funcionalidade do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="45558-166">Azure portal functionality</span></span>
<span data-ttu-id="45558-167">Procure tooa VM.</span><span class="sxs-lookup"><span data-stu-id="45558-167">Browse tooa VM.</span></span> <span data-ttu-id="45558-168">Em Configurações -> Geral, clique em "Extensões".</span><span class="sxs-lookup"><span data-stu-id="45558-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="45558-169">Um novo painel é criado.</span><span class="sxs-lookup"><span data-stu-id="45558-169">A new pane is created.</span></span> <span data-ttu-id="45558-170">Clique em "Adicionar" e selecione DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45558-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="45558-171">portal de saudação precisa de entrada.</span><span class="sxs-lookup"><span data-stu-id="45558-171">hello portal needs input.</span></span>
<span data-ttu-id="45558-172">**Script ou módulos de configuração**: esse campo é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="45558-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="45558-173">Requer um arquivo. ps1 que contém um script de configuração ou um arquivo. zip com um script de configuração na raiz de hello. ps1 e todos os recursos dependentes em pastas de módulo em Olá arquivos. zip.</span><span class="sxs-lookup"><span data-stu-id="45558-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="45558-174">Ele pode ser criado com hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` incluído no SDK do Azure PowerShell de saudação do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45558-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="45558-175">arquivo. zip de saudação é carregado em seu armazenamento de blob de usuário protegido por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="45558-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="45558-176">**Arquivo de configuração PSD1 de dados**: esse campo é opcional.</span><span class="sxs-lookup"><span data-stu-id="45558-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="45558-177">Se sua configuração requer um arquivo de dados de configuração em. psd1, use este campo tooselect-lo e carregue-o armazenamento de BLOBs do usuário tooyour, onde ele é protegido por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="45558-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="45558-178">**Nome de configuração qualificado por módulo**: os arquivos .ps1 podem ter várias funções de configuração.</span><span class="sxs-lookup"><span data-stu-id="45558-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="45558-179">Digite nome Olá Olá. ps1 do script de configuração seguido por um '\' e Olá nome da função de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="45558-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="45558-180">Por exemplo, se seu script. ps1 tem nome hello "configuration.ps1", e a configuração de saudação é "IisInstall", digite:`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="45558-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="45558-181">**Argumentos de configuração**: se a função de configuração Olá utiliza argumentos, digite-os aqui no formato Olá `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="45558-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="45558-182">Observe que esse formato é diferente daquele como argumentos de configuração são aceitos por meio de cmdlets do PowerShell ou modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45558-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="45558-183">Introdução</span><span class="sxs-lookup"><span data-stu-id="45558-183">Getting started</span></span>
<span data-ttu-id="45558-184">Olá extensão de DSC do Azure usa documentos de configuração DSC e aplica-los em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="45558-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="45558-185">A seguir está um exemplo simples de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="45558-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="45558-186">Salve localmente como "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="45558-186">Save it locally as "IisInstall.ps1":</span></span>

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

<span data-ttu-id="45558-187">Olá seguindo as etapas local Olá IisInstall.ps1 script na Olá especificado VM, executar configuração hello e relatar sobre o status.</span><span class="sxs-lookup"><span data-stu-id="45558-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="45558-188">Modelo clássico</span><span class="sxs-lookup"><span data-stu-id="45558-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="45558-189">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45558-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="45558-190">Registro em log</span><span class="sxs-lookup"><span data-stu-id="45558-190">Logging</span></span>
<span data-ttu-id="45558-191">Os logs são colocados em:</span><span class="sxs-lookup"><span data-stu-id="45558-191">Logs are placed in:</span></span>

<span data-ttu-id="45558-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Número de versão]</span><span class="sxs-lookup"><span data-stu-id="45558-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="45558-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45558-193">Next steps</span></span>
<span data-ttu-id="45558-194">Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="45558-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="45558-195">Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45558-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="45558-196">toofind funcionalidade adicional que você pode gerenciar com o PowerShell DSC, [procurar a Galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para obter mais recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="45558-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="45558-197">Para obter detalhes sobre como passar parâmetros confidenciais em configurações, consulte [gerenciar credenciais com segurança com o manipulador de extensão Olá DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45558-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

