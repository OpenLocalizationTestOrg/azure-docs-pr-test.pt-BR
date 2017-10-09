---
title: "aaaSending tooiOS de notificações por push com Hubs de notificação do Azure | Microsoft Docs"
description: "Neste tutorial, você aprenderá como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure."
services: notification-hubs
documentationcenter: ios
keywords: "notificação por push, notificações por push, notificações por push do ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="c12f8-104">TooiOS envio de notificações por push com Hubs de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="c12f8-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c12f8-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c12f8-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="c12f8-106">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c12f8-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c12f8-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c12f8-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c12f8-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="c12f8-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="c12f8-109">Este tutorial mostra como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c12f8-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="c12f8-110">Você criará um aplicativo iOS em branco que recebe notificações por push usando Olá [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="c12f8-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="c12f8-111">Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c12f8-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c12f8-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c12f8-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c12f8-113">Olá concluída de código para este tutorial pode ser encontrado [no GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="c12f8-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c12f8-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c12f8-114">Prerequisites</span></span>
<span data-ttu-id="c12f8-115">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c12f8-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="c12f8-116">[serviços móveis iOS SDK versão 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="c12f8-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="c12f8-117">Versão mais recente do [Xcode]</span><span class="sxs-lookup"><span data-stu-id="c12f8-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="c12f8-118">Um dispositivo compatível com o iOS 8 (ou versão posterior)</span><span class="sxs-lookup"><span data-stu-id="c12f8-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="c12f8-119">[Programa de Desenvolvedores de iOS](https://developer.apple.com/programs/) </span><span class="sxs-lookup"><span data-stu-id="c12f8-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c12f8-120">Devido aos requisitos de configuração para notificações por push, você deve implantar e testar notificações por push em um dispositivo físico iOS (iPhone ou iPad) em vez da saudação simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="c12f8-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="c12f8-121">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre os Hubs de Notificação para aplicativos do iOS.</span><span class="sxs-lookup"><span data-stu-id="c12f8-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="c12f8-122">Configurar o Hub de Notificação para notificações por push do iOS</span><span class="sxs-lookup"><span data-stu-id="c12f8-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="c12f8-123">Esta seção orienta você pela criação de um novo hub de notificação e configurar a autenticação com APNS usando Olá **. p12** certificado de push que você criou.</span><span class="sxs-lookup"><span data-stu-id="c12f8-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="c12f8-124">Se você quiser toouse um hub de notificação que você já tiver criado, você poderá ignorar toostep 5.</span><span class="sxs-lookup"><span data-stu-id="c12f8-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="c12f8-125">Clique Olá <b>Notification Services</b> botão Olá <b>configurações</b> folha, selecione <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="c12f8-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="c12f8-126">Clique em <b>carregar certificado</b> e selecione hello <b>. p12</b> arquivo que você exportou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c12f8-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="c12f8-127">Verifique se que você também especificar a senha correta da saudação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="c12f8-128">Certifique-se de que tooselect <b>Sandbox</b> modo como isso é para o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c12f8-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="c12f8-129">Somente use Olá <b>produção</b> se você quiser toosend toousers de notificações de envio que compraram o aplicativo da loja de saudação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="c12f8-130">&emsp;&emsp;&emsp;&emsp;![Configurar APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="c12f8-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurar certificação do APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="c12f8-132">O hub de notificação agora está configurado toowork com APNS e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="c12f8-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="c12f8-133">Conectar seu aplicativo de iOS tooNotification Hubs</span><span class="sxs-lookup"><span data-stu-id="c12f8-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="c12f8-134">No Xcode, crie um novo projeto de iOS e selecione Olá **único aplicativo de exibição** modelo.</span><span class="sxs-lookup"><span data-stu-id="c12f8-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - aplicativo de modo de exibição único][8]
    
2. <span data-ttu-id="c12f8-136">Ao definir opções de saudação para seu novo projeto, certifique-se de toouse Olá mesmo **nome do produto** e **identificador de organização** que você usou quando você configurado anteriormente ID do pacote Olá Olá desenvolvedor Apple Portal.</span><span class="sxs-lookup"><span data-stu-id="c12f8-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - opções de projeto][11]
    
3. <span data-ttu-id="c12f8-138">Em **destinos**, clique em seu nome de projeto Olá **configurações da compilação** guia e expanda **a identidade de assinatura de código**e, em seguida, em **depurar**, defina sua identidade de assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="c12f8-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="c12f8-139">Ativar/desativar **níveis** de **básica** muito**todos os**e defina **perfil de provisionamento de** toohello provisionamento de perfil que você criou anteriormente .</span><span class="sxs-lookup"><span data-stu-id="c12f8-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="c12f8-140">Se você não vir Olá provisionamento novo perfil que você criou no Xcode, tente atualizar perfis Olá para sua identidade de assinatura.</span><span class="sxs-lookup"><span data-stu-id="c12f8-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="c12f8-141">Clique em **Xcode** na barra de menus do hello, clique em **preferências**, clique em Olá **conta** , clique em Olá **exibir detalhes** , clique em seu assinatura de identidade e, em seguida, clique botão de atualização de saudação no canto inferior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - perfil de provisionamento][9]
4. <span data-ttu-id="c12f8-143">Baixar Olá [serviços móveis iOS SDK versão 1.2.4] e descompacte o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="c12f8-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="c12f8-144">No Xcode, clique com o botão direito e clique em Olá **adicionar arquivos ao** Olá de tooadd opção **WindowsAzureMessaging.framework** projeto de Xcode tooyour pasta.</span><span class="sxs-lookup"><span data-stu-id="c12f8-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="c12f8-145">Selecione **Copiar itens se necessário** e depois clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c12f8-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c12f8-146">hubs de notificação Olá SDK não suporta atualmente bitcode no Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="c12f8-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="c12f8-147">Você deve definir **habilitar Bitcode** muito**não** em Olá **opções de compilação** para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c12f8-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Descompactar o SDK do Azure][10]
5. <span data-ttu-id="c12f8-149">Adicione um novo projeto de tooyour de arquivo de cabeçalho chamado `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="c12f8-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="c12f8-150">Esse arquivo manterá constantes Olá para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="c12f8-151">Adicionar Olá definições a seguir e substitua os espaços reservados literal de cadeia de caracteres hello com seu *nome do hub* e hello *DefaultListenSharedAccessSignature* que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c12f8-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="c12f8-152">Abra seu `AppDelegate.h` adicionar de arquivo hello diretivas de importação a seguir:</span><span class="sxs-lookup"><span data-stu-id="c12f8-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="c12f8-153">No seu `AppDelegate.m file`, adicionar Olá Olá código a seguir `didFinishLaunchingWithOptions` método com base na sua versão do iOS.</span><span class="sxs-lookup"><span data-stu-id="c12f8-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="c12f8-154">Esse código registra seu identificador de dispositivo nas APNs:</span><span class="sxs-lookup"><span data-stu-id="c12f8-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="c12f8-155">Para iOS 8:</span><span class="sxs-lookup"><span data-stu-id="c12f8-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="c12f8-156">Para too8 anteriores do iOS versões:</span><span class="sxs-lookup"><span data-stu-id="c12f8-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="c12f8-157">Em Olá mesmo arquivo, adicione Olá métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c12f8-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="c12f8-158">Esse código conecta-se usando as informações de conexão de saudação especificado em HubInfo.h de hub de notificação toohello.</span><span class="sxs-lookup"><span data-stu-id="c12f8-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="c12f8-159">Ele oferece hub de notificação de token toohello Olá dispositivo, em seguida, para que hello hub de notificação pode enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="c12f8-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="c12f8-160">Em Olá mesmo arquivo, adicione Olá toodisplay do método a seguir um **UIAlert** se notificação de saudação for recebida, enquanto o aplicativo hello está ativo:</span><span class="sxs-lookup"><span data-stu-id="c12f8-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="c12f8-161">Compilar e executar o aplicativo hello em seu tooverify de dispositivo que não há nenhuma falha.</span><span class="sxs-lookup"><span data-stu-id="c12f8-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="c12f8-162">Enviar notificações por push de teste</span><span class="sxs-lookup"><span data-stu-id="c12f8-162">Send test push notifications</span></span>
<span data-ttu-id="c12f8-163">Você pode testar a receber notificações em seu aplicativo por meio do envio de notificações por push em Olá [Portal do Azure] via Olá **solução de problemas** seção na folha de hub hello (use Olá *deenviodeteste* opção).</span><span class="sxs-lookup"><span data-stu-id="c12f8-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portal do Azure - Testar Enviar][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="c12f8-165">(Opcional) Enviar notificações por push do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="c12f8-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c12f8-166">Este exemplo de envio de notificações do aplicativo de cliente de saudação é fornecido para fins de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="c12f8-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="c12f8-167">Uma vez que isso exigirá Olá `DefaultFullSharedAccessSignature` toobe presente no aplicativo de cliente hello, ele expõe o risco de toohello do hub de notificação que um usuário pode obter acesso não autorizado de toosend notificações tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="c12f8-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="c12f8-168">Se você quiser notificações por push de toosend de dentro de um aplicativo, esta seção fornece um exemplo de como toodo Olá isso usando a interface REST.</span><span class="sxs-lookup"><span data-stu-id="c12f8-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="c12f8-169">No Xcode, abra `Main.storyboard` e adicione Olá seguindo os componentes de interface do usuário da saudação objeto biblioteca tooallow Olá usuário toosend notificações por push no aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="c12f8-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="c12f8-170">Um rótulo sem texto de rótulo.</span><span class="sxs-lookup"><span data-stu-id="c12f8-170">A label with no label text.</span></span> <span data-ttu-id="c12f8-171">Ele será usado tooreport erros no envio de notificações.</span><span class="sxs-lookup"><span data-stu-id="c12f8-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="c12f8-172">Olá **linhas** propriedade deve ser definida muito**0** para que ele será dimensionado automaticamente toohello restrita direita e as margens esquerdas e superior de saudação do modo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="c12f8-173">Um campo de texto com **espaço reservado** texto definido muito**Inserir mensagem de notificação**.</span><span class="sxs-lookup"><span data-stu-id="c12f8-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="c12f8-174">Restringir o campo Olá logo abaixo rótulo Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c12f8-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="c12f8-175">Defina Olá View Controller como representante de loja hello.</span><span class="sxs-lookup"><span data-stu-id="c12f8-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="c12f8-176">Um botão chamado **enviar notificação** restrita abaixo de campo de texto de saudação e no Centro de saudação horizontal.</span><span class="sxs-lookup"><span data-stu-id="c12f8-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="c12f8-177">exibição de saudação se assemelhar ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c12f8-177">hello view should look as follows:</span></span>
     
     ![Designer do Xcode][32]
2. <span data-ttu-id="c12f8-179">[Adicionar saídas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de campo de rótulo e o texto de saudação conectado seu modo de exibição e atualizar seu `interface` definição toosupport `UITextFieldDelegate` e `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="c12f8-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="c12f8-180">Adicione declarações de propriedade três Olá mostradas abaixo toohelp suporte chamando Olá API REST e analisar a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="c12f8-181">O arquivo ViewController.h deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c12f8-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="c12f8-182">Abra `HubInfo.h` e adicione Olá constantes que serão usadas para enviar o hub de tooyour notificações a seguir.</span><span class="sxs-lookup"><span data-stu-id="c12f8-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="c12f8-183">Substitua o literal de cadeia de espaço reservado de saudação com seu real *DefaultFullSharedAccessSignature* cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="c12f8-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="c12f8-184">Adicione o seguinte Olá `#import` instruções tooyour `ViewController.h` arquivo.</span><span class="sxs-lookup"><span data-stu-id="c12f8-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="c12f8-185">No `ViewController.m` adicionar Olá implementação de interface toohello de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c12f8-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="c12f8-186">Esse código analisará a cadeia de conexão *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="c12f8-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="c12f8-187">Conforme mencionado em Olá [referência da API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), essas informações analisadas serão toogenerate usado um token SaS para Olá **autorização** cabeçalho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="c12f8-188">Em `ViewController.m`, Olá atualização `viewDidLoad` método tooparse Olá conexão cadeia de caracteres quando a exibição Olá carrega.</span><span class="sxs-lookup"><span data-stu-id="c12f8-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="c12f8-189">Também adicionar métodos de utilitário hello, mostrados abaixo, a implementação de interface toohello.</span><span class="sxs-lookup"><span data-stu-id="c12f8-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="c12f8-190">Em `ViewController.m`, adicionar Olá após código toohello interface implementação toogenerate Olá autorização token SaS que será fornecido em hello **autorização** cabeçalho, como mencionado na Olá [API REST Referência](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="c12f8-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="c12f8-191">CTRL + arrastar de Olá **enviar notificação** botão muito`ViewController.m` tooadd uma ação chamada **SendNotificationMessage** para Olá **toque para baixo** eventos.</span><span class="sxs-lookup"><span data-stu-id="c12f8-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="c12f8-192">Método de atualização com hello notificação de saudação do código toosend usando Olá API REST a seguir.</span><span class="sxs-lookup"><span data-stu-id="c12f8-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="c12f8-193">Em `ViewController.m`, adicionar Olá Delegar método toosupport teclado Olá para o campo de texto de saudação de fechamento a seguir.</span><span class="sxs-lookup"><span data-stu-id="c12f8-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="c12f8-194">CTRL + arrastar Olá texto campo toohello View Controller do ícone de no Olá Olá de designer tooset interface exibir controlador como representante de loja hello.</span><span class="sxs-lookup"><span data-stu-id="c12f8-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="c12f8-195">Em `ViewController.m`, adicione a seguinte Olá delegar a resposta de análise Olá métodos toosupport usando `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="c12f8-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="c12f8-196">Criar projeto hello e verifique se não há nenhum erro.</span><span class="sxs-lookup"><span data-stu-id="c12f8-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="c12f8-197">Se você encontrar um erro de compilação em Xcode7 sobre o suporte de bitcode, você deve alterar Olá **configurações da compilação** > **Bitcode habilitar (ENABLE_BITCODE)** muito**não** no Xcode.</span><span class="sxs-lookup"><span data-stu-id="c12f8-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="c12f8-198">Olá SDK de Hubs de notificação atualmente não dá suporte para bitcode.</span><span class="sxs-lookup"><span data-stu-id="c12f8-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="c12f8-199">Você encontrará todas as cargas de notificações possíveis Olá Olá Apple [Local e o guia de programação de notificação por Push].</span><span class="sxs-lookup"><span data-stu-id="c12f8-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="c12f8-200">Como verificar se o aplicativo pode receber notificações por push</span><span class="sxs-lookup"><span data-stu-id="c12f8-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="c12f8-201">notificações de push tootest no iOS, você deve implantar o dispositivo de e / s físicas Olá aplicativo tooa.</span><span class="sxs-lookup"><span data-stu-id="c12f8-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="c12f8-202">Você não pode enviar notificações de envio por push da Apple usando Olá simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="c12f8-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="c12f8-203">Execute o aplicativo hello e verifique que o registro for bem-sucedido e, em seguida, pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c12f8-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Teste de registro de notificação por push de aplicativo do iOS][33]
2. <span data-ttu-id="c12f8-205">Você pode enviar uma notificação por push de teste do hello [Portal do Azure], conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="c12f8-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="c12f8-206">Se você adicionou o código para enviar notificações por push no aplicativo hello, toque em tooenter de campo de texto de saudação uma mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="c12f8-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="c12f8-207">Pressione Olá **enviar** botão no teclado hello ou Olá **enviar notificação** botão na mensagem de notificação de saudação do hello exibição toosend.</span><span class="sxs-lookup"><span data-stu-id="c12f8-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Teste de envio de notificação por push de aplicativo do iOS][34]
3. <span data-ttu-id="c12f8-209">Olá push notificação é enviada tooall dispositivos registrado tooreceive notificações de saudação do hello Hub de notificação específica.</span><span class="sxs-lookup"><span data-stu-id="c12f8-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Teste de recebimento de notificação por push de aplicativo do iOS][35]

## <a name="next-steps"></a><span data-ttu-id="c12f8-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c12f8-211">Next steps</span></span>
<span data-ttu-id="c12f8-212">Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos iOS registrados.</span><span class="sxs-lookup"><span data-stu-id="c12f8-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="c12f8-213">Sugerimos como uma próxima etapa do aprendizado continuar toohello [notificação Hubs notificar os usuários do Azure para iOS com o back-end .NET] tutorial, que irá orientá-lo na criação de um envio por push do back-end toosend notificações usando marcas.</span><span class="sxs-lookup"><span data-stu-id="c12f8-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="c12f8-214">Se você quiser toosegment os usuários, grupos de interesse, você poderá mover além no toohello [toosend de Hubs de notificação de uso últimas notícias] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c12f8-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="c12f8-215">Para obter informações gerais sobre os Hubs de Notificação, confira [Diretrizes dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="c12f8-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[serviços móveis iOS SDK versão 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[notificação Hubs notificar os usuários do Azure para iOS com o back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local e o guia de programação de notificação por Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal do Azure]: https://portal.azure.com
