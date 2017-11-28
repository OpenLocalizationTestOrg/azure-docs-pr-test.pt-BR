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
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="cbf46-103">Aplicar a contas de toostorage de políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="cbf46-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="cbf46-104">Este tópico mostra vários [políticas de recursos](resource-manager-policy.md) você pode aplicar tooAzure contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cbf46-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="cbf46-105">Essas políticas garantem a consistência para contas de armazenamento Olá implantados na sua organização.</span><span class="sxs-lookup"><span data-stu-id="cbf46-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="cbf46-106">Definir tipos de conta de armazenamento permitidos</span><span class="sxs-lookup"><span data-stu-id="cbf46-106">Define permitted storage account types</span></span>

<span data-ttu-id="cbf46-107">Olá seguinte política restringe quais [tipos de conta de armazenamento](../storage/common/storage-redundancy.md) pode ser implantado:</span><span class="sxs-lookup"><span data-stu-id="cbf46-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="cbf46-108">Uma regra de política semelhante com um parâmetro para aceitar Olá permitido SKUs está disponível como uma definição de política interna.</span><span class="sxs-lookup"><span data-stu-id="cbf46-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="cbf46-109">diretiva interna Olá possui ID de recurso de saudação do `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="cbf46-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="cbf46-110">Definir o nível de acesso permitido</span><span class="sxs-lookup"><span data-stu-id="cbf46-110">Define permitted access tier</span></span>

<span data-ttu-id="cbf46-111">Hello, seguinte política especifica o tipo de saudação do [camada de acesso](../storage/blobs/storage-blob-storage-tiers.md) que pode ser especificada para contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="cbf46-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="cbf46-112">Certifique-se de que a criptografia esteja habilitada</span><span class="sxs-lookup"><span data-stu-id="cbf46-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="cbf46-113">Hello seguinte política requer que todos os tooenable de contas de armazenamento [criptografia do serviço de armazenamento](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="cbf46-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="cbf46-114">Essa regra de política também está disponível como uma definição de política interna com a ID de recurso de saudação do `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="cbf46-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbf46-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cbf46-115">Next steps</span></span>
* <span data-ttu-id="cbf46-116">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="cbf46-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="cbf46-117">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="cbf46-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="cbf46-118">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbf46-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="cbf46-119">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="cbf46-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="cbf46-120">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cbf46-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

