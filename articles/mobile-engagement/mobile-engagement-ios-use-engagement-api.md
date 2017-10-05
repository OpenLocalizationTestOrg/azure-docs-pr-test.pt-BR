---
title: Como usar o API Engagement no iOS
description: SDK do iOS mais recente - Como usar a API Engagement no iOS
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
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="f82a9-103">Como usar o API Engagement no iOS</span><span class="sxs-lookup"><span data-stu-id="f82a9-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="f82a9-104">Este documento é um complemento para o documento Como integrar o Engagement no iOS: ele fornece detalhes aprofundados sobre como usar a API Engagement para relatar as estatísticas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f82a9-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="f82a9-105">Tenha em mente que caso queira o Engagement apenas para relatar as sessões, atividades, falhas e informações técnicas do seu aplicativo, então a maneira mais simples é fazer todos os seus objetos personalizados `UIViewController` herdados da classe `EngagementViewController` correspondente.</span><span class="sxs-lookup"><span data-stu-id="f82a9-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="f82a9-106">Se você quiser fazer mais, por exemplo, se você precisar reportar eventos, erros e trabalhos específicos do aplicativo ou se você tiver que relatar as atividades do seu aplicativo de maneira diferente de um implementado nas classes `EngagementViewController`, você precisará usar a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f82a9-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="f82a9-107">A API do Engagement é fornecida pela classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="f82a9-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="f82a9-108">Uma instância desta classe pode ser recuperada chamando o método estático `[EngagementAgent shared]` (Observe que o objeto retornado `EngagementAgent` é um singleton).</span><span class="sxs-lookup"><span data-stu-id="f82a9-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="f82a9-109">Antes de qualquer chamada de API, o objeto `EngagementAgent` deve ser inicializado chamando o método `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="f82a9-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="f82a9-110">Conceitos de Engagement</span><span class="sxs-lookup"><span data-stu-id="f82a9-110">Engagement concepts</span></span>
<span data-ttu-id="f82a9-111">As seguintes partes refinam os [Conceitos de Mobile Engagement](mobile-engagement-concepts.md) usuais para a plataforma iOS.</span><span class="sxs-lookup"><span data-stu-id="f82a9-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="f82a9-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="f82a9-112">`Session` and `Activity`</span></span>
<span data-ttu-id="f82a9-113">Uma *atividade* geralmente está associada com uma tela do aplicativo, isso significa que a *atividade* se inicia quando a tela é exibida e é interrompida quando a tela for fechada: esse é o caso quando o SDK Engagement é integrado usando as classes `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="f82a9-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="f82a9-114">Mas as *atividades* também podem ser controladas manualmente usando a API do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f82a9-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="f82a9-115">Isso permite dividir uma determinada tela em várias partes secundárias para obter mais detalhes sobre o uso desta tela (por exemplo para com frequência e por quanto tempo as caixas de diálogo são usadas dentro desta tela).</span><span class="sxs-lookup"><span data-stu-id="f82a9-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="f82a9-116">Relatório de atividades</span><span class="sxs-lookup"><span data-stu-id="f82a9-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="f82a9-117">O usuário inicia uma nova atividade</span><span class="sxs-lookup"><span data-stu-id="f82a9-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="f82a9-118">É necessário chamar `startActivity()` sempre que houver alterações de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="f82a9-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="f82a9-119">A primeira chamada para essa função inicia uma nova sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="f82a9-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="f82a9-120">O usuário encerra sua atividade atual</span><span class="sxs-lookup"><span data-stu-id="f82a9-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="f82a9-121">Você **NUNCA** deve chamar essa função por conta própria, exceto se você quiser dividir um uso de seu aplicativo em várias sessões: uma chamada para essa função encerraria a sessão atual imediatamente, portanto, uma chamada subsequente para `startActivity()` deveria iniciar uma nova sessão.</span><span class="sxs-lookup"><span data-stu-id="f82a9-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="f82a9-122">Essa função é chamada automaticamente pelo SDK quando seu aplicativo é fechado.</span><span class="sxs-lookup"><span data-stu-id="f82a9-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="f82a9-123">Eventos de relatório</span><span class="sxs-lookup"><span data-stu-id="f82a9-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="f82a9-124">Eventos de sessão</span><span class="sxs-lookup"><span data-stu-id="f82a9-124">Session events</span></span>
<span data-ttu-id="f82a9-125">Eventos de sessão são geralmente usados para relatar as ações executadas por um usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="f82a9-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="f82a9-126">**Exemplo sem dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="f82a9-127">**Exemplo com dados adicionais:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="f82a9-128">Eventos autônomos</span><span class="sxs-lookup"><span data-stu-id="f82a9-128">Standalone events</span></span>
<span data-ttu-id="f82a9-129">Ao contrário dos eventos de sessão, os eventos autônomos podem ser usados fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="f82a9-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="f82a9-130">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="f82a9-131">Erros de relatório</span><span class="sxs-lookup"><span data-stu-id="f82a9-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="f82a9-132">Erros de sessão</span><span class="sxs-lookup"><span data-stu-id="f82a9-132">Session errors</span></span>
<span data-ttu-id="f82a9-133">Erros de sessão são geralmente usados para relatar os erros que afetam o usuário durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="f82a9-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="f82a9-134">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="f82a9-135">Erros autônomos</span><span class="sxs-lookup"><span data-stu-id="f82a9-135">Standalone errors</span></span>
<span data-ttu-id="f82a9-136">Ao contrário dos erros de sessão, os erros autônomos podem ser usados fora do contexto de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="f82a9-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="f82a9-137">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="f82a9-138">Relatório de trabalhos</span><span class="sxs-lookup"><span data-stu-id="f82a9-138">Reporting Jobs</span></span>
<span data-ttu-id="f82a9-139">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-139">**Example:**</span></span>

<span data-ttu-id="f82a9-140">Suponha que você deseja relatar a duração do processo de logon:</span><span class="sxs-lookup"><span data-stu-id="f82a9-140">Suppose you want to report the duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="f82a9-141">Relatar erros durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="f82a9-141">Report Errors during a Job</span></span>
<span data-ttu-id="f82a9-142">Os erros podem estar relacionados a um trabalho em execução, em vez de serem relacionados a sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="f82a9-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="f82a9-143">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-143">**Example:**</span></span>

<span data-ttu-id="f82a9-144">Suponha que você deseja relatar um erro durante o processo de logon:</span><span class="sxs-lookup"><span data-stu-id="f82a9-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="f82a9-145">Eventos durante um trabalho</span><span class="sxs-lookup"><span data-stu-id="f82a9-145">Events during a job</span></span>
<span data-ttu-id="f82a9-146">Os erros podem estar relacionados a um trabalho em execução, em vez de serem relacionados a sessão do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="f82a9-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="f82a9-147">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-147">**Example:**</span></span>

<span data-ttu-id="f82a9-148">Suponha que temos uma rede social e usamos um trabalho para relatar o tempo total durante o qual o usuário está conectado ao servidor.</span><span class="sxs-lookup"><span data-stu-id="f82a9-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="f82a9-149">O usuário pode receber mensagens de seus amigos, esse é um evento de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f82a9-149">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="f82a9-150">Parâmetros adicionais</span><span class="sxs-lookup"><span data-stu-id="f82a9-150">Extra parameters</span></span>
<span data-ttu-id="f82a9-151">Os dados arbitrários podem ser anexados aos eventos, erros, atividades e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f82a9-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="f82a9-152">Esses dados podem ser estruturados, eles usam a classe NSDictionary do iOS.</span><span class="sxs-lookup"><span data-stu-id="f82a9-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="f82a9-153">Observe que os extras podem conter `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou outras instâncias de `NSDictionary`. </span><span class="sxs-lookup"><span data-stu-id="f82a9-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="f82a9-154">Esse parâmetro adicional é serializado em JSON.</span><span class="sxs-lookup"><span data-stu-id="f82a9-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="f82a9-155">Se você quiser passar objetos diferentes dos descritos acima, você deve implementar o método a seguir em sua classe:</span><span class="sxs-lookup"><span data-stu-id="f82a9-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="f82a9-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="f82a9-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="f82a9-157">O método deve retornar uma representação JSON de seu objeto.</span><span class="sxs-lookup"><span data-stu-id="f82a9-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="f82a9-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f82a9-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="f82a9-159">Limites</span><span class="sxs-lookup"><span data-stu-id="f82a9-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="f82a9-160">simétricas</span><span class="sxs-lookup"><span data-stu-id="f82a9-160">Keys</span></span>
<span data-ttu-id="f82a9-161">Cada chave no `NSDictionary` deve corresponder a seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="f82a9-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="f82a9-162">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="f82a9-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="f82a9-163">Tamanho</span><span class="sxs-lookup"><span data-stu-id="f82a9-163">Size</span></span>
<span data-ttu-id="f82a9-164">Os adicionais estão limitados à **1024** caracteres por chamada (uma vez codificado no JSON pelo agente de Engagement).</span><span class="sxs-lookup"><span data-stu-id="f82a9-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="f82a9-165">No exemplo anterior, o JSON enviado para o servidor tem 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="f82a9-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="f82a9-166">Relatório de informações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f82a9-166">Reporting Application Information</span></span>
<span data-ttu-id="f82a9-167">Você pode relatar manualmente informações (ou quaisquer outras informações específicas do aplicativo) de controle usando a função `sendAppInfo:` .</span><span class="sxs-lookup"><span data-stu-id="f82a9-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="f82a9-168">Observe que essas informações podem ser enviadas de forma incremental: somente o último valor para uma determinada chave será mantido por um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f82a9-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="f82a9-169">Como os adicionais de evento, a classe `NSDictionary` é usada para abstrair as informações do aplicativo, observe que matrizes ou subdicionários serão tratados como cadeias de caracteres simples (usando a serialização JSON).</span><span class="sxs-lookup"><span data-stu-id="f82a9-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="f82a9-170">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="f82a9-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="f82a9-171">Limites</span><span class="sxs-lookup"><span data-stu-id="f82a9-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="f82a9-172">simétricas</span><span class="sxs-lookup"><span data-stu-id="f82a9-172">Keys</span></span>
<span data-ttu-id="f82a9-173">Cada chave no `NSDictionary` deve corresponder a seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="f82a9-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="f82a9-174">Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).</span><span class="sxs-lookup"><span data-stu-id="f82a9-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="f82a9-175">Tamanho</span><span class="sxs-lookup"><span data-stu-id="f82a9-175">Size</span></span>
<span data-ttu-id="f82a9-176">Os adicionais estão limitados à **1024** caracteres por chamada (uma vez codificado no JSON pelo agente de Engagement).</span><span class="sxs-lookup"><span data-stu-id="f82a9-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="f82a9-177">No exemplo anterior, o JSON enviado para o servidor tem 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="f82a9-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
