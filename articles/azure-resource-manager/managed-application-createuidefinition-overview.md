---
title: "aaaUnderstand criação de definição de interface do usuário para aplicativos gerenciados do Azure | Microsoft Docs"
description: "Descreve como toocreate definições de interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Introdução a CreateUiDefinition
Este documento apresenta os conceitos básicos de saudação de um CreateUiDefinition, que é usado pela interface de usuário de Olá Olá toogenerate portal do Azure para criar um aplicativo gerenciado.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

Um CreateUiDefinition sempre contém três propriedades: 

* handler
* version
* parâmetros

Para aplicativos gerenciados, o manipulador deve sempre ser `Microsoft.Compute.MultiVm`, e a versão mais recente com suporte de saudação é `0.1.2-preview`.

esquema de saudação da propriedade de parâmetros de saudação depende da combinação de saudação do manipulador de saudação especificado e a versão. Para aplicativos gerenciados, propriedades de saudação com suporte são `basics`, `steps`, e `outputs`. Propriedades de Noções básicas e etapas Hello contêm Olá _elementos_ - como caixas de texto e listas suspensas - toobe exibido no hello portal do Azure. Olá saídas propriedade é toomap usados valores de saída Olá Olá elementos especificados toohello parâmetros de modelo de implantação do Azure Resource Manager hello.

A inclusão de `$schema` é opcional, mas recomendada. Se especificado, Olá valor `version` deve coincidir com a versão Olá Olá `$schema` URI.

## <a name="basics"></a>Noções básicas
etapa de Noções básicas de saudação sempre é Olá primeira etapa do Assistente de saudação gerado quando a saudação portal do Azure analisa um CreateUiDefinition. Além de elementos de saudação toodisplaying especificado no `basics`, portal Olá injeta elementos para assinatura de saudação toochoose usuários, o grupo de recursos e o local para a implantação de saudação. Em geral, os elementos de consulta para parâmetros de toda a implantação, como nome de saudação de credenciais de um cluster ou o administrador, devem ficar nesta etapa.

Se o comportamento de um elemento depende da assinatura do usuário hello, grupo de recursos ou local, esse elemento não pode ser usado em Noções básicas. Por exemplo, **Microsoft.Compute.SizeSelector** depende assinatura e localização toodetermine Olá lista do usuário Olá de tamanhos disponíveis. Portanto, **Microsoft.Compute.SizeSelector** só pode ser usado em steps. Em geral, apenas elementos no hello **Microsoft.Common** namespace pode ser usado em Noções básicas. Embora alguns elementos de outros namespaces (como **Microsoft.Compute.Credentials**) que não dependem do contexto do usuário hello, ainda são permitidos.

## <a name="steps"></a>Etapas
propriedade de etapas de saudação pode conter zero ou mais toodisplay de etapas adicionais após Noções básicas, cada qual contendo um ou mais elementos. Considere adicionar etapas por função ou camada do aplicativo hello está sendo implantado. Por exemplo, adicione uma etapa para entradas de nós mestres Olá e um para nós de trabalho Olá em um cluster.

## <a name="outputs"></a>outputs
Olá, portal do Azure usa Olá `outputs` toomap elementos da propriedade de `basics` e `steps` toohello parâmetros de modelo de implantação do Azure Resource Manager Olá. chaves deste dicionário Olá são nomes de Olá Olá dos parâmetros de modelo e valores de saudação são propriedades dos objetos de saída Olá dos elementos de saudação referenciado.

## <a name="functions"></a>Funções
Semelhante muito[funções de modelo](resource-group-template-functions.md) no Azure Resource Manager (tanto na sintaxe e funcionalidade), CreateUiDefinition fornece funções para trabalhar com elementos entradas e saídas, bem como recursos como condicionais.

## <a name="next-steps"></a>Próximas etapas
O próprio CreateUiDefinition tem um esquema simples. profundidade de saudação real é proveniente de todos os elementos de saudação com suporte e funções, quais Olá documentos a seguir descrevem detalhadamente esplêndida:

- [Elementos](managed-application-createuidefinition-elements.md)
- [Funções](managed-application-createuidefinition-functions.md)

Um esquema JSON atual para CreateUiDefinition está disponível aqui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Em versões posteriores estarão disponíveis em Olá mesmo local. Substituir saudação `0.1.2-preview` parte da URL hello e hello `version` valor com o identificador de versão Olá você pretende toouse. identificadores de versão Olá atualmente com suporte são `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.
