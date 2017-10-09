---
title: "segurança de aaaEnforce com as políticas em VMs do Linux no Azure | Microsoft Docs"
description: "Como tooapply tooan uma diretiva Máquina Virtual do Azure Resource Manager Linux"
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
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="4d0b3-103">Aplicar políticas tooLinux VMs com o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="4d0b3-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="4d0b3-104">Usando políticas, uma organização pode aplicar várias convenções e regras em toda a empresa hello.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="4d0b3-105">Imposição de comportamento de saudação desejado pode ajudar a reduzir o risco ao toohello sucesso da organização de saudação de contribuição.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="4d0b3-106">Neste artigo, descreveremos como você pode usar o comportamento do Gerenciador de recursos do Azure políticas toodefine Olá desejado para as máquinas virtuais de sua organização.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="4d0b3-107">Para toopolicies uma introdução, consulte [recursos de toomanage de política de uso e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="4d0b3-108">Máquinas virtuais permitidas</span><span class="sxs-lookup"><span data-stu-id="4d0b3-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="4d0b3-109">tooensure que máquinas virtuais para a sua organização são compatíveis com um aplicativo, você pode restringir Olá permitido sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="4d0b3-110">Olá política de exemplo a seguir, você permitir somente Ubuntu 14.04.2-LTS as máquinas virtuais toobe criado.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

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

<span data-ttu-id="4d0b3-111">Use uma saudação de toomodify curinga anterior política tooallow qualquer imagem Ubuntu LTS:</span><span class="sxs-lookup"><span data-stu-id="4d0b3-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="4d0b3-112">Para obter informações sobre campos de política, consulte [Aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="4d0b3-113">Discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="4d0b3-113">Managed disks</span></span>

<span data-ttu-id="4d0b3-114">toorequire Olá uso de discos gerenciados, use Olá diretiva a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d0b3-114">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="4d0b3-115">Imagens de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="4d0b3-115">Images for Virtual Machines</span></span>

<span data-ttu-id="4d0b3-116">Por motivos de segurança, você pode exigir que apenas imagens personalizadas aprovadas sejam implantadas em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="4d0b3-117">Você pode especificar o grupo de recursos de saudação que contém imagens Olá aprovado ou imagens aprovados específicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="4d0b3-118">saudação de exemplo a seguir exige imagens de um grupo de recursos aprovado:</span><span class="sxs-lookup"><span data-stu-id="4d0b3-118">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="4d0b3-119">Olá exemplo a seguir especifica a imagem de saudação aprovada IDs:</span><span class="sxs-lookup"><span data-stu-id="4d0b3-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="4d0b3-120">Extensões de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="4d0b3-120">Virtual Machine extensions</span></span>

<span data-ttu-id="4d0b3-121">Talvez você queira tooforbid o uso de certos tipos de extensões.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="4d0b3-122">Por exemplo, uma extensão pode não ser compatível com determinadas imagens de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="4d0b3-123">Olá mostrado no exemplo a seguir como tooblock uma extensão específica.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="4d0b3-124">Ele usa o publicador e tipo toodetermine tooblock qual extensão.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="4d0b3-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d0b3-125">Next steps</span></span>
* <span data-ttu-id="4d0b3-126">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="4d0b3-127">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4d0b3-128">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="4d0b3-129">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="4d0b3-130">Para políticas de tooresource uma introdução, consulte [visão geral do recurso política](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="4d0b3-131">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
