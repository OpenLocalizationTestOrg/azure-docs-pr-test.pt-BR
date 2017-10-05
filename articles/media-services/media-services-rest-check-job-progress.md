---
title: Como verificar o andamento do trabalho usando a API REST | Microsoft Docs
description: Aprenda a controlar o andamento do trabalho.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a1a1f956-c035-448a-af9c-5ac15fcce9dd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: fea4383e81f3ca21955252cf1d573f1b347b5a38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-check-job-progress"></a><span data-ttu-id="ba1c4-103">Como verificar o andamento do trabalho</span><span class="sxs-lookup"><span data-stu-id="ba1c4-103">How to: check job progress</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba1c4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ba1c4-104">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="ba1c4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ba1c4-105">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="ba1c4-106">REST</span><span class="sxs-lookup"><span data-stu-id="ba1c4-106">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="ba1c4-107">Quando você executa trabalhos, geralmente precisa de uma maneira de acompanhar o andamento do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ba1c4-107">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="ba1c4-108">Você pode descobrir o status do trabalho, usando a propriedade de estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ba1c4-108">You can find out the Job status by using the Job's State property.</span></span> <span data-ttu-id="ba1c4-109">Para obter mais informações sobre a propriedade de Estado, consulte [Propriedades de entidade de trabalho](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span><span class="sxs-lookup"><span data-stu-id="ba1c4-109">For more information on the State property, see [Job Entity Properties](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="ba1c4-110">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ba1c4-110">Connect to Media Services</span></span>

<span data-ttu-id="ba1c4-111">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ba1c4-111">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ba1c4-112">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="ba1c4-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ba1c4-113">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="ba1c4-113">You must make subsequent calls to the new URI.</span></span>

## <a name="check-job-progress"></a><span data-ttu-id="ba1c4-114">Verificar o andamento do trabalho</span><span class="sxs-lookup"><span data-stu-id="ba1c4-114">Check job progress</span></span>

<span data-ttu-id="ba1c4-115">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="ba1c4-115">Request:</span></span>

    GET https://media.windows.net/api/Jobs()?$filter=Id%20eq%20'nb%3Ajid%3AUUID%3Af3c43f94-327f-2347-90bb-3bf79f8559f1'&$top=1 HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423640758&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=z5yFIG%2bk8Z2G2aXABqM60P9smHNKD7P4BfSxXanwKFc%3d
    x-ms-version: 2.11
    Host: media.windows.net



<span data-ttu-id="ba1c4-116">Resposta:</span><span class="sxs-lookup"><span data-stu-id="ba1c4-116">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 450
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d9b83c57-e26c-4d10-a20b-2be634c4b6a8
    request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    x-ms-request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains

    {"odata.metadata":"https://media.windows.net/api/$metadata#Jobs","value":[{"Id":"nb:jid:UUID:f3c43f94-327f-2347-90bb-3bf79f8559f1","Name":"Encoding BigBuckBunny into to H264 Adaptive Bitrate MP4 Set 720p","Created":"2015-02-11T01:46:08.897","LastModified":"2015-02-11T01:46:08.897","EndTime":null,"Priority":0,"RunningDuration":0.0,"StartTime":"2015-02-11T01:46:16.58","State":2,"TemplateId":null,"JobNotificationSubscriptions":[]}]} 


## <a name="media-services-learning-paths"></a><span data-ttu-id="ba1c4-117">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ba1c4-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ba1c4-118">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ba1c4-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ba1c4-119">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ba1c4-119">See also</span></span>

[<span data-ttu-id="ba1c4-120">Visão geral da API REST das Operações dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ba1c4-120">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)
