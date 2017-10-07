---
title: "aaaAdvanced opções de relatório para o Android SDK do Azure Mobile Engagement"
description: "Descreve como toodo reporting toocapture análise avançada para Android SDK do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Relatório avançado com o Engagement no Android
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Este tópico descreve cenários de relatório adicionais em seu aplicativo Android. Você pode aplicar esses aplicativos de toohello opções criado no hello [Introdução](mobile-engagement-android-get-started.md) tutorial.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

tutorial Olá você concluído foi deliberadamente simples e direta, mas existem avançados opções que você pode escolher.

## <a name="modifying-your-activity-classes"></a>Modificação das classes `Activity`
Em Olá [tutorial de Introdução](mobile-engagement-android-get-started.md), tudo o que você tinha toodo foi toomake seu `*Activity` subclasses herdam Olá correspondente `Engagement*Activity` classes. Por exemplo, se sua atividade herdada tiver estendido o `ListActivity`, você a faria estender `EngagementListActivity`.

> [!IMPORTANT]
> Ao usar `EngagementListActivity` ou `EngagementExpandableListActivity`, certifique-se de que qualquer chamada muito`requestWindowFeature(...);` é feita antes da chamada de saudação muito`super.onCreate(...);`, caso contrário ocorrerá uma falha.
> 
> 

Você pode encontrar essas classes no hello `src` pasta e pode copiá-los em seu projeto. classes de saudação também estão em hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Método alternativo: chame `startActivity()` e `endActivity()` manualmente
Se você não pode ou não toooverload seu `Activity` classes, você pode em vez disso, iniciar e terminar suas atividades chamando Olá `EngagementAgent`do métodos diretamente.

> [!IMPORTANT]
> Olá Android SDK nunca chama Olá `endActivity()` método, mesmo quando o aplicativo hello é fechado (no Android, aplicativos são nunca fechados). Portanto, é *altamente* recomendado Olá toocall `startActivity()` método hello `onResume` retorno de chamada de *todos os* suas atividades e Olá `endActivity()` método hello `onPause()` retorno de chamada de *todas as* suas atividades. Isso é Olá somente modo toobe-se de que não vazam sessões. Se uma sessão é vazada, Olá serviço contrato nunca desconecta de back-end de contrato de saudação (como serviço Olá permanece conectado enquanto uma sessão estiver pendente).
> 
> 

Aqui está um exemplo:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

Este exemplo é semelhante toohello `EngagementActivity` classe e suas variantes, cujo código-fonte é fornecido no hello `src` pasta.

## <a name="using-applicationoncreate"></a>Usando Application.onCreate()
Qualquer código que você coloca em `Application.onCreate()` e em outro aplicativo de retornos de chamada é executado para processos de todos os seus aplicativos, incluindo o serviço de contrato de saudação. Pode ter efeitos colaterais indesejados, como as alocações de memória desnecessários e threads no processo de saudação do contrato, ou duplicados de difusão de destinatários ou serviços.

Se você substituir `Application.onCreate()`, é recomendável adicionar Olá seguindo o trecho de código no início de saudação do seu `Application.onCreate()` função:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Você pode fazer Olá para a mesma coisa `Application.onTerminate()`, `Application.onLowMemory()`, e `Application.onConfigurationChanged(...)`.

Você também pode estender `EngagementApplication` em vez de estender `Application`: Olá retorno de chamada `Application.onCreate()` Olá seleção de processo e chamadas `Application.onApplicationProcessCreate()` somente se processo atual Olá for não Olá uma saudação contrato serviço de hospedagem, hello mesmas regras se aplicam para Olá outras chamadas de retorno.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Marcas no arquivo de AndroidManifest.xml Olá
Na marca de serviço Olá no arquivo de AndroidManifest.xml hello, Olá `android:label` atributo permite que você toochoose Olá nome da saudação serviço contrato como ele aparece tooend usuários na tela de "Serviços em execução" hello do seu telefone. Recomendamos que a configuração deste atributo muito`"<Your application name>Service"` (por exemplo, `"AcmeFunGameService"`).

Olá especificando `android:process` atributo garante que Olá contrato o serviço é executado em seu próprio processo (executando o contrato Olá mesmo processo que seu aplicativo faz com que o thread principal de interfaces de usuário responsivo potencialmente menor).

## <a name="building-with-proguard"></a>Compilando com o ProGuard
Se você criar seu pacote de aplicativo com ProGuard, será necessário tookeep algumas classes. Você pode usar o hello trecho de configuração a seguir:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
