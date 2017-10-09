---
title: "aaaOMS extensão de máquina virtual do Azure para Linux | Microsoft Docs"
description: "Implante o agente do OMS Olá na máquina virtual do Linux usando uma extensão de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Extensão da máquina virtual do OMS para Linux

## <a name="overview"></a>Visão geral

O OMS (Operations Management Suite) fornece recursos de monitoramento, alertas e correção de alertas nos ativos locais e da nuvem. Olá extensão de máquina virtual do agente do OMS para Linux é publicada e suporte da Microsoft. extensão de saudação instala o agente do OMS Olá em máquinas virtuais do Azure e registra as máquinas virtuais em um espaço de trabalho existente do OMS. Saudação de detalhes neste documento suporte a plataformas, configurações e opções de implantação para Olá extensão de máquina virtual do OMS para Linux.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operacional

Olá extensão do agente do OMS pode ser executado em relação a essas distribuições do Linux.

| Distribuição | Versão |
|---|---|
| CentOS Linux | 5, 6 e 7 |
| Oracle Linux | 5, 6 e 7 |
| Red Hat Enterprise Linux Server | 5, 6 e 7 |
| Debian GNU/Linux | 6, 7 e 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 e 12 |

### <a name="internet-connectivity"></a>Conectividade com a Internet

Olá extensão do agente do OMS para Linux requer que a máquina virtual Olá destino é toohello conectado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá JSON a seguir mostra esquema Olá Olá extensão do agente do OMS. extensão de saudação requer a chave de ID e o espaço de trabalho de espaço de trabalho de saudação do espaço de trabalho OMS do destino Olá; Esses valores podem ser encontrados no portal do OMS hello. Porque a chave do espaço de trabalho Olá deve ser tratado como dados confidenciais, devem ser armazenado em uma configuração protegida. Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello. Observe que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor/Exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publicador | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (por exemplo) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (por exemplo) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>Implantação de modelo

Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager. Modelos são ideais ao implantar um ou mais máquinas virtuais que exigem configuração de implantação de post como tooOMS de integração. Um Gerenciador de recursos de modelo que inclui a extensão de VM de agente do OMS Olá pode ser encontrado no hello [Galeria de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

configuração de JSON Olá para uma extensão de máquina virtual pode ser aninhada dentro do recurso de máquina virtual de saudação ou colocada na raiz de saudação ou de nível superior de um modelo JSON do Gerenciador de recursos. posicionamento de saudação da configuração de JSON de saudação afeta o valor de saudação do nome do recurso hello e tipo. Para obter mais informações, consulte [Definir o nome e o tipo de recursos filho](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Olá exemplo a seguir supõe extensão do OMS hello está aninhado em Olá recurso da máquina virtual. Ao aninhar o recurso de extensão hello, Olá JSON é colocado no hello `"resources": []` objeto da máquina virtual de saudação.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Ao inserir extensão Olá JSON na raiz de saudação do modelo Olá, nome do recurso de saudação inclui uma máquina virtual do referência toohello pai e tipo hello reflete configuração aninhada Olá.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Implantação da CLI do Azure

Olá CLI do Azure pode ser usado toodeploy Olá VM de agente do OMS extensão tooan máquina virtual existente. Substitua a chave OMS do hello e ID do OMS com os de seu espaço de trabalho do OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Solução de problemas e suporte

### <a name="troubleshoot"></a>Solucionar problemas

Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando Olá CLI do Azure. estado da implantação Olá toosee de extensões para uma determinada VM, execute hello usando o comando a seguir Olá CLI do Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Execução de extensão é conectado toohello após o arquivo de saída:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Códigos de erro e seus significados

| Código do Erro | Significado | Ação possível |
| :---: | --- | --- |
| 10 | VM já está conectado tooan espaço de trabalho do OMS | tooconnect Olá VM toohello espaço de trabalho especificado no esquema de extensão Olá, defina stopOnMultipleConnections toofalse nas configurações de públicas ou remova esta propriedade. Essa VM é cobrada uma vez para cada espaço de trabalho ao qual está conectada. |
| 11 | Extensão de toohello de configuração inválido fornecida | Siga Olá anterior exemplos tooset todos os valores de propriedade necessários à implantação. |
| 12 | Gerenciador de pacote dpkg Hello está bloqueado | Verifique se o todas as operações de atualização de dpkg na máquina de saudação terminar e tente novamente. |
| 20 | Habilitar chamado prematuramente | [Saudação de atualização do Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versão mais recente. |
| 51 | Não há suporte para essa extensão no sistema de operação de saudação da VM | |
| 55 | Não é possível conectar o serviço do Microsoft Operations Management Suite toohello | Verifique se Olá sistema tem acesso à Internet ou que um proxy HTTP válido foi fornecido. Além disso, verifique a exatidão de saudação da ID do espaço de trabalho de saudação. |

Informações de solução de problemas adicionais podem ser encontradas em Olá [guia de solução de problemas de agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Suporte

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
