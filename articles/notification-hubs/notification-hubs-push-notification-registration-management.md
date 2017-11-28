---
title: Gerenciamento de registros
description: "Este tópico explica como registrar dispositivos em hubs de notificação para receber notificações por push."
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
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="6ac60-103">Gerenciamento de registros</span><span class="sxs-lookup"><span data-stu-id="6ac60-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="6ac60-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6ac60-104">Overview</span></span>
<span data-ttu-id="6ac60-105">Este tópico explica como registrar dispositivos em hubs de notificação para receber notificações por push.</span><span class="sxs-lookup"><span data-stu-id="6ac60-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="6ac60-106">O tópico descreve em alto nível os registros e apresenta os dois padrões principais para registro de dispositivos: registro diretamente do dispositivo para o hub de notificação e registro por meio de um back-end de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="6ac60-107">O que é o registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6ac60-107">What is device registration</span></span>
<span data-ttu-id="6ac60-108">O registro de dispositivos com um Hub de Notificação é realizado usando um **Registro** ou uma **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="6ac60-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="6ac60-109">Registros</span><span class="sxs-lookup"><span data-stu-id="6ac60-109">Registrations</span></span>
<span data-ttu-id="6ac60-110">Um registro associa o identificador PNS (Serviço de Notificação de Plataforma) de um dispositivo com marcas e, possivelmente, um modelo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="6ac60-111">O identificador PNS pode ser um ChannelURI, um token do dispositivo ou uma ID de registro de GCM.</span><span class="sxs-lookup"><span data-stu-id="6ac60-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="6ac60-112">As marcas são usadas para direcionar notificações para o conjunto correto de identificadores de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6ac60-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="6ac60-113">Para saber mais, veja [Expressões de marca e de roteamento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="6ac60-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="6ac60-114">Os modelos são usados para implementar transformações por registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="6ac60-115">Para saber mais, veja [Modelos](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6ac60-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="6ac60-116">Instalações</span><span class="sxs-lookup"><span data-stu-id="6ac60-116">Installations</span></span>
<span data-ttu-id="6ac60-117">Uma instalação é um registro aprimorado que inclui um conjunto de propriedades relacionadas ao envio por push.</span><span class="sxs-lookup"><span data-stu-id="6ac60-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="6ac60-118">Essa é a abordagem mais recente e adequada para registrar seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6ac60-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="6ac60-119">No entanto, não há suporte pelo SDK do .NET do lado do cliente ([SDK do Hub de Notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) até o momento.</span><span class="sxs-lookup"><span data-stu-id="6ac60-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="6ac60-120">Isso significa que, se você estiver registrando no próprio dispositivo cliente, precisará usar a abordagem da [API REST de Hubs de Notificação](https://msdn.microsoft.com/library/mt621153.aspx) para dar suporte às instalações.</span><span class="sxs-lookup"><span data-stu-id="6ac60-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="6ac60-121">Se você estiver usando um serviço de back-end, deverá ser capaz de usar o [SDK do Hub de Notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6ac60-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="6ac60-122">A seguir, algumas vantagens importantes do uso de instalações:</span><span class="sxs-lookup"><span data-stu-id="6ac60-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="6ac60-123">A criação ou atualização de uma instalação é totalmente idempotente.</span><span class="sxs-lookup"><span data-stu-id="6ac60-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="6ac60-124">Portanto, você pode repetir sem as preocupações com registros duplicados.</span><span class="sxs-lookup"><span data-stu-id="6ac60-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="6ac60-125">O modelo de instalação facilita a realização de envios individuais por push - direcionando a um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="6ac60-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="6ac60-126">Uma marca de sistema **"$InstallationId: [installationId]"** é adicionada automaticamente com cada registro com base em instalação.</span><span class="sxs-lookup"><span data-stu-id="6ac60-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="6ac60-127">Portanto, você pode chamar um envio para essa marca a fim de direcionar a um dispositivo específico sem precisar fazer qualquer codificação adicional.</span><span class="sxs-lookup"><span data-stu-id="6ac60-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="6ac60-128">O uso de instalações também permite que você faça atualizações parciais no registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="6ac60-129">A atualização parcial de uma instalação é solicitada com um método PATCH usando o [padrão JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="6ac60-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="6ac60-130">Isso é particularmente útil quando você deseja atualizar marcas no registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="6ac60-131">Não é necessário obter todo o registro e reenviar todas as marcas anteriores novamente.</span><span class="sxs-lookup"><span data-stu-id="6ac60-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="6ac60-132">Uma instalação pode conter as seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="6ac60-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="6ac60-133">Para obter uma lista completa de propriedades de instalação, veja [Criar ou Sobrescrever uma Instalação com REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [Propriedades da Instalação](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para o .</span><span class="sxs-lookup"><span data-stu-id="6ac60-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
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



<span data-ttu-id="6ac60-134">É importante observar que, por padrão, os registros e as instalações não expiram mais.</span><span class="sxs-lookup"><span data-stu-id="6ac60-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="6ac60-135">Os registros e instalações devem conter um identificador PNS válido para cada dispositivo/canal.</span><span class="sxs-lookup"><span data-stu-id="6ac60-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="6ac60-136">Como os identificadores PNS só podem ser obtidos em um aplicativo cliente no dispositivo, um padrão é registrar diretamente no dispositivo com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="6ac60-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="6ac60-137">Por outro lado, as considerações de segurança e a lógica de negócios relacionadas às marcas podem exigir o gerenciamento do registro do dispositivo no back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="6ac60-138">Modelos</span><span class="sxs-lookup"><span data-stu-id="6ac60-138">Templates</span></span>
<span data-ttu-id="6ac60-139">Se você quiser usar [Modelos](notification-hubs-templates-cross-platform-push-messages.md), a instalação do dispositivo também armazenará todos os modelos associados a esse dispositivo em um formato JSON (veja o exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="6ac60-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="6ac60-140">Os nomes de modelo ajudam a direcionar a modelos diferentes do mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="6ac60-141">Observe que cada nome de modelo é mapeado para um corpo de modelo e um conjunto opcional de marcas.</span><span class="sxs-lookup"><span data-stu-id="6ac60-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="6ac60-142">Além disso, cada plataforma pode ter propriedades adicionais de modelo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="6ac60-143">Para a Windows Store (usando WNS) e o Windows Phone 8 (usando MPNS), um conjunto adicional de cabeçalhos pode fazer parte do modelo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="6ac60-144">No caso dos APNs, você pode definir uma propriedade de expiração para uma constante ou para uma expressão de modelo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="6ac60-145">Para obter uma lista completa de propriedades de instalação, confira o tópico [Criar ou substituir uma instalação com REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6ac60-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="6ac60-146">Blocos secundários para aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="6ac60-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="6ac60-147">Para aplicativos cliente da Windows Store, o envio de notificações para blocos secundários é igual ao envio delas ao bloco primário.</span><span class="sxs-lookup"><span data-stu-id="6ac60-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="6ac60-148">Isso também tem suporte nas instalações.</span><span class="sxs-lookup"><span data-stu-id="6ac60-148">This is also supported in installations.</span></span> <span data-ttu-id="6ac60-149">Observe que os blocos secundários têm um ChannelUri diferente, o qual o SDK no aplicativo cliente trata de forma transparente.</span><span class="sxs-lookup"><span data-stu-id="6ac60-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="6ac60-150">O dicionário SecondaryTiles usa o mesmo TileId usado para criar o objeto SecondaryTiles em seu aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="6ac60-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="6ac60-151">Assim como acontece com o ChannelUri primário, os ChannelUris de blocos secundários podem ser alterados a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="6ac60-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="6ac60-152">Para manter as instalações no hub de notificação atualizadas, o dispositivo deve atualizá-las com os ChannelUris atuais dos blocos secundários.</span><span class="sxs-lookup"><span data-stu-id="6ac60-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="6ac60-153">Gerenciamento de registro do dispositivo</span><span class="sxs-lookup"><span data-stu-id="6ac60-153">Registration management from the device</span></span>
<span data-ttu-id="6ac60-154">Ao gerenciar o registro de dispositivos de aplicativos cliente, o back-end é responsável apenas pelo envio de notificações.</span><span class="sxs-lookup"><span data-stu-id="6ac60-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="6ac60-155">Os aplicativos cliente mantêm os identificadores PNS atualizados e registram marcas.</span><span class="sxs-lookup"><span data-stu-id="6ac60-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="6ac60-156">A figura a seguir ilustra esse padrão.</span><span class="sxs-lookup"><span data-stu-id="6ac60-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="6ac60-157">Primeiro, o dispositivo recupera o identificador PNS do PNS e registra diretamente com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6ac60-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="6ac60-158">Após a conclusão do registro, o back-end do aplicativo pode enviar uma notificação visando esse registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="6ac60-159">Para saber mais sobre como enviar notificações, veja [Expressões de marca e de roteamento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="6ac60-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="6ac60-160">Observe que, nesse caso, você usará apenas direitos de Escuta para acessar os hubs de notificação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="6ac60-161">Para saber mais, consulte [Segurança](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="6ac60-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="6ac60-162">O registro do dispositivo é o método mais simples, mas tem algumas desvantagens.</span><span class="sxs-lookup"><span data-stu-id="6ac60-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="6ac60-163">A primeira desvantagem é que um aplicativo cliente só pode atualizar suas marcas quando está ativo.</span><span class="sxs-lookup"><span data-stu-id="6ac60-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="6ac60-164">Por exemplo, se um usuário tiver dois dispositivos que registram marcas relacionadas a equipes esportivas, quando o primeiro dispositivo registrar-se para uma marca adicional (por exemplo, Seahawks), o segundo dispositivo não receberá notificações sobre o Seahawks até que o aplicativo no segundo dispositivo seja executado uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="6ac60-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="6ac60-165">Normalmente, quando as marcas são afetadas por vários dispositivos, o gerenciamento das marcas do back-end é uma opção desejável.</span><span class="sxs-lookup"><span data-stu-id="6ac60-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="6ac60-166">A segunda desvantagem do gerenciamento de registro do aplicativo cliente é que, como os aplicativos podem ser violados, a proteção do registro para marcas específicas exige um cuidado extra, conforme explicado na seção "Segurança no nível da marca".</span><span class="sxs-lookup"><span data-stu-id="6ac60-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="6ac60-167">Exemplo de código para registrar com um hub de notificação de um dispositivo usando uma instalação</span><span class="sxs-lookup"><span data-stu-id="6ac60-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="6ac60-168">Neste momento, isso tem suporte somente com o uso da [API REST dos Hubs de Notificação](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac60-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="6ac60-169">Você também pode usar o método PATCH com o [padrão JSON-Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação.</span><span class="sxs-lookup"><span data-stu-id="6ac60-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

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

        // Determine the targetUri that we will sign
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



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="6ac60-170">Exemplo de código para registrar com um hub de notificação de um dispositivo usando um registro</span><span class="sxs-lookup"><span data-stu-id="6ac60-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="6ac60-171">Esses métodos criam ou atualizam um registro para o dispositivo no qual são chamados.</span><span class="sxs-lookup"><span data-stu-id="6ac60-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="6ac60-172">Isso significa que, para atualizar o indicador ou as marcas, você deve substituir todo o registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="6ac60-173">Lembre-se de que os registros são temporários e, portanto, você sempre deverá ter um armazenamento confiável com as marcas atuais exigidas por um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="6ac60-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="6ac60-174">Gerenciamento de registros de um back-end</span><span class="sxs-lookup"><span data-stu-id="6ac60-174">Registration management from a backend</span></span>
<span data-ttu-id="6ac60-175">O gerenciamento de registros do back-end exige a produção adicional de código.</span><span class="sxs-lookup"><span data-stu-id="6ac60-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="6ac60-176">O aplicativo do dispositivo deve fornecer o indicador PNS atualizado para o back-end sempre que o aplicativo for iniciado (junto com marcas e modelos) e o back-end deve atualizar esse identificador no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6ac60-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="6ac60-177">A figura a seguir ilustra esse design.</span><span class="sxs-lookup"><span data-stu-id="6ac60-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="6ac60-178">As vantagens do gerenciamento de registros a partir do back-end incluem a capacidade de modificar marcas para os registros, mesmo quando o aplicativo correspondente no dispositivo estiver inativo, e a capacidade de autenticar o aplicativo cliente antes de adicionar uma marca a seu registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="6ac60-179">Exemplo de código para registrar com um hub de notificação de um back-end usando uma instalação</span><span class="sxs-lookup"><span data-stu-id="6ac60-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="6ac60-180">O dispositivo do cliente ainda obtém seu identificador PNS e as propriedades de instalação relevantes como fazia antes, e chama uma API personalizada no back-end que pode executar o registro e autorizar marcas etc. O back-end pode aproveitar o [SDK do Hub de Notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6ac60-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="6ac60-181">Você também pode usar o método PATCH com o [padrão JSON-Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação.</span><span class="sxs-lookup"><span data-stu-id="6ac60-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
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


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="6ac60-182">Exemplo de código para registrar com um hub de notificação de um dispositivo usando uma ID de registro</span><span class="sxs-lookup"><span data-stu-id="6ac60-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="6ac60-183">No back-end do aplicativo, você pode executar operações básicas de CRUDS nos registros.</span><span class="sxs-lookup"><span data-stu-id="6ac60-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="6ac60-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ac60-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
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


<span data-ttu-id="6ac60-185">O back-end deve manipular a simultaneidade entre as atualizações do registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="6ac60-186">O Barramento de Serviço oferece um controle de simultaneidade otimista para gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="6ac60-187">No nível HTTP, isso é implementado com o uso de ETag nas operações de gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="6ac60-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="6ac60-188">Esse recurso é usado de forma transparente pelos SDKs da Microsoft, que lançam uma exceção se uma atualização for rejeitada por motivos de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="6ac60-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="6ac60-189">O back-end é responsável por manipular essas exceções e tentar atualizar novamente, se isso for necessário.</span><span class="sxs-lookup"><span data-stu-id="6ac60-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

