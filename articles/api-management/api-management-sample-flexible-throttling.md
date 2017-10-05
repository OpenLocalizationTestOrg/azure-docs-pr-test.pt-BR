---
title: "Limitação de solicitação avançada com o Gerenciamento de API do Azure"
description: "Saiba como criar e aplicar políticas flexíveis de limitação de cota e de taxa com o Gerenciamento de API do Azure."
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
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="2e0f7-103">Limitação de solicitação avançada com o Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="2e0f7-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="2e0f7-104">Ser capaz de limitar as solicitações de entrada é fundamental para o Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="2e0f7-105">Ao controlar a taxa de solicitações ou as solicitações/dados totais transferidos, o Gerenciamento de API permite que os provedores de API protejam suas APIs contra o abuso e criem valor para diferentes níveis de produto de API.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="2e0f7-106">Limitação baseada em produto</span><span class="sxs-lookup"><span data-stu-id="2e0f7-106">Product based throttling</span></span>
<span data-ttu-id="2e0f7-107">Até o momento, os recursos de limitação da taxa estavam restritos à assinatura de um produto específico (essencialmente uma chave), definida no portal do publicador de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="2e0f7-108">Isso é útil para o provedor de API aplicar limites aos desenvolvedores que se inscreveram para usar sua API, mas não ajuda, por exemplo, na limitação de usuários finais individuais da API.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="2e0f7-109">É possível que um único usuário do aplicativo do desenvolvedor consuma toda a cota, impedindo que outros clientes do desenvolvedor possam usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="2e0f7-110">Além disso, vários clientes que gerem um grande volume de solicitações podem limitar o acesso a usuários ocasionais.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="2e0f7-111">Limitação baseada em chave personalizada</span><span class="sxs-lookup"><span data-stu-id="2e0f7-111">Custom key based throttling</span></span>
<span data-ttu-id="2e0f7-112">As novas políticas [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) fornecem uma solução consideravelmente mais flexível para o controle de tráfego.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="2e0f7-113">Essas novas políticas permitem que você defina expressões a fim de identificar as chaves que serão usadas para acompanhar o tráfego.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="2e0f7-114">O modo como isso funciona será ilustrado com mais facilidade usando um exemplo.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="2e0f7-115">Limitação de endereço IP</span><span class="sxs-lookup"><span data-stu-id="2e0f7-115">IP Address throttling</span></span>
<span data-ttu-id="2e0f7-116">As políticas a seguir restringem um endereço IP de cliente individual para apenas 10 chamadas a cada minuto, com um total de 1.000.000 chamadas e 10.000 quilobytes de largura de banda por mês.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="2e0f7-117">Se todos os clientes na Internet usassem um endereço IP exclusivo, essa poderia ser uma maneira eficaz de limitar o uso por usuário.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="2e0f7-118">No entanto, é bastante provável que vários usuários compartilhem um único endereço IP público, já que acessam a Internet por meio de um dispositivo NAT.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="2e0f7-119">Apesar disso, para as APIs que permitem o acesso não autenticado, o `IpAddress` pode ser a melhor opção.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="2e0f7-120">Limitação de identidade do usuário</span><span class="sxs-lookup"><span data-stu-id="2e0f7-120">User identity throttling</span></span>
<span data-ttu-id="2e0f7-121">Se um usuário final for autenticado, uma chave de limitação poderá ser gerada com base nas informações que identificam esse usuário exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="2e0f7-122">Neste exemplo, extraímos o cabeçalho Autorização, o convertemos no objeto `JWT` e usamos o assunto do token para identificar o usuário e como a chave de limitação de taxa.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="2e0f7-123">Se a identidade do usuário for armazenada no `JWT` como uma das outras declarações, esse valor poderá ser usado em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="2e0f7-124">Políticas combinadas</span><span class="sxs-lookup"><span data-stu-id="2e0f7-124">Combined policies</span></span>
<span data-ttu-id="2e0f7-125">Embora as novas políticas de limitação forneçam mais controle do que as políticas de limitação existentes, ainda vale a pena combinar os dois recursos.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="2e0f7-126">Limitar por chave de assinatura do produto ([Limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [Definir a cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) é uma ótima maneira de habilitar a monetização de uma API por meio da cobrança com base nos níveis de uso.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="2e0f7-127">O controle mais preciso proporcionado pela limitação de acordo com o usuário é complementar e impede que o comportamento de um usuário afete a experiência de outros.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="2e0f7-128">Limitação controlada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="2e0f7-128">Client driven throttling</span></span>
<span data-ttu-id="2e0f7-129">Quando a chave de limitação é definida usando uma [expressão de política](https://msdn.microsoft.com/library/azure/dn910913.aspx), é o provedor de API que está escolhendo como a limitação é delimitada.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="2e0f7-130">No entanto, um desenvolvedor pode querer controlar como vai limitar seus próprios clientes.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="2e0f7-131">Isso pode ser habilitado pelo provedor da API introduzindo um cabeçalho personalizado para permitir que o aplicativo cliente do desenvolvedor comunique a chave para a API.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="2e0f7-132">Isso permite que o aplicativo cliente do desenvolvedor escolha como quer criar a chave de limitação de taxa.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="2e0f7-133">Com um pouco de criatividade, um desenvolvedor cliente pode criar suas próprias camadas de taxas, alocando conjuntos de chaves a usuários e promovendo a rotatividade do uso da chave.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="2e0f7-134">Resumo</span><span class="sxs-lookup"><span data-stu-id="2e0f7-134">Summary</span></span>
<span data-ttu-id="2e0f7-135">O Gerenciamento de API do Azure fornece limitação de taxa e de cota para proteger e agregar valor ao serviço de sua API.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="2e0f7-136">As novas políticas de limitação com regras de escopo personalizadas permitem um controle mais preciso sobre essas políticas para permitir que seus clientes criem aplicativos ainda melhores.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="2e0f7-137">Os exemplos deste artigo demonstram o uso dessas novas políticas criando chaves de limitação de taxa com endereços IP do cliente, identidade do usuário e valores gerados pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="2e0f7-138">No entanto, há muitas outras partes da mensagem que podem ser usadas como agente do usuário, fragmentos de caminho de URL, tamanho da mensagem.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e0f7-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e0f7-139">Next steps</span></span>
<span data-ttu-id="2e0f7-140">Envie-nos seus comentários no thread de discussão deste tópico.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="2e0f7-141">Seria ótimo conhecer outros possíveis valores de chave que foram uma escolha lógica para os seus cenários.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="2e0f7-142">Assista a uma visão geral dessas políticas em vídeo</span><span class="sxs-lookup"><span data-stu-id="2e0f7-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="2e0f7-143">Para saber mais sobre as políticas de [limite de taxa por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e de [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) abordadas neste artigo, assista ao vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="2e0f7-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

