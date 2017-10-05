---
title: "Como usar parceiros para fornecer licenças Widevine para os Serviços de Mídia do Azure | Microsoft Docs"
description: "Este artigo descreve como é possível usar os serviços de mídia do Azure (AMS) para oferecer um fluxo dinamicamente é criptografado pelo AMS com os DRMs do PlayReady e Widevine. A licença do PlayReady vem do servidor de licenças do PlayReady dos serviços de mídia e a licença do Widevine é fornecida pelo servidor de licenças do castLabs."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="f5499-104">Usando parceiros  para fornecer licenças Widevine para os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="f5499-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="f5499-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f5499-105">Overview</span></span>
<span data-ttu-id="f5499-106">Os Serviços de Mídia do Microsoft Azure permitem o fornecimento de MPEG-DASH protegido por DRM Widevine, que é criptografado de acordo com a especificação de Criptografia Comum (CENC).</span><span class="sxs-lookup"><span data-stu-id="f5499-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="f5499-107">A partir da versão 3.5.2 do SDK do .NET dos Serviços de Mídia, os Serviços de Mídia permitem que você configure um modelo de licença do Widevine e obtenha licenças do Widevine.</span><span class="sxs-lookup"><span data-stu-id="f5499-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="f5499-108">Você também pode usar os seguintes parceiros do AMS para ajudar no fornecimento de licenças do Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) e [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="f5499-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="f5499-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="f5499-109">castLabs</span></span>
<span data-ttu-id="f5499-110">Você pode usar [castLabs](http://castlabs.com/company/partners/azure/) para fornecer licenças Widevine.</span><span class="sxs-lookup"><span data-stu-id="f5499-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="f5499-111">Para saber mais, consulte [Usando o castLabs para fornecer licenças DRM aos Serviços de Mídia do Azure](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="f5499-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="f5499-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="f5499-112">Axinom</span></span>
<span data-ttu-id="f5499-113">Você pode usar [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) para fornecer licenças Widevine.</span><span class="sxs-lookup"><span data-stu-id="f5499-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="f5499-114">Para saber mais, consulte [Usando o Axinom para fornecer licenças DRM aos Serviços de Mídia do Azure](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="f5499-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f5499-115">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="f5499-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f5499-116">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="f5499-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f5499-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f5499-117">See also</span></span>
[<span data-ttu-id="f5499-118">Usando a PlayReady e/ou a criptografia comum dinâmica Widevine.</span><span class="sxs-lookup"><span data-stu-id="f5499-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="f5499-119">Blog do Mingfei</span><span class="sxs-lookup"><span data-stu-id="f5499-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

