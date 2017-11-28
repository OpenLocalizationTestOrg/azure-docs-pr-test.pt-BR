---
title: "aaaCustom extensão do Script em uma VM do Windows | Microsoft Docs"
description: "Automatizar tarefas de configuração de máquina virtual do Azure usando scripts do PowerShell Olá Script personalizado extensão toorun em uma VM remoto do Windows"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="74fce-103">Personalizado extensão para janelas de Script usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="74fce-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="74fce-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="74fce-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="74fce-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="74fce-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="74fce-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74fce-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="74fce-107">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74fce-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="74fce-108">Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="74fce-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="74fce-109">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="74fce-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="74fce-110">Scripts podem ser baixados do armazenamento do Azure ou GitHub ou fornecidos toohello portal do Azure em tempo de execução de extensão.</span><span class="sxs-lookup"><span data-stu-id="74fce-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="74fce-111">Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="74fce-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="74fce-112">Este documento detalha como toouse Olá extensão de Script personalizado usando Olá módulo PowerShell do Azure, modelos de Gerenciador de recursos do Azure e detalhes de solução de problemas etapas em sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="74fce-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74fce-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74fce-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="74fce-114">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="74fce-114">Operating System</span></span>

<span data-ttu-id="74fce-115">Olá extensão de Script personalizado para o Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="74fce-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="74fce-116">Local do script</span><span class="sxs-lookup"><span data-stu-id="74fce-116">Script Location</span></span>

<span data-ttu-id="74fce-117">script de saudação precisa toobe armazenado no armazenamento do Azure, ou qualquer outro local acessível por meio de uma URL válida.</span><span class="sxs-lookup"><span data-stu-id="74fce-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="74fce-118">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="74fce-118">Internet Connectivity</span></span>

<span data-ttu-id="74fce-119">Olá extensão para janelas de Script personalizado requer que a máquina virtual Olá destino toohello conectado à internet.</span><span class="sxs-lookup"><span data-stu-id="74fce-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="74fce-120">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="74fce-120">Extension schema</span></span>

<span data-ttu-id="74fce-121">Olá JSON a seguir mostra esquema Olá Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="74fce-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="74fce-122">extensão de saudação requer um local de script (armazenamento do Azure ou em outro local com URL válida) e um comando tooexecute.</span><span class="sxs-lookup"><span data-stu-id="74fce-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="74fce-123">Se usar o armazenamento do Azure como fonte do script hello, uma chave de nome e uma conta de conta do armazenamento do Azure é necessária.</span><span class="sxs-lookup"><span data-stu-id="74fce-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="74fce-124">Esses itens devem ser tratados como dados confidenciais e especificados na configuração de configuração protegida Olá extensões.</span><span class="sxs-lookup"><span data-stu-id="74fce-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="74fce-125">Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="74fce-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="74fce-126">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="74fce-126">Property values</span></span>

| <span data-ttu-id="74fce-127">Nome</span><span class="sxs-lookup"><span data-stu-id="74fce-127">Name</span></span> | <span data-ttu-id="74fce-128">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="74fce-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="74fce-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="74fce-129">apiVersion</span></span> | <span data-ttu-id="74fce-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="74fce-130">2015-06-15</span></span> |
| <span data-ttu-id="74fce-131">publicador</span><span class="sxs-lookup"><span data-stu-id="74fce-131">publisher</span></span> | <span data-ttu-id="74fce-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="74fce-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="74fce-133">extensão</span><span class="sxs-lookup"><span data-stu-id="74fce-133">extension</span></span> | <span data-ttu-id="74fce-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="74fce-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="74fce-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="74fce-135">typeHandlerVersion</span></span> | <span data-ttu-id="74fce-136">1.8</span><span class="sxs-lookup"><span data-stu-id="74fce-136">1.8</span></span> |
| <span data-ttu-id="74fce-137">fileUris (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="74fce-137">fileUris (e.g)</span></span> | <span data-ttu-id="74fce-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="74fce-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="74fce-139">commandToExecute (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="74fce-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="74fce-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="74fce-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="74fce-141">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="74fce-141">Template deployment</span></span>

<span data-ttu-id="74fce-142">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74fce-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="74fce-143">esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão de Script personalizado durante uma implantação de modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="74fce-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="74fce-144">Um modelo de exemplo que inclui Olá extensão de Script personalizado podem ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="74fce-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="74fce-145">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="74fce-145">PowerShell deployment</span></span>

<span data-ttu-id="74fce-146">Olá `Set-AzureVMCustomScriptExtension` comando pode ser usado tooadd Olá Script personalizado extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="74fce-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="74fce-147">Para saber mais, confira [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="74fce-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="74fce-148">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="74fce-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="74fce-149">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="74fce-149">Troubleshoot</span></span>

<span data-ttu-id="74fce-150">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74fce-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="74fce-151">estado da implantação toosee Olá de extensões para uma determinada VM, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="74fce-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="74fce-152">Execução de extensão de saída nos toofiles conectado encontrado no hello diretório a seguir na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="74fce-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="74fce-153">script Hello propriamente dito é baixado em Olá diretório a seguir na máquina de virtual de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="74fce-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="74fce-154">Suporte</span><span class="sxs-lookup"><span data-stu-id="74fce-154">Support</span></span>

<span data-ttu-id="74fce-155">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="74fce-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="74fce-156">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="74fce-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="74fce-157">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="74fce-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="74fce-158">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="74fce-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
