---
title: "entidades de serviços de mídia aaaManaging com REST | Microsoft Docs"
description: "Saiba como os serviços de mídia toomanage entidades com a API REST."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="8766f-103">Gerenciar entidades dos Serviços de Mídia com REST</span><span class="sxs-lookup"><span data-stu-id="8766f-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8766f-104">REST</span><span class="sxs-lookup"><span data-stu-id="8766f-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="8766f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8766f-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="8766f-106">O Serviço de mídia do Microsoft Azure é um serviço baseado em REST integrado ao OData v3.</span><span class="sxs-lookup"><span data-stu-id="8766f-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="8766f-107">Você pode adicionar, consulta, atualizar e excluir entidades Olá mesma maneira que faria com qualquer outro serviço OData.</span><span class="sxs-lookup"><span data-stu-id="8766f-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="8766f-108">As exceções serão indicadas, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="8766f-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="8766f-109">Para obter mais informações sobre OData, consulte [Documentação do protocolo Open Data](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="8766f-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="8766f-110">Este tópico mostra como entidades de serviços de mídia do Azure toomanage com REST.</span><span class="sxs-lookup"><span data-stu-id="8766f-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="8766f-111">Começando em 1 de abril de 2017, qualquer registro de trabalho em sua conta mais de 90 dias será excluído automaticamente, junto com seus registros de tarefas associados, mesmo se Olá o número total de registros é abaixo de cota máximo hello.</span><span class="sxs-lookup"><span data-stu-id="8766f-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="8766f-112">Por exemplo, no dia 1º de abril de 2017, qualquer registro de Trabalho em sua conta que seja mais antigo do que 31 de dezembro de 2016 será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8766f-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="8766f-113">Se precisar de informações de trabalho/tarefa do tooarchive hello, você pode usar código Olá descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="8766f-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="8766f-114">Considerações</span><span class="sxs-lookup"><span data-stu-id="8766f-114">Considerations</span></span>  

<span data-ttu-id="8766f-115">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8766f-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8766f-116">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8766f-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="8766f-117">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="8766f-117">Connect tooMedia Services</span></span>

<span data-ttu-id="8766f-118">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8766f-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8766f-119">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="8766f-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8766f-120">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="8766f-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="8766f-121">Adicionando entidades</span><span class="sxs-lookup"><span data-stu-id="8766f-121">Adding entities</span></span>
<span data-ttu-id="8766f-122">Cada entidade no Media Services é adicionada tooan conjunto de entidades, como ativos, por meio de uma solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="8766f-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="8766f-123">Olá mostrado no exemplo a seguir como toocreate uma AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="8766f-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="8766f-124">Consultando entidades</span><span class="sxs-lookup"><span data-stu-id="8766f-124">Querying entities</span></span>
<span data-ttu-id="8766f-125">Consultar e listar entidades é simples e envolve apenas uma solicitação HTTP GET e operações OData opcionais.</span><span class="sxs-lookup"><span data-stu-id="8766f-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="8766f-126">Olá, exemplo a seguir recupera uma lista de todas as entidades MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="8766f-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="8766f-127">Você também pode recuperar uma entidade específica ou todos os conjuntos de entidade associados a uma entidade específica, como em Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8766f-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="8766f-128">Olá, exemplo a seguir retorna apenas as propriedade de estado Olá de todos os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="8766f-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="8766f-129">Olá, exemplo a seguir retorna todos os JobTemplates com o nome hello "SampleTemplate".</span><span class="sxs-lookup"><span data-stu-id="8766f-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="8766f-130">operação Olá $expand não tem suporte nos serviços de mídia, bem como Olá não há suporte para métodos LINQ, descritos em considerações sobre o LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="8766f-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="8766f-131">Enumerar através de grandes coleções de entidades</span><span class="sxs-lookup"><span data-stu-id="8766f-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="8766f-132">Ao consultar entidades, há um limite de 1000 entidades retornadas ao mesmo tempo porque pública v2 do REST limita os resultados da consulta resultados too1000.</span><span class="sxs-lookup"><span data-stu-id="8766f-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="8766f-133">Use **ignorar** e **superior** tooenumerate por meio de coleção grandes de saudação de entidades.</span><span class="sxs-lookup"><span data-stu-id="8766f-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="8766f-134">Olá mostrado no exemplo a seguir como toouse **ignorar** e **superior** tooskip Olá primeiro 2000 trabalhos e get hello lado 1000 trabalhos.</span><span class="sxs-lookup"><span data-stu-id="8766f-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="8766f-135">Atualizando entidades</span><span class="sxs-lookup"><span data-stu-id="8766f-135">Updating entities</span></span>
<span data-ttu-id="8766f-136">Dependendo o tipo de entidade hello e do estado de saudação que está no, você pode atualizar propriedades nesta entidade por meio de um PATCH, solicitações PUT ou HTTP MERGE.</span><span class="sxs-lookup"><span data-stu-id="8766f-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="8766f-137">Para obter mais informações sobre essas operações, consulte [PATCH, PUT, MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="8766f-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="8766f-138">saudação de exemplo de código a seguir mostra como tooupdate Olá propriedade Name de uma entidade de ativos.</span><span class="sxs-lookup"><span data-stu-id="8766f-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="8766f-139">Excluindo entidades</span><span class="sxs-lookup"><span data-stu-id="8766f-139">Deleting entities</span></span>
<span data-ttu-id="8766f-140">As  entidades podem ser excluídas do Media Services usando uma solicitação HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="8766f-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="8766f-141">Dependendo da entidade Olá, ordem de saudação em que você exclui as entidades pode ser importante.</span><span class="sxs-lookup"><span data-stu-id="8766f-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="8766f-142">Por exemplo, entidades como ativos exigem que você revogar (ou excluir) todos os localizadores que fazem referência a este ativo em particular antes de excluir Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="8766f-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="8766f-143">Olá mostrado no exemplo a seguir como toodelete um localizador que foi usado tooupload um arquivo no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="8766f-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="8766f-144">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="8766f-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8766f-145">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8766f-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

