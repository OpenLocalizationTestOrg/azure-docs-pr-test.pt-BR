---
title: "aaaAzure notificação Hubs seguro Push"
description: "Saiba como toosend segura notificações por push no Azure. Exemplos de código escritos em c# usando Olá API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Push Seguro dos Hubs de Notificação do Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.

Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello. Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo de cliente hello e back-end de aplicativo hello.

Em um nível alto, o fluxo de saudação é o seguinte:

1. Olá aplicativo back-end:
   * Armazena uma carga segura no banco de dados de back-end.
   * Envia a ID de saudação do dispositivo toohello notificação (nenhuma informação de segurança é enviada).
2. Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:
   * dispositivo Olá contata Olá back-end solicitante Olá carga de segurança.
   * aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.

É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon. Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token. Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, hello aplicativo de dispositivo, ao receber a notificação de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo. aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.

Este tutorial seguro Push mostra como toosend uma notificação por push com segurança. Olá tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro.

> [!NOTE]
> Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Além disso, observe que o Windows Phone 8.1 requer credenciais do Windows (não Windows Phone) e tarefas em segundo plano não funcionam no Windows Phone 8.0 ou Silverlight 8.1. Para aplicativos da Windows Store, você pode receber notificações por meio de uma tarefa em segundo plano apenas se o aplicativo hello está habilitada na tela de bloqueio (clique na caixa de seleção Olá Olá Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Modificar Olá projeto do Windows Phone
1. Em Olá **NotifyUserWindowsPhone** de projeto, adicione Olá tarefa em segundo plano por push de saudação do código tooApp.xaml.cs tooregister a seguir. Adicionar Olá a seguinte linha de código final Olá Olá `OnLaunched()` método:
   
        RegisterBackgroundTask();
2. Ainda em App.xaml.cs, adicionar Olá código a seguir imediatamente após Olá `OnLaunched()` método:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Adicione o seguinte Olá `using` instruções no topo de saudação do arquivo App.xaml.cs-Olá:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. De saudação **arquivo** no Visual Studio, clique em **Salvar tudo**.

## <a name="create-hello-push-background-component"></a>Criar hello Push componente do plano de fundo
Olá próxima etapa é o componente de plano de fundo toocreate Olá por push.

1. No Gerenciador de soluções, clique com botão direito nó de nível superior de saudação de solução de saudação (**solução SecurePush** nesse caso), em seguida, clique em **adicionar**, em seguida, clique em **novo projeto**.
2. Expanda **Aplicativos da Loja** e clique em **Aplicativos do Windows Phone** e em **Componente do Tempo de Execução do Windows (Windows Phone)**. Projeto de saudação do nome **PushBackgroundComponent**e, em seguida, clique em **Okey** toocreate projeto de saudação.
   
    ![][12]
3. No Gerenciador de soluções, clique com botão direito Olá **PushBackgroundComponent (Windows Phone 8.1)** projeto e, em seguida, clique em **adicionar**, em seguida, clique em **classe**. Nomeie a nova classe de saudação **PushBackgroundTask.cs**. Clique em **adicionar** toogenerate classe de saudação.
4. Substitua todo o conteúdo do Olá Olá **PushBackgroundComponent** definição de namespace com hello código a seguir, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade do back-end Olá obtido ao implantar o back-end:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. No Gerenciador de soluções, clique com botão direito Olá **PushBackgroundComponent (Windows Phone 8.1)** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
6. No lado esquerdo do hello, clique em **Online**.
7. Em Olá **pesquisa** , digite **cliente Http**.
8. Na lista de resultados de saudação, clique em **bibliotecas de cliente HTTP Microsoft**e, em seguida, clique em **instalar**. Concluir a instalação de saudação.
9. Em Olá NuGet **pesquisa** , digite **Json.net**. Instalar Olá **Json.NET** pacote e a janela do Gerenciador de pacotes do NuGet Olá fechar.
10. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **PushBackgroundTask.cs** arquivo:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. No Solution Explorer, no hello **NotifyUserWindowsPhone (Windows Phone 8.1)** de projeto, clique no **referências**, em seguida, clique em **adicionar referência...** . Na caixa de diálogo de Gerenciador de referências hello, caixa de seleção Olá Avançar muito**PushBackgroundComponent**e, em seguida, clique em **Okey**.
12. No Solution Explorer, clique duas vezes em **Package. appxmanifest** em Olá **NotifyUserWindowsPhone (Windows Phone 8.1)** projeto. Em **notificações**, defina **compatíveis com notificação do sistema** muito**Sim**.
    
    ![][3]
13. Ainda no **Package. appxmanifest**, clique em Olá **declarações** menu superior hello. Em Olá **Available Declarations** lista suspensa, clique em **tarefas em segundo plano**e, em seguida, clique em **adicionar**.
14. Em **Package.appxmanifest**, em **Propriedades**, marque **Notificação por push**.
15. Em **Package. appxmanifest**, em **configurações do aplicativo**, tipo **PushBackgroundComponent.PushBackgroundTask** em Olá **ponto de entrada** campo.
    
    ![][13]
16. De saudação **arquivo** menu, clique em **Salvar tudo**.

## <a name="run-hello-application"></a>Executar Olá aplicativo
toorun Olá aplicativo, Olá a seguir:

1. No Visual Studio, executar Olá **AppBackend** aplicativo de API da Web. Uma página da Web do ASP.NET é exibida.
2. No Visual Studio, executar Olá **NotifyUserWindowsPhone (Windows Phone 8.1)** aplicativo do Windows Phone. emulador do Windows Phone Olá é executado e carrega o aplicativo hello automaticamente.
3. Em Olá **NotifyUserWindowsPhone** aplicativo da interface do usuário, insira um nome de usuário e senha. Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.
4. Em Olá **NotifyUserWindowsPhone** aplicativo da interface do usuário, clique em **efetuar login e registrar**. Em seguida, clique em **Enviar push**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
