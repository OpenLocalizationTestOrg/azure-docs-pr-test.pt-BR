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
# <a name="custom-script-extension-for-windows"></a>Extensão de script personalizado para o Windows

Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure. Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento. Scripts podem ser baixados do armazenamento do Azure ou GitHub ou fornecidos toohello portal do Azure em tempo de execução de extensão. Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.

Este documento detalha como toouse Olá extensão de Script personalizado usando Olá módulo PowerShell do Azure, modelos de Gerenciador de recursos do Azure e detalhes de solução de problemas etapas em sistemas Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional

Olá extensão de Script personalizado para o Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.

### <a name="script-location"></a>Local do script

script de saudação precisa toobe armazenado no armazenamento de BLOBs do Azure, ou qualquer outro local acessível por meio de uma URL válida.

### <a name="internet-connectivity"></a>Conectividade com a Internet

Olá extensão para janelas de Script personalizado requer que a máquina virtual Olá destino toohello conectado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá JSON a seguir mostra esquema Olá Olá extensão de Script personalizado. extensão de saudação requer um local de script (armazenamento do Azure ou em outro local com URL válida) e um comando tooexecute. Se usar o armazenamento do Azure como fonte do script hello, uma chave de nome e uma conta de conta do armazenamento do Azure é necessária. Esses itens devem ser tratados como dados confidenciais e especificados na configuração de configuração protegida Olá extensões. Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.

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

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor/Exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publicador | Microsoft.Compute |
| type | extensions |
| typeHandlerVersion | 1.9 |
| fileUris (por exemplo) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (por exemplo) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (por exemplo) | examplestorageacct |
| storageAccountKey (por exemplo) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas. Use nomes de saudação como mostrado acima tooavoid problemas de implantação.

## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão de Script personalizado durante uma implantação de modelo do Gerenciador de recursos do Azure. Um modelo de exemplo que inclui Olá extensão de Script personalizado podem ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Implantação do PowerShell

Olá `Set-AzureRmVMCustomScriptExtension` comando pode ser usado tooadd Olá Script personalizado extensão tooan máquina virtual existente. Para saber mais, confira [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Solução de problemas e suporte

### <a name="troubleshoot"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello. estado da implantação toosee Olá de extensões para uma determinada VM, execute Olá comando a seguir.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Execução de extensão de saída é conectado toofiles encontrado em Olá após diretório na máquina de virtual de destino hello.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Olá especificado arquivos são baixados em Olá diretório a seguir na máquina de virtual de destino hello.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
onde `<n>` é um inteiro decimal que possa alterar entre as execuções da extensão de saudação.  Olá `1.*` valor faz a correspondência atual real, Olá `typeHandlerVersion` valor da extensão de saudação.  Por exemplo, o diretório real Olá pode ser `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Ao executar Olá `commandToExecute` de comando, extensão Olá ter definirá neste diretório (por exemplo, `...\Downloads\2`) como o diretório de trabalho atual hello. Esse uso de saudação habilita dos arquivos de saudação toolocate caminhos relativos baixados via Olá `fileURIs` propriedade. Consulte Olá a tabela abaixo para obter exemplos.

Como o caminho de download absoluto Olá pode variar ao longo do tempo, é melhor tooopt para caminhos de arquivo/script relativo da saudação `commandToExecute` cadeia de caracteres, sempre que possível. Por exemplo:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Informações de caminho após o primeiro segmento de URI Olá é retido para arquivos baixados via Olá `fileUris` lista de propriedades.  Conforme mostrado na tabela de saudação abaixo, os arquivos baixados são mapeados em estrutura de saudação do download subdiretórios tooreflect de saudação `fileUris` valores.  

#### <a name="examples-of-downloaded-files"></a>Exemplos de Arquivos Baixados

| URI no fileUris | Localização baixada relativa | Localização baixada absoluta * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Como acima, os caminhos de diretório absolutos Olá serão alterado em tempo de vida de saudação do hello VM, mas não dentro de uma única execução da extensão de CustomScript hello.

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha] (https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
