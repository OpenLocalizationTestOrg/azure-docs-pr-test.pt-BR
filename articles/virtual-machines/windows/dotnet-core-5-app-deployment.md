---
title: "Implantação de aplicativo com extensões de máquina Virtual de aaaAutomating | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="16baa-103">Implantação de aplicativos com modelos do Azure Resource Manager para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="16baa-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="16baa-104">Depois que todos os requisitos de infra-estrutura do Azure foram identificados e convertidos em um modelo de implantação, implantação de aplicativo real Olá precisa toobe resolvido.</span><span class="sxs-lookup"><span data-stu-id="16baa-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="16baa-105">Implantação de aplicativo aqui se refere a tooinstalling Olá real binários em recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="16baa-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="16baa-106">Para exemplo de repositório de música hello, .net Core e o IIS precisa toobe instalado e configurado em cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="16baa-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="16baa-107">Olá binários necessário toobe instalado na máquina virtual de saudação do repositório de música e Olá banco de dados do repositório de música criado previamente.</span><span class="sxs-lookup"><span data-stu-id="16baa-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="16baa-108">Este documento detalha como extensões de máquina Virtual podem automatizar máquinas de virtuais de tooAzure de implantação e configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16baa-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="16baa-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="16baa-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="16baa-110">Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="16baa-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="16baa-111">modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="16baa-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="16baa-112">Script de configuração</span><span class="sxs-lookup"><span data-stu-id="16baa-112">Configuration script</span></span>
<span data-ttu-id="16baa-113">Extensões de máquina virtual são programas especializados que são executadas em automação de configuração de tooprovide de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="16baa-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="16baa-114">As extensões estão disponíveis para várias finalidades específicas, como antivírus, configuração de registro e configuração do Docker.</span><span class="sxs-lookup"><span data-stu-id="16baa-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="16baa-115">Olá extensão de Script personalizado pode ser usado toorun os scripts em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="16baa-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="16baa-116">Com exemplo de repositório de música hello, é a extensão de script personalizado de toohello tooconfigure máquinas de virtuais do Windows de saudação e instalar o aplicativo de repositório de música hello.</span><span class="sxs-lookup"><span data-stu-id="16baa-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="16baa-117">Antes de Detalhar como extensões de máquina virtual são declaradas em um modelo do Azure Resource Manager, examine o script hello que é executado.</span><span class="sxs-lookup"><span data-stu-id="16baa-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="16baa-118">Esse script configura Olá Windows máquina virtual toohost Olá aplicativo de repositório de música.</span><span class="sxs-lookup"><span data-stu-id="16baa-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="16baa-119">Quando executado, o script de Olá instala o software necessário todos os, instalar o aplicativo de repositório de música de saudação do controle de origem e preparar o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="16baa-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="16baa-120">Este exemplo é para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="16baa-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="16baa-121">Extensão de script da VM</span><span class="sxs-lookup"><span data-stu-id="16baa-121">VM Script Extension</span></span>
<span data-ttu-id="16baa-122">Extensões de VM pode ser executadas em uma máquina virtual no momento da compilação, incluindo o recurso de extensão Olá no modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="16baa-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="16baa-123">extensão de saudação pode ser adicionado com o Assistente do Visual Studio adicionar recurso hello, ou inserindo um JSON válido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="16baa-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="16baa-124">Olá recursos de extensão do Script está aninhado em Olá recurso de máquina Virtual. Isso pode ser visto no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="16baa-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="16baa-125">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [extensão do Script VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="16baa-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="16baa-126">Observe Olá abaixo JSON que Olá script é armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="16baa-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="16baa-127">Esse script também pode ser armazenado no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="16baa-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="16baa-128">Além disso, os modelos de Gerenciador de recursos do Azure permitem Olá script execução cadeia de caracteres toobe construído de forma que os valores de parâmetros de modelo podem ser usados como parâmetros para a execução do script.</span><span class="sxs-lookup"><span data-stu-id="16baa-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="16baa-129">Nesse caso os dados são fornecidos ao implantar modelos Olá, e esses valores, em seguida, podem ser usados ao executar o script hello.</span><span class="sxs-lookup"><span data-stu-id="16baa-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="16baa-130">Conforme mencionado acima, também é possível toostore scripts personalizados no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="16baa-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="16baa-131">Há duas opções para armazenar recursos de script hello no armazenamento de blob; tornar Olá público de contêiner/script e siga Olá mesma abordagem acima, ou também podem ser mantido no armazenamento de blob privada que exige que você tooprovide Olá storageAccountName e storageAccountKey toohello CustomScriptExtension definição de recurso.</span><span class="sxs-lookup"><span data-stu-id="16baa-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="16baa-132">No exemplo hello abaixo é tenha sido uma etapa adicional.</span><span class="sxs-lookup"><span data-stu-id="16baa-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="16baa-133">Embora seja possível tooprovide nome de conta de armazenamento de saudação e a chave como um parâmetro ou variável durante a implantação, os modelos de Gerenciador de recursos fornecem Olá `listKeys` função que pode obter a conta de armazenamento Olá chave programaticamente e inseri-lo em toohello modelo para você no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="16baa-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="16baa-134">No exemplo hello definição de recurso CustomScriptExtension abaixo, nosso script personalizado já foi carregado tooan conta de armazenamento do Azure chamado `mystorageaccount9999` que existe em outro grupo de recursos chamado `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="16baa-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="16baa-135">Quando é implantar um modelo que contém esse recurso, Olá `listKeys` função programaticamente obtém a chave de conta de armazenamento Olá Olá conta de armazenamento `mystorageaccount9999` em Olá grupo de recursos `mysa999rgname` e o insere no modelo toohello para nós.</span><span class="sxs-lookup"><span data-stu-id="16baa-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="16baa-136">Olá principal vantagem dessa abordagem é que ele não requer que você toochange seu modelo ou parâmetros de implantação no evento de saudação do hello alterar chave de conta do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="16baa-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="16baa-137">Para obter mais informações sobre como usar a extensão do script personalizado hello, consulte [extensões de script personalizado com modelos do Gerenciador de recursos](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16baa-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="16baa-138">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="16baa-138">Next Step</span></span>
<hr>

[<span data-ttu-id="16baa-139">Explorar mais modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="16baa-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

