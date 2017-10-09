---
title: "arquivos de aaaUpload em uma conta de serviços de mídia usando REST | Microsoft Docs"
description: "Saiba como tooget do conteúdo de mídia nos serviços de mídia criando e carregando ativos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="49c77-103">Carregar arquivos em uma conta dos Serviços de Mídia usando o REST</span><span class="sxs-lookup"><span data-stu-id="49c77-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49c77-104">.NET</span><span class="sxs-lookup"><span data-stu-id="49c77-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="49c77-105">REST</span><span class="sxs-lookup"><span data-stu-id="49c77-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="49c77-106">Portal</span><span class="sxs-lookup"><span data-stu-id="49c77-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="49c77-107">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="49c77-108">Olá [ativo](https://docs.microsoft.com/rest/api/media/operations/asset) entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Quando arquivos Olá são carregados em Olá ativo, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="49c77-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="49c77-109">Olá considerações a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="49c77-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="49c77-110">Serviços de mídia usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem.</span><span class="sxs-lookup"><span data-stu-id="49c77-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="49c77-111">Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="49c77-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="49c77-112">Além disso, só pode haver um '.' para a extensão de nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="49c77-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="49c77-113">comprimento de saudação do nome de saudação não deve ser maior do que 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="49c77-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="49c77-114">Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="49c77-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="49c77-115">Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="49c77-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="49c77-116">fluxo de trabalho básico para carregar ativos Olá é dividido em Olá seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c77-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="49c77-117">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="49c77-117">Create an Asset</span></span>
* <span data-ttu-id="49c77-118">Criptografar um ativo (opcional)</span><span class="sxs-lookup"><span data-stu-id="49c77-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="49c77-119">Carregar um armazenamento de tooblob do arquivo</span><span class="sxs-lookup"><span data-stu-id="49c77-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="49c77-120">AMS também permite que você ativos tooupload em massa.</span><span class="sxs-lookup"><span data-stu-id="49c77-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="49c77-121">Para saber mais, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) seção.</span><span class="sxs-lookup"><span data-stu-id="49c77-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="49c77-122">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="49c77-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="49c77-123">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="49c77-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="49c77-124">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="49c77-124">Connect tooMedia Services</span></span>

<span data-ttu-id="49c77-125">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="49c77-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="49c77-126">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="49c77-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="49c77-127">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="49c77-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="49c77-128">Carregar ativos</span><span class="sxs-lookup"><span data-stu-id="49c77-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="49c77-129">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="49c77-129">Create an asset</span></span>

<span data-ttu-id="49c77-130">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada.</span><span class="sxs-lookup"><span data-stu-id="49c77-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="49c77-131">Olá API REST, criando um ativo requer o envio de POSTAGEM solicitar serviços tooMedia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="49c77-132">Uma das propriedades de saudação que você pode especificar quando a criação de um ativo é **opções**.</span><span class="sxs-lookup"><span data-stu-id="49c77-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="49c77-133">**Opções de** é um valor de enumeração que descreve as opções de criptografia de saudação um ativo pode ser criado com.</span><span class="sxs-lookup"><span data-stu-id="49c77-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="49c77-134">Um valor válido é um dos valores de saudação da lista da saudação abaixo, não uma combinação de valores.</span><span class="sxs-lookup"><span data-stu-id="49c77-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="49c77-135">**Nenhuma** = **0**: nenhuma criptografia será usada.</span><span class="sxs-lookup"><span data-stu-id="49c77-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="49c77-136">Este é o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-136">This is hello default value.</span></span> <span data-ttu-id="49c77-137">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49c77-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="49c77-138">Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="49c77-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="49c77-139">**StorageEncrypted** = **1**: Especifique se você deseja para sua toobe arquivos criptografado com criptografia AES-256 bits para carregamento e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49c77-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="49c77-140">Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="49c77-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="49c77-141">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="49c77-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="49c77-142">**CommonEncryptionProtected** = **2**: especifique se você estiver carregando arquivos protegidos com um método de criptografia comum (por exemplo, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="49c77-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="49c77-143">**EnvelopeEncryptionProtected** = **4**: especifique se você estiver carregando HLS criptografado com arquivos AES.</span><span class="sxs-lookup"><span data-stu-id="49c77-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="49c77-144">Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="49c77-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="49c77-145">Se o ativo for usar criptografia, você deve criar um **ContentKey** e vinculá-lo ativo tooyour conforme descrito no tópico a seguir de saudação:[como toocreate um ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="49c77-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="49c77-146">Observe que, depois de carregar arquivos de saudação em ativo hello, você precisa tooupdate propriedades de criptografia de saudação em hello **AssetFile** entidade com valores hello obtidos durante a saudação **ativo** criptografia.</span><span class="sxs-lookup"><span data-stu-id="49c77-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="49c77-147">Fazer isso usando Olá **mesclar** solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="49c77-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="49c77-148">Olá mostrado no exemplo a seguir como toocreate um ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="49c77-149">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="49c77-150">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-150">**HTTP Response**</span></span>

<span data-ttu-id="49c77-151">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="49c77-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="49c77-152">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="49c77-152">Create an AssetFile</span></span>
<span data-ttu-id="49c77-153">Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="49c77-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="49c77-154">Um arquivo de ativo está sempre associado a um ativo e um ativo pode conter um ou vários arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="49c77-155">tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="49c77-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="49c77-156">Observe que Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="49c77-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="49c77-157">instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.</span><span class="sxs-lookup"><span data-stu-id="49c77-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="49c77-158">Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usará Olá **mesclar** Olá tooupdate de solicitação HTTP AssetFile com informações sobre o arquivo de mídia (conforme mostrado posteriormente no tópico Olá).</span><span class="sxs-lookup"><span data-stu-id="49c77-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="49c77-159">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="49c77-160">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="49c77-161">Criando Olá AccessPolicy com permissão de gravação.</span><span class="sxs-lookup"><span data-stu-id="49c77-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="49c77-162">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="49c77-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="49c77-163">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="49c77-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="49c77-164">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="49c77-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="49c77-165">Antes de carregar todos os arquivos no armazenamento de blob, defina acesso Olá direitos de política para gravar tooan ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="49c77-166">Definir toodo que, após uma solicitação HTTP toohello entidade AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="49c77-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="49c77-167">Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta.</span><span class="sxs-lookup"><span data-stu-id="49c77-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="49c77-168">Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="49c77-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="49c77-169">Olá mostrado no exemplo a seguir como toocreate um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="49c77-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="49c77-170">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="49c77-171">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="49c77-172">Obter URL de carregamento de saudação</span><span class="sxs-lookup"><span data-stu-id="49c77-172">Get hello Upload URL</span></span>
<span data-ttu-id="49c77-173">tooreceive Olá URL de carregamento real, crie um localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="49c77-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="49c77-174">Os localizadores definem a hora de início da saudação e o tipo de ponto de extremidade de conexão para clientes que deseja tooaccess arquivos em um ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="49c77-175">Você pode criar várias entidades de localizador para um cliente AccessPolicy e ativos par toohandle diferente determinado solicitações e necessidades.</span><span class="sxs-lookup"><span data-stu-id="49c77-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="49c77-176">Cada um destes localizadores usa o valor de StartTime hello mais valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá período uma URL pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="49c77-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="49c77-177">Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="49c77-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="49c77-178">Uma URL SAS tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c77-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="49c77-179">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="49c77-179">Some considerations apply:</span></span>

* <span data-ttu-id="49c77-180">Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="49c77-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="49c77-181">Para saber mais, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="49c77-181">For more information, see Locator.</span></span>
* <span data-ttu-id="49c77-182">Se precisar tooupload seus arquivos imediatamente, você deve definir seu minutos de toofive valor StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="49c77-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="49c77-183">Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="49c77-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="49c77-184">Além disso, o valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="49c77-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="49c77-185">Pode haver um 30 a 40 segundos atrasar após um localizador de criação toowhen está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="49c77-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="49c77-186">Esse problema se aplica a tooboth URL SAS e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="49c77-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="49c77-187">saudação de exemplo a seguir mostra como toocreate um localizador URL SAS, conforme definido pelo Olá propriedade Type no corpo da solicitação hello ("1" para um localizador SAS) e "2" para um localizador de origem sob demanda.</span><span class="sxs-lookup"><span data-stu-id="49c77-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="49c77-188">Olá **caminho** propriedade retornada contém Olá URL que você deve usar tooupload seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="49c77-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="49c77-189">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="49c77-190">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-190">**HTTP Response**</span></span>

<span data-ttu-id="49c77-191">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="49c77-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="49c77-192">Carregar um arquivo em um contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="49c77-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="49c77-193">Depois que você tiver hello AccessPolicy e conjunto de localizador, real do arquivo hello é carregado tooan contêiner de armazenamento de BLOBs do Azure usando Olá APIs de REST do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c77-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="49c77-194">Você deve carregar arquivos hello como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="49c77-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="49c77-195">Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c77-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="49c77-196">Você deve adicionar o nome do arquivo hello arquivo hello deseja tooupload toohello localizador **caminho** valor recebido na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="49c77-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="49c77-197">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="49c77-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="49c77-198">.</span><span class="sxs-lookup"><span data-stu-id="49c77-198">.</span></span> <span data-ttu-id="49c77-199">.</span><span class="sxs-lookup"><span data-stu-id="49c77-199">.</span></span> <span data-ttu-id="49c77-200">.</span><span class="sxs-lookup"><span data-stu-id="49c77-200">.</span></span> 
> 
> 

<span data-ttu-id="49c77-201">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="49c77-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="49c77-202">Saudação de atualização AssetFile</span><span class="sxs-lookup"><span data-stu-id="49c77-202">Update hello AssetFile</span></span>
<span data-ttu-id="49c77-203">Agora que você carregou o arquivo, atualize as informações de FileAsset tamanho (e outros) de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="49c77-204">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="49c77-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="49c77-205">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-205">**HTTP Response**</span></span>

<span data-ttu-id="49c77-206">Se for bem-sucedido, Olá seguinte é retornado: HTTP/1.1 204 sem conteúdo</span><span class="sxs-lookup"><span data-stu-id="49c77-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="49c77-207">Excluir hello localizador e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="49c77-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="49c77-208">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="49c77-209">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-209">**HTTP Response**</span></span>

<span data-ttu-id="49c77-210">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="49c77-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="49c77-211">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="49c77-212">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-212">**HTTP Response**</span></span>

<span data-ttu-id="49c77-213">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="49c77-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="49c77-214"><a id="upload_in_bulk"></a>Carregar ativos em massa</span><span class="sxs-lookup"><span data-stu-id="49c77-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="49c77-215">Criar hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="49c77-215">Create hello IngestManifest</span></span>
<span data-ttu-id="49c77-216">Olá IngestManifest é um contêiner para um conjunto de ativos, arquivos de ativo e as informações de estatísticas que podem ser usado o progresso de saudação toodetermine de ingestão em massa para o conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="49c77-217">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="49c77-218">Criar ativos</span><span class="sxs-lookup"><span data-stu-id="49c77-218">Create assets</span></span>
<span data-ttu-id="49c77-219">Antes de criar hello IngestManifestAsset, você precisa toocreate Olá ativo que será concluído usando a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="49c77-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="49c77-220">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada.</span><span class="sxs-lookup"><span data-stu-id="49c77-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="49c77-221">Em Olá API REST, criar um ativo requer enviar uma solicitação de HTTP POST tooMicrosoft Azure Media Services e fazer qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação. Neste exemplo, Olá ativo é criado usando Olá storageencryption (1) opção incluída no corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="49c77-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="49c77-222">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="49c77-223">Criar hello IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="49c77-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="49c77-224">Os IngestManifestAssets representam os Ativos em um IngestManifest usados com a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="49c77-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="49c77-225">Olá basicamente manifesto de toohello link Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="49c77-226">Serviços de mídia do Azure observa internamente para carregamento do arquivo hello com base em associados de coleção de IngestManifestFiles toohello IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="49c77-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="49c77-227">Depois que esses arquivos são carregados, o ativo de saudação é concluído.</span><span class="sxs-lookup"><span data-stu-id="49c77-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="49c77-228">Você pode criar um novo IngestManifestAsset com uma solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="49c77-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="49c77-229">No corpo da solicitação de hello, incluem hello Id do IngestManifest e Olá Id do ativo que Olá IngestManifestAsset deve vincular para ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="49c77-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="49c77-230">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="49c77-231">Criar hello IngestManifestFiles para cada ativo</span><span class="sxs-lookup"><span data-stu-id="49c77-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="49c77-232">Um IngestManifestFile representa um objeto de blob de vídeo ou de áudio real que será carregado como parte da ingestão em massa de um ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="49c77-233">Propriedades não são necessárias, a menos que o ativo de saudação é usando uma opção de criptografia relacionadas à criptografia.</span><span class="sxs-lookup"><span data-stu-id="49c77-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="49c77-234">exemplo Hello usado nesta seção demonstra a criação de um IngestManifestFile que usa StorageEncryption para Olá que ativo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49c77-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="49c77-235">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="49c77-236">Carregar arquivos de saudação tooBlob armazenamento</span><span class="sxs-lookup"><span data-stu-id="49c77-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="49c77-237">Você pode usar qualquer aplicativo cliente de alta velocidade capaz de carregar o contêiner de armazenamento do blob da arquivos para ativo Olá toohello Uri fornecido pelo Olá propriedade BlobStorageUriForUpload de saudação IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="49c77-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="49c77-238">Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="49c77-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="49c77-239">Monitorar o progresso de ingestão em massa</span><span class="sxs-lookup"><span data-stu-id="49c77-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="49c77-240">Você pode monitorar o progresso de saudação de operações para um IngestManifest sondando a propriedade de estatísticas de saudação do hello IngestManifest de ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="49c77-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="49c77-241">Essa propriedade é um tipo complexo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="49c77-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="49c77-242">Olá toopoll propriedade Statistics, envie uma solicitação HTTP GET passando Olá ID IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="49c77-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="49c77-243">Criar ContentKeys usadas para criptografia</span><span class="sxs-lookup"><span data-stu-id="49c77-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="49c77-244">Se o ativo for usar criptografia, você deve criar hello ContentKey toobe usado para criptografia antes de criar hello arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="49c77-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="49c77-245">Para criptografia de armazenamento, hello propriedades a seguir devem ser incluídas no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="49c77-246">Propriedade do corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="49c77-246">Request body property</span></span> | <span data-ttu-id="49c77-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="49c77-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49c77-248">ID</span><span class="sxs-lookup"><span data-stu-id="49c77-248">Id</span></span> |<span data-ttu-id="49c77-249">Olá Id de ContentKey que podemos gerar nós usando Olá após formatar, "NB:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="49c77-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="49c77-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="49c77-250">ContentKeyType</span></span> |<span data-ttu-id="49c77-251">Isso é o tipo de chave de conteúdo do hello como um inteiro para esta chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="49c77-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="49c77-252">Passamos o valor de saudação 1 para criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49c77-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="49c77-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="49c77-253">EncryptedContentKey</span></span> |<span data-ttu-id="49c77-254">Criamos um novo valor de chave de conteúdo, que é um valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="49c77-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="49c77-255">chave de saudação é criptografada usando o certificado x. 509 de criptografia de armazenamento de saudação que recuperamos de serviços de mídia do Microsoft Azure, executando uma solicitação HTTP GET para hello GetProtectionKeyId e GetProtectionKey métodos.</span><span class="sxs-lookup"><span data-stu-id="49c77-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="49c77-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="49c77-256">ProtectionKeyId</span></span> |<span data-ttu-id="49c77-257">Isso é Olá id de chave de proteção para o certificado x. 509 de criptografia de armazenamento de saudação que foi usado tooencrypt a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="49c77-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="49c77-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="49c77-258">ProtectionKeyType</span></span> |<span data-ttu-id="49c77-259">Este é o tipo de criptografia de saudação para chave de proteção de saudação que foi usado tooencrypt chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="49c77-260">Em nosso exemplo, este valor será StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="49c77-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="49c77-261">Soma de verificação</span><span class="sxs-lookup"><span data-stu-id="49c77-261">Checksum</span></span> |<span data-ttu-id="49c77-262">Olá MD5 soma de verificação calculada para a chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="49c77-263">Ela é computada criptografando a Id do conteúdo Olá com chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c77-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="49c77-264">o código de exemplo Hello demonstra como toocalculate Olá soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="49c77-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="49c77-265">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="49c77-266">Saudação de link ContentKey toohello ativo</span><span class="sxs-lookup"><span data-stu-id="49c77-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="49c77-267">Olá ContentKey é associado tooone ou mais ativos enviando uma solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="49c77-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="49c77-268">Olá, solicitação a seguir é um ativo de exemplo exemplo toolink Olá exemplo ContentKey toohello por ID.</span><span class="sxs-lookup"><span data-stu-id="49c77-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="49c77-269">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="49c77-270">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="49c77-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="49c77-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49c77-271">Next steps</span></span>

<span data-ttu-id="49c77-272">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="49c77-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="49c77-273">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="49c77-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="49c77-274">Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="49c77-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="49c77-275">Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="49c77-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="49c77-276">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="49c77-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="49c77-277">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="49c77-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

