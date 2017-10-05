---
title: "Uso de Configuração de Estado Desejado com Conjuntos de Dimensionamento de Máquinas Virtuais | Microsoft Docs"
description: "Uso de Conjuntos de Escala de Máquina Virtual com a Extensão de DSC do Azure"
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
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="0df4b-103">Uso de Conjuntos de Escala de Máquina Virtual com a Extensão de DSC do Azure</span><span class="sxs-lookup"><span data-stu-id="0df4b-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="0df4b-104">[Os Conjuntos de Dimensionamento de Máquina Virtual](virtual-machine-scale-sets-overview.md) podem ser usados com o manipulador de extensão [DSC (Configuração de Estado Desejado) do Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0df4b-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="0df4b-105">Os conjuntos de dimensionamento de máquina virtual fornecem uma maneira de implantar e gerenciar uma grande quantidade de máquinas virtuais e podem ser reduzidos e escalados horizontalmente de forma elástica em resposta ao carregamento.</span><span class="sxs-lookup"><span data-stu-id="0df4b-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="0df4b-106">O DSC é usado para configurar as VMs quando elas ficam online, para que executem o software de produção.</span><span class="sxs-lookup"><span data-stu-id="0df4b-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="0df4b-107">Diferenças entre implantação para máquinas virtuais e conjuntos de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0df4b-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="0df4b-108">A estrutura do modelo subjacente para um conjunto de dimensionamento de máquinas virtuais é ligeiramente diferente daquela encontrada em uma única VM.</span><span class="sxs-lookup"><span data-stu-id="0df4b-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="0df4b-109">Especificamente, uma única VM implanta extensões sob o nó "virtualMachines".</span><span class="sxs-lookup"><span data-stu-id="0df4b-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="0df4b-110">Há uma entrada do tipo "extensions" em que o DSC é adicionado ao modelo</span><span class="sxs-lookup"><span data-stu-id="0df4b-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

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

<span data-ttu-id="0df4b-111">Um nó de conjunto de dimensionamento de máquinas virtuais tem uma seção "properties" com o atributo "VirtualMachineProfile", "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="0df4b-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="0df4b-112">O DSC é adicionado sob "extensões"</span><span class="sxs-lookup"><span data-stu-id="0df4b-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="0df4b-113">Comportamento de um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="0df4b-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="0df4b-114">O comportamento de um conjunto de dimensionamento de máquinas virtuais é idêntico ao comportamento de uma única VM.</span><span class="sxs-lookup"><span data-stu-id="0df4b-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="0df4b-115">Quando uma nova VM é criada, ela é provisionada automaticamente com a extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="0df4b-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="0df4b-116">Se uma versão mais recente do WMF for necessária para a extensão, a VM será reiniciada antes de ser colocada online.</span><span class="sxs-lookup"><span data-stu-id="0df4b-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="0df4b-117">Quando ela estiver online, baixará o arquivo .zip de configuração de DSC e o provisionará na VM.</span><span class="sxs-lookup"><span data-stu-id="0df4b-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="0df4b-118">Mais detalhes podem ser encontrados em [Visão geral da Extensão DSC do Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0df4b-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0df4b-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0df4b-119">Next steps</span></span>
<span data-ttu-id="0df4b-120">Examine o [modelo do Azure Resource Manager para a extensão de DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0df4b-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0df4b-121">Saiba como a [extensão DSC manipula com segurança as credenciais](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0df4b-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="0df4b-122">Para saber mais sobre o manipulador de extensões DSC do Azure, confira [Introduction to the Azure Desired State Configuration extension handler (Introdução ao manipulador de extensões Configuração de Estado Desejado do Azure)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0df4b-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="0df4b-123">Para saber mais sobre a DSC do PowerShell, [visite o centro de documentação do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="0df4b-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

