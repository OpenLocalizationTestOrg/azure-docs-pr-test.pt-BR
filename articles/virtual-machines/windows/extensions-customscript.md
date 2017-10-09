---
title: "aaaAzure extensão para janelas de Script personalizado | Microsoft Docs"
description: "Automatizar tarefas de configuração de máquina virtual do Windows usando a extensão de Script personalizado Olá"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="2d8df-103">Extensão de script personalizado para o Windows</span><span class="sxs-lookup"><span data-stu-id="2d8df-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="2d8df-104">Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8df-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="2d8df-105">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2d8df-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="2d8df-106">Scripts podem ser baixados do armazenamento do Azure ou GitHub ou fornecidos toohello portal do Azure em tempo de execução de extensão.</span><span class="sxs-lookup"><span data-stu-id="2d8df-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="2d8df-107">Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8df-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="2d8df-108">Este documento detalha como toouse Olá extensão de Script personalizado usando Olá módulo PowerShell do Azure, modelos de Gerenciador de recursos do Azure e detalhes de solução de problemas etapas em sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="2d8df-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d8df-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2d8df-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="2d8df-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="2d8df-110">Operating System</span></span>

<span data-ttu-id="2d8df-111">Olá extensão de Script personalizado para o Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="2d8df-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="2d8df-112">Local do script</span><span class="sxs-lookup"><span data-stu-id="2d8df-112">Script Location</span></span>

<span data-ttu-id="2d8df-113">script de saudação precisa toobe armazenado no armazenamento de BLOBs do Azure, ou qualquer outro local acessível por meio de uma URL válida.</span><span class="sxs-lookup"><span data-stu-id="2d8df-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="2d8df-114">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="2d8df-114">Internet Connectivity</span></span>

<span data-ttu-id="2d8df-115">Olá extensão para janelas de Script personalizado requer que a máquina virtual Olá destino toohello conectado à internet.</span><span class="sxs-lookup"><span data-stu-id="2d8df-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="2d8df-116">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="2d8df-116">Extension schema</span></span>

<span data-ttu-id="2d8df-117">Olá JSON a seguir mostra esquema Olá Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="2d8df-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="2d8df-118">extensão de saudação requer um local de script (armazenamento do Azure ou em outro local com URL válida) e um comando tooexecute.</span><span class="sxs-lookup"><span data-stu-id="2d8df-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="2d8df-119">Se usar o armazenamento do Azure como fonte do script hello, uma chave de nome e uma conta de conta do armazenamento do Azure é necessária.</span><span class="sxs-lookup"><span data-stu-id="2d8df-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="2d8df-120">Esses itens devem ser tratados como dados confidenciais e especificados na configuração de configuração protegida Olá extensões.</span><span class="sxs-lookup"><span data-stu-id="2d8df-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="2d8df-121">Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="2d8df-122">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="2d8df-122">Property values</span></span>

| <span data-ttu-id="2d8df-123">Nome</span><span class="sxs-lookup"><span data-stu-id="2d8df-123">Name</span></span> | <span data-ttu-id="2d8df-124">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="2d8df-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="2d8df-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2d8df-125">apiVersion</span></span> | <span data-ttu-id="2d8df-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="2d8df-126">2015-06-15</span></span> |
| <span data-ttu-id="2d8df-127">publicador</span><span class="sxs-lookup"><span data-stu-id="2d8df-127">publisher</span></span> | <span data-ttu-id="2d8df-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="2d8df-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="2d8df-129">type</span><span class="sxs-lookup"><span data-stu-id="2d8df-129">type</span></span> | <span data-ttu-id="2d8df-130">extensions</span><span class="sxs-lookup"><span data-stu-id="2d8df-130">extensions</span></span> |
| <span data-ttu-id="2d8df-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="2d8df-131">typeHandlerVersion</span></span> | <span data-ttu-id="2d8df-132">1.9</span><span class="sxs-lookup"><span data-stu-id="2d8df-132">1.9</span></span> |
| <span data-ttu-id="2d8df-133">fileUris (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="2d8df-133">fileUris (e.g)</span></span> | <span data-ttu-id="2d8df-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="2d8df-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="2d8df-135">commandToExecute (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="2d8df-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="2d8df-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="2d8df-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="2d8df-137">storageAccountName (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="2d8df-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="2d8df-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="2d8df-138">examplestorageacct</span></span> |
| <span data-ttu-id="2d8df-139">storageAccountKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="2d8df-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="2d8df-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="2d8df-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="2d8df-141">**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2d8df-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="2d8df-142">Use nomes de saudação como mostrado acima tooavoid problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="2d8df-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="2d8df-143">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="2d8df-143">Template deployment</span></span>

<span data-ttu-id="2d8df-144">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d8df-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="2d8df-145">esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão de Script personalizado durante uma implantação de modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8df-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="2d8df-146">Um modelo de exemplo que inclui Olá extensão de Script personalizado podem ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="2d8df-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="2d8df-147">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d8df-147">PowerShell deployment</span></span>

<span data-ttu-id="2d8df-148">Olá `Set-AzureRmVMCustomScriptExtension` comando pode ser usado tooadd Olá Script personalizado extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="2d8df-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="2d8df-149">Para saber mais, confira [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="2d8df-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="2d8df-150">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="2d8df-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="2d8df-151">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2d8df-151">Troubleshoot</span></span>

<span data-ttu-id="2d8df-152">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="2d8df-153">estado da implantação toosee Olá de extensões para uma determinada VM, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2d8df-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="2d8df-154">Execução de extensão de saída é conectado toofiles encontrado em Olá após diretório na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="2d8df-155">Olá especificado arquivos são baixados em Olá diretório a seguir na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="2d8df-156">onde `<n>` é um inteiro decimal que possa alterar entre as execuções da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d8df-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="2d8df-157">Olá `1.*` valor faz a correspondência atual real, Olá `typeHandlerVersion` valor da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d8df-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="2d8df-158">Por exemplo, o diretório real Olá pode ser `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="2d8df-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="2d8df-159">Ao executar Olá `commandToExecute` de comando, extensão Olá ter definirá neste diretório (por exemplo, `...\Downloads\2`) como o diretório de trabalho atual hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="2d8df-160">Esse uso de saudação habilita dos arquivos de saudação toolocate caminhos relativos baixados via Olá `fileURIs` propriedade.</span><span class="sxs-lookup"><span data-stu-id="2d8df-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="2d8df-161">Consulte Olá a tabela abaixo para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="2d8df-161">See hello table below for examples.</span></span>

<span data-ttu-id="2d8df-162">Como o caminho de download absoluto Olá pode variar ao longo do tempo, é melhor tooopt para caminhos de arquivo/script relativo da saudação `commandToExecute` cadeia de caracteres, sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="2d8df-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="2d8df-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2d8df-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="2d8df-164">Informações de caminho após o primeiro segmento de URI Olá é retido para arquivos baixados via Olá `fileUris` lista de propriedades.</span><span class="sxs-lookup"><span data-stu-id="2d8df-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="2d8df-165">Conforme mostrado na tabela de saudação abaixo, os arquivos baixados são mapeados em estrutura de saudação do download subdiretórios tooreflect de saudação `fileUris` valores.</span><span class="sxs-lookup"><span data-stu-id="2d8df-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="2d8df-166">Exemplos de Arquivos Baixados</span><span class="sxs-lookup"><span data-stu-id="2d8df-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="2d8df-167">URI no fileUris</span><span class="sxs-lookup"><span data-stu-id="2d8df-167">URI in fileUris</span></span> | <span data-ttu-id="2d8df-168">Localização baixada relativa</span><span class="sxs-lookup"><span data-stu-id="2d8df-168">Relative downloaded location</span></span> | <span data-ttu-id="2d8df-169">Localização baixada absoluta *</span><span class="sxs-lookup"><span data-stu-id="2d8df-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="2d8df-170">\*Como acima, os caminhos de diretório absolutos Olá serão alterado em tempo de vida de saudação do hello VM, mas não dentro de uma única execução da extensão de CustomScript hello.</span><span class="sxs-lookup"><span data-stu-id="2d8df-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="2d8df-171">Suporte</span><span class="sxs-lookup"><span data-stu-id="2d8df-171">Support</span></span>

<span data-ttu-id="2d8df-172">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="2d8df-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="2d8df-173">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8df-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="2d8df-174">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="2d8df-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="2d8df-175">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="2d8df-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
