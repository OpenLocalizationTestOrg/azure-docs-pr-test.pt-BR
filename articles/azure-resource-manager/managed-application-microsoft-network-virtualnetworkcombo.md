---
title: "elemento de interface do usuário VirtualNetworkCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Network.VirtualNetworkCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="f1d63-103">Elemento de interface do usuário Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="f1d63-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="f1d63-104">Um grupo de controles para selecionar uma rede virtual nova ou existente.</span><span class="sxs-lookup"><span data-stu-id="f1d63-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="f1d63-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f1d63-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f1d63-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="f1d63-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="f1d63-108">Em wireframe superior do hello, usuário Olá separou uma nova rede virtual para que usuário Olá pode personalizar o prefixo de nome e endereço de cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f1d63-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="f1d63-109">Configurar sub-redes, nesse caso, é opcional.</span><span class="sxs-lookup"><span data-stu-id="f1d63-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="f1d63-110">Olá inferior wireframe, usuário Olá separou uma rede virtual existente, para que o usuário Olá deve mapear cada modelo de implantação de saudação sub-rede requer tooan subrede existente.</span><span class="sxs-lookup"><span data-stu-id="f1d63-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="f1d63-111">Configurar sub-redes, nesse caso, é necessário.</span><span class="sxs-lookup"><span data-stu-id="f1d63-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="f1d63-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="f1d63-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="f1d63-113">Comentários</span><span class="sxs-lookup"><span data-stu-id="f1d63-113">Remarks</span></span>
- <span data-ttu-id="f1d63-114">Se especificado, Olá primeiro prefixo de endereço sem sobreposição de tamanho `defaultValue.addressPrefixSize` é determinado automaticamente com base em redes virtuais existentes na assinatura saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1d63-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="f1d63-115">Olá valor padrão para `defaultValue.name` e `defaultValue.addressPrefixSize` é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="f1d63-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="f1d63-116">`constraints.minAddressPrefixSize`deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="f1d63-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="f1d63-117">Nenhuma rede virtual existente com um espaço de endereço menor do que o hello valor especificado não estão disponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="f1d63-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="f1d63-118">`subnets`deve ser especificado e `constraints.minAddressPrefixSize` deve ser especificado para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f1d63-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="f1d63-119">Ao criar uma nova rede virtual, o prefixo de endereço da sub-rede cada é calculado automaticamente com base no prefixo de endereço da rede virtual hello e os respectivos `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="f1d63-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="f1d63-120">Ao usar uma rede virtual existente, todas as sub-redes menores que os respectivos `constraints.minAddressPrefixSize` ficarão indisponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="f1d63-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="f1d63-121">Além disso, se especificado, as sub-redes que não contêm pelo menos `minAddressCount` endereços disponíveis ficam indisponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="f1d63-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="f1d63-122">valor padrão de saudação é **0**.</span><span class="sxs-lookup"><span data-stu-id="f1d63-122">hello default value is **0**.</span></span> <span data-ttu-id="f1d63-123">tooensure que Olá endereços disponíveis são contíguas, especifique **true** para `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="f1d63-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="f1d63-124">valor padrão de saudação é **true**.</span><span class="sxs-lookup"><span data-stu-id="f1d63-124">hello default value is **true**.</span></span>
- <span data-ttu-id="f1d63-125">Não há suporte para a criação de sub-redes em uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f1d63-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="f1d63-126">Se `options.hideExisting` é **true**, usuário Olá não é possível escolher uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f1d63-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="f1d63-127">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="f1d63-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f1d63-128">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="f1d63-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="f1d63-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1d63-129">Next steps</span></span>
* <span data-ttu-id="f1d63-130">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1d63-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f1d63-131">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1d63-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f1d63-132">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f1d63-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
