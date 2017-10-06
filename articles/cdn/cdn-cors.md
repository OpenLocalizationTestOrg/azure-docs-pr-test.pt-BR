---
title: aaaUsing CDN do Azure com CORS | Microsoft Docs
description: Saiba como toouse hello Azure Content Delivery Network (CDN) toowith compartilhamento de recursos entre origens (CORS).
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="0c0e4-103">Usar a CDN do Azure com o CORS</span><span class="sxs-lookup"><span data-stu-id="0c0e4-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="0c0e4-104">O que é CORS?</span><span class="sxs-lookup"><span data-stu-id="0c0e4-104">What is CORS?</span></span>
<span data-ttu-id="0c0e4-105">CORS (Cross origem Resource Sharing) é um recurso HTTP que permite que um aplicativo web executando os recursos de tooaccess em um domínio em outro domínio.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="0c0e4-106">Possibilidade de saudação de tooreduce de ordem de ataques de script entre sites, todos os navegadores modernos implementam uma restrição de segurança, conhecida como [política de mesma origem](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="0c0e4-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="0c0e4-107">Isso impede que uma página da Web chame APIs em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="0c0e4-108">CORS fornece uma maneira segura tooallow uma origem (domínio de origem Olá) toocall APIs em outra origem.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0c0e4-109">Como funciona</span><span class="sxs-lookup"><span data-stu-id="0c0e4-109">How it works</span></span>
<span data-ttu-id="0c0e4-110">Há dois tipos de solicitações CORS, *solicitações simples* e *solicitações complexas.*</span><span class="sxs-lookup"><span data-stu-id="0c0e4-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="0c0e4-111">Para solicitações simples:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-111">For simple requests:</span></span>

1. <span data-ttu-id="0c0e4-112">navegador Olá envia a solicitação CORS de saudação com adicional **origem** cabeçalho de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="0c0e4-113">valor Olá desse cabeçalho é a origem de saudação que serviu a página pai hello, o que é definida como a combinação de saudação do *protocolo,* *domínio,* e *porta.*</span><span class="sxs-lookup"><span data-stu-id="0c0e4-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="0c0e4-114">Quando uma página da https://www.contoso.com tenta tooaccess dados de um usuário na origem de fabrikam.com hello, Olá cabeçalho de solicitação a seguir seria enviado toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="0c0e4-115">servidor de saudação pode responder com qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="0c0e4-116">Um cabeçalho **Access-Control-Allow-Origin** em sua resposta indicando qual site de origem é permitido.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="0c0e4-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="0c0e4-118">Código de erro HTTP como 403 se o servidor de saudação não permitir solicitação entre origens de saudação depois de verificar se o cabeçalho de origem Olá</span><span class="sxs-lookup"><span data-stu-id="0c0e4-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="0c0e4-119">Um cabeçalho **Access-Control-Allow-Origin** com um caractere curinga que permite todas as origens:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="0c0e4-120">Para solicitações complexas:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-120">For complex requests:</span></span>

<span data-ttu-id="0c0e4-121">Uma solicitação complexa é uma solicitação de CORS onde navegador Olá toosend necessária uma *solicitação de simulação* (ou seja, uma investigação preliminar) antes de enviar a solicitação CORS real hello.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="0c0e4-122">Olá solicitação de simulação solicita permissão do servidor de saudação se a solicitação CORS original Olá pode continuar e é um `OPTIONS` solicitação toohello mesma URL.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="0c0e4-123">Para obter mais detalhes sobre fluxos de CORS e armadilhas comuns, exibir hello [guia tooCORS para APIs REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="0c0e4-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="0c0e4-124">Cenários de origem única ou curinga</span><span class="sxs-lookup"><span data-stu-id="0c0e4-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="0c0e4-125">CORS na CDN do Azure funcionará automaticamente sem nenhuma configuração adicional quando hello **Access-Control-Allow-Origin** cabeçalho é definido toowildcard (*) ou uma origem única.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="0c0e4-126">Olá CDN armazenará em cache primeira resposta do hello e solicitações subsequentes usarão Olá mesmo cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="0c0e4-127">Se as solicitações já foram feitas toohello CDN anterior tooCORS, sendo definido Olá sua origem, você precisará toopurge conteúdo na sua Olá tooreload conteúdo de ponto de extremidade conteúdo com hello **Access-Control-Allow-Origin** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="0c0e4-128">Cenários de várias origens</span><span class="sxs-lookup"><span data-stu-id="0c0e4-128">Multiple origin scenarios</span></span>
<span data-ttu-id="0c0e4-129">Se você precisar tooallow uma lista específica de origens toobe permitido para CORS, as coisas são um pouco mais complicadas.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="0c0e4-130">problema de saudação ocorre quando Olá CDN armazena em cache Olá **Access-Control-Allow-Origin** cabeçalho para a origem CORS primeiro hello.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="0c0e4-131">Quando uma origem diferente do CORS faz uma solicitação subsequente, Olá CDN servirá Olá armazenado em cache **Access-Control-Allow-Origin** cabeçalho, que não corresponde.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="0c0e4-132">Há várias toocorrect de maneiras isso.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="0c0e4-133">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="0c0e4-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="0c0e4-134">Olá tooenable de maneira melhor trata toouse **Premium do Azure CDN da Verizon**, que expõe alguns recursos avançados.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="0c0e4-135">Você precisará de muito[criar uma regra de](cdn-rules-engine.md) toocheck Olá **origem** cabeçalho na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="0c0e4-136">Se for uma origem válida, a regra será definida Olá **Access-Control-Allow-Origin** cabeçalho com origem Olá fornecido na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="0c0e4-137">Se origem Olá especificado em Olá **origem** cabeçalho não é permitido, a regra deve omitir Olá **Access-Control-Allow-Origin** cabeçalho que fará com que a solicitação de saudação do hello navegador tooreject.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="0c0e4-138">Há toodo de duas maneiras isso com o mecanismo de regras de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="0c0e4-139">Em ambos os casos, Olá **Access-Control-Allow-Origin** cabeçalho do servidor de origem do arquivo hello completamente é ignorado, o mecanismo de regras do CDN Olá gerencia totalmente Olá permitido origens CORS.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="0c0e4-140">Uma expressão regular com todas as origens válidas</span><span class="sxs-lookup"><span data-stu-id="0c0e4-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="0c0e4-141">Nesse caso, você criará uma expressão regular que inclui todas as origens de saudação desejado tooallow:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="0c0e4-142">A **CDN do Azure da Verizon** usa as [Expressões Regulares Compatíveis com o Perl](http://pcre.org/) como seu mecanismo de expressões regulares.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="0c0e4-143">Você pode usar uma ferramenta como [101 de expressões regulares](https://regex101.com/) toovalidate sua expressão regular.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="0c0e4-144">Observe que o caractere "/" hello é válido em expressões regulares e não precisa de escape de toobe, no entanto, o escape de caractere é considerada uma prática recomendada e é esperado por alguns validadores de regex.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="0c0e4-145">Se corresponder a expressão regular hello, sua regra substitui Olá **Access-Control-Allow-Origin** cabeçalho (se houver) da origem de saudação com origem de saudação que enviou a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="0c0e4-146">Você também pode adicionar outros cabeçalhos CORS, como **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Exemplo de regras com expressões regulares](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="0c0e4-148">Solicitar a regra de cabeçalho para cada origem.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-148">Request header rule for each origin.</span></span>
<span data-ttu-id="0c0e4-149">Em vez de expressões regulares, você pode criar um separado de regra para cada origem você deseja tooallow usando Olá **curinga de cabeçalho de solicitação** [correspondem à condição](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="0c0e4-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="0c0e4-150">Como com o método de expressão regular hello, Olá mecanismo de regras apenas conjuntos de cabeçalhos CORS de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Exemplo de regras sem expressões regulares](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="0c0e4-152">O exemplo hello acima, Olá uso do caractere curinga de saudação * informa ao mecanismo de regras de saudação toomatch HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="0c0e4-153">Padrão do Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0c0e4-153">Azure CDN Standard</span></span>
<span data-ttu-id="0c0e4-154">No padrão do Azure CDN perfis, Olá somente tooallow do mecanismo de várias origens sem o uso de saudação de origem de curinga Olá é toouse [cache de cadeia de caracteres de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="0c0e4-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="0c0e4-155">Você precisa tooenable configuração de cadeia de caracteres de consulta para o ponto de extremidade CDN hello e, em seguida, usa uma cadeia de caracteres de consulta exclusiva para solicitações de cada domínio permitido.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="0c0e4-156">Isso resultará em Olá um objeto separado para cada cadeia de caracteres de consulta exclusiva do cache da CDN.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="0c0e4-157">Essa abordagem não é ideal, no entanto, como resultará em várias cópias de saudação mesmo arquivo hello armazenado em cache na CDN.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

