---
title: Como usar o API do Engagement no Windows Phone Silverlight
description: Como usar o API do Engagement no Windows Phone Silverlight
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="b27ae-103">Como usar o API do Engagement no Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b27ae-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="b27ae-104">Este documento é um complemento para o documento [Como integrar o Mobile Engagement em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="b27ae-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="b27ae-105">Ele fornece detalhes aprofundados sobre como usar a API do Engagement para relatar as estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="b27ae-106">Se você desejar apenas relatar as sessões, atividades, falhas e informações técnicas do seu aplicativo, então a maneira mais simples é fazer todas as suas subclasses `PhoneApplicationPage` herdarem da classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="b27ae-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="b27ae-107">Se você quiser fazer mais, por exemplo, se você precisar reportar eventos, erros e trabalhos específicos do aplicativo ou se você tiver que relatar as atividades do seu aplicativo de maneira diferente de um implementado nas classes `EngagementPage`, você precisará usar a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="b27ae-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="b27ae-108">A API do Engagement é fornecida pela classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="b27ae-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="b27ae-109">Você pode obter acesso a esses métodos por meio de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="b27ae-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="b27ae-110">Mesmo se o módulo de agente não foi inicializado, cada chamada para a API é adiada e será executada novamente quando o agente está disponível.</span><span class="sxs-lookup"><span data-stu-id="b27ae-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="b27ae-111">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="b27ae-111">Engagement concepts</span></span>
<span data-ttu-id="b27ae-112">As seguintes partes refinam os Conceitos de Mobile Engagement para a plataforma do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b27ae-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="b27ae-113">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="b27ae-113">`Session` and `Activity`</span></span>
<span data-ttu-id="b27ae-114">Uma *atividade* geralmente está associada a uma página de aplicativo. Isso significa que a *atividade* iniciará quando a página for exibida e será interrompida quando a página for fechada: esse é o caso quando o SDK do Engagement é integrado usando a classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="b27ae-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="b27ae-115">Mas as *atividades* também podem ser controladas manualmente usando a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="b27ae-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="b27ae-116">Isso permite dividir uma determinada página em várias partes secundárias para obter mais detalhes sobre o uso desta página (por exemplo para saber com que frequência e por quanto tempo as caixas de diálogo são usadas dentro desta página).</span><span class="sxs-lookup"><span data-stu-id="b27ae-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="b27ae-117">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="b27ae-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="b27ae-118">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="b27ae-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-119">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-120">É necessário chamar `StartActivity()` sempre que houver alterações de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="b27ae-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="b27ae-121">A primeira chamada para essa função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="b27ae-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b27ae-122">O SDK chama automaticamente o método EndActivity quando o aplicativo é fechado.</span><span class="sxs-lookup"><span data-stu-id="b27ae-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="b27ae-123">Portanto, é ALTAMENTE recomendado chamar o método StartActivity sempre que a atividade do usuário for alterada para NUNCA chamar o método EndActivity, visto que chamar esse método força o encerramento da sessão atual.</span><span class="sxs-lookup"><span data-stu-id="b27ae-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="b27ae-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="b27ae-125">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="b27ae-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-126">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="b27ae-127">É necessário chamar `EndActivity()` pelo menos uma vez quando o usuário conclui sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="b27ae-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="b27ae-128">Isso informa o SDK do Engagement que o usuário está ocioso no momento e que a sessão do usuário precisa ser fechada quando o tempo limite da sessão expirar (se você chamar `StartActivity()` antes de expirar o tempo limite da sessão, a sessão será simplesmente retomada).</span><span class="sxs-lookup"><span data-stu-id="b27ae-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="b27ae-130">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="b27ae-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="b27ae-131">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-132">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-133">Você pode usar o trabalho para acompanhar determinadas tarefa por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="b27ae-135">Encerrar um trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-136">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="b27ae-137">Assim que uma tarefa controlada por um trabalho foi finalizada, você deve chamar o método EndJob para esse trabalho, fornecendo o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="b27ae-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="b27ae-139">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="b27ae-139">Reporting Events</span></span>
<span data-ttu-id="b27ae-140">Há três tipos de eventos :</span><span class="sxs-lookup"><span data-stu-id="b27ae-140">There is three types of events :</span></span>

* <span data-ttu-id="b27ae-141">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="b27ae-141">Standalone events</span></span>
* <span data-ttu-id="b27ae-142">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="b27ae-142">Session events</span></span>
* <span data-ttu-id="b27ae-143">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="b27ae-144">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="b27ae-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-145">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-146">Eventos autônomos podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-147">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="b27ae-148">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="b27ae-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-149">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-150">Eventos de sessão são geralmente usados para relatar as ações executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-151">Example</span></span>
<span data-ttu-id="b27ae-152">**Sem dados :**</span><span class="sxs-lookup"><span data-stu-id="b27ae-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="b27ae-153">**Com dados :**</span><span class="sxs-lookup"><span data-stu-id="b27ae-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="b27ae-154">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-155">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-156">Eventos de trabalho são geralmente usados para relatar as ações executadas por um usuário durante um trabalho.</span><span class="sxs-lookup"><span data-stu-id="b27ae-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-157">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="b27ae-158">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="b27ae-158">Reporting Errors</span></span>
<span data-ttu-id="b27ae-159">Há três tipos de erros:</span><span class="sxs-lookup"><span data-stu-id="b27ae-159">There is three types of errors :</span></span>

* <span data-ttu-id="b27ae-160">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="b27ae-160">Standalone errors</span></span>
* <span data-ttu-id="b27ae-161">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="b27ae-161">Session errors</span></span>
* <span data-ttu-id="b27ae-162">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="b27ae-163">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="b27ae-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-164">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-165">Ao contrário dos erros de sessão, os erros autônomos podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="b27ae-167">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="b27ae-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-168">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-169">Erros de sessão são geralmente usados para relatar os erros que afetam o usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="b27ae-171">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="b27ae-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-172">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="b27ae-173">Os erros podem estar relacionados a um trabalho em execução, em vez de serem relacionados a sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b27ae-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="b27ae-175">Relatórios de falhas</span><span class="sxs-lookup"><span data-stu-id="b27ae-175">Reporting Crashes</span></span>
<span data-ttu-id="b27ae-176">O agente fornece dois métodos para lidar com falhas.</span><span class="sxs-lookup"><span data-stu-id="b27ae-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="b27ae-177">Enviar uma exceção</span><span class="sxs-lookup"><span data-stu-id="b27ae-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-178">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="b27ae-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-179">Example</span></span>
<span data-ttu-id="b27ae-180">Você pode enviar uma exceção a qualquer momento chamando :</span><span class="sxs-lookup"><span data-stu-id="b27ae-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="b27ae-181">Você também pode usar um parâmetro opcional para encerrar a sessão do engagement ao mesmo tempo que envia a falha.</span><span class="sxs-lookup"><span data-stu-id="b27ae-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="b27ae-182">Para fazer isso, chame :</span><span class="sxs-lookup"><span data-stu-id="b27ae-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="b27ae-183">Se você fizer isso, os trabalhos e a sessão serão fechados apenas após o envio da falha.</span><span class="sxs-lookup"><span data-stu-id="b27ae-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="b27ae-184">Enviar uma exceção sem tratamento</span><span class="sxs-lookup"><span data-stu-id="b27ae-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="b27ae-185">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="b27ae-186">O Engagement também fornece um método para enviar as exceções sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="b27ae-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="b27ae-187">Isso é especialmente útil quando usado dentro do manipulador de eventos do aplicativo UnhandledException do silverlight.</span><span class="sxs-lookup"><span data-stu-id="b27ae-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="b27ae-188">Esse método **SEMPRE** encerrará a sessão de engagement depois de ser chamado.</span><span class="sxs-lookup"><span data-stu-id="b27ae-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="b27ae-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-189">Example</span></span>
<span data-ttu-id="b27ae-190">Você pode usá-lo para implementar seu próprio manipulador UnhandledException (especialmente se você tiver desativado a recurso de relatório de falhas automático do Engagement).</span><span class="sxs-lookup"><span data-stu-id="b27ae-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="b27ae-191">Por exemplo, no método `Application_UnhandledException` do arquivo `App.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="b27ae-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="b27ae-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="b27ae-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="b27ae-193">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="b27ae-194">Quando o usuário navega para frente, para longe de um aplicativo, após o evento Deactivated ser gerado, o sistema operacional tenta colocar o aplicativo em um estado inativo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="b27ae-195">Depois, o aplicativo é a marcado para exclusão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="b27ae-196">Nesse processo, um aplicativo é encerrado, mas alguns dados sobre o estado do aplicativo e as páginas individuais dentro do aplicativo são preservados.</span><span class="sxs-lookup"><span data-stu-id="b27ae-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="b27ae-197">Você precisa inserir `EngagementAgent.Instance.OnActivated(e)` no método `Application_Activated` do arquivo App.xaml.cs para redefinir o Agente do Engagement quando o aplicativo foi marcado para a exclusão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="b27ae-198">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="b27ae-199">Id do dispositivo</span><span class="sxs-lookup"><span data-stu-id="b27ae-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="b27ae-200">Você pode obter a id do dispositivo do engagement chamando esse método.</span><span class="sxs-lookup"><span data-stu-id="b27ae-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="b27ae-201">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="b27ae-201">Extras parameters</span></span>
<span data-ttu-id="b27ae-202">Dados arbitrários podem ser anexados a um evento, um erro, uma atividade ou um trabalho.</span><span class="sxs-lookup"><span data-stu-id="b27ae-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="b27ae-203">Esses dados podem ser estruturados usando um dicionário.</span><span class="sxs-lookup"><span data-stu-id="b27ae-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="b27ae-204">Chaves e valores podem ser de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="b27ae-205">Dados adicionais são serializados para que se desejar inserir seu próprio tipo em adicionais, você precisará adicionar um contrato de dados para esse tipo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="b27ae-206">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-206">Example</span></span>
<span data-ttu-id="b27ae-207">Criamos uma nova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="b27ae-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="b27ae-208">Depois, adicionaremos uma instância `Person` para um arquivo extra.</span><span class="sxs-lookup"><span data-stu-id="b27ae-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="b27ae-209">Se você colocar outros tipos de objetos, verifique se o método ToString () é implementado para retornar uma cadeia de caracteres legível humana.</span><span class="sxs-lookup"><span data-stu-id="b27ae-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="b27ae-210">Limites</span><span class="sxs-lookup"><span data-stu-id="b27ae-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="b27ae-211">simétricas</span><span class="sxs-lookup"><span data-stu-id="b27ae-211">Keys</span></span>
<span data-ttu-id="b27ae-212">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="b27ae-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="b27ae-213">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="b27ae-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="b27ae-214">Tamanho</span><span class="sxs-lookup"><span data-stu-id="b27ae-214">Size</span></span>
<span data-ttu-id="b27ae-215">Os arquivos extras estão limitados a **1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="b27ae-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="b27ae-216">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="b27ae-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="b27ae-217">Referência</span><span class="sxs-lookup"><span data-stu-id="b27ae-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="b27ae-218">Você pode relatar manualmente informações (ou quaisquer outras informações específicas do aplicativo) de controle usando a função SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="b27ae-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="b27ae-219">Observe que essas informações podem ser enviadas de forma incremental: somente o último valor para uma determinada chave será mantido por um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b27ae-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="b27ae-220">Como extras de eventos, use um Dicionário\<object, object\> para anexar informações.</span><span class="sxs-lookup"><span data-stu-id="b27ae-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="b27ae-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b27ae-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="b27ae-222">Limites</span><span class="sxs-lookup"><span data-stu-id="b27ae-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="b27ae-223">simétricas</span><span class="sxs-lookup"><span data-stu-id="b27ae-223">Keys</span></span>
<span data-ttu-id="b27ae-224">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="b27ae-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="b27ae-225">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="b27ae-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="b27ae-226">Tamanho</span><span class="sxs-lookup"><span data-stu-id="b27ae-226">Size</span></span>
<span data-ttu-id="b27ae-227">As informações do aplicativo estão limitadas a **1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="b27ae-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="b27ae-228">No exemplo anterior, o JSON enviado para o servidor tem 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="b27ae-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="b27ae-229">Registro em log</span><span class="sxs-lookup"><span data-stu-id="b27ae-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="b27ae-230">Habilitar registro em log</span><span class="sxs-lookup"><span data-stu-id="b27ae-230">Enable Logging</span></span>
<span data-ttu-id="b27ae-231">O SDK pode ser configurado para gerar logs de teste no console do IDE.</span><span class="sxs-lookup"><span data-stu-id="b27ae-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="b27ae-232">Esses logs não são ativados por padrão.</span><span class="sxs-lookup"><span data-stu-id="b27ae-232">These logs are not activated by default.</span></span> <span data-ttu-id="b27ae-233">Para personalizar esse recurso, atualize a propriedade `EngagementAgent.Instance.TestLogEnabled` para um dos valores disponíveis na enumeração `EngagementTestLogLevel`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b27ae-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
