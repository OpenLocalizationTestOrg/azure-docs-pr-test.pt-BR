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
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Introdução ao Azure Mobile Engagement para Aplicativos Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo e como toosend envio os usuários toosegmented de notificações de um aplicativo do Android.
Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement. Nele, você cria um aplicativo Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).

## <a name="prerequisites"></a>Pré-requisitos
Concluir este tutorial requer Olá [Android Developer Tools](https://developer.android.com/sdk/index.html), que inclui o ambiente de desenvolvimento integrado do Android Studio hello e plataforma Android mais recentes de saudação.

Ela também exige Olá [Android SDK do Mobile Engagement](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete neste tutorial, você precisa de uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Configurar o Mobile Engagement para seu aplicativo Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push. Você pode criar um aplicativo básico com a integração do Android Studio toodemonstrate hello.

documentação de integração completa Olá pode ser encontrada no hello [integração Android SDK do Mobile Engagement](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Criar um projeto Android
1. Iniciar **Android Studio**e no pop-up hello, selecione **iniciar um novo projeto do Android Studio**.

    ![][1]
2. Forneça um nome de aplicativo e um domínio da empresa. Anote o que você está preenchendo, porque precisará disso posteriormente. Clique em **Avançar**.

    ![][2]
3. Selecione o fator de forma de destino hello e nível de API e, em seguida, clique em **próximo**.

   > [!NOTE]
   > O Mobile Engagement requer nível mínimo de API de 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Selecione **atividade em branco** aqui, que é a única tela hello para este aplicativo e clique em **próximo**.

    ![][4]
5. Finalmente, mantenha os padrões de saudação como está e clique em **concluir**.

    ![][5]

Agora, o Android Studio cria Olá aplicativo de demonstração em que podemos integrar Mobile Engagement.

### <a name="include-hello-sdk-library-in-your-project"></a>Incluir a biblioteca de saudação do SDK em seu projeto
1. Baixar Olá [Android SDK do Mobile Engagement](https://aka.ms/vq9mfn).
2. Extrai Olá arquivo tooa morto em seu computador.
3. Identificar hello. jar biblioteca para a versão atual de saudação desse SDK e copiá-lo toohello da área de transferência.

      ![][6]
4. Navegue toohello **projeto** seção (1) e cole. Olá JAR na pasta de bibliotecas de saudação (2).

      ![][7]
5. biblioteca de saudação tooload, projeto de saudação de sincronização.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Conecte-se o seu back-end do aplicativo tooMobile contrato com hello cadeia de caracteres de Conexão
1. Saudação de copiar linhas de código a seguir para criação de atividade de saudação (deve ser feito apenas em um local do seu aplicativo, geralmente atividade principal da saudação). Para este aplicativo de exemplo, abra Olá MainActivity em src -> principal -> pasta java e adicione Olá seguinte:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Resolva referências Olá pressionando Alt + Enter ou adicionando Olá seguindo as instruções de importação:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Voltar toohello Portal clássico do Azure em seu aplicativo **informações de Conexão** Olá página e cópia **cadeia de caracteres de Conexão**.

      ![][9]
4. Cole Olá `setConnectionString` parâmetro, substituindo a cadeia de caracteres inteira Olá Olá código a seguir mostrada:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Adicionar permissões e uma declaração de serviço
1. Adicionar toohello essas permissões manifest. XML do projeto imediatamente antes ou após Olá `<application>` marca:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare Olá serviço de agente, adicione este código entre hello `<application>` e `</application>` marcas:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. No código de saudação colados, substitua `"<Your application name>"` no rótulo hello, que é exibido no hello **configurações** onde você pode ver os serviços em execução no dispositivo de saudação do menu. Por exemplo você pode adicionar palavra hello "Serviço" nesse rótulo.

### <a name="send-a-screen-toomobile-engagement"></a>Enviar um tooMobile tela Contrato
toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.

Vá muito**MainActivity.java** e adicione Olá tooreplace hello classe base a seguir **MainActivity** muito**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Se sua classe base não for *atividade*, consulte [avançado Android Reporting](mobile-engagement-android-advanced-reporting.md) como tooinherit de classes diferentes.
>
>

Comentar Olá linha para este cenário de exemplo simples a seguir:

    // setSupportActionBar(toolbar);

Se você quiser Olá tookeep `ActionBar` em seu aplicativo, consulte [avançado Android Reporting](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Habilitar notificações por push e mensagens no aplicativo
Durante uma campanha, o Mobile Engagement permite interagir e acessar em REACH seus usuários com notificações por push e mensagens no aplicativo. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seção a seguir define o seu aplicativo tooreceive-los.

### <a name="copy-sdk-resources-in-your-project"></a>Copiar recursos de SDK em seu projeto
1. Navegue Olá de conteúdo e cópia de download SDK do back tooyour **res** pasta.

    ![][10]
2. Voltar tooAndroid Studio, selecione Olá **principal** diretório de arquivos de projeto e, em seguida, cole-o projeto de tooyour tooadd Olá recursos.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Próximas etapas
Vá muito[SDK do Android](mobile-engagement-android-sdk-overview.md) tooget detalhadas conhecimento sobre Olá integração SDK.

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
