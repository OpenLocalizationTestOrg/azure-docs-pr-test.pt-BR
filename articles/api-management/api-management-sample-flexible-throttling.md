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
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="61efa-103">Limitação de solicitação avançada com o Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="61efa-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="61efa-104">Ser capaz de toothrottle as solicitações de entrada é uma função-chave de gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="61efa-104">Being able toothrottle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="61efa-105">Por controlar taxa de saudação de solicitações ou Olá total de solicitações/dados transferidos, permite o gerenciamento de API API provedores tooprotect suas APIs de abuso e criar um valor para diferentes camadas de produto de API.</span><span class="sxs-lookup"><span data-stu-id="61efa-105">Either by controlling hello rate of requests or hello total requests/data transferred, API Management allows API providers tooprotect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="61efa-106">Limitação baseada em produto</span><span class="sxs-lookup"><span data-stu-id="61efa-106">Product based throttling</span></span>
<span data-ttu-id="61efa-107">toodate, recursos de limitação de taxa de saudação foi limitado toobeing no escopo tooa determinado produto assinatura (essencialmente uma chave), definido no hello portal de gerenciamento de API do publicador.</span><span class="sxs-lookup"><span data-stu-id="61efa-107">toodate, hello rate throttling capabilities have been limited toobeing scoped tooa particular Product subscription (essentially a key), defined in hello API Management publisher portal.</span></span> <span data-ttu-id="61efa-108">Isso é útil para Olá API provedor tooapply limites desenvolvedores Olá que se inscreveram toouse API, no entanto, isso não ajuda, por exemplo, na limitação de usuários finais individuais de saudação API.</span><span class="sxs-lookup"><span data-stu-id="61efa-108">This is useful for hello API provider tooapply limits on hello developers who have signed up toouse their API, however, it does not help, for example, in throttling individual end-users of hello API.</span></span> <span data-ttu-id="61efa-109">É possível que o usuário único do tooconsume de aplicativo do desenvolvedor Olá Olá cota e, em seguida, impedir que outros clientes de desenvolvedor Olá toouse capaz de aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="61efa-109">It is possible that for single user of hello developer's application tooconsume hello entire quota and then prevent other customers of hello developer from being able toouse hello application.</span></span> <span data-ttu-id="61efa-110">Além disso, vários clientes que podem gerar um grande volume de solicitações podem limitar acesso toooccasional usuários.</span><span class="sxs-lookup"><span data-stu-id="61efa-110">Also, several customers who might generate a high volume of requests may limit access toooccasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="61efa-111">Limitação baseada em chave personalizada</span><span class="sxs-lookup"><span data-stu-id="61efa-111">Custom key based throttling</span></span>
<span data-ttu-id="61efa-112">Olá novo [limite de taxa por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas fornecem um controle tootraffic significativamente mais flexível.</span><span class="sxs-lookup"><span data-stu-id="61efa-112">hello new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution tootraffic control.</span></span> <span data-ttu-id="61efa-113">Essas novas políticas permitem toodefine expressões tooidentify Olá as chaves que serão usados tootrack utilização de tráfego.</span><span class="sxs-lookup"><span data-stu-id="61efa-113">These new policies allow you toodefine expressions tooidentify hello keys that will be used tootrack traffic usage.</span></span> <span data-ttu-id="61efa-114">Isso funciona de maneira de Hello mais fácil é ilustrada com um exemplo.</span><span class="sxs-lookup"><span data-stu-id="61efa-114">hello way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="61efa-115">Limitação de endereço IP</span><span class="sxs-lookup"><span data-stu-id="61efa-115">IP Address throttling</span></span>
<span data-ttu-id="61efa-116">as seguintes políticas Hello restringem um único cliente IP endereço tooonly 10 chama a cada minuto, com um total de 1.000.000 chamadas e 10.000 quilobytes de largura de banda por mês.</span><span class="sxs-lookup"><span data-stu-id="61efa-116">hello following policies restrict a single client IP address tooonly 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="61efa-117">Se todos os clientes na Internet de saudação usaram um endereço IP exclusivo, isso pode ser uma maneira eficiente de limitar o uso por usuário.</span><span class="sxs-lookup"><span data-stu-id="61efa-117">If all clients on hello Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="61efa-118">No entanto, é muito provável que vários usuários irão compartilhar um único endereço IP público devido Olá acessando toothem da Internet por meio de um dispositivo NAT.</span><span class="sxs-lookup"><span data-stu-id="61efa-118">However, it is quite likely that multiple users will sharing a single public IP address due toothem accessing hello Internet via a NAT device.</span></span> <span data-ttu-id="61efa-119">Apesar de isso, APIs que permitem a saudação de acesso não autenticado `IpAddress` pode ser a melhor opção de saudação.</span><span class="sxs-lookup"><span data-stu-id="61efa-119">Despite this, for APIs that allow unauthenticated access hello `IpAddress` might be hello best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="61efa-120">Limitação de identidade do usuário</span><span class="sxs-lookup"><span data-stu-id="61efa-120">User identity throttling</span></span>
<span data-ttu-id="61efa-121">Se um usuário final for autenticado, uma chave de limitação poderá ser gerada com base nas informações que identificam esse usuário exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="61efa-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="61efa-122">Neste exemplo, extrair o cabeçalho de autorização hello, convertê-lo muito`JWT` do objeto e usar assunto de saudação do usuário de saudação do hello tooidentify token e usá-lo como chave de limitação de taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="61efa-122">In this example we extract hello Authorization header, convert it too`JWT` object and use hello subject of hello token tooidentify hello user and use that as hello rate limiting key.</span></span> <span data-ttu-id="61efa-123">Se a identidade do usuário Olá é armazenada em Olá `JWT` como uma saudação outra declarações depois que o valor pode ser usado em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="61efa-123">If hello user identity is stored in hello `JWT` as one of hello other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="61efa-124">Políticas combinadas</span><span class="sxs-lookup"><span data-stu-id="61efa-124">Combined policies</span></span>
<span data-ttu-id="61efa-125">Embora Olá limitação novas políticas de fornece mais controle que Olá existente as políticas de limitação, ainda há valor combinando os dois recursos.</span><span class="sxs-lookup"><span data-stu-id="61efa-125">Although hello new throttling policies provide more control than hello existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="61efa-126">Limitação por chave de assinatura do produto ([limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [definir cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) é uma ótima maneira de tooenable monetizing de uma API ao cobrar com base nos níveis de uso.</span><span class="sxs-lookup"><span data-stu-id="61efa-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way tooenable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="61efa-127">Hello controle mais preciso de ser capaz de toothrottle pelo usuário é um complemento e impede que o comportamento de um usuário afetar a experiência de saudação do outro.</span><span class="sxs-lookup"><span data-stu-id="61efa-127">hello finer grained control of being able toothrottle by user is complementary and prevents one user's behavior from degrading hello experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="61efa-128">Limitação controlada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="61efa-128">Client driven throttling</span></span>
<span data-ttu-id="61efa-129">Quando Olá limitação chave é definida usando um [expressão de diretiva](https://msdn.microsoft.com/library/azure/dn910913.aspx), é provedor Olá API que escolher como Olá limitação tem seu escopo definido.</span><span class="sxs-lookup"><span data-stu-id="61efa-129">When hello throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is hello API provider that is choosing how hello throttling is scoped.</span></span> <span data-ttu-id="61efa-130">No entanto, um desenvolvedor pode ser toocontrol como classificam limitar seus clientes.</span><span class="sxs-lookup"><span data-stu-id="61efa-130">However, a developer might want toocontrol how they rate limit their own customers.</span></span> <span data-ttu-id="61efa-131">Isso pôde ser ativado pelo provedor de API Olá introduzindo cliente aplicativo toocommunicate Olá chave toohello um cabeçalho personalizado tooallow Olá desenvolvedor API.</span><span class="sxs-lookup"><span data-stu-id="61efa-131">This could be enabled by hello API provider by introducing a custom header tooallow hello developer's client application toocommunicate hello key toohello API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="61efa-132">Isso permite que toochoose de aplicativo do cliente do desenvolvedor hello como quiserem chave de limitação de taxa de saudação de toocreate.</span><span class="sxs-lookup"><span data-stu-id="61efa-132">This enables hello developer's client application toochoose how they want toocreate hello rate limiting key.</span></span> <span data-ttu-id="61efa-133">Com um pouco de criatividade um desenvolvedor de cliente pode criar seus próprios níveis de taxa alocando conjuntos de chaves toousers e rotação de uso de chave hello.</span><span class="sxs-lookup"><span data-stu-id="61efa-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys toousers and rotating hello key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="61efa-134">Resumo</span><span class="sxs-lookup"><span data-stu-id="61efa-134">Summary</span></span>
<span data-ttu-id="61efa-135">Gerenciamento de API do Azure fornece taxa aspas limitação tooboth proteger e adicionar o serviço de API do valor tooyour.</span><span class="sxs-lookup"><span data-stu-id="61efa-135">Azure API Management provides rate and quote throttling tooboth protect and add value tooyour API service.</span></span> <span data-ttu-id="61efa-136">Olá limitação novas políticas com as regras de escopo personalizadas permite a que você mais refinada controle sobre as políticas tooenable aplicativos clientes toobuild ainda melhores.</span><span class="sxs-lookup"><span data-stu-id="61efa-136">hello new throttling policies with custom scoping rules allow you finer grained control over those policies tooenable your customers toobuild even better applications.</span></span> <span data-ttu-id="61efa-137">exemplos de saudação neste artigo demonstram o uso de saudação dessas novas políticas por chaves com endereços IP do cliente, a identidade do usuário e valores de cliente gerado de limitação de taxa de produção.</span><span class="sxs-lookup"><span data-stu-id="61efa-137">hello examples in this article demonstrate hello use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="61efa-138">No entanto, há muitas outras partes da mensagem de saudação que pode ser usado como agente de usuário, fragmentos de caminho de URL, o tamanho da mensagem.</span><span class="sxs-lookup"><span data-stu-id="61efa-138">However, there are many other parts of hello message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61efa-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61efa-139">Next steps</span></span>
<span data-ttu-id="61efa-140">Por favor, forneça seus comentários no thread do Disqus Olá deste tópico.</span><span class="sxs-lookup"><span data-stu-id="61efa-140">Please give us your feedback in hello Disqus thread for this topic.</span></span> <span data-ttu-id="61efa-141">Seria ótimo toohear sobre outros possíveis valores de chave que foram uma opção lógica em seus cenários.</span><span class="sxs-lookup"><span data-stu-id="61efa-141">It would be great toohear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="61efa-142">Assista a uma visão geral dessas políticas em vídeo</span><span class="sxs-lookup"><span data-stu-id="61efa-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="61efa-143">Para obter mais informações sobre Olá [limite de taxa por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas abordadas neste artigo, assista Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="61efa-143">For more information on hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

