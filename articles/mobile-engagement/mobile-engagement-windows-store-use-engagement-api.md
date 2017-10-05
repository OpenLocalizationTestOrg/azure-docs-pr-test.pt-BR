---
title: Como usar o API do Engagement no Windows Universal
description: Como usar o API do Engagement no Windows Universal
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="f1834-103">Como usar o API do Engagement no Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f1834-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="f1834-104">Este documento é um complemento para o documento [Como integrar o Engagement no Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): ele fornece detalhes aprofundados sobre como usar a API do Engagement para relatar as estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1834-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="f1834-105">Tenha em mente que caso queira o Engagement apenas para relatar as sessões, atividades, falhas e informações técnicas do seu aplicativo, então a maneira mais simples é fazer todas as suas subclasses `Page` herdarem da classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="f1834-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="f1834-106">Se você quiser fazer mais, por exemplo, se você precisar reportar eventos, erros e trabalhos específicos do aplicativo ou se você tiver que relatar as atividades do seu aplicativo de maneira diferente de um implementado nas classes `EngagementPage`, você precisará usar a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1834-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="f1834-107">A API do Engagement é fornecida pela classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="f1834-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="f1834-108">Você pode obter acesso a esses métodos por meio de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="f1834-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="f1834-109">Mesmo se o módulo de agente não foi inicializado, cada chamada para a API é adiada e será executada novamente quando o agente está disponível.</span><span class="sxs-lookup"><span data-stu-id="f1834-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="f1834-110">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="f1834-110">Engagement concepts</span></span>
<span data-ttu-id="f1834-111">As seguintes partes refinam os [Conceitos de Mobile Engagement](mobile-engagement-concepts.md) usuais para a plataforma Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="f1834-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="f1834-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="f1834-112">`Session` and `Activity`</span></span>
<span data-ttu-id="f1834-113">Uma *atividade* geralmente está associada a uma página de aplicativo. Isso significa que a *atividade* iniciará quando a página for exibida e será interrompida quando a página for fechada: esse é o caso quando o SDK do Engagement é integrado usando a classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="f1834-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="f1834-114">Mas as *atividades* também podem ser controladas manualmente usando a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1834-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="f1834-115">Isso permite dividir uma determinada página em várias partes secundárias para obter mais detalhes sobre o uso desta página (por exemplo para saber com que frequência e por quanto tempo as caixas de diálogo são usadas dentro dessa página).</span><span class="sxs-lookup"><span data-stu-id="f1834-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="f1834-116">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="f1834-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="f1834-117">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="f1834-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-118">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-119">É necessário chamar `StartActivity()` sempre que houver alterações de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1834-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="f1834-120">A primeira chamada para essa função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="f1834-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1834-121">O SDK chama automaticamente o método EndActivity quando o aplicativo é fechado.</span><span class="sxs-lookup"><span data-stu-id="f1834-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="f1834-122">Portanto, é ALTAMENTE recomendado chamar o método StartActivity sempre que a atividade do usuário for alterada e NUNCA chamar o método EndActivity, visto que chamar esse método força o encerramento da sessão atual.</span><span class="sxs-lookup"><span data-stu-id="f1834-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="f1834-123">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="f1834-124">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="f1834-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-125">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="f1834-126">Isso encerra a atividade e a sessão.</span><span class="sxs-lookup"><span data-stu-id="f1834-126">This ends the activity and the session.</span></span> <span data-ttu-id="f1834-127">Você não deve chamar esse método, a menos que você realmente sabe o que está fazendo.</span><span class="sxs-lookup"><span data-stu-id="f1834-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-128">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="f1834-129">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="f1834-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="f1834-130">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-131">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-132">Você pode usar o trabalho para acompanhar determinadas tarefa por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f1834-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-133">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="f1834-134">Encerrar um trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-135">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="f1834-136">Assim que uma tarefa controlada por um trabalho foi finalizada, você deve chamar o método EndJob para esse trabalho, fornecendo o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="f1834-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="f1834-138">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="f1834-138">Reporting Events</span></span>
<span data-ttu-id="f1834-139">Há três tipos de eventos :</span><span class="sxs-lookup"><span data-stu-id="f1834-139">There is three types of events :</span></span>

* <span data-ttu-id="f1834-140">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="f1834-140">Standalone events</span></span>
* <span data-ttu-id="f1834-141">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="f1834-141">Session events</span></span>
* <span data-ttu-id="f1834-142">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="f1834-143">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="f1834-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-144">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-145">Eventos autônomos podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="f1834-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="f1834-147">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="f1834-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-148">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-149">Eventos de sessão são geralmente usados para relatar as ações executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="f1834-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-150">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-150">Example</span></span>
<span data-ttu-id="f1834-151">**Sem dados :**</span><span class="sxs-lookup"><span data-stu-id="f1834-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="f1834-152">**Com dados :**</span><span class="sxs-lookup"><span data-stu-id="f1834-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="f1834-153">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-154">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-155">Eventos de trabalho são geralmente usados para relatar as ações executadas por um usuário durante um trabalho.</span><span class="sxs-lookup"><span data-stu-id="f1834-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-156">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="f1834-157">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="f1834-157">Reporting Errors</span></span>
<span data-ttu-id="f1834-158">Há três tipos de erros:</span><span class="sxs-lookup"><span data-stu-id="f1834-158">There are three types of errors :</span></span>

* <span data-ttu-id="f1834-159">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="f1834-159">Standalone errors</span></span>
* <span data-ttu-id="f1834-160">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="f1834-160">Session errors</span></span>
* <span data-ttu-id="f1834-161">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="f1834-162">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="f1834-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-163">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-164">Ao contrário dos erros de sessão, os erros autônomos podem ocorrer fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="f1834-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-165">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="f1834-166">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="f1834-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-167">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-168">Erros de sessão são geralmente usados para relatar os erros que afetam o usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="f1834-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-169">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="f1834-170">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1834-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-171">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="f1834-172">Os erros podem estar relacionados a um trabalho em execução, em vez de serem relacionados a sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="f1834-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="f1834-174">Relatórios de falhas</span><span class="sxs-lookup"><span data-stu-id="f1834-174">Reporting Crashes</span></span>
<span data-ttu-id="f1834-175">O agente fornece dois métodos para lidar com falhas.</span><span class="sxs-lookup"><span data-stu-id="f1834-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="f1834-176">Enviar uma exceção</span><span class="sxs-lookup"><span data-stu-id="f1834-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-177">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="f1834-178">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-178">Example</span></span>
<span data-ttu-id="f1834-179">Você pode enviar uma exceção a qualquer momento chamando :</span><span class="sxs-lookup"><span data-stu-id="f1834-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="f1834-180">Você também pode usar um parâmetro opcional para encerrar a sessão do engagement ao mesmo tempo que envia a falha.</span><span class="sxs-lookup"><span data-stu-id="f1834-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="f1834-181">Para fazer isso, chame :</span><span class="sxs-lookup"><span data-stu-id="f1834-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="f1834-182">Se você fizer isso, os trabalhos e a sessão serão fechados apenas após o envio da falha.</span><span class="sxs-lookup"><span data-stu-id="f1834-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="f1834-183">Enviar uma exceção sem tratamento</span><span class="sxs-lookup"><span data-stu-id="f1834-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="f1834-184">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="f1834-185">O Engagement também fornece um método para enviar as exceções sem tratamento se você tiver **DESABILITADO** o relatório de **falha** automático do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1834-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="f1834-186">Isso é especialmente útil quando usado dentro do manipulador de eventos do aplicativo UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="f1834-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="f1834-187">Esse método **SEMPRE** encerrará a sessão e os trabalhos do engagement depois de ser chamado.</span><span class="sxs-lookup"><span data-stu-id="f1834-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="f1834-188">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-188">Example</span></span>
<span data-ttu-id="f1834-189">Você pode usá-lo para implementar seu próprio manipulador UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="f1834-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="f1834-190">Por exemplo, adicione o método `Current_UnhandledException` do arquivo `App.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="f1834-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="f1834-191">Em App.xaml.cs em "Public App(){}" adicione:</span><span class="sxs-lookup"><span data-stu-id="f1834-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="f1834-192">Id do dispositivo</span><span class="sxs-lookup"><span data-stu-id="f1834-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="f1834-193">Você pode obter a id do dispositivo do engagement chamando esse método.</span><span class="sxs-lookup"><span data-stu-id="f1834-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="f1834-194">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="f1834-194">Extras parameters</span></span>
<span data-ttu-id="f1834-195">Dados arbitrários podem ser anexados a um evento, um erro, uma atividade ou um trabalho.</span><span class="sxs-lookup"><span data-stu-id="f1834-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="f1834-196">Esses dados podem ser estruturados usando um dicionário.</span><span class="sxs-lookup"><span data-stu-id="f1834-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="f1834-197">Chaves e valores podem ser de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="f1834-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="f1834-198">Dados adicionais são serializados para que se desejar inserir seu próprio tipo em adicionais, você precisará adicionar um contrato de dados para esse tipo.</span><span class="sxs-lookup"><span data-stu-id="f1834-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="f1834-199">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-199">Example</span></span>
<span data-ttu-id="f1834-200">Criamos uma nova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="f1834-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="f1834-201">Depois, adicionaremos uma instância `Person` para um arquivo extra.</span><span class="sxs-lookup"><span data-stu-id="f1834-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="f1834-202">Se você colocar outros tipos de objetos, verifique se o método ToString () é implementado para retornar uma cadeia de caracteres legível humana.</span><span class="sxs-lookup"><span data-stu-id="f1834-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="f1834-203">Limites</span><span class="sxs-lookup"><span data-stu-id="f1834-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="f1834-204">simétricas</span><span class="sxs-lookup"><span data-stu-id="f1834-204">Keys</span></span>
<span data-ttu-id="f1834-205">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="f1834-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="f1834-206">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="f1834-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="f1834-207">Tamanho</span><span class="sxs-lookup"><span data-stu-id="f1834-207">Size</span></span>
<span data-ttu-id="f1834-208">Os arquivos extras estão limitados a **1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="f1834-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="f1834-209">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f1834-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="f1834-210">Referência</span><span class="sxs-lookup"><span data-stu-id="f1834-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="f1834-211">Você pode relatar manualmente informações (ou quaisquer outras informações específicas do aplicativo) de controle usando a função SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="f1834-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="f1834-212">Observe que essas informações podem ser enviadas de forma incremental: somente o valor mais recente de uma determinada chave será mantido para um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="f1834-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="f1834-213">Como extras de eventos, use um Dicionário\<object, object\> para anexar dados.</span><span class="sxs-lookup"><span data-stu-id="f1834-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="f1834-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f1834-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="f1834-215">Limites</span><span class="sxs-lookup"><span data-stu-id="f1834-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="f1834-216">simétricas</span><span class="sxs-lookup"><span data-stu-id="f1834-216">Keys</span></span>
<span data-ttu-id="f1834-217">Cada chave no objeto deve corresponder à seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="f1834-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="f1834-218">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="f1834-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="f1834-219">Tamanho</span><span class="sxs-lookup"><span data-stu-id="f1834-219">Size</span></span>
<span data-ttu-id="f1834-220">As informações do aplicativo estão limitadas a **1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="f1834-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="f1834-221">No exemplo anterior, o JSON enviado para o servidor tem 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="f1834-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="f1834-222">Registro em log</span><span class="sxs-lookup"><span data-stu-id="f1834-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="f1834-223">Habilitar registro em log</span><span class="sxs-lookup"><span data-stu-id="f1834-223">Enable Logging</span></span>
<span data-ttu-id="f1834-224">O SDK pode ser configurado para gerar logs de teste no console do IDE.</span><span class="sxs-lookup"><span data-stu-id="f1834-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="f1834-225">Esses logs não são ativados por padrão.</span><span class="sxs-lookup"><span data-stu-id="f1834-225">These logs are not activated by default.</span></span> <span data-ttu-id="f1834-226">Para personalizar esse recurso, atualize a propriedade `EngagementAgent.Instance.TestLogEnabled` para um dos valores disponíveis na enumeração `EngagementTestLogLevel`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f1834-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

