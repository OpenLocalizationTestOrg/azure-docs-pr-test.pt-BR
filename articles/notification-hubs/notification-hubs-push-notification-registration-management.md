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
# <a name="registration-management"></a><span data-ttu-id="e308f-103">Gerenciamento de registros</span><span class="sxs-lookup"><span data-stu-id="e308f-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="e308f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e308f-104">Overview</span></span>
<span data-ttu-id="e308f-105">Este tópico explica como os dispositivos de tooregister com hubs de notificação na ordem tooreceive notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="e308f-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="e308f-106">tópico de saudação descreve os registros em um nível alto, em seguida, apresenta Olá dois padrões de principal para o registro de dispositivos: registro de dispositivo Olá diretamente o hub de notificação toohello e registro através de um back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e308f-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="e308f-107">O que é o registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="e308f-107">What is device registration</span></span>
<span data-ttu-id="e308f-108">O registro de dispositivos com um Hub de Notificação é realizado usando um **Registro** ou uma **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="e308f-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="e308f-109">Registros</span><span class="sxs-lookup"><span data-stu-id="e308f-109">Registrations</span></span>
<span data-ttu-id="e308f-110">Um registro associa Olá identificador de serviço de notificação de plataforma (PNS) para um dispositivo com marcas e, possivelmente, um modelo.</span><span class="sxs-lookup"><span data-stu-id="e308f-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="e308f-111">Olá PNS identificador pode ser um ChannelURI, token do dispositivo ou id de registro do GCM. Marcas são usadas tooroute notificações toohello o conjunto correto de identificadores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e308f-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="e308f-112">Para saber mais, veja [Expressões de marca e de roteamento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e308f-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="e308f-113">Os modelos são usados tooimplement por registro transformação.</span><span class="sxs-lookup"><span data-stu-id="e308f-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="e308f-114">Para saber mais, veja [Modelos](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e308f-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="e308f-115">Instalações</span><span class="sxs-lookup"><span data-stu-id="e308f-115">Installations</span></span>
<span data-ttu-id="e308f-116">Uma instalação é um registro aprimorado que inclui um conjunto de propriedades relacionadas ao envio por push.</span><span class="sxs-lookup"><span data-stu-id="e308f-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="e308f-117">É Olá tooregistering abordagem melhor e mais recentes em seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e308f-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="e308f-118">No entanto, não há suporte pelo SDK do .NET do lado do cliente ([SDK do Hub de Notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) até o momento.</span><span class="sxs-lookup"><span data-stu-id="e308f-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="e308f-119">Isso significa que se você estiver registrando do próprio dispositivo de cliente hello, você teria Olá toouse [API de REST de Hubs de notificação](https://msdn.microsoft.com/library/mt621153.aspx) abordagem toosupport instalações.</span><span class="sxs-lookup"><span data-stu-id="e308f-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="e308f-120">Se você estiver usando um serviço de back-end, você deve ser capaz de toouse [SDK do Hub de notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="e308f-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="e308f-121">Olá seguem algumas instalações de toousing principais vantagens:</span><span class="sxs-lookup"><span data-stu-id="e308f-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="e308f-122">A criação ou atualização de uma instalação é totalmente idempotente.</span><span class="sxs-lookup"><span data-stu-id="e308f-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="e308f-123">Portanto, você pode repetir sem as preocupações com registros duplicados.</span><span class="sxs-lookup"><span data-stu-id="e308f-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="e308f-124">modelo de instalação Olá torna fácil toodo individuais envios por push - direcionando o dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="e308f-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="e308f-125">Uma marca de sistema **"$InstallationId: [installationId]"** é adicionada automaticamente com cada registro com base em instalação.</span><span class="sxs-lookup"><span data-stu-id="e308f-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="e308f-126">Assim você pode chamar um tootarget de marca toothis enviar um dispositivo específico sem ter que toodo qualquer codificação adicional.</span><span class="sxs-lookup"><span data-stu-id="e308f-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="e308f-127">Usar instalações também permite que você toodo registro parcial atualizações.</span><span class="sxs-lookup"><span data-stu-id="e308f-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="e308f-128">Olá atualização parcial de uma instalação é solicitada com um método de PATCH usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="e308f-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="e308f-129">Isso é particularmente útil quando você quiser tooupdate marcas no registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="e308f-130">Você não tem toopull para baixo de registro todo hello e reenviar a todas as marcas de saudação anterior novamente.</span><span class="sxs-lookup"><span data-stu-id="e308f-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="e308f-131">Uma instalação pode conter Olá Olá propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="e308f-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="e308f-132">Para obter uma lista completa de saudação instalação propriedades, consulte [criar ou substituir uma instalação com a API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [propriedades de instalação](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para hello.</span><span class="sxs-lookup"><span data-stu-id="e308f-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

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



<span data-ttu-id="e308f-133">É importante toonote que instalações por padrão e os registros não expiram.</span><span class="sxs-lookup"><span data-stu-id="e308f-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="e308f-134">Os registros e instalações devem conter um identificador PNS válido para cada dispositivo/canal.</span><span class="sxs-lookup"><span data-stu-id="e308f-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="e308f-135">Como os identificadores PNS só podem ser obtidos em um aplicativo cliente no dispositivo hello, um padrão é tooregister diretamente no dispositivo com o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="e308f-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="e308f-136">Olá outro lado, as considerações de segurança e lógica de negócios relacionam tootags pode exigir o registro de dispositivos toomanage no back-end do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e308f-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="e308f-137">Modelos</span><span class="sxs-lookup"><span data-stu-id="e308f-137">Templates</span></span>
<span data-ttu-id="e308f-138">Se você quiser toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md), a instalação do dispositivo Olá também manter todos os modelos associados a esse dispositivo em JSON formatar (veja o exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="e308f-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="e308f-139">Olá nomes de modelo ajuda destino modelos diferentes para Olá mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e308f-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="e308f-140">Observe que cada nome de modelo mapeia tooa corpo de modelo e um conjunto opcional de marcas.</span><span class="sxs-lookup"><span data-stu-id="e308f-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="e308f-141">Além disso, cada plataforma pode ter propriedades adicionais de modelo.</span><span class="sxs-lookup"><span data-stu-id="e308f-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="e308f-142">Para Windows Store (usando WNS) e Windows Phone 8 (usando MPNS), um conjunto adicional de cabeçalhos pode ser parte do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="e308f-143">No caso de saudação de APNs, você pode definir uma expressão de modelo constante ou tooa um tooeither de propriedade de expiração.</span><span class="sxs-lookup"><span data-stu-id="e308f-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="e308f-144">Para obter uma lista completa de saudação instalação propriedades, consulte [criar ou substituir uma instalação com REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="e308f-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="e308f-145">Blocos secundários para aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="e308f-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="e308f-146">Para aplicativos de cliente da Windows Store, notificações de enviadas é toosecondary blocos mesmo Olá como enviá-los toohello principal.</span><span class="sxs-lookup"><span data-stu-id="e308f-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="e308f-147">Isso também tem suporte nas instalações.</span><span class="sxs-lookup"><span data-stu-id="e308f-147">This is also supported in installations.</span></span> <span data-ttu-id="e308f-148">Observe que o secundários blocos têm um ChannelUri diferente, quais Olá SDK em seu aplicativo cliente trata transparente.</span><span class="sxs-lookup"><span data-stu-id="e308f-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="e308f-149">Olá SecondaryTiles dicionário usa Olá TileId mesmo que é usado toocreate Olá SecondaryTiles objeto em seu aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="e308f-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="e308f-150">Como com hello primário ChannelUri, ChannelUris de blocos secundários pode alterar a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e308f-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="e308f-151">Em instalações de saudação ordem tookeep no hub de notificação Olá atualizado, dispositivo Olá deve atualizá-los com hello ChannelUris atual de blocos secundário hello.</span><span class="sxs-lookup"><span data-stu-id="e308f-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="e308f-152">Gerenciamento de registro de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="e308f-152">Registration management from hello device</span></span>
<span data-ttu-id="e308f-153">Ao gerenciar o registro de dispositivos de aplicativos cliente, Olá back-end só é responsável por enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="e308f-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="e308f-154">Aplicativos cliente manter os identificadores PNS backup toodate e registrar marcas.</span><span class="sxs-lookup"><span data-stu-id="e308f-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="e308f-155">Olá a imagem a seguir ilustra esse padrão.</span><span class="sxs-lookup"><span data-stu-id="e308f-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="e308f-156">dispositivo Olá primeiro recupera Olá PNS tratar da saudação PNS e registra com o hub de notificação Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="e308f-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="e308f-157">Após o registro de saudação for bem-sucedida, o back-end de aplicativo hello pode enviar uma notificação direcionamento esse registro.</span><span class="sxs-lookup"><span data-stu-id="e308f-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="e308f-158">Para obter mais informações sobre como toosend notificações, consulte [expressões de marca e roteamento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e308f-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="e308f-159">Observe que, nesse caso, você usará escutar apenas direitos tooaccess seus hubs de notificação de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="e308f-160">Para saber mais, consulte [Segurança](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="e308f-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="e308f-161">Registro de dispositivo de saudação é o método mais simples de hello, mas ele apresenta algumas desvantagens.</span><span class="sxs-lookup"><span data-stu-id="e308f-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="e308f-162">desvantagem primeiro Olá é que um aplicativo cliente só pode atualizar suas marcas quando o aplicativo hello está ativo.</span><span class="sxs-lookup"><span data-stu-id="e308f-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="e308f-163">Por exemplo, se um usuário tiver dois dispositivos que registram marcas toosport relacionados equipes, quando o primeiro dispositivo de saudação registra para uma marca adicional (por exemplo, Seahawks), Olá segundo dispositivo não receberá notificações Olá sobre Olá Seahawks até que o aplicativo hello Olá segundo dispositivo é executado uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="e308f-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="e308f-164">Geralmente, quando marcas são afetadas por vários dispositivos, gerenciar marcas de saudação back-end é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="e308f-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="e308f-165">desvantagem de segundo saudação do gerenciamento de registro de aplicativo cliente do hello é que, desde que os aplicativos podem ser quebrados, proteger registro Olá marcas toospecific requer muito cuidado, conforme explicado na seção hello "segurança de nível de marca".</span><span class="sxs-lookup"><span data-stu-id="e308f-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="e308f-166">Tooregister de código de exemplo com um hub de notificação de um dispositivo usando uma instalação</span><span class="sxs-lookup"><span data-stu-id="e308f-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="e308f-167">Neste momento, isso só é suportado usando Olá [API de REST de Hubs de notificação](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="e308f-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="e308f-168">Você também pode usar o método de PATCH hello usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="e308f-169">Tooregister de código de exemplo com um hub de notificação de um dispositivo usando um registro</span><span class="sxs-lookup"><span data-stu-id="e308f-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="e308f-170">Esses métodos de criar ou atualizar um registro de dispositivo Olá no qual eles são chamados.</span><span class="sxs-lookup"><span data-stu-id="e308f-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="e308f-171">Isso significa que, em ordem tooupdate Olá identificador ou hello marcas, você deve substituir o registro inteiro Olá.</span><span class="sxs-lookup"><span data-stu-id="e308f-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="e308f-172">Lembre-se de que os registros são transitórios, para que você sempre deve ter um repositório confiável com marcas atuais de saudação que precisa de um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="e308f-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="e308f-173">Gerenciamento de registros de um back-end</span><span class="sxs-lookup"><span data-stu-id="e308f-173">Registration management from a backend</span></span>
<span data-ttu-id="e308f-174">Gerenciar registros de back-end de saudação requer a criação de código adicional.</span><span class="sxs-lookup"><span data-stu-id="e308f-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="e308f-175">Olá aplicativo de dispositivo Olá deve fornecer Olá back-end toohello do identificador do PNS atualizada sempre que o aplicativo hello iniciado (junto com marcas e modelos) e back-end de saudação deverá atualizar esse identificador no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="e308f-176">Olá a imagem a seguir ilustra esse design.</span><span class="sxs-lookup"><span data-stu-id="e308f-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="e308f-177">as vantagens de saudação do gerenciamento de registros de back-end de saudação incluem hello capacidade toomodify marcas tooregistrations mesmo quando a saudação de aplicativo correspondente no dispositivo hello está inativo e o aplicativo de cliente de saudação do tooauthenticate antes de adicionar um registro de tooits de marca.</span><span class="sxs-lookup"><span data-stu-id="e308f-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="e308f-178">Tooregister de código de exemplo com um hub de notificação de um back-end usando uma instalação</span><span class="sxs-lookup"><span data-stu-id="e308f-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="e308f-179">dispositivo de cliente Olá ainda obtém seu identificador PNS e propriedades de instalação relevantes como antes e chama uma API personalizada no back-end Olá que pode realizar o registro de saudação e autorizar marcas back-end de saudação etc. pode aproveitar Olá [SDK do Hub de notificação para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="e308f-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="e308f-180">Você também pode usar o método de PATCH hello usando Olá [padrão JSON Patch](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e308f-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="e308f-181">Tooregister de código de exemplo com um hub de notificação de um dispositivo usando uma id de registro</span><span class="sxs-lookup"><span data-stu-id="e308f-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="e308f-182">No back-end do aplicativo, você pode executar operações básicas de CRUDS nos registros.</span><span class="sxs-lookup"><span data-stu-id="e308f-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="e308f-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e308f-183">For example:</span></span>

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


<span data-ttu-id="e308f-184">Olá back-end deve tratar de simultaneidade entre as atualizações de registro.</span><span class="sxs-lookup"><span data-stu-id="e308f-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="e308f-185">O Barramento de Serviço oferece um controle de simultaneidade otimista para gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="e308f-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="e308f-186">No nível de saudação HTTP, isso é implementado com o uso de saudação do ETag em operações de gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="e308f-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="e308f-187">Esse recurso é usado de forma transparente pelos SDKs da Microsoft, que lançam uma exceção se uma atualização for rejeitada por motivos de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="e308f-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="e308f-188">Olá backend do aplicativo é responsável por gerenciar essas exceções e tentar novamente a atualização de saudação se necessário.</span><span class="sxs-lookup"><span data-stu-id="e308f-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

