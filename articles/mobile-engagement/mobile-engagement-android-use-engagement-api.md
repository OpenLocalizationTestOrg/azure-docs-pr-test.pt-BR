---
title: "saudação de tooUse aaaHow contrato de API no Android"
description: "SDK do Android mais recente - como tooUse Olá contrato de API no Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="52fdb-103">Como tooUse Olá contrato de API no Android</span><span class="sxs-lookup"><span data-stu-id="52fdb-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="52fdb-104">Este é um documento de toohello complemento [opções avançadas de relatório para o Android SDK do Mobile Engagement](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="52fdb-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="52fdb-105">Ele fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52fdb-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="52fdb-106">Tenha em mente que se você desejar contrato tooreport somente sessões, atividades, falhas e obter informações técnicas do seu aplicativo, em seguida, hello forma mais simples é toomake todos os seus `Activity` subclasses herdam Olá correspondente `EngagementActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="52fdb-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="52fdb-107">Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementActivity` classes, e em seguida, você precisa toouse Olá Contrato de API.</span><span class="sxs-lookup"><span data-stu-id="52fdb-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="52fdb-108">Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="52fdb-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="52fdb-109">Uma instância desta classe pode ser recuperada pela chamada hello `EngagementAgent.getInstance(Context)` método estático (Observe que Olá `EngagementAgent` objeto retornado é um singleton).</span><span class="sxs-lookup"><span data-stu-id="52fdb-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="52fdb-110">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="52fdb-110">Engagement concepts</span></span>
<span data-ttu-id="52fdb-111">seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md), para a plataforma Android hello.</span><span class="sxs-lookup"><span data-stu-id="52fdb-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="52fdb-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="52fdb-112">`Session` and `Activity`</span></span>
<span data-ttu-id="52fdb-113">Se usuário Olá permanecer mais de alguns segundos de ociosidade entre dois *atividades*, em seguida, sua sequência de *atividades* é dividido em dois distintos *sessões*.</span><span class="sxs-lookup"><span data-stu-id="52fdb-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="52fdb-114">Esses alguns segundos são chamados hello "tempo limite da sessão".</span><span class="sxs-lookup"><span data-stu-id="52fdb-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="52fdb-115">Um *atividade* geralmente está associado com uma tela do aplicativo hello, que é hello toosay *atividade* inicia quando a tela hello é exibida e é interrompido quando a tela hello está fechada: isso é hello quando Olá SDK de contrato é integrado usando Olá `EngagementActivity` classes.</span><span class="sxs-lookup"><span data-stu-id="52fdb-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="52fdb-116">Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API.</span><span class="sxs-lookup"><span data-stu-id="52fdb-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="52fdb-117">Isso permite uma determinada tela toosplit em vários tooget de partes sub mais detalhes sobre Olá uso desta tela (por exemplo tooknown frequência e quanto tempo as caixas de diálogo são usadas dentro desta tela).</span><span class="sxs-lookup"><span data-stu-id="52fdb-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="52fdb-118">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="52fdb-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52fdb-119">Não é necessário tooreport atividades, como descrito nesta seção se você estiver usando Olá `EngagementActivity` classe e suas variantes conforme explicado em hello como tooIntegrate contrato no documento Android.</span><span class="sxs-lookup"><span data-stu-id="52fdb-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="52fdb-120">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="52fdb-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="52fdb-121">Você precisa toocall `startActivity()` alterações de cada atividade de usuário de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="52fdb-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="52fdb-122">Olá primeira chamada toothis função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="52fdb-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="52fdb-123">Olá melhor toocall local é essa função em cada atividade `onResume` retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="52fdb-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="52fdb-124">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="52fdb-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="52fdb-125">Você precisa toocall `endActivity()` pelo menos uma vez quando o usuário Olá termina sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="52fdb-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="52fdb-126">Isso informa Olá expirará SDK de contrato que usuário hello está ocioso no momento e que a sessão de usuário Olá necessário toobe uma vez fechado Olá tempo limite da sessão (se você chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado).</span><span class="sxs-lookup"><span data-stu-id="52fdb-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="52fdb-127">Olá melhor toocall local é essa função em cada atividade `onPause` retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="52fdb-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="52fdb-128">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="52fdb-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="52fdb-129">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="52fdb-129">Session events</span></span>
<span data-ttu-id="52fdb-130">Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="52fdb-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="52fdb-131">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="52fdb-132">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="52fdb-133">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="52fdb-133">Standalone Events</span></span>
<span data-ttu-id="52fdb-134">Eventos de toosession contrary, podem ocorrer eventos autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="52fdb-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="52fdb-135">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-135">**Example:**</span></span>

<span data-ttu-id="52fdb-136">Suponha que você deseja tooreport os eventos que ocorrem quando um receptor de difusão é acionado:</span><span class="sxs-lookup"><span data-stu-id="52fdb-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="52fdb-137">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="52fdb-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="52fdb-138">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="52fdb-138">Session errors</span></span>
<span data-ttu-id="52fdb-139">Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="52fdb-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="52fdb-140">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="52fdb-141">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="52fdb-141">Standalone errors</span></span>
<span data-ttu-id="52fdb-142">Erros de toosession contrary, podem ocorrer erros autônomo fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="52fdb-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="52fdb-143">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-143">**Example:**</span></span>

<span data-ttu-id="52fdb-144">Olá exemplo a seguir mostra como tooreport um erro sempre que a memória de saudação se torna baixa no telefone Olá durante o processo de aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="52fdb-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="52fdb-145">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="52fdb-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="52fdb-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="52fdb-146">Example</span></span>
<span data-ttu-id="52fdb-147">Suponha que você deseja tooreport Olá duração do processo de logon:</span><span class="sxs-lookup"><span data-stu-id="52fdb-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="52fdb-148">Relatar erros durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="52fdb-148">Report Errors during a Job</span></span>
<span data-ttu-id="52fdb-149">Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="52fdb-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="52fdb-150">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-150">**Example:**</span></span>

<span data-ttu-id="52fdb-151">Suponha que você queira tooreport um erro durante a você fazer logon em processo:</span><span class="sxs-lookup"><span data-stu-id="52fdb-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="52fdb-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="52fdb-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="52fdb-153">Relatar eventos durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="52fdb-153">Reporting Events during a job</span></span>
<span data-ttu-id="52fdb-154">Os eventos podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="52fdb-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="52fdb-155">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="52fdb-155">**Example:**</span></span>

<span data-ttu-id="52fdb-156">Suponha que temos uma rede social e usamos um trabalho tooreport Olá total tempo durante o qual Olá usuário conectado toohello server.</span><span class="sxs-lookup"><span data-stu-id="52fdb-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="52fdb-157">usuário Olá pode permanecer conectado em segundo plano, mesmo se ele estiver usando outro aplicativo ou ao telefone hello está em suspensão, portanto não há nenhuma sessão.</span><span class="sxs-lookup"><span data-stu-id="52fdb-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="52fdb-158">usuário Olá pode receber mensagens de seus amigos, este é um evento de trabalho.</span><span class="sxs-lookup"><span data-stu-id="52fdb-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="52fdb-159">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="52fdb-159">Extra parameters</span></span>
<span data-ttu-id="52fdb-160">Dados arbitrários podem ser anexados tooevents, erros, atividades e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="52fdb-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="52fdb-161">Esses dados podem ser estruturados, eles usam a classe de pacote do Android (na verdade, eles funcionam como parâmetros extras no Android Intents).</span><span class="sxs-lookup"><span data-stu-id="52fdb-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="52fdb-162">Observe que um pacote pode conter matrizes ou outras instâncias de pacote.</span><span class="sxs-lookup"><span data-stu-id="52fdb-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52fdb-163">Se você colocar em parâmetros parcelable ou serializáveis, verifique se seus `toString()` método é implementado tooreturn uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="52fdb-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="52fdb-164">As classes serializáveis que contêm campos não transitórios que não são serializáveis farão com que o Android falhe quando você chamar `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="52fdb-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="52fdb-165">Não há suporte para matrizes esparsas em parâmetros extras, ou seja, ela não será serializada como uma matriz.</span><span class="sxs-lookup"><span data-stu-id="52fdb-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="52fdb-166">Você deve convertê-las em matrizes padrão antes de usá-las em parâmetros extras.</span><span class="sxs-lookup"><span data-stu-id="52fdb-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="52fdb-167">Exemplo</span><span class="sxs-lookup"><span data-stu-id="52fdb-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="52fdb-168">Limites</span><span class="sxs-lookup"><span data-stu-id="52fdb-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="52fdb-169">simétricas</span><span class="sxs-lookup"><span data-stu-id="52fdb-169">Keys</span></span>
<span data-ttu-id="52fdb-170">Cada chave no hello `Bundle` devem corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fdb-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="52fdb-171">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="52fdb-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="52fdb-172">Tamanho</span><span class="sxs-lookup"><span data-stu-id="52fdb-172">Size</span></span>
<span data-ttu-id="52fdb-173">Extras são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo serviço de contrato de saudação).</span><span class="sxs-lookup"><span data-stu-id="52fdb-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="52fdb-174">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="52fdb-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="52fdb-175">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="52fdb-175">Reporting Application Information</span></span>
<span data-ttu-id="52fdb-176">Você pode relatar manualmente controle informações (ou quaisquer outras informações específicas do aplicativo) usando Olá `sendAppInfo()` função.</span><span class="sxs-lookup"><span data-stu-id="52fdb-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="52fdb-177">Observe que essas informações podem ser enviadas incrementalmente: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="52fdb-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="52fdb-178">Como evento extras, Olá classe do pacote é usado tooabstract informações do aplicativo, observe que matrizes ou sub pacotes será tratado como cadeias de caracteres simples (usando a serialização JSON).</span><span class="sxs-lookup"><span data-stu-id="52fdb-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="52fdb-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="52fdb-179">Example</span></span>
<span data-ttu-id="52fdb-180">Aqui está um gênero do usuário de toosend de exemplo de código e a data de nascimento:</span><span class="sxs-lookup"><span data-stu-id="52fdb-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="52fdb-181">limites</span><span class="sxs-lookup"><span data-stu-id="52fdb-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="52fdb-182">simétricas</span><span class="sxs-lookup"><span data-stu-id="52fdb-182">Keys</span></span>
<span data-ttu-id="52fdb-183">Cada chave no hello `Bundle` devem corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fdb-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="52fdb-184">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="52fdb-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="52fdb-185">Tamanho</span><span class="sxs-lookup"><span data-stu-id="52fdb-185">Size</span></span>
<span data-ttu-id="52fdb-186">Informações do aplicativo são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo serviço de contrato de saudação).</span><span class="sxs-lookup"><span data-stu-id="52fdb-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="52fdb-187">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="52fdb-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
