---
title: "aaaHow tooadd operações tooan API no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como tooadd operações tooan API no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Como as operações de tooadd tooan API no gerenciamento de API do Azure
Antes que uma API no Gerenciamento de API possa ser usada, as operações devem ser adicionadas. Este guia mostra como tooadd e configurar os diferentes tipos de operações tooan API no gerenciamento de API.

## <a name="add-operation"> </a>Adicionar uma operação
As operações são adicionadas e configurados tooan API no portal do publicador Olá. tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Selecione Olá desejado API no portal do publicador hello e, em seguida, selecione Olá **operações** guia. 

![Operações][api-management-operations]

Clique em **Adicionar operação** tooadd uma nova operação. Olá **nova operação** serão exibidas e Olá **assinatura** guia será selecionada por padrão.

![Adicionar operação][api-management-add-operation]

Especifique a saudação **verbo HTTP** escolhendo na lista suspensa de saudação.

![Método HTTP][api-management-http-method]

<a name="url-template"></a>

Defina modelo de URL Olá digitando em um fragmento de URL que consiste em um ou mais segmentos de caminho de URL e zero ou mais parâmetros de cadeia de caracteres de consulta. modelo de URL Hello, toohello acrescentadas a URL base do hello API, identifica uma única operação HTTP. Ele pode conter uma ou mais partes variáveis nomeadas que são identificadas por chaves. Essas partes variável são chamados de parâmetros de modelo e valores extraídos da URL de solicitação hello quando Olá solicitação está sendo processada pela plataforma de gerenciamento de API de saudação são atribuídos dinamicamente.

> modelo de URL Olá pode incluir padrões de curinga. Por exemplo, especificar `/*` encaminhar todas as solicitações para esse método toohello HTTP volta terminará serviço.

![Modelo do URL][api-management-url-template]

<a name="rewrite-url-template"></a>

Se desejar, especifique Olá **modelo regravar URL**. Isso permite que você modelo de URL padrão do toouse Olá para processar as solicitações de entrada hello front-end, ao chamar hello back-end através de uma URL convertida de acordo com o toohello reconfiguração de modelo. Parâmetros de modelo do modelo de URL Olá devem ser usados no modelo de regravação de saudação. Olá exemplo a seguir mostra como conteúdo tipo codificado como o segmento de caminho no serviço da web de saudação do exemplo anterior Olá pode ser fornecido como um parâmetro de consulta em Olá API publicados por meio de saudação usando modelos de URL de saudação de plataforma de gerenciamento de API.

![Modelo de URL reescrito][api-management-url-template-rewrite]

Operação de toohello chamadores usará o formato de saudação `/customers?customerid=ALFKI` e isso será mapeado muito`/Customers('ALFKI')` quando o serviço de back-end de saudação é invocado.

**Exibição** nome e **descrição** forneça uma descrição da operação de saudação e é usadas tooprovide documentação desenvolvedores toohello usando essa API no portal do desenvolvedor hello.

![Descrição][api-management-description]

Descrição da operação Olá pode ser especificada como texto sem formatação ou HTML em Olá **descrição** caixa de texto.

## <a name="operation-caching"> </a>Cache da operação
Cache de resposta reduz a latência percebida pelos consumidores Olá API, reduz o consumo de largura de banda e diminui Olá carga sobre a implementação do serviço web do hello HTTP Olá API. 

tooeasily e habilitar rapidamente o cache para operação hello, selecione Olá **cache** guia e verifique Olá **habilitar** caixa de seleção.

![Cache][api-management-caching-tab]

**Duração** Especifica o período de tempo durante o qual Olá resposta de operação permanece no cache de saudação de saudação. valor padrão de saudação é 3600 segundos ou 1 hora.

Chaves de cache são toodifferentiate usado entre as respostas para que a resposta de saudação correspondente chave de cache diferentes tooeach obterá seu próprio valor armazenado em cache separado. Opcionalmente, insira parâmetros de cadeia de caracteres de consulta específicos e/ou toobe de cabeçalhos HTTP usada no cálculo de valores de chave de cache em Olá **variar por parâmetros de cadeia de caracteres de consulta** e **variam por cabeçalhos** nas caixas de texto respectivamente. Quando nenhum é especificado, o total de solicitação de URL e Olá valores de cabeçalho HTTP a seguir é usado na geração de chave de cache: **aceitar** e **Accept-Charset**.

> Para obter mais informações sobre o cache e cache de políticas, consulte [como os resultados de operação toocache no gerenciamento de API do Azure][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"> </a>Parâmetros da solicitação
Parâmetros de operação são gerenciados na guia parâmetros de saudação. Parâmetros especificados na Olá **modelo de URL** em Olá **assinatura** guia são adicionados automaticamente e podem ser alteradas somente com a edição do modelo de URL hello. Parâmetros adicionais podem ser inseridos manualmente.

tooadd um novo parâmetro de consulta, clique em **Adicionar parâmetro de consulta** e digite Olá informações a seguir:

* **Nome** - nome do parâmetro.
* **Descrição** -uma breve descrição do parâmetro hello (opcional).
* **Tipo** -tipo de parâmetro selecionado na saudação da lista suspensa.
* **Valores** -valores que podem ser atribuídos toothis parâmetro. Um dos valores de saudação pode ser marcado como padrão (opcional).
* **Necessário** -tornar o parâmetro hello obrigatório, marcando a caixa de seleção de saudação. 

![Parâmetros da solicitação][api-management-request-parameters]

## <a name="request-body"> </a>Corpo da solicitação
Se a operação Olá permite (por exemplo, PUT, POST) e requer um corpo que você pode fornecer um exemplo dele em todos os Olá suporte para formatos de representação (por exemplo, json, XML). 

> corpo da solicitação Olá é usado para fins de documentação somente e não é validado.
> 
> 

tooenter um corpo de solicitação, alternar toohello **corpo** guia.

Clique em **Adicionar representação**, comece a digitar o nome do tipo de conteúdo desejado (por exemplo, application/json), selecione-o no hello suspenso e colar Olá desejado exemplo de corpo de solicitação no formato de saudação selecionado na caixa de texto de saudação. 

![Corpo da solicitação][api-management-request-body]

Em toorepresentations adicionais, você também pode especificar uma descrição de texto opcional na Olá **descrição** caixa de texto.

## <a name="responses"> </a>Respostas
Exemplos de tooprovide uma boa prática de respostas para todos os códigos de status que pode produzir operação Olá é. Cada código de status pode ter mais de um exemplo de corpo de resposta, uma para cada Olá suporte para tipos de conteúdo. 

tooadd uma resposta, clique em **adicionar** e comece a digitar o código de status de saudação desejado. Esse status do exemplo hello código é **200 Okey**. Depois que o código de saudação é exibido na lista suspensa hello, selecioná-la e o código de resposta de saudação é criado e adicionado tooyour operação.

![Código de resposta][api-management-response-code]

Clique em **Adicionar representação**, comece a digitar o nome de tipo de conteúdo desejado hello (por exemplo, application/json) e, em seguida, selecione no hello lista suspensa.

![Tipo de conteúdo do corpo][api-management-response-body-content-type]

Cole o exemplo de corpo de resposta hello no formato selecionado Olá na caixa de texto de hello. 

![Corpo da resposta][api-management-response-body]

Se desejar, adicione uma descrição opcional para Olá **descrição** caixa de texto.

Após configurar a operação de saudação, clique em **salvar**.

## <a name="next-steps"> </a>Próximas etapas
Quando as operações de saudação são adicionadas tooan API, o hello próxima etapa é tooassociate hello API com um produto e publicá-lo para que os desenvolvedores podem chamar suas operações.

* [Como toocreate e publicar um produto][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
