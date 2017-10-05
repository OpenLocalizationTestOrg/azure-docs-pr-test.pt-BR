---
title: "Introdução ao fornecimento de conteúdo sob demanda usando a REST | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de implementação de um aplicativo de fornecimento de conteúdo sob demanda com os Serviços de Mídia do Azure usando API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="a101a-103">Introdução ao fornecimento de conteúdo sob demanda usando a REST</span><span class="sxs-lookup"><span data-stu-id="a101a-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a101a-104">Este início rápido orienta você pelas etapas de implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) com as APIs REST dos Serviços de Mídia do Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="a101a-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="a101a-105">O tutorial apresenta o fluxo de trabalho básico dos Serviços de Mídia e os objetos e as tarefas de programação mais comuns necessárias para o desenvolvimento dos Serviços de Mídia do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="a101a-106">No final do tutorial, você poderá transmitir ou baixar progressivamente um arquivo de mídia de exemplo que você carregou, codificou e baixou.</span><span class="sxs-lookup"><span data-stu-id="a101a-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="a101a-107">A imagem a seguir mostra alguns dos objetos mais usados ao desenvolver aplicativos VoD em relação ao modelo de OData de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="a101a-108">Clique na imagem para exibi-la em tamanho normal.</span><span class="sxs-lookup"><span data-stu-id="a101a-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="a101a-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a101a-109">Prerequisites</span></span>
<span data-ttu-id="a101a-110">Os seguintes pré-requisitos são necessários para começar a desenvolver com os serviços de mídia com APIs REST.</span><span class="sxs-lookup"><span data-stu-id="a101a-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="a101a-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-111">An Azure account.</span></span> <span data-ttu-id="a101a-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a101a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a101a-113">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-113">A Media Services account.</span></span> <span data-ttu-id="a101a-114">Para criar uma conta de Serviços de Mídia, consulte [Como criar uma conta de Serviços de Mídia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a101a-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a101a-115">Noções básicas sobre como desenvolver com API REST dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="a101a-116">Para saber mais, consulte [Visão Geral da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a101a-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="a101a-117">Um aplicativo de sua escolha que pode enviar solicitações e respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="a101a-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="a101a-118">Este tutorial usa o [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="a101a-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="a101a-119">As tarefas a seguir são mostradas neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="a101a-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="a101a-120">Iniciar pontos de extremidade de streaming (usando o Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="a101a-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="a101a-121">Conectar à conta de serviços de mídia com a API REST.</span><span class="sxs-lookup"><span data-stu-id="a101a-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="a101a-122">Criar um novo ativo e carregar um arquivo de vídeo com a API REST.</span><span class="sxs-lookup"><span data-stu-id="a101a-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="a101a-123">Codificar o arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável com a API REST.</span><span class="sxs-lookup"><span data-stu-id="a101a-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="a101a-124">Publicar o ativo e obter URLs de download progressivo e streaming com API REST.</span><span class="sxs-lookup"><span data-stu-id="a101a-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="a101a-125">Reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a101a-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="a101a-126">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a101a-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a101a-127">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="a101a-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a101a-128">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="a101a-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="a101a-129">Para obter detalhes sobre as entidades do REST do AMS usadas neste tópico, consulte [Referência de API REST dos Serviços de Mídia do Azure](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="a101a-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="a101a-130">Além disso, consulte [Conceitos dos Serviços de Mídia do Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a101a-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="a101a-131">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="a101a-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a101a-132">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a101a-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="a101a-133">Iniciar pontos de extremidade de streaming usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a101a-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="a101a-134">Ao trabalhar com os Serviços de Mídia do Azure, um dos cenários mais comuns o fornecimento de vídeo via streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="a101a-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a101a-135">Os Serviços de Mídia fornecem um empacotamento dinâmico que permite a você enviar o conteúdo codificado para MP4 da taxa de bits adaptável nos formatos de transmissão suportados pelos Serviços de Mídia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem ter que armazenar as versões recolocadas de cada um dos formatos de transmissão.</span><span class="sxs-lookup"><span data-stu-id="a101a-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a101a-136">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="a101a-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a101a-137">Para iniciar seu conteúdo de streaming e tirar proveito do empacotamento dinâmico e da criptografia dinâmica, o ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar em estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="a101a-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="a101a-138">Para iniciar o ponto de extremidade de streaming, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="a101a-139">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a101a-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a101a-140">Na janela Configurações, clique em Pontos de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="a101a-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="a101a-141">Clique no ponto de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="a101a-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="a101a-142">A janela DETALHES DO PONTO DE EXTREMIDADE DE STREAMING PADRÃO é exibida.</span><span class="sxs-lookup"><span data-stu-id="a101a-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a101a-143">Clique no ícone Iniciar.</span><span class="sxs-lookup"><span data-stu-id="a101a-143">Click the Start icon.</span></span>
5. <span data-ttu-id="a101a-144">Clique no botão Salvar para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="a101a-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="a101a-145"><a id="connect"></a>Conectar-se à conta de Serviços de Mídia com a API REST</span><span class="sxs-lookup"><span data-stu-id="a101a-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="a101a-146">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a101a-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a101a-147">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a101a-148">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="a101a-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="a101a-149">Por exemplo, se depois de tentar se conectar, você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="a101a-150">Você deve postar suas chamadas de API subsequentes para https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="a101a-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="a101a-151"><a id="upload"></a>Criar um novo ativo e carregar um arquivo de vídeo com a API REST</span><span class="sxs-lookup"><span data-stu-id="a101a-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="a101a-152">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a101a-153">A entidade **Asset** pode conter vídeo, áudio, imagens, coleções de miniaturas, sequências de texto e arquivos de legendas (e os metadados sobre esses arquivos).  Depois que os arquivos são carregados no ativo, o conteúdo é armazenado com segurança na nuvem para processamento e transmissão adicionais.</span><span class="sxs-lookup"><span data-stu-id="a101a-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="a101a-154">Um dos valores que você precisa fornecer ao criar um ativo é opções de criação do ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="a101a-155">A propriedade **Options** é um valor de enumeração que descreve as opções de criptografia em que um ativo pode ser criado.</span><span class="sxs-lookup"><span data-stu-id="a101a-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="a101a-156">Um valor válido é um dos valores na lista abaixo, não uma combinação de valores desta lista:</span><span class="sxs-lookup"><span data-stu-id="a101a-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="a101a-157">**Nenhuma** = **0** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="a101a-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="a101a-158">Ao usar essa opção, seu conteúdo não é protegido quando está em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a101a-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="a101a-159">Se você pretende enviar um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="a101a-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="a101a-160">**StorageEncrypted** = **1** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega-o para o armazenamento do Azure, onde ele é armazenado, criptografado em rest.</span><span class="sxs-lookup"><span data-stu-id="a101a-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a101a-161">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um sistema de arquivos criptografado antes da codificação, então opcionalmente criptografados novamente antes do carregamento como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="a101a-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="a101a-162">O caso de uso primário para criptografia de armazenamento é quando você deseja proteger seus arquivos de mídia de entrada de alta qualidade com criptografia forte em repouso no disco.</span><span class="sxs-lookup"><span data-stu-id="a101a-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="a101a-163">**CommonEncryptionProtected** = **2** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="a101a-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="a101a-164">**EnvelopeEncryptionProtected** = **4** – use esta opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="a101a-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="a101a-165">Os arquivos devem ter sido codificados e criptografados pelo Gerenciador de Transformação.</span><span class="sxs-lookup"><span data-stu-id="a101a-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="a101a-166">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="a101a-166">Create an asset</span></span>
<span data-ttu-id="a101a-167">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada.</span><span class="sxs-lookup"><span data-stu-id="a101a-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="a101a-168">Na API REST, criar um ativo requer enviar solicitação POST para serviços de mídia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="a101a-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="a101a-169">O exemplo a seguir mostra como criar um ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="a101a-170">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="a101a-171">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-171">**HTTP Response**</span></span>

<span data-ttu-id="a101a-172">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="a101a-173">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="a101a-173">Create an AssetFile</span></span>
<span data-ttu-id="a101a-174">A entidade [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="a101a-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="a101a-175">Um arquivo de ativo está sempre associado a um ativo, e um ativo pode conter um ou vários AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="a101a-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="a101a-176">A tarefa do Codificador dos serviços de mídia falha se um objeto de arquivo de ativo não estiver associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="a101a-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="a101a-177">Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usará a solicitação **MESCLAR** HTTP para atualizar o AssetFile com as informações sobre o arquivo de mídia (como mostrado posteriormente no tópico).</span><span class="sxs-lookup"><span data-stu-id="a101a-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="a101a-178">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="a101a-179">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="a101a-180">Criando o AccessPolicy com permissão de gravação</span><span class="sxs-lookup"><span data-stu-id="a101a-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="a101a-181">Antes de carregar todos os arquivos no armazenamento de blobs, defina os direitos de política de acesso para gravar em um ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="a101a-182">Para fazer isso, POSTE uma solicitação HTTP para o conjunto de entidade AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="a101a-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="a101a-183">Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta.</span><span class="sxs-lookup"><span data-stu-id="a101a-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="a101a-184">Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="a101a-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="a101a-185">O exemplo a seguir mostra como criar um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="a101a-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="a101a-186">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="a101a-187">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-187">**HTTP Response**</span></span>

<span data-ttu-id="a101a-188">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-188">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="a101a-189">Obter a URL de carregamento</span><span class="sxs-lookup"><span data-stu-id="a101a-189">Get the Upload URL</span></span>

<span data-ttu-id="a101a-190">Para receber a URL de carregamento real, crie um localizador de SAS.</span><span class="sxs-lookup"><span data-stu-id="a101a-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="a101a-191">Os localizadores definem a hora de início e o tipo de ponto de extremidade de conexão para clientes que desejam acessar arquivos em um ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="a101a-192">Você pode criar várias entidades de localizador para um determinado par de AccessPolicy e ativos para manipular solicitações e necessidades de clientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="a101a-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="a101a-193">Cada um destes localizadores usa o valor StartTime mais o valor de DurationInMinutes do AccessPolicy para determinar quanto tempo uma URL pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="a101a-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="a101a-194">Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="a101a-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="a101a-195">Uma URL SAS tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a101a-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="a101a-196">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="a101a-196">Some considerations apply:</span></span>

* <span data-ttu-id="a101a-197">Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a101a-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="a101a-198">Para saber mais, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="a101a-198">For more information, see Locator.</span></span>
* <span data-ttu-id="a101a-199">Se você precisar carregar os arquivos imediatamente, você deve definir o valor StartTime como cinco minutos antes da hora atual.</span><span class="sxs-lookup"><span data-stu-id="a101a-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="a101a-200">Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="a101a-201">Além disso, o valor de StartTime deve estar no seguinte formato DateTime: AAAA-MM-DDTHH:mm:ssZ (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="a101a-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="a101a-202">Pode haver um 30 a 40 segundos de atraso após a criação de um localizador quando ele está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="a101a-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="a101a-203">Esse problema se aplica a URL SAS e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="a101a-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="a101a-204">Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="a101a-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="a101a-205">O exemplo a seguir mostra como criar um localizador URL SAS, conforme definido pela propriedade Type no corpo da solicitação ("1" para um localizador SAS e "2" para um localizador de origem sob demanda).</span><span class="sxs-lookup"><span data-stu-id="a101a-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="a101a-206">A propriedade **Path** retornada contém a URL que você deve usar para carregar seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="a101a-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="a101a-207">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="a101a-208">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-208">**HTTP Response**</span></span>

<span data-ttu-id="a101a-209">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-209">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="a101a-210">Carregar um arquivo em um contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="a101a-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="a101a-211">Depois de definir AccessPolicy e Localizador, o arquivo real é carregado em um contêiner de armazenamento de blobs do Azure usando as APIs REST do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="a101a-212">Você deve carregar os arquivos como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="a101a-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="a101a-213">Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="a101a-214">Você deve adicionar o nome do arquivo para o arquivo que você deseja carregar no valor **Path** do Localizador recebido na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a101a-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="a101a-215">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="a101a-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="a101a-216">.</span><span class="sxs-lookup"><span data-stu-id="a101a-216">.</span></span> <span data-ttu-id="a101a-217">.</span><span class="sxs-lookup"><span data-stu-id="a101a-217">.</span></span> <span data-ttu-id="a101a-218">.</span><span class="sxs-lookup"><span data-stu-id="a101a-218">.</span></span>
>
>

<span data-ttu-id="a101a-219">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a101a-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="a101a-220">Atualizar o AssetFile</span><span class="sxs-lookup"><span data-stu-id="a101a-220">Update the AssetFile</span></span>
<span data-ttu-id="a101a-221">Agora que você carregou o arquivo, atualize as informações de tamanho do FileAsset (e outros).</span><span class="sxs-lookup"><span data-stu-id="a101a-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="a101a-222">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a101a-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="a101a-223">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-223">**HTTP Response**</span></span>

<span data-ttu-id="a101a-224">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="a101a-225">Excluir o AccessPolicy e localizador</span><span class="sxs-lookup"><span data-stu-id="a101a-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="a101a-226">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a101a-227">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-227">**HTTP Response**</span></span>

<span data-ttu-id="a101a-228">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="a101a-229">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="a101a-230">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-230">**HTTP Response**</span></span>

<span data-ttu-id="a101a-231">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a101a-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="a101a-232"><a id="encode"></a>Codificar o arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável</span><span class="sxs-lookup"><span data-stu-id="a101a-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="a101a-233">Após a inserção de Ativos nos Serviços de Mídia, a mídia poderá ser codificada, transmultiplexada, marcada com marca d'água e assim por diante, antes que seja entregue aos clientes.</span><span class="sxs-lookup"><span data-stu-id="a101a-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="a101a-234">Essas atividades são agendadas e executadas em contraste com várias instâncias de função de plano de fundo para garantir a disponibilidade e desempenho elevados.</span><span class="sxs-lookup"><span data-stu-id="a101a-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="a101a-235">Essas atividades são chamadas de Trabalhos, e cada Trabalho é composto por Tarefas atômicas, que fazem o trabalho real no arquivo do Ativo. (Para saber mais, consulte as descrições de [Trabalho](/rest/api/media/services/job), [Tarefa](/rest/api/media/services/task)).</span><span class="sxs-lookup"><span data-stu-id="a101a-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="a101a-236">Como foi mencionado anteriormente, ao trabalhar com os Serviços de Mídia do Azure, um dos cenários mais comuns é fornecer streaming com uma taxa de bits adaptável aos clientes dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="a101a-237">Os Serviços de Mídia podem empacotar dinamicamente um conjunto de arquivos MP4 com taxa de bit adaptável em um dos seguintes formatos: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a101a-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="a101a-238">A seção a seguir mostra como criar um trabalho que contém uma tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="a101a-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="a101a-239">A tarefa especifica a transcodificação do arquivo de mezanino em um conjunto de MP4s de taxa de bits adaptável usando o **Codificador de Mídia Padrão**.</span><span class="sxs-lookup"><span data-stu-id="a101a-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="a101a-240">A seção também mostra como monitorar o progresso de processamento de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a101a-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="a101a-241">Quando o trabalho for concluído, você poderá criar localizadores, que serão necessários para acessar seus ativos.</span><span class="sxs-lookup"><span data-stu-id="a101a-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="a101a-242">Obter um processador de mídia</span><span class="sxs-lookup"><span data-stu-id="a101a-242">Get a media processor</span></span>
<span data-ttu-id="a101a-243">Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="a101a-244">Para a tarefa de codificação mostrada neste tutorial, usaremos o Codificador de Mídia Padrão.</span><span class="sxs-lookup"><span data-stu-id="a101a-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="a101a-245">O código a seguir solicita a ID do codificador.</span><span class="sxs-lookup"><span data-stu-id="a101a-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="a101a-246">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a101a-247">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
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

### <a name="create-a-job"></a><span data-ttu-id="a101a-248">Criar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a101a-248">Create a job</span></span>
<span data-ttu-id="a101a-249">Cada trabalho pode ter uma ou mais tarefas dependendo do tipo de processamento que você deseja realizar.</span><span class="sxs-lookup"><span data-stu-id="a101a-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="a101a-250">Por meio da API REST, você pode criar Trabalhos e as Tarefas relacionadas de uma destas duas maneiras: as Tarefas podem ser definidas embutidas por meio da propriedade de navegação Tarefas nas entidades de Trabalho ou por meio do processamento de lote OData.</span><span class="sxs-lookup"><span data-stu-id="a101a-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="a101a-251">O SDK dos Serviços de Mídia usa o processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="a101a-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="a101a-252">No entanto, para fins de legibilidade dos exemplos de código neste tópico, as tarefas serão definidas em linha.</span><span class="sxs-lookup"><span data-stu-id="a101a-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="a101a-253">Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="a101a-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="a101a-254">O exemplo a seguir mostra como criar e publicar um trabalho com uma tarefa definida para codificar um vídeo em uma determinada resolução e qualidade.</span><span class="sxs-lookup"><span data-stu-id="a101a-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="a101a-255">A seção de documentação a seguir contém a lista de todas as [predefinições de tarefa](http://msdn.microsoft.com/library/mt269960) compatíveis com o processador do Codificador de Mídia Padrão.</span><span class="sxs-lookup"><span data-stu-id="a101a-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="a101a-256">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="a101a-257">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-257">**HTTP Response**</span></span>

<span data-ttu-id="a101a-258">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="a101a-259">Há algumas coisas importantes a observar em qualquer solicitação de trabalho:</span><span class="sxs-lookup"><span data-stu-id="a101a-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="a101a-260">As propriedades TaskBody DEVEM usar XML literal para definir o número de entradas ou os ativos de saída que serão usados pela Tarefa.</span><span class="sxs-lookup"><span data-stu-id="a101a-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="a101a-261">O tópico Tarefa contém a Definição de Esquema XML para o XML.</span><span class="sxs-lookup"><span data-stu-id="a101a-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="a101a-262">Na definição de TaskBody, cada valor interno para <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="a101a-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="a101a-263">Uma tarefa pode ter vários ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="a101a-263">A task can have multiple output assets.</span></span> <span data-ttu-id="a101a-264">Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a101a-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="a101a-265">Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a101a-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="a101a-266">As tarefas não devem formar um ciclo.</span><span class="sxs-lookup"><span data-stu-id="a101a-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="a101a-267">O parâmetro de valor passado para JobInputAsset ou JobOutputAsset representa o valor de índice para um ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="a101a-268">Os ativos reais são definidos nas propriedades de navegação InputMediaAssets e OutputMediaAssets na definição de entidade de tarefa.</span><span class="sxs-lookup"><span data-stu-id="a101a-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="a101a-269">Como os serviços de mídia são baseados no OData v3, os ativos individuais nas coleções de propriedade de navegação InputMediaAssets e OutputMediaAssets são referenciados por meio de um par nome-valor "__metadata : uri".</span><span class="sxs-lookup"><span data-stu-id="a101a-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="a101a-270">Os InputMediaAssets mapeiam para um ou mais ativos que você criou nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="a101a-271">Os OutputMediaAssets são criados pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="a101a-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="a101a-272">Eles não fazem referência a um ativo existente.</span><span class="sxs-lookup"><span data-stu-id="a101a-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="a101a-273">Os OutputMediaAssets podem ser nomeados usando o atributo assetName.</span><span class="sxs-lookup"><span data-stu-id="a101a-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="a101a-274">Se esse atributo não estiver presente, então o nome do OutputMediaAsset será tudo o que é o valor de texto interno do elemento <outputAsset> com um sufixo do valor do nome do trabalho ou o valor da ID de trabalho (no caso em que a propriedade Nome não esteja definida).</span><span class="sxs-lookup"><span data-stu-id="a101a-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="a101a-275">Por exemplo, se você definir um valor de assetName como "Amostra", a propriedade Nome de OutputMediaAsset deve ser definida como "Amostra".</span><span class="sxs-lookup"><span data-stu-id="a101a-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="a101a-276">No entanto, se você não definiu um valor para assetName, mas definiu o nome do trabalho como "NewJob", o nome do OutputMediaAsset poderia ser "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="a101a-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="a101a-277">O exemplo a seguir mostra como definir o atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="a101a-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="a101a-278">Para habilitar o encadeamento de tarefas:</span><span class="sxs-lookup"><span data-stu-id="a101a-278">To enable task chaining:</span></span>

  * <span data-ttu-id="a101a-279">Um trabalho deve ter, pelo menos, duas tarefas</span><span class="sxs-lookup"><span data-stu-id="a101a-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="a101a-280">Deve haver pelo menos uma tarefa cujas entradas são a saída de outra tarefa no trabalho.</span><span class="sxs-lookup"><span data-stu-id="a101a-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="a101a-281">Para saber mais, consulte [Criar um trabalho de codificação com a API REST dos Serviços de Mídia.](media-services-rest-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="a101a-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="a101a-282">Monitorar o progresso de processamento</span><span class="sxs-lookup"><span data-stu-id="a101a-282">Monitor Processing Progress</span></span>
<span data-ttu-id="a101a-283">Você pode recuperar o status do trabalho, usando a propriedade State, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="a101a-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="a101a-284">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="a101a-285">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-285">**HTTP Response**</span></span>

<span data-ttu-id="a101a-286">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="a101a-287">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a101a-287">Cancel a job</span></span>
<span data-ttu-id="a101a-288">Os serviços de mídia permitem cancelar trabalhos em execução com a função CancelJob.</span><span class="sxs-lookup"><span data-stu-id="a101a-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="a101a-289">Esta chamada retornará um código de erro 400 se você tentar cancelar um Trabalho quando seu estado estiver definido como Cancelado, Cancelando, Erro ou Concluído.</span><span class="sxs-lookup"><span data-stu-id="a101a-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="a101a-290">O exemplo a seguir mostra como chamar a função CancelJob.</span><span class="sxs-lookup"><span data-stu-id="a101a-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="a101a-291">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="a101a-292">Se tiver êxito, uma resposta de código 204 é retornada sem corpo de mensagem.</span><span class="sxs-lookup"><span data-stu-id="a101a-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="a101a-293">Você deve codificar a URL da ID do trabalho (normalmente nb:jid:UUID: algumvalor) ao passá-la como um parâmetro para CancelJob.</span><span class="sxs-lookup"><span data-stu-id="a101a-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="a101a-294">Obtenha o ativo de saída</span><span class="sxs-lookup"><span data-stu-id="a101a-294">Get the output asset</span></span>
<span data-ttu-id="a101a-295">O código a seguir mostra como solicitar a ID do ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="a101a-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="a101a-296">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a101a-297">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a101a-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="a101a-298"><a id="publish_get_urls"></a>Publicar o ativo e obter URLs de download progressivo e streaming com API REST</span><span class="sxs-lookup"><span data-stu-id="a101a-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="a101a-299">Para transmitir ou baixar um ativo, primeiro você precisa "publicá-lo" criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="a101a-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="a101a-300">Os localizadores fornecem acesso aos arquivos contidos no ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="a101a-301">Os Serviços de Mídia oferecem suporte a dois tipos de localizador: OnDemandOrigin, usados para transmitir mídia por streaming (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e SAS (Assinatura de Acesso), usados para baixar arquivos de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="a101a-302">Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="a101a-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="a101a-303">Depois de criar os localizadores, você pode criar as URLs usadas para transmitir ou baixar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="a101a-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="a101a-304">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="a101a-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a101a-305">Para iniciar seu conteúdo de streaming e tirar proveito do empacotamento dinâmico e da criptografia dinâmica, o ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar em estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="a101a-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="a101a-306">Uma URL de streaming para Smooth Streaming tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a101a-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="a101a-307">Uma URL de streaming para HLS tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a101a-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="a101a-308">Uma URL de streaming para MPEG DASH tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a101a-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="a101a-309">Uma URL SAS usada para baixar arquivos tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a101a-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="a101a-310">Esta seção mostra como executar as seguintes tarefas necessárias para "publicar" seus ativos.</span><span class="sxs-lookup"><span data-stu-id="a101a-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="a101a-311">Criando o AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="a101a-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="a101a-312">Criando uma URL SAS para download de conteúdo</span><span class="sxs-lookup"><span data-stu-id="a101a-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="a101a-313">Criando uma URL de origem para conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="a101a-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="a101a-314">Criando o AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="a101a-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="a101a-315">Antes de baixar ou realizar streaming de qualquer conteúdo de mídia primeiro defina um AccessPolicy com permissões de leitura e crie a entidade do localizador apropriada que especifica o tipo de mecanismo de entrega que você deseja habilitar para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="a101a-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="a101a-316">Para saber mais sobre as propriedades disponíveis, consulte [Propriedades da entidade AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="a101a-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="a101a-317">O exemplo a seguir mostra como especificar o AccessPolicy para permissões de leitura para um determinado ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="a101a-318">Se tiver êxito, um código de sucesso 201 é retornado descrevendo a entidade AccessPolicy que você criou.</span><span class="sxs-lookup"><span data-stu-id="a101a-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="a101a-319">Em seguida, você usará a ID do AccessPolicy com a ID do Ativo que contém o arquivo que você deseja fornecer (como um ativo de saída) para criar a entidade do Localizador.</span><span class="sxs-lookup"><span data-stu-id="a101a-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="a101a-320">Esse fluxo de trabalho básico é o mesmo utilizado para carregar um arquivo ao ingerir um ativo (como foi discutido neste tópico).</span><span class="sxs-lookup"><span data-stu-id="a101a-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="a101a-321">Além disso, como o carregamento de arquivos, se você (ou seus clientes) precisarem acessar os arquivos imediatamente, defina o valor StartTime para cinco minutos antes da hora atual</span><span class="sxs-lookup"><span data-stu-id="a101a-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="a101a-322">Essa ação é necessária porque pode haver uma defasagem horária entre o cliente e os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="a101a-323">O valor de StartTime deve estar no seguinte formato de DateTime: AAAA-MM-DDTHH:mm:ssZ (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="a101a-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="a101a-324">Criando uma URL SAS para download de conteúdo</span><span class="sxs-lookup"><span data-stu-id="a101a-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="a101a-325">O código a seguir mostra como obter uma URL que pode ser usada para baixar um arquivo de mídia criado e carregado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a101a-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="a101a-326">O AccessPolicy tem o conjunto de permissões de leitura e o caminho do localizador se refere a uma URL de download SAS.</span><span class="sxs-lookup"><span data-stu-id="a101a-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="a101a-327">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="a101a-328">A propriedade **Path** retornada contém a URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="a101a-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="a101a-329">Se você baixar o conteúdo de armazenamento criptografado, deverá manualmente descriptografá-lo antes de renderizá-lo ou usar o MediaProcessor de descriptografia de armazenamento em uma tarefa de processamento para arquivos processados de saída de modo transparente para um OutputAsset e, em seguida, fazer o download deste ativo.</span><span class="sxs-lookup"><span data-stu-id="a101a-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="a101a-330">Para saber mais sobre processamento, consulte Criar um trabalho de codificação com a API REST dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a101a-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="a101a-331">Além disso, os localizadores URL SAS não podem ser atualizados depois que eles foram criados.</span><span class="sxs-lookup"><span data-stu-id="a101a-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="a101a-332">Por exemplo, você não pode reutilizar o mesmo localizador com um valor StartTime atualizado.</span><span class="sxs-lookup"><span data-stu-id="a101a-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="a101a-333">Isso é devido ao modo como as URLs SAS são criadas.</span><span class="sxs-lookup"><span data-stu-id="a101a-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="a101a-334">Se você quiser acessar um ativo para baixar após um localizador ter expirado, você deve criar um novo com um novo StartTime.</span><span class="sxs-lookup"><span data-stu-id="a101a-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="a101a-335">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="a101a-335">Download files</span></span>
<span data-ttu-id="a101a-336">Depois de definir AccessPolicy e localizador, você pode baixar arquivos usando as APIs de REST do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a101a-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="a101a-337">Você deve adicionar o nome do arquivo para o arquivo que você deseja carregar no valor de **Path** do Localizador recebido na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a101a-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="a101a-338">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="a101a-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="a101a-339">.</span><span class="sxs-lookup"><span data-stu-id="a101a-339">.</span></span> <span data-ttu-id="a101a-340">.</span><span class="sxs-lookup"><span data-stu-id="a101a-340">.</span></span> <span data-ttu-id="a101a-341">.</span><span class="sxs-lookup"><span data-stu-id="a101a-341">.</span></span>
>
>

<span data-ttu-id="a101a-342">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a101a-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="a101a-343">Como resultado do trabalho de codificação que você executou anteriormente (codificação no conjunto de MP4 adaptável), você tem vários arquivos MP4 que pode baixar progressivo.</span><span class="sxs-lookup"><span data-stu-id="a101a-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="a101a-344">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a101a-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="a101a-345">Criando uma URL de streaming para conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="a101a-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="a101a-346">O código a seguir mostra como criar um localizador de URL de streaming:</span><span class="sxs-lookup"><span data-stu-id="a101a-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="a101a-347">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="a101a-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="a101a-348">Para transmitir uma URL de origem de Smooth Streaming em um reprodutor de mídia de streaming, você deve acrescentar a propriedade do Caminho com o nome do arquivo manifesto do Smooth Streaming, seguido de "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a101a-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="a101a-349">Para transmitir HLS, anexe (format=m3u8-aapl) após o "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a101a-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="a101a-350">Para transmitir MPEG DASH, anexe (format=mpd-time-csf) após o "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a101a-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="a101a-351"><a id="play"></a>Reproduzir o conteúdo</span><span class="sxs-lookup"><span data-stu-id="a101a-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="a101a-352">Para o fluxo de vídeo, use [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a101a-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="a101a-353">Para testar o download progressivo, cole uma URL em um navegador (por exemplo, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="a101a-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="a101a-354">Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a101a-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a101a-355">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a101a-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
