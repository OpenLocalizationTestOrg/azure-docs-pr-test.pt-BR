---
title: "Implantar serviços do Gerenciamento de API do Azure em várias regiões do Azure | Microsoft Docs"
description: "Saiba como implantar uma instância do serviço de Gerenciamento de API do Azure em múltiplas regiões do Azure."
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
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="9a127-103">Como implantar uma instância do serviço de Gerenciamento de API do Azure em múltiplas regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="9a127-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="9a127-104">O Gerenciamento de API dá suporte à implantação multirregião, que permite a editores de API distribuir um único serviço de gerenciamento de API por qualquer número desejado de regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a127-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="9a127-105">Isso ajuda a reduzir a solicitação de latência percebida pelos consumidores de API distribuídos geograficamente e também melhora a disponibilidade do serviço se uma região ficar offline.</span><span class="sxs-lookup"><span data-stu-id="9a127-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="9a127-106">Quando um serviço de Gerenciamento de API é inicialmente criado, ele contém apenas uma [unidade][unit] e reside em uma única região do Azure, que é designada como a Região Primária.</span><span class="sxs-lookup"><span data-stu-id="9a127-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="9a127-107">Regiões adicionais podem ser facilmente adicionadas por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a127-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="9a127-108">Um servidor de gateway do Gerenciamento de API é implantado em cada região e o tráfego de chamada será encaminhado para o gateway mais próximo.</span><span class="sxs-lookup"><span data-stu-id="9a127-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="9a127-109">Se uma região fica offline, o tráfego é automaticamente redirecionado para o gateway mais próximo entre os demais.</span><span class="sxs-lookup"><span data-stu-id="9a127-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a127-110">A implantação multirregião só está disponível na camada **[Premium][Premium]**.</span><span class="sxs-lookup"><span data-stu-id="9a127-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="9a127-111"><a name="add-region"> </a>Implantar uma instância do serviço de Gerenciamento de API em uma nova região</span><span class="sxs-lookup"><span data-stu-id="9a127-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="9a127-112">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9a127-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9a127-113">No Portal do Azure, navegue até a página **Escala e preço** da sua instância do serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9a127-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Guia Escala][api-management-scale-service]

<span data-ttu-id="9a127-115">Para implantar uma nova região, clique em **+ Adicionar região** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="9a127-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Adicionar região][api-management-add-region]

<span data-ttu-id="9a127-117">Selecione o local na lista suspensa e defina o número de unidades com o controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="9a127-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Especificar unidades][api-management-select-location-units]

<span data-ttu-id="9a127-119">Clique em **Adicionar** para colocar sua seleção na tabela Locais.</span><span class="sxs-lookup"><span data-stu-id="9a127-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="9a127-120">Repita esse processo até que todos os locais estejam configurados e clique em **Salvar** na barra de ferramentas para iniciar o processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="9a127-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="9a127-121"><a name="remove-region"> </a>Excluir uma instância do serviço de Gerenciamento de API de um local</span><span class="sxs-lookup"><span data-stu-id="9a127-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="9a127-122">No Portal do Azure, navegue até a página **Escala e preço** da sua instância do serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9a127-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Guia Escala][api-management-scale-service]

<span data-ttu-id="9a127-124">Para o local em que você deseja remover, abra o menu de contexto usando o botão **...** na extremidade direita da tabela.</span><span class="sxs-lookup"><span data-stu-id="9a127-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="9a127-125">Selecione a opção **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a127-125">Select the **Delete** option.</span></span>

![Remover região][api-management-remove-region]

<span data-ttu-id="9a127-127">Confirme a exclusão e clique em **Salvar** para aplicar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9a127-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

