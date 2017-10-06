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
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Como tooUse Olá contrato de API no iOS
Este documento é um complemento toohello como tooIntegrate contrato no iOS: fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.

Tenha em mente que se você quiser apenas contrato tooreport sessões, atividades, falhas e obter informações técnicas, seu aplicativo hello mais simples é forma toomake todos os personalizados `UIViewController` objetos herdam Olá correspondente `EngagementViewController` classe .

Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementViewController` classes, e em seguida, você precisa toouse Olá Contrato de API.

Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe. Uma instância desta classe pode ser recuperada pela chamada hello `[EngagementAgent shared]` método estático (Observe que Olá `EngagementAgent` objeto retornado é um singleton).

Antes de qualquer chamadas de API, hello `EngagementAgent` objeto deve ser inicializado chamando o método hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Conceitos de Engagement
seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md) para a plataforma do iOS hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Um *atividade* geralmente está associado com uma tela do aplicativo hello, que é hello toosay *atividade* inicia quando a tela hello é exibida e é interrompido quando a tela hello está fechada: isso é hello quando Olá SDK de contrato é integrado usando Olá `EngagementViewController` classes.

Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API. Isso permite uma determinada tela toosplit em vários tooget de partes sub mais detalhes sobre Olá uso desta tela (por exemplo tooknown frequência e quanto tempo as caixas de diálogo são usadas dentro desta tela).

## <a name="reporting-activities"></a>Relatório de atividades
### <a name="user-starts-a-new-activity"></a>O usuário inicia uma nova atividade
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Você precisa toocall `startActivity()` alterações de cada atividade de usuário de saudação do tempo. Olá primeira chamada toothis função inicia uma nova sessão de usuário.

### <a name="user-ends-his-current-activity"></a>O usuário encerra sua atividade atual
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Você deve **nunca** chamar essa função por conta própria, exceto se você quiser toosplit um uso de seu aplicativo em várias sessões: uma chamada de função toothis terminaria Olá atual sessão imediatamente, portanto, uma chamada subsequente muito`startActivity()`deve iniciar uma nova sessão. Esta função é chamada automaticamente por Olá SDK quando seu aplicativo for fechado.
> 
> 

## <a name="reporting-events"></a>Eventos de relatório
### <a name="session-events"></a>Eventos de sessão
Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.

**Exemplo sem dados adicionais:**

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

**Exemplo com dados adicionais:**

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

### <a name="standalone-events"></a>Eventos autônomos
Toosession contrary eventos, autônomo podem ser usados fora do contexto de saudação de uma sessão.

**Exemplo:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Erros de relatório
### <a name="session-errors"></a>Erros de sessão
Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.

**Exemplo:**

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

### <a name="standalone-errors"></a>Erros autônomos
Erros de toosession contrary, erros de autônomo podem ser usados fora do contexto de saudação de uma sessão.

**Exemplo:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Relatório de trabalhos
**Exemplo:**

Suponha que você deseja tooreport Olá duração do processo de logon:

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

### <a name="report-errors-during-a-job"></a>Relatar erros durante um trabalho
Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.

**Exemplo:**

Suponha que você deseja tooreport um erro durante o processo de logon:

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

### <a name="events-during-a-job"></a>Eventos durante um trabalho
Os eventos podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.

**Exemplo:**

Suponha que temos uma rede social e usamos um trabalho tooreport Olá total tempo durante o qual Olá usuário conectado toohello server. usuário Olá pode receber mensagens de seus amigos, este é um evento de trabalho.

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

## <a name="extra-parameters"></a>Parâmetros adicionais
Dados arbitrários podem ser anexados tooevents, erros, atividades e trabalhos.

Esses dados podem ser estruturados, eles usam a classe NSDictionary do iOS.

Observe que os extras podem conter `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou outras instâncias de `NSDictionary`. 

> [!NOTE]
> Olá parâmetro extra é serializado em JSON. Se você quiser toopass diferentes objetos que Olá descritos acima, você deve implementar Olá método na classe a seguir:
> 
> -(NSString*)JSONRepresentation;
> 
> método Hello deve retornar uma representação JSON do seu objeto.
> 
> 

### <a name="example"></a>Exemplo
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limites
#### <a name="keys"></a>simétricas
Cada chave no hello `NSDictionary` devem corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Extras são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo agente de contrato Olá).

Em Olá o exemplo anterior, Olá JSON enviado toohello server é 58 caracteres:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Relatório de informações de aplicativo
Você pode relatar manualmente controle informações (ou quaisquer outras informações específicas do aplicativo) usando Olá `sendAppInfo:` função.

Observe que essas informações podem ser enviadas incrementalmente: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.

Como extras de evento, hello `NSDictionary` classe é usada tooabstract informações do aplicativo, observe que as matrizes ou dicionários sub serão tratados como cadeias de caracteres simples (usando a serialização JSON).

**Exemplo:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limites
#### <a name="keys"></a>simétricas
Cada chave no hello `NSDictionary` devem corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Informações do aplicativo são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo agente de contrato Olá).

Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:

    {"birthdate":"1983-12-07","gender":"female"}
