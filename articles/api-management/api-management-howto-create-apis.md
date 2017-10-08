---
title: aaaHow toocreate APIs no gerenciamento de API do Azure
description: Saiba como toocreate e configurar APIs no gerenciamento de API do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Como toocreate APIs no gerenciamento de API do Azure
Uma API no Gerenciamento de API representa um conjunto de operações que pode ser invocado pelas aplicações clientes. Novas APIs são criadas no portal do publicador hello e, em seguida, Olá desejado operações são adicionadas. Quando as operações de saudação são adicionadas, Olá API é adicionado tooa produto e pode ser publicado. Quando uma API for publicada, pode ser assinado tooand usado por desenvolvedores.

Este guia mostra a primeira etapa de saudação no processo de saudação: como toocreate e configurar uma nova API de gerenciamento de API. Para obter mais informações sobre operações de adicionar e publicar um produto, consulte [como tooadd operações tooan API] [ How tooadd operations tooan API] e [como toocreate e publicar um produto] [ How toocreate and publish a product].

## <a name="create-new-api"> </a>Criar uma nova API
APIs são criados e configurados no portal do publicador hello. tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar API**.

![Criar API][api-management-create-api]

Saudação de uso **adicionar nova API** tooconfigure janela Olá nova API.

![Adicionar nova API][api-management-add-new-api]

Olá campos a seguir é usadas tooconfigure Olá nova API.

* **Nome da API da Web** fornece um nome exclusivo e descritivo para Olá API. Ela é exibida em portais de desenvolvedor e o publicador hello.
* **URL do serviço Web** referências Olá implementando Olá API de serviço HTTP. Gerenciamento de API encaminha solicitações toothis endereço.
* **Sufixo de URL da API da Web** é toohello acrescentadas a URL base para serviço de gerenciamento de API de saudação. URL base Olá é comum para todas as APIs hospedadas por uma instância do serviço de gerenciamento de API. Gerenciamento de API distingue APIs pelo seu sufixo e, portanto, o sufixo Olá deve ser exclusivo para cada API para um determinado publicador.
* **Esquema de URL da API da Web** determina quais protocolos podem ser usados tooaccess Olá API. A HTTPs é especificada por padrão.
* toooptionally adicionar esse novo produto tooa API, clique em Olá **produtos (opcionais)** suspensa e escolha um produto. Esta etapa pode ser repetida várias vezes tooadd Olá API toomultiple produtos.

Depois de saudação desejado valores estão configurados, clique em **salvar**. Depois que Olá nova API é criada, hello página Resumo para a API de saudação é exibida no portal do publicador hello.

![Resumo da API][api-management-api-summary]

## <a name="configure-api-settings"> </a>Definir configurações de API
Você pode usar o hello **configurações** guia tooverify e editar a configuração de saudação de uma API. **Nome da API da Web**, **URL do serviço Web**, e **sufixo de URL da API da Web** são inicialmente definidas quando Olá API é criada e pode ser modificado aqui. **Descrição** fornece uma descrição opcional e **esquema de URL da API da Web** determina quais protocolos podem ser usados tooaccess Olá API.

![Configurações da API][api-management-api-settings]

autenticação de gateway tooconfigure hello de back-end serviço API de implementação hello, selecione Olá **segurança** Olá guia **com credenciais** suspenso pode ser usado tooconfigure **HTTP básico** ou **certificados de cliente** autenticação. a autenticação básica HTTP de toouse, basta digitar as credenciais de saudação desejada. Para obter informações sobre como usar a autenticação de certificado de cliente, consulte [como toosecure serviços de back-end usando o cliente de certificado autenticação no gerenciamento de API do Azure][How toosecure back-end services using client certificate authentication in Azure API Management].

Olá **segurança** guia também pode ser usado tooconfigure **autorização do usuário** usando OAuth 2.0. Para obter mais informações, consulte [como desenvolvedor tooauthorize contas usando OAuth 2.0 no gerenciamento de API do Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Configurações da autenticação Básica][api-management-api-settings-credentials]

Clique em **salvar** toosave qualquer alteração feita toohello configurações de API.

## <a name="next-steps"> </a>Próximas etapas
Depois que uma API é criada e configurações hello, Olá próximas etapas são tooadd Olá operações toohello API, adicionar Olá API tooa produto e publicá-lo para que ele está disponível para desenvolvedores. Para obter mais informações, consulte Olá artigos a seguir.

* [Como as operações de tooadd tooan API][How tooadd operations tooan API]
* [Como toocreate e publicar um produto][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
