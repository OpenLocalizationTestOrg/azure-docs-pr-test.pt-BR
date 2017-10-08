---
title: chamadas de aaaTrace com o Inspetor de API - gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como chamadas tootrace usando Olá Inspetor de API no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Como toouse Olá Inspetor API tootrace chama no gerenciamento de API do Azure
API de gerenciamento fornece um Inspetor de API toohelp ferramenta de depuração e suas APIs de solução de problemas. Olá Inspetor de API pode ser usado de forma programática e também pode ser usado diretamente do portal do desenvolvedor hello. 

Além disso tootracing operações, Inspetor de API também rastreia [expressão de diretiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) avaliações. Para ver uma demonstração, consulte [nuvem abrangem episódio 177: recursos de gerenciamento de API mais](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too21:00.

Este guia fornece uma explicação da utilização do Inspetor de API.

> [!NOTE]
> Inspetor de API rastreamentos só são gerados e disponibilizados para solicitações que contêm as chaves de assinatura que pertencem a toohello [administrador](api-management-howto-create-groups.md) conta.
> 
> 

## <a name="trace-call"></a> Tootrace Inspetor de API use uma chamada
toouse Inspetor de API, adicione um **ocp-apim de rastreamento: true** cabeçalho tooyour operação chamada, de solicitação e, em seguida, baixar e inspecionar rastreamento hello usando URL Olá indicado pelo Olá **ocp-apim rastreamento local** cabeçalho de resposta. Isso pode ser feito de maneira programática e também pode ser feito diretamente do portal do desenvolvedor hello.

Este tutorial mostra como as operações de tootrace Inspetor Olá API toouse usando Olá API de calculadora básica que está configurado no hello [gerenciar sua primeira API](api-management-get-started.md) tutorial de Introdução. Se você ainda não concluiu o tutorial leva apenas Olá tooimport de alguns instantes API de calculadora básica, ou você pode usar a API de outro de sua escolha, como Olá Echo API. Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API. Olá Echo API retorna qualquer entrada é enviada tooit. toouse-lo, você pode chamar qualquer verbo HTTP, e o valor de retorno hello serão apenas o que você enviou. 

tooget iniciado, clique em **portal do desenvolvedor** em hello Portal do Azure para seu serviço de gerenciamento de API. Operações podem ser chamadas diretamente no portal do desenvolvedor Olá que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API.

> Se você ainda não criou uma instância de serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

![Portal do desenvolvedor do Gerenciamento da API][api-management-developer-portal-menu]

Clique em **APIs** no menu superior hello e clique **Calculadora básica**.

![API de Eco][api-management-api]

Clique em **Experimente** tootry Olá **adicionar dois inteiros** operação.

![Experimente][api-management-open-console]

Manter valores de parâmetro padrão hello e chave de assinatura selecione Olá para produto Olá desejado toouse de saudação **chave de assinatura** lista suspensa.

Por padrão no Olá Olá portal do desenvolvedor **Ocp-Apim-rastreamento** cabeçalho já está definido muito**true**. Esse cabeçalho define se um rastreamento é gerado ou não.

![Enviar][api-management-http-get]

Clique em **enviar** tooinvoke operação de saudação.

![Enviar][api-management-send-results]

Em resposta Olá cabeçalhos será um **ocp-apim rastreamento local** com um toohello semelhante valor exemplo a seguir.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

rastreamento de saudação pode ser baixado do hello local especificado e revisadas conforme demonstrado na próxima etapa do hello. Observe que apenas Olá últimas 100 entradas de log são armazenadas e locais de log são reutilizados em rotação. Portanto, se você fazer mais de 100 chamadas com o rastreamento ativado, eventualmente, você irá iniciar substituindo rastreamentos de saudação primeiro em vigor.

## <a name="inspect-trace"></a>Inspecionar rastreamento Olá
tooreview valores hello rastreamento Olá, baixe o arquivo de rastreamento de saudação do hello **ocp-apim rastreamento local** URL. Ele é um arquivo de texto no formato JSON e contém entradas toohello semelhante exemplo a seguir.

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded toohello backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <a name="next-steps"> </a>Próximas etapas
* Assista a uma demonstração das expressões da política de rastreamento no [Episódio 177 do Cloud Cover: mais recursos de Gerenciamento de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Demonstração de saudação do avanço too21:00 toosee.

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




