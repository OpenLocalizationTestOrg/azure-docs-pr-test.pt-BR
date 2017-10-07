---
title: "Grupos de recursos do Azure que contêm extensões de VM do aaaExporting | Microsoft Docs"
description: "Exporte modelos do Resource Manager que incluem as extensões da máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Exportar Grupos de Recursos que contêm extensões de VM

Os Grupos de Recursos do Azure podem ser exportados para um novo modelo do Resource Manager que, depois, pode ser reimplantado. Olá processo de exportação interpreta os recursos existentes e cria um modelo do Gerenciador de recursos que quando implantado resulta em um grupo de recursos semelhantes. Ao usar a opção de exportação de grupo de recursos de saudação em relação a um grupo de recursos que contém as extensões de máquina Virtual, vários toobe necessidade de itens considerado como compatibilidade de extensão e protegido configurações.

Este documento detalha como funciona o processo de exportação do grupo de recursos de saudação sobre extensões de máquina virtual, incluindo uma lista de extensões de suporte, e detalhes sobre o tratamento seguro dados.

## <a name="supported-virtual-machine-extensions"></a>Extensões da máquina virtual com suporte

Há muitas extensões da máquina virtual disponíveis. Nem todas as extensões podem ser exportadas para um modelo do Gerenciador de recursos usando o recurso de "Script de automação" hello. Não há suporte para uma extensão de máquina virtual, precisa toobe manualmente colocado de volta em modelo exportado hello.

Olá extensões a seguir podem ser exportadas com o recurso de script de automação de saudação.

| Extensão ||||
|---|---|---|---|
| Acronis Backup | Datadog Windows Agent | OS Patching For Linux | VM Snapshot Linux
| Acronis Backup Linux | Extensão do Docker | Puppet Agent |
| Bg Info | DSC Extension | Site 24x7 Apm Insight |
| BMC CTM Agent Linux | Dynatrace Linux | Site 24x7 Linux Server |
| BMC CTM Agent Windows | Dynatrace Windows | Site 24x7 Windows Server |
| Chef Client | HPE Security Application Defender | Trend Micro DSA |
| Custom Script | IaaS Antimalware | Trend Micro DSA Linux |
| Extensão de script personalizado | Diagnóstico do IaaS | Acesso de VM para Linux |
| Script Personalizado para Linux | Linux Chef Client | Acesso de VM para Linux |
| Datadog Linux Agent | Diagnóstico do Linux | VM Snapshot |

## <a name="export-hello-resource-group"></a>Saudação de exportação de grupo de recursos

tooexport um grupo de recursos em um modelo reutilizável, Olá concluir as etapas a seguir:

1. Entrar toohello portal do Azure
2. No hello Menu Hub, clique em grupos de recursos
3. Selecione o grupo de recursos de destino de saudação da lista de saudação
4. Na folha de grupo de recursos de saudação, clique em Script de automação

![Exportação de modelo](./media/extensions-export-templates/template-export.png)

Olá script do Azure Resource Manager automações produz um modelo do Gerenciador de recursos, um arquivo de parâmetros e vários scripts de implantação de exemplo, como o PowerShell e a CLI do Azure. Neste ponto, modelo exportado Olá pode ser obtido com o botão de download hello, adicionado como uma biblioteca de modelos de toohello modelo novo ou reimplantado com hello botão implantar.

## <a name="configure-protected-settings"></a>Definir as configurações protegidas

Muitas extensões da máquina virtual do Azure incluem uma definição de configurações protegidas que criptografa dados confidenciais, como credenciais e cadeias de configuração. Configurações protegidas não são exportadas com o script de automação de saudação. Se precisam de configurações necessárias e protegidas toobe reinserida hello exportada modelado.

### <a name="step-1---remove-template-parameter"></a>Etapa 1: Remover o parâmetro de modelo

Quando saudação do que grupo de recursos é exportado, um parâmetro de modelo único é criada tooprovide toohello um valor exportado configurações protegidas. Esse parâmetro pode ser removido. parâmetro de saudação tooremove, examine a lista de parâmetros de saudação e excluir parâmetro hello que parece semelhante exemplo JSON toothis.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Etapa 2: Obter as propriedades das configurações protegidas

Como cada configuração protegido tem um conjunto de propriedades obrigatórias, uma lista dessas propriedades necessário toobe coletada. Cada parâmetro de configuração de configurações protegidas de saudação pode ser encontrado no hello [esquema do Gerenciador de recursos do Azure no GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Esse esquema inclui apenas conjuntos de parâmetros Olá para extensões de saudação listadas na seção de visão geral de saudação deste documento. 

De dentro do repositório de esquema Olá, procurar extensão Olá desejado, para este exemplo `IaaSDiagnostics`. Uma vez Olá extensões `protectedSettings` objeto foi localizado, tome nota de cada parâmetro. No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá requer que os parâmetros são `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Etapa 3 - configuração de saudação protegida recriar

No modelo exportado de hello, procure `protectedSettings` e substitua hello exportada protegido de configuração do objeto com um novo que inclui parâmetros de extensão Olá necessário e um valor para cada um.

No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá novo protegido configuração seria semelhante a saudação de exemplo a seguir:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

recurso de extensão final Olá parece semelhante toohello JSON de exemplo a seguir:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Se usar os valores de propriedade de tooprovide de parâmetros de modelo, será necessário toobe criado. Ao criar parâmetros de modelo para definir valores de protegido, verifique Olá de toouse-se de que `SecureString` tipo de parâmetro para que os valores confidenciais são protegidos. Para saber mais sobre como usar parâmetros, confira [Criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).

No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá parâmetros a seguir seria criado na seção de parâmetros de saudação do modelo do Gerenciador de recursos de saudação.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

Neste ponto, o modelo de saudação pode ser implantado usando qualquer método de implantação de modelo.
