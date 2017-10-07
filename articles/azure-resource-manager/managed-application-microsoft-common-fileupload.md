---
title: "elemento de interface do usuário carregamento de arquivos de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.FileUpload da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Elemento de interface do usuário Microsoft.Common.FileUpload
Um controle que permite que um usuário toospecify um ou mais arquivos tooupload. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

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
- `constraints.accept`Especifica os tipos de saudação de arquivos que são mostrados na caixa de diálogo do navegador de saudação do arquivo. Consulte Olá [especificação de HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para os valores permitidos. valor padrão de saudação é **nulo**.
- Se `options.multiple` está definido muito**true**, usuário Olá é permitido tooselect mais de um arquivo na caixa de diálogo do navegador de saudação do arquivo. valor padrão de saudação é **false**.
- Esse elemento oferece suporte ao carregar arquivos em dois modos com base no valor de saudação do `options.uploadMode`. Se **arquivo** for especificado, saída de hello contém o conteúdo de saudação do arquivo hello como um blob. Se **url** for especificado, arquivo hello local temporário tooa carregado e saída de hello contém a URL de saudação do blob de saudação. Blobs temporários serão limpos após 24 horas. valor padrão de saudação é **arquivo**.
- Olá valor `options.openMode` determina como o arquivo de saudação é lido. Especifique se o arquivo de saudação toobe esperado um texto sem formatação, **texto**; caso contrário, especifique **binário**. valor padrão de saudação é **texto**.
- Se `options.uploadMode` está definido muito**arquivo** e `options.openMode` está definido muito**binário**, saída de hello é codificado na base64.
- `options.encoding`Especifica o toouse codificação Olá ao ler o arquivo hello. valor padrão de saudação é **UTF-8**e é usado apenas quando `options.openMode` está definido muito**texto**.

## <a name="sample-output"></a>Saída de exemplo
Se options.multiple for false e options.uploadMode é o arquivo, a saída contém conteúdo de saudação do arquivo hello como uma cadeia de caracteres JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Se options.multiple for verdadeira and'options.uploadMode é um arquivo, a saída contém conteúdo Olá arquivos hello como uma matriz JSON:

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

Ao testar um CreateUiDefinition, alguns navegadores (como Google Chrome) truncam URLs geradas por elemento de Microsoft.Common.FileUpload Olá no console do navegador hello. Talvez seja necessário tooright clique links individuais toocopy Olá completo URLs.


## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
