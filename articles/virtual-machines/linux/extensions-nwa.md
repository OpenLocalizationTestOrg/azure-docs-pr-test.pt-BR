---
title: "aaaAzure extensão de máquina virtual do agente do Inspetor de rede para Linux | Microsoft Docs"
description: "Implante Olá agente do Inspetor de rede na máquina virtual do Linux usando uma extensão de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux

## <a name="overview"></a>Visão geral

[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure. Olá extensão do agente do Inspetor de rede de máquina virtual é um requisito para alguns dos recursos de rede Inspetor Olá em máquinas virtuais do Azure. Isso inclui capturar o tráfego de rede sob demanda e outras funcionalidades avançadas.

Saudação de detalhes neste documento suporte a plataformas e opções de implantação para Olá extensão do agente do Inspetor de rede de máquina virtual para Linux.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional

Olá extensão do agente do Inspetor de rede pode ser executada em relação a essas distribuições do Linux:

| Distribuição | Versão |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS e 12.04 LTS |
| Debian | 7 e 8 |
| RedHat | 6.x e 7.x |
| Oracle Linux | 7x |
| Suse | 11 e 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Observe que o CoreOS não tem suporte neste momento.

### <a name="internet-connectivity"></a>Conectividade com a Internet

Alguns Olá funcionalidade de agente do Inspetor de rede requer que a máquina virtual Olá destino ser toohello conectado à Internet. Sem conexões de saída Olá capacidade tooestablish alguns dos recursos de agente do Inspetor de rede Olá podem mau funcionamento ou se tornar indisponível. Para obter mais detalhes, consulte Olá [documentação do observador de rede](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do Inspetor de rede durante uma implantação de modelo do Gerenciador de recursos do Azure.

## <a name="azure-cli-deployment"></a>Implantação da CLI do Azure

Olá CLI do Azure pode ser usado toodeploy Olá rede Inspetor agente VM extensão tooan máquina virtual existente.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Solução de problemas e suporte

### <a name="troubleshooting"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando Olá CLI do Azure. estado da implantação Olá toosee de extensões para uma determinada VM, execute hello usando o comando a seguir Olá CLI do Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode consulte a documentação do observador de rede toohello ou entre em contato com o hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
