---
title: "Notas de versão de serviços de aaaMedia | Microsoft Docs"
description: "Notas de versão dos Serviços de Mídia"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Notas de versão dos Serviços de Mídia do Azure
Estas notas de versão resumem as alterações de versões anteriores e os problemas conhecidos.

> [!NOTE]
> Podemos deseja toohear de nossos clientes e concentrar em resolver problemas que afetam você. tooreport um problema ou fazer perguntas, poste no hello [Fórum do MSDN do Azure Media Services].
> 
> 

## <a id="issues"></a>Problemas conhecidos no momento
### <a id="general_issues"></a>Problemas gerais dos Serviços de Mídia
| Problema | Descrição |
| --- | --- |
| Muitos cabeçalhos HTTP comuns não são fornecidos nos Olá API REST. |Se você desenvolver aplicativos de serviços de mídia usando Olá API REST, você perceberá que alguns campos de cabeçalho HTTP comuns (incluindo CLIENT-REQUEST-ID REQUEST-ID e RETURN-CLIENT-REQUEST-ID) não têm suporte. Olá cabeçalhos serão adicionados em uma atualização futura. |
| Não é permitida a codificação por porcentagem. |Serviços de mídia usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem. Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, pode haver somente um ‘.’ para a extensão de nome de arquivo hello. |
| Olá método ListBlobs que faz parte da versão do SDK do armazenamento do Azure Olá 3. x falhar. |Serviços de mídia geram URLs SAS baseadas em Olá [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) versão. Se você desejar blobs de toolist toouse SDK de armazenamento do Azure em um contêiner de blob, use Olá [Cloudblobcontainer](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) método que faz parte do SDK do armazenamento do Azure versão 2. x. Olá método ListBlobs que faz parte da versão do SDK do armazenamento do Azure Olá 3. x falhará. |
| Mecanismo de limitação de serviços de mídia restringe o uso de recursos de saudação para aplicativos que fazem o serviço de toohello solicitações excessivas. serviço de saudação pode retornar o código de status HTTP serviço não disponível (503) hello. |Para obter mais informações, consulte a descrição de saudação do código de status HTTP 503 de saudação em Olá [códigos de erro do Azure Media Services](media-services-encoding-error-codes.md) tópico. |
| Ao consultar entidades, há um limite de 1000 entidades retornadas ao mesmo tempo porque pública v2 do REST limita os resultados da consulta resultados too1000. |Você precisa toouse **ignorar** e **levar** (.NET) / **superior** (REST), conforme descrito em [Este exemplo .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) e [nesta API REST exemplo](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Alguns clientes podem vir entre um problema de marca de repetição no manifesto de Smooth Streaming hello. |Para saber mais, consulte [esta](media-services-deliver-content-overview.md#known-issues) seção. |
| Os objetos do SDK do .NET dos Serviços de Mídia do Azure não podem ser serializados, e, por isso, não funcionam com o Caching do Azure. |Se você tentar tooserialize Olá AssetCollection do SDK objeto tooadd-tooAzure cache, uma exceção será lançado. |
| Os trabalhos de codificação falham com uma cadeia de caracteres de mensagem "Stage: DownloadFile. Código: System.NullReferenceException". |Olá codificação fluxo de trabalho típico é tooupload tooan de arquivos de vídeo de entrada ativo de entrada e enviar um ou mais trabalhos de codificação para esse ativo, de entrada sem modificação adicional que ativo de entrada. No entanto, se você modificar Olá ativo (por exemplo, ao adicionar/excluir/renomear arquivos dentro de Olá ativos) de entrada e os trabalhos subsequentes podem falhar com um erro DownloadFile. solução alternativa de saudação é toodelete ativo de entrada hello e carregar novamente tooa de arquivo (s) de entrada novo ativo. |

## <a id="rest_version_history"></a>Histórico de versão da API REST
Para obter informações sobre Olá histórico de versão de API de REST de serviços de mídia, consulte [referência da API REST do Azure Media Services].

## <a name="june-2017-release"></a>Versão de junho de 2017

Os Serviços de Mídia agora dão suporte à [autenticação baseada no Azure AD (Azure Active Directory)](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Atualmente, os serviços de mídia oferece suporte a modelo de autenticação de serviço de controle de acesso do Azure hello. No entanto, a autorização de Controle de Acesso será preterida em 1º de junho de 2018. É recomendável que você migre o modelo de autenticação toohello AD do Azure assim que possível.

## <a name="march-2017-release"></a>Versão de março de 2017

Agora você pode usar o padrão de mídia do Azure muito[gerar automaticamente uma taxa de bits Escada](media-services-autogen-bitrate-ladder-with-mes.md) especificando hello "Streaming adaptável" cadeia de caracteres de predefinição ao criar uma tarefa de codificação. "Streaming adaptável" é predefinição recomendado Olá se você quiser tooencode um vídeo para streaming com os serviços de mídia. Se você precisar toocustomize uma codificação predefinida para seu cenário específico, você pode começar com [esses](media-services-mes-presets-overview.md) predefinições.

Agora você pode usar o padrão de mídia do Azure ou o fluxo de trabalho do Media Encoder Premium muito[criar uma tarefa de codificação que gera fMP4 partes](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Versão de fevereiro de 2017

Começando em 1 de abril de 2017, qualquer registro de trabalho em sua conta mais de 90 dias será excluído automaticamente, junto com seus registros de tarefas associados, mesmo se Olá o número total de registros é abaixo de cota máximo hello. Se precisar de informações de trabalho/tarefa Olá tooarchive, você pode usar código Olá descrito [aqui](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Versão de janeiro de 2017

No Microsoft Azure Media Services AMS (), um **ponto de extremidade de Streaming** representa um serviço de streaming que pode entregar conteúdo diretamente tooa Player do cliente ou tooa rede de fornecimento de conteúdo (CDN) para melhor distribuição. Os Serviços de Mídia também fornecem integração perfeita da CDN do Azure. fluxo de saída de saudação de um serviço StreamingEndpoint pode ser uma transmissão ao vivo, um vídeo sob demanda ou download progressivo do seu ativo em sua conta de serviços de mídia. Cada conta dos Serviços de Mídia do Azure inclui um StreamingEndpoint padrão. StreamingEndpoints adicionais podem ser criadas na conta de saudação. Há duas versões do StreamingEndpoints, 1.0 e 2.0. A partir de 10 de janeiro de 2017, todas as contas AMS recém-criadas incluirão a versão 2.0 **padrão** do StreamingEndpoint. Adicional de pontos de extremidade que você adicione a conta de toothis streaming também será a versão 2.0. Essa alteração não afetará as contas existentes Olá; StreamingEndpoints existentes serão versão 1.0 e pode ser atualizado tooversion 2.0. Com essa alteração, haverá alterações de comportamento, cobrança e recurso (para obter mais informações, confira [este](media-services-streaming-endpoints-overview.md) tópico).

Além disso, o Azure Media Services a partir da versão de hello 2.15, adicionados Olá entidade de ponto de extremidade de Streaming toohello propriedades a seguir: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Para obter uma visão detalhada dessas propriedades, clique [aqui](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Versão de dezembro de 2016

Serviços de mídia do Azure agora permite que você tooaccess dados de telemetria/métricas para seus serviços. versão atual de saudação do AMS permite coletar dados de telemetria para canal ao vivo, StreamingEndpoint, e as entidades de arquivo em tempo real. Para obter mais informações, consulte [este](media-services-telemetry-overview.md) tópico.

## <a id="july_changes16"></a>Versão de julho de 2016
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Arquivo de atualizações de toomanifest (*. ISM) gerado por tarefas de codificação
Quando uma tarefa de codificação é enviada tooMedia codificador padrão ou o Azure Media Encoder, a tarefa de codificação hello gera um [arquivo de manifesto de streaming](media-services-deliver-content-overview.md) (*. ISM) ativo de saída do arquivo hello. Com a versão mais recente do serviço hello, sintaxe de saudação desse arquivo de manifesto de streaming foi atualizado.

> [!NOTE]
> sintaxe de saudação do hello streaming de arquivo de manifesto (. ISM) é reservado para uso interno e é toochange assunto em versões futuras. Não modifique ou manipular o conteúdo deste arquivo hello.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Um novo manifesto de cliente (*. Arquivo ISMC) é gerado no hello ativo de saída quando uma tarefa de codificação gera um ou mais arquivos MP4
Começando com a versão mais recente do serviço hello, após a conclusão de saudação de uma tarefa de codificação que gera um mais arquivos MP4, Olá saída que ativo também conterá um arquivo de manifesto (*.ismc) streaming do cliente. arquivo. ismc Olá ajuda a melhorar o desempenho de saudação do streaming dinâmico. 

> [!NOTE]
> sintaxe de saudação do arquivo de manifesto (. ismc) de cliente Olá é reservado para uso interno e é o assunto toochange em versões futuras. Não modifique ou manipular o conteúdo deste arquivo hello.
> 
> 

Para saber mais, confira [este](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blog.

### <a name="known-issues"></a>Problemas conhecidos
Alguns clientes podem vir entre um problema de marca de repetição no manifesto de Smooth Streaming hello. Para saber mais, consulte [esta](media-services-deliver-content-overview.md#known-issues) seção.

## <a id="apr_changes16"></a>Versão de abril de 2016
### <a name="azure-media-analytics"></a>Análise de Mídia do Azure
Os Serviços de Mídia do Azure introduziram a Análise de Mídia do Azure para proporcionar uma inteligência de vídeo avançada. Para obter informações detalhadas, confira [Visão Geral da Análise dos Serviços de Mídia do Azure](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (Preview)
Serviços de mídia do Azure agora permite que você toodynamically criptografar seu HTTP Live Streaming (HLS) de conteúdo com FairPlay da Apple. Você também pode usar a entrega de licença AMS serviço toodeliver FairPlay licenças tooclients. Para obter mais informações, consulte [tooStream de serviços de mídia do Azure Use seu conteúdo HLS protegido com Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Versão de fevereiro de 2016
versão mais recente de saudação do SDK de serviços de mídia do Azure para .NET (3.5.3) contém uma correção de bug Widevine relacionada. Olá problema era: AssetDeliveryPolicy não pôde ser reutilizado para vários ativos criptografados com Widevine. Como parte da saudação correção de bug propriedade a seguir foi adicionada toohello SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Versão de janeiro de 2016
Unidades reservadas de codificação renomeado tooreduce confusão com nomes de codificador.

Olá Basic, Standard e Premium unidades reservadas de codificação são renomeados tooS1, S2, e unidades reservadas S3, respectivamente.  Os clientes que usam RUs de codificação básicas hoje verá S1 como rótulo Olá no Portal do Azure (e na lista de saudação), ao padrão e Premium verá rótulos Olá S2 e S3 respectivamente. 

## <a id="dec_changes_15"></a>Versão de dezembro de 2015

### <a name="azure-media-encoder-deprecation-announcement"></a>Comunicado de substituição do Codificador de Mídia do Azure

O codificador de mídia do Azure começando em cerca de 12 meses da versão de saudação do codificador de mídia padrão será substituído.

### <a name="azure-sdk-for-php"></a>SDK do Azure para PHP
equipe do SDK do Azure Olá publicado uma nova versão de hello [Azure SDK para PHP](http://github.com/Azure/azure-sdk-for-php) pacote que contém as atualizações e novos recursos para serviços de mídia do Microsoft Azure. Em particular, Olá SDK de serviços de mídia do Azure para PHP agora dá suporte a mais recente Olá [proteção de conteúdo](media-services-content-protection-overview.md) recursos: criptografia dinâmica com o AES e DRM (PlayReady e Widevine) com e sem restrição de Token. Ele também oferece suporte a [Unidades de Codificação](media-services-dotnet-encoding-units.md)de dimensionamento.

Para obter mais informações, consulte:

* Olá [SDK de serviços de mídia do Microsoft Azure para PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blog.
* a seguir Olá [exemplos de código](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp começar rapidamente:
  * **vodworkflow_aes.PHP**: Este é um arquivo do PHP que mostra como toouse criptografia dinâmica AES-128 e o serviço de entrega de chave. Ela é baseada no exemplo de .NET hello explicado em [isso](media-services-protect-with-aes128.md) artigo.
  * **vodworkflow_aes.PHP**: Este é um arquivo do PHP que mostra como toouse criptografia dinâmica PlayReady e o serviço de entrega de licenças. Ela é baseada no exemplo de .NET hello explicado em [isso](media-services-protect-with-drm.md) artigo.
  * **scale_encoding_units.PHP**: Este é um arquivo do PHP que mostra como a codificação tooscale reservado unidade.

## <a id="nov_changes_15"></a>Versão de novembro de 2015
Serviços de mídia do Azure agora oferece serviço de entrega de licença do Google Widevine na nuvem hello. Para obter mais detalhes, consulte muito[este blog comunicado](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Veja também [este tutorial](media-services-protect-with-drm.md) e o [repositório do GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Observe que os serviços de entrega de licenças do Widevine fornecidos pelos Serviços de Mídia do Azure estão em versão de visualização. Para saber mais, confira [este blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Versão de outubro de 2015
Serviços de mídia do Azure (AMS) agora está ativo no hello centros de dados a seguir: Sul do Brasil, Índia Oeste, Sul da Índia e Índia Central. Agora você pode usar o hello portal do Azure muito[criar contas de serviço de mídia](media-services-portal-create-account.md) e executar várias tarefas descritas [aqui](https://azure.microsoft.com/documentation/services/media-services/). No entanto, a Codificação Ativa não está habilitada nesses datacenters. Além disso, nem todos os tipos de Unidades Reservadas para Codificação estão disponíveis nesses datacenters.

* Sul do Brasil:                                          somente as Unidades Reservadas para Codificação Standard e Básica estão disponíveis
* Índia Ocidental, Sul da Índia e Índia Central:             somente as Unidades Reservadas para Codificação Básica estão disponíveis

## <a id="september_changes_15"></a>Versão de setembro de 2015
* AMS agora oferece Olá capacidade tooprotect vídeo sob demanda (VOD) e fluxos ao vivo com tecnologia DRM Modular Widevine. Você pode usar o hello entrega serviços parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Para saber mais, confira [este blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Você pode usar [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (começando com a versão de hello 3.5.1) ou REST API tooconfigure seu toouse AssetDeliveryConfiguration Widevine.  
* O AMS adicionou suporte para vídeos ProRes da Apple. Agora você pode carregar os arquivos de vídeos de origem do QuickTime que usam Apple ProRes ou outros codecs. Para saber mais, confira [este blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Agora você pode usar o codificador de mídia padrão toodo ao vivo e abaixo de recorte extração de arquivo morto. Para saber mais, confira [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* Olá filtragem de atualizações a seguir foram feita: 
  
  * Agora você pode usar o formato HLS (Apple HTTP Live Streaming) com filtro somente áudio. Essa atualização permite rastrear somente de áudio de tooremove especificando (somente de áudio = false) na URL de saudação.
  * Ao definir filtros para seus ativos, agora você tem capacidade toocombine vários (se too3) filtros em uma única URL.
    
    Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.
* O AMS agora dá suporte ao I-Frames no HLS v4. O suporte do I-Frame otimiza as operações de avanço e retrocesso. Por padrão, todas as saídas do HLS v4 incluem o playlist do I-Frame (EXT-X-I-FRAME-STREAM-INF).
  
    Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a id="august_changes_15"></a>Versão de agosto de 2015
* Agora, o SDK do Serviços de Mídia do Azure para Java versão V0.8.0  e novos exemplos estão disponíveis. Para obter mais informações, confira:
  
  * [Postagem no blog](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Repositório de amostras de Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Atualização do Player de Mídia do Azure com suporte de fluxo de vários áudios. Para obter mais informações, confira:
  * [Postagem no blog](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Versão de julho de 2015
* Apresentação da disponibilidade geral de saudação do codificador de mídia padrão. Para saber mais, confira [esta postagem no blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    O Codificador de Mídia Padrão usa as predefinições descritas [nesta](http://go.microsoft.com/fwlink/?LinkId=618336) seção. Observe que, ao usar uma predefinição de 4K codifica, você deve obter Olá **Premium** tipo de unidade reservada. Para obter mais informações, consulte [como tooScale codificação](media-services-scale-media-processing-overview.md).
* Legendas em tempo real ativas com os Serviços de Mídia e o Player do Azure. Para saber mais, veja [esta postagem no blog](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>Atualizações do SDK do .NET dos Serviços de Mídia
O SDK do .NET dos Serviços de Mídia do Azure está agora na versão 3.4.0.0. Olá funcionalidade a seguir foi adicionado nesta versão:  

* Suporte implementado para arquivo morto dinâmico. Observe que você não pode baixar um ativo que contenha um arquivo morto dinâmico.
* Suporte implementado para filtros dinâmicos.
* Funcionalidade implementada que permite que o contêiner de armazenamento de tookeep usuários ao excluir o ativo.
* Correções de bug relacionado tooretry políticas nos canais.
* **Fluxo de Trabalho Premium do Codificador de Mídia** habilitado.

## <a id="june_changes_15"></a>Versão de junho de 2015
### <a name="media-services-net-sdk-updates"></a>Atualizações do SDK do .NET dos Serviços de Mídia
O SDK do .NET dos Serviços de Mídia do Azure está agora na versão 3.3.0.0. Olá funcionalidade a seguir foi adicionado nesta versão:  

* suporte para especificação de Descoberta do OpenId Connect,
* suporte para tratamento de substituição de chaves no lado do provedor de identidade. 

Se você estiver usando um provedor de identidade que expõe o documento de descoberta de OpenID Connect (como Olá seguintes provedores de fazer: Active Directory do Azure, Google, Salesforce), você pode instruir o Azure Media Services tooobtain chaves para validação de token JWT de assinatura OpenID se conectar a especificação de descoberta. 

Para obter mais informações, consulte [usando Json Web as chaves do OpenID Connect toowork especificações de descoberta com JWT token de autenticação no Azure Media Services](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Versão de maio de 2015
Anunciando Olá novos recursos a seguir:

* [Uma visualização da Codificação Ativa com os Serviços de Mídia](media-services-manage-live-encoder-enabled-channels.md)
* [Manifesto dinâmico](media-services-dynamic-manifest-overview.md)
* [Uma visualização do processador de mídia Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Versão de abril de 2015
### <a name="general-media-services-updates"></a>Atualizações gerais dos Serviços de Mídia
* [Anunciando o Player de Mídia do Azure](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* Começando com 2.10 de REST de serviços de mídia, canais tooingest configurado um protocolo RTMP, são criados com primário e secundário URLs de ingestão. Para saber mais, confira [Configurações de inclusão de canal](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Atualizações do Indexador de Mídia do Azure
* Suporte ao idioma espanhol
* Novo formato xml de configuração

Para saber mais, confira [este blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Atualizações do SDK do .NET dos Serviços de Mídia
O SDK do .NET dos Serviços de Mídia do Azure está agora na versão 3.2.0.0.

Olá seguem alguns Prezado cliente voltados para atualizações:

* **Alteração recente**: alterado **TokenRestrictionTemplate.Issuer** e **TokenRestrictionTemplate.Audience** toobe de um tipo de cadeia de caracteres.
* Atualizações relacionadas toocreating políticas de repetição personalizada.
* Correções de bug relacionado toouploading/baixar arquivos.
* Olá **MediaServicesCredentials** classe agora aceita tooauthenticate de ponto de extremidade de controle de acesso primária e secundária contra.

## <a id="march_changes_15"></a>Versão de março de 2015
### <a name="general-media-services-updates"></a>Atualizações gerais dos Serviços de Mídia
* Agora, os Serviços de Mídia fornecem integração com a CDN do Azure. toosupport Olá integração, hello **CdnEnabled** propriedade foi adicionada muito**StreamingEndpoint**.  **CdnEnabled** pode ser usado com APIs REST a partir da versão 2.9 (para saber mais, confira [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** pode ser usado com o SDK do .NET a partir da versão 3.1.0.2 (para saber mais, confira [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Anúncio do **Fluxo de trabalho do Media Encoder Premium**. Para saber mais, confira [Apresentando a codificação Premium nos Serviços de Mídia do Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Versão de fevereiro de 2015
### <a name="general-media-services-updates"></a>Atualizações gerais dos Serviços de Mídia
A API REST dos Serviços de Mídia agora está na versão 2.9. A partir desta versão, você pode habilitar Olá integração do Azure CDN com pontos de extremidade de streaming. Para saber mais, confira [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Versão de janeiro de 2015
### <a name="general-media-services-updates"></a>Atualizações gerais dos Serviços de Mídia
Anúncio da disponibilidade geral (GA) de proteção de conteúdo com criptografia dinâmica. Para saber mais, confira [Os Serviços de mídia do Azure aprimoram a segurança de streaming com a disponibilidade geral da tecnologia DRM](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>Atualizações do SDK do .NET dos Serviços de Mídia
O SDK do .NET dos Serviços de Mídia do Azure está agora na versão 3.1.0.1.

Esta versão marcou o construtor de Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate saudação padrão como obsoleto. Olá novo construtor usa TokenType como um argumento.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Versão de dezembro de 2014
### <a name="general-media-services-updates"></a>Atualizações gerais dos Serviços de Mídia
* Algumas atualizações e novos recursos foram adicionados toohello processador de indexador de mídia do Azure. Para saber mais, confira [Notas de versão de indexador de mídia do Azure 1.1.6.7](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Adicionada uma nova API de REST que permite que você tooupdate unidades reservadas de codificação: [EncodingReservedUnitType com resto](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Acrescentado suporte a CORS para o serviço de distribuição de chaves.
* Foram feitos aprimoramentos de desempenho nas opções das políticas de autorização de consulta.
* No data center da China, Olá [chave entrega URL](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) agora é por cliente (assim como em outros data centers).
* Duração de destino automático HLS adicionada. Ao fazer streaming ao vivo, o HLS é sempre empacotado dinamicamente. Por padrão, o Media Services calcula automaticamente empacotamento taxa de segmento HLS (FragmentsPerSegment) com base em Olá quadro-chave intervalo (KeyFrameInterval), também chamado tooas grupo de imagens – GOP, que é recebido do codificador dinâmico Olá. Para obter mais informações, consulte [Trabalhando com a Transmissão ao Vivo dos Serviços de Mídia do Azure].

### <a name="media-services-net-sdk-updates"></a>Atualizações do SDK do .NET dos Serviços de Mídia
* [O SDK do .NET dos Serviços de Mídia do Azure](http://www.nuget.org/packages/windowsazure.mediaservices/) está agora na versão 3.1.0.0.
* Atualizado Olá .net SDK dependência too.NET 4.5 Framework.
* Adicionada uma nova API que permite que você tooupdate unidades reservadas de codificação. Para saber mais, confira [Atualizando tipo de unidade reservada e aumentando unidades reservadas de codificação usando o .NET](media-services-dotnet-encoding-units.md).
* Acrescentado suporte a JWT (JSON Web Token) para autenticação via token. Para saber mais, confira [Autenticação de token JWT nos Serviços de Mídia do Azure e criptografia dinâmica](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Adicionado deslocamentos relativos para BeginDate e ExpirationDate no modelo de licença do PlayReady hello.

## <a id="november_changes_14"></a>Versão de novembro de 2014
* Serviços de mídia agora permite que você tooingest uma transmissão ao vivo suave (FMP4) conteúdo em uma conexão SSL. tooingest por SSL, verifique Olá de tooupdate se tooHTTPS de URL de ingestão.  Observe que, atualmente, o AMS não dá suporte ao SSL com domínios personalizados.  Para saber mais sobre a transmissão ao vivo, confira [Trabalhando com a Transmissão ao Vivo dos Serviços de Mídia do Azure].
* Observe que, no momento, você não pode ingerir um fluxo ao vivo RTMP por uma conexão SSL.
* Só é possível transmitir sobre SSL se saudação do qual você distribuir o conteúdo do ponto de extremidade de streaming foi criada após 10 de setembro de 2014. Se suas URLs de streaming se baseiam em Olá criados após 10 de setembro de pontos de extremidade de streaming, Olá URL contém "streaming.mediaservices.windows.net" (novo formato de saudação). As URLs de streaming que contêm "origin.mediaservices.windows.net" (formato antigo do hello) não dão suporte a SSL. Se a URL estiver no formato antigo hello e você desejar toostream capaz de toobe por SSL, [criar um novo ponto de extremidade de streaming](media-services-portal-manage-streaming-endpoints.md). Use as URLs criadas com base em Olá novo streaming toostream de ponto de extremidade seu conteúdo sobre SSL.

## <a id="october_changes_14"></a>Versão de outubro de 2014
### <a id="new_encoder_release"></a>Versão do codificador de Serviços de Mídia
Anunciando Olá nova versão dos serviços de mídia Azure Media Encoder. Com hello Azure Media Encoder mais recente será cobrado apenas para saída de GBs, mas caso contrário, o hello novo codificador é o recurso compatível com o codificador de saudação anterior. Para mais informações [Detalhes dos preços dos Serviços de Mídia]).

### <a id="oct_sdk"></a>SDK do .NET dos Serviços de Mídia
O SDK dos Serviços de Mídia para extensões .NET agora está na versão 2.0.0.3.

O SDK dos Serviços de Mídia para .NET agora está na versão 3.0.0.8.

Olá, as seguintes alterações foram feita:

* Refatoração em classes de política de repetição.
* Adicionando cabeçalhos de solicitação toohttp do cadeia de caracteres de agente de usuário.
* Adicionando a etapa de compilação de restauração do nuget.
* Corrigindo cenário testes toouse x509 cert do repositório.
* Validando configurações durante a atualização de canal e do ponto de extremidade de streaming.

### <a name="new-github-repository-toohost-media-services-samples"></a>Novos exemplos de serviços de mídia GitHub repositório toohost
Os exemplos estão localizados em [Repositório GitHub de exemplos dos Serviços de Mídia do Azure](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Versão de setembro de 2014
Os metadados REST dos Serviços de Mídia agora estão na versão 2.7. Para obter mais informações sobre atualizações mais recentes de REST hello, consulte [referência da API REST do Azure Media Services].

SDK dos Serviços de Mídia para .NET agora está na versão 3.0.0.7

### <a id="sept_14_breaking_changes"></a>Alterações interruptivas
* **Origem** foi renomeado muito[StreamingEndpoint].
* Uma alteração no comportamento padrão de saudação ao usar Olá **portal do Azure** tooencode e, em seguida, publicar arquivos MP4.

Anteriormente, ao usar o hello Portal clássico do Azure toopublish um ativo de vídeo MP4 único arquivo uma URL SAS seria criada (URLs SAS permitem Olá toodownload vídeo de um armazenamento de blob). Atualmente, quando você usar Olá Portal clássico do Azure tooencode e, em seguida, publica um ativo de vídeo de MP4 de arquivo único, Olá gerado URL pontos tooan Azure Media Services ponto de extremidade de streaming.  Essa alteração não afeta vídeos MP4 que são carregados diretamente tooMedia serviços e publicados sem ser codificados pelos serviços de mídia do Azure.

No momento, você tem Olá dois problemas de saudação toosolve opções a seguir.

* Habilitar unidades de streaming e usar ativos do empacotamento dinâmico toostream hello. mp4 como uma apresentação de streaming suave.
* Criar toodownload uma url SAS (ou reproduzir progressivamente) Olá MP4. Para obter mais informações sobre como toocreate um localizador SAS, consulte [entregando conteúdo].

### <a id="sept_14_GA_changes"></a>Novos recursos/cenários que fazem parte da versão do GA
* **Processador de Mídia do Indexador**. Para obter mais informações, consulte [Indexando arquivos de mídia com o Indexador de Mídia do Azure].
* Olá [StreamingEndpoint] entidade agora permite que você tooadd nomes de domínio personalizado (host).
  
    Para um nome de domínio personalizado toobe usado como nome de ponto de extremidade de streaming de serviços de mídia hello, você precisa tooyour de nomes de host personalizado tooadd ponto de extremidade de streaming. Use nomes de host personalizado de tooadd de APIs de REST de serviços de mídia ou o SDK do .NET de saudação.
  
    Olá considerações a seguir se aplicam:
  
  * Você deve ter a propriedade Olá Olá personalizado do nome de domínio.
  * propriedade Olá Olá do nome de domínio deve ser validada pelos serviços de mídia do Azure. domínio de saudação toovalidate, criar um CName que mapeia <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices-dns-zone >. 
  * Você deve criar outro CName que mapeia nome de host do Olá host personalizado nome (por exemplo, sports.contoso.com) tooyour StreamingEndpont serviços de mídia (por exemplo, amstest.streaming.mediaservices.windows.net).

    Para obter mais informações, consulte Olá **CustomHostNames** propriedade Olá [StreamingEndpoint] tópico.

### <a id="sept_14_preview_changes"></a>Novos recursos/cenários que fazem parte da versão de visualização pública Olá
* Visualização de Live Streaming. Para obter mais informações, consulte [Trabalhando com a Transmissão ao Vivo dos Serviços de Mídia do Azure].
* Serviço de entrega de chave. Para obter mais informações, consulte [Usando o serviço de entrega de chave e criptografia dinâmica do AES-128].
* Criptografia dinâmica do EAS. Para obter mais informações, consulte [Usando o serviço de entrega de chave e criptografia dinâmica do AES-128].
* Serviço de entrega de licença do PlayReady. Para obter mais informações, consulte [Usando o serviço de entrega de licença e criptografia dinâmica do PlayReady].
* Criptografia dinâmica do PlayReady. Para obter mais informações, consulte [Usando o serviço de entrega de licença e criptografia dinâmica do PlayReady].
* Modelo de licença do PlayReady dos Serviços de Mídia. Para obter mais informações, consulte [Visão geral do modelo de licença do PlayReady dos Serviços de Mídia].
* Streaming de ativos criptografados de armazenamento. Para obter mais informações, consulte [Streaming de conteúdo criptografado de armazenamento].

## <a id="august_changes_14"></a>Versão de agosto de 2014
Quando você codifica um ativo, é produzido um ativo de saída após a conclusão do trabalho de codificação de saudação. Até esta versão, o Codificador de Serviços de Mídia do Azure produzia metadados sobre os ativos de saída. Começando com o codificador de saudação essa versão também produz metadados sobre os ativos de entrada. Para obter mais informações, consulte Olá [metadados de entrada] e [metadados de saída] tópicos.

## <a id="july_changes_14"></a>Versão de julho de 2014
Olá correções de bug a seguir foram feita para hello Azure Media Services Packager e Criptografador:

* Apenas o áudio é reproduzido quando transmultiplexação um tooHTTP de ativos de arquivamento dinâmico transmissão ao vivo – isso foi corrigido e agora o áudio e vídeo são reproduzidos.
* Ao empacotar um ativo tooHTTP criptografia de envelope AES de 128 bits e de transmissão ao vivo, fluxos de pacotes de saudação não são reproduzidos em dispositivos Android – esse bug foi corrigido e fluxo de pacotes de saudação é reproduzido nos dispositivos Android que dão suporte a HTTP Live Streaming.

## <a id="may_changes_14"></a>Versão de maio de 2014
### <a id="may_14_changes"></a>Atualizações gerais dos Serviços de Mídia
Agora você pode usar [empacotamento dinâmico] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, adicione Olá seguindo o caminho de localizador de origem do formato toohello: * .ism/manifest(format=m3u8-aapl-v3). Para obter mais informações, consulte o [Blog de Nick Drouin].

O Empacotamento Dinâmico agora também oferece suporte à entrega de HLS (v3 e v4) criptografado com PlayReady com base em Smooth Streaming estaticamente criptografado com PlayReady. Para obter informações sobre como tooencrypt Smooth Streaming com PlayReady, consulte [protegendo Smooth Stream com PlayReady].

### <a name="may_14_donnet_changes"></a>Atualizações do SDK do .NET dos Serviços de Mídia
Olá aprimoramentos a seguir está incluído no hello versão 3.0.0.5 do Media Services .NET SDK:

* Melhor velocidade e resiliência para carregar/baixar ativos de mídia.
* Melhorias na lógica de repetição e manipulação de exceção temporária: 
  
  * Detecção de erro temporário e lógica de repetição foram aprimorados para as exceções causadas por consultar, salvar alterações, carregar ou baixar arquivos. 
  * Ao obter Exceções da Web (por exemplo, durante uma solicitação de token ACS), você observará que erros fatais estão falhando mais rapidamente agora.

Para obter mais informações, consulte [lógica de repetição no SDK do Media Services para .NET de saudação].

## <a id="april_changes_14"></a>Versão do Codificador de abril de 2014
### <a name="april_14_enocer_changes"></a>Atualizações do Codificador de Serviços de Mídia
* Suporte adicionado para a ingestão de arquivos AVI criados usando Olá Grass Valley EDIUS o editor não linear, onde Olá vídeo é pouco compactados usando Grass Valley HQ/HQX codec. Para obter mais informações, consulte [Grass Valley anuncia EDIUS 7 Streaming por meio de saudação nuvem].
* Adicionado suporte para especificação de convenção de nomenclatura de saudação para arquivos Olá produzido pelo Olá Media Encoder. Para obter mais informações, consulte [Controlando nomes de arquivo de saída do Codificador do Serviço de Mídia].
* Adicionado suporte para sobreposições de vídeo e/ou áudio. Para obter mais informações, consulte [Criando sobreposições].
* Adicionado suporte para unir vários segmentos de vídeo. Para obter mais informações, consulte [Unindo segmentos de vídeo].
* Correção de bug relacionado tootranscoding de MP4s onde Olá áudio foi codificado com MPEG-1 Audio layer 3 (MP3).

## <a id="jan_feb_changes_14"></a>Versões de janeiro/fevereiro de 2014
### <a name="jan_fab_14_donnet_changes"></a>SDK do .NET dos Serviços de Mídia do Azure 3.0.0.1, 3.0.0.2 e 3.0.0.3
Olá alterações do 3.0.0.1 e 3.0.0.2 incluem:

* Correção de problemas relacionados ao toousage de consultas LINQ com instruções OrderBy.
* Divida as soluções de teste em [GitHub] em testes baseados em unidade e testes baseados em cenário.

Para obter mais detalhes sobre alterações hello, consulte: [versões do SDK do Azure Media Services .NET 3.0.0.1 e 3.0.0.2].

Olá, as seguintes alterações foram realizada na 3.0.0.3:

* Versão do armazenamento do Azure atualizada dependências toouse 3.0.3.0. 
* Corrigido o problema de compatibilidade reversa para versões 3.0*.* . 

## <a id="december_changes_13"></a>Versão de dezembro de 2013
### <a name="dec_13_donnet_changes"></a>SDK do .NET dos Serviços de Mídia do Azure 3.0.0.0
> [!NOTE]
> As versões 3.0.x.x não são compatíveis com versões 2.4.x.x.
> 
> 

versão mais recente de saudação do hello SDK do Media Services agora é 3.0.0.0. Você pode baixar o pacote mais recente de saudação do Nuget ou obter os bits de saudação do [GitHub].

Começando com hello SDK de serviços de mídia versão 3.0.0.0, você pode reutilizar Olá [Azure Active Directory Access Control Service (ACS)] tokens. Para obter mais informações, consulte hello "reutilizando Tokens controle de acesso Service" seção Olá [conectando serviços tooMedia com hello SDK do Media Services para .NET] tópico.

### <a name="dec_13_donnet_ext_changes"></a>Extensões do SDK do .NET dos Serviços de Mídia do Azure 2.0.0.0
Olá extensões de SDK .NET do serviços de mídia do Azure é um conjunto de métodos de extensão e funções auxiliares que simplificam seu código e torná-lo mais fácil toodevelop com os serviços de mídia do Azure. Você pode obter os bits mais recentes de saudação do [extensões do SDK do Azure Media Services .NET].

## <a id="november_changes_13"></a>Versão de novembro de 2013
### <a name="nov_13_donnet_changes"></a>Alterações do SDK do .NET dos Serviços de Mídia do Azure
A partir desta versão, Olá SDK de serviços de mídia para .NET trata erros de falha temporária que podem ocorrer ao fazer a camada de API de REST de serviços de mídia toohello chamadas.

## <a id="august_changes_13"></a>Versão de agosto de 2013
### <a name="aug_13_powershell_changes"></a>Cmdlets do PowerShell dos Serviços de Mídia incluídos nas Ferramentas de SDK do Azure
Olá cmdlets do PowerShell de serviços de mídia a seguir agora está incluída no [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Por exemplo: `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Por exemplo: `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Por exemplo: `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Por exemplo: `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Versão de junho de 2013
### <a name="june_13_general_changes"></a>Alterações dos Serviços de Mídia do Azure
alterações de saudação mencionadas nesta seção são atualizações incluídas no hello que versões de junho de 2013 do Media Services.

* Capacidade toolink armazenamento várias contas tooa conta de serviço de mídia. 
  
    StorageAccount
  
    Asset.StorageAccountName e Asset.StorageAccount
* Capacidade tooupdate Priority. 
* Entidades e propriedades relacionadas à notificação: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Trabalho
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Alterações do SDK do .NET dos Serviços de Mídia do Azure
Olá alterações a seguir estão incluídas em junho de 2013 versões SDK do Media Services. Olá a mais recente do Media Services SDK está disponível no GitHub.

* Começando com a versão de hello 2.3.0.0, Olá SDK do Media Services oferece suporte à vinculação tooa de contas de armazenamento várias contas de serviços de mídia. Olá seguintes APIs oferecem suporte a esse recurso:
  
    Olá IStorageAccount tipo.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts propriedade.
  
    Olá propriedade StorageAccount.
  
    Olá StorageAccountName propriedade.
  
    Para obter mais informações, consulte [Gerenciando ativos de Serviços de Mídia através de várias contas de armazenamento].
* APIs relacionadas à notificação. Começando com a versão de hello 2.2.0.0 ter notificações de armazenamento de fila Olá capacidade toolisten tooAzure. Para obter mais informações, consulte [Manipulando notificações de trabalho dos Serviços de Mídia].
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions propriedade.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint tipo.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription tipo.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection tipo.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType tipo.
  
    Olá Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState tipo.
* Dependência Olá cliente de armazenamento do Azure SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Dependência de OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Versão de dezembro de 2012
### <a name="dec_12_dotnet_changes"></a>Alterações do SDK do .NET dos Serviços de Mídia do Azure
* Intellisense: adicionada a documentação do Intellisense que faltava para vários tipos.
* Microsoft.Practices.TransientFaultHandling.Core: Corrigido um problema onde hello SDK ainda tinha uma versão antiga do tooan dependência desse assembly. Olá SDK agora faz referência à versão 5.1.1209.1 desse assembly.

Correções para problemas encontrados em Olá SDK de novembro de 2012:

* IAsset.Locators.Count : essa contagem agora é relatada corretamente em novas interfaces IAsset depois de todos os localizadores terem sido excluídos.
* IAssetFile.ContentFileSize : esse valor agora é definido adequadamente após um upload por IAssetFile.Upload(filePath).
* IAssetfile.ContentFileSize: essa propriedade agora pode ser definida durante a criação de um arquivo de ativo. Antes era somente leitura.
* Iassetfile: Corrigido um problema em que esse método de upload síncrono gerava Olá seguinte erro ao carregar o ativo de toohello vários arquivos. Erro de saudação foi "solicitação de saudação tooauthenticate falha no servidor. Verifique se o valor de saudação do cabeçalho de autorização está formado corretamente e inclui assinatura hello."
* IAssetFile.UploadAsync : corrigido um problema em que não mais de cinco arquivos podiam ser carregados ao mesmo tempo.
* Iassetfile. Uploadprogresschanged: Este evento agora é fornecido pelo Olá SDK.
* IAssetFile.DownloadAsync (string, BlobTransferClient, ILocator, CancellationToken): essa sobrecarga de método agora é fornecida.
* IAssetFile.DownloadAsync : corrigido um problema em que não mais de cinco arquivos podiam ser baixados ao mesmo tempo.
* IAssetFile.Delete(): Corrigido um problema em que chamar delete pode lançar uma exceção se nenhum arquivo foi carregado para IAssetFile de saudação.
* Trabalhos: Corrigido um problema em que o encadeamento de uma "MP4 tooSmooth fluxos tarefa" com uma "tarefa de proteção PlayReady" usando um modelo de trabalho não cria todas as tarefas em todos os.
* EncryptionUtils.GetCertificateFromStore(): Este método não lança uma exceção de referência nula devido a falhas de tooa Localizando certificado Olá com base em problemas de configuração de certificado.

## <a id="november_changes_12"></a>Versão de novembro de 2012
Olá, as alterações mencionadas nesta seção são atualizações incluídas no hello novembro de 2012 (versão 2.0.0.0) SDK. Essas alterações podem requerer qualquer código escrito para saudação de junho de 2012 preview SDK versão toobe modificação ou reformulação.

* Ativos
  
    Create (assetname) é uma função de criação de ativo hello apenas. IAsset não carrega arquivos como parte da chamada de método hello. Use IAssetFile para carregar.
  
    método IAsset Publish Hello e o valor de enumeração Assetstate Olá foram removidos da saudação SDK dos serviços. Qualquer código que conte com esse valor deve ser reescrito.
* FileInfo
  
    Essa classe foi removida e substituída pelo IAssetFile.
  
    IAssetFiles
  
    IAssetFile substitui FileInfo e tem um comportamento diferente. toouse, instanciar o objeto do hello IAssetFiles, seguido por um carregamento de arquivo usando Olá SDK do Media Services ou hello SDK de armazenamento do Azure. Olá sobrecargas iassetfile. upload a seguir pode ser usado:
  
  * Iassetfile: Um método síncrono que bloqueia o thread de saudação e é recomendado apenas ao carregar um único arquivo.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken): um método assíncrono. Esse é o mecanismo de carregamento de saudação preferido. 
    
    Bug conhecido: usar Olá cancellationToken cancelará o carregamento de saudação; No entanto, o estado de cancelamento de Olá tarefas Olá pode ser qualquer um dos vários estados. É preciso capturar e tratar as exceções adequadamente.
* Localizadores
  
    Olá versões específicas à origem foram removidas. contexto de saudação específico a SAS. Locators.CreateSasLocator (asset, accessPolicy) será marcado como preterido ou removido pelo GA. Consulte Olá localizadores seção em novas funcionalidades para o comportamento atualizado.

## <a id="june_changes_12"></a>Versão de visualização de junho de 2012
Olá funcionalidade a seguir é novo na versão de novembro de saudação do hello SDK.

* Excluindo entidades
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey objetos agora são excluídos no nível de objeto hello, ou seja, seja, em vez de exigirem uma exclusão no hello coleção, Delete (objinstance).
* Localizadores
  
    Os localizadores devem ser criados usando o método CreateLocator de saudação e usar valores de enumeração LocatorType.SAS ou Locatortype Olá como um argumento de tipo específico de saudação do localizador, você deseja toocreate.
  
    Novas propriedades foram adicionadas tooLocators toomake-tooobtain mais fácil URIs utilizáveis para o seu conteúdo. Essa reestruturação de localizadores foi destinada tooprovide mais flexibilidade para extensibilidade futura de terceiros e aumentar a facilidade de uso para aplicativos de cliente de mídia.
* Suporte ao método assíncrono
  
    Foi adicionado suporte assíncrono tooall métodos.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Fórum do MSDN do Azure Media Services]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[referência da API REST do Azure Media Services]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Detalhes dos preços dos Serviços de Mídia]: http://azure.microsoft.com/pricing/details/media-services/
[metadados de entrada]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[metadados de saída]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[entregando conteúdo]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Indexando arquivos de mídia com o Indexador de Mídia do Azure]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Trabalhando com a Transmissão ao Vivo dos Serviços de Mídia do Azure]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[Usando o serviço de entrega de chave e criptografia dinâmica do AES-128]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[Usando o serviço de entrega de licença e criptografia dinâmica do PlayReady]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Visão geral do modelo de licença do PlayReady dos Serviços de Mídia]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Streaming de conteúdo criptografado de armazenamento]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[empacotamento dinâmico]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[Blog de Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[protegendo Smooth Stream com PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[lógica de repetição no SDK do Media Services para .NET de saudação]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley anuncia EDIUS 7 Streaming por meio de saudação nuvem]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[Controlando nomes de arquivo de saída do Codificador do Serviço de Mídia]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Criando sobreposições]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Unindo segmentos de vídeo]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[versões do SDK do Azure Media Services .NET 3.0.0.1 e 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory Access Control Service (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[conectando serviços tooMedia com hello SDK do Media Services para .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[extensões do SDK do Azure Media Services .NET]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Gerenciando ativos de Serviços de Mídia através de várias contas de armazenamento]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Manipulando notificações de trabalho dos Serviços de Mídia]: http://msdn.microsoft.com/library/azure/dn261241.aspx

