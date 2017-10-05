---
title: Usando a CDN do Azure com o CORS | Microsoft Docs
description: "Saiba como usar a CDN (Rede de Distribuição de Conteúdo) do Azure com o CORS (Compartilhamento de Recursos entre Origens)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="96924-103">Usar a CDN do Azure com o CORS</span><span class="sxs-lookup"><span data-stu-id="96924-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="96924-104">O que é CORS?</span><span class="sxs-lookup"><span data-stu-id="96924-104">What is CORS?</span></span>
<span data-ttu-id="96924-105">O CORS (Compartilhamento de Recursos entre Origens) é um recurso HTTP que permite que um aplicativo web em execução em um domínio acesse recursos em outro domínio.</span><span class="sxs-lookup"><span data-stu-id="96924-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="96924-106">Para reduzir a possibilidade de ataques de script entre sites, todos os navegadores modernos implementam uma restrição de segurança conhecida como [política de mesma origem](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="96924-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="96924-107">Isso impede que uma página da Web chame APIs em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="96924-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="96924-108">O CORS fornece uma maneira segura para permitir que uma origem (o domínio de origem) chame APIs em outra origem.</span><span class="sxs-lookup"><span data-stu-id="96924-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="96924-109">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="96924-109">How it works</span></span>
<span data-ttu-id="96924-110">Há dois tipos de solicitações CORS, *solicitações simples* e *solicitações complexas.*</span><span class="sxs-lookup"><span data-stu-id="96924-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="96924-111">Para solicitações simples:</span><span class="sxs-lookup"><span data-stu-id="96924-111">For simple requests:</span></span>

1. <span data-ttu-id="96924-112">O navegador envia a solicitação CORS com adicional **origem** cabeçalho de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="96924-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="96924-113">O valor desse cabeçalho é a origem que serviu a página pai, que é definida como a combinação de *protocolo,* *domínio,* e *porta.*</span><span class="sxs-lookup"><span data-stu-id="96924-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="96924-114">Quando uma página de https://www.contoso.com tenta acessar os dados de um usuário na origem fabrikam.com, o seguinte cabeçalho de solicitação é enviado para fabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="96924-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="96924-115">O servidor pode responder com um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="96924-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="96924-116">Um cabeçalho **Access-Control-Allow-Origin** em sua resposta indicando qual site de origem é permitido.</span><span class="sxs-lookup"><span data-stu-id="96924-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="96924-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="96924-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="96924-118">Um código de erro HTTP como 403, se o servidor não permite que a solicitação entre origens depois de verificar o cabeçalho de origem</span><span class="sxs-lookup"><span data-stu-id="96924-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="96924-119">Um cabeçalho **Access-Control-Allow-Origin** com um caractere curinga que permite todas as origens:</span><span class="sxs-lookup"><span data-stu-id="96924-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="96924-120">Para solicitações complexas:</span><span class="sxs-lookup"><span data-stu-id="96924-120">For complex requests:</span></span>

<span data-ttu-id="96924-121">Uma solicitação complexa é uma solicitação CORS onde o navegador é necessário para enviar um *solicitação de simulação* (ou seja, uma investigação preliminar) antes de enviar a solicitação CORS real.</span><span class="sxs-lookup"><span data-stu-id="96924-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="96924-122">A solicitação de simulação pede a permissão do servidor se o CORS originais da solicitação pode continuar e é um `OPTIONS` solicitação para a mesma URL.</span><span class="sxs-lookup"><span data-stu-id="96924-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="96924-123">Para obter mais detalhes sobre fluxos CORS e armadilhas comuns, consulte o [guia CORS para APIs REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="96924-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="96924-124">Cenários de origem única ou curinga</span><span class="sxs-lookup"><span data-stu-id="96924-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="96924-125">O CORS na Azure CDN funcionará automaticamente sem nenhuma configuração adicional quando o cabeçalho **Access-Control-Allow-Origin** for definido como caractere curinga (*) ou uma origem única.</span><span class="sxs-lookup"><span data-stu-id="96924-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="96924-126">A CDN armazenará a primeira resposta em cache e as solicitações subsequentes usarão o mesmo cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="96924-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="96924-127">Se já tiverem sido feitas solicitações à CDN antes de o CORS ser definido na origem, você precisará limpar o conteúdo no conteúdo do ponto de extremidade para recarregar o conteúdo com o cabeçalho **Access-Control-Allow-Origin** .</span><span class="sxs-lookup"><span data-stu-id="96924-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="96924-128">Cenários de várias origens</span><span class="sxs-lookup"><span data-stu-id="96924-128">Multiple origin scenarios</span></span>
<span data-ttu-id="96924-129">Se você precisar permitir que uma lista específica de origens seja permitida para o CORS, isso será um pouco mais complicado.</span><span class="sxs-lookup"><span data-stu-id="96924-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="96924-130">O problema ocorre quando a CDN armazena o cabeçalho **Access-Control-Allow-Origin** em cache para a primeira origem do CORS.</span><span class="sxs-lookup"><span data-stu-id="96924-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="96924-131">Quando uma origem do CORS diferente fizer uma solicitação subsequente, a CDN terá fornecido o cabeçalho **Access-Control-Allow-Origin** armazenado em cache que não é correspondente.</span><span class="sxs-lookup"><span data-stu-id="96924-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="96924-132">Há várias maneiras de corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="96924-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="96924-133">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="96924-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="96924-134">A melhor maneira de habilitar essa opção é usar o **Azure CDN Premium da Verizon**, que expõe algumas funcionalidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="96924-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="96924-135">Você precisará [criar uma regra](cdn-rules-engine.md) para verificar o cabeçalho **Origin** na solicitação.</span><span class="sxs-lookup"><span data-stu-id="96924-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="96924-136">Se for uma origem válida, a regra definirá o cabeçalho **Access-Control-Allow-Origin** com a origem fornecida na solicitação.</span><span class="sxs-lookup"><span data-stu-id="96924-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="96924-137">Se a origem especificada no cabeçalho **Origem** não for permitida, a regra deverá omitir o cabeçalho **Access-Control-Allow-Origin**, que fará com que o navegador rejeite a solicitação.</span><span class="sxs-lookup"><span data-stu-id="96924-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="96924-138">Há duas maneiras de fazer isso com o mecanismo de regras.</span><span class="sxs-lookup"><span data-stu-id="96924-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="96924-139">Em ambos os casos, o cabeçalho **Access-Control-Allow-Origin** do servidor de origem do arquivo é totalmente ignorado e o mecanismo de regras da CDN gerencia completamente as origens CORS permitidas.</span><span class="sxs-lookup"><span data-stu-id="96924-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="96924-140">Uma expressão regular com todas as origens válidas</span><span class="sxs-lookup"><span data-stu-id="96924-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="96924-141">Nesse caso, você criará uma expressão regular que inclua todas as origens que deseja permitir:</span><span class="sxs-lookup"><span data-stu-id="96924-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="96924-142">A **CDN do Azure da Verizon** usa as [Expressões Regulares Compatíveis com o Perl](http://pcre.org/) como seu mecanismo de expressões regulares.</span><span class="sxs-lookup"><span data-stu-id="96924-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="96924-143">Você pode usar uma ferramenta, como [Expressões Regulares 101](https://regex101.com/), para validar sua expressão regular.</span><span class="sxs-lookup"><span data-stu-id="96924-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="96924-144">Observe que o caractere "/" é válido em expressões regulares e não precisa ter um caractere de escape. No entanto, adicionar um caractere de escape a esse caractere é considerado uma prática recomendada e é esperado por alguns validadores de regex.</span><span class="sxs-lookup"><span data-stu-id="96924-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="96924-145">Se a expressão regular for correspondente, a regra substituirá o cabeçalho **Access-Control-Allow-Origin** (se houver) da origem pela origem que enviou a solicitação.</span><span class="sxs-lookup"><span data-stu-id="96924-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="96924-146">Você também pode adicionar outros cabeçalhos CORS, como **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="96924-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Exemplo de regras com expressões regulares](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="96924-148">Solicitar a regra de cabeçalho para cada origem.</span><span class="sxs-lookup"><span data-stu-id="96924-148">Request header rule for each origin.</span></span>
<span data-ttu-id="96924-149">Em vez de expressões regulares, você pode criar uma regra separada para cada origem que deseja permitir usando a **condição de correspondência** [Curinga do Cabeçalho de Solicitação](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="96924-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="96924-150">Assim como acontece com o método de expressão regular, apenas o mecanismo de regras define os cabeçalhos do CORS.</span><span class="sxs-lookup"><span data-stu-id="96924-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Exemplo de regras sem expressões regulares](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="96924-152">No exemplo acima, o uso do caractere curinga * instrui o mecanismo de regras a corresponder HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96924-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="96924-153">Padrão do Azure CDN</span><span class="sxs-lookup"><span data-stu-id="96924-153">Azure CDN Standard</span></span>
<span data-ttu-id="96924-154">Em perfis Padrão do Azure CDN, o único mecanismo para permitir várias origens sem o uso da origem curinga é usar o [armazenamento em cache da cadeia de caracteres de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="96924-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="96924-155">Você precisa habilitar a configuração da cadeia de caracteres de consulta para o ponto de extremidade da CDN e usar uma cadeia de caracteres de consulta exclusiva para solicitações de cada domínio permitido.</span><span class="sxs-lookup"><span data-stu-id="96924-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="96924-156">Isso fará com que a CDN armazene em cache um objeto separado para cada cadeia de caractere de consulta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="96924-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="96924-157">No entanto, essa abordagem não é ideal, pois resultará em várias cópias do mesmo arquivo armazenadas em cache na CDN.</span><span class="sxs-lookup"><span data-stu-id="96924-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

