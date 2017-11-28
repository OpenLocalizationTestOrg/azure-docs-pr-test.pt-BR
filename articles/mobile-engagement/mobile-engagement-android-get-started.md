---
title: "Introdução ao Azure Mobile Engagement para Aplicativos Android"
description: "Aprenda a usar o Azure Mobile Engagement com análises e notificações por push para aplicativos Android."
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
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="f8f98-103">Introdução ao Azure Mobile Engagement para Aplicativos Android</span><span class="sxs-lookup"><span data-stu-id="f8f98-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="f8f98-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e como enviar notificações por push para usuários segmentados de um aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="f8f98-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="f8f98-105">Esse tutorial demonstra um cenário de transmissão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f8f98-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="f8f98-106">Nele, você cria um aplicativo Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="f8f98-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8f98-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8f98-107">Prerequisites</span></span>
<span data-ttu-id="f8f98-108">A conclusão deste tutorial requer as [Ferramentas para desenvolvedores do Android](https://developer.android.com/sdk/index.html), que incluem o ambiente de desenvolvimento integrado do Android Studio e a plataforma Android mais recente.</span><span class="sxs-lookup"><span data-stu-id="f8f98-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="f8f98-109">Também é necessário baixar o [SDK do Mobile Engagement Android](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="f8f98-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8f98-110">Para concluir este tutorial, você precisa de uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8f98-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="f8f98-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f8f98-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f8f98-112">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="f8f98-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="f8f98-113">Configurar o Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="f8f98-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="f8f98-114">Conectar o aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f8f98-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="f8f98-115">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="f8f98-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="f8f98-116">Você cria um aplicativo básico com o Android Studio para demonstrar a integração.</span><span class="sxs-lookup"><span data-stu-id="f8f98-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="f8f98-117">A documentação de integração completa pode ser encontrada na [Integração do SDK do Mobile Engagement Android](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8f98-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="f8f98-118">Criar um projeto Android</span><span class="sxs-lookup"><span data-stu-id="f8f98-118">Create an Android project</span></span>
1. <span data-ttu-id="f8f98-119">Inicie o **Android Studio** e no pop-up, selecione **Iniciar um novo projeto do Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="f8f98-120">Forneça um nome de aplicativo e um domínio da empresa.</span><span class="sxs-lookup"><span data-stu-id="f8f98-120">Provide an app name and company domain.</span></span> <span data-ttu-id="f8f98-121">Anote o que você está preenchendo, porque precisará disso posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8f98-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="f8f98-122">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="f8f98-123">Selecione o fator forma de destino e o nível de API e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f8f98-124">O Mobile Engagement requer nível mínimo de API de 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="f8f98-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="f8f98-125">Selecione a **Atividade em Branco** aqui, que é a única tela para esse aplicativo e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="f8f98-126">Finalmente, mantenha os padrões como estão e clique **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="f8f98-127">O Android Studio agora criará o aplicativo de demonstração no qual integraremos o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f8f98-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="f8f98-128">Inclua a biblioteca de SDK em seu projeto</span><span class="sxs-lookup"><span data-stu-id="f8f98-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="f8f98-129">Baixe o [SDK do Mobile Engagement Android](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="f8f98-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="f8f98-130">Extraia o file de arquivo para uma pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f8f98-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="f8f98-131">Identifique a biblioteca. jar para a versão atual desse SDK e copie-a para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="f8f98-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="f8f98-132">Navegue para a seção **Projeto** (1) e cole o .jar na pasta de bibliotecas (2).</span><span class="sxs-lookup"><span data-stu-id="f8f98-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="f8f98-133">Para carregar a biblioteca, sincronize o projeto.</span><span class="sxs-lookup"><span data-stu-id="f8f98-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="f8f98-134">Conecte seu aplicativo ao back-end do Mobile Engagement com a Cadeia de Conexão</span><span class="sxs-lookup"><span data-stu-id="f8f98-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="f8f98-135">Copie as seguintes linhas de código para a criação da atividade (deve ser feito apenas em um local do seu aplicativo, geralmente a atividade principal).</span><span class="sxs-lookup"><span data-stu-id="f8f98-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="f8f98-136">Para este aplicativo de exemplo, abra a MainActivity em src -> main -> pasta java e adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8f98-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="f8f98-137">Resolva as referências pressionando Alt + Enter ou adicionando as seguintes instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="f8f98-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="f8f98-138">Volte para o Portal Clássico do Azure na página **Informações da Conexão** do seu aplicativo e copie a **Cadeia de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="f8f98-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="f8f98-139">Cole no parâmetro `setConnectionString`, substituindo a cadeia de caracteres inteira mostrada no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8f98-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="f8f98-140">Adicionar permissões e uma declaração de serviço</span><span class="sxs-lookup"><span data-stu-id="f8f98-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="f8f98-141">Adicionar essas permissões ao Manifest.xml do projeto imediatamente anteriores ou posteriores à marca `<application>`:</span><span class="sxs-lookup"><span data-stu-id="f8f98-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="f8f98-142">Para declarar o serviço do agente, adicione este código entre as marcações `<application>` e `</application>`:</span><span class="sxs-lookup"><span data-stu-id="f8f98-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="f8f98-143">No código colado, substitua `"<Your application name>"` no rótulo, que é exibido no menu **Configurações** onde você pode ver os serviços em execução no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f8f98-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="f8f98-144">Você pode adicionar a palavra "Serviço" desse rótulo por exemplo.</span><span class="sxs-lookup"><span data-stu-id="f8f98-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="f8f98-145">Enviar uma tela ao Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f8f98-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="f8f98-146">Para iniciar o envio dos dados e assegurar que os usuários estão ativos, você deve enviar pelo menos uma tela (Atividade) para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f8f98-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="f8f98-147">Vá para **MainActivity. Java** e adicione o seguinte para substituir a classe base de **MainActivity** por **EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="f8f98-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="f8f98-148">Se sua classe base não for *Activity*, consulte [Relatório Android Avançado](mobile-engagement-android-advanced-reporting.md) para saber como herdar de classes diferentes.</span><span class="sxs-lookup"><span data-stu-id="f8f98-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="f8f98-149">Comente (exclua) a linha a seguir para este cenário de exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="f8f98-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="f8f98-150">Se você quiser manter `ActionBar` em seu aplicativo, consulte [Relatório Avançado do Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="f8f98-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="f8f98-151">Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="f8f98-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="f8f98-152">Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="f8f98-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="f8f98-153">Durante uma campanha, o Mobile Engagement permite interagir e acessar em REACH seus usuários com notificações por push e mensagens no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8f98-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="f8f98-154">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f8f98-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="f8f98-155">A seção a seguir configura seu aplicativo para recebê-las.</span><span class="sxs-lookup"><span data-stu-id="f8f98-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="f8f98-156">Copiar recursos de SDK em seu projeto</span><span class="sxs-lookup"><span data-stu-id="f8f98-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="f8f98-157">Navegue de volta até o conteúdo baixado do SDK e copie a pasta **res** .</span><span class="sxs-lookup"><span data-stu-id="f8f98-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="f8f98-158">Volte para o Android Studio, selecione o diretório **principal** dos arquivos de projeto e cole-o para adicionar os recursos ao projeto.</span><span class="sxs-lookup"><span data-stu-id="f8f98-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="f8f98-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8f98-159">Next steps</span></span>
<span data-ttu-id="f8f98-160">Vá para [SDK do Android](mobile-engagement-android-sdk-overview.md) para ter um conhecimento detalhado sobre a integração do SDK.</span><span class="sxs-lookup"><span data-stu-id="f8f98-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

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
