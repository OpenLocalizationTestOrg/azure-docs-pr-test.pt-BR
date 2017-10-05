---
title: "Como enviar notificações por push para iOS com Hubs de Notificação do Azure | Microsoft Docs"
description: "Neste tutorial, você aprenderá a usar os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo do iOS."
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
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="74934-104">Como enviar notificações por push para iOS com Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="74934-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="74934-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="74934-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="74934-106">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="74934-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="74934-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="74934-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="74934-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="74934-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="74934-109">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push para um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="74934-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="74934-110">Você criará um aplicativo do iOS em branco que recebe notificações por push usando o [APNs (Apple Push Notification Service)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="74934-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="74934-111">Ao finalizar, você poderá usar seu hub de notificação para transmitir notificações por push a todos os dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74934-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="74934-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="74934-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="74934-113">O código completo deste tutorial pode ser encontrado [no GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="74934-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="74934-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74934-114">Prerequisites</span></span>
<span data-ttu-id="74934-115">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="74934-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="74934-116">[versão 1.2.4 do SDK do iOS dos Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="74934-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="74934-117">Versão mais recente do [Xcode]</span><span class="sxs-lookup"><span data-stu-id="74934-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="74934-118">Um dispositivo compatível com o iOS 8 (ou versão posterior)</span><span class="sxs-lookup"><span data-stu-id="74934-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="74934-119">[Programa de Desenvolvedores de iOS](https://developer.apple.com/programs/) </span><span class="sxs-lookup"><span data-stu-id="74934-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="74934-120">Devido aos requisitos de configuração das notificações por push, você deve implantá-las e testá-las em um dispositivo iOS físico (iPhone ou iPad), em vez de usar o Simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="74934-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="74934-121">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre os Hubs de Notificação para aplicativos do iOS.</span><span class="sxs-lookup"><span data-stu-id="74934-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="74934-122">Configurar o Hub de Notificação para notificações por push do iOS</span><span class="sxs-lookup"><span data-stu-id="74934-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="74934-123">Esta seção mostra a criação de um novo hub de notificação e a configuração da autenticação com APNS usando o certificado push **.p12** que você criou.</span><span class="sxs-lookup"><span data-stu-id="74934-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="74934-124">Se você quiser usar um hub de notificação já criado, ignore a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="74934-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="74934-125">Clique no botão <b>Serviços de Notificação</b> na folha <b>Configurações</b> e selecione <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="74934-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="74934-126">Clique em <b>Carregar certificad</b>o e selecione o arquivo <b>.p12</b> exportado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74934-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="74934-127">Especifique também a senha correta.</span><span class="sxs-lookup"><span data-stu-id="74934-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="74934-128">Selecione o modo de <b>Área Restrita</b>, pois se trata de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="74934-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="74934-129">Use a <b>Produção</b> apenas se quiser enviar notificações por push aos usuários que adquiriram seu aplicativo na loja.</span><span class="sxs-lookup"><span data-stu-id="74934-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="74934-130">&emsp;&emsp;&emsp;&emsp;![Configurar APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="74934-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurar certificação do APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="74934-132">Seu hub de notificação agora está configurado para funcionar com o APNS e você tem as cadeias de conexão para registrar seu aplicativo e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="74934-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="74934-133">Conectar seu aplicativo do iOS aos Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="74934-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="74934-134">No Xcode, crie um novo projeto do iOS e selecione o modelo **Aplicativo de Modo de Exibição Único** .</span><span class="sxs-lookup"><span data-stu-id="74934-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - aplicativo de modo de exibição único][8]
    
2. <span data-ttu-id="74934-136">Ao definir as opções para o novo projeto, lembre-se de usar os mesmos **Nome do Produto** e **Identificador Organizacional** que você usou quando configurou a ID do pacote no portal de desenvolvimento da Apple.</span><span class="sxs-lookup"><span data-stu-id="74934-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - opções de projeto][11]
    
3. <span data-ttu-id="74934-138">Em **Destinos**, clique no nome do projeto, clique na guia **Configurações de Compilação** e expanda **Identidade de Assinatura de Código**. Depois, em **Depurar**, defina sua identidade de assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="74934-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="74934-139">Alterne **Níveis** de **Básico** para **Todos** e defina o **Perfil de Provisionamento** para o perfil de provisionamento que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74934-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="74934-140">Se você não vir o novo perfil de provisionamento que você criou no Xcode, tente atualizar os perfis da sua identidade de assinatura.</span><span class="sxs-lookup"><span data-stu-id="74934-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="74934-141">Clique em **Xcode** na barra de menus, em **Preferências**, na guia **Conta**, no botão **Exibir Detalhes**, em sua identidade de assinatura e depois clique no botão Atualizar no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="74934-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - perfil de provisionamento][9]
4. <span data-ttu-id="74934-143">Baixe a [versão 1.2.4 do SDK do iOS dos Serviços Móveis] e descompacte o arquivo.</span><span class="sxs-lookup"><span data-stu-id="74934-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="74934-144">No Xcode, clique com o botão direito do mouse no projeto e clique na opção **Adicionar Arquivos a** para adicionar a pasta **WindowsAzureMessaging.framework** ao seu projeto do Xcode.</span><span class="sxs-lookup"><span data-stu-id="74934-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="74934-145">Selecione **Copiar itens se necessário** e depois clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="74934-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="74934-146">No momento, o SDK de hubs de notificação não oferece suporte a bitcode em Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="74934-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="74934-147">Você deve definir **Habilitar Bitcode** como **Não** nas **Opções de Build** para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="74934-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Descompactar o SDK do Azure][10]
5. <span data-ttu-id="74934-149">Adicione ao projeto um novo arquivo de cabeçalho chamado `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="74934-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="74934-150">Esse arquivo conterá as constantes para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="74934-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="74934-151">Adicione as seguintes definições e substitua os espaços reservados da cadeia de caracteres literal pelo *nome do hub* e a *DefaultListenSharedAccessSignature* que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74934-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="74934-152">Abra o arquivo `AppDelegate.h` e adicione as seguintes diretivas de importação:</span><span class="sxs-lookup"><span data-stu-id="74934-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="74934-153">No `AppDelegate.m file`, adicione o código a seguir ao método `didFinishLaunchingWithOptions` de acordo com sua versão do iOS.</span><span class="sxs-lookup"><span data-stu-id="74934-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="74934-154">Esse código registra seu identificador de dispositivo nas APNs:</span><span class="sxs-lookup"><span data-stu-id="74934-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="74934-155">Para iOS 8:</span><span class="sxs-lookup"><span data-stu-id="74934-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="74934-156">Para versões do iOS anteriores a 8:</span><span class="sxs-lookup"><span data-stu-id="74934-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="74934-157">No mesmo arquivo, adicione os métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="74934-157">In the same file, add the following methods.</span></span> <span data-ttu-id="74934-158">Esse código conecta-se ao hub de notificação usando as informações de conexão que você especificou em HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="74934-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="74934-159">Esse código fornece o token do dispositivo ao hub de notificação para que o hub de notificação possa enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="74934-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="74934-160">No mesmo arquivo, adicione o seguinte método para exibir um **UIAlert** caso a notificação seja recebida enquanto o aplicativo estiver ativo:</span><span class="sxs-lookup"><span data-stu-id="74934-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="74934-161">Compile e execute o aplicativo no dispositivo para verificar se não há falhas.</span><span class="sxs-lookup"><span data-stu-id="74934-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="74934-162">Enviar notificações por push de teste</span><span class="sxs-lookup"><span data-stu-id="74934-162">Send test push notifications</span></span>
<span data-ttu-id="74934-163">Você pode testar o recebimento de notificações no aplicativo enviando notificações por push no [Portal do Azure] por meio da seção **Solução de problemas** na folha de hub (use a opção *Testar Enviar* ).</span><span class="sxs-lookup"><span data-stu-id="74934-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Portal do Azure - Testar Enviar][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="74934-165">(Opcional) Enviar notificações por push do aplicativo</span><span class="sxs-lookup"><span data-stu-id="74934-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="74934-166">Este exemplo de envio de notificações do aplicativo cliente é fornecido somente para fins de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="74934-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="74934-167">Como o exemplo exigirá a presença da `DefaultFullSharedAccessSignature` no aplicativo cliente, ele expõe seu hub de notificação ao risco de um usuário obter acesso para enviar notificações não autorizadas aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="74934-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="74934-168">Se você quer enviar notificações por push de dentro de um aplicativo, esta seção fornece um exemplo de como fazer isso usando a interface REST.</span><span class="sxs-lookup"><span data-stu-id="74934-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="74934-169">No Xcode, abra `Main.storyboard` e adicione os seguintes componentes da interface do usuário da biblioteca de objetos para permitir que o usuário envie notificações por push no aplicativo:</span><span class="sxs-lookup"><span data-stu-id="74934-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="74934-170">Um rótulo sem texto de rótulo.</span><span class="sxs-lookup"><span data-stu-id="74934-170">A label with no label text.</span></span> <span data-ttu-id="74934-171">Ele será usado para relatar erros no envio de notificações.</span><span class="sxs-lookup"><span data-stu-id="74934-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="74934-172">A propriedade **Lines** deve ser definida como **0** para que ela dimensione automaticamente as margens restritas à direita e à esquerda e na parte superior da exibição.</span><span class="sxs-lookup"><span data-stu-id="74934-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="74934-173">Um campo de texto com o texto de **Espaço Reservado** definido como **Inserir Mensagem de Notificação**.</span><span class="sxs-lookup"><span data-stu-id="74934-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="74934-174">Restrinja o campo logo abaixo do rótulo, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="74934-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="74934-175">Defina o Controlador de Exibição como o delegado de saída.</span><span class="sxs-lookup"><span data-stu-id="74934-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="74934-176">Um botão chamado **Enviar Notificação** restrito logo abaixo do campo de texto e no centro horizontal.</span><span class="sxs-lookup"><span data-stu-id="74934-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="74934-177">O modo de exibição deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="74934-177">The view should look as follows:</span></span>
     
     ![Designer do Xcode][32]
2. <span data-ttu-id="74934-179">[Adicione saídas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) para o rótulo e o campo de texto conectados à exibição e atualize a definição `interface` para dar suporte a `UITextFieldDelegate` e a `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="74934-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="74934-180">Adicione as três declarações de propriedade mostradas abaixo para ajudar a dar suporte a chamar à API REST e fazer a análise da resposta.</span><span class="sxs-lookup"><span data-stu-id="74934-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="74934-181">O arquivo ViewController.h deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="74934-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="74934-182">Abra `HubInfo.h` e adicione as constantes a seguir, que serão usadas para enviar notificações ao hub.</span><span class="sxs-lookup"><span data-stu-id="74934-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="74934-183">Substitua a cadeia de caracteres literal no espaço reservado pela cadeia de conexão *DefaultFullSharedAccessSignature* real.</span><span class="sxs-lookup"><span data-stu-id="74934-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="74934-184">Adicione as instruções `#import` a seguir ao arquivo `ViewController.h`.</span><span class="sxs-lookup"><span data-stu-id="74934-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="74934-185">Em `ViewController.m` , adicione o código a seguir à implementação da interface.</span><span class="sxs-lookup"><span data-stu-id="74934-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="74934-186">Esse código analisará a cadeia de conexão *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="74934-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="74934-187">Como mencionado na [referência da API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), essas informações analisadas serão usadas para gerar um token SaS para o cabeçalho de solicitação da **Autorização** .</span><span class="sxs-lookup"><span data-stu-id="74934-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="74934-188">Em `ViewController.m`, atualize o método `viewDidLoad` para analisar a cadeia de conexão quando a exibição for carregada.</span><span class="sxs-lookup"><span data-stu-id="74934-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="74934-189">além disso, adicione os métodos de utilitário, mostrados abaixo, à implementação da interface.</span><span class="sxs-lookup"><span data-stu-id="74934-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

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





1. <span data-ttu-id="74934-190">Em `ViewController.m`, adicione o código a seguir à implementação da interface para gerar o token de autorização de SaS que será fornecido no cabeçalho da **Autorização** , como mencionamos na [Referência da API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="74934-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
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
2. <span data-ttu-id="74934-191">Ctrl+arraste do botão **Enviar Notificação** para `ViewController.m` a fim de adicionar uma ação chamada **SendNotificationMessage** ao evento **Touch Down**.</span><span class="sxs-lookup"><span data-stu-id="74934-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="74934-192">Atualize o método com o código a seguir para enviar a notificação usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="74934-192">Update method with the following code to send the notification using the REST API.</span></span>
   
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
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
3. <span data-ttu-id="74934-193">Em `ViewController.m`, adicione o método de representante a seguir para dar suporte ao fechamento do teclado para o campo de texto.</span><span class="sxs-lookup"><span data-stu-id="74934-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="74934-194">Use Ctrl + arrastar do campo de texto para o ícone do Controlador de Exibição no designer de interface para definir o controlador de exibição como o representante de saída.</span><span class="sxs-lookup"><span data-stu-id="74934-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="74934-195">Em `ViewController.m`, adicione os métodos de representante a seguir para dar suporte à análise da resposta usando `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="74934-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
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
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="74934-196">Compile o projeto e verifique se não há erros.</span><span class="sxs-lookup"><span data-stu-id="74934-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="74934-197">Se você encontrar um erro de compilação em Xcode7 sobre o suporte de bitcode, altere as **Configurações de Build** > **Habilitar Bitcode (ENABLE_BITCODE)** para **NO** no Xcode.</span><span class="sxs-lookup"><span data-stu-id="74934-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="74934-198">No momento, o SDK de Hubs de Notificação não oferece suporte a bitcode.</span><span class="sxs-lookup"><span data-stu-id="74934-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="74934-199">Você encontrará todas as cargas de notificação possíveis no [Guia de programação de notificação local e por push]da Apple.</span><span class="sxs-lookup"><span data-stu-id="74934-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="74934-200">Como verificar se o aplicativo pode receber notificações por push</span><span class="sxs-lookup"><span data-stu-id="74934-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="74934-201">Para testar as notificações por push no iOS, você deve implantar o aplicativo em um dispositivo iOS físico.</span><span class="sxs-lookup"><span data-stu-id="74934-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="74934-202">Não é possível enviar notificações por push da Apple com o Simulador do iOS.</span><span class="sxs-lookup"><span data-stu-id="74934-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="74934-203">Execute o aplicativo e verifique se o registro foi bem-sucedido e pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="74934-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Teste de registro de notificação por push de aplicativo do iOS][33]
2. <span data-ttu-id="74934-205">Você pode enviar uma notificação por push de teste do [Portal do Azure], conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="74934-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="74934-206">Se você adicionou o código para enviar notificações por push no aplicativo, toque dentro do campo de texto para inserir uma mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="74934-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="74934-207">Em seguida, pressione o botão **Enviar** no teclado ou o botão **Enviar Notificação** no modo de exibição para enviar a mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="74934-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Teste de envio de notificação por push de aplicativo do iOS][34]
3. <span data-ttu-id="74934-209">A notificação por push é enviada a todos os dispositivos que estão registrados para receber as notificações do Hub de Notificação específico.</span><span class="sxs-lookup"><span data-stu-id="74934-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Teste de recebimento de notificação por push de aplicativo do iOS][35]

## <a name="next-steps"></a><span data-ttu-id="74934-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74934-211">Next steps</span></span>
<span data-ttu-id="74934-212">Neste exemplo simples, você enviou notificações por push a todos os seus dispositivos iOS registrados.</span><span class="sxs-lookup"><span data-stu-id="74934-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="74934-213">Como próxima etapa do aprendizado, sugerimos que você vá para o tutorial [Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET] , que o orientará na criação de um back-end para enviar notificações por push usando marcas.</span><span class="sxs-lookup"><span data-stu-id="74934-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="74934-214">Se desejar segmentar os usuários por grupos de interesse, você também poderá ir para o tutorial [Usar Hubs de Notificação para enviar as últimas notícias] .</span><span class="sxs-lookup"><span data-stu-id="74934-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="74934-215">Para obter informações gerais sobre os Hubs de Notificação, confira [Diretrizes dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="74934-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="74934-216">[versão 1.2.4 do SDK do iOS dos Serviços Móveis]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="74934-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="74934-217">[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="74934-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="74934-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="74934-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="74934-219">[Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="74934-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="74934-220">[Usar Hubs de Notificação para enviar as últimas notícias]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="74934-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="74934-221">[Guia de programação de notificação local e por push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="74934-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="74934-222">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="74934-222">[Azure Portal]: https://portal.azure.com</span></span>
