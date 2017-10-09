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
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Aplicar políticas tooLinux VMs com o Gerenciador de recursos do Azure
Usando políticas, uma organização pode aplicar várias convenções e regras em toda a empresa hello. Imposição de comportamento de saudação desejado pode ajudar a reduzir o risco ao toohello sucesso da organização de saudação de contribuição. Neste artigo, descreveremos como você pode usar o comportamento do Gerenciador de recursos do Azure políticas toodefine Olá desejado para as máquinas virtuais de sua organização.

Para toopolicies uma introdução, consulte [recursos de toomanage de política de uso e controlar o acesso](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Máquinas virtuais permitidas
tooensure que máquinas virtuais para a sua organização são compatíveis com um aplicativo, você pode restringir Olá permitido sistemas operacionais. Olá política de exemplo a seguir, você permitir somente Ubuntu 14.04.2-LTS as máquinas virtuais toobe criado.

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

Use uma saudação de toomodify curinga anterior política tooallow qualquer imagem Ubuntu LTS: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Para obter informações sobre campos de política, consulte [Aliases de política](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Discos gerenciados

toorequire Olá uso de discos gerenciados, use Olá diretiva a seguir:

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

## <a name="images-for-virtual-machines"></a>Imagens de máquinas virtuais

Por motivos de segurança, você pode exigir que apenas imagens personalizadas aprovadas sejam implantadas em seu ambiente. Você pode especificar o grupo de recursos de saudação que contém imagens Olá aprovado ou imagens aprovados específicas de saudação.

saudação de exemplo a seguir exige imagens de um grupo de recursos aprovado:

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

Olá exemplo a seguir especifica a imagem de saudação aprovada IDs:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Extensões de Máquina Virtual

Talvez você queira tooforbid o uso de certos tipos de extensões. Por exemplo, uma extensão pode não ser compatível com determinadas imagens de máquina virtual personalizadas. Olá mostrado no exemplo a seguir como tooblock uma extensão específica. Ele usa o publicador e tipo toodetermine tooblock qual extensão.

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


## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo. escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Para políticas de tooresource uma introdução, consulte [visão geral do recurso política](../../azure-resource-manager/resource-manager-policy.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](../../azure-resource-manager/resource-manager-subscription-governance.md).
