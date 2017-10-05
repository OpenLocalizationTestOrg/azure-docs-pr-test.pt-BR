---
title: "Elemento de interface do usuário PublicIpAddressCombo de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Compute.PublicIpAddressCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="b6c85-103">Elemento de interface do usuário Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="b6c85-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="b6c85-104">Um grupo de controles para selecionar um endereço IP público novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="b6c85-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="b6c85-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b6c85-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="b6c85-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b6c85-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="b6c85-108">Se o usuário selecionar 'Nenhum' como endereço IP público, a caixa de texto de rótulo do nome de domínio ficará oculta.</span><span class="sxs-lookup"><span data-stu-id="b6c85-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="b6c85-109">Se o usuário selecionar um endereço IP público existente, a caixa de texto de rótulo do nome de domínio ficará desabilitada.</span><span class="sxs-lookup"><span data-stu-id="b6c85-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="b6c85-110">Seu valor é o rótulo de nome de domínio do endereço IP selecionado.</span><span class="sxs-lookup"><span data-stu-id="b6c85-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="b6c85-111">O sufixo do nome de domínio (por exemplo, westus.cloudapp.azure.com) é atualizado automaticamente com base no local selecionado.</span><span class="sxs-lookup"><span data-stu-id="b6c85-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="b6c85-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="b6c85-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="b6c85-113">Comentários</span><span class="sxs-lookup"><span data-stu-id="b6c85-113">Remarks</span></span>
- <span data-ttu-id="b6c85-114">Se `constraints.required.domainNameLabel` é definido como **true**, o usuário deve fornecer um rótulo de nome de domínio ao criar um novo endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="b6c85-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="b6c85-115">Endereços IP públicos existentes sem um rótulo não ficam disponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="b6c85-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="b6c85-116">Se `options.hideNone` é definido como **true**, a opção de selecionar **Nenhum** para o endereço IP público fica oculta.</span><span class="sxs-lookup"><span data-stu-id="b6c85-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="b6c85-117">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="b6c85-117">The default value is **false**.</span></span>
- <span data-ttu-id="b6c85-118">Se `options.hideDomainNameLabel` é definido como **true**, a caixa de texto do rótulo de nome de domínio fica oculta.</span><span class="sxs-lookup"><span data-stu-id="b6c85-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="b6c85-119">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="b6c85-119">The default value is **false**.</span></span>
- <span data-ttu-id="b6c85-120">Se `options.hideExisting` é true, o usuário não pode escolher um endereço IP público existente.</span><span class="sxs-lookup"><span data-stu-id="b6c85-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="b6c85-121">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="b6c85-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="b6c85-122">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="b6c85-122">Sample output</span></span>
<span data-ttu-id="b6c85-123">Se o usuário não seleciona nenhum endereço IP público,a seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="b6c85-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="b6c85-124">Se o usuário seleciona um endereço IP novo ou existente,a seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="b6c85-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="b6c85-125">Quando `options.hideNone` for especificado, `newOrExistingOrNone` sempre retornará **none**.</span><span class="sxs-lookup"><span data-stu-id="b6c85-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="b6c85-126">Quando `options.hideDomainNameLabel` for especificado, `domainNameLabel` não será declarado.</span><span class="sxs-lookup"><span data-stu-id="b6c85-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6c85-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6c85-127">Next steps</span></span>
* <span data-ttu-id="b6c85-128">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6c85-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b6c85-129">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6c85-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="b6c85-130">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="b6c85-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
