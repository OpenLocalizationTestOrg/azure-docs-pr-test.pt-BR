---
title: aaaAzure APIs do SDK do Mobile Engagement Web | Microsoft Docs
description: "Olá procedimentos para Olá Web SDK e atualizações mais recentes para o Azure Mobile Engagement"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="78bdb-103">Saudação de usar a API do Azure Mobile Engagement em um aplicativo web</span><span class="sxs-lookup"><span data-stu-id="78bdb-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="78bdb-104">Este é um documento de toohello adição que informa como muito[integrar o Mobile Engagement em um aplicativo web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="78bdb-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="78bdb-105">Ele fornece detalhes sobre como toouse Olá tooreport da API do Azure Mobile Engagement suas estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78bdb-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="78bdb-106">Olá Mobile Engagement API fornecida pelo Olá `engagement.agent` objeto.</span><span class="sxs-lookup"><span data-stu-id="78bdb-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="78bdb-107">Olá padrão da Web SDK do Azure Mobile Engagement alias é `engagement`.</span><span class="sxs-lookup"><span data-stu-id="78bdb-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="78bdb-108">Você pode redefinir este alias da configuração de SDK hello.</span><span class="sxs-lookup"><span data-stu-id="78bdb-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="78bdb-109">Conceitos do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="78bdb-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="78bdb-110">Olá seguintes partes refinar comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) de plataforma da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bdb-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="78bdb-111">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="78bdb-111">`Session` and `Activity`</span></span>
<span data-ttu-id="78bdb-112">Se o usuário Olá permanecer ocioso por mais de alguns segundos entre duas atividades, hello sequência do usuário de atividades é dividida em duas sessões distintas.</span><span class="sxs-lookup"><span data-stu-id="78bdb-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="78bdb-113">Esses alguns segundos são chamados de tempo limite da sessão hello.</span><span class="sxs-lookup"><span data-stu-id="78bdb-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="78bdb-114">Se seu aplicativo da web não declara final Olá de atividades do usuário por si só (por chamada hello `engagement.agent.endActivity` função), servidor do Mobile Engagement Olá expira automaticamente Olá sessão de usuário dentro de três minutos após a página de aplicativo hello está fechada.</span><span class="sxs-lookup"><span data-stu-id="78bdb-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="78bdb-115">Isso é chamado de tempo limite de sessão de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bdb-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="78bdb-116">Relatórios automatizados de exceções não identificadas de JavaScript não são criados por padrão.</span><span class="sxs-lookup"><span data-stu-id="78bdb-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="78bdb-117">No entanto, você pode relatar falhas manualmente usando Olá `sendCrash` função (consulte a seção de saudação nos relatórios de falhas).</span><span class="sxs-lookup"><span data-stu-id="78bdb-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="78bdb-118">Relatando atividades</span><span class="sxs-lookup"><span data-stu-id="78bdb-118">Reporting activities</span></span>
<span data-ttu-id="78bdb-119">Relatório de atividade de usuário inclui quando um usuário inicia uma nova atividade e quando o usuário Olá termina a atividade atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bdb-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="78bdb-120">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="78bdb-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="78bdb-121">Você precisa toocall `startActivity()` alterações de cada atividade de usuário do tempo.</span><span class="sxs-lookup"><span data-stu-id="78bdb-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="78bdb-122">Olá primeira chamada toothis função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="78bdb-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="78bdb-123">Usuário encerra a atividade atual de saudação</span><span class="sxs-lookup"><span data-stu-id="78bdb-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="78bdb-124">Você precisa toocall `endActivity()` pelo menos uma vez quando o usuário Olá termina sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="78bdb-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="78bdb-125">Isso informa Olá Web SDK do Mobile Engagement que usuário hello está ocioso no momento e que a sessão de usuário Olá precisa toobe fechado após a expiração do tempo limite da sessão hello.</span><span class="sxs-lookup"><span data-stu-id="78bdb-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="78bdb-126">Se você chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado.</span><span class="sxs-lookup"><span data-stu-id="78bdb-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="78bdb-127">Como não há nenhuma chamada confiável para quando a janela do navegador hello está fechada, geralmente é final de saudação toocatch difíceis ou impossíveis de atividades do usuário dentro de um ambiente web.</span><span class="sxs-lookup"><span data-stu-id="78bdb-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="78bdb-128">Por que é Olá Mobile Engagement servidor expira automaticamente sessão de usuário hello dentro de três minutos após a página de aplicativo hello está fechada.</span><span class="sxs-lookup"><span data-stu-id="78bdb-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="78bdb-129">Relatando eventos</span><span class="sxs-lookup"><span data-stu-id="78bdb-129">Reporting events</span></span>
<span data-ttu-id="78bdb-130">Relatórios sobre eventos abordam eventos de sessão e eventos autônomos.</span><span class="sxs-lookup"><span data-stu-id="78bdb-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="78bdb-131">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="78bdb-131">Session events</span></span>
<span data-ttu-id="78bdb-132">Eventos de sessão normalmente são ações de saudação tooreport usado executadas por um usuário durante a sessão de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="78bdb-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="78bdb-133">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="78bdb-134">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="78bdb-135">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="78bdb-135">Standalone events</span></span>
<span data-ttu-id="78bdb-136">Ao contrário de eventos de sessão, podem ocorrer eventos de autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="78bdb-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="78bdb-137">Para isso, use ``engagement.agent.sendEvent`` em vez de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="78bdb-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="78bdb-138">Relatando erros</span><span class="sxs-lookup"><span data-stu-id="78bdb-138">Reporting errors</span></span>
<span data-ttu-id="78bdb-139">Relatórios de erros abordam erros de sessão e autônomos.</span><span class="sxs-lookup"><span data-stu-id="78bdb-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="78bdb-140">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="78bdb-140">Session errors</span></span>
<span data-ttu-id="78bdb-141">Erros de sessão normalmente são erros de saudação tooreport usadas que têm um impacto no usuário Olá durante a sessão do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="78bdb-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="78bdb-142">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="78bdb-143">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="78bdb-144">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="78bdb-144">Standalone errors</span></span>
<span data-ttu-id="78bdb-145">Ao contrário dos erros de sessão, podem ocorrer erros de autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="78bdb-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="78bdb-146">Para isso, use `engagement.agent.sendError` em vez de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="78bdb-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="78bdb-147">Relatando trabalhos</span><span class="sxs-lookup"><span data-stu-id="78bdb-147">Reporting jobs</span></span>
<span data-ttu-id="78bdb-148">Relatórios sobre trabalhos abrangem erros e eventos que ocorrem durante um trabalho de emissão de relatórios e relatórios de falhas.</span><span class="sxs-lookup"><span data-stu-id="78bdb-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="78bdb-149">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-149">**Example:**</span></span>

<span data-ttu-id="78bdb-150">Se você quiser toomonitor uma solicitação AJAX, você usaria o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="78bdb-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="78bdb-151">Relatando erros durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="78bdb-151">Reporting errors during a job</span></span>
<span data-ttu-id="78bdb-152">Erros podem ser relacionada tooa executando o trabalho em vez de toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="78bdb-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="78bdb-153">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-153">**Example:**</span></span>

<span data-ttu-id="78bdb-154">Se você quiser tooreport um erro se uma solicitação AJAX falha:</span><span class="sxs-lookup"><span data-stu-id="78bdb-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="78bdb-155">Relatar eventos durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="78bdb-155">Reporting events during a job</span></span>
<span data-ttu-id="78bdb-156">Os eventos podem ser relacionada tooa executando o trabalho em vez de toohello a sessão atual do usuário, graças toohello `engagement.agent.sendJobEvent` função.</span><span class="sxs-lookup"><span data-stu-id="78bdb-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="78bdb-157">Essa função funciona exatamente como `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="78bdb-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="78bdb-158">Relatando falhas</span><span class="sxs-lookup"><span data-stu-id="78bdb-158">Reporting crashes</span></span>
<span data-ttu-id="78bdb-159">Saudação de uso `sendCrash` função tooreport falhas manualmente.</span><span class="sxs-lookup"><span data-stu-id="78bdb-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="78bdb-160">Olá `crashid` argumento é uma cadeia de caracteres que identifica o tipo de saudação de travamento.</span><span class="sxs-lookup"><span data-stu-id="78bdb-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="78bdb-161">Olá `crash` argumento geralmente é o rastreamento de pilha de saudação de travamento hello como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="78bdb-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="78bdb-162">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="78bdb-162">Extra parameters</span></span>
<span data-ttu-id="78bdb-163">Você pode anexar dados arbitrários tooan eventos, erro, atividade ou trabalho.</span><span class="sxs-lookup"><span data-stu-id="78bdb-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="78bdb-164">dados de saudação podem ser qualquer objeto JSON (mas não uma matriz ou tipo primitivo).</span><span class="sxs-lookup"><span data-stu-id="78bdb-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="78bdb-165">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="78bdb-166">limites</span><span class="sxs-lookup"><span data-stu-id="78bdb-166">Limits</span></span>
<span data-ttu-id="78bdb-167">Limites que se aplicam a parâmetros tooextra são áreas de saudação de expressões regulares para chaves, tipos de valor e tamanho.</span><span class="sxs-lookup"><span data-stu-id="78bdb-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="78bdb-168">simétricas</span><span class="sxs-lookup"><span data-stu-id="78bdb-168">Keys</span></span>
<span data-ttu-id="78bdb-169">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bdb-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="78bdb-170">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="78bdb-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="78bdb-171">Valores</span><span class="sxs-lookup"><span data-stu-id="78bdb-171">Values</span></span>
<span data-ttu-id="78bdb-172">Os valores são toostring limitado, número e tipos boolianos.</span><span class="sxs-lookup"><span data-stu-id="78bdb-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="78bdb-173">Tamanho</span><span class="sxs-lookup"><span data-stu-id="78bdb-173">Size</span></span>
<span data-ttu-id="78bdb-174">Extras são limitados too1, 024 caracteres por chamada (após Olá Web SDK do Mobile Engagement codifica em JSON).</span><span class="sxs-lookup"><span data-stu-id="78bdb-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="78bdb-175">Relatando informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="78bdb-175">Reporting application information</span></span>
<span data-ttu-id="78bdb-176">Você pode relatar informações (ou quaisquer outras informações específicas do aplicativo) de rastreamento manualmente usando Olá `sendAppInfo()` função.</span><span class="sxs-lookup"><span data-stu-id="78bdb-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="78bdb-177">Observe que essas informações podem ser enviadas de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="78bdb-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="78bdb-178">Somente Olá valor mais recente para uma chave específica será mantido para um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="78bdb-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="78bdb-179">Como o evento extras, você pode usar informações de aplicativo tooabstract do objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="78bdb-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="78bdb-180">Observe que matrizes ou subobjetos são tratados como cadeias de caracteres simples (usando a serialização JSON).</span><span class="sxs-lookup"><span data-stu-id="78bdb-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="78bdb-181">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="78bdb-181">**Example:**</span></span>

<span data-ttu-id="78bdb-182">Aqui está um exemplo de código de gênero do usuário Olá envio e a data de nascimento:</span><span class="sxs-lookup"><span data-stu-id="78bdb-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="78bdb-183">limites</span><span class="sxs-lookup"><span data-stu-id="78bdb-183">Limits</span></span>
<span data-ttu-id="78bdb-184">Limites que se aplicam a tooapplication informações estão em áreas de saudação de expressões regulares de chaves e tamanho.</span><span class="sxs-lookup"><span data-stu-id="78bdb-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="78bdb-185">simétricas</span><span class="sxs-lookup"><span data-stu-id="78bdb-185">Keys</span></span>
<span data-ttu-id="78bdb-186">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bdb-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="78bdb-187">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="78bdb-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="78bdb-188">Tamanho</span><span class="sxs-lookup"><span data-stu-id="78bdb-188">Size</span></span>
<span data-ttu-id="78bdb-189">Informações do aplicativo são limitado too1, 024 caracteres por chamada (após Olá Web SDK do Mobile Engagement codifica em JSON).</span><span class="sxs-lookup"><span data-stu-id="78bdb-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="78bdb-190">Em Olá anterior de exemplo, hello JSON enviado toohello server é 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="78bdb-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
