---
title: "Carregar arquivos em uma conta dos Serviços de Mídia usando REST | Microsoft Docs"
description: "Saiba como obter o conteúdo de mídia nos serviços de mídia ao criar e carregar ativos."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="bc16b-103">Carregar arquivos em uma conta dos Serviços de Mídia usando o REST</span><span class="sxs-lookup"><span data-stu-id="bc16b-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc16b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="bc16b-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="bc16b-105">REST</span><span class="sxs-lookup"><span data-stu-id="bc16b-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="bc16b-106">Portal</span><span class="sxs-lookup"><span data-stu-id="bc16b-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="bc16b-107">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="bc16b-108">A entidade [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) pode conter vídeo, áudio, imagens, coleções de miniaturas, sequências de texto e arquivos de legendas (e os metadados sobre esses arquivos).  Depois que os arquivos são carregados no ativo, o conteúdo é armazenado com segurança na nuvem para processamento e transmissão adicionais.</span><span class="sxs-lookup"><span data-stu-id="bc16b-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="bc16b-109">As seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="bc16b-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="bc16b-110">Os serviços de mídia usam o valor da propriedade IAssetFile.Name ao construir URLs para o conteúdo de streaming (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem.</span><span class="sxs-lookup"><span data-stu-id="bc16b-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="bc16b-111">O valor da propriedade **Name** não pode ter quaisquer dos seguintes [caracteres reservados para codificação de percentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="bc16b-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="bc16b-112">Além disso, pode haver somente um '.' para a extensão de nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="bc16b-113">O comprimento do nome não deve ser maior do que 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="bc16b-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="bc16b-114">Há um limite no tamanho máximo de arquivo com suporte para o processamento nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="bc16b-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="bc16b-115">Confira [este](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="bc16b-116">O fluxo de trabalho básico para o carregamento de Ativos é dividido nas seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="bc16b-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="bc16b-117">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="bc16b-117">Create an Asset</span></span>
* <span data-ttu-id="bc16b-118">Criptografar um ativo (opcional)</span><span class="sxs-lookup"><span data-stu-id="bc16b-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="bc16b-119">Carregar um arquivo no armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="bc16b-119">Upload a file to blob storage</span></span>

<span data-ttu-id="bc16b-120">O AMS também permite que você carregue ativos em massa.</span><span class="sxs-lookup"><span data-stu-id="bc16b-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="bc16b-121">Para saber mais, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) seção.</span><span class="sxs-lookup"><span data-stu-id="bc16b-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="bc16b-122">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc16b-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="bc16b-123">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bc16b-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="bc16b-124">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bc16b-124">Connect to Media Services</span></span>

<span data-ttu-id="bc16b-125">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bc16b-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="bc16b-126">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bc16b-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bc16b-127">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="bc16b-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="bc16b-128">Carregar ativos</span><span class="sxs-lookup"><span data-stu-id="bc16b-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="bc16b-129">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="bc16b-129">Create an asset</span></span>

<span data-ttu-id="bc16b-130">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada.</span><span class="sxs-lookup"><span data-stu-id="bc16b-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="bc16b-131">Na API REST, criar um ativo requer enviar solicitação POST para serviços de mídia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="bc16b-132">Uma das propriedades que você pode especificar quando criar um ativo está em **Opções**.</span><span class="sxs-lookup"><span data-stu-id="bc16b-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="bc16b-133">**Opções** é um valor de enumeração que descreve as opções de criptografia em que um ativo pode ser criado.</span><span class="sxs-lookup"><span data-stu-id="bc16b-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="bc16b-134">Um valor válido é um dos valores na lista abaixo, não uma combinação de valores.</span><span class="sxs-lookup"><span data-stu-id="bc16b-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="bc16b-135">**Nenhuma** = **0**: nenhuma criptografia será usada.</span><span class="sxs-lookup"><span data-stu-id="bc16b-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="bc16b-136">Esse é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="bc16b-136">This is the default value.</span></span> <span data-ttu-id="bc16b-137">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bc16b-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="bc16b-138">Se você pretende enviar um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="bc16b-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="bc16b-139">**StorageEncrypted** = **1**: especifique se você deseja que os arquivos sejam criptografados com a criptografia AES de 256 bits para carregamento e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bc16b-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="bc16b-140">Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="bc16b-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="bc16b-141">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bc16b-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="bc16b-142">**CommonEncryptionProtected** = **2**: especifique se você estiver carregando arquivos protegidos com um método de criptografia comum (por exemplo, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="bc16b-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="bc16b-143">**EnvelopeEncryptionProtected** = **4**: especifique se você estiver carregando HLS criptografado com arquivos AES.</span><span class="sxs-lookup"><span data-stu-id="bc16b-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="bc16b-144">Observe que os arquivos devem ter sido codificados e criptografados pelo Gerenciador de Transformação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="bc16b-145">Se o ativo for usar criptografia, você deverá criar uma **ContentKey** e vinculá-la ao seu ativo conforme descrito no tópico a seguir:[Como criar uma ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="bc16b-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="bc16b-146">Observe que, depois de carregar os arquivos para o ativo, você precisa atualizar as propriedades de criptografia na entidade **AssetFile** com os valores obtidos durante a criptografia dos **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="bc16b-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="bc16b-147">Faça isso usando a solicitação HTTP **MERGE** .</span><span class="sxs-lookup"><span data-stu-id="bc16b-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="bc16b-148">O exemplo a seguir mostra como criar um ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="bc16b-149">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-149">**HTTP Request**</span></span>

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

<span data-ttu-id="bc16b-150">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-150">**HTTP Response**</span></span>

<span data-ttu-id="bc16b-151">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc16b-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="bc16b-152">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="bc16b-152">Create an AssetFile</span></span>
<span data-ttu-id="bc16b-153">A entidade [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="bc16b-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="bc16b-154">Um arquivo de ativo está sempre associado a um ativo e um ativo pode conter um ou vários arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="bc16b-155">A tarefa do Codificador dos serviços de mídia falha se um objeto de arquivo de ativo não estiver associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="bc16b-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="bc16b-156">Observe que a instância de **AssetFile** e o arquivo de mídia real são dois objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="bc16b-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="bc16b-157">A instância de AssetFile contém metadados sobre o arquivo de mídia, enquanto o arquivo de mídia contém o conteúdo de mídia real.</span><span class="sxs-lookup"><span data-stu-id="bc16b-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="bc16b-158">Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usará a solicitação HTTP **MERGE** para atualizar o AssetFile com informações sobre o arquivo de mídia (como mostrado posteriormente no tópico).</span><span class="sxs-lookup"><span data-stu-id="bc16b-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="bc16b-159">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-159">**HTTP Request**</span></span>

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

<span data-ttu-id="bc16b-160">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="bc16b-161">Criando o AccessPolicy com permissão de gravação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="bc16b-162">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="bc16b-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="bc16b-163">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="bc16b-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="bc16b-164">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="bc16b-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="bc16b-165">Antes de carregar todos os arquivos no armazenamento de blobs, defina os direitos de política de acesso para gravar em um ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="bc16b-166">Para fazer isso, POSTE uma solicitação HTTP para o conjunto de entidade AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="bc16b-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="bc16b-167">Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta.</span><span class="sxs-lookup"><span data-stu-id="bc16b-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="bc16b-168">Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="bc16b-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="bc16b-169">O exemplo a seguir mostra como criar um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="bc16b-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="bc16b-170">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-170">**HTTP Request**</span></span>

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

<span data-ttu-id="bc16b-171">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="bc16b-172">Obter a URL de carregamento</span><span class="sxs-lookup"><span data-stu-id="bc16b-172">Get the Upload URL</span></span>
<span data-ttu-id="bc16b-173">Para receber a URL de carregamento real, crie um localizador de SAS.</span><span class="sxs-lookup"><span data-stu-id="bc16b-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="bc16b-174">Os localizadores definem a hora de início e o tipo de ponto de extremidade de conexão para clientes que desejam acessar arquivos em um ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="bc16b-175">Você pode criar várias entidades de localizador para um determinado par de AccessPolicy e ativos para manipular solicitações e necessidades de clientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="bc16b-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="bc16b-176">Cada um destes localizadores usam o valor StartTime mais o valor de DurationInMinutes do AccessPolicy para determinar quanto tempo uma URL pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="bc16b-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="bc16b-177">Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="bc16b-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="bc16b-178">Uma URL SAS tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="bc16b-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="bc16b-179">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="bc16b-179">Some considerations apply:</span></span>

* <span data-ttu-id="bc16b-180">Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="bc16b-181">Para saber mais, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="bc16b-181">For more information, see Locator.</span></span>
* <span data-ttu-id="bc16b-182">Se você precisar carregar os arquivos imediatamente, você deve definir o valor StartTime como cinco minutos antes da hora atual.</span><span class="sxs-lookup"><span data-stu-id="bc16b-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="bc16b-183">Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bc16b-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="bc16b-184">Além disso, o valor de StartTime deve estar no seguinte formato DateTime: AAAA-MM-DDTHH:mm:ssZ (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="bc16b-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="bc16b-185">Pode haver um 30 a 40 segundos de atraso após a criação de um localizador quando ele está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="bc16b-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="bc16b-186">Esse problema se aplica a URL SAS e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="bc16b-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="bc16b-187">O exemplo a seguir mostra como criar um localizador URL SAS, conforme definido pela propriedade Type no corpo da solicitação ("1" para um localizador SAS e "2" para um localizador de origem sob demanda).</span><span class="sxs-lookup"><span data-stu-id="bc16b-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="bc16b-188">A propriedade **Path** retornada contém a URL que você deve usar para carregar seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="bc16b-189">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-189">**HTTP Request**</span></span>

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

<span data-ttu-id="bc16b-190">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-190">**HTTP Response**</span></span>

<span data-ttu-id="bc16b-191">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="bc16b-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="bc16b-192">Carregar um arquivo em um contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="bc16b-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="bc16b-193">Depois de definir AccessPolicy e localizador, o arquivo real é carregado como um contêiner de armazenamento de blobs do Azure usando as APIs de REST do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc16b-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="bc16b-194">Você deve carregar os arquivos como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="bc16b-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="bc16b-195">Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc16b-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="bc16b-196">Você deve adicionar o nome do arquivo para o arquivo que você deseja carregar no valor **Path** do Localizador recebido na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="bc16b-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="bc16b-197">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="bc16b-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="bc16b-198">.</span><span class="sxs-lookup"><span data-stu-id="bc16b-198">.</span></span> <span data-ttu-id="bc16b-199">.</span><span class="sxs-lookup"><span data-stu-id="bc16b-199">.</span></span> <span data-ttu-id="bc16b-200">.</span><span class="sxs-lookup"><span data-stu-id="bc16b-200">.</span></span> 
> 
> 

<span data-ttu-id="bc16b-201">Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="bc16b-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="bc16b-202">Atualizar o AssetFile</span><span class="sxs-lookup"><span data-stu-id="bc16b-202">Update the AssetFile</span></span>
<span data-ttu-id="bc16b-203">Agora que você carregou o arquivo, atualize as informações de tamanho do FileAsset (e outros).</span><span class="sxs-lookup"><span data-stu-id="bc16b-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="bc16b-204">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bc16b-204">For example:</span></span>

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


<span data-ttu-id="bc16b-205">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-205">**HTTP Response**</span></span>

<span data-ttu-id="bc16b-206">Se for bem-sucedido, será retornado o seguinte: HTTP/1.1 204 No Content</span><span class="sxs-lookup"><span data-stu-id="bc16b-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="bc16b-207">Excluir o AccessPolicy e localizador</span><span class="sxs-lookup"><span data-stu-id="bc16b-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="bc16b-208">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="bc16b-209">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-209">**HTTP Response**</span></span>

<span data-ttu-id="bc16b-210">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc16b-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="bc16b-211">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="bc16b-212">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-212">**HTTP Response**</span></span>

<span data-ttu-id="bc16b-213">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc16b-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="bc16b-214"><a id="upload_in_bulk"></a>Carregar ativos em massa</span><span class="sxs-lookup"><span data-stu-id="bc16b-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="bc16b-215">Criar o IngestManifest</span><span class="sxs-lookup"><span data-stu-id="bc16b-215">Create the IngestManifest</span></span>
<span data-ttu-id="bc16b-216">O IngestManifest é um contêiner para um conjunto de ativos, arquivos de ativo e informações de estatísticas que podem ser usadas para determinar o progresso da ingestão em massa para o conjunto.</span><span class="sxs-lookup"><span data-stu-id="bc16b-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="bc16b-217">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="bc16b-218">Criar ativos</span><span class="sxs-lookup"><span data-stu-id="bc16b-218">Create assets</span></span>
<span data-ttu-id="bc16b-219">Antes de criar o IngestManifestAsset, você precisa criar o Ativo que será concluído usando a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="bc16b-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="bc16b-220">Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda oculta.</span><span class="sxs-lookup"><span data-stu-id="bc16b-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="bc16b-221">Na API REST, a criação de um Ativo exige o envio de uma solicitação HTTP POST para os Serviços de Mídia do Microsoft Azure e a inserção de qualquer informação de propriedade sobre seu ativo no corpo da solicitação. Neste exemplo, o Ativo é criado usando a opção StorageEncrption(1) incluída no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="bc16b-222">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="bc16b-223">Criar os IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="bc16b-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="bc16b-224">Os IngestManifestAssets representam os Ativos em um IngestManifest usados com a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="bc16b-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="bc16b-225">Eles basicamente vinculam o ativo ao manifesto.</span><span class="sxs-lookup"><span data-stu-id="bc16b-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="bc16b-226">Os Serviços de Mídia do Azure analisam internamente o upload do arquivo com base na coleção de IngestManifestFiles associada ao IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="bc16b-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="bc16b-227">Após o carregamento desses arquivos, o ativo será concluído.</span><span class="sxs-lookup"><span data-stu-id="bc16b-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="bc16b-228">Você pode criar um novo IngestManifestAsset com uma solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="bc16b-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="bc16b-229">No corpo da solicitação, inclua a ID do IngestManifest e a ID do ativo que o IngestManifestAsset deve vincular à ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="bc16b-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="bc16b-230">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="bc16b-231">Criar os IngestManifestFiles para cada Ativo</span><span class="sxs-lookup"><span data-stu-id="bc16b-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="bc16b-232">Um IngestManifestFile representa um objeto de blob de vídeo ou de áudio real que será carregado como parte da ingestão em massa de um ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="bc16b-233">As propriedades de criptografia relacionadas não serão necessárias, a menos que o ativo esteja usando uma opção de criptografia.</span><span class="sxs-lookup"><span data-stu-id="bc16b-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="bc16b-234">O exemplo usado nesta seção demonstra a criação de um IngestManifestFile que usa StorageEncryption para o Ativo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bc16b-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="bc16b-235">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="bc16b-236">Carregar os arquivos no Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="bc16b-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="bc16b-237">Você pode usar qualquer aplicativo cliente de alta velocidade capaz de carregar os arquivos de ativo no URI do contêiner de armazenamento de blobs fornecido pela propriedade BlobStorageUriForUpload do IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="bc16b-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="bc16b-238">Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="bc16b-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="bc16b-239">Monitorar o progresso de ingestão em massa</span><span class="sxs-lookup"><span data-stu-id="bc16b-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="bc16b-240">Você pode determinar o progresso de operações de ingestão em massa para um IngestManifest sondando a propriedade Statistics do IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="bc16b-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="bc16b-241">Essa propriedade é um tipo complexo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="bc16b-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="bc16b-242">Para sondar a propriedade Statistics, envie uma solicitação HTTP GET passando a ID do IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="bc16b-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="bc16b-243">Criar ContentKeys usadas para criptografia</span><span class="sxs-lookup"><span data-stu-id="bc16b-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="bc16b-244">Se o ativo for usar criptografia, será necessário criar o ContentKey a ser usado para a criptografia antes de criar os arquivos do ativo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="bc16b-245">Na criptografia de armazenamento, as propriedades a seguir devem ser incluídas no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="bc16b-246">Propriedade do corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="bc16b-246">Request body property</span></span> | <span data-ttu-id="bc16b-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="bc16b-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc16b-248">ID</span><span class="sxs-lookup"><span data-stu-id="bc16b-248">Id</span></span> |<span data-ttu-id="bc16b-249">A ID de ContentKey que nós mesmos geramos usando o seguinte formato, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="bc16b-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="bc16b-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="bc16b-250">ContentKeyType</span></span> |<span data-ttu-id="bc16b-251">Esse é o tipo de chave de conteúdo, como um inteiro para esta chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="bc16b-252">Passamos o valor 1 para a criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bc16b-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="bc16b-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="bc16b-253">EncryptedContentKey</span></span> |<span data-ttu-id="bc16b-254">Criamos um novo valor de chave de conteúdo, que é um valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="bc16b-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="bc16b-255">A chave é criptografada usando o certificado X.509 de criptografia de armazenamento que recuperamos dos Serviços de Mídia do Microsoft Azure por meio da execução de uma solicitação HTTP GET para os métodos GetProtectionKeyId e GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="bc16b-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="bc16b-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="bc16b-256">ProtectionKeyId</span></span> |<span data-ttu-id="bc16b-257">Essa é a ID da chave de proteção para o certificado X.509 de criptografia de armazenamento usado para criptografar nossa chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="bc16b-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="bc16b-258">ProtectionKeyType</span></span> |<span data-ttu-id="bc16b-259">Esse é o tipo de criptografia para a chave de proteção usada para criptografar a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="bc16b-260">Em nosso exemplo, este valor será StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="bc16b-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="bc16b-261">Soma de verificação</span><span class="sxs-lookup"><span data-stu-id="bc16b-261">Checksum</span></span> |<span data-ttu-id="bc16b-262">A soma de verificação calculada por MD5 para a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="bc16b-263">Ela é calculada pela criptografia da ID de conteúdo com a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bc16b-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="bc16b-264">O exemplo de código demonstra como calcular a soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="bc16b-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="bc16b-265">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="bc16b-266">Vincular o ContentKey ao Ativo</span><span class="sxs-lookup"><span data-stu-id="bc16b-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="bc16b-267">O ContentKey é associado a um ou mais ativos enviando uma solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="bc16b-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="bc16b-268">A solicitação a seguir é um exemplo de vinculação do exemplo de ContentKey ao exemplo de ativo por meio da ID.</span><span class="sxs-lookup"><span data-stu-id="bc16b-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="bc16b-269">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-269">**HTTP Response**</span></span>

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

<span data-ttu-id="bc16b-270">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="bc16b-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="bc16b-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc16b-271">Next steps</span></span>

<span data-ttu-id="bc16b-272">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="bc16b-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="bc16b-273">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="bc16b-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="bc16b-274">Você também pode usar as Azure Functions para disparar um trabalho de codificação baseado em um arquivo que chega no contêiner configurado.</span><span class="sxs-lookup"><span data-stu-id="bc16b-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="bc16b-275">Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="bc16b-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bc16b-276">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bc16b-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bc16b-277">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="bc16b-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

