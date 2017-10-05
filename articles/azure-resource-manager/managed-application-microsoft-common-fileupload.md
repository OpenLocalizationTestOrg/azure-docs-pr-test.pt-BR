---
title: "Elemento de interface do usuário FileUpload de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Common.FileUpload da interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Elemento de interface do usuário Microsoft.Common.FileUpload
Um controle que permite a um usuário especificar um ou mais arquivos a carregar. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- `constraints.accept`Especifica os tipos de arquivos que são mostrados no diálogo do arquivo do navegador. Consulte a [especificação do HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para obter os valores permitidos. O valor padrão é **null**.
- Se `options.multiple` é definido como **true**, o usuário pode selecionar mais de um arquivo no diálogo do arquivo do navegador. O valor padrão é **false**.
- Esse elemento dá suporte ao carregamento de arquivos em dois modos com base no valor de `options.uploadMode`. Se **file** for especificado, a saída conterá o conteúdo do arquivo como um blob. Se **url** for especificado, o arquivo será carregado em um local temporário e a saída conterá a URL do blob. Blobs temporários serão limpos após 24 horas. O valor padrão é **file**.
- O valor de `options.openMode` determina como o arquivo é lido. Se o arquivo deve ser texto sem formatação, especifique **text**; caso contrário, especifique **binary**. O valor padrão é **text**.
- Se `options.uploadMode` é definido como **file** e `options.openMode` é definido como **binary**, a saída é codificada em base64.
- `options.encoding`Especifica a codificação a ser usada para ler o arquivo. O valor padrão é **UTF-8**e é usado apenas quando `options.openMode` é definido como **text**.

## <a name="sample-output"></a>Saída de exemplo
Se options.multiple for false e options.uploadMode for file, a saída conterá o conteúdo do arquivo como uma cadeia de caracteres JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Se options.multiple for true e options.uploadMode for file, a saída conterá o conteúdo do arquivo como uma matriz JSON:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Se options.multiple for false e options.uploadMode for url, a saída conterá a URL como uma cadeia de caracteres JSON:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Se options.multiple for true e options.uploadMode for url, a saída conterá a URL como uma matriz JSON:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Ao testar um CreateUiDefinition, alguns navegadores (como o Google Chrome) truncam URLs geradas pelo elemento Microsoft.Common.FileUpload no console do navegador. Talvez seja necessário clicar com o botão direito do mouse em links individuais para copiar as URLs completas.


## <a name="next-steps"></a>Próximas etapas
* Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
