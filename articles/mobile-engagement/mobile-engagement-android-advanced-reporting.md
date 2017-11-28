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
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="8a8c7-103">Relatório avançado com o Engagement no Android</span><span class="sxs-lookup"><span data-stu-id="8a8c7-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a8c7-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="8a8c7-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="8a8c7-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8a8c7-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="8a8c7-106">iOS</span><span class="sxs-lookup"><span data-stu-id="8a8c7-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="8a8c7-107">Android</span><span class="sxs-lookup"><span data-stu-id="8a8c7-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="8a8c7-108">Este tópico descreve cenários de relatório adicionais em seu aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="8a8c7-109">Você pode aplicar esses aplicativos de toohello opções criado no hello [Introdução](mobile-engagement-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a8c7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8a8c7-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="8a8c7-111">tutorial Olá você concluído foi deliberadamente simples e direta, mas existem avançados opções que você pode escolher.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="8a8c7-112">Modificação das classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="8a8c7-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="8a8c7-113">Em Olá [tutorial de Introdução](mobile-engagement-android-get-started.md), tudo o que você tinha toodo foi toomake seu `*Activity` subclasses herdam Olá correspondente `Engagement*Activity` classes.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="8a8c7-114">Por exemplo, se sua atividade herdada tiver estendido o `ListActivity`, você a faria estender `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a8c7-115">Ao usar `EngagementListActivity` ou `EngagementExpandableListActivity`, certifique-se de que qualquer chamada muito`requestWindowFeature(...);` é feita antes da chamada de saudação muito`super.onCreate(...);`, caso contrário ocorrerá uma falha.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="8a8c7-116">Você pode encontrar essas classes no hello `src` pasta e pode copiá-los em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="8a8c7-117">classes de saudação também estão em hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="8a8c7-118">Método alternativo: chame `startActivity()` e `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="8a8c7-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="8a8c7-119">Se você não pode ou não toooverload seu `Activity` classes, você pode em vez disso, iniciar e terminar suas atividades chamando Olá `EngagementAgent`do métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a8c7-120">Olá Android SDK nunca chama Olá `endActivity()` método, mesmo quando o aplicativo hello é fechado (no Android, aplicativos são nunca fechados).</span><span class="sxs-lookup"><span data-stu-id="8a8c7-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="8a8c7-121">Portanto, é *altamente* recomendado Olá toocall `startActivity()` método hello `onResume` retorno de chamada de *todos os* suas atividades e Olá `endActivity()` método hello `onPause()` retorno de chamada de *todas as* suas atividades.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="8a8c7-122">Isso é Olá somente modo toobe-se de que não vazam sessões.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="8a8c7-123">Se uma sessão é vazada, Olá serviço contrato nunca desconecta de back-end de contrato de saudação (como serviço Olá permanece conectado enquanto uma sessão estiver pendente).</span><span class="sxs-lookup"><span data-stu-id="8a8c7-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="8a8c7-124">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="8a8c7-124">Here is an example:</span></span>

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

<span data-ttu-id="8a8c7-125">Este exemplo é semelhante toohello `EngagementActivity` classe e suas variantes, cujo código-fonte é fornecido no hello `src` pasta.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="8a8c7-126">Usando Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="8a8c7-126">Using Application.onCreate()</span></span>
<span data-ttu-id="8a8c7-127">Qualquer código que você coloca em `Application.onCreate()` e em outro aplicativo de retornos de chamada é executado para processos de todos os seus aplicativos, incluindo o serviço de contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="8a8c7-128">Pode ter efeitos colaterais indesejados, como as alocações de memória desnecessários e threads no processo de saudação do contrato, ou duplicados de difusão de destinatários ou serviços.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="8a8c7-129">Se você substituir `Application.onCreate()`, é recomendável adicionar Olá seguindo o trecho de código no início de saudação do seu `Application.onCreate()` função:</span><span class="sxs-lookup"><span data-stu-id="8a8c7-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="8a8c7-130">Você pode fazer Olá para a mesma coisa `Application.onTerminate()`, `Application.onLowMemory()`, e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="8a8c7-131">Você também pode estender `EngagementApplication` em vez de estender `Application`: Olá retorno de chamada `Application.onCreate()` Olá seleção de processo e chamadas `Application.onApplicationProcessCreate()` somente se processo atual Olá for não Olá uma saudação contrato serviço de hospedagem, hello mesmas regras se aplicam para Olá outras chamadas de retorno.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="8a8c7-132">Marcas no arquivo de AndroidManifest.xml Olá</span><span class="sxs-lookup"><span data-stu-id="8a8c7-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="8a8c7-133">Na marca de serviço Olá no arquivo de AndroidManifest.xml hello, Olá `android:label` atributo permite que você toochoose Olá nome da saudação serviço contrato como ele aparece tooend usuários na tela de "Serviços em execução" hello do seu telefone.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="8a8c7-134">Recomendamos que a configuração deste atributo muito`"<Your application name>Service"` (por exemplo, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="8a8c7-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="8a8c7-135">Olá especificando `android:process` atributo garante que Olá contrato o serviço é executado em seu próprio processo (executando o contrato Olá mesmo processo que seu aplicativo faz com que o thread principal de interfaces de usuário responsivo potencialmente menor).</span><span class="sxs-lookup"><span data-stu-id="8a8c7-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="8a8c7-136">Compilando com o ProGuard</span><span class="sxs-lookup"><span data-stu-id="8a8c7-136">Building with ProGuard</span></span>
<span data-ttu-id="8a8c7-137">Se você criar seu pacote de aplicativo com ProGuard, será necessário tookeep algumas classes.</span><span class="sxs-lookup"><span data-stu-id="8a8c7-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="8a8c7-138">Você pode usar o hello trecho de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a8c7-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
