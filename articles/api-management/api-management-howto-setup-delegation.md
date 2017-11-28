---
title: "aaaHow toodelegate assinatura de produto e o registro do usuário"
description: "Saiba como tooa de assinatura toodelegate usuário registro e o produto de terceiros no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="269b1-103">Como toodelegate assinatura de produto e o registro do usuário</span><span class="sxs-lookup"><span data-stu-id="269b1-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="269b1-104">A delegação permite que você toouse seu site da Web existente para lidar com tooproducts de entrada-em/entrada o e assinatura de desenvolvedor como oposição toousing Olá funcionalidade no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="269b1-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="269b1-105">Isso permite que seus dados de usuário do site tooown hello e executar a validação de saudação dessas etapas de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="269b1-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="269b1-106"><a name="delegate-signin-up"> </a>Delegando a entrada e inscrição de desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="269b1-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="269b1-107">toodelegate desenvolvedor tooyour entrar e inscreva-se site existente que será necessário toocreate um ponto de extremidade de delegação especial em seu site que atua como Olá ponto de entrada para qualquer tal solicitação iniciada do portal do desenvolvedor de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="269b1-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="269b1-108">fluxo de trabalho final Olá será da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="269b1-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="269b1-109">Desenvolvedor clica no link de saudação entrar ou se inscreva no portal do desenvolvedor de gerenciamento de API de saudação</span><span class="sxs-lookup"><span data-stu-id="269b1-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="269b1-110">Navegador é redirecionado toohello ponto de extremidade de delegação</span><span class="sxs-lookup"><span data-stu-id="269b1-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="269b1-111">Ponto de extremidade de delegação de retorno redireciona tooor apresenta interface de usuário solicitando usuário toosign ou de inscrição</span><span class="sxs-lookup"><span data-stu-id="269b1-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="269b1-112">Em caso de sucesso, usuário Olá é redirecionado toohello back API developer portal página Gerenciamento de que eles começaram a partir</span><span class="sxs-lookup"><span data-stu-id="269b1-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="269b1-113">toobegin, vamos primeiro tooroute de gerenciamento de API de configuração solicitações por meio de seu ponto de extremidade de delegação.</span><span class="sxs-lookup"><span data-stu-id="269b1-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="269b1-114">No portal do publicador de gerenciamento de API de saudação, clique em **segurança** e, em seguida, clique em Olá **delegação** guia. Clique em tooenable caixa de seleção de saudação 'Delegado entrar & inscrição'.</span><span class="sxs-lookup"><span data-stu-id="269b1-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Página de delegação][api-management-delegation-signin-up]

* <span data-ttu-id="269b1-116">Decidir quais Olá URL de seu ponto de extremidade de delegação especial será e insira Olá **URL de ponto de extremidade de delegação** campo.</span><span class="sxs-lookup"><span data-stu-id="269b1-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="269b1-117">Dentro de saudação **chave de autenticação de delegação** campo Digite um segredo que será usado toocompute tooyou uma assinatura fornecida para verificação tooensure que Olá solicitação realmente vem de gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="269b1-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="269b1-118">Você pode clicar em Olá **gerar** toohave botão gerenciamento de API gerar aleatoriamente uma chave para você.</span><span class="sxs-lookup"><span data-stu-id="269b1-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="269b1-119">Agora você precisa Olá toocreate **ponto de extremidade de delegação**.</span><span class="sxs-lookup"><span data-stu-id="269b1-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="269b1-120">Ele tem tooperform uma série de ações:</span><span class="sxs-lookup"><span data-stu-id="269b1-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="269b1-121">Receba uma solicitação em Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="269b1-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="269b1-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL da página de origem}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="269b1-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="269b1-123">Parâmetros de consulta para o caso de entrada / inscrição hello:</span><span class="sxs-lookup"><span data-stu-id="269b1-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="269b1-124">**operation**: identifica o tipo de solicitação de delegação – neste caso, pode ser somente **SignIn**</span><span class="sxs-lookup"><span data-stu-id="269b1-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="269b1-125">**returnUrl**: Olá URL da página de saudação em que o usuário Olá clicou em um link entre ou inscreva-se</span><span class="sxs-lookup"><span data-stu-id="269b1-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="269b1-126">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="269b1-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="269b1-127">**SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio</span><span class="sxs-lookup"><span data-stu-id="269b1-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="269b1-128">Verifique se que essa solicitação de saudação é proveniente de gerenciamento de API do Azure (opcional, mas altamente recomendado para segurança)</span><span class="sxs-lookup"><span data-stu-id="269b1-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="269b1-129">Computar um hash HMAC-SHA512 de uma cadeia de caracteres com base em Olá **returnUrl** e **salt** parâmetros de consulta ([código de exemplo fornecido abaixo]):</span><span class="sxs-lookup"><span data-stu-id="269b1-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="269b1-130">HMAC(**salt**+ '\n' +**returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="269b1-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="269b1-131">Comparar toohello valor hash calculado acima Olá Olá **sig** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="269b1-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="269b1-132">Se dois hashes de saudação corresponderem, move na toohello próxima etapa, caso contrário, negar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="269b1-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="269b1-133">Verifique se que você está recebendo uma solicitação de entrada-no/sign-up: Olá **operação** parâmetro de consulta será definido muito "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="269b1-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="269b1-134">Apresentar Olá usuário da interface do usuário toosign ou de inscrição</span><span class="sxs-lookup"><span data-stu-id="269b1-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="269b1-135">Se o usuário Olá é registrar-se você tiver toocreate uma conta correspondente para eles no gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="269b1-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="269b1-136">[Criar um usuário] com hello API de REST de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="269b1-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="269b1-137">Ao fazer isso, certifique-se de que você defina Olá toohello de ID de usuário, mesmo se que ele está em seu repositório do usuário ou ID tooan que você pode manter controle das.</span><span class="sxs-lookup"><span data-stu-id="269b1-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="269b1-138">Quando o usuário Olá for autenticado com êxito:</span><span class="sxs-lookup"><span data-stu-id="269b1-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="269b1-139">[solicitar um token single-sign-on (SSO)] via Olá API de REST de gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="269b1-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="269b1-140">Acrescente uma toohello de parâmetro de consulta returnUrl URL SSO você recebeu de chamada de API de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="269b1-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="269b1-141">por exemplo: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="269b1-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="269b1-142">Olá usuário toohello acima produzido URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="269b1-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="269b1-143">Em adição toohello **SignIn** operação, você também pode executar o gerenciamento de conta, seguindo as etapas anteriores hello e usando uma das seguintes operações de saudação.</span><span class="sxs-lookup"><span data-stu-id="269b1-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="269b1-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="269b1-144">**ChangePassword**</span></span>
* <span data-ttu-id="269b1-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="269b1-145">**ChangeProfile**</span></span>
* <span data-ttu-id="269b1-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="269b1-146">**CloseAccount**</span></span>

<span data-ttu-id="269b1-147">Você deve passar Olá parâmetros de consulta para operações de gerenciamento de conta a seguir.</span><span class="sxs-lookup"><span data-stu-id="269b1-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="269b1-148">**operation**: identifica o tipo de solicitação de delegação (ChangePassword, ChangeProfile ou CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="269b1-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="269b1-149">**userId**: id de usuário de saudação do hello conta toomanage</span><span class="sxs-lookup"><span data-stu-id="269b1-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="269b1-150">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="269b1-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="269b1-151">**SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio</span><span class="sxs-lookup"><span data-stu-id="269b1-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="269b1-152"><a name="delegate-product-subscription"> </a>Delegando a assinatura de produtos</span><span class="sxs-lookup"><span data-stu-id="269b1-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="269b1-153">Delegando a assinatura de produto funciona da mesma forma toodelegating usuário entrar/backup.</span><span class="sxs-lookup"><span data-stu-id="269b1-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="269b1-154">fluxo de trabalho final Olá seria a seguinte:</span><span class="sxs-lookup"><span data-stu-id="269b1-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="269b1-155">Desenvolvedor seleciona um produto no portal do desenvolvedor de gerenciamento de API hello e clica no botão de inscrição Olá</span><span class="sxs-lookup"><span data-stu-id="269b1-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="269b1-156">Navegador é redirecionado toohello ponto de extremidade de delegação</span><span class="sxs-lookup"><span data-stu-id="269b1-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="269b1-157">Ponto de extremidade de delegação executa etapas de assinatura de produto necessária - este é o tooyou e pode envolver o redirecionamento tooanother toorequest de página informações de cobrança, fazer perguntas adicionais, ou simplesmente armazenando informações de saudação e não exigem nenhuma ação do usuário</span><span class="sxs-lookup"><span data-stu-id="269b1-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="269b1-158">tooenable Olá funcionalidade, Olá **delegação** página clique **delegar assinatura produto**.</span><span class="sxs-lookup"><span data-stu-id="269b1-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="269b1-159">Em seguida, certifique-se de ponto de extremidade de delegação Olá executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="269b1-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="269b1-160">Receba uma solicitação em Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="269b1-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="269b1-161">*http://www.yourwebsite.com/apimdelegation?Operation= {operação} & productId = {toosubscribe de produto para} & userId = {usuário fazer solicitação} & salt = {string} & sig = {string}*</span><span class="sxs-lookup"><span data-stu-id="269b1-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="269b1-162">Parâmetros de consulta para o caso de assinatura de produto hello:</span><span class="sxs-lookup"><span data-stu-id="269b1-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="269b1-163">**operation**: identifica o tipo de solicitação de delegação.</span><span class="sxs-lookup"><span data-stu-id="269b1-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="269b1-164">Para a assinatura de produto solicitações Olá as opções válidas são:</span><span class="sxs-lookup"><span data-stu-id="269b1-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="269b1-165">"Assinar": fornecidos de uma solicitação toosubscribe Olá usuário tooa, considerando o produto com ID (veja abaixo)</span><span class="sxs-lookup"><span data-stu-id="269b1-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="269b1-166">"Unsubscribe": toounsubscribe uma solicitação de um produto de um usuário</span><span class="sxs-lookup"><span data-stu-id="269b1-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="269b1-167">"Renovar": uma solicitação toorenew uma assinatura (por exemplo, que pode expirar)</span><span class="sxs-lookup"><span data-stu-id="269b1-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="269b1-168">**productId**: ID de saudação do usuário Olá Olá solicitado toosubscribe para</span><span class="sxs-lookup"><span data-stu-id="269b1-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="269b1-169">**userId**: Olá ID do usuário Olá para o qual é feita a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="269b1-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="269b1-170">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="269b1-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="269b1-171">**SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio</span><span class="sxs-lookup"><span data-stu-id="269b1-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="269b1-172">Verifique se que essa solicitação de saudação é proveniente de gerenciamento de API do Azure (opcional, mas altamente recomendado para segurança)</span><span class="sxs-lookup"><span data-stu-id="269b1-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="269b1-173">Calcular um HMAC-SHA512 de uma cadeia de caracteres com base em Olá **productId**, **userId** e **salt** parâmetros de consulta:</span><span class="sxs-lookup"><span data-stu-id="269b1-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="269b1-174">HMAC(**salt**+ '\n' +**productId**+ '\n' +**userId**)</span><span class="sxs-lookup"><span data-stu-id="269b1-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="269b1-175">Comparar toohello valor hash calculado acima Olá Olá **sig** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="269b1-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="269b1-176">Se dois hashes de saudação corresponderem, move na toohello próxima etapa, caso contrário, negar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="269b1-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="269b1-177">Executar qualquer processamento de assinatura de produto com base no tipo de saudação da operação solicitada no **operação** -por exemplo, cobrança, mais perguntas, etc.</span><span class="sxs-lookup"><span data-stu-id="269b1-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="269b1-178">Sobre a inscrição com êxito o produto de toohello Olá usuário ao seu lado, inscrever-se o produto de gerenciamento de API do hello usuário toohello por [chamada hello API REST para assinatura de produto].</span><span class="sxs-lookup"><span data-stu-id="269b1-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="269b1-179"><a name="delegate-example-code"> </a> Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="269b1-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="269b1-180">Eles mostram exemplos de código como Olá tootake *chave de validação de delegação*, que é definido na tela de delegação de saudação do portal do publicador hello, toocreate um HMAC que é então usado assinatura de saudação toovalidate, provando validade de saudação do hello returnUrl passado.</span><span class="sxs-lookup"><span data-stu-id="269b1-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="269b1-181">Olá mesmo código funciona para productId hello e userId com pequenas modificações.</span><span class="sxs-lookup"><span data-stu-id="269b1-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="269b1-182">**C# hash de toogenerate código de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="269b1-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="269b1-183">**Hash de toogenerate NodeJS código de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="269b1-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="269b1-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="269b1-184">Next steps</span></span>
<span data-ttu-id="269b1-185">Para obter mais informações sobre a delegação, consulte Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="269b1-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[solicitar um token single-sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Crie um usuário]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[chamada hello API REST para assinatura de produto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de exemplo fornecido abaixo]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
