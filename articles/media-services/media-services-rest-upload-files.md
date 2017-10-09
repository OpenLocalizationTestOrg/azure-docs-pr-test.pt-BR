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
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Carregar arquivos em uma conta dos Serviços de Mídia usando o REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo. Olá [ativo](https://docs.microsoft.com/rest/api/media/operations/asset) entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Quando arquivos Olá são carregados em Olá ativo, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming. 

> [!NOTE]
> Olá considerações a seguir se aplicam:
> 
> * Serviços de mídia usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem. Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, só pode haver um '.' para a extensão de nome de arquivo hello.
> * comprimento de saudação do nome de saudação não deve ser maior do que 260 caracteres.
> * Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia. Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.
> 

fluxo de trabalho básico para carregar ativos Olá é dividido em Olá seções a seguir:

* Criar um ativo
* Criptografar um ativo (opcional)
* Carregar um armazenamento de tooblob do arquivo

AMS também permite que você ativos tooupload em massa. Para saber mais, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) seção.

> [!NOTE]
> Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>Conectar os serviços de tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

## <a name="upload-assets"></a>Carregar ativos

### <a name="create-an-asset"></a>Criar um ativo

Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada. Olá API REST, criando um ativo requer o envio de POSTAGEM solicitar serviços tooMedia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação.

Uma das propriedades de saudação que você pode especificar quando a criação de um ativo é **opções**. **Opções de** é um valor de enumeração que descreve as opções de criptografia de saudação um ativo pode ser criado com. Um valor válido é um dos valores de saudação da lista da saudação abaixo, não uma combinação de valores. 

* **Nenhuma** = **0**: nenhuma criptografia será usada. Este é o valor padrão de saudação. Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.
    Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção. 
* **StorageEncrypted** = **1**: Especifique se você deseja para sua toobe arquivos criptografado com criptografia AES-256 bits para carregamento e armazenamento.
  
    Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos. Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2**: especifique se você estiver carregando arquivos protegidos com um método de criptografia comum (por exemplo, PlayReady). 
* **EnvelopeEncryptionProtected** = **4**: especifique se você estiver carregando HLS criptografado com arquivos AES. Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.

> [!NOTE]
> Se o ativo for usar criptografia, você deve criar um **ContentKey** e vinculá-lo ativo tooyour conforme descrito no tópico a seguir de saudação:[como toocreate um ContentKey](media-services-rest-create-contentkey.md). Observe que, depois de carregar arquivos de saudação em ativo hello, você precisa tooupdate propriedades de criptografia de saudação em hello **AssetFile** entidade com valores hello obtidos durante a saudação **ativo** criptografia. Fazer isso usando Olá **mesclar** solicitação HTTP. 
> 
> 

Olá mostrado no exemplo a seguir como toocreate um ativo.

**Solicitação HTTP**

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

**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

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

### <a name="create-an-assetfile"></a>Criar um AssetFile
Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob. Um arquivo de ativo está sempre associado a um ativo e um ativo pode conter um ou vários arquivos de ativo. tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.

Observe que Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos. instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.

Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usará Olá **mesclar** Olá tooupdate de solicitação HTTP AssetFile com informações sobre o arquivo de mídia (conforme mostrado posteriormente no tópico Olá). 

**Solicitação HTTP**

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

**Resposta HTTP**

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a>Criando Olá AccessPolicy com permissão de gravação.

>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Antes de carregar todos os arquivos no armazenamento de blob, defina acesso Olá direitos de política para gravar tooan ativo. Definir toodo que, após uma solicitação HTTP toohello entidade AccessPolicies. Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta. Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Olá mostrado no exemplo a seguir como toocreate um AccessPolicy:

**Solicitação HTTP**

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

**Solicitação HTTP**

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

### <a name="get-hello-upload-url"></a>Obter URL de carregamento de saudação
tooreceive Olá URL de carregamento real, crie um localizador SAS. Os localizadores definem a hora de início da saudação e o tipo de ponto de extremidade de conexão para clientes que deseja tooaccess arquivos em um ativo. Você pode criar várias entidades de localizador para um cliente AccessPolicy e ativos par toohandle diferente determinado solicitações e necessidades. Cada um destes localizadores usa o valor de StartTime hello mais valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá período uma URL pode ser usada. Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).

Uma URL SAS tem Olá formato a seguir:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Algumas considerações se aplicam:

* Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo. Para saber mais, consulte Localizador.
* Se precisar tooupload seus arquivos imediatamente, você deve definir seu minutos de toofive valor StartTime antes Olá hora atual. Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia. Além disso, o valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").    
* Pode haver um 30 a 40 segundos atrasar após um localizador de criação toowhen está disponível para uso. Esse problema se aplica a tooboth URL SAS e localizadores de origem.

saudação de exemplo a seguir mostra como toocreate um localizador URL SAS, conforme definido pelo Olá propriedade Type no corpo da solicitação hello ("1" para um localizador SAS) e "2" para um localizador de origem sob demanda. Olá **caminho** propriedade retornada contém Olá URL que você deve usar tooupload seu arquivo.

**Solicitação HTTP**

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

**Resposta HTTP**

Se for bem-sucedido, Olá resposta a seguir será retornada:

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

### <a name="upload-a-file-into-a-blob-storage-container"></a>Carregar um arquivo em um contêiner de armazenamento de blobs
Depois que você tiver hello AccessPolicy e conjunto de localizador, real do arquivo hello é carregado tooan contêiner de armazenamento de BLOBs do Azure usando Olá APIs de REST do armazenamento do Azure. Você deve carregar arquivos hello como blobs de blocos. Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.  

> [!NOTE]
> Você deve adicionar o nome do arquivo hello arquivo hello deseja tooupload toohello localizador **caminho** valor recebido na seção anterior hello. Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Saudação de atualização AssetFile
Agora que você carregou o arquivo, atualize as informações de FileAsset tamanho (e outros) de saudação. Por exemplo:

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


**Resposta HTTP**

Se for bem-sucedido, Olá seguinte é retornado: HTTP/1.1 204 sem conteúdo

### <a name="delete-hello-locator-and-accesspolicy"></a>Excluir hello localizador e AccessPolicy
**Solicitação HTTP**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

    HTTP/1.1 204 No Content 
    ...

**Solicitação HTTP**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Carregar ativos em massa
### <a name="create-hello-ingestmanifest"></a>Criar hello IngestManifest
Olá IngestManifest é um contêiner para um conjunto de ativos, arquivos de ativo e as informações de estatísticas que podem ser usado o progresso de saudação toodetermine de ingestão em massa para o conjunto de saudação.

**Solicitação HTTP**

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

### <a name="create-assets"></a>Criar ativos
Antes de criar hello IngestManifestAsset, você precisa toocreate Olá ativo que será concluído usando a ingestão em massa. Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada. Em Olá API REST, criar um ativo requer enviar uma solicitação de HTTP POST tooMicrosoft Azure Media Services e fazer qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação. Neste exemplo, Olá ativo é criado usando Olá storageencryption (1) opção incluída no corpo da solicitação hello.

**Resposta HTTP**

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

### <a name="create-hello-ingestmanifestassets"></a>Criar hello IngestManifestAssets
Os IngestManifestAssets representam os Ativos em um IngestManifest usados com a ingestão em massa. Olá basicamente manifesto de toohello link Olá ativo. Serviços de mídia do Azure observa internamente para carregamento do arquivo hello com base em associados de coleção de IngestManifestFiles toohello IngestManifestAsset. Depois que esses arquivos são carregados, o ativo de saudação é concluído. Você pode criar um novo IngestManifestAsset com uma solicitação HTTP POST. No corpo da solicitação de hello, incluem hello Id do IngestManifest e Olá Id do ativo que Olá IngestManifestAsset deve vincular para ingestão em massa.

**Resposta HTTP**

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


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Criar hello IngestManifestFiles para cada ativo
Um IngestManifestFile representa um objeto de blob de vídeo ou de áudio real que será carregado como parte da ingestão em massa de um ativo. Propriedades não são necessárias, a menos que o ativo de saudação é usando uma opção de criptografia relacionadas à criptografia. exemplo Hello usado nesta seção demonstra a criação de um IngestManifestFile que usa StorageEncryption para Olá que ativo criado anteriormente.

**Resposta HTTP**

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

### <a name="upload-hello-files-tooblob-storage"></a>Carregar arquivos de saudação tooBlob armazenamento
Você pode usar qualquer aplicativo cliente de alta velocidade capaz de carregar o contêiner de armazenamento do blob da arquivos para ativo Olá toohello Uri fornecido pelo Olá propriedade BlobStorageUriForUpload de saudação IngestManifest. Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=272001).

### <a name="monitor-bulk-ingest-progress"></a>Monitorar o progresso de ingestão em massa
Você pode monitorar o progresso de saudação de operações para um IngestManifest sondando a propriedade de estatísticas de saudação do hello IngestManifest de ingestão em massa. Essa propriedade é um tipo complexo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). Olá toopoll propriedade Statistics, envie uma solicitação HTTP GET passando Olá ID IngestManifest.

## <a name="create-contentkeys-used-for-encryption"></a>Criar ContentKeys usadas para criptografia
Se o ativo for usar criptografia, você deve criar hello ContentKey toobe usado para criptografia antes de criar hello arquivos de ativo. Para criptografia de armazenamento, hello propriedades a seguir devem ser incluídas no corpo da solicitação de saudação.

| Propriedade do corpo da solicitação | Descrição |
| --- | --- |
| ID |Olá Id de ContentKey que podemos gerar nós usando Olá após formatar, "NB:<NEW GUID>". |
| ContentKeyType |Isso é o tipo de chave de conteúdo do hello como um inteiro para esta chave de conteúdo. Passamos o valor de saudação 1 para criptografia de armazenamento. |
| EncryptedContentKey |Criamos um novo valor de chave de conteúdo, que é um valor de 256 bits (32 bytes). chave de saudação é criptografada usando o certificado x. 509 de criptografia de armazenamento de saudação que recuperamos de serviços de mídia do Microsoft Azure, executando uma solicitação HTTP GET para hello GetProtectionKeyId e GetProtectionKey métodos. |
| ProtectionKeyId |Isso é Olá id de chave de proteção para o certificado x. 509 de criptografia de armazenamento de saudação que foi usado tooencrypt a chave de conteúdo. |
| ProtectionKeyType |Este é o tipo de criptografia de saudação para chave de proteção de saudação que foi usado tooencrypt chave de conteúdo de saudação. Em nosso exemplo, este valor será StorageEncryption(1). |
| Soma de verificação |Olá MD5 soma de verificação calculada para a chave de conteúdo de saudação. Ela é computada criptografando a Id do conteúdo Olá com chave de conteúdo de saudação. o código de exemplo Hello demonstra como toocalculate Olá soma de verificação. |

**Resposta HTTP**

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

### <a name="link-hello-contentkey-toohello-asset"></a>Saudação de link ContentKey toohello ativo
Olá ContentKey é associado tooone ou mais ativos enviando uma solicitação HTTP POST. Olá, solicitação a seguir é um ativo de exemplo exemplo toolink Olá exemplo ContentKey toohello por ID.

**Resposta HTTP**

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

**Resposta HTTP**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Próximas etapas

Agora você pode codificar seus ativos carregados. Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).

Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada. Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

