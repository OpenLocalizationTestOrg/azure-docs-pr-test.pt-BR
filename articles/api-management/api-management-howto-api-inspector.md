---
title: Rastrear chamadas com o Inspetor de API - Gerenciamento de API do Azure | Microsoft Docs
description: Saiba como rastrear chamadas usando o Inspetor de API no Gerenciamento de API do Azure.
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
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="b22e1-103">Como usar o Inspetor de API para rastrear chamadas no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="b22e1-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="b22e1-104">O Gerenciamento de API oferece uma ferramenta de Inspetor de API para ajudá-lo a depurar e solucionar problemas de suas APIs.</span><span class="sxs-lookup"><span data-stu-id="b22e1-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="b22e1-105">O Inspetor de API pode ser usado de forma programática e pode também ser usado diretamente do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b22e1-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="b22e1-106">Além das operações de rastreamento, o Inspetor de API também rastreia as avaliações de [expressão de política](https://msdn.microsoft.com/library/azure/dn910913.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b22e1-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="b22e1-107">Para assistir a uma demonstração, confira o [Episódio 177 do Cloud Cover: mais recursos de Gerenciamento de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e avance até 21:00.</span><span class="sxs-lookup"><span data-stu-id="b22e1-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="b22e1-108">Este guia fornece uma explicação da utilização do Inspetor de API.</span><span class="sxs-lookup"><span data-stu-id="b22e1-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="b22e1-109">Os rastreamentos de um Inspetor de API são gerados e disponibilizados somente para solicitações que contêm chaves de assinatura que pertencem à conta de [administrador](api-management-howto-create-groups.md) .</span><span class="sxs-lookup"><span data-stu-id="b22e1-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="b22e1-110"><a name="trace-call"> </a> Usar o Inspetor de API para rastrear uma chamada</span><span class="sxs-lookup"><span data-stu-id="b22e1-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="b22e1-111">Para usar o Inspetor de API, adicione um cabeçalho de solicitação **ocp-apim-trace: true** à sua chamada de operação, baixe e inspecione o rastreamento utilizando a URL indicada pelo cabeçalho de resposta **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="b22e1-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="b22e1-112">Isso pode ser feito de forma programática ou diretamente a partir do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b22e1-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="b22e1-113">Este tutorial mostra como usar o Inspetor de API para operações de rastreamento usando a API de Calculadora Básica configurada no tutorial de introdução [Gerenciar sua primeira API](api-management-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="b22e1-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="b22e1-114">Se você ainda não concluiu esse tutorial, leva apenas alguns minutos para importar a API de Calculadora Básica; outra opção é usar outra API de sua escolha, como a API de Eco.</span><span class="sxs-lookup"><span data-stu-id="b22e1-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="b22e1-115">Cada instância de serviço de Gerenciamento de API vem pré-configurada com uma API de ECO que pode ser usada para experimentar e aprender sobre o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b22e1-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="b22e1-116">A API de ECO retorna qualquer entrada enviada a ela.</span><span class="sxs-lookup"><span data-stu-id="b22e1-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="b22e1-117">Para usá-la, você pode invocar qualquer verbo HTTP e o valor retornado será simplesmente o que você tiver enviado.</span><span class="sxs-lookup"><span data-stu-id="b22e1-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="b22e1-118">Para começar, clique no **Portal do desenvolvedor** no Portal do Azure para seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b22e1-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="b22e1-119">As operações podem ser chamadas diretamente do portal do desenvolvedor, que fornece uma maneira conveniente de exibir e testar as operações de uma API.</span><span class="sxs-lookup"><span data-stu-id="b22e1-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="b22e1-120">Se você ainda não criou uma instância do serviço de Gerenciamento de API, veja [Criar uma instância do serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b22e1-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portal do desenvolvedor do Gerenciamento da API][api-management-developer-portal-menu]

<span data-ttu-id="b22e1-122">Clique em **APIs** no menu superior e depois clique em **Calculadora Básica**.</span><span class="sxs-lookup"><span data-stu-id="b22e1-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![API de Eco][api-management-api]

<span data-ttu-id="b22e1-124">Clique em **Experimentar** para experimentar a operação **Adicionar dois inteiros**.</span><span class="sxs-lookup"><span data-stu-id="b22e1-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Experimente][api-management-open-console]

<span data-ttu-id="b22e1-126">Mantenha os valores de parâmetros padrão e selecione a chave de assinatura do produto que deseja usar no menu suspenso **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="b22e1-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="b22e1-127">Por padrão, no portal do desenvolvedor, o cabeçalho **Ocp-Apim-Trace** já está definido como **true**.</span><span class="sxs-lookup"><span data-stu-id="b22e1-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="b22e1-128">Esse cabeçalho define se um rastreamento é gerado ou não.</span><span class="sxs-lookup"><span data-stu-id="b22e1-128">This header configures whether or not a trace is generated.</span></span>

![Enviar][api-management-http-get]

<span data-ttu-id="b22e1-130">Clique em **Enviar** para invocar a operação.</span><span class="sxs-lookup"><span data-stu-id="b22e1-130">Click **Send** to invoke the operation.</span></span>

![Enviar][api-management-send-results]

<span data-ttu-id="b22e1-132">Nos cabeçalhos de resposta, haverá um **ocp-apim-trace-location** com um valor semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b22e1-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="b22e1-133">O rastreamento pode ser baixado do local especificado e revisado, conforme demonstrado na etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="b22e1-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="b22e1-134">Observe que apenas as últimas 100 entradas de log são armazenadas e os locais de log são reutilizados no esquema rotativo.</span><span class="sxs-lookup"><span data-stu-id="b22e1-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="b22e1-135">Portanto, se você fizer mais de 100 chamadas com rastreamento habilitado, consequentemente iniciará a substituição dos primeiros rastreamentos em vigor.</span><span class="sxs-lookup"><span data-stu-id="b22e1-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="b22e1-136"><a name="inspect-trace"> </a>Inspecionar o rastreamento</span><span class="sxs-lookup"><span data-stu-id="b22e1-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="b22e1-137">Para revisar os valores no rastreamento, baixe o arquivo de rastreamento da URL **ocp-apim-trace-location** .</span><span class="sxs-lookup"><span data-stu-id="b22e1-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="b22e1-138">Trata-se de um texto no formato JSON que contém entradas semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b22e1-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

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
                    "message": "Request is being forwarded to the backend service.",
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
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="b22e1-139"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b22e1-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="b22e1-140">Assista a uma demonstração das expressões da política de rastreamento no [Episódio 177 do Cloud Cover: mais recursos de Gerenciamento de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="b22e1-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="b22e1-141">Avance até 21:00 para assistir à demonstração.</span><span class="sxs-lookup"><span data-stu-id="b22e1-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
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




