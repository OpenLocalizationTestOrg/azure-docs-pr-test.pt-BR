---
title: APIs do SDK para Web do Azure Mobile Engagement | Microsoft Docs
description: "As atualizações e procedimentos mais recentes do SDK para Web do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="4f10b-103">Usar a API do Azure Mobile Engagement em um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="4f10b-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="4f10b-104">Este documento é um complemento do documento que descreve como [integrar o Mobile Engagement a um aplicativo Web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="4f10b-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="4f10b-105">Ele fornece detalhes aprofundados sobre como usar a API do Azure Mobile Engagement para relatar as estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f10b-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="4f10b-106">A API do Mobile Engagement é fornecida pelo objeto `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="4f10b-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="4f10b-107">O alias padrão do SDK Web do Azure Mobile Engagement é `engagement`.</span><span class="sxs-lookup"><span data-stu-id="4f10b-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="4f10b-108">Você pode redefinir esse alias na configuração do SDK.</span><span class="sxs-lookup"><span data-stu-id="4f10b-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="4f10b-109">Conceitos do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4f10b-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="4f10b-110">As partes a seguir refinam os [Conceitos do Mobile Engagement](mobile-engagement-concepts.md) comuns para a plataforma da Web.</span><span class="sxs-lookup"><span data-stu-id="4f10b-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="4f10b-111">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="4f10b-111">`Session` and `Activity`</span></span>
<span data-ttu-id="4f10b-112">Se o usuário permanecer ocioso mais de alguns segundos entre duas atividades, a sua sequência de atividades é dividida em duas sessões diferentes.</span><span class="sxs-lookup"><span data-stu-id="4f10b-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="4f10b-113">Esses poucos segundos são chamados de tempo limite da sessão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="4f10b-114">Se o aplicativo Web não declarar o fim das atividades do usuário por si só (chamando a função `engagement.agent.endActivity` ), o servidor do Mobile Engagement vai expirar automaticamente a sessão do usuário em três minutos depois que a página do aplicativo for fechada.</span><span class="sxs-lookup"><span data-stu-id="4f10b-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="4f10b-115">Isso é chamado de tempo limite da sessão do servidor.</span><span class="sxs-lookup"><span data-stu-id="4f10b-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="4f10b-116">Relatórios automatizados de exceções não identificadas de JavaScript não são criados por padrão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="4f10b-117">No entanto, você pode relatar falhas manualmente usando a função `sendCrash` (confira a seção sobre relatórios de falhas).</span><span class="sxs-lookup"><span data-stu-id="4f10b-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="4f10b-118">Relatando atividades</span><span class="sxs-lookup"><span data-stu-id="4f10b-118">Reporting activities</span></span>
<span data-ttu-id="4f10b-119">Relatórios sobre a atividade de usuário incluem quando um usuário inicia uma nova atividade e quando o usuário encerra a atividade atual.</span><span class="sxs-lookup"><span data-stu-id="4f10b-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="4f10b-120">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="4f10b-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="4f10b-121">É necessário chamar `startActivity()` sempre que houver alterações de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="4f10b-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="4f10b-122">A primeira chamada para essa função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="4f10b-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="4f10b-123">O usuário encerra a atividade atual</span><span class="sxs-lookup"><span data-stu-id="4f10b-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="4f10b-124">É necessário chamar `endActivity()` pelo menos uma vez quando o usuário conclui sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="4f10b-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="4f10b-125">Isso informa ao SDK Web do Mobile Engagement que o usuário está ocioso no momento e que a sessão do usuário precisa ser fechada quanto o tempo limite expirar.</span><span class="sxs-lookup"><span data-stu-id="4f10b-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="4f10b-126">Se você chamar `startActivity()` antes de expirar o tempo limite da sessão, a sessão será simplesmente retomada.</span><span class="sxs-lookup"><span data-stu-id="4f10b-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="4f10b-127">Como não existe uma chamada confiável quando a janela do navegador é fechada, muitas vezes isso dificulta ou impossibilita capturar o fim das atividades do usuário em ambientes da Web.</span><span class="sxs-lookup"><span data-stu-id="4f10b-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="4f10b-128">Por esse motivo, o servidor do Mobile Engagement expira automaticamente a sessão do usuário em três minutos depois que a página do aplicativo é fechada.</span><span class="sxs-lookup"><span data-stu-id="4f10b-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="4f10b-129">Relatando eventos</span><span class="sxs-lookup"><span data-stu-id="4f10b-129">Reporting events</span></span>
<span data-ttu-id="4f10b-130">Relatórios sobre eventos abordam eventos de sessão e eventos autônomos.</span><span class="sxs-lookup"><span data-stu-id="4f10b-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="4f10b-131">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="4f10b-131">Session events</span></span>
<span data-ttu-id="4f10b-132">Eventos de sessão são geralmente usados para relatar as ações executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="4f10b-133">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="4f10b-134">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="4f10b-135">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="4f10b-135">Standalone events</span></span>
<span data-ttu-id="4f10b-136">Ao contrário dos eventos de sessão, os eventos independentes podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="4f10b-137">Para isso, use ``engagement.agent.sendEvent`` em vez de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="4f10b-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="4f10b-138">Relatando erros</span><span class="sxs-lookup"><span data-stu-id="4f10b-138">Reporting errors</span></span>
<span data-ttu-id="4f10b-139">Relatórios de erros abordam erros de sessão e autônomos.</span><span class="sxs-lookup"><span data-stu-id="4f10b-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="4f10b-140">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="4f10b-140">Session errors</span></span>
<span data-ttu-id="4f10b-141">Erros de sessão geralmente são usados para relatar os erros que têm um impacto no usuário durante sua sessão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="4f10b-142">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="4f10b-143">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="4f10b-144">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="4f10b-144">Standalone errors</span></span>
<span data-ttu-id="4f10b-145">Ao contrário dos erros de sessão, os erros autônomos podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="4f10b-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="4f10b-146">Para isso, use `engagement.agent.sendError` em vez de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="4f10b-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="4f10b-147">Relatando trabalhos</span><span class="sxs-lookup"><span data-stu-id="4f10b-147">Reporting jobs</span></span>
<span data-ttu-id="4f10b-148">Relatórios sobre trabalhos abrangem erros e eventos que ocorrem durante um trabalho de emissão de relatórios e relatórios de falhas.</span><span class="sxs-lookup"><span data-stu-id="4f10b-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="4f10b-149">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-149">**Example:**</span></span>

<span data-ttu-id="4f10b-150">Se você quer monitorar uma solicitação AJAX, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4f10b-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="4f10b-151">Relatando erros durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="4f10b-151">Reporting errors during a job</span></span>
<span data-ttu-id="4f10b-152">Os erros podem estar relacionados a um trabalho em execução, em vez de a uma sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="4f10b-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="4f10b-153">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-153">**Example:**</span></span>

<span data-ttu-id="4f10b-154">Suponha que você queira relatar um erro se uma solicitação AJAX falhar:</span><span class="sxs-lookup"><span data-stu-id="4f10b-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="4f10b-155">Relatar eventos durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="4f10b-155">Reporting events during a job</span></span>
<span data-ttu-id="4f10b-156">Os erros podem estar relacionados a um trabalho em execução, em vez de à sessão do usuário atual graças à função `engagement.agent.sendJobEvent` .</span><span class="sxs-lookup"><span data-stu-id="4f10b-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="4f10b-157">Essa função funciona exatamente como `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="4f10b-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="4f10b-158">Relatando falhas</span><span class="sxs-lookup"><span data-stu-id="4f10b-158">Reporting crashes</span></span>
<span data-ttu-id="4f10b-159">Use a função `sendCrash` para relatar falhas manualmente.</span><span class="sxs-lookup"><span data-stu-id="4f10b-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="4f10b-160">O `crashid` é uma cadeia de caracteres que identifica o tipo de falha.</span><span class="sxs-lookup"><span data-stu-id="4f10b-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="4f10b-161">O `crash` é geralmente o rastreamento de pilha da falha como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="4f10b-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="4f10b-162">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="4f10b-162">Extra parameters</span></span>
<span data-ttu-id="4f10b-163">Você pode anexar dados arbitrários a evento, erro, atividade ou trabalho.</span><span class="sxs-lookup"><span data-stu-id="4f10b-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="4f10b-164">Esses dados podem ser qualquer objeto JSON (mas não uma matriz ou tipos primitivos).</span><span class="sxs-lookup"><span data-stu-id="4f10b-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="4f10b-165">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="4f10b-166">Limites</span><span class="sxs-lookup"><span data-stu-id="4f10b-166">Limits</span></span>
<span data-ttu-id="4f10b-167">Limites que se aplicam a parâmetros extras estão nas áreas de expressões regulares de chaves, tipos de valor e tamanho.</span><span class="sxs-lookup"><span data-stu-id="4f10b-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="4f10b-168">simétricas</span><span class="sxs-lookup"><span data-stu-id="4f10b-168">Keys</span></span>
<span data-ttu-id="4f10b-169">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="4f10b-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="4f10b-170">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="4f10b-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="4f10b-171">Valores</span><span class="sxs-lookup"><span data-stu-id="4f10b-171">Values</span></span>
<span data-ttu-id="4f10b-172">Os valores são limitados aos tipos de booliano, número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="4f10b-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="4f10b-173">Tamanho</span><span class="sxs-lookup"><span data-stu-id="4f10b-173">Size</span></span>
<span data-ttu-id="4f10b-174">Os extras são limitados a 1024 caracteres por chamada (depois que o SDK Web do Mobile Engagement codifica em JSON).</span><span class="sxs-lookup"><span data-stu-id="4f10b-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="4f10b-175">Relatando informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4f10b-175">Reporting application information</span></span>
<span data-ttu-id="4f10b-176">Você pode relatar manualmente informações (ou quaisquer outras informações específicas do aplicativo) de controle usando a função `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="4f10b-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="4f10b-177">Observe que essas informações podem ser enviadas de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="4f10b-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="4f10b-178">Somente o último valor para uma chave específica será mantido para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4f10b-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="4f10b-179">Como extras de evento, você pode usar qualquer objeto JSON para abstrair as informações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f10b-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="4f10b-180">Observe que matrizes ou subobjetos são tratados como cadeias de caracteres simples (usando a serialização JSON).</span><span class="sxs-lookup"><span data-stu-id="4f10b-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="4f10b-181">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4f10b-181">**Example:**</span></span>

<span data-ttu-id="4f10b-182">Aqui está um exemplo de código para enviar a data de nascimento e o sexo do usuário:</span><span class="sxs-lookup"><span data-stu-id="4f10b-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="4f10b-183">Limites</span><span class="sxs-lookup"><span data-stu-id="4f10b-183">Limits</span></span>
<span data-ttu-id="4f10b-184">Limites que se aplicam às informações do aplicativo são nas áreas de expressões regulares de chaves e tamanho.</span><span class="sxs-lookup"><span data-stu-id="4f10b-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="4f10b-185">simétricas</span><span class="sxs-lookup"><span data-stu-id="4f10b-185">Keys</span></span>
<span data-ttu-id="4f10b-186">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="4f10b-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="4f10b-187">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="4f10b-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4f10b-188">Tamanho</span><span class="sxs-lookup"><span data-stu-id="4f10b-188">Size</span></span>
<span data-ttu-id="4f10b-189">Informações do aplicativo são limitadas a 1024 caracteres por chamada (depois que o SDK Web do Mobile Engagement codifica em JSON).</span><span class="sxs-lookup"><span data-stu-id="4f10b-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="4f10b-190">No exemplo anterior, o JSON enviado para o servidor tem 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="4f10b-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
