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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="5da49-103">Como toouse Olá Inspetor API tootrace chama no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="5da49-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="5da49-104">API de gerenciamento fornece um Inspetor de API toohelp ferramenta de depuração e suas APIs de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="5da49-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="5da49-105">Olá Inspetor de API pode ser usado de forma programática e também pode ser usado diretamente do portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="5da49-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="5da49-106">Além disso tootracing operações, Inspetor de API também rastreia [expressão de diretiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) avaliações.</span><span class="sxs-lookup"><span data-stu-id="5da49-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="5da49-107">Para ver uma demonstração, consulte [nuvem abrangem episódio 177: recursos de gerenciamento de API mais](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too21:00.</span><span class="sxs-lookup"><span data-stu-id="5da49-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="5da49-108">Este guia fornece uma explicação da utilização do Inspetor de API.</span><span class="sxs-lookup"><span data-stu-id="5da49-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="5da49-109">Inspetor de API rastreamentos só são gerados e disponibilizados para solicitações que contêm as chaves de assinatura que pertencem a toohello [administrador](api-management-howto-create-groups.md) conta.</span><span class="sxs-lookup"><span data-stu-id="5da49-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="5da49-110"><a name="trace-call"></a> Tootrace Inspetor de API use uma chamada</span><span class="sxs-lookup"><span data-stu-id="5da49-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="5da49-111">toouse Inspetor de API, adicione um **ocp-apim de rastreamento: true** cabeçalho tooyour operação chamada, de solicitação e, em seguida, baixar e inspecionar rastreamento hello usando URL Olá indicado pelo Olá **ocp-apim rastreamento local** cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="5da49-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="5da49-112">Isso pode ser feito de maneira programática e também pode ser feito diretamente do portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="5da49-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="5da49-113">Este tutorial mostra como as operações de tootrace Inspetor Olá API toouse usando Olá API de calculadora básica que está configurado no hello [gerenciar sua primeira API](api-management-get-started.md) tutorial de Introdução.</span><span class="sxs-lookup"><span data-stu-id="5da49-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="5da49-114">Se você ainda não concluiu o tutorial leva apenas Olá tooimport de alguns instantes API de calculadora básica, ou você pode usar a API de outro de sua escolha, como Olá Echo API.</span><span class="sxs-lookup"><span data-stu-id="5da49-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="5da49-115">Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="5da49-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="5da49-116">Olá Echo API retorna qualquer entrada é enviada tooit.</span><span class="sxs-lookup"><span data-stu-id="5da49-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="5da49-117">toouse-lo, você pode chamar qualquer verbo HTTP, e o valor de retorno hello serão apenas o que você enviou.</span><span class="sxs-lookup"><span data-stu-id="5da49-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="5da49-118">tooget iniciado, clique em **portal do desenvolvedor** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="5da49-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="5da49-119">Operações podem ser chamadas diretamente no portal do desenvolvedor Olá que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API.</span><span class="sxs-lookup"><span data-stu-id="5da49-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="5da49-120">Se você ainda não criou uma instância de serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5da49-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portal do desenvolvedor do Gerenciamento da API][api-management-developer-portal-menu]

<span data-ttu-id="5da49-122">Clique em **APIs** no menu superior hello e clique **Calculadora básica**.</span><span class="sxs-lookup"><span data-stu-id="5da49-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![API de Eco][api-management-api]

<span data-ttu-id="5da49-124">Clique em **Experimente** tootry Olá **adicionar dois inteiros** operação.</span><span class="sxs-lookup"><span data-stu-id="5da49-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Experimente][api-management-open-console]

<span data-ttu-id="5da49-126">Manter valores de parâmetro padrão hello e chave de assinatura selecione Olá para produto Olá desejado toouse de saudação **chave de assinatura** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="5da49-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="5da49-127">Por padrão no Olá Olá portal do desenvolvedor **Ocp-Apim-rastreamento** cabeçalho já está definido muito**true**.</span><span class="sxs-lookup"><span data-stu-id="5da49-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="5da49-128">Esse cabeçalho define se um rastreamento é gerado ou não.</span><span class="sxs-lookup"><span data-stu-id="5da49-128">This header configures whether or not a trace is generated.</span></span>

![Enviar][api-management-http-get]

<span data-ttu-id="5da49-130">Clique em **enviar** tooinvoke operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5da49-130">Click **Send** tooinvoke hello operation.</span></span>

![Enviar][api-management-send-results]

<span data-ttu-id="5da49-132">Em resposta Olá cabeçalhos será um **ocp-apim rastreamento local** com um toohello semelhante valor exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5da49-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="5da49-133">rastreamento de saudação pode ser baixado do hello local especificado e revisadas conforme demonstrado na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="5da49-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="5da49-134">Observe que apenas Olá últimas 100 entradas de log são armazenadas e locais de log são reutilizados em rotação.</span><span class="sxs-lookup"><span data-stu-id="5da49-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="5da49-135">Portanto, se você fazer mais de 100 chamadas com o rastreamento ativado, eventualmente, você irá iniciar substituindo rastreamentos de saudação primeiro em vigor.</span><span class="sxs-lookup"><span data-stu-id="5da49-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="5da49-136"><a name="inspect-trace"></a>Inspecionar rastreamento Olá</span><span class="sxs-lookup"><span data-stu-id="5da49-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="5da49-137">tooreview valores hello rastreamento Olá, baixe o arquivo de rastreamento de saudação do hello **ocp-apim rastreamento local** URL.</span><span class="sxs-lookup"><span data-stu-id="5da49-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="5da49-138">Ele é um arquivo de texto no formato JSON e contém entradas toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5da49-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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

## <span data-ttu-id="5da49-139"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5da49-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="5da49-140">Assista a uma demonstração das expressões da política de rastreamento no [Episódio 177 do Cloud Cover: mais recursos de Gerenciamento de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="5da49-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="5da49-141">Demonstração de saudação do avanço too21:00 toosee.</span><span class="sxs-lookup"><span data-stu-id="5da49-141">Fast-forward too21:00 toosee hello demo.</span></span>

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




