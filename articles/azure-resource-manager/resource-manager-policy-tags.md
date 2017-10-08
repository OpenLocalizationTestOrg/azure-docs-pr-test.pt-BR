---
title: "políticas de recursos aaaAzure marcas | Microsoft Docs"
description: "Fornece exemplos de políticas de recurso para gerenciamento de marcas em recursos"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Aplicar políticas de recurso a marcas

Este tópico fornece a você pode aplicar o uso consistente de marcas tooensure nos recursos de regras de política comum.

Aplicação de um grupo de recursos de tooa de política de marca ou a assinatura com recursos existentes não se aplicam retroativamente recursos de toothose política hello. políticas de saudação do tooenforce sobre os recursos, disparar uma toohello de atualização existente de recursos. Este artigo inclui um exemplo do PowerShell para disparar uma atualização.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Garantir que todos os recursos em um grupo de recursos tenham um valor/marca

Um requisito comum é o de que todos os recursos em um grupo de recursos tenham uma marca e um valor específicos. Esse requisito é geralmente custos tootrack necessárias pelo departamento. Olá condições a seguir deve ser atendido:

* Olá necessário marca e valor são acrescentado toonew e recursos que não têm marca Olá atualizado.
* Olá necessário marca e o valor não pode ser removido de todos os recursos existentes.

Você atender a esse requisito, aplicando o grupo de recursos do duas políticas internas tooa.

| ID | Descrição |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Aplica uma marca necessária e seu valor padrão quando não for especificado pelo usuário hello. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Impõe uma marca necessária e seu valor. |

### <a name="powershell"></a>PowerShell

saudação de script do PowerShell a seguir atribui o grupo de recursos do hello política interna duas definições tooa. Antes de executar o script hello, atribua todas as marcas necessárias toohello recurso grupo. Cada marca no grupo de recursos de saudação é necessária para recursos de saudação no grupo de saudação. grupos de recursos de tooall tooassign em sua assinatura, não fornecem Olá `-Name` parâmetro ao obter grupos de recursos de saudação.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Depois de atribuir políticas hello, você pode disparar um tooall de atualização existente políticas de recursos tooenforce Olá marca que você adicionou. Olá, script a seguir retém outras marcas que existiam em recursos de saudação:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Exigir marcas para um tipo de recurso
saudação de exemplo a seguir mostra como toonest operadores lógicos toorequire um aplicativo de marca para apenas um tipo de recurso especificado (neste caso, as contas de armazenamento).

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Exigir marca
Olá seguinte política nega as solicitações que não têm uma marca que contém a chave "costCenter" (qualquer valor pode ser aplicado):

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo. escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).
* Para políticas de tooresource uma introdução, consulte [visão geral do recurso política](resource-manager-policy.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

