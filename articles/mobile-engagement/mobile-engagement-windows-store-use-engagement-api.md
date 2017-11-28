---
title: "saudação de tooUse aaaHow contrato de API no Windows Universal"
description: "Como tooUse Olá contrato de API no Windows Universal"
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
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="a041a-103">Como tooUse Olá contrato de API no Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a041a-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="a041a-104">Este é um documento de toohello complemento [como tooIntegrate contrato no Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a041a-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="a041a-105">Tenha em mente que se você desejar contrato tooreport somente sessões, atividades, falhas e obter informações técnicas do seu aplicativo, em seguida, hello forma mais simples é toomake todos os seus `Page` subclasses herdam Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="a041a-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="a041a-106">Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementPage` classes, e em seguida, você precisa toouse Olá Contrato de API.</span><span class="sxs-lookup"><span data-stu-id="a041a-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="a041a-107">Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="a041a-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="a041a-108">Você pode acessar os métodos de toothose por meio de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="a041a-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="a041a-109">Mesmo que o módulo de saudação do agente não foi inicializado, cada API toohello de chamada é adiada e será executado novamente quando o agente hello está disponível.</span><span class="sxs-lookup"><span data-stu-id="a041a-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="a041a-110">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="a041a-110">Engagement concepts</span></span>
<span data-ttu-id="a041a-111">seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md) para plataforma Universal do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a041a-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a041a-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="a041a-112">`Session` and `Activity`</span></span>
<span data-ttu-id="a041a-113">Um *atividade* geralmente está associado com uma página de aplicativo hello, que é toosay hello *atividade* inicia quando a página Olá é exibida e é interrompido quando Olá página é fechada: esse é o caso de Olá quando hello SDK do contrato é integrado usando Olá `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="a041a-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="a041a-114">Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API.</span><span class="sxs-lookup"><span data-stu-id="a041a-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="a041a-115">Isso permite que você toosplit uma determinada página em várias sub partes tooget mais detalhes sobre o uso de saudação desta página (por exemplo tooknow frequência e quanto tempo as caixas de diálogo são usadas dentro desta página).</span><span class="sxs-lookup"><span data-stu-id="a041a-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a041a-116">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="a041a-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a041a-117">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="a041a-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-118">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-119">Você precisa toocall `StartActivity()` alterações de cada atividade de usuário de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="a041a-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="a041a-120">Olá primeira chamada toothis função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="a041a-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a041a-121">Olá SDK automaticamente chama o método de EndActivity de saudação quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="a041a-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="a041a-122">Portanto, é altamente recomendável método de StartActivity toocall hello sempre hello atividade de usuário Olá alterações e término da chamada tooNEVER Olá método EndActivity, desde chamar esse método força Olá toobe de sessão atual.</span><span class="sxs-lookup"><span data-stu-id="a041a-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="a041a-123">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="a041a-124">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="a041a-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-125">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="a041a-126">Isso encerra a atividade de saudação e a sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a041a-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="a041a-127">Você não deve chamar esse método, a menos que você realmente sabe o que está fazendo.</span><span class="sxs-lookup"><span data-stu-id="a041a-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-128">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="a041a-129">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="a041a-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="a041a-130">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-131">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-132">Você pode usar o hello tootrack alguns tarefas em um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="a041a-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-133">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="a041a-134">Encerrar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-135">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="a041a-136">Assim que uma tarefa controlada por um trabalho foi encerrada, você deve chamar o método de EndJob de saudação para esse trabalho, fornecendo o nome do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="a041a-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="a041a-138">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="a041a-138">Reporting Events</span></span>
<span data-ttu-id="a041a-139">Há três tipos de eventos :</span><span class="sxs-lookup"><span data-stu-id="a041a-139">There is three types of events :</span></span>

* <span data-ttu-id="a041a-140">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="a041a-140">Standalone events</span></span>
* <span data-ttu-id="a041a-141">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="a041a-141">Session events</span></span>
* <span data-ttu-id="a041a-142">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="a041a-143">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="a041a-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-144">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-145">Autônomo eventos podem ocorrer fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="a041a-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="a041a-147">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="a041a-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-148">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-149">Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="a041a-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-150">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-150">Example</span></span>
<span data-ttu-id="a041a-151">**Sem dados :**</span><span class="sxs-lookup"><span data-stu-id="a041a-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="a041a-152">**Com dados :**</span><span class="sxs-lookup"><span data-stu-id="a041a-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="a041a-153">Eventos de trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-154">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-155">Eventos de trabalho são ações que Olá tooreport usados normalmente executadas por um usuário durante um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a041a-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-156">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="a041a-157">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="a041a-157">Reporting Errors</span></span>
<span data-ttu-id="a041a-158">Há três tipos de erros:</span><span class="sxs-lookup"><span data-stu-id="a041a-158">There are three types of errors :</span></span>

* <span data-ttu-id="a041a-159">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="a041a-159">Standalone errors</span></span>
* <span data-ttu-id="a041a-160">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="a041a-160">Session errors</span></span>
* <span data-ttu-id="a041a-161">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="a041a-162">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="a041a-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-163">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-164">Erros de toosession contrary, podem ocorrer erros autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="a041a-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-165">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="a041a-166">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="a041a-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-167">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-168">Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="a041a-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-169">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="a041a-170">Erros de trabalho</span><span class="sxs-lookup"><span data-stu-id="a041a-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-171">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a041a-172">Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="a041a-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="a041a-174">Relatórios de falhas</span><span class="sxs-lookup"><span data-stu-id="a041a-174">Reporting Crashes</span></span>
<span data-ttu-id="a041a-175">Agente de saudação fornece dois toodeal de métodos com falhas.</span><span class="sxs-lookup"><span data-stu-id="a041a-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="a041a-176">Enviar uma exceção</span><span class="sxs-lookup"><span data-stu-id="a041a-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-177">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="a041a-178">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-178">Example</span></span>
<span data-ttu-id="a041a-179">Você pode enviar uma exceção a qualquer momento chamando :</span><span class="sxs-lookup"><span data-stu-id="a041a-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="a041a-180">Você também pode usar uma sessão de contrato de saudação do parâmetro opcional tooterminate em Olá mesmo tempo que o envio de falhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="a041a-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="a041a-181">Portanto, chame toodo:</span><span class="sxs-lookup"><span data-stu-id="a041a-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="a041a-182">Se você fizer isso, trabalhos e sessão Olá serão fechados imediatamente após enviar falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="a041a-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="a041a-183">Enviar uma exceção sem tratamento</span><span class="sxs-lookup"><span data-stu-id="a041a-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a041a-184">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="a041a-185">Contrato também fornece um exceções toosend sem tratamento de método se você tiver **desabilitado** contrato automático **falha** reporting.</span><span class="sxs-lookup"><span data-stu-id="a041a-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="a041a-186">Isso é especialmente útil quando usado dentro do manipulador de eventos do hello aplicativo UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="a041a-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="a041a-187">Esse método será **sempre** encerrar a sessão de contrato hello e trabalhos após a chamada.</span><span class="sxs-lookup"><span data-stu-id="a041a-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="a041a-188">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-188">Example</span></span>
<span data-ttu-id="a041a-189">Você pode usá-lo tooimplement seu próprio manipulador de UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="a041a-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="a041a-190">Por exemplo, adicionar Olá `Current_UnhandledException` método hello `App.xaml.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="a041a-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="a041a-191">Em App.xaml.cs em "Public App(){}" adicione:</span><span class="sxs-lookup"><span data-stu-id="a041a-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="a041a-192">Id do dispositivo</span><span class="sxs-lookup"><span data-stu-id="a041a-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="a041a-193">Você pode obter o id do dispositivo Olá engagement por chamar esse método.</span><span class="sxs-lookup"><span data-stu-id="a041a-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="a041a-194">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="a041a-194">Extras parameters</span></span>
<span data-ttu-id="a041a-195">Dados arbitrários podem ser anexados tooan evento, um erro, uma atividade ou um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a041a-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="a041a-196">Esses dados podem ser estruturados usando um dicionário.</span><span class="sxs-lookup"><span data-stu-id="a041a-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="a041a-197">Chaves e valores podem ser de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="a041a-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="a041a-198">Dados extras são serializados para que tooinsert seu próprio tipo de extras você ter se tooadd um contrato de dados para este tipo.</span><span class="sxs-lookup"><span data-stu-id="a041a-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="a041a-199">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-199">Example</span></span>
<span data-ttu-id="a041a-200">Criamos uma nova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="a041a-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="a041a-201">Em seguida, adicionaremos um `Person` tooan de instância extra.</span><span class="sxs-lookup"><span data-stu-id="a041a-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="a041a-202">Se você colocar outros tipos de objetos, verifique se que o método ToString () é implementado tooreturn uma cadeia de caracteres legível humana.</span><span class="sxs-lookup"><span data-stu-id="a041a-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="a041a-203">limites</span><span class="sxs-lookup"><span data-stu-id="a041a-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a041a-204">simétricas</span><span class="sxs-lookup"><span data-stu-id="a041a-204">Keys</span></span>
<span data-ttu-id="a041a-205">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="a041a-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a041a-206">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="a041a-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a041a-207">Tamanho</span><span class="sxs-lookup"><span data-stu-id="a041a-207">Size</span></span>
<span data-ttu-id="a041a-208">Extras são muito limitadas**1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="a041a-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="a041a-209">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a041a-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="a041a-210">Referência</span><span class="sxs-lookup"><span data-stu-id="a041a-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="a041a-211">Manualmente, você pode relatar informações (ou quaisquer outras informações específicas do aplicativo) usando a função de SendAppInfo() hello de controle.</span><span class="sxs-lookup"><span data-stu-id="a041a-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="a041a-212">Observe que esses dados podem ser enviados de forma incremental: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a041a-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="a041a-213">Como o evento extras, usar um dicionário\<objeto, objeto\> tooattach dados.</span><span class="sxs-lookup"><span data-stu-id="a041a-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="a041a-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a041a-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="a041a-215">Limites</span><span class="sxs-lookup"><span data-stu-id="a041a-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a041a-216">simétricas</span><span class="sxs-lookup"><span data-stu-id="a041a-216">Keys</span></span>
<span data-ttu-id="a041a-217">Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="a041a-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a041a-218">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="a041a-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a041a-219">Tamanho</span><span class="sxs-lookup"><span data-stu-id="a041a-219">Size</span></span>
<span data-ttu-id="a041a-220">Informações do aplicativo são muito limitadas**1024** caracteres por chamada.</span><span class="sxs-lookup"><span data-stu-id="a041a-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="a041a-221">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="a041a-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="a041a-222">Registro em log</span><span class="sxs-lookup"><span data-stu-id="a041a-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="a041a-223">Habilitar registro em log</span><span class="sxs-lookup"><span data-stu-id="a041a-223">Enable Logging</span></span>
<span data-ttu-id="a041a-224">Olá SDK pode ser configurado tooproduce logs de teste no console do IDE hello.</span><span class="sxs-lookup"><span data-stu-id="a041a-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="a041a-225">Esses logs não são ativados por padrão.</span><span class="sxs-lookup"><span data-stu-id="a041a-225">These logs are not activated by default.</span></span> <span data-ttu-id="a041a-226">toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a041a-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

