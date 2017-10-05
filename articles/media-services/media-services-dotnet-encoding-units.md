---
title: "Dimensionar o processamento de mídia adicionando unidades de codificação - Azure | Microsoft Docs"
description: "Saiba como adicionar unidades de codificação com o .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="97b5e-103">Como dimensionar a codificação com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="97b5e-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97b5e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="97b5e-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="97b5e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="97b5e-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="97b5e-106">REST</span><span class="sxs-lookup"><span data-stu-id="97b5e-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="97b5e-107">Java</span><span class="sxs-lookup"><span data-stu-id="97b5e-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="97b5e-108">PHP</span><span class="sxs-lookup"><span data-stu-id="97b5e-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="97b5e-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="97b5e-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97b5e-110">Lembre-se de examinar o tópico [Visão geral](media-services-scale-media-processing-overview.md) para obter mais informações sobre o tópico de dimensionamento de processamento de mídia.</span><span class="sxs-lookup"><span data-stu-id="97b5e-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="97b5e-111">Para alterar o tipo de unidade reservada e o número de unidades reservadas para codificação usando o SDK do .NET, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="97b5e-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="97b5e-112">Abrindo um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="97b5e-112">Opening a Support Ticket</span></span>
<span data-ttu-id="97b5e-113">Por padrão, todas as contas dos Serviços de Mídia podem ser dimensionadas para até 25 Unidades Reservadas para Codificação e cinco para Streaming por Demanda.</span><span class="sxs-lookup"><span data-stu-id="97b5e-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="97b5e-114">Você pode solicitar um limite mais alto abrindo um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="97b5e-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="97b5e-115">Abra um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="97b5e-115">Open a support ticket</span></span>
<span data-ttu-id="97b5e-116">Para abrir um tíquete de suporte, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="97b5e-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="97b5e-117">Clique em [Obter suporte](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="97b5e-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="97b5e-118">Se você não estiver conectado, você será solicitado a inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="97b5e-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="97b5e-119">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="97b5e-119">Select your subscription.</span></span>
3. <span data-ttu-id="97b5e-120">Em tipo de suporte, selecione "Técnico".</span><span class="sxs-lookup"><span data-stu-id="97b5e-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="97b5e-121">Clique em "Criar Tíquete".</span><span class="sxs-lookup"><span data-stu-id="97b5e-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="97b5e-122">Selecione "Serviços de Mídia do Azure" na lista de produtos apresentados na próxima página.</span><span class="sxs-lookup"><span data-stu-id="97b5e-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="97b5e-123">Selecione um "tipo de problema" que é apropriado para o seu problema.</span><span class="sxs-lookup"><span data-stu-id="97b5e-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="97b5e-124">Clique em Continuar.</span><span class="sxs-lookup"><span data-stu-id="97b5e-124">Click Continue.</span></span>
8. <span data-ttu-id="97b5e-125">Siga as instruções na próxima página e, em seguida, insira os detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="97b5e-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="97b5e-126">Clique em Enviar para abrir o tíquete.</span><span class="sxs-lookup"><span data-stu-id="97b5e-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="97b5e-127">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="97b5e-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97b5e-128">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="97b5e-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

