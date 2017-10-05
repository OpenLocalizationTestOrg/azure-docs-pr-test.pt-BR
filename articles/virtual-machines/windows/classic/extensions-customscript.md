---
title: "Extensão de Script Personalizado em uma VM do Windows | Microsoft Docs"
description: "Automatizar tarefas de configuração de VM do Azure usando a extensão de Script Personalizado para executar scripts do PowerShell em uma VM remota do Windows"
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
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="54c1f-103">Extensão de Script Personalizado para Windows usando o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="54c1f-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="54c1f-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="54c1f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="54c1f-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="54c1f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="54c1f-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="54c1f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="54c1f-107">Saiba como [executar estas etapas usando o modelo do Resource Manager](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54c1f-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="54c1f-108">A extensão de script personalizado baixa e executa scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="54c1f-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="54c1f-109">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="54c1f-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="54c1f-110">Os scripts podem ser baixados do armazenamento do Azure ou do GitHub, ou fornecidos ao Portal do Azure no tempo de execução da extensão.</span><span class="sxs-lookup"><span data-stu-id="54c1f-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="54c1f-111">A extensão de script personalizado se integra com modelos do Azure Resource Manager e também pode ser executada usando a CLI do Azure, o PowerShell, o portal do Azure ou a API REST da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="54c1f-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="54c1f-112">Este documento detalha como usar a Extensão de Script Personalizado usando o módulo do Azure PowerShell e modelos do Azure Resource Manager, além de detalhar as etapas da solução de problemas em sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="54c1f-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54c1f-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54c1f-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="54c1f-114">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="54c1f-114">Operating System</span></span>

<span data-ttu-id="54c1f-115">A Extensão de Script Personalizado para Windows pode ser executada nas versões 2008 R2, 2012, 2012 R2 e 2016 do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="54c1f-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="54c1f-116">Local do script</span><span class="sxs-lookup"><span data-stu-id="54c1f-116">Script Location</span></span>

<span data-ttu-id="54c1f-117">O script precisa ser armazenado no armazenamento do Azure ou em qualquer outro local acessível por meio de uma URL válida.</span><span class="sxs-lookup"><span data-stu-id="54c1f-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="54c1f-118">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="54c1f-118">Internet Connectivity</span></span>

<span data-ttu-id="54c1f-119">A Extensão de Script Personalizado para Windows requer que a máquina virtual de destino esteja conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="54c1f-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="54c1f-120">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="54c1f-120">Extension schema</span></span>

<span data-ttu-id="54c1f-121">O JSON a seguir mostra o esquema para a Extensão de Script Personalizado.</span><span class="sxs-lookup"><span data-stu-id="54c1f-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="54c1f-122">A extensão requer um local de script (Armazenamento do Azure ou outro local com URL válida) e um comando a ser executado.</span><span class="sxs-lookup"><span data-stu-id="54c1f-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="54c1f-123">Se estiver usando o Armazenamento do Azure como a origem do script, o nome e a chave da conta de armazenamento do Azure são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="54c1f-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="54c1f-124">Esses itens devem ser tratados como dados confidenciais e especificados na configuração de definição protegida por extensões.</span><span class="sxs-lookup"><span data-stu-id="54c1f-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="54c1f-125">Os dados de configuração protegidos pela extensão da VM do Azure são criptografados, sendo descriptografados apenas na máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="54c1f-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="54c1f-126">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="54c1f-126">Property values</span></span>

| <span data-ttu-id="54c1f-127">Nome</span><span class="sxs-lookup"><span data-stu-id="54c1f-127">Name</span></span> | <span data-ttu-id="54c1f-128">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="54c1f-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="54c1f-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="54c1f-129">apiVersion</span></span> | <span data-ttu-id="54c1f-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="54c1f-130">2015-06-15</span></span> |
| <span data-ttu-id="54c1f-131">publicador</span><span class="sxs-lookup"><span data-stu-id="54c1f-131">publisher</span></span> | <span data-ttu-id="54c1f-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="54c1f-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="54c1f-133">extensão</span><span class="sxs-lookup"><span data-stu-id="54c1f-133">extension</span></span> | <span data-ttu-id="54c1f-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="54c1f-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="54c1f-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="54c1f-135">typeHandlerVersion</span></span> | <span data-ttu-id="54c1f-136">1.8</span><span class="sxs-lookup"><span data-stu-id="54c1f-136">1.8</span></span> |
| <span data-ttu-id="54c1f-137">fileUris (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="54c1f-137">fileUris (e.g)</span></span> | <span data-ttu-id="54c1f-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="54c1f-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="54c1f-139">commandToExecute (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="54c1f-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="54c1f-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="54c1f-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="54c1f-141">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="54c1f-141">Template deployment</span></span>

<span data-ttu-id="54c1f-142">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54c1f-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="54c1f-143">O esquema JSON detalhado na seção anterior pode ser usado em um modelo do Azure Resource Manager para executar a Extensão de Script Personalizado durante uma implantação de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54c1f-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="54c1f-144">Um modelo de exemplo que inclui a Extensão de Script Personalizado pode ser encontrado aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="54c1f-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="54c1f-145">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="54c1f-145">PowerShell deployment</span></span>

<span data-ttu-id="54c1f-146">O comando `Set-AzureVMCustomScriptExtension` pode ser usado para adicionar a Extensão de Script Personalizado a uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="54c1f-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="54c1f-147">Para saber mais, confira [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="54c1f-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="54c1f-148">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="54c1f-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="54c1f-149">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="54c1f-149">Troubleshoot</span></span>

<span data-ttu-id="54c1f-150">Os dados sobre o estado das implantações de extensão podem ser recuperados no Portal do Azure usando o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54c1f-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="54c1f-151">Para ver o estado da implantação das extensões de uma determinada VM, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="54c1f-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="54c1f-152">A saída de execução da extensão é registrada nos arquivos localizados no diretório a seguir da máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="54c1f-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="54c1f-153">O script propriamente dito é baixado no diretório a seguir na máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="54c1f-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="54c1f-154">Suporte</span><span class="sxs-lookup"><span data-stu-id="54c1f-154">Support</span></span>

<span data-ttu-id="54c1f-155">Caso precise de mais ajuda em qualquer ponto deste artigo, entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="54c1f-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="54c1f-156">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="54c1f-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="54c1f-157">Vá para o [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione Obter suporte.</span><span class="sxs-lookup"><span data-stu-id="54c1f-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="54c1f-158">Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="54c1f-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>