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
# <a name="how-toouse-hello-engagement-api-on-android"></a>Como tooUse Olá contrato de API no Android
Este é um documento de toohello complemento [opções avançadas de relatório para o Android SDK do Mobile Engagement](mobile-engagement-android-advanced-reporting.md). Ele fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.

Tenha em mente que se você desejar contrato tooreport somente sessões, atividades, falhas e obter informações técnicas do seu aplicativo, em seguida, hello forma mais simples é toomake todos os seus `Activity` subclasses herdam Olá correspondente `EngagementActivity` classe.

Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementActivity` classes, e em seguida, você precisa toouse Olá Contrato de API.

Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe. Uma instância desta classe pode ser recuperada pela chamada hello `EngagementAgent.getInstance(Context)` método estático (Observe que Olá `EngagementAgent` objeto retornado é um singleton).

## <a name="engagement-concepts"></a>Conceitos de Engagement
seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md), para a plataforma Android hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se usuário Olá permanecer mais de alguns segundos de ociosidade entre dois *atividades*, em seguida, sua sequência de *atividades* é dividido em dois distintos *sessões*. Esses alguns segundos são chamados hello "tempo limite da sessão".

Um *atividade* geralmente está associado com uma tela do aplicativo hello, que é hello toosay *atividade* inicia quando a tela hello é exibida e é interrompido quando a tela hello está fechada: isso é hello quando Olá SDK de contrato é integrado usando Olá `EngagementActivity` classes.

Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API. Isso permite uma determinada tela toosplit em vários tooget de partes sub mais detalhes sobre Olá uso desta tela (por exemplo tooknown frequência e quanto tempo as caixas de diálogo são usadas dentro desta tela).

## <a name="reporting-activities"></a>Relatório de atividades
> [!IMPORTANT]
> Não é necessário tooreport atividades, como descrito nesta seção se você estiver usando Olá `EngagementActivity` classe e suas variantes conforme explicado em hello como tooIntegrate contrato no documento Android.
> 
> 

### <a name="user-starts-a-new-activity"></a>O usuário inicia uma nova atividade
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Você precisa toocall `startActivity()` alterações de cada atividade de usuário de saudação do tempo. Olá primeira chamada toothis função inicia uma nova sessão de usuário.

Olá melhor toocall local é essa função em cada atividade `onResume` retorno de chamada.

### <a name="user-ends-his-current-activity"></a>O usuário encerra sua atividade atual
            EngagementAgent.getInstance(this).endActivity();

Você precisa toocall `endActivity()` pelo menos uma vez quando o usuário Olá termina sua última atividade. Isso informa Olá expirará SDK de contrato que usuário hello está ocioso no momento e que a sessão de usuário Olá necessário toobe uma vez fechado Olá tempo limite da sessão (se você chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado).

Olá melhor toocall local é essa função em cada atividade `onPause` retorno de chamada.

## <a name="reporting-events"></a>Eventos de relatório
### <a name="session-events"></a>Eventos de sessão
Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.

**Exemplo sem dados adicionais:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Exemplo com dados adicionais:**

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

### <a name="standalone-events"></a>Eventos autônomos
Eventos de toosession contrary, podem ocorrer eventos autônomo fora do contexto de saudação de uma sessão.

**Exemplo:**

Suponha que você deseja tooreport os eventos que ocorrem quando um receptor de difusão é acionado:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Erros de relatório
### <a name="session-errors"></a>Erros de sessão
Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.

**Exemplo:**

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

### <a name="standalone-errors"></a>Erros autônomos
Erros de toosession contrary, podem ocorrer erros autônomo fora do contexto de saudação de uma sessão.

**Exemplo:**

Olá exemplo a seguir mostra como tooreport um erro sempre que a memória de saudação se torna baixa no telefone Olá durante o processo de aplicativo está sendo executado.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Relatório de trabalhos
### <a name="example"></a>Exemplo
Suponha que você deseja tooreport Olá duração do processo de logon:

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

### <a name="report-errors-during-a-job"></a>Relatar erros durante um trabalho
Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.

**Exemplo:**

Suponha que você queira tooreport um erro durante a você fazer logon em processo:

[...] public void signIn(Context context, ...) {

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

### <a name="reporting-events-during-a-job"></a>Relatar eventos durante um trabalho
Os eventos podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.

**Exemplo:**

Suponha que temos uma rede social e usamos um trabalho tooreport Olá total tempo durante o qual Olá usuário conectado toohello server. usuário Olá pode permanecer conectado em segundo plano, mesmo se ele estiver usando outro aplicativo ou ao telefone hello está em suspensão, portanto não há nenhuma sessão.

usuário Olá pode receber mensagens de seus amigos, este é um evento de trabalho.

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

## <a name="extra-parameters"></a>Parâmetros adicionais
Dados arbitrários podem ser anexados tooevents, erros, atividades e trabalhos.

Esses dados podem ser estruturados, eles usam a classe de pacote do Android (na verdade, eles funcionam como parâmetros extras no Android Intents). Observe que um pacote pode conter matrizes ou outras instâncias de pacote.

> [!IMPORTANT]
> Se você colocar em parâmetros parcelable ou serializáveis, verifique se seus `toString()` método é implementado tooreturn uma cadeia de caracteres legível. As classes serializáveis que contêm campos não transitórios que não são serializáveis farão com que o Android falhe quando você chamar `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Não há suporte para matrizes esparsas em parâmetros extras, ou seja, ela não será serializada como uma matriz. Você deve convertê-las em matrizes padrão antes de usá-las em parâmetros extras.
> 
> 

### <a name="example"></a>Exemplo
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limites
#### <a name="keys"></a>simétricas
Cada chave no hello `Bundle` devem corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Extras são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo serviço de contrato de saudação).

Em Olá o exemplo anterior, Olá JSON enviado toohello server é 58 caracteres:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Relatório de informações de aplicativo
Você pode relatar manualmente controle informações (ou quaisquer outras informações específicas do aplicativo) usando Olá `sendAppInfo()` função.

Observe que essas informações podem ser enviadas incrementalmente: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo.

Como evento extras, Olá classe do pacote é usado tooabstract informações do aplicativo, observe que matrizes ou sub pacotes será tratado como cadeias de caracteres simples (usando a serialização JSON).

### <a name="example"></a>Exemplo
Aqui está um gênero do usuário de toosend de exemplo de código e a data de nascimento:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>limites
#### <a name="keys"></a>simétricas
Cada chave no hello `Bundle` devem corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Informações do aplicativo são muito limitadas**1024** caracteres por chamada (uma vez codificada em JSON pelo serviço de contrato de saudação).

Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:

            {"expiration":"2016-12-07","status":"premium"}
