---
title: "AAA como tooget uma instância do processador de mídia usando REST | Microsoft Docs"
description: "Saiba como toocreate uma tooencode de componente de processador de mídia, converter o formato, criptografar ou descriptografar o conteúdo de mídia do Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="af551-103">Como tooget uma instância do processador de mídia</span><span class="sxs-lookup"><span data-stu-id="af551-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af551-104">.NET</span><span class="sxs-lookup"><span data-stu-id="af551-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="af551-105">REST</span><span class="sxs-lookup"><span data-stu-id="af551-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="af551-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="af551-106">Overview</span></span>
<span data-ttu-id="af551-107">Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="af551-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="af551-108">Normalmente você cria um processador de mídia quando você estiver criando uma tarefa tooencode, criptografar ou converter o formato de saudação do conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="af551-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="af551-109">Processadores de mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="af551-109">Azure media processors</span></span> 

<span data-ttu-id="af551-110">Olá tópico a seguir fornece listas de processadores de mídia:</span><span class="sxs-lookup"><span data-stu-id="af551-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="af551-111">Codificação de processadores de mídia</span><span class="sxs-lookup"><span data-stu-id="af551-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="af551-112">Processadores de mídia do Analytics</span><span class="sxs-lookup"><span data-stu-id="af551-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="af551-113">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="af551-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="af551-114">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="af551-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="af551-115">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="af551-115">Connect tooMedia Services</span></span>

<span data-ttu-id="af551-116">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="af551-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="af551-117">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="af551-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="af551-118">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="af551-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="af551-119">Obter um processador de mídia</span><span class="sxs-lookup"><span data-stu-id="af551-119">Get a media processor</span></span>

<span data-ttu-id="af551-120">Olá chamada REST a seguir mostra como tooget um processador de mídia instância pelo nome (nesse caso, **codificador de mídia padrão**).</span><span class="sxs-lookup"><span data-stu-id="af551-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="af551-121">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af551-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="af551-122">Resposta:</span><span class="sxs-lookup"><span data-stu-id="af551-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="af551-123">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="af551-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="af551-124">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="af551-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="af551-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af551-125">Next Steps</span></span>
<span data-ttu-id="af551-126">Agora que você sabe como tooget uma instância do processador de mídia, vá toohello [como um ativo de tooEncode](media-services-rest-get-started.md) tópico que lhe mostrará como toouse Olá tooencode codificador de mídia padrão um ativo.</span><span class="sxs-lookup"><span data-stu-id="af551-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

