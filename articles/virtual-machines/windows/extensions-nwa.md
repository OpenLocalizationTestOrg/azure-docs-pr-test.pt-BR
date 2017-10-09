---
title: "aaaAzure extensão de máquina virtual do agente do Inspetor de rede para Windows | Microsoft Docs"
description: "Implante Olá agente do Inspetor de rede na máquina virtual do Windows usando uma extensão de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Extensão da máquina virtual do Agente do Observador de Rede para Windows

## <a name="overview"></a>Visão geral

[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure. Olá extensão do agente do Inspetor de rede de máquina virtual é um requisito para alguns dos recursos de rede Inspetor Olá em máquinas virtuais do Azure. Isso inclui capturar o tráfego de rede sob demanda e outras funcionalidades avançadas.

Saudação de detalhes neste documento suporte a plataformas e opções de implantação para Olá extensão do agente do Inspetor de rede de máquina virtual para Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional

Olá extensão do agente do Inspetor de rede para Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera. Observe que Olá Nano Server não é suportado no momento.

### <a name="internet-connectivity"></a>Conectividade com a Internet

Alguns Olá funcionalidade de agente do Inspetor de rede requer que a máquina virtual Olá destino ser toohello conectado à Internet. Sem conexões de saída Olá capacidade tooestablish alguns dos recursos de agente do Inspetor de rede Olá podem mau funcionamento ou se tornar indisponível. Para obter mais detalhes, consulte Olá [documentação do observador de rede](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Esquema de extensão

Olá JSON a seguir mostra esquema Olá Olá extensão do agente do Inspetor de rede. extensão de saudação não requer nem dá suporte a todas as configurações fornecidas pelo usuário no momento e se baseia em sua configuração padrão.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor/Exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publicador | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do Inspetor de rede durante uma implantação de modelo do Gerenciador de recursos do Azure.

## <a name="powershell-deployment"></a>Implantação do PowerShell

Olá `Set-AzureRmVMExtension` comando pode ser usado toodeploy Olá agente do Inspetor de rede virtual machine extensão tooan máquina virtual existente.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Solução de problemas e suporte

### <a name="troubleshooting"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello. estado da implantação Olá toosee de extensões para uma determinada VM, Olá execução usando o comando a seguir Olá módulo PowerShell do Azure.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode consulte a documentação do guia do usuário de Inspetor de rede toohello ou entre em contato com o hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
