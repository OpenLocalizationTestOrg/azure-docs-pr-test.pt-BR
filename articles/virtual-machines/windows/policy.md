---
title: "segurança de aaaEnforce com as políticas em VMs do Windows no Azure | Microsoft Docs"
description: "Como tooapply tooan uma diretiva Máquina Virtual do Azure Resource Manager Windows"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="35784-103">Aplicar políticas tooWindows VMs com o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="35784-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="35784-104">Usando políticas, uma organização pode aplicar várias convenções e regras em toda a empresa hello.</span><span class="sxs-lookup"><span data-stu-id="35784-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="35784-105">Imposição de comportamento de saudação desejado pode ajudar a reduzir o risco ao toohello sucesso da organização de saudação de contribuição.</span><span class="sxs-lookup"><span data-stu-id="35784-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="35784-106">Neste artigo, descreveremos como você pode usar o comportamento do Gerenciador de recursos do Azure políticas toodefine Olá desejado para as máquinas virtuais de sua organização.</span><span class="sxs-lookup"><span data-stu-id="35784-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="35784-107">Para toopolicies uma introdução, consulte [recursos de toomanage de política de uso e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="35784-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="35784-108">Máquinas virtuais permitidas</span><span class="sxs-lookup"><span data-stu-id="35784-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="35784-109">tooensure que máquinas virtuais para a sua organização são compatíveis com um aplicativo, você pode restringir Olá permitido sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="35784-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="35784-110">Olá política de exemplo a seguir, você permitir apenas toobe máquinas de virtuais do Windows Server 2012 R2 Datacenter criado:</span><span class="sxs-lookup"><span data-stu-id="35784-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
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

<span data-ttu-id="35784-111">Use uma saudação de toomodify curinga anterior política tooallow qualquer imagem do Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="35784-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="35784-112">Use Nenhum toomodify Olá anterior política tooallow qualquer Windows Server 2012 R2 Datacenter ou imagem superior:</span><span class="sxs-lookup"><span data-stu-id="35784-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="35784-113">Para obter informações sobre campos de política, consulte [Aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="35784-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="35784-114">Discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="35784-114">Managed disks</span></span>

<span data-ttu-id="35784-115">toorequire Olá uso de discos gerenciados, use Olá diretiva a seguir:</span><span class="sxs-lookup"><span data-stu-id="35784-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="35784-116">Imagens de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="35784-116">Images for Virtual Machines</span></span>

<span data-ttu-id="35784-117">Por motivos de segurança, você pode exigir que apenas imagens personalizadas aprovadas sejam implantadas em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="35784-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="35784-118">Você pode especificar o grupo de recursos de saudação que contém imagens Olá aprovado ou imagens aprovados específicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="35784-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="35784-119">saudação de exemplo a seguir exige imagens de um grupo de recursos aprovado:</span><span class="sxs-lookup"><span data-stu-id="35784-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="35784-120">Olá exemplo a seguir especifica a imagem de saudação aprovada IDs:</span><span class="sxs-lookup"><span data-stu-id="35784-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="35784-121">Extensões de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="35784-121">Virtual Machine extensions</span></span>

<span data-ttu-id="35784-122">Talvez você queira tooforbid o uso de certos tipos de extensões.</span><span class="sxs-lookup"><span data-stu-id="35784-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="35784-123">Por exemplo, uma extensão pode não ser compatível com determinadas imagens de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="35784-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="35784-124">Olá mostrado no exemplo a seguir como tooblock uma extensão específica.</span><span class="sxs-lookup"><span data-stu-id="35784-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="35784-125">Ele usa o publicador e tipo toodetermine tooblock qual extensão.</span><span class="sxs-lookup"><span data-stu-id="35784-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="35784-126">Benefício de Uso do Azure Híbrido</span><span class="sxs-lookup"><span data-stu-id="35784-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="35784-127">Quando você tiver uma licença de local, você pode salvar a taxa de licença Olá em suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="35784-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="35784-128">Quando você não tem licença hello, você deve proíba opção hello.</span><span class="sxs-lookup"><span data-stu-id="35784-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="35784-129">Olá seguindo a política proíbe o uso do benefício de uso do Azure híbrida (AHUB):</span><span class="sxs-lookup"><span data-stu-id="35784-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="35784-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35784-130">Next steps</span></span>
* <span data-ttu-id="35784-131">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="35784-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="35784-132">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="35784-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="35784-133">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35784-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="35784-134">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="35784-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="35784-135">Para políticas de tooresource uma introdução, consulte [visão geral do recurso política](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="35784-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="35784-136">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="35784-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
