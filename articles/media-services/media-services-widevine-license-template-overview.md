---
title: "Visão geral do modelo de licença aaaWidevine | Microsoft Docs"
description: "Este tópico fornece uma visão geral de um modelo de licença Widevine usado tooconfigure Widevine licenças."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Visão geral do modelo de licença do Widevine
## <a name="overview"></a>Visão geral
Serviços de mídia do Azure agora permite que você os licenças Widevine tooconfigure e solicitação. Quando o player de saudação do usuário final tenta tooplay seu conteúdo Widevine protegido, uma solicitação é enviada toohello licença entrega serviço tooobtain uma licença. Se o serviço de licença Olá Aprovar solicitação de Olá, ele emite licença saudação que é enviada toohello cliente e pode ser usado toodecrypt e play Olá conteúdo especificado.

A solicitação de licença do Widevine é formatada como uma mensagem JSON.  

>[!NOTE]
> Você pode escolher toocreate uma mensagem vazia com nenhuma valores apenas "{}" e um modelo de licença será criado com todos os padrões. padrão de saudação funciona na maioria dos casos. Por exemplo, para cenários de entrega de licença com base em MS que sempre devem ser o padrão. Se você precisar tooset hello "provedor" e "content_id" valores, um provedor deve corresponder às credenciais de Widevine do Google.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Mensagem JSON
| Nome | Valor | Descrição |
| --- | --- | --- |
| payload |Cadeia codificada em Base64 |solicitação de licença Olá enviada por um cliente. |
| content_id |Cadeia codificada em Base64 |Identificador usado tooderive KeyId(s) e chaves de conteúdo para cada content_key_specs.track_type. |
| provider |string |Toolook usada chaves de conteúdo e políticas. Se a distribuição de chaves MS é usada para entrega de licença do Widevine, esse parâmetro é ignorado. |
| policy_name |string |Nome de uma política registrada anteriormente. Opcional |
| allowed_track_types |enum |SD_ONLY ou SD_HD. Controla quais chaves de conteúdo devem ser incluídas em uma licença |
| content_key_specs |matriz de estruturas JSON, confira **Especificações de chave de conteúdo** abaixo |Um controle mais preciso sobre qual conteúdo chaves tooreturn. Confira Especificações de chave de conteúdo a seguir para obter detalhes.  Apenas um entre allowed_track_types e content_key_specs pode ser especificado. |
| use_policy_overrides_exclusively |booliano. true ou false |Use os atributos de política especificados por policy_overrides e omita todas as políticas armazenadas anteriormente. |
| policy_overrides |Estrutura JSON, confira **Substituições de política** abaixo |Configurações de política para esta licença.  No evento de saudação ativo tem uma política predefinida, esses valores especificados serão usados. |
| session_init |Estrutura JSON, confira **Inicialização da sessão** abaixo |Dados opcionais passado toolicense. |
| parse_only |booliano. true ou false |solicitação de licença Olá é analisada, mas nenhuma licença é emitida. No entanto, a solicitação de licença de saudação de formulário de valores são retornados na resposta de hello. |

## <a name="content-key-specs"></a>Especificações de chave de conteúdo
Se existir uma política já existente, não há nenhum toospecify necessidade qualquer Olá valores em Olá especificação de chave de conteúdo.  Olá uma diretiva preexistente associada a esse conteúdo será usado toodetermine Olá saída proteção como HDCP e CGMS.  Se uma política pré-existente não estiver registrada com o servidor de licenças Widevine de hello, provedor de conteúdo de saudação pode injetar valores hello na solicitação de licença hello.   

Cada content_key_specs deve ser especificado para todas as faixas, independentemente de saudação opção use_policy_overrides_exclusively. 

| Nome | Valor | Descrição |
| --- | --- | --- |
| content_key_specs. track_type |string |Um nome de tipo de controle. Se content_key_specs for especificado na solicitação de licença hello, explicitamente tornar toospecify-se de que todos os controlam como tipos. Falha toodo portanto resultará em falha tooplayback últimos 10 segundos. |
| content_key_specs  <br/> security_level |uint32 |Define os requisitos de robustez de reprodução do cliente. <br/> 1 - É necessário aplicar a criptografia whitebox baseada em software. <br/> 2 - É necessário aplicar a criptografia de software e um decodificador ofuscado. <br/> 3 - operações de criptografia e material de chave de Olá devem ser executadas em um ambiente de execução confiável de backup de hardware. <br/> 4 - Olá, criptografia e decodificação de conteúdo deve ser executada em um ambiente de execução confiável de backup de hardware.  <br/> 5 - Olá, criptografia e decodificação todos manipulação de mídia hello (compactado e descompactado) deve ser tratado em um ambiente de execução confiável de backup de hardware. |
| content_key_specs <br/> required_output_protection.hdc |cadeia de caracteres - uma das seguintes: HDCP_NONE, HDCP_V1, HDCP_V2 |Indica se HDCP é necessário |
| content_key_specs <br/>chave |Cadeia codificada em  <br/>Base64 |Conteúdo toouse chave para este controle. Se especificado, Olá track_type ou key_id é necessário.  Esta opção permite ao provedor de conteúdo de saudação chave de conteúdo tooinject Olá para esta faixa em vez de deixar o servidor de licenças Widevine gerar ou de uma chave de pesquisa. |
| content_key_specs.key_id |Binário de cadeia de caracteres codificada em Base64, 16 bytes |Identificador exclusivo para a chave de saudação. |

## <a name="policy-overrides"></a>Substituições de política
| Nome | Valor | Descrição |
| --- | --- | --- |
| policy_overrides. can_play |booliano. true ou false |Indica que a reprodução de saudação conteúdo é permitido. O padrão é falso. |
| policy_overrides. can_persist |booliano. true ou false |Indica a que licença Olá pode ser persistente toonon volátil para uso offline. O padrão é falso. |
| policy_overrides. can_renew |booliano true ou false |Indica que a renovação dessa licença é permitida. Se true, duração de saudação da licença Olá pode ser estendida por pulsação. O padrão é falso. |
| policy_overrides. license_duration_seconds |int64 |Indica a janela de tempo de saudação para esta licença específica. Um valor de 0 indica que não há nenhuma duração toohello de limite. O padrão é 0. |
| policy_overrides. rental_duration_seconds |int64 |Indica a janela de tempo de saudação enquanto a reprodução é permitida. Um valor de 0 indica que não há nenhuma duração toohello de limite. O padrão é 0. |
| policy_overrides. playback_duration_seconds |int64 |Olá exibindo a janela de tempo depois de reprodução é iniciada dentro de duração de licença hello. Um valor de 0 indica que não há nenhuma duração toohello de limite. O padrão é 0. |
| policy_overrides. renewal_server_url |string |Todas as solicitações de pulsação (renovação) para esta licença deverão ser direcionadas toohello especificou a URL. Este campo só será usado se can_renew for true. |
| policy_overrides. renewal_delay_seconds |int64 |O número de segundos após license_start_time, antes da primeira tentativa de renovação. Este campo só será usado se can_renew for true. O padrão é 0 |
| policy_overrides. renewal_retry_interval_seconds |int64 |Especifica o atraso de saudação em segundos entre as solicitações de renovação da licença subsequentes, em caso de falha. Este campo só será usado se can_renew for true. |
| policy_overrides. renewal_recovery_duration_seconds |int64 |saudação de tempo, em que a reprodução tem toocontinue durante a renovação é janela tentativa ainda malsucedida devido toobackend problemas com o servidor de licença de saudação. Um valor de 0 indica que não há nenhuma duração toohello de limite. Este campo só será usado se can_renew for true. |
| policy_overrides. renew_with_usage |booliano true ou false |Indica a que licença Olá deverão ser enviada para a renovação quando uso for iniciado. Este campo só será usado se can_renew for true. |

## <a name="session-initialization"></a>Inicialização da sessão
| Nome | Valor | Descrição |
| --- | --- | --- |
| provider_session_token |Cadeia codificada em Base64 |Esse token de sessão for repassado em licença hello e existirá renovações subsequentes.  o token de sessão Olá não persistirá além de sessões. |
| provider_client_token |Cadeia codificada em Base64 |Cliente toosend token em resposta de licença hello.  Se a solicitação de licença Olá contém um token de cliente, esse valor é ignorado. token de cliente Olá persistirá além de sessões de licença. |
| override_provider_client_token |booliano. true ou false |Se a solicitação de licença false e hello contém um token de cliente, use o token de saudação do solicitação Olá mesmo se um token de cliente foi especificado nessa estrutura.  Se true, sempre use o token Olá especificado nessa estrutura. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Configurar suas licenças do Widevine usando tipos .NET
Os Serviços de Mídia fornecem APIs .NET que permitem a configuração de suas licenças do Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Classes, conforme definido no SDK do Media Services .NET de saudação
Olá seguem definições Olá desses tipos.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Exemplo
Olá mostrado no exemplo a seguir como toouse APIs .NET tooconfigure uma licença Widevine simple.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Usando a PlayReady e/ou a Criptografia Comum Dinâmica Widevine](media-services-protect-with-drm.md)

