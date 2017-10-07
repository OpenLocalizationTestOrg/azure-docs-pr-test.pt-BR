---
title: "aaaAzure aplicativo gerenciado criar funções de definição de interface do usuário | Microsoft Docs"
description: "Descreve Olá funções toouse ao criar definições de interface do usuário para aplicativos gerenciados do Azure"
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
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Elementos CreateUiDefinition
Este artigo descreve o esquema de saudação e as propriedades de todos os elementos com suporte de um CreateUiDefinition. Use esses elementos ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md). esquema de saudação à maioria dos elementos é o seguinte:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Propriedade | Obrigatório | Descrição |
| -------- | -------- | ----------- |
| name | Sim | Um identificador interno tooreference uma instância específica de um elemento. Olá uso mais comum de nome de elemento hello está em `outputs`, onde os valores de saída de saudação do hello especificado de elementos são mapeados toohello parâmetros do modelo de saudação. Você também pode usá-lo toobind Olá valor de saída de um elemento toohello `defaultValue` de outro elemento. |
| type | Sim | Olá toorender de controle de interface do usuário para o elemento de saudação. Para obter uma lista dos tipos com suporte, consulte [Elementos](#elements). |
| label | Sim | Olá exibir o texto do elemento de saudação. Alguns tipos de elemento contêm vários rótulos, valor Olá pode ser um objeto que contém várias cadeias de caracteres. |
| defaultValue | Não | valor padrão de saudação do elemento de saudação. Alguns tipos de elemento dá suporte a valores complexos, valor de saudação poderia ser um objeto. |
| toolTip | Não | Olá toodisplay texto na dica de ferramenta de saudação do elemento de saudação. Semelhante muito`label`, alguns elementos oferecem suporte a várias cadeias de caracteres de dica de ferramenta. Links embutidos podem ser inseridos usando a sintaxe de markdown.
| constraints | Não | Uma ou mais propriedades que são toocustomize usado comportamento de validação de saudação do elemento de saudação. Propriedades de Olá tem suportada para restrições variam por tipo de elemento. Alguns tipos de elemento não oferecem suporte a personalização do comportamento de validação hello e, portanto, não ter nenhuma propriedade de restrições. |
| options | Não | Propriedades adicionais que personalizam o comportamento de saudação do elemento de saudação. Semelhante muito`constraints`, propriedades de saudação com suporte variam por tipo de elemento. |
| visible | Não | Indica se o elemento de saudação é exibido. Se `true`, elemento hello e elementos filho aplicáveis são exibidos. valor padrão de saudação é `true`. Use [funções lógicas](managed-application-createuidefinition-functions.md#logical-functions) toodynamically controlar o valor desta propriedade.

## <a name="elements"></a>Elementos

Olá documentação para cada elemento contém um exemplo de interface do usuário, o esquema, comentários sobre o comportamento de saudação do elemento de saudação (geralmente sobre a validação e personalização com suporte) e a saída de exemplo.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
