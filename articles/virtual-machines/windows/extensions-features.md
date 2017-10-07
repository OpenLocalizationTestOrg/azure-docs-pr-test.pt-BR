---
title: "aaaVirtual computador extensões e recursos do Windows no Azure | Microsoft Docs"
description: "Saiba quais extensões estão disponíveis para as máquinas virtuais do Azure, agrupadas pelas funcionalidades fornecidas ou aperfeiçoadas."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="49898-103">Recursos e extensões da máquina virtual para Windows</span><span class="sxs-lookup"><span data-stu-id="49898-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="49898-104">Extensões da máquina virtual do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="49898-105">Por exemplo, se uma máquina virtual requer a instalação de software, proteção contra vírus ou a configuração do Docker, uma extensão de VM pode ser usado toocomplete essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="49898-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="49898-106">Extensões VM do Azure podem ser executadas usando Olá CLI do Azure, o PowerShell, modelos do Gerenciador de recursos do Azure e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="49898-107">Extensões podem ser agrupadas com uma nova implantação de máquina virtual ou executar qualquer sistema existente.</span><span class="sxs-lookup"><span data-stu-id="49898-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="49898-108">Este documento fornece uma visão geral de extensões de máquina virtual, pré-requisitos para usar extensões de máquina virtual e orientação sobre como toodetect, gerenciar e remover extensões de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49898-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="49898-109">Este documento fornece informações generalizadas, pois há muitas extensões de VM disponíveis e cada uma delas tem uma configuração possivelmente exclusiva.</span><span class="sxs-lookup"><span data-stu-id="49898-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="49898-110">Detalhes de extensão podem ser encontrados em cada extensão individuais do documento toohello específico.</span><span class="sxs-lookup"><span data-stu-id="49898-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="49898-111">Casos de uso e exemplos</span><span class="sxs-lookup"><span data-stu-id="49898-111">Use cases and samples</span></span>

<span data-ttu-id="49898-112">Há várias extensões de VM do Azure diferentes disponíveis, cada uma com um caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="49898-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="49898-113">Alguns exemplos de caso de uso são:</span><span class="sxs-lookup"><span data-stu-id="49898-113">Some example use cases are:</span></span>

- <span data-ttu-id="49898-114">Se aplicam a máquina virtual do PowerShell Desired estado configurações tooa usando a extensão de saudação DSC para Windows.</span><span class="sxs-lookup"><span data-stu-id="49898-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="49898-115">Para saber mais, confira [Extensão de configuração de Estado Desejado do Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49898-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="49898-116">Configure o monitoramento de máquina virtual usando a extensão de VM do agente de monitoramento Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="49898-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="49898-117">Para obter mais informações, consulte [tooLog de máquinas virtuais do Azure conectar análise](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="49898-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="49898-118">Configure o monitoramento da infra-estrutura do Azure com hello Datadog extensão.</span><span class="sxs-lookup"><span data-stu-id="49898-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="49898-119">Para obter mais informações, consulte Olá [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="49898-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="49898-120">Configure uma máquina virtual do Azure usando o Chef.</span><span class="sxs-lookup"><span data-stu-id="49898-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="49898-121">Para saber mais, veja [Automatizar a implantação de máquina virtual do Azure com o Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="49898-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="49898-122">Além disso extensões específicas de tooprocess, uma extensão de Script personalizado está disponível para máquinas virtuais Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="49898-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="49898-123">Olá extensão de Script personalizado para o Windows permite que qualquer toobe de script do PowerShell executado em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49898-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="49898-124">Isso é útil para a criação de implantações do Azure que exigem uma configurações que vão além da capacidade das ferramentas nativas do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="49898-125">Para saber mais, veja [Extensão de Script personalizado de VM do Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="49898-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="49898-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49898-126">Prerequisites</span></span>

<span data-ttu-id="49898-127">Cada extensão da máquina virtual pode ter seu próprio conjunto de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="49898-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="49898-128">Por exemplo, Olá extensão da VM Docker tem um pré-requisito de uma distribuição de Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="49898-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="49898-129">Requisitos das extensões individuais são detalhados na documentação do hello específicas da extensão.</span><span class="sxs-lookup"><span data-stu-id="49898-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="49898-130">Agente de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-130">Azure VM agent</span></span>
<span data-ttu-id="49898-131">Agente de VM do Azure Olá gerencia a interação entre uma máquina virtual do Azure e o controlador de malha do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="49898-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="49898-132">Olá VM agent é responsável por muitos aspectos funcionais de implantação e gerenciamento de máquinas virtuais do Azure, incluindo a execução de extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="49898-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="49898-133">Agente de VM do Azure Olá foi pré-instalado no imagens do Azure Marketplace e pode ser instalado em sistemas operacionais com suporte.</span><span class="sxs-lookup"><span data-stu-id="49898-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="49898-134">Para saber mais sobre os sistemas operacionais com suporte e as instruções de instalação, confira [Agente de máquina virtual do Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="49898-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="49898-135">Descobrir extensões de VM</span><span class="sxs-lookup"><span data-stu-id="49898-135">Discover VM extensions</span></span>
<span data-ttu-id="49898-136">Muitas extensões de VM diferentes estão disponíveis para uso com as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="49898-137">toosee uma lista completa, execute Olá comando com o módulo do PowerShell do Azure Resource Manager Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="49898-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="49898-138">Tornar-se de local de saudação desejada de toospecify quando você estiver executando este comando.</span><span class="sxs-lookup"><span data-stu-id="49898-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="49898-139">Executar extensões de VM</span><span class="sxs-lookup"><span data-stu-id="49898-139">Run VM extensions</span></span>

<span data-ttu-id="49898-140">Extensões de máquina virtual do Azure podem ser executadas em máquinas virtuais existentes, que é útil quando você precisa toomake alterações de configuração ou recuperar de conectividade em uma VM já implantada.</span><span class="sxs-lookup"><span data-stu-id="49898-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="49898-141">As extensões de VM também podem ser agrupadas com implantações de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49898-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="49898-142">Usando extensões com modelos do Gerenciador de recursos, você pode habilitar toobe de máquinas virtuais do Azure implantadas e configuradas sem necessidade de saudação de intervenção de pós-implantação.</span><span class="sxs-lookup"><span data-stu-id="49898-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="49898-143">Olá métodos a seguir pode ser usado toorun uma extensão em uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="49898-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="49898-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49898-144">PowerShell</span></span>

<span data-ttu-id="49898-145">Há vários comandos do PowerShell para a execução de extensões individuais.</span><span class="sxs-lookup"><span data-stu-id="49898-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="49898-146">toosee executar Olá comandos do PowerShell a seguir uma lista.</span><span class="sxs-lookup"><span data-stu-id="49898-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="49898-147">Isso fornece o seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="49898-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="49898-148">Hello exemplo a seguir usa toodownload de extensão de Script personalizado Olá um script de um repositório GitHub em Olá máquina de virtual de destino e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="49898-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="49898-149">Para obter mais informações sobre Olá extensão de Script personalizado, consulte [visão geral de extensões de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="49898-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="49898-150">Neste exemplo, Olá extensão de acesso da máquina virtual é a senha administrativa do hello tooreset usados de uma máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="49898-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="49898-151">Para obter mais informações sobre Olá extensão de acesso da máquina virtual, consulte [serviço de redefinição de área de trabalho remota em uma VM do Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="49898-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="49898-152">Olá `Set-AzureRmVMExtension` comando pode ser usado toostart qualquer extensão VM.</span><span class="sxs-lookup"><span data-stu-id="49898-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="49898-153">Para obter mais informações, consulte Olá [referência de conjunto AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="49898-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="49898-154">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-154">Azure portal</span></span>

<span data-ttu-id="49898-155">Uma extensão de VM pode ser aplicado tooan de máquina virtual existente por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="49898-156">toodo portanto, selecione a máquina virtual de saudação deseja toouse, escolha **extensões**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49898-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="49898-157">Isso fornece uma lista de extensões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="49898-157">This provides a list of available extensions.</span></span> <span data-ttu-id="49898-158">Selecione Olá desejada e siga as etapas de saudação do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="49898-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="49898-159">Olá imagem a seguir mostra instalação Olá Olá extensão Antimalware da Microsoft da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Instalar a extensão de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="49898-161">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="49898-162">Extensões de VM podem ser adicionado tooan Azure Resource Manager modelo e executado com a implantação de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49898-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="49898-163">Implantar extensões com um modelo é útil para a criação de implantações do Azure totalmente configuradas.</span><span class="sxs-lookup"><span data-stu-id="49898-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="49898-164">Por exemplo, hello que JSON a seguir é obtido de um modelo do Gerenciador de recursos que implanta um conjunto de VMs com balanceamento de carga e um banco de dados do SQL Azure e, em seguida, instala um aplicativo .NET Core em cada VM.</span><span class="sxs-lookup"><span data-stu-id="49898-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="49898-165">Olá extensão de VM cuida Olá da instalação do software.</span><span class="sxs-lookup"><span data-stu-id="49898-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="49898-166">Para obter mais informações, consulte Olá [modelo completo do Gerenciador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="49898-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="49898-167">Para saber mais, veja [Criação de modelos do Azure Resource Manager com extensões de VM do Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="49898-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="49898-168">Proteger dados de extensão da VM</span><span class="sxs-lookup"><span data-stu-id="49898-168">Secure VM extension data</span></span>

<span data-ttu-id="49898-169">Quando você estiver executando uma extensão de VM, talvez seja necessário tooinclude informações confidenciais, como as credenciais, nomes de conta de armazenamento e chaves de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49898-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="49898-170">Muitas extensões VM incluem uma configuração protegida que criptografa os dados e a descriptografa apenas dentro de saudação máquina de virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="49898-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="49898-171">Cada extensão tem um esquema específico de configuração protegida, e cada um é detalhado na documentação específica associada à extensão.</span><span class="sxs-lookup"><span data-stu-id="49898-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="49898-172">saudação de exemplo a seguir mostra uma instância do hello extensão de Script personalizado para o Windows.</span><span class="sxs-lookup"><span data-stu-id="49898-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="49898-173">Observe que tooexecute de comando Olá inclui um conjunto de credenciais.</span><span class="sxs-lookup"><span data-stu-id="49898-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="49898-174">Neste exemplo, a saudação comando tooexecute não será criptografado.</span><span class="sxs-lookup"><span data-stu-id="49898-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="49898-175">Proteger a cadeia de caracteres de execução de saudação movendo Olá **comando tooexecute** propriedade toohello **protegido** configuração.</span><span class="sxs-lookup"><span data-stu-id="49898-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="49898-176">Solucionar problemas de extensões de VM</span><span class="sxs-lookup"><span data-stu-id="49898-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="49898-177">Cada extensão de VM pode ter etapas de solução de problemas específicas.</span><span class="sxs-lookup"><span data-stu-id="49898-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="49898-178">Por exemplo, quando você estiver usando a extensão de Script personalizado hello, detalhes de execução de script podem ser encontrados localmente na Olá máquina virtual no qual a extensão de saudação foi executado.</span><span class="sxs-lookup"><span data-stu-id="49898-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="49898-179">As etapas de solução de problemas específicas à extensão são detalhadas na documentação associada.</span><span class="sxs-lookup"><span data-stu-id="49898-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="49898-180">Olá etapas de solução de problemas a seguir se aplicam a tooall extensões de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49898-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="49898-181">Exibir o status da extensão</span><span class="sxs-lookup"><span data-stu-id="49898-181">View extension status</span></span>

<span data-ttu-id="49898-182">Depois que uma extensão de máquina virtual tiver sido executada em uma máquina virtual, use Olá status da extensão de tooreturn comando PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="49898-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="49898-183">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="49898-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="49898-184">Olá `Name` parâmetro aceita nome hello dado toohello extensão em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="49898-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="49898-185">saída de Hello semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="49898-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="49898-186">Status da extensão de execução também podem ser encontradas no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="49898-187">status de saudação tooview de uma extensão, a máquina virtual de select Olá, escolha **extensões**, e selecione Olá extensão desejado.</span><span class="sxs-lookup"><span data-stu-id="49898-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="49898-188">Executar extensões de VM novamente</span><span class="sxs-lookup"><span data-stu-id="49898-188">Rerun VM extensions</span></span>

<span data-ttu-id="49898-189">Pode haver casos em que uma extensão de máquina virtual deve toobe novamente.</span><span class="sxs-lookup"><span data-stu-id="49898-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="49898-190">Você pode fazer isso, removendo a extensão hello e, em seguida, executar novamente a extensão de saudação com um método de execução de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="49898-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="49898-191">tooremove uma extensão, executar Olá comando com o módulo do PowerShell do Azure Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="49898-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="49898-192">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="49898-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="49898-193">Uma extensão também pode ser removida usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49898-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="49898-194">toodo para:</span><span class="sxs-lookup"><span data-stu-id="49898-194">toodo so:</span></span>

1. <span data-ttu-id="49898-195">Selecione uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49898-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="49898-196">Selecione **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="49898-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="49898-197">Escolha a extensão de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="49898-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="49898-198">Selecione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="49898-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="49898-199">Referência a extensões de VM comuns</span><span class="sxs-lookup"><span data-stu-id="49898-199">Common VM extensions reference</span></span>
| <span data-ttu-id="49898-200">Nome da extensão</span><span class="sxs-lookup"><span data-stu-id="49898-200">Extension name</span></span> | <span data-ttu-id="49898-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="49898-201">Description</span></span> | <span data-ttu-id="49898-202">Mais informações</span><span class="sxs-lookup"><span data-stu-id="49898-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49898-203">Extensão de script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="49898-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="49898-204">Executar scripts em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="49898-205">Extensão de script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="49898-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="49898-206">Extensão de DSC para o Windows</span><span class="sxs-lookup"><span data-stu-id="49898-206">DSC Extension for Windows</span></span> |<span data-ttu-id="49898-207">Extensão PowerShell DSC (Configuração de Estado Desejado)</span><span class="sxs-lookup"><span data-stu-id="49898-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="49898-208">Extensão DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="49898-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="49898-209">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="49898-210">Gerenciar Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="49898-211">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="49898-212">Extensão de acesso à VM do Azure</span><span class="sxs-lookup"><span data-stu-id="49898-212">Azure VM Access Extension</span></span> |<span data-ttu-id="49898-213">Gerenciar usuários e credenciais</span><span class="sxs-lookup"><span data-stu-id="49898-213">Manage users and credentials</span></span> |[<span data-ttu-id="49898-214">Extensão de Acesso à VM para Linux</span><span class="sxs-lookup"><span data-stu-id="49898-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
