---
title: "mídia aaaScale processamento adicionando unidades de codificação - Azure |  Microsoft Docs"
description: "Saiba como unidades de codificação tooadd toohow com .NET"
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
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="a0267-103">Como tooscale codificação com o SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a0267-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0267-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a0267-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="a0267-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a0267-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="a0267-106">REST</span><span class="sxs-lookup"><span data-stu-id="a0267-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="a0267-107">Java</span><span class="sxs-lookup"><span data-stu-id="a0267-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="a0267-108">PHP</span><span class="sxs-lookup"><span data-stu-id="a0267-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="a0267-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a0267-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0267-110">Verifique se Olá de tooreview [visão geral](media-services-scale-media-processing-overview.md) tooget tópico para obter mais informações sobre como dimensionar um tópico de processamento de mídia.</span><span class="sxs-lookup"><span data-stu-id="a0267-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="a0267-111">toochange Olá reservado hello e tipo de número de unidade usando o SDK do .NET, de unidades reservadas de codificação Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0267-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="a0267-112">Abrindo um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="a0267-112">Opening a Support Ticket</span></span>
<span data-ttu-id="a0267-113">Por padrão, todas as contas de serviços de mídia podem dimensionar tooup too25 codificação e 5 sob demanda unidades reservadas de Streaming.</span><span class="sxs-lookup"><span data-stu-id="a0267-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="a0267-114">Você pode solicitar um limite mais alto abrindo um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="a0267-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="a0267-115">Abra um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="a0267-115">Open a support ticket</span></span>
<span data-ttu-id="a0267-116">tooopen um tíquete de suporte Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0267-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="a0267-117">Clique em [Obter suporte](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="a0267-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="a0267-118">Se você não estiver conectado, você vai ser tooenter solicitada suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="a0267-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="a0267-119">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a0267-119">Select your subscription.</span></span>
3. <span data-ttu-id="a0267-120">Em tipo de suporte, selecione "Técnico".</span><span class="sxs-lookup"><span data-stu-id="a0267-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="a0267-121">Clique em "Criar Tíquete".</span><span class="sxs-lookup"><span data-stu-id="a0267-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="a0267-122">Selecione "Azure Media Services" na lista de produtos Olá apresentada na próxima página de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0267-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="a0267-123">Selecione um "tipo de problema" que é apropriado para o seu problema.</span><span class="sxs-lookup"><span data-stu-id="a0267-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="a0267-124">Clique em Continuar.</span><span class="sxs-lookup"><span data-stu-id="a0267-124">Click Continue.</span></span>
8. <span data-ttu-id="a0267-125">Siga as instruções na próxima página e, em seguida, insira os detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="a0267-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="a0267-126">Clique em enviar um tíquete de saudação tooopen.</span><span class="sxs-lookup"><span data-stu-id="a0267-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a0267-127">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a0267-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0267-128">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a0267-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

