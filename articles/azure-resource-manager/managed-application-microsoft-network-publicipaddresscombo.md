---
title: "elemento de interface do usuário PublicIpAddressCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Network.PublicIpAddressCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="72a57-103">Elemento de interface do usuário Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="72a57-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="72a57-104">Um grupo de controles para selecionar um endereço IP público novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="72a57-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="72a57-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="72a57-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="72a57-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="72a57-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="72a57-108">Se o usuário Olá seleciona 'Nenhum' para o endereço IP público, caixa de texto rótulo do nome de domínio hello está oculto.</span><span class="sxs-lookup"><span data-stu-id="72a57-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="72a57-109">Se o usuário Olá seleciona um endereço IP público existente, a caixa de texto rótulo do nome de domínio Olá está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="72a57-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="72a57-110">Seu valor é o rótulo de nome de domínio de saudação do endereço IP de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="72a57-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="72a57-111">Olá domínio nome sufixo (por exemplo, westus.cloudapp.azure.com) atualizações automaticamente com base na localização de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="72a57-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="72a57-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="72a57-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="72a57-113">Comentários</span><span class="sxs-lookup"><span data-stu-id="72a57-113">Remarks</span></span>
- <span data-ttu-id="72a57-114">Se `constraints.required.domainNameLabel` está definido muito**true**, usuário Olá deve fornecer um rótulo de nome de domínio ao criar um novo endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="72a57-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="72a57-115">Endereços IP públicos existentes sem um rótulo não ficam disponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="72a57-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="72a57-116">Se `options.hideNone` está definido muito**true**, Olá, em seguida, a opção tooselect **nenhum** para o IP público Olá endereço está oculto.</span><span class="sxs-lookup"><span data-stu-id="72a57-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="72a57-117">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="72a57-117">hello default value is **false**.</span></span>
- <span data-ttu-id="72a57-118">Se `options.hideDomainNameLabel` está definido muito**true**, em seguida, a caixa de texto de saudação do rótulo de nome de domínio está oculto.</span><span class="sxs-lookup"><span data-stu-id="72a57-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="72a57-119">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="72a57-119">hello default value is **false**.</span></span>
- <span data-ttu-id="72a57-120">Se `options.hideExisting` for true, o usuário Olá não é capaz de toochoose um endereço IP público existente.</span><span class="sxs-lookup"><span data-stu-id="72a57-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="72a57-121">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="72a57-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="72a57-122">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="72a57-122">Sample output</span></span>
<span data-ttu-id="72a57-123">Se o usuário Olá não seleciona Nenhum endereço IP público, hello seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="72a57-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="72a57-124">Se o usuário Olá seleciona um endereço IP novo ou existente, hello seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="72a57-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="72a57-125">Quando `options.hideNone` for especificado, `newOrExistingOrNone` sempre retornará **none**.</span><span class="sxs-lookup"><span data-stu-id="72a57-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="72a57-126">Quando `options.hideDomainNameLabel` for especificado, `domainNameLabel` não será declarado.</span><span class="sxs-lookup"><span data-stu-id="72a57-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72a57-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72a57-127">Next steps</span></span>
* <span data-ttu-id="72a57-128">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72a57-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="72a57-129">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72a57-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="72a57-130">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="72a57-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
