---
title: aaaAdd cache tooimprove desempenho no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como latência de saudação tooimprove, consumo de largura de banda e serviço web de carga para chamadas de serviço de gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Adicionar cache tooimprove desempenho no gerenciamento de API do Azure
É possível configurar as operações do Gerenciamento de API para cache das respostas. O cache das respostas pode reduzir significativamente a latência da API, o consumo da largura de banda e a carga de serviço Web para dados que não são alterados com frequência.

Este guia mostra como tooadd resposta para a sua API de cache e configurar políticas para operações de API de eco do exemplo hello. Em seguida, você pode chamar operação Olá do cache tooverify portal do desenvolvedor do hello em ação.

> [!NOTE]
> Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de saudação seguir as etapas neste guia, você deve ter uma instância do serviço de gerenciamento de API com uma API e um produto configurado. Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.

## <a name="configure-caching"> </a>Configurar uma operação para caching
Nesta etapa, você revisará Olá configurações de saudação de cache **obter recursos (em cache)** operação do exemplo hello Echo API.

> [!NOTE]
> Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API. Para obter mais informações, confira [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].
> 
> 

tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Isso leva toohello portal do publicador de gerenciamento de API.

![Portal do editor][api-management-management-console]

Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **Echo API**.

![API de Eco][api-management-echo-api]

Clique em Olá **operações** guia e, em seguida, clique em Olá **obter recursos (em cache)** operação Olá **operações** lista.

![Operações de API de ECO][api-management-echo-api-operations]

Clique em Olá **cache** Olá tooview de guia Configurações para esta operação de cache.

![Guia Cache][api-management-caching-tab]

tooenable cache para uma operação, selecione Olá **habilitar** caixa de seleção. Neste exemplo, o caching está habilitado.

Cada resposta de operação é organizada com base nos valores Olá Olá **variar por parâmetros de cadeia de caracteres de consulta** e **variam por cabeçalhos** campos. Se você quiser toocache várias respostas com base em parâmetros de cadeia de caracteres de consulta ou cabeçalhos, você pode configurá-los nesses dois campos.

**Duração** Especifica o intervalo de expiração de saudação de respostas de saudação armazenado em cache. Neste exemplo, o intervalo de saudação é **3600** segundos, que é hora de tooone equivalente.

Usando Olá configuração neste exemplo de cache, Olá primeiro toohello de solicitação **obter recursos (em cache)** operação retorna uma resposta do serviço de back-end de saudação. Essa resposta será armazenada, chaveado Olá especificado parâmetros de cadeia de caracteres de cabeçalhos e consulta. Chamadas subsequentes operação toohello, com parâmetros, será necessário Olá armazenados em cache resposta retornada, até que o intervalo de duração do cache de saudação expirou.

## <a name="caching-policies"></a>Olá revisão políticas de cache
Nesta etapa, você examine Olá cache configurações para Olá **obter recursos (em cache)** operação do exemplo hello Echo API.

Quando as configurações de cache são configuradas para uma operação em Olá **cache** guia cache políticas são adicionadas para a operação de saudação. Essas políticas podem ser exibidas e editadas no editor de diretiva de saudação.

Clique em **políticas** de saudação **gerenciamento de API** menu Olá esquerdo e, em seguida, selecione **Echo API / obter recursos (em cache)** de saudação **operação**lista suspensa.

![Operação de escopo da política][api-management-operation-dropdown]

Isso exibe políticas Olá para esta operação no editor de diretiva de saudação.

![Editor de políticas de Gerenciamento de API][api-management-policy-editor]

definição de política de saudação para essa operação inclui Olá as políticas que definem Olá configuração de cache que foram examinadas usando Olá **cache** guia na etapa anterior hello.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> As alterações feitas toohello políticas no editor de diretiva de saudação de cache será refletida no hello **cache** guia de uma operação e vice-versa.
> 
> 

## <a name="test-operation"></a>Chamar uma operação e testar o caching Olá
Olá toosee cache em ação, podemos chamar a operação de saudação do portal do desenvolvedor Olá. Clique em **portal do desenvolvedor** no menu superior direito da saudação.

![Portal do desenvolvedor][api-management-developer-portal-menu]

Clique em **APIs** Olá menu superior e, em seguida, selecione **Echo API**.

![API de Eco][api-management-apis-echo-api]

> Se você tiver apenas uma API configurada ou conta tooyour visível, clique em APIs leva você diretamente toohello operações para essa API.
> 
> 

Selecione Olá **obter recursos (em cache)** operação e depois clique em **abrir o Console**.

![Abrir console][api-management-open-console]

Olá console permite operações tooinvoke diretamente do portal do desenvolvedor hello.

![Console][api-management-console]

Manter valores padrão Olá **param1** e **param2**.

Selecione Olá tecla desejada da saudação **chave de assinatura** lista suspensa. Se a sua conta tiver somente uma assinatura, ela já estará selecionada.

Digite **sampleheader:value1** em Olá **cabeçalhos de solicitação** caixa de texto.

Clique em **HTTP Get** e anote Olá cabeçalhos de resposta.

Digite **sampleheader:value2** em Olá **cabeçalhos de solicitação** caixa de texto e clique **HTTP Get**.

Observe que valor Olá **sampleheader** ainda é **value1** em resposta hello. Tente alguns valores diferentes e observe que Olá a resposta armazenada em cache na primeira chamada de saudação é retornado.

Digite **25** em Olá **param2** campo e, em seguida, clique em **HTTP Get**.

Observe que valor Olá **sampleheader** Olá resposta agora é **value2**. Porque os resultados da operação Olá inseridos pela cadeia de caracteres de consulta, a resposta armazenada em cache anterior de saudação não foi retornada.

## <a name="next-steps"> </a>Próximas etapas
* Para obter mais informações sobre políticas de cache, consulte [políticas de cache] [ Caching policies] em Olá [referência de política de gerenciamento de API][API Management policy reference].
* Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
