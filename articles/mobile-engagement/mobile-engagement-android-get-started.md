---
title: aaaGet iniciado com o Android aplicativos do Azure Mobile Engagement
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="285aa-103">Introdução ao Azure Mobile Engagement para Aplicativos Android</span><span class="sxs-lookup"><span data-stu-id="285aa-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="285aa-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo e como toosend envio os usuários toosegmented de notificações de um aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="285aa-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="285aa-105">Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="285aa-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="285aa-106">Nele, você cria um aplicativo Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="285aa-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="285aa-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="285aa-107">Prerequisites</span></span>
<span data-ttu-id="285aa-108">Concluir este tutorial requer Olá [Android Developer Tools](https://developer.android.com/sdk/index.html), que inclui o ambiente de desenvolvimento integrado do Android Studio hello e plataforma Android mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="285aa-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="285aa-109">Ela também exige Olá [Android SDK do Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="285aa-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="285aa-110">toocomplete neste tutorial, você precisa de uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="285aa-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="285aa-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="285aa-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="285aa-112">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="285aa-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="285aa-113">Configurar o Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="285aa-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="285aa-114">Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="285aa-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="285aa-115">Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="285aa-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="285aa-116">Você pode criar um aplicativo básico com a integração do Android Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="285aa-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="285aa-117">documentação de integração completa Olá pode ser encontrada no hello [integração Android SDK do Mobile Engagement](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="285aa-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="285aa-118">Criar um projeto Android</span><span class="sxs-lookup"><span data-stu-id="285aa-118">Create an Android project</span></span>
1. <span data-ttu-id="285aa-119">Iniciar **Android Studio**e no pop-up hello, selecione **iniciar um novo projeto do Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="285aa-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="285aa-120">Forneça um nome de aplicativo e um domínio da empresa.</span><span class="sxs-lookup"><span data-stu-id="285aa-120">Provide an app name and company domain.</span></span> <span data-ttu-id="285aa-121">Anote o que você está preenchendo, porque precisará disso posteriormente.</span><span class="sxs-lookup"><span data-stu-id="285aa-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="285aa-122">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="285aa-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="285aa-123">Selecione o fator de forma de destino hello e nível de API e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="285aa-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="285aa-124">O Mobile Engagement requer nível mínimo de API de 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="285aa-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="285aa-125">Selecione **atividade em branco** aqui, que é a única tela hello para este aplicativo e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="285aa-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="285aa-126">Finalmente, mantenha os padrões de saudação como está e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="285aa-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="285aa-127">Agora, o Android Studio cria Olá aplicativo de demonstração em que podemos integrar Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="285aa-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="285aa-128">Incluir a biblioteca de saudação do SDK em seu projeto</span><span class="sxs-lookup"><span data-stu-id="285aa-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="285aa-129">Baixar Olá [Android SDK do Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="285aa-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="285aa-130">Extrai Olá arquivo tooa morto em seu computador.</span><span class="sxs-lookup"><span data-stu-id="285aa-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="285aa-131">Identificar hello. jar biblioteca para a versão atual de saudação desse SDK e copiá-lo toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="285aa-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="285aa-132">Navegue toohello **projeto** seção (1) e cole. Olá JAR na pasta de bibliotecas de saudação (2).</span><span class="sxs-lookup"><span data-stu-id="285aa-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="285aa-133">biblioteca de saudação tooload, projeto de saudação de sincronização.</span><span class="sxs-lookup"><span data-stu-id="285aa-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="285aa-134">Conecte-se o seu back-end do aplicativo tooMobile contrato com hello cadeia de caracteres de Conexão</span><span class="sxs-lookup"><span data-stu-id="285aa-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="285aa-135">Saudação de copiar linhas de código a seguir para criação de atividade de saudação (deve ser feito apenas em um local do seu aplicativo, geralmente atividade principal da saudação).</span><span class="sxs-lookup"><span data-stu-id="285aa-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="285aa-136">Para este aplicativo de exemplo, abra Olá MainActivity em src -> principal -> pasta java e adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="285aa-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="285aa-137">Resolva referências Olá pressionando Alt + Enter ou adicionando Olá seguindo as instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="285aa-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="285aa-138">Voltar toohello Portal clássico do Azure em seu aplicativo **informações de Conexão** Olá página e cópia **cadeia de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="285aa-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="285aa-139">Cole Olá `setConnectionString` parâmetro, substituindo a cadeia de caracteres inteira Olá Olá código a seguir mostrada:</span><span class="sxs-lookup"><span data-stu-id="285aa-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="285aa-140">Adicionar permissões e uma declaração de serviço</span><span class="sxs-lookup"><span data-stu-id="285aa-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="285aa-141">Adicionar toohello essas permissões manifest. XML do projeto imediatamente antes ou após Olá `<application>` marca:</span><span class="sxs-lookup"><span data-stu-id="285aa-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="285aa-142">toodeclare Olá serviço de agente, adicione este código entre hello `<application>` e `</application>` marcas:</span><span class="sxs-lookup"><span data-stu-id="285aa-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="285aa-143">No código de saudação colados, substitua `"<Your application name>"` no rótulo hello, que é exibido no hello **configurações** onde você pode ver os serviços em execução no dispositivo de saudação do menu.</span><span class="sxs-lookup"><span data-stu-id="285aa-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="285aa-144">Por exemplo você pode adicionar palavra hello "Serviço" nesse rótulo.</span><span class="sxs-lookup"><span data-stu-id="285aa-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="285aa-145">Enviar um tooMobile tela Contrato</span><span class="sxs-lookup"><span data-stu-id="285aa-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="285aa-146">toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="285aa-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="285aa-147">Vá muito**MainActivity.java** e adicione Olá tooreplace hello classe base a seguir **MainActivity** muito**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="285aa-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="285aa-148">Se sua classe base não for *atividade*, consulte [avançado Android Reporting](mobile-engagement-android-advanced-reporting.md) como tooinherit de classes diferentes.</span><span class="sxs-lookup"><span data-stu-id="285aa-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="285aa-149">Comentar Olá linha para este cenário de exemplo simples a seguir:</span><span class="sxs-lookup"><span data-stu-id="285aa-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="285aa-150">Se você quiser Olá tookeep `ActionBar` em seu aplicativo, consulte [avançado Android Reporting](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="285aa-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="285aa-151">Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="285aa-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="285aa-152">Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="285aa-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="285aa-153">Durante uma campanha, o Mobile Engagement permite interagir e acessar em REACH seus usuários com notificações por push e mensagens no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="285aa-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="285aa-154">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="285aa-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="285aa-155">Olá seção a seguir define o seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="285aa-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="285aa-156">Copiar recursos de SDK em seu projeto</span><span class="sxs-lookup"><span data-stu-id="285aa-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="285aa-157">Navegue Olá de conteúdo e cópia de download SDK do back tooyour **res** pasta.</span><span class="sxs-lookup"><span data-stu-id="285aa-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="285aa-158">Voltar tooAndroid Studio, selecione Olá **principal** diretório de arquivos de projeto e, em seguida, cole-o projeto de tooyour tooadd Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="285aa-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="285aa-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="285aa-159">Next steps</span></span>
<span data-ttu-id="285aa-160">Vá muito[SDK do Android](mobile-engagement-android-sdk-overview.md) tooget detalhadas conhecimento sobre Olá integração SDK.</span><span class="sxs-lookup"><span data-stu-id="285aa-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
