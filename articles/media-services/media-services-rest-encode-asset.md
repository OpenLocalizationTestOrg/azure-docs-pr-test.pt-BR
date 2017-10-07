---
title: "aaaHow tooencode um ativo do Azure usando o codificador de mídia padrão | Microsoft Docs"
description: "Saiba como toouse codificador de mídia padrão tooencode mídia de conteúdo nos serviços de mídia do Azure. Exemplos de código usam a API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Como tooencode um ativo usando o codificador de mídia padrão
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Visão geral
toodeliver vídeo digital pela Olá da Internet, você deve compactar mídia hello. Arquivos de vídeo digital são grandes e podem ser muito grande toodeliver via Olá da Internet, ou para toodisplay de dispositivos de seus clientes corretamente. Codificação é o processo de saudação de compactação de vídeo e áudio para que os clientes possam exibir sua mídia.

Trabalhos de codificação são uma das operações de processamento mais comuns Olá nos serviços de mídia do Azure. Criar arquivos de mídia de tooconvert trabalhos codificação de um tooanother de codificação. Ao codificar, você pode usar o codificador interno de serviços de mídia de saudação (padrão de codificador de mídia). Você também pode usar um codificador fornecido por um parceiro dos Serviços de Mídia. Codificadores de terceiros estão disponíveis por meio de saudação do Azure Marketplace. Você pode especificar os detalhes de saudação de trabalhos de codificação usando cadeias de caracteres predefinidas para o seu codificador ou usando arquivos de configuração predefinidos. toosee Olá tipos de predefinições disponíveis, consulte [predefinições de tarefa para o codificador de mídia padrão](http://msdn.microsoft.com/library/mt269960).

Cada trabalho pode ter um ou mais tarefas dependendo do tipo de saudação de processamento que você deseja tooaccomplish. Por meio de Olá API REST, você pode criar trabalhos e as tarefas relacionadas em uma das duas maneiras:

* Tarefas podem ser definidas embutidas por meio da propriedade de navegação Olá tarefas nas entidades de trabalho.
* Use o processamento em lotes OData.

É recomendável que você sempre codifica arquivos de origem em uma conjunto de MP4 de taxa de bits adaptável e, em seguida, converte o formato desejado do hello conjunto toohello usando [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).

Se seu ativo de saída é armazenamento criptografado, você deve configurar política de entrega de ativos de saudação. Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Considerações

Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).

Antes de começar a fazer referência a processadores de mídia, verifique se que você tenha Olá ID de processador de mídia correta. Para obter mais informações, consulte [Obter processadores de mídia](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Conectar os serviços de tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Criar um trabalho com uma única tarefa de codificação
> [!NOTE]
> Quando você está trabalhando com hello API de REST de serviços de mídia, hello seguintes considerações se aplicam:
>
> Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).
>
> Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI. Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).
>
> Quando usando JSON e especificando Olá toouse **Metadata** palavra-chave na solicitação de saudação (por exemplo, tooreferences um objeto vinculado), você deve definir Olá **aceitar** cabeçalho muito[formato JSON detalhado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Aceitar: application/json; odata = verbose.
>
>

saudação de exemplo a seguir mostra como toocreate e lançar um trabalho com uma tarefa definir tooencode um vídeo em uma resolução e qualidade específicas. Quando estiver codificando com o Media Encoder Standard, você poderá usar as predefinições de configuração de tarefa especificadas [aqui](http://msdn.microsoft.com/library/mt269960).

Solicitação:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Resposta:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Definir nome do ativo de saída Olá
saudação de exemplo a seguir mostra como tooset Olá atributo assetName:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Considerações
* Propriedades TaskBody devem usar o número do literal XML toodefine Olá de entrada ou ativos de saída que são usados pela tarefa de saudação. tópico de tarefa Olá contém hello definição de esquema XML para Olá XML.
* Olá definição de TaskBody, valor da cada interna de <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).
* Uma tarefa pode ter vários ativos de saída. Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.
* Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.
* As tarefas não devem formar um ciclo.
* parâmetro de valor Hello que você passe tooJobInputAsset ou JobOutputAsset representa o valor de índice de saudação para um ativo. ativos reais Olá são definidos em hello InputMediaAssets e OutputMediaAssets propriedades de navegação na definição de entidade de trabalho hello.
* Como os serviços de mídia se baseia no OData v3, Olá ativos individuais nas Olá InputMediaAssets e coleções de propriedades de navegação OutputMediaAssets são referenciadas por meio de um " Metadata: uri" par nome-valor.
* Os InputMediaAssets mapeiam tooone ou mais ativos que você criou nos serviços de mídia. Os OutputMediaAssets são criados pelo sistema hello. Eles não referenciam um ativo existente.
* Os OutputMediaAssets podem ser nomeados usando o atributo assetName de saudação. Se esse atributo não estiver presente, o nome de saudação do hello OutputMediaAsset é qualquer valor de texto interno de saudação do hello <outputAsset> elemento for com um sufixo do valor do nome do trabalho hello, ou valor de Id do trabalho hello (no caso de Olá onde a propriedade de nome de saudação não está definida). Por exemplo, se você definir um valor para assetName muito "Exemplo", em seguida, Olá Name de OutputMediaAsset será definida muito "Sample." No entanto, se não definir um valor para assetName, mas definido o nome do trabalho Olá muito "Novotrabalho" e, em seguida, Olá Name de OutputMediaAsset será "JobOutputAsset (valor) novotrabalho."

## <a name="create-a-job-with-chained-tasks"></a>Criar um trabalho com tarefas encadeadas
Em muitos cenários de aplicativo, os desenvolvedores desejam toocreate uma série de tarefas de processamento. Nos serviços de mídia, você pode criar uma série de tarefas encadeadas. Cada tarefa executa etapas de processamento diferentes e pode usar diferentes processadores de mídia. tarefas Olá encadeado podem entregar um ativo de uma tarefa tooanother, executando uma sequência linear de tarefas no ativo de saudação. No entanto, tarefas de Olá executadas em um trabalho não são necessário toobe em uma sequência. Quando você cria uma tarefa encadeada, Olá encadeados **ITask** objetos são criados em uma única **IJob** objeto.

> [!NOTE]
> Atualmente, há um limite de 30 tarefas por trabalho. Se você precisar de mais de 30 tarefas toochain, crie mais de um trabalho de tarefas de saudação do toocontain.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Considerações
tooenable encadeamento de tarefas:

* Um trabalho deve ter, pelo menos, duas tarefas.
* Deve haver pelo menos uma tarefa cuja entrada é saída de saudação de outra tarefa no trabalho de saudação.

## <a name="use-odata-batch-processing"></a>Usar o processamento em lotes OData
saudação de exemplo a seguir mostra como toouse OData em lote toocreate de processamento de um trabalho e tarefas. Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Criar um trabalho usando um JobTemplate
Ao processar múltiplos ativos usando um conjunto comum de tarefas, use que uma tarefa de padrão JobTemplate toospecify Olá predefinições ou ordem de saudação tooset das tarefas.

saudação de exemplo a seguir mostra como toocreate um JobTemplate com um TaskTemplate que é definida embutida. Olá TaskTemplate usa Olá codificador de mídia padrão como o arquivo de ativo do hello MediaProcessor tooencode hello. No entanto, outros MediaProcessors também podem ser usados.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> Ao contrário de outras entidades de serviços de mídia, você deve definir um novo identificador GUID para cada TaskTemplate e colocá-lo em Olá taskTemplateId e a propriedade de Id no corpo da solicitação. esquema de conteúdo de identificação de saudação deve seguir o esquema de saudação descrito em identificar entidades de serviços de mídia do Azure. Além disso, os JobTemplates não podem ser atualizados. Em vez disso, você deve criar um novo com as suas alterações atualizadas.
>
>

Se for bem-sucedido, Olá resposta a seguir será retornada:

    HTTP/1.1 201 Created

    . . .


Olá mostrado no exemplo a seguir como toocreate um trabalho que faz referência a uma Id de JobTemplate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Se for bem-sucedido, Olá resposta a seguir será retornada:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe como toocreate tooencode um trabalho um ativo, consulte [como toocheck trabalho andamento com os serviços de mídia](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Consulte também
[Obter processadores de mídia](media-services-rest-get-media-processor.md)
