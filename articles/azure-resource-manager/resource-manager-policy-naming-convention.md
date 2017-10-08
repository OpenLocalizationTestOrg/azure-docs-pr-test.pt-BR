---
title: "políticas de recursos aaaAzure para convenções de nomenclatura | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para convenções de nomenclatura de recursos."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Aplicar políticas de recursos a nomes e texto
Este tópico mostra vários [políticas de recursos](resource-manager-policy.md) você pode aplicar as convenções de nomenclatura e texto tooestablish. Essas políticas garantem a consistência de nomes de recursos e valores de marcação. 

## <a name="set-naming-convention-with-wildcard"></a>Definir a convenção de nomenclatura com um curinga
Olá, exemplo a seguir mostra uso Olá de caractere curinga, que é suportado pelo Olá **como** condição. Olá condição declara que se hello nome corresponder padrão mencionadas hello (namePrefix\*nameSuffix), em seguida, negar a solicitação de saudação:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Definir a convenção de nomenclatura com um padrão

toospecify que os nomes de recursos correspondem a um padrão, use Olá correspondem à condição. exemplo a seguir Hello requer nomes toostart com `contoso` e conter seis letras adicionais:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Definir um padrão de data para um valor de marcação

toorequire um padrão de data de dois dígitos, hífen, três letras, traço e quatro dígitos, use:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo. escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md). 
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

