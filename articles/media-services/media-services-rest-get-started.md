---
title: "aaaGet iniciado com o fornecimento de conteúdo sob demanda usando REST | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação da implementação de um aplicativo de entrega de conteúdo na demanda com os serviços de mídia do Azure usando a API REST."
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
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="bbd32-103">Introdução ao fornecimento de conteúdo sob demanda usando a REST</span><span class="sxs-lookup"><span data-stu-id="bbd32-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="bbd32-104">Este guia de início rápido o guiará durante as etapas de saudação da implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) usando as APIs de REST de serviços de mídia do Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="bbd32-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="bbd32-105">tutorial de Olá apresenta o fluxo de trabalho de serviços de mídia básico hello e objetos de programação mais comuns hello e tarefas necessárias para o desenvolvimento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="bbd32-106">Na conclusão de saudação do tutorial Olá, você será capaz de toostream ou baixar progressivamente um arquivo de mídia de exemplo que você carregado, codificado e baixado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="bbd32-107">Hello imagem a seguir mostra alguns dos objetos hello mais comumente usada ao desenvolver aplicativos VoD em modelo de mídia serviços OData hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="bbd32-108">Clique em Olá imagem tooview-tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="bbd32-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bbd32-109">Prerequisites</span></span>
<span data-ttu-id="bbd32-110">Hello seguintes pré-requisitos são necessário toostart desenvolver com os serviços de mídia com APIs REST.</span><span class="sxs-lookup"><span data-stu-id="bbd32-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="bbd32-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd32-111">An Azure account.</span></span> <span data-ttu-id="bbd32-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbd32-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bbd32-113">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-113">A Media Services account.</span></span> <span data-ttu-id="bbd32-114">toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bbd32-115">Compreensão de como toodevelop com a API de REST de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="bbd32-116">Para saber mais, consulte [Visão Geral da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="bbd32-117">Um aplicativo de sua escolha que pode enviar solicitações e respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="bbd32-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="bbd32-118">Este tutorial usa o [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="bbd32-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="bbd32-119">Olá tarefas a seguir é mostrado neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="bbd32-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="bbd32-120">Inicie o streaming de ponto de extremidade (usando Olá portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="bbd32-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="bbd32-121">Conecte-se toohello conta de serviços de mídia com a API REST.</span><span class="sxs-lookup"><span data-stu-id="bbd32-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="bbd32-122">Criar um novo ativo e carregar um arquivo de vídeo com a API REST.</span><span class="sxs-lookup"><span data-stu-id="bbd32-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="bbd32-123">Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável com a API REST.</span><span class="sxs-lookup"><span data-stu-id="bbd32-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="bbd32-124">Publica ativo hello e get streaming e URLs de download progressivo com a API REST.</span><span class="sxs-lookup"><span data-stu-id="bbd32-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="bbd32-125">Reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="bbd32-126">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="bbd32-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="bbd32-127">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="bbd32-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="bbd32-128">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="bbd32-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="bbd32-129">Para obter detalhes sobre as entidades do REST do AMS usadas neste tópico, consulte [Referência de API REST dos Serviços de Mídia do Azure](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="bbd32-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="bbd32-130">Além disso, consulte [Conceitos dos Serviços de Mídia do Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="bbd32-131">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="bbd32-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="bbd32-132">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="bbd32-133">Iniciar o streaming de pontos de extremidade usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bbd32-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="bbd32-134">Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="bbd32-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="bbd32-135">Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="bbd32-136">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="bbd32-137">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="bbd32-138">toostart Olá ponto de extremidade de streaming, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="bbd32-139">Faça logon em Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bbd32-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bbd32-140">Na janela de configurações de saudação, clique em pontos de extremidade de Streaming.</span><span class="sxs-lookup"><span data-stu-id="bbd32-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="bbd32-141">Clique em padrão Olá ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="bbd32-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="bbd32-142">saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="bbd32-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="bbd32-143">Clique o ícone de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="bbd32-144">Clique em Olá toosave de botão de salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="bbd32-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="bbd32-145"><a id="connect"></a>Conecte-se a conta de serviços de mídia toohello com a API REST</span><span class="sxs-lookup"><span data-stu-id="bbd32-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="bbd32-146">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="bbd32-147">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bbd32-148">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="bbd32-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="bbd32-149">Por exemplo, se depois de tentar tooconnect, você obteve seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bbd32-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="bbd32-150">Você deve publicar seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="bbd32-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="bbd32-151"><a id="upload"></a>Criar um novo ativo e carregar um arquivo de vídeo com a API REST</span><span class="sxs-lookup"><span data-stu-id="bbd32-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="bbd32-152">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="bbd32-153">Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Quando arquivos Olá são carregados em Olá ativo, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="bbd32-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="bbd32-154">Um dos valores de saudação que você tenha tooprovide ao criar um ativo é opções de criação de ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="bbd32-155">Olá **opções** propriedade é um valor de enumeração que descreve as opções de criptografia de saudação um ativo pode ser criado com.</span><span class="sxs-lookup"><span data-stu-id="bbd32-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="bbd32-156">Um valor válido é um dos valores de saudação da lista Olá abaixo, não uma combinação de valores da lista:</span><span class="sxs-lookup"><span data-stu-id="bbd32-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="bbd32-157">**Nenhuma** = **0** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="bbd32-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="bbd32-158">Ao usar essa opção, seu conteúdo não é protegido quando está em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbd32-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="bbd32-159">Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="bbd32-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="bbd32-160">**StorageEncrypted** = **1** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="bbd32-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="bbd32-161">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="bbd32-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="bbd32-162">caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.</span><span class="sxs-lookup"><span data-stu-id="bbd32-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="bbd32-163">**CommonEncryptionProtected** = **2** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="bbd32-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="bbd32-164">**EnvelopeEncryptionProtected** = **4** – use esta opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="bbd32-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="bbd32-165">arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="bbd32-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="bbd32-166">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="bbd32-166">Create an asset</span></span>
<span data-ttu-id="bbd32-167">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada.</span><span class="sxs-lookup"><span data-stu-id="bbd32-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="bbd32-168">Olá API REST, criando um ativo requer o envio de POSTAGEM solicitar serviços tooMedia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="bbd32-169">Olá mostrado no exemplo a seguir como toocreate um ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="bbd32-170">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-170">**HTTP Request**</span></span>

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


<span data-ttu-id="bbd32-171">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-171">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-172">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="bbd32-173">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="bbd32-173">Create an AssetFile</span></span>
<span data-ttu-id="bbd32-174">Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="bbd32-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="bbd32-175">Um arquivo de ativo está sempre associado a um ativo, e um ativo pode conter um ou vários AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="bbd32-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="bbd32-176">tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="bbd32-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="bbd32-177">Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usar Olá **mesclar** Olá tooupdate de solicitação HTTP AssetFile com informações sobre o arquivo de mídia (conforme mostrado posteriormente no tópico Olá).</span><span class="sxs-lookup"><span data-stu-id="bbd32-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="bbd32-178">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-178">**HTTP Request**</span></span>

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


<span data-ttu-id="bbd32-179">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="bbd32-180">Criando Olá AccessPolicy com permissão de gravação</span><span class="sxs-lookup"><span data-stu-id="bbd32-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="bbd32-181">Antes de carregar todos os arquivos no armazenamento de blob, defina acesso Olá direitos de política para gravar tooan ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="bbd32-182">Definir toodo que, após uma solicitação HTTP toohello entidade AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="bbd32-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="bbd32-183">Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta.</span><span class="sxs-lookup"><span data-stu-id="bbd32-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="bbd32-184">Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="bbd32-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="bbd32-185">Olá mostrado no exemplo a seguir como toocreate um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="bbd32-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="bbd32-186">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-186">**HTTP Request**</span></span>

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

<span data-ttu-id="bbd32-187">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-187">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-188">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="bbd32-189">Obter URL de carregamento de saudação</span><span class="sxs-lookup"><span data-stu-id="bbd32-189">Get hello Upload URL</span></span>

<span data-ttu-id="bbd32-190">tooreceive Olá URL de carregamento real, crie um localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="bbd32-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="bbd32-191">Os localizadores definem a hora de início da saudação e o tipo de ponto de extremidade de conexão para clientes que deseja tooaccess arquivos em um ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="bbd32-192">Você pode criar várias entidades de localizador para um cliente AccessPolicy e ativos par toohandle diferente determinado solicitações e necessidades.</span><span class="sxs-lookup"><span data-stu-id="bbd32-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="bbd32-193">Cada um destes localizadores usa o valor de StartTime hello mais valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá período que uma URL pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="bbd32-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="bbd32-194">Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="bbd32-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="bbd32-195">Uma URL SAS tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="bbd32-196">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="bbd32-196">Some considerations apply:</span></span>

* <span data-ttu-id="bbd32-197">Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="bbd32-198">Para saber mais, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="bbd32-198">For more information, see Locator.</span></span>
* <span data-ttu-id="bbd32-199">Se precisar tooupload seus arquivos imediatamente, você deve definir seu minutos de toofive valor StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="bbd32-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="bbd32-200">Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="bbd32-201">Além disso, o valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="bbd32-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="bbd32-202">Pode haver um 30 a 40 segundos atrasar após um localizador de criação toowhen está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="bbd32-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="bbd32-203">Esse problema se aplica a tooboth URL SAS e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="bbd32-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="bbd32-204">Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="bbd32-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="bbd32-205">saudação de exemplo a seguir mostra como toocreate um localizador URL SAS, conforme definido pelo Olá propriedade Type no corpo da solicitação hello ("1" para um localizador SAS) e "2" para um localizador de origem sob demanda.</span><span class="sxs-lookup"><span data-stu-id="bbd32-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="bbd32-206">Olá **caminho** propriedade retornada contém Olá URL que você deve usar tooupload seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="bbd32-207">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-207">**HTTP Request**</span></span>

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


<span data-ttu-id="bbd32-208">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-208">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-209">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="bbd32-210">Carregar um arquivo em um contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="bbd32-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="bbd32-211">Depois que você tiver hello AccessPolicy e conjunto de localizador, real do arquivo hello é carregado tooan contêiner de armazenamento de BLOBs do Azure usando Olá APIs de REST do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd32-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="bbd32-212">Você deve carregar arquivos hello como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="bbd32-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="bbd32-213">Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd32-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="bbd32-214">Você deve adicionar o nome do arquivo hello arquivo hello deseja tooupload toohello localizador **caminho** valor recebido na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="bbd32-215">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="bbd32-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="bbd32-216">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-216">.</span></span> <span data-ttu-id="bbd32-217">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-217">.</span></span> <span data-ttu-id="bbd32-218">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-218">.</span></span>
>
>

<span data-ttu-id="bbd32-219">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="bbd32-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="bbd32-220">Saudação de atualização AssetFile</span><span class="sxs-lookup"><span data-stu-id="bbd32-220">Update hello AssetFile</span></span>
<span data-ttu-id="bbd32-221">Agora que você carregou o arquivo, atualize as informações de FileAsset tamanho (e outros) de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="bbd32-222">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bbd32-222">For example:</span></span>

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


<span data-ttu-id="bbd32-223">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-223">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-224">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="bbd32-225">Excluir hello localizador e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="bbd32-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="bbd32-226">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="bbd32-227">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-227">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-228">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="bbd32-229">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="bbd32-230">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-230">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-231">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="bbd32-232"><a id="encode"></a>Codificar o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável</span><span class="sxs-lookup"><span data-stu-id="bbd32-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="bbd32-233">Após a ingestão de que ativos em serviços de mídia, mídia podem ser codificados, transmultiplexar, marca d'água e assim por diante, antes ele é distribuído tooclients.</span><span class="sxs-lookup"><span data-stu-id="bbd32-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="bbd32-234">Essas atividades são agendadas e executadas várias em segundo plano função instâncias tooensure alto desempenho e disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bbd32-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="bbd32-235">Essas atividades são chamadas de trabalhos e cada trabalho é composto de tarefas atômicas que Olá real trabalho no arquivo de ativo de saudação (para obter mais informações, consulte [trabalho](/rest/api/media/services/job), [tarefa](/rest/api/media/services/task) descrições).</span><span class="sxs-lookup"><span data-stu-id="bbd32-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="bbd32-236">Como mencionado anteriormente, ao trabalhar com o Azure Media Services um dos cenários mais comuns de saudação está entregando tooyour clientes de streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="bbd32-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="bbd32-237">Serviços de mídia pode empacotar dinamicamente um conjunto de arquivos MP4 com taxa de bits adaptável em uma saudação formatos a seguir: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="bbd32-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="bbd32-238">Olá seção a seguir mostra como toocreate um trabalho que contém a codificação de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="bbd32-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="bbd32-239">Olá tarefa Especifica arquivo de mezanino Olá tootranscode em um conjunto de MP4s de taxa de bits adaptável usando **codificador de mídia padrão**.</span><span class="sxs-lookup"><span data-stu-id="bbd32-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="bbd32-240">seção de saudação também mostra como toomonitor Olá andamento do processamento de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bbd32-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="bbd32-241">Quando o trabalho de saudação for concluído, seria capaz de toocreate localizadores que são necessárias tooget acesso tooyour ativos.</span><span class="sxs-lookup"><span data-stu-id="bbd32-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="bbd32-242">Obter um processador de mídia</span><span class="sxs-lookup"><span data-stu-id="bbd32-242">Get a media processor</span></span>
<span data-ttu-id="bbd32-243">Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="bbd32-244">Olá codificação tarefa mostrada neste tutorial, vamos toouse Olá codificador de mídia padrão.</span><span class="sxs-lookup"><span data-stu-id="bbd32-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="bbd32-245">id do codificador de saudação solicitações de código a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="bbd32-246">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="bbd32-247">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="bbd32-248">Criar um trabalho</span><span class="sxs-lookup"><span data-stu-id="bbd32-248">Create a job</span></span>
<span data-ttu-id="bbd32-249">Cada trabalho pode ter um ou mais tarefas dependendo do tipo de saudação de processamento que você deseja tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="bbd32-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="bbd32-250">Por meio de Olá API REST, você pode criar trabalhos e as tarefas relacionadas em uma das duas maneiras: tarefas podem ser definidas embutidas por meio da propriedade de navegação Olá tarefas nas entidades de trabalho ou por meio do processamento de lote do OData.</span><span class="sxs-lookup"><span data-stu-id="bbd32-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="bbd32-251">Olá SDK do Media Services usa processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="bbd32-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="bbd32-252">No entanto, para facilitar a leitura Olá Olá exemplos de código neste tópico, tarefas são definidas embutidas.</span><span class="sxs-lookup"><span data-stu-id="bbd32-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="bbd32-253">Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="bbd32-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="bbd32-254">saudação de exemplo a seguir mostra como toocreate e lançar um trabalho com uma tarefa definir tooencode um vídeo em uma resolução e qualidade específicas.</span><span class="sxs-lookup"><span data-stu-id="bbd32-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="bbd32-255">Olá seção da documentação a seguir contém a lista de saudação de saudação todos os [predefinições de tarefa](http://msdn.microsoft.com/library/mt269960) suportadas pelo codificador de mídia padrão hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="bbd32-256">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-256">**HTTP Request**</span></span>

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

<span data-ttu-id="bbd32-257">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-257">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-258">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="bbd32-259">Há toonote de algumas coisas importantes em qualquer solicitação de trabalho:</span><span class="sxs-lookup"><span data-stu-id="bbd32-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="bbd32-260">Propriedades TaskBody devem usar o número do literal XML toodefine Olá de entrada ou ativos de saída que são usados pela tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="bbd32-261">tópico de tarefa Olá contém hello definição de esquema XML para Olá XML.</span><span class="sxs-lookup"><span data-stu-id="bbd32-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="bbd32-262">Olá definição de TaskBody, valor da cada interna de <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="bbd32-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="bbd32-263">Uma tarefa pode ter vários ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="bbd32-263">A task can have multiple output assets.</span></span> <span data-ttu-id="bbd32-264">Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="bbd32-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="bbd32-265">Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="bbd32-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="bbd32-266">As tarefas não devem formar um ciclo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="bbd32-267">parâmetro de valor de saudação que você passe tooJobInputAsset ou JobOutputAsset representa o valor de índice Olá para um ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="bbd32-268">Olá ativos reais são definidos nas propriedades de navegação InputMediaAssets e OutputMediaAssets de saudação em Olá definição de entidade de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bbd32-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd32-269">Porque os serviços de mídia é desenvolvido no OData v3, Olá ativos individuais nas InputMediaAssets e OutputMediaAssets coleções de propriedades de navegação são referenciadas por meio de um " Metadata: uri" par nome-valor.</span><span class="sxs-lookup"><span data-stu-id="bbd32-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="bbd32-270">Os InputMediaAssets mapeiam tooone ou mais ativos que você criou nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="bbd32-271">Os OutputMediaAssets são criados pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="bbd32-272">Eles não fazem referência a um ativo existente.</span><span class="sxs-lookup"><span data-stu-id="bbd32-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="bbd32-273">Os OutputMediaAssets podem ser nomeados usando o atributo assetName hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="bbd32-274">Se esse atributo não estiver presente, o nome de saudação do hello OutputMediaAsset é qualquer valor de texto interno de saudação do hello <outputAsset> elemento for com um sufixo do valor do nome do trabalho hello, ou valor de Id do trabalho hello (no caso de Olá onde a propriedade de nome de saudação não está definida).</span><span class="sxs-lookup"><span data-stu-id="bbd32-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="bbd32-275">Por exemplo, se você definir um valor para assetName muito "Sample", em seguida, Olá propriedade Name de OutputMediaAsset será definida muito "Sample".</span><span class="sxs-lookup"><span data-stu-id="bbd32-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="bbd32-276">No entanto, se você não definiu um valor para assetName, mas definido o nome do trabalho Olá muito "Novotrabalho" e, em seguida, Olá Name de OutputMediaAsset seria "JobOutputAsset (valor) novotrabalho".</span><span class="sxs-lookup"><span data-stu-id="bbd32-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="bbd32-277">saudação de exemplo a seguir mostra como tooset Olá atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="bbd32-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="bbd32-278">tooenable encadeamento de tarefas:</span><span class="sxs-lookup"><span data-stu-id="bbd32-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="bbd32-279">Um trabalho deve ter, pelo menos, duas tarefas</span><span class="sxs-lookup"><span data-stu-id="bbd32-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="bbd32-280">Deve haver pelo menos uma tarefa cuja entrada é saída de outra tarefa no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="bbd32-281">Para obter mais informações, consulte [criar um trabalho de codificação com hello API REST do Media Services](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="bbd32-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="bbd32-282">Monitorar o progresso de processamento</span><span class="sxs-lookup"><span data-stu-id="bbd32-282">Monitor Processing Progress</span></span>
<span data-ttu-id="bbd32-283">Você pode recuperar o status do trabalho hello usando a propriedade de estado hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbd32-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="bbd32-284">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="bbd32-285">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-285">**HTTP Response**</span></span>

<span data-ttu-id="bbd32-286">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="bbd32-287">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="bbd32-287">Cancel a job</span></span>
<span data-ttu-id="bbd32-288">Serviços de mídia permitem toocancel trabalhos em execução por meio de saudação função CancelJob.</span><span class="sxs-lookup"><span data-stu-id="bbd32-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="bbd32-289">Essa chamada retornará um código de 400 erro se você tentar toocancel um trabalho quando seu estado é cancelado, cancelando, erro ou concluído.</span><span class="sxs-lookup"><span data-stu-id="bbd32-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="bbd32-290">Olá mostrado no exemplo a seguir como toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="bbd32-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="bbd32-291">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="bbd32-292">Se tiver êxito, uma resposta de código 204 é retornada sem corpo de mensagem.</span><span class="sxs-lookup"><span data-stu-id="bbd32-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd32-293">Você deve codificar URL id do trabalho hello (normalmente nb:jid:UUID: algumvalor) ao passá-lo como um parâmetro tooCancelJob.</span><span class="sxs-lookup"><span data-stu-id="bbd32-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="bbd32-294">Obter Olá ativo de saída</span><span class="sxs-lookup"><span data-stu-id="bbd32-294">Get hello output asset</span></span>
<span data-ttu-id="bbd32-295">Olá código a seguir mostra como toorequest Olá saída ID de ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="bbd32-296">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="bbd32-297">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd32-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="bbd32-298"><a id="publish_get_urls"></a>Publicar ativo hello e get streaming e URLs de download progressivo com a API REST</span><span class="sxs-lookup"><span data-stu-id="bbd32-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="bbd32-299">toostream ou baixar um ativo, você primeiro precisa muito "Publicar"-lo criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="bbd32-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="bbd32-300">Os localizadores fornecem acesso toofiles contidos em Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="bbd32-301">Serviços de mídia oferece suporte a dois tipos de localizadores: OnDemandOrigin localizadores, mídia toostream usado (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e localizadores da assinatura de acesso (SAS), usados arquivos de mídia toodownload.</span><span class="sxs-lookup"><span data-stu-id="bbd32-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="bbd32-302">Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="bbd32-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="bbd32-303">Depois de criar localizadores hello, você pode criar URLs Olá toostream usado ou baixar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="bbd32-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="bbd32-304">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="bbd32-305">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="bbd32-306">Uma URL de streaming para Smooth Streaming tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="bbd32-307">Uma URL de streaming para HLS tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="bbd32-308">Uma URL de streaming MPEG DASH tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="bbd32-309">Arquivos de toodownload uma URL SAS usada tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd32-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="bbd32-310">Esta seção mostra como a seguir Olá tooperform as tarefas necessárias muito "Publicar" seus ativos.</span><span class="sxs-lookup"><span data-stu-id="bbd32-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="bbd32-311">Criando Olá AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="bbd32-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="bbd32-312">Criando uma URL SAS para download de conteúdo</span><span class="sxs-lookup"><span data-stu-id="bbd32-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="bbd32-313">Criando uma URL de origem para conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="bbd32-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="bbd32-314">Criando Olá AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="bbd32-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="bbd32-315">Antes de baixar ou qualquer conteúdo de mídia de streaming, primeiro defina um AccessPolicy com permissões de leitura e criar hello entidade do localizador apropriada que especifica o tipo de saudação do mecanismo de entrega, você deseja tooenable para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="bbd32-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="bbd32-316">Para obter mais informações sobre as propriedades de saudação disponíveis, consulte [propriedades da entidade AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="bbd32-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="bbd32-317">saudação de exemplo a seguir mostra como toospecify Olá AccessPolicy para permissões de leitura para um determinado ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="bbd32-318">Se for bem-sucedido, um código de 201 sucesso é retornado descrevendo a entidade AccessPolicy Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="bbd32-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="bbd32-319">Você, em seguida, usar Olá Id de AccessPolicy com hello Id do ativo de saudação que contém o arquivo hello deseja toodeliver (como um ativo de saída) toocreate Olá localizador entidade.</span><span class="sxs-lookup"><span data-stu-id="bbd32-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd32-320">Este fluxo de trabalho básico é Olá mesmo como carregar um arquivo quando uma ingestão de ativos (conforme foi discutido neste tópico).</span><span class="sxs-lookup"><span data-stu-id="bbd32-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="bbd32-321">Além disso, como carregar arquivos, se você (ou seus clientes) precisam tooaccess arquivos imediatamente, defina seu minutos de toofive valor StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="bbd32-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="bbd32-322">Essa ação é necessária porque pode haver relógio defasagem horária entre o cliente hello e serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="bbd32-323">Olá valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="bbd32-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="bbd32-324">Criando uma URL SAS para download de conteúdo</span><span class="sxs-lookup"><span data-stu-id="bbd32-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="bbd32-325">saudação de código a seguir mostra como a tooget uma URL que pode ser usado toodownload um arquivo de mídia criado e carregado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bbd32-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="bbd32-326">Olá AccessPolicy tem o conjunto de permissões de leitura e caminho do localizador Olá refere-se a URL de download do tooa SAS.</span><span class="sxs-lookup"><span data-stu-id="bbd32-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="bbd32-327">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="bbd32-328">Olá retornado **caminho** propriedade contém Olá URL SAS.</span><span class="sxs-lookup"><span data-stu-id="bbd32-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd32-329">Se você baixar o conteúdo de armazenamento criptografado, deve manualmente descriptografá-lo antes de renderizá-lo ou usar Olá MediaProcessor de descriptografia de armazenamento em um toooutput de tarefa de processamento processou arquivos no hello limpar tooan OutputAsset e, em seguida, faça o download deste ativo.</span><span class="sxs-lookup"><span data-stu-id="bbd32-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="bbd32-330">Para obter mais informações sobre o processamento, consulte Criar um trabalho de codificação com hello API de REST de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bbd32-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="bbd32-331">Além disso, os localizadores URL SAS não podem ser atualizados depois que eles foram criados.</span><span class="sxs-lookup"><span data-stu-id="bbd32-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="bbd32-332">Por exemplo, não é possível reutilizar Olá mesmo localizador com um valor StartTime atualizado.</span><span class="sxs-lookup"><span data-stu-id="bbd32-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="bbd32-333">Isso é devido à forma como o hello URLs SAS são criadas.</span><span class="sxs-lookup"><span data-stu-id="bbd32-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="bbd32-334">Se você quiser tooaccess um ativo para download após um localizador tiver expirado, você deve criar um novo com um novo StartTime.</span><span class="sxs-lookup"><span data-stu-id="bbd32-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="bbd32-335">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="bbd32-335">Download files</span></span>
<span data-ttu-id="bbd32-336">Depois que você tiver hello AccessPolicy e conjunto de localizador, você pode baixar arquivos usando Olá APIs de REST do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd32-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="bbd32-337">Você deve adicionar o nome do arquivo hello arquivo hello deseja toodownload toohello localizador **caminho** valor recebido na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="bbd32-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="bbd32-338">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="bbd32-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="bbd32-339">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-339">.</span></span> <span data-ttu-id="bbd32-340">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-340">.</span></span> <span data-ttu-id="bbd32-341">.</span><span class="sxs-lookup"><span data-stu-id="bbd32-341">.</span></span>
>
>

<span data-ttu-id="bbd32-342">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="bbd32-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="bbd32-343">Como resultado da saudação codificação trabalho executado anteriormente (codificação em conjunto de MP4 adaptável), você tem vários arquivos MP4 que você pode baixar progressivamente.</span><span class="sxs-lookup"><span data-stu-id="bbd32-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="bbd32-344">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bbd32-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="bbd32-345">Criando uma URL de streaming para conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="bbd32-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="bbd32-346">Olá mostrado no código a seguir como toocreate um localizador URL de streaming:</span><span class="sxs-lookup"><span data-stu-id="bbd32-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="bbd32-347">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="bbd32-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="bbd32-348">toostream uma URL de origem Smooth Streaming em um reprodutor de mídia de streaming, você deve acrescentar a propriedade Path Olá com nome Olá Olá Smooth Streaming manifesto do arquivo, seguido de "/manifest".</span><span class="sxs-lookup"><span data-stu-id="bbd32-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="bbd32-349">toostream HLS, acrescente (format = m3u8-aapl) após hello "/manifest".</span><span class="sxs-lookup"><span data-stu-id="bbd32-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="bbd32-350">toostream MPEG DASH, acrescente (formato = mpd-tempo-csf) após hello "/manifest".</span><span class="sxs-lookup"><span data-stu-id="bbd32-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="bbd32-351"><a id="play"></a>Reproduzir o conteúdo</span><span class="sxs-lookup"><span data-stu-id="bbd32-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="bbd32-352">toostream vídeo, você use [Player de serviços de mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="bbd32-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="bbd32-353">tootest progressivo baixar, cole uma URL em um navegador (por exemplo, Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="bbd32-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="bbd32-354">Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bbd32-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bbd32-355">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="bbd32-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
