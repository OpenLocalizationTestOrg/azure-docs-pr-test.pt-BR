---
title: "aaaUsing desejado estado de configuração com escala conjuntos de máquinas virtuais | Microsoft Docs"
description: "Usando conjuntos de escala de máquinas virtuais com hello extensão de DSC do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Usando conjuntos de escala de máquinas virtuais com hello extensão de DSC do Azure
[Conjuntos de escala de máquina virtual](virtual-machine-scale-sets-overview.md) pode ser usado com hello [configuração de estado desejado (DSC) da Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) manipulador de extensão. Conjuntos de escala de máquinas virtuais fornecem uma maneira toodeploy e gerenciarem um grande número de máquinas virtuais e elasticidade podem escalar horizontalmente em tooload de resposta. A DSC é usado tooconfigure Olá VMs conforme eles forem on-line para que eles estão executando o software de produção de hello.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Diferenças entre implantar máquinas tooVirtual e conjuntos de escala de máquinas virtuais
estrutura de modelo subjacente Olá para um conjunto de escala de máquina virtual é ligeiramente diferente de uma única VM. Especificamente, uma única VM implanta extensões no nó de "virtualMachines" hello. Há uma entrada do tipo "extensões" onde a DSC é adicionado toohello modelo

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

Um nó de conjunto de escala de máquina virtual tem uma seção de "propriedades" com hello "VirtualMachineProfile", o atributo "extensionProfile". O DSC é adicionado sob "extensões"

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Comportamento de um conjunto de dimensionamento de máquinas virtuais
comportamento de saudação para um conjunto de escala de máquina virtual é o comportamento de toohello idênticos para uma única VM. Quando uma nova VM é criada, ela é automaticamente provisionada com hello extensão DSC. Se uma versão mais recente do hello que WMF é necessário por extensão hello, Olá VM reinicia antes de ser colocado online. Quando estiver online, ele baixa Olá DSC configuração zip e provisioná-la em Olá VM. Mais detalhes podem ser encontrados em [hello Azure visão geral da extensão DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Próximas etapas
Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Saiba como Olá [extensão DSC manipula com segurança as credenciais](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

