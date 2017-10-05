---
title: "Recursos e extensões da máquina virtual para Windows no Azure | Microsoft Docs"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="cc898-103">Recursos e extensões da máquina virtual para Windows</span><span class="sxs-lookup"><span data-stu-id="cc898-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="cc898-104">Extensões da máquina virtual do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="cc898-105">Por exemplo, se uma máquina virtual exigir a instalação de software, proteção antivírus ou a configuração do Docker, uma extensão da VM poderá ser usada para concluir essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="cc898-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="cc898-106">As extensões da VM do Azure podem ser executadas usando a CLI do Azure, o PowerShell, modelos do Azure Resource Manager e o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="cc898-107">Extensões podem ser agrupadas com uma nova implantação de máquina virtual ou executar qualquer sistema existente.</span><span class="sxs-lookup"><span data-stu-id="cc898-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="cc898-108">Este documento fornece uma visão geral das extensões da máquina virtual, pré-requisitos para utilização das extensões da máquina virtual e orientação sobre como detectar, gerenciar e remover extensões da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc898-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="cc898-109">Este documento fornece informações generalizadas, pois há muitas extensões de VM disponíveis e cada uma delas tem uma configuração possivelmente exclusiva.</span><span class="sxs-lookup"><span data-stu-id="cc898-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="cc898-110">Encontre detalhes específicos sobre cada extensão na documentação individual.</span><span class="sxs-lookup"><span data-stu-id="cc898-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="cc898-111">Casos de uso e exemplos</span><span class="sxs-lookup"><span data-stu-id="cc898-111">Use cases and samples</span></span>

<span data-ttu-id="cc898-112">Há várias extensões de VM do Azure diferentes disponíveis, cada uma com um caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="cc898-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="cc898-113">Alguns exemplos de caso de uso são:</span><span class="sxs-lookup"><span data-stu-id="cc898-113">Some example use cases are:</span></span>

- <span data-ttu-id="cc898-114">Aplique as configurações de Estado Desejado do PowerShell a uma máquina virtual usando a extensão de DSC para Windows.</span><span class="sxs-lookup"><span data-stu-id="cc898-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="cc898-115">Para saber mais, confira [Extensão de configuração de Estado Desejado do Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="cc898-116">Configure o monitoramento da máquina virtual usando a extensão de VM do Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="cc898-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="cc898-117">Para saber mais, veja [Conectar máquinas virtuais do Azure ao Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="cc898-118">Configure o monitoramento de sua infraestrutura do Azure com a extensão Datadog.</span><span class="sxs-lookup"><span data-stu-id="cc898-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="cc898-119">Para saber mais, confira [blog Datadog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="cc898-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="cc898-120">Configure uma máquina virtual do Azure usando o Chef.</span><span class="sxs-lookup"><span data-stu-id="cc898-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="cc898-121">Para saber mais, veja [Automatizar a implantação de máquina virtual do Azure com o Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="cc898-122">Além de extensões específicas ao processo, uma extensão de Script Personalizado está disponível para máquinas virtuais Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="cc898-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="cc898-123">A extensão de Script personalizado para Windows permite a execução de qualquer script do PowerShell em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc898-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="cc898-124">Isso é útil para a criação de implantações do Azure que exigem uma configurações que vão além da capacidade das ferramentas nativas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="cc898-125">Para saber mais, veja [Extensão de Script personalizado de VM do Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cc898-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cc898-126">Prerequisites</span></span>

<span data-ttu-id="cc898-127">Cada extensão da máquina virtual pode ter seu próprio conjunto de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="cc898-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="cc898-128">Por exemplo, a extensão de VM do Docker tem um pré-requisito de uma distribuição Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="cc898-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="cc898-129">Os requisitos específicos das extensões estão detalhados na documentação associada.</span><span class="sxs-lookup"><span data-stu-id="cc898-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="cc898-130">Agente de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-130">Azure VM agent</span></span>
<span data-ttu-id="cc898-131">O Agente de VM do Azure gerencia a interação entre uma máquina virtual do Azure e o controlador de malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="cc898-132">O agente de VM é responsável por muitos aspectos funcionais de implantação e gerenciamento de máquinas virtuais do Azure, incluindo a execução de extensões da VM.</span><span class="sxs-lookup"><span data-stu-id="cc898-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="cc898-133">O agente de VM do Azure é pré-instalado em imagens do Azure Marketplace e pode ser instalado em sistemas operacionais compatíveis.</span><span class="sxs-lookup"><span data-stu-id="cc898-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="cc898-134">Para saber mais sobre os sistemas operacionais com suporte e as instruções de instalação, confira [Agente de máquina virtual do Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="cc898-135">Descobrir extensões de VM</span><span class="sxs-lookup"><span data-stu-id="cc898-135">Discover VM extensions</span></span>
<span data-ttu-id="cc898-136">Muitas extensões de VM diferentes estão disponíveis para uso com as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="cc898-137">Para ver uma lista completa, execute o comando a seguir com o módulo do Azure Resource Manager PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc898-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="cc898-138">Especifique o local desejado ao executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="cc898-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="cc898-139">Executar extensões de VM</span><span class="sxs-lookup"><span data-stu-id="cc898-139">Run VM extensions</span></span>

<span data-ttu-id="cc898-140">As extensões da máquina virtual do Azure podem ser executadas em máquinas virtuais existentes, o que é útil quando você precisa fazer alterações de configuração ou recuperar a conectividade em uma VM já implantada.</span><span class="sxs-lookup"><span data-stu-id="cc898-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="cc898-141">As extensões de VM também podem ser agrupadas com implantações de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc898-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="cc898-142">Ao usar extensões com modelos do Resource Manager, as máquinas virtuais do Azure podem ser implantadas e configuradas sem a necessidade de intervenção pós-implantação.</span><span class="sxs-lookup"><span data-stu-id="cc898-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="cc898-143">Os métodos a seguir podem ser usados para executar uma extensão em uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="cc898-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="cc898-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc898-144">PowerShell</span></span>

<span data-ttu-id="cc898-145">Há vários comandos do PowerShell para a execução de extensões individuais.</span><span class="sxs-lookup"><span data-stu-id="cc898-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="cc898-146">Para ver uma lista, execute os comandos do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc898-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="cc898-147">O resultado é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="cc898-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="cc898-148">O exemplo a seguir usa a extensão de Script personalizado para baixar um script de um repositório do GitHub para a máquina virtual de destino e, em seguida, executa o script.</span><span class="sxs-lookup"><span data-stu-id="cc898-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="cc898-149">Para saber mais sobre como usar a extensão de Script personalizado, veja [Visão geral da extensão de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="cc898-150">Neste exemplo, a extensão de acesso à VM é usada para redefinir a senha administrativa de uma máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="cc898-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="cc898-151">Para saber mais sobre a extensão de acesso à VM, veja [Serviço de redefinição de área de trabalho remota em uma VM do Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="cc898-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="cc898-152">O comando `Set-AzureRmVMExtension` pode ser usado para iniciar qualquer extensão de VM.</span><span class="sxs-lookup"><span data-stu-id="cc898-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="cc898-153">Para saber mais, veja a [referência de Set-AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc898-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="cc898-154">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-154">Azure portal</span></span>

<span data-ttu-id="cc898-155">É possível aplicar extensões de VM a uma máquina virtual existente por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="cc898-156">Para fazer isso, selecione a máquina virtual que deseja usar, escolha **Extensões** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cc898-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="cc898-157">Isso fornece uma lista de extensões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cc898-157">This provides a list of available extensions.</span></span> <span data-ttu-id="cc898-158">Selecione a desejada e siga as instruções no assistente.</span><span class="sxs-lookup"><span data-stu-id="cc898-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="cc898-159">A imagem a seguir mostra a instalação da extensão Microsoft Antimalware no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Instalar a extensão de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="cc898-161">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="cc898-162">É possível adicionar extensões de VM a um modelo do Azure Resource Manager e executá-las com a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="cc898-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="cc898-163">Implantar extensões com um modelo é útil para a criação de implantações do Azure totalmente configuradas.</span><span class="sxs-lookup"><span data-stu-id="cc898-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="cc898-164">Por exemplo, o JSON a seguir é obtido de um modelo do Resource Manager que implanta um conjunto de máquinas virtuais com balanceamento de carga e um banco de dados SQL do Azure e, em seguida, instala um aplicativo .NET Core em cada VM.</span><span class="sxs-lookup"><span data-stu-id="cc898-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="cc898-165">A extensão da VM se encarrega da instalação do software.</span><span class="sxs-lookup"><span data-stu-id="cc898-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="cc898-166">Para saber mais, confira o [Modelo completo do Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="cc898-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="cc898-167">Para saber mais, veja [Criação de modelos do Azure Resource Manager com extensões de VM do Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="cc898-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="cc898-168">Proteger dados de extensão da VM</span><span class="sxs-lookup"><span data-stu-id="cc898-168">Secure VM extension data</span></span>

<span data-ttu-id="cc898-169">Quando você estiver executando uma extensão de VM, talvez seja necessário incluir informações confidenciais, como credenciais, nomes de conta de armazenamento e chaves de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cc898-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="cc898-170">Muitas extensões de VM incluem uma configuração protegida que criptografa dados e os descriptografa somente dentro da máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="cc898-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="cc898-171">Cada extensão tem um esquema específico de configuração protegida, e cada um é detalhado na documentação específica associada à extensão.</span><span class="sxs-lookup"><span data-stu-id="cc898-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="cc898-172">O exemplo a seguir mostra uma instância da extensão Script personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="cc898-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="cc898-173">Observe que o comando a ser executado inclui um conjunto de credenciais.</span><span class="sxs-lookup"><span data-stu-id="cc898-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="cc898-174">Neste exemplo, o comando a ser executado não será criptografado.</span><span class="sxs-lookup"><span data-stu-id="cc898-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="cc898-175">Proteja a cadeia de caracteres de execução movendo a propriedade **command to execute** para a configuração **protected**.</span><span class="sxs-lookup"><span data-stu-id="cc898-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="cc898-176">Solucionar problemas de extensões de VM</span><span class="sxs-lookup"><span data-stu-id="cc898-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="cc898-177">Cada extensão de VM pode ter etapas de solução de problemas específicas.</span><span class="sxs-lookup"><span data-stu-id="cc898-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="cc898-178">Por exemplo, quando você está usando a extensão Script personalizado, é possível encontrar detalhes da execução do script localmente na máquina virtual na qual a extensão foi executada.</span><span class="sxs-lookup"><span data-stu-id="cc898-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="cc898-179">As etapas de solução de problemas específicas à extensão são detalhadas na documentação associada.</span><span class="sxs-lookup"><span data-stu-id="cc898-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="cc898-180">As etapas de solução de problemas a seguir aplicam-se a todas as extensões da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc898-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="cc898-181">Exibir o status da extensão</span><span class="sxs-lookup"><span data-stu-id="cc898-181">View extension status</span></span>

<span data-ttu-id="cc898-182">Após a execução da extensão da máquina virtual em uma máquina virtual, use o seguinte comando do PowerShell para retornar o status da extensão.</span><span class="sxs-lookup"><span data-stu-id="cc898-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="cc898-183">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cc898-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="cc898-184">O parâmetro `Name` usa o nome fornecido à extensão no momento da execução.</span><span class="sxs-lookup"><span data-stu-id="cc898-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="cc898-185">A saída se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cc898-185">The output looks like the following:</span></span>

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

<span data-ttu-id="cc898-186">O status de execução da extensão também pode ser encontrado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="cc898-187">Para exibir o status de uma extensão, selecione a máquina virtual, escolha **Extensões** e selecione a extensão desejada.</span><span class="sxs-lookup"><span data-stu-id="cc898-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="cc898-188">Executar extensões de VM novamente</span><span class="sxs-lookup"><span data-stu-id="cc898-188">Rerun VM extensions</span></span>

<span data-ttu-id="cc898-189">Pode haver casos nos quais uma extensão da máquina virtual precisa ser executada novamente.</span><span class="sxs-lookup"><span data-stu-id="cc898-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="cc898-190">Faça isso removendo a extensão e, em seguida, executando novamente a extensão com um método de execução de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="cc898-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="cc898-191">Para remover uma extensão, execute o seguinte comando com o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc898-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="cc898-192">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cc898-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="cc898-193">Uma extensão também pode ser removida usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc898-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="cc898-194">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="cc898-194">To do so:</span></span>

1. <span data-ttu-id="cc898-195">Selecione uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc898-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="cc898-196">Selecione **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="cc898-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="cc898-197">Escolha a extensão desejada.</span><span class="sxs-lookup"><span data-stu-id="cc898-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="cc898-198">Selecione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="cc898-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="cc898-199">Referência a extensões de VM comuns</span><span class="sxs-lookup"><span data-stu-id="cc898-199">Common VM extensions reference</span></span>
| <span data-ttu-id="cc898-200">Nome da extensão</span><span class="sxs-lookup"><span data-stu-id="cc898-200">Extension name</span></span> | <span data-ttu-id="cc898-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="cc898-201">Description</span></span> | <span data-ttu-id="cc898-202">Mais informações</span><span class="sxs-lookup"><span data-stu-id="cc898-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc898-203">Extensão de script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="cc898-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="cc898-204">Executar scripts em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="cc898-205">Extensão de script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="cc898-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="cc898-206">Extensão de DSC para o Windows</span><span class="sxs-lookup"><span data-stu-id="cc898-206">DSC Extension for Windows</span></span> |<span data-ttu-id="cc898-207">Extensão PowerShell DSC (Configuração de Estado Desejado)</span><span class="sxs-lookup"><span data-stu-id="cc898-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="cc898-208">Extensão DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="cc898-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="cc898-209">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="cc898-210">Gerenciar Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="cc898-211">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="cc898-212">Extensão de acesso à VM do Azure</span><span class="sxs-lookup"><span data-stu-id="cc898-212">Azure VM Access Extension</span></span> |<span data-ttu-id="cc898-213">Gerenciar usuários e credenciais</span><span class="sxs-lookup"><span data-stu-id="cc898-213">Manage users and credentials</span></span> |[<span data-ttu-id="cc898-214">Extensão de Acesso à VM para Linux</span><span class="sxs-lookup"><span data-stu-id="cc898-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
