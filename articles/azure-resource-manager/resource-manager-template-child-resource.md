---
title: recurso de filho aaaDefine no modelo do Azure | Microsoft Docs
description: "Mostra como tooset Olá tipo de recurso e o nome de recurso filho em um modelo do Gerenciador de recursos do Azure"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Definir o nome e o tipo do recurso filho no modelo do Resource Manager
Ao criar um modelo, você normalmente precisa tooinclude um recurso filho que é o recurso pai de tooa relacionados. Por exemplo, o modelo pode incluir um banco de dados e um servidor SQL. Olá SQL server é o recurso pai de Olá, e banco de dados de saudação recurso filho de saudação. 

formato de Olá Olá filho do tipo de recurso é:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

formato de saudação do nome de recurso Olá filho é:`{parent-resource-name}/{child-resource-name}`

No entanto, você especificar o tipo hello e o nome de um modelo diferente com base em se ele está aninhado no recurso pai de hello, ou por conta própria no nível superior de saudação. Este tópico mostra como toohandle ambas as abordagens.

Ao construir um recurso de tooa referência totalmente qualificada, Olá ordem toocombine segmentos de tipo hello e nome não é simplesmente uma concatenação de saudação dois.  Em vez disso, após a saudação namespace, use uma sequência de *nome do tipo* pares de menos específico toomost específico:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Por exemplo:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`está correto, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` não está correto

## <a name="nested-child-resource"></a>Recurso filho aninhado
toodefine de maneira mais fácil de saudação um recurso filho é toonest-lo no recurso pai de saudação. Olá, exemplo a seguir mostra um banco de dados SQL aninhado em um SQL Server.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Para o recurso de filho hello, tipo de saudação está definido muito`databases` , mas seu tipo de recurso completo é `Microsoft.Sql/servers/databases`. Você não fornecer `Microsoft.Sql/servers/` porque é considerado Olá pai do tipo de recurso. nome do recurso filho Hello está definido muito`exampledatabase` mas nome completo Olá inclui o nome do pai hello. Você não fornecer `exampleserver` porque supõe-se do recurso pai de saudação.

## <a name="top-level-child-resource"></a>Recurso filho de nível superior
Você pode definir o recurso de filho Olá no nível superior de saudação. Você pode usar essa abordagem se o recurso pai de saudação não é implantado em Olá mesmo modelo, ou se deseja toouse `copy` toocreate vários recursos filho. Com essa abordagem, forneça o tipo de recurso completo de saudação e incluem o nome do recurso pai Olá no nome de recurso Olá filho.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

banco de dados de Olá é um servidor de toohello de recursos filho, embora elas são definidas em Olá mesmo nível no modelo de saudação.

## <a name="next-steps"></a>Próximas etapas
* Para obter recomendações sobre como toocreate modelos, consulte [práticas recomendadas para a criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).
* Para obter um exemplo de como criar vários recursos filho, consulte [Implantar várias instâncias de recursos nos modelos do Azure Resource Manager](resource-group-create-multiple.md).
