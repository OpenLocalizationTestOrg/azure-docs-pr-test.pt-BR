---
title: "Funções Criar definições de interface do usuário de aplicativos gerenciados pelo Azure | Microsoft Docs"
description: "Descreve as funções para uso na criação de definições de interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 23e407bf93bc51116ca45339bffcb801d69290f0
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
---
# <a name="createuidefinition-elements"></a>Elementos CreateUiDefinition
Este artigo descreve o esquema e as propriedades de todos os elementos de um CreateUiDefinition com suporte. Use esses elementos ao [criar um Aplicativo Gerenciado do Azure](publish-service-catalog-app.md). O esquema para a maioria dos elementos é o seguinte:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```

| Propriedade | Obrigatório | Descrição |
| -------- | -------- | ----------- |
| name | Sim | Um identificador interno para fazer referência a uma instância específica de um elemento. O uso mais comum do nome do elemento está em `outputs`, onde os valores de saída de elementos especificados são mapeados para os parâmetros do modelo. Você também pode usá-lo para associar o valor de saída de um elemento ao `defaultValue` de outro elemento. |
| type | Sim | O controle de interface do usuário a ser processado para o elemento. Para obter uma lista dos tipos com suporte, consulte [Elementos](#elements). |
| label | Sim | O texto de exibição do elemento. Alguns tipos de elemento contêm vários rótulos e, portanto, o valor pode ser um objeto que contém várias cadeias de caracteres. |
| defaultValue | Não | O valor padrão do elemento. Alguns tipos de elemento dão suporte a valores padrão complexos e, portanto, o valor pode ser um objeto. |
| toolTip | Não | O texto exibido na dica de ferramenta do elemento. Semelhante a `label`, alguns elementos dão suporte a várias cadeias de caracteres de dica de ferramenta. Links embutidos podem ser inseridos usando a sintaxe de markdown.
| constraints | Não | Uma ou mais propriedades que são usadas para personalizar o comportamento de validação do elemento. As propriedades com suporte a restrições variam de acordo com o tipo de elemento. Alguns tipos de elemento não dão suporte à personalização do comportamento de validação e, portanto, não têm nenhuma propriedade de restrições. |
| options | Não | Propriedades adicionais que personalizam o comportamento do elemento. Semelhantemente a `constraints`, as propriedades com suporte variam de acordo com o tipo de elemento. |
| visible | Não | Indica se o elemento é exibido. Se `true`, o elemento e os elementos filho aplicáveis são exibidos. O valor padrão é `true`. Use [funções lógicas](create-uidefinition-functions.md#logical-functions) para controlar o valor da propriedade dinamicamente.

## <a name="elements"></a>Elementos

A documentação para cada elemento contém exemplo de interface do usuário, esquema, comentários sobre o comportamento do elemento (normalmente sobre a validação e a personalização com suporte) e saída de exemplo.

- [Microsoft.Common.DropDown](microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](microsoft-common-section.md)
- [Microsoft.Common.TextBox](microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Próximas etapas
* Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](overview.md).
* Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](create-uidefinition-overview.md).
