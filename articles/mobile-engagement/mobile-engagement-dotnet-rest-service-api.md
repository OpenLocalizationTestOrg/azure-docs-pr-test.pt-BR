---
title: "Olá aaaUsing tooaccess da API REST APIs de serviço do Azure Mobile Engagement"
description: "Descreve como toouse Olá tooaccess de APIs de REST do Mobile Engagement APIs de serviço do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="ac00d-103">Usando REST tooaccess APIs de serviço do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ac00d-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="ac00d-104">O Azure Mobile Engagement fornece Olá [API REST do Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) para você toomanage dispositivos, campanhas de alcance/enviar por Push etc.</span><span class="sxs-lookup"><span data-stu-id="ac00d-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="ac00d-105">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="ac00d-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="ac00d-106">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="ac00d-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="ac00d-107">Se você não quiser toouse Olá APIs REST diretamente, nós também fornecemos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que você pode usar com ferramentas toogenerate SDKs para seu idioma preferencial.</span><span class="sxs-lookup"><span data-stu-id="ac00d-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="ac00d-108">É recomendável usar Olá [AutoRest](https://github.com/Azure/AutoRest) ferramenta toogenerate o SDK do nosso arquivo Swagger.</span><span class="sxs-lookup"><span data-stu-id="ac00d-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="ac00d-109">Criamos um SDK .NET de maneira semelhante, que permite que você toointeract com essas APIs usando um wrapper em c# e você não tiver toodo Olá negociação do token de autenticação e atualização por conta própria.</span><span class="sxs-lookup"><span data-stu-id="ac00d-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="ac00d-110">Consulte [amostra do SDK do serviço de API .NET](mobile-engagement-dotnet-sdk-service-api.md) toolearn como toouse Olá .net SDK para API</span><span class="sxs-lookup"><span data-stu-id="ac00d-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
