---
title: "aaaOMS extensão de máquina virtual do Azure para Windows | Microsoft Docs"
description: "Implante o agente do OMS Olá na máquina virtual do Windows usando uma extensão de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>Extensão da máquina virtual do OMS para Windows

O OMS (Operations Management Suite) fornece recursos de monitoramento, alertas e correção de alertas nos ativos locais e da nuvem. Olá extensão de máquina virtual do agente do OMS para Windows é publicada e suporte da Microsoft. extensão de saudação instala o agente do OMS Olá em máquinas virtuais do Azure e registra as máquinas virtuais em um espaço de trabalho existente do OMS. Saudação de detalhes neste documento suporte a plataformas, configurações e opções de implantação para Olá extensão de máquina virtual do OMS para Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional
Olá extensão do agente do OMS para Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.

### <a name="internet-connectivity"></a>Conectividade com a Internet
Olá extensão do agente do OMS para Windows requer que a máquina virtual Olá destino toohello conectado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá JSON a seguir mostra esquema Olá Olá extensão do agente do OMS. extensão de saudação requer a chave de Id e o espaço de trabalho de espaço de trabalho de saudação do espaço de trabalho do OMS Olá destino, eles podem ser encontrados no portal do OMS hello. Porque a chave do espaço de trabalho Olá deve ser tratado como dados confidenciais, devem ser armazenado em uma configuração protegida. Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello. Observe que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Valores de propriedade

| Nome | Valor/Exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publicador | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (por exemplo) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (por exemplo) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |

## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do OMS durante uma implantação de modelo do Gerenciador de recursos do Azure. Um modelo de exemplo que inclui a extensão de VM de agente do OMS Olá pode ser encontrado no hello [Galeria de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Olá JSON para uma extensão de máquina virtual pode ser aninhado dentro do recurso de máquina virtual de saudação ou colocado na raiz de saudação ou de nível superior de um modelo JSON do Gerenciador de recursos. posicionamento de saudação do hello JSON afeta o valor de saudação do nome do recurso hello e tipo. Para obter mais informações, consulte [Definir o nome e o tipo de recursos filho](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Olá exemplo a seguir supõe extensão do OMS hello está aninhado em Olá recurso da máquina virtual. Ao aninhar o recurso de extensão hello, Olá JSON é colocado no hello `"resources": []` objeto da máquina virtual de saudação.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Ao inserir extensão Olá JSON na raiz de saudação do modelo Olá, nome do recurso de saudação inclui uma máquina virtual do referência toohello pai e tipo hello reflete configuração aninhada Olá. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>Implantação do PowerShell

Olá `Set-AzureRmVMExtension` comando pode ser usado toodeploy Olá agente do OMS máquina virtual extensão tooan máquina virtual existente. Antes de executar o comando hello, configurações públicas e privadas de saudação necessário toobe armazenado em uma tabela de hash do PowerShell. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Solução de problemas e suporte

### <a name="troubleshoot"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello. estado da implantação Olá toosee de extensões para uma determinada VM, Olá execução usando o comando a seguir Olá módulo PowerShell do Azure.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
