---
title: "Impor a segurança com políticas em VMs do Linux no Azure | Microsoft Docs"
description: "Como aplicar uma política a uma Máquina Virtual Windows Linux do Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="03edb-103">Aplicar políticas a VMs Linux com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03edb-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="03edb-104">Usando políticas, uma organização pode impor várias convenções e regras em toda a empresa.</span><span class="sxs-lookup"><span data-stu-id="03edb-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="03edb-105">A imposição do comportamento desejado pode ajudar a reduzir o risco e contribui para o sucesso da organização.</span><span class="sxs-lookup"><span data-stu-id="03edb-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="03edb-106">Neste artigo, descrevemos como você pode usar as políticas do Azure Resource Manager para definir o comportamento desejado das Máquinas Virtuais de sua organização.</span><span class="sxs-lookup"><span data-stu-id="03edb-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="03edb-107">Para obter uma introdução às políticas, consulte [Usar a política para gerenciar recursos e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="03edb-108">Máquinas virtuais permitidas</span><span class="sxs-lookup"><span data-stu-id="03edb-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="03edb-109">Para garantir que as máquinas virtuais de sua organização são compatíveis com um aplicativo, você pode restringir os sistemas operacionais permitidos.</span><span class="sxs-lookup"><span data-stu-id="03edb-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="03edb-110">No exemplo de política a seguir, você permite que apenas Máquinas Virtuais Ubuntu 14.04.2-LTS sejam criadas.</span><span class="sxs-lookup"><span data-stu-id="03edb-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="03edb-111">Use um curinga para modificar a política anterior a fim de permitir qualquer imagem do Ubuntu LTS:</span><span class="sxs-lookup"><span data-stu-id="03edb-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="03edb-112">Para obter informações sobre campos de política, consulte [Aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="03edb-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="03edb-113">Discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="03edb-113">Managed disks</span></span>

<span data-ttu-id="03edb-114">Para exigir o uso de discos gerenciados, use a seguinte política:</span><span class="sxs-lookup"><span data-stu-id="03edb-114">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="03edb-115">Imagens de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="03edb-115">Images for Virtual Machines</span></span>

<span data-ttu-id="03edb-116">Por motivos de segurança, você pode exigir que apenas imagens personalizadas aprovadas sejam implantadas em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="03edb-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="03edb-117">Você pode especificar o grupo de recursos que contém as imagens aprovadas ou as imagens aprovadas específicas.</span><span class="sxs-lookup"><span data-stu-id="03edb-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="03edb-118">O exemplo a seguir exige imagens de um grupo de recursos aprovado:</span><span class="sxs-lookup"><span data-stu-id="03edb-118">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="03edb-119">O exemplo a seguir especifica as IDs de imagem aprovadas:</span><span class="sxs-lookup"><span data-stu-id="03edb-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="03edb-120">Extensões de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="03edb-120">Virtual Machine extensions</span></span>

<span data-ttu-id="03edb-121">Talvez você queira proibir o uso de determinados tipos de extensões.</span><span class="sxs-lookup"><span data-stu-id="03edb-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="03edb-122">Por exemplo, uma extensão pode não ser compatível com determinadas imagens de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="03edb-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="03edb-123">O exemplo a seguir mostra como bloquear uma extensão específica.</span><span class="sxs-lookup"><span data-stu-id="03edb-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="03edb-124">Ele usa o publicador e o tipo para determinar qual extensão será bloqueada.</span><span class="sxs-lookup"><span data-stu-id="03edb-124">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="03edb-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03edb-125">Next steps</span></span>
* <span data-ttu-id="03edb-126">Depois de definir uma regra de política (conforme mostrado nos exemplos anteriores), você precisará criar a definição de política e atribuí-la a um escopo.</span><span class="sxs-lookup"><span data-stu-id="03edb-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="03edb-127">O escopo pode ser uma assinatura, grupo de recursos ou recurso.</span><span class="sxs-lookup"><span data-stu-id="03edb-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="03edb-128">Para atribuir políticas por meio do portal, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="03edb-129">Para atribuir políticas por meio da API REST, do PowerShell ou da CLI do Azure, consulte [Atribuir e gerenciar políticas por meio de script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="03edb-130">Para ver uma introdução às políticas de recurso, confira [Visão geral da política de recurso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="03edb-131">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="03edb-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
