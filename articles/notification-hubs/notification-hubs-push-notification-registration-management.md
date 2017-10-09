---
title: aaaRegistration gerenciamento
description: "Este tópico explica como os dispositivos de tooregister com hubs de notificação na ordem tooreceive notificações de envio."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Gerenciamento de registros
## <a name="overview"></a>Visão geral
Este tópico explica como os dispositivos de tooregister com hubs de notificação na ordem tooreceive notificações de envio. tópico de saudação descreve os registros em um nível alto, em seguida, apresenta Olá dois padrões de principal para o registro de dispositivos: registro de dispositivo Olá diretamente o hub de notificação toohello e registro através de um back-end do aplicativo. 

## <a name="what-is-device-registration"></a>O que é o registro de dispositivos
O registro de dispositivos com um Hub de Notificação é realizado usando um **Registro** ou uma **Instalação**.

#### <a name="registrations"></a>Registros
Um registro associa Olá identificador de serviço de notificação de plataforma (PNS) para um dispositivo com marcas e, possivelmente, um modelo. Olá PNS identificador pode ser um ChannelURI, token do dispositivo ou id de registro do GCM. Marcas são usadas tooroute notificações toohello o conjunto correto de identificadores de dispositivo. Para saber mais, veja [Expressões de marca e de roteamento](notification-hubs-tags-segment-push-message.md). Os modelos são usados tooimplement por registro transformação. Para saber mais, veja [Modelos](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Instalações
Uma instalação é um registro aprimorado que inclui um conjunto de propriedades relacionadas ao envio por push. É Olá tooregistering abordagem melhor e mais recentes em seus dispositivos. No entanto, não há suporte pelo SDK do .NET do lado do cliente ([SDK do Hub de Notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) até o momento.  Isso significa que se você estiver registrando do próprio dispositivo de cliente hello, você teria Olá toouse [API de REST de Hubs de notificação](https://msdn.microsoft.com/library/mt621153.aspx) abordagem toosupport instalações. Se você estiver usando um serviço de back-end, você deve ser capaz de toouse [SDK do Hub de notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Olá seguem algumas instalações de toousing principais vantagens:

* A criação ou atualização de uma instalação é totalmente idempotente. Portanto, você pode repetir sem as preocupações com registros duplicados.
* modelo de instalação Olá torna fácil toodo individuais envios por push - direcionando o dispositivo específico. Uma marca de sistema **"$InstallationId: [installationId]"** é adicionada automaticamente com cada registro com base em instalação. Assim você pode chamar um tootarget de marca toothis enviar um dispositivo específico sem ter que toodo qualquer codificação adicional.
* Usar instalações também permite que você toodo registro parcial atualizações. Olá atualização parcial de uma instalação é solicitada com um método de PATCH usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902). Isso é particularmente útil quando você quiser tooupdate marcas no registro de saudação. Você não tem toopull para baixo de registro todo hello e reenviar a todas as marcas de saudação anterior novamente.

Uma instalação pode conter Olá Olá propriedades a seguir. Para obter uma lista completa de saudação instalação propriedades, consulte [criar ou substituir uma instalação com a API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [propriedades de instalação](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para hello.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



É importante toonote que instalações por padrão e os registros não expiram.

Os registros e instalações devem conter um identificador PNS válido para cada dispositivo/canal. Como os identificadores PNS só podem ser obtidos em um aplicativo cliente no dispositivo hello, um padrão é tooregister diretamente no dispositivo com o aplicativo de cliente hello. Olá outro lado, as considerações de segurança e lógica de negócios relacionam tootags pode exigir o registro de dispositivos toomanage no back-end do aplicativo hello. 

#### <a name="templates"></a>Modelos
Se você quiser toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md), a instalação do dispositivo Olá também manter todos os modelos associados a esse dispositivo em JSON formatar (veja o exemplo acima). Olá nomes de modelo ajuda destino modelos diferentes para Olá mesmo dispositivo.

Observe que cada nome de modelo mapeia tooa corpo de modelo e um conjunto opcional de marcas. Além disso, cada plataforma pode ter propriedades adicionais de modelo. Para Windows Store (usando WNS) e Windows Phone 8 (usando MPNS), um conjunto adicional de cabeçalhos pode ser parte do modelo de saudação. No caso de saudação de APNs, você pode definir uma expressão de modelo constante ou tooa um tooeither de propriedade de expiração. Para obter uma lista completa de saudação instalação propriedades, consulte [criar ou substituir uma instalação com REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tópico.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Blocos secundários para aplicativos da Windows Store
Para aplicativos de cliente da Windows Store, notificações de enviadas é toosecondary blocos mesmo Olá como enviá-los toohello principal. Isso também tem suporte nas instalações. Observe que o secundários blocos têm um ChannelUri diferente, quais Olá SDK em seu aplicativo cliente trata transparente.

Olá SecondaryTiles dicionário usa Olá TileId mesmo que é usado toocreate Olá SecondaryTiles objeto em seu aplicativo da Windows Store.
Como com hello primário ChannelUri, ChannelUris de blocos secundários pode alterar a qualquer momento. Em instalações de saudação ordem tookeep no hub de notificação Olá atualizado, dispositivo Olá deve atualizá-los com hello ChannelUris atual de blocos secundário hello.

## <a name="registration-management-from-hello-device"></a>Gerenciamento de registro de dispositivo Olá
Ao gerenciar o registro de dispositivos de aplicativos cliente, Olá back-end só é responsável por enviar notificações. Aplicativos cliente manter os identificadores PNS backup toodate e registrar marcas. Olá a imagem a seguir ilustra esse padrão.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

dispositivo Olá primeiro recupera Olá PNS tratar da saudação PNS e registra com o hub de notificação Olá diretamente. Após o registro de saudação for bem-sucedida, o back-end de aplicativo hello pode enviar uma notificação direcionamento esse registro. Para obter mais informações sobre como toosend notificações, consulte [expressões de marca e roteamento](notification-hubs-tags-segment-push-message.md).
Observe que, nesse caso, você usará escutar apenas direitos tooaccess seus hubs de notificação de dispositivo de saudação. Para saber mais, consulte [Segurança](notification-hubs-push-notification-security.md).

Registro de dispositivo de saudação é o método mais simples de hello, mas ele apresenta algumas desvantagens.
desvantagem primeiro Olá é que um aplicativo cliente só pode atualizar suas marcas quando o aplicativo hello está ativo. Por exemplo, se um usuário tiver dois dispositivos que registram marcas toosport relacionados equipes, quando o primeiro dispositivo de saudação registra para uma marca adicional (por exemplo, Seahawks), Olá segundo dispositivo não receberá notificações Olá sobre Olá Seahawks até que o aplicativo hello Olá segundo dispositivo é executado uma segunda vez. Geralmente, quando marcas são afetadas por vários dispositivos, gerenciar marcas de saudação back-end é uma boa opção.
desvantagem de segundo saudação do gerenciamento de registro de aplicativo cliente do hello é que, desde que os aplicativos podem ser quebrados, proteger registro Olá marcas toospecific requer muito cuidado, conforme explicado na seção hello "segurança de nível de marca".

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Tooregister de código de exemplo com um hub de notificação de um dispositivo usando uma instalação
Neste momento, isso só é suportado usando Olá [API de REST de Hubs de notificação](https://msdn.microsoft.com/library/mt621153.aspx).

Você também pode usar o método de PATCH hello usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de saudação.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Tooregister de código de exemplo com um hub de notificação de um dispositivo usando um registro
Esses métodos de criar ou atualizar um registro de dispositivo Olá no qual eles são chamados. Isso significa que, em ordem tooupdate Olá identificador ou hello marcas, você deve substituir o registro inteiro Olá. Lembre-se de que os registros são transitórios, para que você sempre deve ter um repositório confiável com marcas atuais de saudação que precisa de um dispositivo específico.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Gerenciamento de registros de um back-end
Gerenciar registros de back-end de saudação requer a criação de código adicional. Olá aplicativo de dispositivo Olá deve fornecer Olá back-end toohello do identificador do PNS atualizada sempre que o aplicativo hello iniciado (junto com marcas e modelos) e back-end de saudação deverá atualizar esse identificador no hub de notificação de saudação. Olá a imagem a seguir ilustra esse design.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

as vantagens de saudação do gerenciamento de registros de back-end de saudação incluem hello capacidade toomodify marcas tooregistrations mesmo quando a saudação de aplicativo correspondente no dispositivo hello está inativo e o aplicativo de cliente de saudação do tooauthenticate antes de adicionar um registro de tooits de marca.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Tooregister de código de exemplo com um hub de notificação de um back-end usando uma instalação
dispositivo de cliente Olá ainda obtém seu identificador PNS e propriedades de instalação relevantes como antes e chama uma API personalizada no back-end Olá que pode realizar o registro de saudação e autorizar marcas back-end de saudação etc. pode aproveitar Olá [SDK do Hub de notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Você também pode usar o método de PATCH hello usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de saudação.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Tooregister de código de exemplo com um hub de notificação de um dispositivo usando uma id de registro
No back-end do aplicativo, você pode executar operações básicas de CRUDS nos registros. Por exemplo:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


Olá back-end deve tratar de simultaneidade entre as atualizações de registro. O Barramento de Serviço oferece um controle de simultaneidade otimista para gerenciamento de registro. No nível de saudação HTTP, isso é implementado com o uso de saudação do ETag em operações de gerenciamento de registro. Esse recurso é usado de forma transparente pelos SDKs da Microsoft, que lançam uma exceção se uma atualização for rejeitada por motivos de simultaneidade. Olá backend do aplicativo é responsável por gerenciar essas exceções e tentar novamente a atualização de saudação se necessário.

