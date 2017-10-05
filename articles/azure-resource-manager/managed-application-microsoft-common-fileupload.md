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
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="217b7-103">Elemento de interface do usuário Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="217b7-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="217b7-104">Um controle que permite a um usuário especificar um ou mais arquivos a carregar.</span><span class="sxs-lookup"><span data-stu-id="217b7-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="217b7-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="217b7-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="217b7-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="217b7-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="217b7-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="217b7-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="217b7-109">Remarks</span></span>
- <span data-ttu-id="217b7-110">`constraints.accept`Especifica os tipos de arquivos que são mostrados no diálogo do arquivo do navegador.</span><span class="sxs-lookup"><span data-stu-id="217b7-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="217b7-111">Consulte a [especificação do HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para obter os valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="217b7-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="217b7-112">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="217b7-112">The default value is **null**.</span></span>
- <span data-ttu-id="217b7-113">Se `options.multiple` é definido como **true**, o usuário pode selecionar mais de um arquivo no diálogo do arquivo do navegador.</span><span class="sxs-lookup"><span data-stu-id="217b7-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="217b7-114">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="217b7-114">The default value is **false**.</span></span>
- <span data-ttu-id="217b7-115">Esse elemento dá suporte ao carregamento de arquivos em dois modos com base no valor de `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="217b7-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="217b7-116">Se **file** for especificado, a saída conterá o conteúdo do arquivo como um blob.</span><span class="sxs-lookup"><span data-stu-id="217b7-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="217b7-117">Se **url** for especificado, o arquivo será carregado em um local temporário e a saída conterá a URL do blob.</span><span class="sxs-lookup"><span data-stu-id="217b7-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="217b7-118">Blobs temporários serão limpos após 24 horas.</span><span class="sxs-lookup"><span data-stu-id="217b7-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="217b7-119">O valor padrão é **file**.</span><span class="sxs-lookup"><span data-stu-id="217b7-119">The default value is **file**.</span></span>
- <span data-ttu-id="217b7-120">O valor de `options.openMode` determina como o arquivo é lido.</span><span class="sxs-lookup"><span data-stu-id="217b7-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="217b7-121">Se o arquivo deve ser texto sem formatação, especifique **text**; caso contrário, especifique **binary**.</span><span class="sxs-lookup"><span data-stu-id="217b7-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="217b7-122">O valor padrão é **text**.</span><span class="sxs-lookup"><span data-stu-id="217b7-122">The default value is **text**.</span></span>
- <span data-ttu-id="217b7-123">Se `options.uploadMode` é definido como **file** e `options.openMode` é definido como **binary**, a saída é codificada em base64.</span><span class="sxs-lookup"><span data-stu-id="217b7-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="217b7-124">`options.encoding`Especifica a codificação a ser usada para ler o arquivo.</span><span class="sxs-lookup"><span data-stu-id="217b7-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="217b7-125">O valor padrão é **UTF-8**e é usado apenas quando `options.openMode` é definido como **text**.</span><span class="sxs-lookup"><span data-stu-id="217b7-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="217b7-126">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="217b7-126">Sample output</span></span>
<span data-ttu-id="217b7-127">Se options.multiple for false e options.uploadMode for file, a saída conterá o conteúdo do arquivo como uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="217b7-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="217b7-128">Se options.multiple for true e options.uploadMode for file, a saída conterá o conteúdo do arquivo como uma matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="217b7-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="217b7-129">Se options.multiple for false e options.uploadMode for url, a saída conterá a URL como uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="217b7-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="217b7-130">Se options.multiple for true e options.uploadMode for url, a saída conterá a URL como uma matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="217b7-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="217b7-131">Ao testar um CreateUiDefinition, alguns navegadores (como o Google Chrome) truncam URLs geradas pelo elemento Microsoft.Common.FileUpload no console do navegador.</span><span class="sxs-lookup"><span data-stu-id="217b7-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="217b7-132">Talvez seja necessário clicar com o botão direito do mouse em links individuais para copiar as URLs completas.</span><span class="sxs-lookup"><span data-stu-id="217b7-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="217b7-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="217b7-133">Next steps</span></span>
* <span data-ttu-id="217b7-134">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="217b7-135">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="217b7-136">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
