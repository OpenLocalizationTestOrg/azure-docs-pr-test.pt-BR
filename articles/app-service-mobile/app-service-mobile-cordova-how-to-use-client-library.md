---
title: "aaaHow tooUse plug-in do Apache Cordova para aplicativos móveis do Azure"
description: "Como tooUse plug-in do Apache Cordova para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="cad5f-103">Como biblioteca de cliente do Apache Cordova toouse para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="cad5f-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="cad5f-104">Este guia ensina usando hello mais recente de cenários comuns de tooperform [plug-in do Apache Cordova para aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="cad5f-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="cad5f-105">Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end, crie uma tabela e baixar um projeto do Apache Cordova pré-criado.</span><span class="sxs-lookup"><span data-stu-id="cad5f-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="cad5f-106">Neste guia, vamos nos concentrar no lado do cliente Olá plug-in do Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="cad5f-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="cad5f-107">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="cad5f-107">Supported platforms</span></span>
<span data-ttu-id="cad5f-108">Esse SDK dá suporte à versão 6.0.0 do Apache Cordova e posterior nos dispositivos iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="cad5f-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="cad5f-109">suporte a plataformas Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cad5f-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="cad5f-110">API do Android 19 a 24 (KitKat usando Nougat).</span><span class="sxs-lookup"><span data-stu-id="cad5f-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="cad5f-111">iOS versão 8.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="cad5f-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="cad5f-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="cad5f-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="cad5f-113">Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="cad5f-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="cad5f-114"><a name="Setup"></a>Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cad5f-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="cad5f-115">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="cad5f-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="cad5f-116">Este guia presume que tabela Olá tenha Olá mesmo esquema de tabelas Olá esses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="cad5f-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="cad5f-117">Este guia também pressupõe que você adicionou o código de tooyour Olá plug-in do Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="cad5f-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="cad5f-118">Se você não tiver feito isso, você pode adicionar o projeto de tooyour Olá Apache Cordova plug-in na linha de comando hello:</span><span class="sxs-lookup"><span data-stu-id="cad5f-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="cad5f-119">Para saber mais sobre como criar [seu primeiro aplicativo do Apache Cordova], consulte a documentação.</span><span class="sxs-lookup"><span data-stu-id="cad5f-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="cad5f-120"><a name="ionic"></a>Configurar um aplicativo Ionic v2</span><span class="sxs-lookup"><span data-stu-id="cad5f-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="cad5f-121">tooproperly configurar um projeto Ionic v2, primeiro criar um aplicativo básico e adicionar plug-in Cordova de saudação:</span><span class="sxs-lookup"><span data-stu-id="cad5f-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="cad5f-122">Adicionar Olá linhas seguintes muito`app.component.ts` objeto de toocreate saudação do cliente:</span><span class="sxs-lookup"><span data-stu-id="cad5f-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="cad5f-123">Você agora pode compilar e executar o projeto Olá no navegador de saudação:</span><span class="sxs-lookup"><span data-stu-id="cad5f-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="cad5f-124">plug-in de Cordova de aplicativos móveis do Azure Olá dá suporte a ambos os aplicativos Ionic v1 e v2.</span><span class="sxs-lookup"><span data-stu-id="cad5f-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="cad5f-125">Somente aplicativos Olá v2 Ionic requerem a declaração adicional para Olá `WindowsAzure` objeto.</span><span class="sxs-lookup"><span data-stu-id="cad5f-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="cad5f-126"><a name="auth"></a>Como autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="cad5f-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="cad5f-127">O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="cad5f-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="cad5f-128">Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários.</span><span class="sxs-lookup"><span data-stu-id="cad5f-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="cad5f-129">Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="cad5f-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="cad5f-130">Para obter mais informações, consulte Olá [Introdução à autenticação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="cad5f-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="cad5f-131">Ao usar a autenticação em um aplicativo do Apache Cordova, Olá plug-ins do Cordova a seguir deve estar disponível:</span><span class="sxs-lookup"><span data-stu-id="cad5f-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="cad5f-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="cad5f-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="cad5f-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="cad5f-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="cad5f-134">Dois fluxos de autenticação são suportados: um server flow e um client flow.</span><span class="sxs-lookup"><span data-stu-id="cad5f-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="cad5f-135">fluxo do servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web.</span><span class="sxs-lookup"><span data-stu-id="cad5f-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="cad5f-136">Olá fluxo cliente permite integração mais profunda com recursos específicos do dispositivo, como single-sign-on pois depende de SDKs de específico do dispositivo específico do provedor.</span><span class="sxs-lookup"><span data-stu-id="cad5f-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="cad5f-137"><a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.</span><span class="sxs-lookup"><span data-stu-id="cad5f-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="cad5f-138">Vários tipos de aplicativos do Apache Cordova usam um toohandle de capacidade de loopback que OAuth UI flui.</span><span class="sxs-lookup"><span data-stu-id="cad5f-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="cad5f-139">Fluxos de OAuth UI no localhost causam problemas desde que o serviço de autenticação da saudação só sabe como tooutilize seu serviço por padrão.</span><span class="sxs-lookup"><span data-stu-id="cad5f-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="cad5f-140">Exemplos de fluxos de interface do usuário OAuth problemáticos incluem:</span><span class="sxs-lookup"><span data-stu-id="cad5f-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="cad5f-141">emulador do Ripple Hello.</span><span class="sxs-lookup"><span data-stu-id="cad5f-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="cad5f-142">Recarregamento dinâmico com Ionic.</span><span class="sxs-lookup"><span data-stu-id="cad5f-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="cad5f-143">Em execução Olá móvel back-end localmente</span><span class="sxs-lookup"><span data-stu-id="cad5f-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="cad5f-144">Executando o back-end de saudação móvel em um serviço de aplicativo do Azure diferente que a autenticação fornecendo uma saudação.</span><span class="sxs-lookup"><span data-stu-id="cad5f-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="cad5f-145">Siga essas instruções tooadd sua configuração de toohello configurações locais:</span><span class="sxs-lookup"><span data-stu-id="cad5f-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="cad5f-146">Faça logon no toohello [portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="cad5f-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="cad5f-147">Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="cad5f-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="cad5f-148">Clique em **Ferramentas**</span><span class="sxs-lookup"><span data-stu-id="cad5f-148">Click **Tools**</span></span>
4. <span data-ttu-id="cad5f-149">Clique em **Gerenciador de recursos** no menu OBSERVE Olá, em seguida, clique em **vá**.</span><span class="sxs-lookup"><span data-stu-id="cad5f-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="cad5f-150">Uma nova janela ou guia é aberta.</span><span class="sxs-lookup"><span data-stu-id="cad5f-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="cad5f-151">Expanda Olá **config**, **authsettings** nós para o seu site na navegação esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="cad5f-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="cad5f-152">Clique em **Editar**</span><span class="sxs-lookup"><span data-stu-id="cad5f-152">Click **Edit**</span></span>
7. <span data-ttu-id="cad5f-153">Procure o elemento de "allowedExternalRedirectUrls" hello.</span><span class="sxs-lookup"><span data-stu-id="cad5f-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="cad5f-154">Ele pode ser definido toonull ou uma matriz de valores.</span><span class="sxs-lookup"><span data-stu-id="cad5f-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="cad5f-155">Alterar Olá valor toohello seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="cad5f-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="cad5f-156">Substitua URLs Olá Olá URLs do serviço.</span><span class="sxs-lookup"><span data-stu-id="cad5f-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="cad5f-157">Exemplos incluem "http://localhost:3000" (para Olá serviço de exemplo do Node. js) ou "http://localhost:4400" (para o serviço de ondulação Olá).</span><span class="sxs-lookup"><span data-stu-id="cad5f-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="cad5f-158">No entanto, essas URLs são exemplos - sua situação, incluindo serviços de saudação mencionados nos exemplos Olá, podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="cad5f-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="cad5f-159">Clique em Olá **leitura/gravação** botão no canto superior direito de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="cad5f-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="cad5f-160">Clique em Olá verde **colocar** botão.</span><span class="sxs-lookup"><span data-stu-id="cad5f-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="cad5f-161">configurações de saudação são salvas neste momento.</span><span class="sxs-lookup"><span data-stu-id="cad5f-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="cad5f-162">Não feche a janela do navegador Olá até que as configurações de saudação concluiu a salvar.</span><span class="sxs-lookup"><span data-stu-id="cad5f-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="cad5f-163">Também adicione essas configurações de CORS loopback URLs toohello para o serviço de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="cad5f-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="cad5f-164">Faça logon no toohello [portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="cad5f-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="cad5f-165">Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="cad5f-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="cad5f-166">folha de configurações de saudação é aberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cad5f-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="cad5f-167">Se não for, clique em **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="cad5f-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="cad5f-168">Clique em **CORS** menu Olá API.</span><span class="sxs-lookup"><span data-stu-id="cad5f-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="cad5f-169">Digite a URL Olá que você deseja tooadd na caixa Olá fornecida e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="cad5f-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="cad5f-170">Insira URLs adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="cad5f-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="cad5f-171">Clique em **salvar** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="cad5f-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="cad5f-172">Leva aproximadamente 10 a 15 segundos para efeito de tootake do hello novas configurações.</span><span class="sxs-lookup"><span data-stu-id="cad5f-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="cad5f-173"><a name="register-for-push"></a>Como registrar notificações por push</span><span class="sxs-lookup"><span data-stu-id="cad5f-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="cad5f-174">Instalar Olá [phonegap de plug-in de push] toohandle notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="cad5f-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="cad5f-175">Este plug-in pode ser facilmente adicionada usando o `cordova plugin add` comando na linha de comando hello, ou por meio do instalador de plug-in de Git hello dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cad5f-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="cad5f-176">O código a seguir em seu aplicativo Apache Cordova registra seu dispositivo para notificações por push:</span><span class="sxs-lookup"><span data-stu-id="cad5f-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="cad5f-177">Use notificações de push de toosend Olá SDK de Hubs de notificação do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cad5f-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="cad5f-178">Nunca envie notificações por push diretamente dos clientes.</span><span class="sxs-lookup"><span data-stu-id="cad5f-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="cad5f-179">Fazer assim pode ser usado tootrigger um ataque de negação de serviço em relação a Hubs de notificação ou Olá PNS.</span><span class="sxs-lookup"><span data-stu-id="cad5f-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="cad5f-180">Olá PNS pode proibir o tráfego como resultado de tais ataques.</span><span class="sxs-lookup"><span data-stu-id="cad5f-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="cad5f-181">Mais informações</span><span class="sxs-lookup"><span data-stu-id="cad5f-181">More information</span></span>

<span data-ttu-id="cad5f-182">Você pode encontrar detalhes de API detalhadas em nossa [Documentação da API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="cad5f-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[portal do Azure]: https://portal.azure.com
[início rápido do Azure Mobile aplicativos]: app-service-mobile-cordova-get-started.md
[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in do Apache Cordova para aplicativos móveis do Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[seu primeiro aplicativo do Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap de plug-in de push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
