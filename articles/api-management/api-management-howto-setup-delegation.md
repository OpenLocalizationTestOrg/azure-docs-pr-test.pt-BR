---
title: "Como delegar o registro de usuário e a assinatura do produto"
description: "Saiba como delegar a assinatura de produto e registro de usuário a um terceiro no Gerenciamento de API do Azure."
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
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="da024-103">Como delegar o registro de usuário e a assinatura do produto</span><span class="sxs-lookup"><span data-stu-id="da024-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="da024-104">A delegação permite usar seu site existente para gerenciar a entrada/inscrição e assinatura de produtos feitas por desenvolvedores em vez de usar a funcionalidade integrada no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="da024-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="da024-105">Isso permite que seu site tenha os dados dos usuários e realize a validação dessas etapas de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="da024-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="da024-106"><a name="delegate-signin-up"> </a>Delegando a entrada e inscrição de desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="da024-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="da024-107">Para delegar a entrada e a assinatura do desenvolvedor em seu site existente, você precisará criar um ponto de extremidade de delegação especial em seu site que atue como ponto de entrada para qualquer solicitação desse tipo por meio do portal do desenvolvedor do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="da024-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="da024-108">O fluxo de trabalho final será o seguinte:</span><span class="sxs-lookup"><span data-stu-id="da024-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="da024-109">O desenvolvedor clica no link de assinatura ou entrada no portal do desenvolvedor do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="da024-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="da024-110">O navegador é redirecionado ao ponto de extremidade de delegação</span><span class="sxs-lookup"><span data-stu-id="da024-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="da024-111">O ponto de extremidade de delegação, por sua vez, redireciona ou apresenta a IU solicitando o usuário a entrar ou se inscrever</span><span class="sxs-lookup"><span data-stu-id="da024-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="da024-112">Em caso de êxito, o usuário é redirecionado de volta para o portal do desenvolvedor do Gerenciamento de API onde começou</span><span class="sxs-lookup"><span data-stu-id="da024-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="da024-113">Para começar, vamos configurar o Gerenciamento de API para encaminhar as solicitações por meio do seu ponto de extremidade de delegação.</span><span class="sxs-lookup"><span data-stu-id="da024-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="da024-114">No portal do editor do Gerenciamento de API, clique em **Segurança** e na guia **Delegação**.</span><span class="sxs-lookup"><span data-stu-id="da024-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="da024-115">Clique na caixa de seleção para habilitar "Delegar entrada e inscrição".</span><span class="sxs-lookup"><span data-stu-id="da024-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Página de delegação][api-management-delegation-signin-up]

* <span data-ttu-id="da024-117">Decida qual será o URL do seu ponto de extremidade de delegação especial e insira-o no campo **URL do ponto de extremidade de delegação** .</span><span class="sxs-lookup"><span data-stu-id="da024-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="da024-118">No campo **Chave de autenticação de delegação** , insira um segredo que será usado para calcular uma assinatura fornecida a você para verificação, para garantir que a solicitação realmente venha do Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="da024-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="da024-119">Você pode clicar no botão **Gerar** para o Gerenciamento de API gerar aleatoriamente uma chave para você.</span><span class="sxs-lookup"><span data-stu-id="da024-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="da024-120">Agora, você precisa criar o **ponto de extremidade de delegação**.</span><span class="sxs-lookup"><span data-stu-id="da024-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="da024-121">Ele precisa realizar uma série de ações:</span><span class="sxs-lookup"><span data-stu-id="da024-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="da024-122">Receba uma solicitação com a seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="da024-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="da024-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL da página de origem}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="da024-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="da024-124">Parâmetros de consulta para a entrada/inscrição:</span><span class="sxs-lookup"><span data-stu-id="da024-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="da024-125">**operation**: identifica o tipo de solicitação de delegação – neste caso, pode ser somente **SignIn**</span><span class="sxs-lookup"><span data-stu-id="da024-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="da024-126">**returnUrl**: a URL da página em que o usuário clicou em um link de entrada ou de inscrição</span><span class="sxs-lookup"><span data-stu-id="da024-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="da024-127">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="da024-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="da024-128">**sig**: um hash de segurança calculado para ser usado para comparação com seu próprio hash calculado</span><span class="sxs-lookup"><span data-stu-id="da024-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="da024-129">Confirme que a solicitação está vindo do Gerenciamento de API do Azure (opcional, mas altamente recomendado por segurança)</span><span class="sxs-lookup"><span data-stu-id="da024-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="da024-130">Calcule um hash HMAC-SHA512 de uma cadeia de caracteres baseada nos parâmetros de consulta **returnUrl** e **salt** ([código de exemplo fornecido abaixo]):</span><span class="sxs-lookup"><span data-stu-id="da024-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="da024-131">HMAC(**salt**+ '\n' +**returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="da024-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="da024-132">Compare o hash calculado acima ao valor do parâmetro de consulta **sig**.</span><span class="sxs-lookup"><span data-stu-id="da024-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="da024-133">Se os dois hashes forem correspondentes, prossiga para a próxima etapa. Caso contrário, recuse as solicitações.</span><span class="sxs-lookup"><span data-stu-id="da024-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="da024-134">Verifique se que você está recebendo uma solicitação de entrada/inscrição: o parâmetro de consulta **operation** será definido como "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="da024-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="da024-135">Apresente ao usuário a IU para entrar ou se inscrever</span><span class="sxs-lookup"><span data-stu-id="da024-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="da024-136">Se o usuário estiver se inscrevendo, você precisará criar uma conta correspondente para ele no Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="da024-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="da024-137">[Crie um usuário] com a API REST do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="da024-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="da024-138">Ao fazer isso, certifique-se de definir a ID de usuário como a mesma que está em seu repositório de usuários ou como uma ID que você possa acompanhar.</span><span class="sxs-lookup"><span data-stu-id="da024-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="da024-139">Quando o usuário for autenticado com sucesso:</span><span class="sxs-lookup"><span data-stu-id="da024-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="da024-140">[solicite um token de logon único (SSO)] por meio da API REST do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="da024-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="da024-141">anexe um parâmetro de consulta returnUrl ao URL SSO que você recebeu da chamada à API acima:</span><span class="sxs-lookup"><span data-stu-id="da024-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="da024-142">por exemplo: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="da024-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="da024-143">redirecione o usuário à URL produzida acima</span><span class="sxs-lookup"><span data-stu-id="da024-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="da024-144">Além da operação **SignIn** , você também pode executar o gerenciamento de conta seguindo as etapas anteriores e usando uma das seguintes operações.</span><span class="sxs-lookup"><span data-stu-id="da024-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="da024-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="da024-145">**ChangePassword**</span></span>
* <span data-ttu-id="da024-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="da024-146">**ChangeProfile**</span></span>
* <span data-ttu-id="da024-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="da024-147">**CloseAccount**</span></span>

<span data-ttu-id="da024-148">Você deve passar os seguintes parâmetros de consulta para operações de gerenciamento de conta.</span><span class="sxs-lookup"><span data-stu-id="da024-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="da024-149">**operation**: identifica o tipo de solicitação de delegação (ChangePassword, ChangeProfile ou CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="da024-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="da024-150">**userId**: a identificação de usuário da conta a ser gerenciada</span><span class="sxs-lookup"><span data-stu-id="da024-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="da024-151">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="da024-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="da024-152">**sig**: um hash de segurança calculado para ser usado para comparação com seu próprio hash calculado</span><span class="sxs-lookup"><span data-stu-id="da024-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="da024-153"><a name="delegate-product-subscription"> </a>Delegando a assinatura de produtos</span><span class="sxs-lookup"><span data-stu-id="da024-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="da024-154">A delegação de uma assinatura de produto funciona de forma semelhante à delegação de uma entrada/inscrição de usuário.</span><span class="sxs-lookup"><span data-stu-id="da024-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="da024-155">O fluxo de trabalho final seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="da024-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="da024-156">O desenvolvedor selecione um produto no portal do desenvolvedor do Gerenciamento de API e clica no botão Assinar</span><span class="sxs-lookup"><span data-stu-id="da024-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="da024-157">O navegador é redirecionado ao ponto de extremidade de delegação</span><span class="sxs-lookup"><span data-stu-id="da024-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="da024-158">O ponto de extremidade de delegação realiza as etapas de assinatura de produto necessária - isso depende de você e pode envolver o redirecionamento para outra página para solicitar informações de cobrança, fazer perguntas adicionais ou simplesmente armazenar as informações sem precisar de ações do usuário</span><span class="sxs-lookup"><span data-stu-id="da024-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="da024-159">Para habilitar a funcionalidade, na página **Delegação**, clique em **Delegar assinatura do produto**.</span><span class="sxs-lookup"><span data-stu-id="da024-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="da024-160">Depois, certifique-se de que o ponto de extremidade de delegação realize as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="da024-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="da024-161">Receba uma solicitação com a seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="da024-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="da024-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={produto a ser assinado}&userId={usuário que faz a solicitação}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="da024-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="da024-163">Parâmetros de consulta para a assinatura de produto:</span><span class="sxs-lookup"><span data-stu-id="da024-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="da024-164">**operation**: identifica o tipo de solicitação de delegação.</span><span class="sxs-lookup"><span data-stu-id="da024-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="da024-165">Para solicitações de assinatura do produto, as opções válidas são:</span><span class="sxs-lookup"><span data-stu-id="da024-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="da024-166">“Subscribe”: uma solicitação para que o usuário assine determinado produto com uma ID fornecida (veja abaixo)</span><span class="sxs-lookup"><span data-stu-id="da024-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="da024-167">“Unsubscribe”: uma solicitação para cancelar a assinatura do usuário de um produto</span><span class="sxs-lookup"><span data-stu-id="da024-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="da024-168">“Renew”: uma solicitação para renovar uma assinatura (que pode, por exemplo, estar expirando)</span><span class="sxs-lookup"><span data-stu-id="da024-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="da024-169">**productId**: a ID do produto para o qual o usuário solicitou uma assinatura</span><span class="sxs-lookup"><span data-stu-id="da024-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="da024-170">**userId**: a ID do usuário para quem a solicitação está sendo feita</span><span class="sxs-lookup"><span data-stu-id="da024-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="da024-171">**salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança</span><span class="sxs-lookup"><span data-stu-id="da024-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="da024-172">**sig**: um hash de segurança calculado para ser usado para comparação com seu próprio hash calculado</span><span class="sxs-lookup"><span data-stu-id="da024-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="da024-173">Confirme que a solicitação está vindo do Gerenciamento de API do Azure (opcional, mas altamente recomendado por segurança)</span><span class="sxs-lookup"><span data-stu-id="da024-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="da024-174">Calcule um hash HMAC-SHA512 de uma cadeia baseada nos parâmetros de consulta **productId**, **userId** e **salt**:</span><span class="sxs-lookup"><span data-stu-id="da024-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="da024-175">HMAC(**salt**+ '\n' +**productId**+ '\n' +**userId**)</span><span class="sxs-lookup"><span data-stu-id="da024-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="da024-176">Compare o hash calculado acima ao valor do parâmetro de consulta **sig**.</span><span class="sxs-lookup"><span data-stu-id="da024-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="da024-177">Se os dois hashes forem correspondentes, prossiga para a próxima etapa. Caso contrário, recuse as solicitações.</span><span class="sxs-lookup"><span data-stu-id="da024-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="da024-178">Faça o processamento de qualquer assinatura de produto com base no tipo de operação solicitada em **operation** - por exemplo, faturamento, perguntas etc.</span><span class="sxs-lookup"><span data-stu-id="da024-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="da024-179">Após realizar com êxito a assinatura do produto pelo usuário pela sua parte, assine o usuário do produto do Gerenciamento de API [chamando a API REST para assinatura do produto].</span><span class="sxs-lookup"><span data-stu-id="da024-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="da024-180"><a name="delegate-example-code"> </a> Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="da024-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="da024-181">Estes códigos de exemplo mostram como usar a *chave de validação de delegação*, que é definida na tela Delegação do Portal do editor, para criar um HMAC que será usado para validar a assinatura, comprovando a validade da returnUrl passada.</span><span class="sxs-lookup"><span data-stu-id="da024-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="da024-182">O mesmo código funciona para productId e userId com pequenas modificações.</span><span class="sxs-lookup"><span data-stu-id="da024-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="da024-183">**Código C# para gerar hash de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="da024-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="da024-184">**Código NodeJS para gerar hash de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="da024-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="da024-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da024-185">Next steps</span></span>
<span data-ttu-id="da024-186">Para obter mais informações sobre delegação, consulte o vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="da024-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="da024-187">[solicite um token de logon único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="da024-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="da024-188">[Crie um usuário]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="da024-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="da024-189">[chamando a API REST para assinatura do produto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="da024-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="da024-190">[código de exemplo fornecido abaixo]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="da024-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
