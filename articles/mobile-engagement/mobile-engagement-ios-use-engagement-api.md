---
title: "aaaHow tooUse Olá contrato de API no iOS"
description: "IOS mais recente SDK - como tooUse Olá contrato de API no iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="11650-103">Como tooUse Olá contrato de API no iOS</span><span class="sxs-lookup"><span data-stu-id="11650-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="11650-104">Este documento é um complemento toohello como tooIntegrate contrato no iOS: fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="11650-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="11650-105">Tenha em mente que se você quiser apenas contrato tooreport sessões, atividades, falhas e obter informações técnicas, seu aplicativo hello mais simples é forma toomake todos os personalizados `UIViewController` objetos herdam Olá correspondente `EngagementViewController` classe .</span><span class="sxs-lookup"><span data-stu-id="11650-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="11650-106">Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementViewController` classes, e em seguida, você precisa toouse Olá Contrato de API.</span><span class="sxs-lookup"><span data-stu-id="11650-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="11650-107">Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="11650-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="11650-108">Uma instância desta classe pode ser recuperada pela chamada hello `[EngagementAgent shared]` método estático (Observe que Olá `EngagementAgent` objeto retornado é um singleton).</span><span class="sxs-lookup"><span data-stu-id="11650-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="11650-109">Antes de qualquer chamadas de API, hello `EngagementAgent` objeto deve ser inicializado chamando o método hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="11650-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="11650-110">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="11650-110">Engagement concepts</span></span>
<span data-ttu-id="11650-111">seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md) para a plataforma do iOS hello.</span><span class="sxs-lookup"><span data-stu-id="11650-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="11650-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="11650-112">`Session` and `Activity`</span></span>
<span data-ttu-id="11650-113">Um *atividade* geralmente está associado com uma tela do aplicativo hello, que é hello toosay *atividade* inicia quando a tela hello é exibida e é interrompido quando a tela hello está fechada: isso é hello quando Olá SDK de contrato é integrado usando Olá `EngagementViewController` classes.</span><span class="sxs-lookup"><span data-stu-id="11650-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="11650-114">Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API.</span><span class="sxs-lookup"><span data-stu-id="11650-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="11650-115">Isso permite uma determinada tela toosplit em vários tooget de partes sub mais detalhes sobre Olá uso desta tela (por exemplo tooknown frequência e quanto tempo as caixas de diálogo são usadas dentro desta tela).</span><span class="sxs-lookup"><span data-stu-id="11650-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="11650-116">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="11650-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="11650-117">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="11650-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="11650-118">Você precisa toocall `startActivity()` alterações de cada atividade de usuário de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="11650-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="11650-119">Olá primeira chamada toothis função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="11650-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="11650-120">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="11650-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="11650-121">Você deve **nunca** chamar essa função por conta própria, exceto se você quiser toosplit um uso de seu aplicativo em várias sessões: uma chamada de função toothis terminaria Olá atual sessão imediatamente, portanto, uma chamada subsequente muito`startActivity()`deve iniciar uma nova sessão.</span><span class="sxs-lookup"><span data-stu-id="11650-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="11650-122">Esta função é chamada automaticamente por Olá SDK quando seu aplicativo for fechado.</span><span class="sxs-lookup"><span data-stu-id="11650-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="11650-123">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="11650-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="11650-124">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="11650-124">Session events</span></span>
<span data-ttu-id="11650-125">Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="11650-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="11650-126">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="11650-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="11650-127">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="11650-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="11650-128">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="11650-128">Standalone events</span></span>
<span data-ttu-id="11650-129">Toosession contrary eventos, autônomo podem ser usados fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="11650-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="11650-130">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="11650-131">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="11650-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="11650-132">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="11650-132">Session errors</span></span>
<span data-ttu-id="11650-133">Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="11650-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="11650-134">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="11650-135">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="11650-135">Standalone errors</span></span>
<span data-ttu-id="11650-136">Erros de toosession contrary, erros de autônomo podem ser usados fora do contexto de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="11650-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="11650-137">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="11650-138">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="11650-138">Reporting Jobs</span></span>
<span data-ttu-id="11650-139">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-139">**Example:**</span></span>

<span data-ttu-id="11650-140">Suponha que você deseja tooreport Olá duração do processo de logon:</span><span class="sxs-lookup"><span data-stu-id="11650-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="11650-141">Relatar erros durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="11650-141">Report Errors during a Job</span></span>
<span data-ttu-id="11650-142">Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="11650-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="11650-143">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-143">**Example:**</span></span>

<span data-ttu-id="11650-144">Suponha que você deseja tooreport um erro durante o processo de logon:</span><span class="sxs-lookup"><span data-stu-id="11650-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="11650-145">Eventos durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="11650-145">Events during a job</span></span>
<span data-ttu-id="11650-146">Os eventos podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="11650-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="11650-147">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-147">**Example:**</span></span>

<span data-ttu-id="11650-148">Suponha que temos uma rede social e usamos um trabalho tooreport Olá total tempo durante o qual Olá usuário conectado toohello server.</span><span class="sxs-lookup"><span data-stu-id="11650-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="11650-149">usuário Olá pode receber mensagens de seus amigos, este é um evento de trabalho.</span><span class="sxs-lookup"><span data-stu-id="11650-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="11650-150">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="11650-150">Extra parameters</span></span>
<span data-ttu-id="11650-151">Dados arbitrários podem ser anexados tooevents, erros, atividades e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="11650-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="11650-152">Esses dados podem ser estruturados, eles usam a classe NSDictionary do iOS.</span><span class="sxs-lookup"><span data-stu-id="11650-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="11650-153">Observe que os extras podem conter `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou outras instâncias de `NSDictionary`. </span><span class="sxs-lookup"><span data-stu-id="11650-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="11650-154">Olá parâmetro extra é serializado em JSON.</span><span class="sxs-lookup"><span data-stu-id="11650-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="11650-155">Se você quiser toopass diferentes objetos que Olá descritos acima, você deve implementar Olá método na classe a seguir:</span><span class="sxs-lookup"><span data-stu-id="11650-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="11650-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="11650-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="11650-157">método Hello deve retornar uma representação JSON do seu objeto.</span><span class="sxs-lookup"><span data-stu-id="11650-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="11650-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="11650-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="11650-159">Limites</span><span class="sxs-lookup"><span data-stu-id="11650-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="11650-160">simétricas</span><span class="sxs-lookup"><span data-stu-id="11650-160">Keys</span></span>
<span data-ttu-id="11650-161">Cada chave no hello `NSDictionary` devem corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="11650-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="11650-162">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="11650-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="11650-163">Tamanho</span><span class="sxs-lookup"><span data-stu-id="11650-163">Size</span></span>
<span data-ttu-id="11650-164">Extras são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo agente de contrato Olá).</span><span class="sxs-lookup"><span data-stu-id="11650-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="11650-165">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="11650-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="11650-166">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="11650-166">Reporting Application Information</span></span>
<span data-ttu-id="11650-167">Você pode relatar manualmente controle informações (ou quaisquer outras informações específicas do aplicativo) usando Olá `sendAppInfo:` função.</span><span class="sxs-lookup"><span data-stu-id="11650-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="11650-168">Observe que essas informações podem ser enviadas incrementalmente: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11650-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="11650-169">Como extras de evento, hello `NSDictionary` classe é usada tooabstract informações do aplicativo, observe que as matrizes ou dicionários sub serão tratados como cadeias de caracteres simples (usando a serialização JSON).</span><span class="sxs-lookup"><span data-stu-id="11650-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="11650-170">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="11650-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="11650-171">Limites</span><span class="sxs-lookup"><span data-stu-id="11650-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="11650-172">simétricas</span><span class="sxs-lookup"><span data-stu-id="11650-172">Keys</span></span>
<span data-ttu-id="11650-173">Cada chave no hello `NSDictionary` devem corresponder Olá expressão regular a seguir:</span><span class="sxs-lookup"><span data-stu-id="11650-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="11650-174">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="11650-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="11650-175">Tamanho</span><span class="sxs-lookup"><span data-stu-id="11650-175">Size</span></span>
<span data-ttu-id="11650-176">Informações do aplicativo são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo agente de contrato Olá).</span><span class="sxs-lookup"><span data-stu-id="11650-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="11650-177">Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="11650-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
