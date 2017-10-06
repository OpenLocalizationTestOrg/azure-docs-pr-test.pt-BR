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
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Personalizado extensão para janelas de Script usando o modelo de implantação clássico Olá

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure. Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento. Scripts podem ser baixados do armazenamento do Azure ou GitHub ou fornecidos toohello portal do Azure em tempo de execução de extensão. Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.

Este documento detalha como toouse Olá extensão de Script personalizado usando Olá módulo PowerShell do Azure, modelos de Gerenciador de recursos do Azure e detalhes de solução de problemas etapas em sistemas Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional

Olá extensão de Script personalizado para o Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.

### <a name="script-location"></a>Local do script

script de saudação precisa toobe armazenado no armazenamento do Azure, ou qualquer outro local acessível por meio de uma URL válida.

### <a name="internet-connectivity"></a>Conectividade com a Internet

Olá extensão para janelas de Script personalizado requer que a máquina virtual Olá destino toohello conectado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá JSON a seguir mostra esquema Olá Olá extensão de Script personalizado. extensão de saudação requer um local de script (armazenamento do Azure ou em outro local com URL válida) e um comando tooexecute. Se usar o armazenamento do Azure como fonte do script hello, uma chave de nome e uma conta de conta do armazenamento do Azure é necessária. Esses itens devem ser tratados como dados confidenciais e especificados na configuração de configuração protegida Olá extensões. Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.

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

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor/Exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publicador | Microsoft.Compute |
| extensão | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (por exemplo) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (por exemplo) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão de Script personalizado durante uma implantação de modelo do Gerenciador de recursos do Azure. Um modelo de exemplo que inclui Olá extensão de Script personalizado podem ser encontrada aqui, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Implantação do PowerShell

Olá `Set-AzureVMCustomScriptExtension` comando pode ser usado tooadd Olá Script personalizado extensão tooan máquina virtual existente. Para saber mais, confira [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Solução de problemas e suporte

### <a name="troubleshoot"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello. estado da implantação toosee Olá de extensões para uma determinada VM, execute Olá comando a seguir.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Execução de extensão de saída nos toofiles conectado encontrado no hello diretório a seguir na máquina de virtual de destino hello.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

script Hello propriamente dito é baixado em Olá diretório a seguir na máquina de virtual de destino de saudação.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
