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
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="43ade-103">Elemento de interface do usuário Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="43ade-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="43ade-104">Um controle que permite que um usuário toospecify um ou mais arquivos tooupload.</span><span class="sxs-lookup"><span data-stu-id="43ade-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="43ade-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="43ade-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="43ade-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="43ade-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="43ade-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="43ade-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="43ade-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="43ade-109">Remarks</span></span>
- <span data-ttu-id="43ade-110">`constraints.accept`Especifica os tipos de saudação de arquivos que são mostrados na caixa de diálogo do navegador de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="43ade-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="43ade-111">Consulte Olá [especificação de HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para os valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="43ade-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="43ade-112">valor padrão de saudação é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="43ade-112">hello default value is **null**.</span></span>
- <span data-ttu-id="43ade-113">Se `options.multiple` está definido muito**true**, usuário Olá é permitido tooselect mais de um arquivo na caixa de diálogo do navegador de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="43ade-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="43ade-114">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="43ade-114">hello default value is **false**.</span></span>
- <span data-ttu-id="43ade-115">Esse elemento oferece suporte ao carregar arquivos em dois modos com base no valor de saudação do `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="43ade-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="43ade-116">Se **arquivo** for especificado, saída de hello contém o conteúdo de saudação do arquivo hello como um blob.</span><span class="sxs-lookup"><span data-stu-id="43ade-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="43ade-117">Se **url** for especificado, arquivo hello local temporário tooa carregado e saída de hello contém a URL de saudação do blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ade-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="43ade-118">Blobs temporários serão limpos após 24 horas.</span><span class="sxs-lookup"><span data-stu-id="43ade-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="43ade-119">valor padrão de saudação é **arquivo**.</span><span class="sxs-lookup"><span data-stu-id="43ade-119">hello default value is **file**.</span></span>
- <span data-ttu-id="43ade-120">Olá valor `options.openMode` determina como o arquivo de saudação é lido.</span><span class="sxs-lookup"><span data-stu-id="43ade-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="43ade-121">Especifique se o arquivo de saudação toobe esperado um texto sem formatação, **texto**; caso contrário, especifique **binário**.</span><span class="sxs-lookup"><span data-stu-id="43ade-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="43ade-122">valor padrão de saudação é **texto**.</span><span class="sxs-lookup"><span data-stu-id="43ade-122">hello default value is **text**.</span></span>
- <span data-ttu-id="43ade-123">Se `options.uploadMode` está definido muito**arquivo** e `options.openMode` está definido muito**binário**, saída de hello é codificado na base64.</span><span class="sxs-lookup"><span data-stu-id="43ade-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="43ade-124">`options.encoding`Especifica o toouse codificação Olá ao ler o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="43ade-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="43ade-125">valor padrão de saudação é **UTF-8**e é usado apenas quando `options.openMode` está definido muito**texto**.</span><span class="sxs-lookup"><span data-stu-id="43ade-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="43ade-126">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="43ade-126">Sample output</span></span>
<span data-ttu-id="43ade-127">Se options.multiple for false e options.uploadMode é o arquivo, a saída contém conteúdo de saudação do arquivo hello como uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="43ade-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="43ade-128">Se options.multiple for verdadeira and'options.uploadMode é um arquivo, a saída contém conteúdo Olá arquivos hello como uma matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="43ade-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="43ade-129">Se options.multiple for false e options.uploadMode for url, a saída conterá a URL como uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="43ade-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="43ade-130">Se options.multiple for true e options.uploadMode for url, a saída conterá a URL como uma matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="43ade-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="43ade-131">Ao testar um CreateUiDefinition, alguns navegadores (como Google Chrome) truncam URLs geradas por elemento de Microsoft.Common.FileUpload Olá no console do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="43ade-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="43ade-132">Talvez seja necessário tooright clique links individuais toocopy Olá completo URLs.</span><span class="sxs-lookup"><span data-stu-id="43ade-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="43ade-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43ade-133">Next steps</span></span>
* <span data-ttu-id="43ade-134">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43ade-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="43ade-135">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43ade-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="43ade-136">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="43ade-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
