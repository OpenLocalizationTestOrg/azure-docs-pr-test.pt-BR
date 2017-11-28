---
title: "Usando a API REST para acessar as APIs de serviço do Azure Mobile Engagement"
description: "Descreve como usar as APIs REST do Mobile Engagement para acessar as APIs de Serviço do Azure Mobile Engagement"
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="fff8d-103">Usando REST para acessar as APIs de Serviço do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fff8d-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="fff8d-104">O Azure Mobile Engagement fornece a [API REST do Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) para gerenciar campanhas de dispositivos, push/alcance, etc.</span><span class="sxs-lookup"><span data-stu-id="fff8d-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="fff8d-105">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="fff8d-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="fff8d-106">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="fff8d-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="fff8d-107">Se você não quiser usar as APIs REST diretamente, também forneceremos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que pode ser usado com ferramentas para gerar SDKs em seu idioma de preferência.</span><span class="sxs-lookup"><span data-stu-id="fff8d-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="fff8d-108">Recomendamos usar a ferramenta [AutoRest](https://github.com/Azure/AutoRest) para gerar o SDK do nosso arquivo de Swagger.</span><span class="sxs-lookup"><span data-stu-id="fff8d-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="fff8d-109">Criamos um SDK do .NET de forma semelhante que permite que você interaja com essas APIs usando um wrapper C#. Você não precisará fazer a negociação do token de autenticação e a atualização por conta própria.</span><span class="sxs-lookup"><span data-stu-id="fff8d-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="fff8d-110">Consulte [Amostra do SDK do .NET da API de serviço](mobile-engagement-dotnet-sdk-service-api.md) para aprender a usar o SDK do .Net para API</span><span class="sxs-lookup"><span data-stu-id="fff8d-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>
