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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Implantação de aplicativos com modelos do Azure Resource Manager para VMs Windows

Depois que todos os requisitos de infra-estrutura do Azure foram identificados e convertidos em um modelo de implantação, implantação de aplicativo real Olá precisa toobe resolvido. Implantação de aplicativo aqui se refere a tooinstalling Olá real binários em recursos do Azure. Para exemplo de repositório de música hello, .net Core e o IIS precisa toobe instalado e configurado em cada máquina virtual. Olá binários necessário toobe instalado na máquina virtual de saudação do repositório de música e Olá banco de dados do repositório de música criado previamente.

Este documento detalha como extensões de máquina Virtual podem automatizar máquinas de virtuais de tooAzure de implantação e configuração de aplicativo. Todas as dependências e configurações exclusivas são realçadas. Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello. modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Script de configuração
Extensões de máquina virtual são programas especializados que são executadas em automação de configuração de tooprovide de máquinas virtuais. As extensões estão disponíveis para várias finalidades específicas, como antivírus, configuração de registro e configuração do Docker. Olá extensão de Script personalizado pode ser usado toorun os scripts em uma máquina virtual. Com exemplo de repositório de música hello, é a extensão de script personalizado de toohello tooconfigure máquinas de virtuais do Windows de saudação e instalar o aplicativo de repositório de música hello.

Antes de Detalhar como extensões de máquina virtual são declaradas em um modelo do Azure Resource Manager, examine o script hello que é executado. Esse script configura Olá Windows máquina virtual toohost Olá aplicativo de repositório de música. Quando executado, o script de Olá instala o software necessário todos os, instalar o aplicativo de repositório de música de saudação do controle de origem e preparar o banco de dados de saudação. 

> Este exemplo é para fins de demonstração.

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

## <a name="vm-script-extension"></a>Extensão de script da VM
Extensões de VM pode ser executadas em uma máquina virtual no momento da compilação, incluindo o recurso de extensão Olá no modelo do Azure Resource Manager hello. extensão de saudação pode ser adicionado com o Assistente do Visual Studio adicionar recurso hello, ou inserindo um JSON válido no modelo de saudação. Olá recursos de extensão do Script está aninhado em Olá recurso de máquina Virtual. Isso pode ser visto no exemplo a seguir de saudação.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [extensão do Script VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Observe Olá abaixo JSON que Olá script é armazenado no GitHub. Esse script também pode ser armazenado no Armazenamento de Blobs do Azure. Além disso, os modelos de Gerenciador de recursos do Azure permitem Olá script execução cadeia de caracteres toobe construído de forma que os valores de parâmetros de modelo podem ser usados como parâmetros para a execução do script. Nesse caso os dados são fornecidos ao implantar modelos Olá, e esses valores, em seguida, podem ser usados ao executar o script hello.

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

Conforme mencionado acima, também é possível toostore scripts personalizados no armazenamento de BLOBs do Azure. Há duas opções para armazenar recursos de script hello no armazenamento de blob; tornar Olá público de contêiner/script e siga Olá mesma abordagem acima, ou também podem ser mantido no armazenamento de blob privada que exige que você tooprovide Olá storageAccountName e storageAccountKey toohello CustomScriptExtension definição de recurso.

No exemplo hello abaixo é tenha sido uma etapa adicional. Embora seja possível tooprovide nome de conta de armazenamento de saudação e a chave como um parâmetro ou variável durante a implantação, os modelos de Gerenciador de recursos fornecem Olá `listKeys` função que pode obter a conta de armazenamento Olá chave programaticamente e inseri-lo em toohello modelo para você no momento da implantação.

No exemplo hello definição de recurso CustomScriptExtension abaixo, nosso script personalizado já foi carregado tooan conta de armazenamento do Azure chamado `mystorageaccount9999` que existe em outro grupo de recursos chamado `mysa999rgname`. Quando é implantar um modelo que contém esse recurso, Olá `listKeys` função programaticamente obtém a chave de conta de armazenamento Olá Olá conta de armazenamento `mystorageaccount9999` em Olá grupo de recursos `mysa999rgname` e o insere no modelo toohello para nós.

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

Olá principal vantagem dessa abordagem é que ele não requer que você toochange seu modelo ou parâmetros de implantação no evento de saudação do hello alterar chave de conta do armazenamento.

Para obter mais informações sobre como usar a extensão do script personalizado hello, consulte [extensões de script personalizado com modelos do Gerenciador de recursos](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Próxima etapa
<hr>

[Explorar mais modelos do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

