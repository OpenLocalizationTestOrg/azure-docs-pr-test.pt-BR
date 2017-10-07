---
title: "aaaDeploy gerenciamento de API do Azure services toomultiple Azure regiões | Microsoft Docs"
description: "Saiba como toodeploy um gerenciamento de API do Azure serviço instância toomultiple Azure regiões."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="9cf1d-103">Como toodeploy um gerenciamento de API do Azure serviço instância toomultiple Azure regiões</span><span class="sxs-lookup"><span data-stu-id="9cf1d-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="9cf1d-104">Gerenciamento de API dá suporte à implantação de várias regiões, que permite que a API editores toodistribute um único serviço de gerenciamento de API em qualquer número de regiões do Azure desejados.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="9cf1d-105">Isso ajuda a reduzir a solicitação de latência percebida pelos consumidores de API distribuídos geograficamente e também melhora a disponibilidade do serviço se uma região ficar offline.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="9cf1d-106">Quando um serviço de gerenciamento de API é criado inicialmente, ele contém apenas um [unidade] [ unit] e reside em uma única região do Azure, que é designada como Olá região primária.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="9cf1d-107">Regiões adicionais podem ser adicionados facilmente por meio de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="9cf1d-108">Um servidor de gateway de gerenciamento de API é implantado tooeach região e tráfego de chamada será gateway mais próximo toohello roteadas.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="9cf1d-109">Se uma região de ficar offline, o tráfego de saudação é automaticamente redirecionada toohello próximo gateway mais próximo.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9cf1d-110">Implantação de várias regiões só está disponível no hello  **[Premium] [ Premium]**  camada.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="9cf1d-111"><a name="add-region"></a>Implantar uma API de gerenciamento serviço instância tooa nova região</span><span class="sxs-lookup"><span data-stu-id="9cf1d-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="9cf1d-112">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9cf1d-113">No hello Portal do Azure, navegue toohello **escala e preços** página da sua instância do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Guia Escala][api-management-scale-service]

<span data-ttu-id="9cf1d-115">toodeploy tooa nova região, clique em **+ adicionar região** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Adicionar região][api-management-add-region]

<span data-ttu-id="9cf1d-117">Selecione o local de saudação da lista suspensa de saudação e definir Olá número de unidades para o com o controle deslizante de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Especificar unidades][api-management-select-location-units]

<span data-ttu-id="9cf1d-119">Clique em **adicionar** tooplace sua seleção na tabela de locais de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="9cf1d-120">Repita esse processo até que todos os locais configurados e clique em **salvar** do processo de implantação do hello barra de ferramentas toostart hello.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="9cf1d-121"><a name="remove-region"> </a>Excluir uma instância do serviço de Gerenciamento de API de um local</span><span class="sxs-lookup"><span data-stu-id="9cf1d-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="9cf1d-122">No hello Portal do Azure, navegue toohello **escala e preços** página da sua instância do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Guia Escala][api-management-scale-service]

<span data-ttu-id="9cf1d-124">Para o local de saudação você gostaria que tooremove abrir menu de contexto de saudação usando Olá **...**  botão na direita da tabela Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="9cf1d-125">Selecione Olá **excluir** opção.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-125">Select hello **Delete** option.</span></span>

![Remover região][api-management-remove-region]

<span data-ttu-id="9cf1d-127">Confirmar exclusão de saudação e clique em **salvar** tooapply alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf1d-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

