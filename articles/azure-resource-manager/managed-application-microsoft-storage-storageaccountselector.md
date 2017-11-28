---
title: "elemento de interface do usuário StorageAccountSelector de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Storage.StorageAccountSelector da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="f2a66-103">Elemento de interface do usuário Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="f2a66-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="f2a66-104">Um controle para selecionar uma conta de armazenamento nova ou existente.</span><span class="sxs-lookup"><span data-stu-id="f2a66-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="f2a66-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f2a66-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f2a66-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="f2a66-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="f2a66-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="f2a66-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="f2a66-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="f2a66-109">Remarks</span></span>
- <span data-ttu-id="f2a66-110">Se especificado, `defaultValue.name` é validados automaticamente por exclusividade.</span><span class="sxs-lookup"><span data-stu-id="f2a66-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="f2a66-111">Se o nome de conta de armazenamento Olá não for exclusivo, o usuário de saudação deve especificar um nome diferente ou escolha uma conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="f2a66-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="f2a66-112">Olá valor padrão para `defaultValue.type` é **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="f2a66-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="f2a66-113">Os tipos não especificados em `constraints.allowedTypes` ficam ocultos e os tipos não especificados em `constraints.excludedTypes` são mostrados.</span><span class="sxs-lookup"><span data-stu-id="f2a66-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="f2a66-114">`constraints.allowedTypes` e `constraints.excludedTypes` são opcionais, mas não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="f2a66-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="f2a66-115">Se `options.hideExisting` é **true**, usuário Olá não é possível escolher uma conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="f2a66-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="f2a66-116">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="f2a66-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="f2a66-117">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="f2a66-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="f2a66-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2a66-118">Next steps</span></span>
* <span data-ttu-id="f2a66-119">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2a66-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f2a66-120">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2a66-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f2a66-121">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f2a66-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
