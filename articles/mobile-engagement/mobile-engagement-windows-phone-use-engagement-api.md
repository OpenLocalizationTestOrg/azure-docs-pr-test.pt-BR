---
title: "saudação de tooUse aaaHow contrato de API no Windows Phone Silverlight"
description: "Como tooUse Olá contrato de API no Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="8037f-103">Como tooUse Olá contrato de API no Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8037f-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="8037f-104">Este é um documento de toohello complemento [como toointegrate Mobile Engagement em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8037f-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="8037f-105">Ele fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8037f-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="8037f-106">Se desejar somente contrato tooreport sessões, atividades, falhas e obter informações técnicas do seu aplicativo, hello mais simples é forma toomake todos os seus `PhoneApplicationPage` subclasses herdam Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="8037f-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="8037f-107">Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementPage` classes, e em seguida, você precisa toouse Olá Contrato de API.</span><span class="sxs-lookup"><span data-stu-id="8037f-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="8037f-108">Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="8037f-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="8037f-109">Você pode acessar os métodos de toothose por meio de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="8037f-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="8037f-110">Mesmo que o módulo de saudação do agente não foi inicializado, cada API toohello de chamada é adiada e será executado novamente quando o agente hello está disponível.</span><span class="sxs-lookup"><span data-stu-id="8037f-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="8037f-111">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="8037f-111">Engagement concepts</span></span>
<span data-ttu-id="8037f-112">Olá partes a seguir refinar Olá Mobile Engagement conceitos para a plataforma do Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="8037f-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="8037f-113">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="8037f-113">`Session` and `Activity`</span></span>
<span data-ttu-id="8037f-114">Um *atividade* geralmente está associado com uma página de aplicativo hello, que é toosay hello *atividade* inicia quando a página Olá é exibida e é interrompido quando Olá página é fechada: esse é o caso de Olá quando hello SDK do contrato é integrado usando Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="8037f-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="8037f-115">Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API.</span><span class="sxs-lookup"><span data-stu-id="8037f-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="8037f-116">Isso permite uma determinada página toosplit em vários tooget de partes sub Olá de obter mais detalhes sobre o uso desta página (por exemplo tooknown frequência e quanto tempo as caixas de diálogo são usadas dentro desta página).</span><span class="sxs-lookup"><span data-stu-id="8037f-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="8037f-117">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="8037f-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="8037f-118">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="8037f-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-119">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-120">Você precisa toocall `StartActivity()` alterações de cada atividade de usuário de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="8037f-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="8037f-121">Olá primeira chamada toothis função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="8037f-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8037f-122">Olá SDK automaticamente chamar o método de EndActivity de saudação quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="8037f-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="8037f-123">Portanto, é altamente recomendável método de StartActivity toocall hello sempre que hello atividade de alteração de usuário hello e chamada tooNEVER Olá método EndActivity, desde chamar esse método força Olá atual sessão toobe finalizada.</span><span class="sxs-lookup"><span data-stu-id="8037f-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="8037f-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="8037f-125">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="8037f-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-126">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="8037f-127">Você precisa toocall `EndActivity()` pelo menos uma vez quando o usuário Olá termina sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="8037f-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="8037f-128">Isso informa Olá expirará SDK de contrato que usuário hello está ocioso no momento e que a sessão de usuário Olá necessário toobe uma vez fechado Olá tempo limite da sessão (se você chamar `StartActivity()` antes do tempo limite da sessão Olá expira, simplesmente continua sessão Olá).</span><span class="sxs-lookup"><span data-stu-id="8037f-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="8037f-130">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="8037f-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="8037f-131">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-132">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-133">Você pode usar o hello tootrack alguns tarefas em um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="8037f-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="8037f-135">Encerrar um trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-136">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="8037f-137">Assim que uma tarefa controlada por um trabalho foi encerrada, você deve chamar o método de EndJob de saudação para esse trabalho, fornecendo o nome do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="8037f-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="8037f-139">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="8037f-139">Reporting Events</span></span>
<span data-ttu-id="8037f-140">Há três tipos de eventos :</span><span class="sxs-lookup"><span data-stu-id="8037f-140">There is three types of events :</span></span>

* <span data-ttu-id="8037f-141">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="8037f-141">Standalone events</span></span>
* <span data-ttu-id="8037f-142">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="8037f-142">Session events</span></span>
* <span data-ttu-id="8037f-143">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="8037f-144">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="8037f-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-145">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-146">Autônomo eventos podem ocorrer fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="8037f-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-147">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="8037f-148">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="8037f-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-149">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-150">Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="8037f-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-151">Example</span></span>
<span data-ttu-id="8037f-152">**Sem dados :**</span><span class="sxs-lookup"><span data-stu-id="8037f-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="8037f-153">**Com dados :**</span><span class="sxs-lookup"><span data-stu-id="8037f-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="8037f-154">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-155">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-156">Eventos de trabalho são ações que Olá tooreport usados normalmente executadas por um usuário durante um trabalho.</span><span class="sxs-lookup"><span data-stu-id="8037f-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-157">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="8037f-158">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="8037f-158">Reporting Errors</span></span>
<span data-ttu-id="8037f-159">Há três tipos de erros:</span><span class="sxs-lookup"><span data-stu-id="8037f-159">There is three types of errors :</span></span>

* <span data-ttu-id="8037f-160">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="8037f-160">Standalone errors</span></span>
* <span data-ttu-id="8037f-161">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="8037f-161">Session errors</span></span>
* <span data-ttu-id="8037f-162">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="8037f-163">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="8037f-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-164">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-165">Erros de toosession contrary, podem ocorrer erros autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="8037f-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="8037f-167">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="8037f-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-168">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-169">Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="8037f-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="8037f-171">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="8037f-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-172">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8037f-173">Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="8037f-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="8037f-175">Relatórios de falhas</span><span class="sxs-lookup"><span data-stu-id="8037f-175">Reporting Crashes</span></span>
<span data-ttu-id="8037f-176">Agente de saudação fornece dois toodeal de métodos com falhas.</span><span class="sxs-lookup"><span data-stu-id="8037f-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="8037f-177">Enviar uma exceção</span><span class="sxs-lookup"><span data-stu-id="8037f-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-178">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="8037f-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-179">Example</span></span>
<span data-ttu-id="8037f-180">Você pode enviar uma exceção a qualquer momento chamando :</span><span class="sxs-lookup"><span data-stu-id="8037f-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="8037f-181">Você também pode usar uma sessão de contrato de saudação do parâmetro opcional tooterminate em Olá mesmo tempo que o envio de falhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8037f-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="8037f-182">Portanto, chame toodo:</span><span class="sxs-lookup"><span data-stu-id="8037f-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="8037f-183">Se você fizer isso, trabalhos e sessão Olá serão fechados imediatamente após enviar falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="8037f-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="8037f-184">Enviar uma exceção sem tratamento</span><span class="sxs-lookup"><span data-stu-id="8037f-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8037f-185">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="8037f-186">Contrato também fornece um exceções toosend sem tratamento do método.</span><span class="sxs-lookup"><span data-stu-id="8037f-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="8037f-187">Isso é especialmente útil quando usado dentro do manipulador de eventos de UnhandledException Olá silverlight.</span><span class="sxs-lookup"><span data-stu-id="8037f-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="8037f-188">Esse método será **sempre** encerrar a sessão de contrato hello e trabalhos após a chamada.</span><span class="sxs-lookup"><span data-stu-id="8037f-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="8037f-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-189">Example</span></span>
<span data-ttu-id="8037f-190">Você pode usá-lo tooimplement seu próprio manipulador de UnhandledException (especialmente se você tiver desabilitado o recurso de contrato de relatório de falha automático do hello).</span><span class="sxs-lookup"><span data-stu-id="8037f-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="8037f-191">Por exemplo, em Olá `Application_UnhandledException` método hello `App.xaml.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="8037f-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="8037f-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="8037f-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="8037f-193">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="8037f-194">Quando o usuário de hello, navegar para fora de um aplicativo, depois Olá desativado é gerado, o sistema de operacional de saudação tentará aplicativo hello de tooput em um estado inativo.</span><span class="sxs-lookup"><span data-stu-id="8037f-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="8037f-195">Em seguida, o aplicativo hello é marca de exclusão.</span><span class="sxs-lookup"><span data-stu-id="8037f-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="8037f-196">Neste processo, um aplicativo é encerrado, mas alguns dados sobre o estado de saudação do aplicativo hello e páginas individuais Olá aplicativo hello são preservados.</span><span class="sxs-lookup"><span data-stu-id="8037f-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="8037f-197">Você tem tooinsert `EngagementAgent.Instance.OnActivated(e)` em Olá `Application_Activated` método de Olá App.xaml.cs arquivo tooreset Olá contrato agente quando o aplicativo hello foi inativo.</span><span class="sxs-lookup"><span data-stu-id="8037f-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="8037f-198">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="8037f-199">Id do dispositivo</span><span class="sxs-lookup"><span data-stu-id="8037f-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="8037f-200">Você pode obter o id do dispositivo Olá engagement por chamar esse método.</span><span class="sxs-lookup"><span data-stu-id="8037f-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="8037f-201">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="8037f-201">Extras parameters</span></span>
<span data-ttu-id="8037f-202">Dados arbitrários podem ser anexados tooan evento, um erro, uma atividade ou um trabalho.</span><span class="sxs-lookup"><span data-stu-id="8037f-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="8037f-203">Esses dados podem ser estruturados usando um dicionário.</span><span class="sxs-lookup"><span data-stu-id="8037f-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="8037f-204">Chaves e valores podem ser de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="8037f-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="8037f-205">Dados extras são serializados para que tooinsert seu próprio tipo de extras você ter se tooadd um contrato de dados para este tipo.</span><span class="sxs-lookup"><span data-stu-id="8037f-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="8037f-206">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-206">Example</span></span>
<span data-ttu-id="8037f-207">Criamos uma nova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="8037f-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="8037f-208">Em seguida, adicionaremos um `Person` tooan de instância extra.</span><span class="sxs-lookup"><span data-stu-id="8037f-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="8037f-209">Se você colocar outros tipos de objetos, verifique se que o método ToString () é implementado tooreturn uma cadeia de caracteres legível humana.</span><span class="sxs-lookup"><span data-stu-id="8037f-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="8037f-210">limites</span><span class="sxs-lookup"><span data-stu-id="8037f-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8037f-211">simétricas</span><span class="sxs-lookup"><span data-stu-id="8037f-211">Keys</span></span>
<span data-ttu-id="8037f-212">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="8037f-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8037f-213">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="8037f-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8037f-214">Tamanho</span><span class="sxs-lookup"><span data-stu-id="8037f-214">Size</span></span>
<span data-ttu-id="8037f-215">Extras são muito limitadas**1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="8037f-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="8037f-216">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8037f-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="8037f-217">Referência</span><span class="sxs-lookup"><span data-stu-id="8037f-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="8037f-218">Manualmente, você pode relatar informações (ou quaisquer outras informações específicas do aplicativo) usando a função de SendAppInfo() hello de controle.</span><span class="sxs-lookup"><span data-stu-id="8037f-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="8037f-219">Observe que essas informações podem ser enviadas incrementalmente: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8037f-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="8037f-220">Como o evento extras, usar um dicionário\<objeto, objeto\> tooattach informações.</span><span class="sxs-lookup"><span data-stu-id="8037f-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="8037f-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8037f-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="8037f-222">Limites</span><span class="sxs-lookup"><span data-stu-id="8037f-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8037f-223">simétricas</span><span class="sxs-lookup"><span data-stu-id="8037f-223">Keys</span></span>
<span data-ttu-id="8037f-224">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="8037f-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8037f-225">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="8037f-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8037f-226">Tamanho</span><span class="sxs-lookup"><span data-stu-id="8037f-226">Size</span></span>
<span data-ttu-id="8037f-227">Informações do aplicativo são muito limitadas**1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="8037f-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="8037f-228">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="8037f-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="8037f-229">Registro em log</span><span class="sxs-lookup"><span data-stu-id="8037f-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="8037f-230">Habilitar registro em log</span><span class="sxs-lookup"><span data-stu-id="8037f-230">Enable Logging</span></span>
<span data-ttu-id="8037f-231">Olá SDK pode ser configurado tooproduce logs de teste no console do IDE hello.</span><span class="sxs-lookup"><span data-stu-id="8037f-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="8037f-232">Esses logs não são ativados por padrão.</span><span class="sxs-lookup"><span data-stu-id="8037f-232">These logs are not activated by default.</span></span> <span data-ttu-id="8037f-233">toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8037f-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
