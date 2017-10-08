---
title: "políticas de aaaAzure de recursos para contas de armazenamento | Microsoft Docs"
description: "Descreve as políticas para gerenciar a implantação de saudação de contas de armazenamento do Azure Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>Aplicar a contas de toostorage de políticas de recursos
Este tópico mostra vários [políticas de recursos](resource-manager-policy.md) você pode aplicar tooAzure contas de armazenamento. Essas políticas garantem a consistência para contas de armazenamento Olá implantados na sua organização. 

## <a name="define-permitted-storage-account-types"></a>Definir tipos de conta de armazenamento permitidos

Olá seguinte política restringe quais [tipos de conta de armazenamento](../storage/common/storage-redundancy.md) pode ser implantado:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
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

Uma regra de política semelhante com um parâmetro para aceitar Olá permitido SKUs está disponível como uma definição de política interna. diretiva interna Olá possui ID de recurso de saudação do `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Definir o nível de acesso permitido

Hello, seguinte política especifica o tipo de saudação do [camada de acesso](../storage/blobs/storage-blob-storage-tiers.md) que pode ser especificada para contas de armazenamento:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>Certifique-se de que a criptografia esteja habilitada

Hello seguinte política requer que todos os tooenable de contas de armazenamento [criptografia do serviço de armazenamento](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Essa regra de política também está disponível como uma definição de política interna com a ID de recurso de saudação do `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo. escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md). 
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

