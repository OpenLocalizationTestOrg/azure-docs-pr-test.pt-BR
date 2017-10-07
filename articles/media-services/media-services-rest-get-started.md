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
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>Introdução ao fornecimento de conteúdo sob demanda usando a REST
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este guia de início rápido o guiará durante as etapas de saudação da implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) usando as APIs de REST de serviços de mídia do Azure (AMS).

tutorial de Olá apresenta o fluxo de trabalho de serviços de mídia básico hello e objetos de programação mais comuns hello e tarefas necessárias para o desenvolvimento de serviços de mídia. Na conclusão de saudação do tutorial Olá, você será capaz de toostream ou baixar progressivamente um arquivo de mídia de exemplo que você carregado, codificado e baixado.

Hello imagem a seguir mostra alguns dos objetos hello mais comumente usada ao desenvolver aplicativos VoD em modelo de mídia serviços OData hello.

Clique em Olá imagem tooview-tamanho máximo.  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>Pré-requisitos
Hello seguintes pré-requisitos são necessário toostart desenvolver com os serviços de mídia com APIs REST.

* Uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Uma conta dos Serviços de Mídia. toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).
* Compreensão de como toodevelop com a API de REST de serviços de mídia. Para saber mais, consulte [Visão Geral da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).
* Um aplicativo de sua escolha que pode enviar solicitações e respostas HTTP. Este tutorial usa o [Fiddler](http://www.telerik.com/download/fiddler).

Olá tarefas a seguir é mostrado neste guia de início rápido.

1. Inicie o streaming de ponto de extremidade (usando Olá portal do Azure).
2. Conecte-se toohello conta de serviços de mídia com a API REST.
3. Criar um novo ativo e carregar um arquivo de vídeo com a API REST.
4. Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável com a API REST.
5. Publica ativo hello e get streaming e URLs de download progressivo com a API REST.
6. Reproduzir o conteúdo.

>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Para obter detalhes sobre as entidades do REST do AMS usadas neste tópico, consulte [Referência de API REST dos Serviços de Mídia do Azure](/rest/api/media/services/azure-media-services-rest-api-reference). Além disso, consulte [Conceitos dos Serviços de Mídia do Azure](media-services-concepts.md).

>[!NOTE]
>Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Iniciar o streaming de pontos de extremidade usando Olá portal do Azure

Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável. Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.

toostart Olá ponto de extremidade de streaming, Olá a seguir:

1. Faça logon em Olá [portal do Azure](https://portal.azure.com/).
2. Na janela de configurações de saudação, clique em pontos de extremidade de Streaming.
3. Clique em padrão Olá ponto de extremidade de streaming.

    saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.

4. Clique o ícone de início de saudação.
5. Clique em Olá toosave de botão de salvar suas alterações.

## <a id="connect"></a>Conecte-se a conta de serviços de mídia toohello com a API REST

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

Por exemplo, se depois de tentar tooconnect, você obteve seguinte hello:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

Você deve publicar seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

## <a id="upload"></a>Criar um novo ativo e carregar um arquivo de vídeo com a API REST

Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo. Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Quando arquivos Olá são carregados em Olá ativo, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.

Um dos valores de saudação que você tenha tooprovide ao criar um ativo é opções de criação de ativo. Olá **opções** propriedade é um valor de enumeração que descreve as opções de criptografia de saudação um ativo pode ser criado com. Um valor válido é um dos valores de saudação da lista Olá abaixo, não uma combinação de valores da lista:

* **Nenhuma** = **0** - nenhuma criptografia é usada. Ao usar essa opção, seu conteúdo não é protegido quando está em trânsito ou em repouso no armazenamento.
    Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.
* **StorageEncrypted** = **1** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso. Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída. caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.
* **CommonEncryptionProtected** = **2** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).
* **EnvelopeEncryptionProtected** = **4** – use esta opção se você estiver carregando HLS criptografado com AES. arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.

### <a name="create-an-asset"></a>Criar um ativo
Um ativo é um contêiner para múltiplos tipos ou conjuntos de objetos nos serviços de mídia, incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada. Olá API REST, criando um ativo requer o envio de POSTAGEM solicitar serviços tooMedia e colocar qualquer informação de propriedade sobre seus ativos no corpo da solicitação de saudação.

Olá mostrado no exemplo a seguir como toocreate um ativo.

**Solicitação HTTP**

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


**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

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

### <a name="create-an-assetfile"></a>Criar um AssetFile
Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob. Um arquivo de ativo está sempre associado a um ativo, e um ativo pode conter um ou vários AssetFiles. tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.

Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usar Olá **mesclar** Olá tooupdate de solicitação HTTP AssetFile com informações sobre o arquivo de mídia (conforme mostrado posteriormente no tópico Olá).

**Solicitação HTTP**

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a>Criando Olá AccessPolicy com permissão de gravação
Antes de carregar todos os arquivos no armazenamento de blob, defina acesso Olá direitos de política para gravar tooan ativo. Definir toodo que, após uma solicitação HTTP toohello entidade AccessPolicies. Defina um valor de DurationInMinutes durante a criação ou você receberá uma mensagem de erro de servidor interno 500 em resposta. Para saber mais sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Olá mostrado no exemplo a seguir como toocreate um AccessPolicy:

**Solicitação HTTP**

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

**Resposta HTTP**

Se for bem-sucedido, Olá resposta a seguir será retornada:

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

### <a name="get-hello-upload-url"></a>Obter URL de carregamento de saudação

tooreceive Olá URL de carregamento real, crie um localizador SAS. Os localizadores definem a hora de início da saudação e o tipo de ponto de extremidade de conexão para clientes que deseja tooaccess arquivos em um ativo. Você pode criar várias entidades de localizador para um cliente AccessPolicy e ativos par toohandle diferente determinado solicitações e necessidades. Cada um destes localizadores usa o valor de StartTime hello mais valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá período que uma URL pode ser usada. Para saber mais, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).

Uma URL SAS tem Olá formato a seguir:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Algumas considerações se aplicam:

* Você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo. Para saber mais, consulte Localizador.
* Se precisar tooupload seus arquivos imediatamente, você deve definir seu minutos de toofive valor StartTime antes Olá hora atual. Isso ocorre porque pode haver uma defasagem horária entre o computador do cliente e os serviços de mídia. Além disso, o valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").    
* Pode haver um 30 a 40 segundos atrasar após um localizador de criação toowhen está disponível para uso. Esse problema se aplica a tooboth URL SAS e localizadores de origem.

Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.

saudação de exemplo a seguir mostra como toocreate um localizador URL SAS, conforme definido pelo Olá propriedade Type no corpo da solicitação hello ("1" para um localizador SAS) e "2" para um localizador de origem sob demanda. Olá **caminho** propriedade retornada contém Olá URL que você deve usar tooupload seu arquivo.

**Solicitação HTTP**

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


**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>Excluir hello localizador e AccessPolicy
**Solicitação HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

    HTTP/1.1 204 No Content
    ...

**Solicitação HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**Resposta HTTP**

Se for bem-sucedido, a seguir Olá será retornada:

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Codificar o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável

Após a ingestão de que ativos em serviços de mídia, mídia podem ser codificados, transmultiplexar, marca d'água e assim por diante, antes ele é distribuído tooclients. Essas atividades são agendadas e executadas várias em segundo plano função instâncias tooensure alto desempenho e disponibilidade. Essas atividades são chamadas de trabalhos e cada trabalho é composto de tarefas atômicas que Olá real trabalho no arquivo de ativo de saudação (para obter mais informações, consulte [trabalho](/rest/api/media/services/job), [tarefa](/rest/api/media/services/task) descrições).

Como mencionado anteriormente, ao trabalhar com o Azure Media Services um dos cenários mais comuns de saudação está entregando tooyour clientes de streaming de taxa de bits adaptável. Serviços de mídia pode empacotar dinamicamente um conjunto de arquivos MP4 com taxa de bits adaptável em uma saudação formatos a seguir: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

Olá seção a seguir mostra como toocreate um trabalho que contém a codificação de uma tarefa. Olá tarefa Especifica arquivo de mezanino Olá tootranscode em um conjunto de MP4s de taxa de bits adaptável usando **codificador de mídia padrão**. seção de saudação também mostra como toomonitor Olá andamento do processamento de trabalho. Quando o trabalho de saudação for concluído, seria capaz de toocreate localizadores que são necessárias tooget acesso tooyour ativos.

### <a name="get-a-media-processor"></a>Obter um processador de mídia
Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia. Olá codificação tarefa mostrada neste tutorial, vamos toouse Olá codificador de mídia padrão.

id do codificador de saudação solicitações de código a seguir de saudação.

**Solicitação HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta HTTP**

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

### <a name="create-a-job"></a>Criar um trabalho
Cada trabalho pode ter um ou mais tarefas dependendo do tipo de saudação de processamento que você deseja tooaccomplish. Por meio de Olá API REST, você pode criar trabalhos e as tarefas relacionadas em uma das duas maneiras: tarefas podem ser definidas embutidas por meio da propriedade de navegação Olá tarefas nas entidades de trabalho ou por meio do processamento de lote do OData. Olá SDK do Media Services usa processamento em lotes. No entanto, para facilitar a leitura Olá Olá exemplos de código neste tópico, tarefas são definidas embutidas. Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

saudação de exemplo a seguir mostra como toocreate e lançar um trabalho com uma tarefa definir tooencode um vídeo em uma resolução e qualidade específicas. Olá seção da documentação a seguir contém a lista de saudação de saudação todos os [predefinições de tarefa](http://msdn.microsoft.com/library/mt269960) suportadas pelo codificador de mídia padrão hello.  

**Solicitação HTTP**

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

**Resposta HTTP**

Se for bem-sucedido, Olá resposta a seguir será retornada:

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


Há toonote de algumas coisas importantes em qualquer solicitação de trabalho:

* Propriedades TaskBody devem usar o número do literal XML toodefine Olá de entrada ou ativos de saída que são usados pela tarefa de saudação. tópico de tarefa Olá contém hello definição de esquema XML para Olá XML.
* Olá definição de TaskBody, valor da cada interna de <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).
* Uma tarefa pode ter vários ativos de saída. Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.
* Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.
* As tarefas não devem formar um ciclo.
* parâmetro de valor de saudação que você passe tooJobInputAsset ou JobOutputAsset representa o valor de índice Olá para um ativo. Olá ativos reais são definidos nas propriedades de navegação InputMediaAssets e OutputMediaAssets de saudação em Olá definição de entidade de trabalho.

> [!NOTE]
> Porque os serviços de mídia é desenvolvido no OData v3, Olá ativos individuais nas InputMediaAssets e OutputMediaAssets coleções de propriedades de navegação são referenciadas por meio de um " Metadata: uri" par nome-valor.
>
>

* Os InputMediaAssets mapeiam tooone ou mais ativos que você criou nos serviços de mídia. Os OutputMediaAssets são criados pelo sistema hello. Eles não fazem referência a um ativo existente.
* Os OutputMediaAssets podem ser nomeados usando o atributo assetName hello. Se esse atributo não estiver presente, o nome de saudação do hello OutputMediaAsset é qualquer valor de texto interno de saudação do hello <outputAsset> elemento for com um sufixo do valor do nome do trabalho hello, ou valor de Id do trabalho hello (no caso de Olá onde a propriedade de nome de saudação não está definida). Por exemplo, se você definir um valor para assetName muito "Sample", em seguida, Olá propriedade Name de OutputMediaAsset será definida muito "Sample". No entanto, se você não definiu um valor para assetName, mas definido o nome do trabalho Olá muito "Novotrabalho" e, em seguida, Olá Name de OutputMediaAsset seria "JobOutputAsset (valor) novotrabalho".

    saudação de exemplo a seguir mostra como tooset Olá atributo assetName:

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* tooenable encadeamento de tarefas:

  * Um trabalho deve ter, pelo menos, duas tarefas
  * Deve haver pelo menos uma tarefa cuja entrada é saída de outra tarefa no trabalho de saudação.

Para obter mais informações, consulte [criar um trabalho de codificação com hello API REST do Media Services](media-services-rest-encode-asset.md).

### <a name="monitor-processing-progress"></a>Monitorar o progresso de processamento
Você pode recuperar o status do trabalho hello usando a propriedade de estado hello, conforme mostrado no exemplo a seguir de saudação.

**Solicitação HTTP**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**Resposta HTTP**

Se for bem-sucedido, Olá resposta a seguir será retornada:

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


### <a name="cancel-a-job"></a>Cancelar um trabalho
Serviços de mídia permitem toocancel trabalhos em execução por meio de saudação função CancelJob. Essa chamada retornará um código de 400 erro se você tentar toocancel um trabalho quando seu estado é cancelado, cancelando, erro ou concluído.

Olá mostrado no exemplo a seguir como toocall CancelJob.

**Solicitação HTTP**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


Se tiver êxito, uma resposta de código 204 é retornada sem corpo de mensagem.

> [!NOTE]
> Você deve codificar URL id do trabalho hello (normalmente nb:jid:UUID: algumvalor) ao passá-lo como um parâmetro tooCancelJob.
>
>

### <a name="get-hello-output-asset"></a>Obter Olá ativo de saída
Olá código a seguir mostra como toorequest Olá saída ID de ativo.

**Solicitação HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta HTTP**

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



## <a id="publish_get_urls"></a>Publicar ativo hello e get streaming e URLs de download progressivo com a API REST

toostream ou baixar um ativo, você primeiro precisa muito "Publicar"-lo criando um localizador. Os localizadores fornecem acesso toofiles contidos em Olá ativo. Serviços de mídia oferece suporte a dois tipos de localizadores: OnDemandOrigin localizadores, mídia toostream usado (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e localizadores da assinatura de acesso (SAS), usados arquivos de mídia toodownload. Para saber mais sobre localizadores SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.

Depois de criar localizadores hello, você pode criar URLs Olá toostream usado ou baixar os arquivos.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.

Uma URL de streaming para Smooth Streaming tem Olá formato a seguir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Uma URL de streaming para HLS tem Olá formato a seguir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Uma URL de streaming MPEG DASH tem Olá formato a seguir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Arquivos de toodownload uma URL SAS usada tem Olá formato a seguir:

    {blob container name}/{asset name}/{file name}/{SAS signature}

Esta seção mostra como a seguir Olá tooperform as tarefas necessárias muito "Publicar" seus ativos.  

* Criando Olá AccessPolicy com permissão de leitura
* Criando uma URL SAS para download de conteúdo
* Criando uma URL de origem para conteúdo de streaming

### <a name="creating-hello-accesspolicy-with-read-permission"></a>Criando Olá AccessPolicy com permissão de leitura
Antes de baixar ou qualquer conteúdo de mídia de streaming, primeiro defina um AccessPolicy com permissões de leitura e criar hello entidade do localizador apropriada que especifica o tipo de saudação do mecanismo de entrega, você deseja tooenable para seus clientes. Para obter mais informações sobre as propriedades de saudação disponíveis, consulte [propriedades da entidade AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).

saudação de exemplo a seguir mostra como toospecify Olá AccessPolicy para permissões de leitura para um determinado ativo.

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

Se for bem-sucedido, um código de 201 sucesso é retornado descrevendo a entidade AccessPolicy Olá que você criou. Você, em seguida, usar Olá Id de AccessPolicy com hello Id do ativo de saudação que contém o arquivo hello deseja toodeliver (como um ativo de saída) toocreate Olá localizador entidade.

> [!NOTE]
> Este fluxo de trabalho básico é Olá mesmo como carregar um arquivo quando uma ingestão de ativos (conforme foi discutido neste tópico). Além disso, como carregar arquivos, se você (ou seus clientes) precisam tooaccess arquivos imediatamente, defina seu minutos de toofive valor StartTime antes Olá hora atual. Essa ação é necessária porque pode haver relógio defasagem horária entre o cliente hello e serviços de mídia. Olá valor StartTime deve estar no hello seguindo o formato de data e hora: AAAA-MM-ddTHH (por exemplo, "2014-05-23T17:53:50Z").
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>Criando uma URL SAS para download de conteúdo
saudação de código a seguir mostra como a tooget uma URL que pode ser usado toodownload um arquivo de mídia criado e carregado anteriormente. Olá AccessPolicy tem o conjunto de permissões de leitura e caminho do localizador Olá refere-se a URL de download do tooa SAS.

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

Se for bem-sucedido, Olá resposta a seguir será retornada:

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


Olá retornado **caminho** propriedade contém Olá URL SAS.

> [!NOTE]
> Se você baixar o conteúdo de armazenamento criptografado, deve manualmente descriptografá-lo antes de renderizá-lo ou usar Olá MediaProcessor de descriptografia de armazenamento em um toooutput de tarefa de processamento processou arquivos no hello limpar tooan OutputAsset e, em seguida, faça o download deste ativo. Para obter mais informações sobre o processamento, consulte Criar um trabalho de codificação com hello API de REST de serviços de mídia. Além disso, os localizadores URL SAS não podem ser atualizados depois que eles foram criados. Por exemplo, não é possível reutilizar Olá mesmo localizador com um valor StartTime atualizado. Isso é devido à forma como o hello URLs SAS são criadas. Se você quiser tooaccess um ativo para download após um localizador tiver expirado, você deve criar um novo com um novo StartTime.
>
>

### <a name="download-files"></a>Baixar arquivos
Depois que você tiver hello AccessPolicy e conjunto de localizador, você pode baixar arquivos usando Olá APIs de REST do armazenamento do Azure.  

> [!NOTE]
> Você deve adicionar o nome do arquivo hello arquivo hello deseja toodownload toohello localizador **caminho** valor recebido na seção anterior hello. Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Para saber mais sobre como trabalhar com blobs de armazenamento do Azure, consulte [API REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

Como resultado da saudação codificação trabalho executado anteriormente (codificação em conjunto de MP4 adaptável), você tem vários arquivos MP4 que você pode baixar progressivamente. Por exemplo:    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>Criando uma URL de streaming para conteúdo de streaming
Olá mostrado no código a seguir como toocreate um localizador URL de streaming:

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

Se for bem-sucedido, Olá resposta a seguir será retornada:

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

toostream uma URL de origem Smooth Streaming em um reprodutor de mídia de streaming, você deve acrescentar a propriedade Path Olá com nome Olá Olá Smooth Streaming manifesto do arquivo, seguido de "/manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

toostream HLS, acrescente (format = m3u8-aapl) após hello "/manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

toostream MPEG DASH, acrescente (formato = mpd-tempo-csf) após hello "/manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>Reproduzir o conteúdo
toostream vídeo, você use [Player de serviços de mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progressivo baixar, cole uma URL em um navegador (por exemplo, Internet Explorer, Chrome, Safari).

## <a name="next-steps-media-services-learning-paths"></a>Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
