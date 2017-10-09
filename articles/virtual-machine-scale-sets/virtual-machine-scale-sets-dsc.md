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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="ab4cd-103">Usando conjuntos de escala de máquinas virtuais com hello extensão de DSC do Azure</span><span class="sxs-lookup"><span data-stu-id="ab4cd-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="ab4cd-104">[Conjuntos de escala de máquina virtual](virtual-machine-scale-sets-overview.md) pode ser usado com hello [configuração de estado desejado (DSC) da Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) manipulador de extensão.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="ab4cd-105">Conjuntos de escala de máquinas virtuais fornecem uma maneira toodeploy e gerenciarem um grande número de máquinas virtuais e elasticidade podem escalar horizontalmente em tooload de resposta.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="ab4cd-106">A DSC é usado tooconfigure Olá VMs conforme eles forem on-line para que eles estão executando o software de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="ab4cd-107">Diferenças entre implantar máquinas tooVirtual e conjuntos de escala de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="ab4cd-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="ab4cd-108">estrutura de modelo subjacente Olá para um conjunto de escala de máquina virtual é ligeiramente diferente de uma única VM.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="ab4cd-109">Especificamente, uma única VM implanta extensões no nó de "virtualMachines" hello.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="ab4cd-110">Há uma entrada do tipo "extensões" onde a DSC é adicionado toohello modelo</span><span class="sxs-lookup"><span data-stu-id="ab4cd-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="ab4cd-111">Um nó de conjunto de escala de máquina virtual tem uma seção de "propriedades" com hello "VirtualMachineProfile", o atributo "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="ab4cd-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="ab4cd-112">O DSC é adicionado sob "extensões"</span><span class="sxs-lookup"><span data-stu-id="ab4cd-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="ab4cd-113">Comportamento de um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="ab4cd-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="ab4cd-114">comportamento de saudação para um conjunto de escala de máquina virtual é o comportamento de toohello idênticos para uma única VM.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="ab4cd-115">Quando uma nova VM é criada, ela é automaticamente provisionada com hello extensão DSC.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="ab4cd-116">Se uma versão mais recente do hello que WMF é necessário por extensão hello, Olá VM reinicia antes de ser colocado online.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="ab4cd-117">Quando estiver online, ele baixa Olá DSC configuração zip e provisioná-la em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ab4cd-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="ab4cd-118">Mais detalhes podem ser encontrados em [hello Azure visão geral da extensão DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab4cd-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab4cd-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab4cd-119">Next steps</span></span>
<span data-ttu-id="ab4cd-120">Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab4cd-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ab4cd-121">Saiba como Olá [extensão DSC manipula com segurança as credenciais](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab4cd-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="ab4cd-122">Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab4cd-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="ab4cd-123">Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="ab4cd-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

