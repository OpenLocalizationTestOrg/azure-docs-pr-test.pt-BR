---
title: "solicitação de aaaAdvanced limitação com gerenciamento de API do Azure"
description: "Saiba como toocreate e aplicar cota flexível e políticas de gerenciamento de API do Azure de limitação de taxa."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Limitação de solicitação avançada com o Gerenciamento de API do Azure
Ser capaz de toothrottle as solicitações de entrada é uma função-chave de gerenciamento de API do Azure. Por controlar taxa de saudação de solicitações ou Olá total de solicitações/dados transferidos, permite o gerenciamento de API API provedores tooprotect suas APIs de abuso e criar um valor para diferentes camadas de produto de API.

## <a name="product-based-throttling"></a>Limitação baseada em produto
toodate, recursos de limitação de taxa de saudação foi limitado toobeing no escopo tooa determinado produto assinatura (essencialmente uma chave), definido no hello portal de gerenciamento de API do publicador. Isso é útil para Olá API provedor tooapply limites desenvolvedores Olá que se inscreveram toouse API, no entanto, isso não ajuda, por exemplo, na limitação de usuários finais individuais de saudação API. É possível que o usuário único do tooconsume de aplicativo do desenvolvedor Olá Olá cota e, em seguida, impedir que outros clientes de desenvolvedor Olá toouse capaz de aplicativo de hello. Além disso, vários clientes que podem gerar um grande volume de solicitações podem limitar acesso toooccasional usuários.

## <a name="custom-key-based-throttling"></a>Limitação baseada em chave personalizada
Olá novo [limite de taxa por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas fornecem um controle tootraffic significativamente mais flexível. Essas novas políticas permitem toodefine expressões tooidentify Olá as chaves que serão usados tootrack utilização de tráfego. Isso funciona de maneira de Hello mais fácil é ilustrada com um exemplo. 

## <a name="ip-address-throttling"></a>Limitação de endereço IP
as seguintes políticas Hello restringem um único cliente IP endereço tooonly 10 chama a cada minuto, com um total de 1.000.000 chamadas e 10.000 quilobytes de largura de banda por mês. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Se todos os clientes na Internet de saudação usaram um endereço IP exclusivo, isso pode ser uma maneira eficiente de limitar o uso por usuário. No entanto, é muito provável que vários usuários irão compartilhar um único endereço IP público devido Olá acessando toothem da Internet por meio de um dispositivo NAT. Apesar de isso, APIs que permitem a saudação de acesso não autenticado `IpAddress` pode ser a melhor opção de saudação.

## <a name="user-identity-throttling"></a>Limitação de identidade do usuário
Se um usuário final for autenticado, uma chave de limitação poderá ser gerada com base nas informações que identificam esse usuário exclusivamente.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

Neste exemplo, extrair o cabeçalho de autorização hello, convertê-lo muito`JWT` do objeto e usar assunto de saudação do usuário de saudação do hello tooidentify token e usá-lo como chave de limitação de taxa de saudação. Se a identidade do usuário Olá é armazenada em Olá `JWT` como uma saudação outra declarações depois que o valor pode ser usado em seu lugar.

## <a name="combined-policies"></a>Políticas combinadas
Embora Olá limitação novas políticas de fornece mais controle que Olá existente as políticas de limitação, ainda há valor combinando os dois recursos. Limitação por chave de assinatura do produto ([limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [definir cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) é uma ótima maneira de tooenable monetizing de uma API ao cobrar com base nos níveis de uso. Hello controle mais preciso de ser capaz de toothrottle pelo usuário é um complemento e impede que o comportamento de um usuário afetar a experiência de saudação do outro. 

## <a name="client-driven-throttling"></a>Limitação controlada pelo cliente
Quando Olá limitação chave é definida usando um [expressão de diretiva](https://msdn.microsoft.com/library/azure/dn910913.aspx), é provedor Olá API que escolher como Olá limitação tem seu escopo definido. No entanto, um desenvolvedor pode ser toocontrol como classificam limitar seus clientes. Isso pôde ser ativado pelo provedor de API Olá introduzindo cliente aplicativo toocommunicate Olá chave toohello um cabeçalho personalizado tooallow Olá desenvolvedor API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Isso permite que toochoose de aplicativo do cliente do desenvolvedor hello como quiserem chave de limitação de taxa de saudação de toocreate. Com um pouco de criatividade um desenvolvedor de cliente pode criar seus próprios níveis de taxa alocando conjuntos de chaves toousers e rotação de uso de chave hello.

## <a name="summary"></a>Resumo
Gerenciamento de API do Azure fornece taxa aspas limitação tooboth proteger e adicionar o serviço de API do valor tooyour. Olá limitação novas políticas com as regras de escopo personalizadas permite a que você mais refinada controle sobre as políticas tooenable aplicativos clientes toobuild ainda melhores. exemplos de saudação neste artigo demonstram o uso de saudação dessas novas políticas por chaves com endereços IP do cliente, a identidade do usuário e valores de cliente gerado de limitação de taxa de produção. No entanto, há muitas outras partes da mensagem de saudação que pode ser usado como agente de usuário, fragmentos de caminho de URL, o tamanho da mensagem.

## <a name="next-steps"></a>Próximas etapas
Por favor, forneça seus comentários no thread do Disqus Olá deste tópico. Seria ótimo toohear sobre outros possíveis valores de chave que foram uma opção lógica em seus cenários.

## <a name="watch-a-video-overview-of-these-policies"></a>Assista a uma visão geral dessas políticas em vídeo
Para obter mais informações sobre Olá [limite de taxa por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas abordadas neste artigo, assista Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

