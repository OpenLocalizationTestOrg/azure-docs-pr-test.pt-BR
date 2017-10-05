---
title: "Como usar o Plug-in do Apache Cordova para os Aplicativos Móveis do Azure"
description: "Como usar o Plug-in do Apache Cordova para os Aplicativos Móveis do Azure"
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="69b74-103">Como usar a biblioteca de cliente do Apache Cordova para os Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="69b74-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="69b74-104">Este guia ensina a executar cenários comuns usando o mais recente [Plug-in do Apache Cordova para os Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="69b74-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="69b74-105">Se você for novo nos Aplicativos Móveis do Azure, primeiro conclua o [Início Rápido dos Aplicativos Móveis do Azure] para criar um back-end, criar uma tabela e baixar um projeto Apache Cordova pré-criado.</span><span class="sxs-lookup"><span data-stu-id="69b74-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="69b74-106">Neste guia, abordaremos o Plug-in do Apache Cordova do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="69b74-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="69b74-107">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="69b74-107">Supported platforms</span></span>
<span data-ttu-id="69b74-108">Esse SDK dá suporte à versão 6.0.0 do Apache Cordova e posterior nos dispositivos iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="69b74-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="69b74-109">O suporte de plataforma é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="69b74-109">The platform support is as follows:</span></span>

* <span data-ttu-id="69b74-110">API do Android 19 a 24 (KitKat usando Nougat).</span><span class="sxs-lookup"><span data-stu-id="69b74-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="69b74-111">iOS versão 8.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="69b74-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="69b74-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="69b74-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="69b74-113">Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="69b74-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="69b74-114"><a name="Setup"></a>Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="69b74-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="69b74-115">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="69b74-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="69b74-116">Este guia pressupõe que a tabela tem o mesmo esquema das tabelas desses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="69b74-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="69b74-117">Este guia também pressupõe que você adicionou o Plug-in do Apache Cordova ao seu código.</span><span class="sxs-lookup"><span data-stu-id="69b74-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="69b74-118">Se você não tiver feito isso, poderá adicionar o plug-in do Apache Cordova ao seu projeto na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="69b74-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="69b74-119">Para saber mais sobre como criar [seu primeiro aplicativo do Apache Cordova], consulte a documentação.</span><span class="sxs-lookup"><span data-stu-id="69b74-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="69b74-120"><a name="ionic"></a>Configurar um aplicativo Ionic v2</span><span class="sxs-lookup"><span data-stu-id="69b74-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="69b74-121">Para configurar corretamente um projeto Ionic v2, primeiro crie um aplicativo básico e adicione o plug-in Cordova:</span><span class="sxs-lookup"><span data-stu-id="69b74-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="69b74-122">Adicione as seguintes linhas a `app.component.ts` para criar o objeto de cliente:</span><span class="sxs-lookup"><span data-stu-id="69b74-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="69b74-123">Agora, você pode criar e executar o projeto no navegador:</span><span class="sxs-lookup"><span data-stu-id="69b74-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="69b74-124">O plug-in Cordova para Aplicativos Móveis do Azure dá suporte a aplicativos Ionic v1 e v2.</span><span class="sxs-lookup"><span data-stu-id="69b74-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="69b74-125">Somente os aplicativos Ionic v2 exigem a declaração adicional para o objeto `WindowsAzure`.</span><span class="sxs-lookup"><span data-stu-id="69b74-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="69b74-126"><a name="auth"></a>Como autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="69b74-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="69b74-127">O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="69b74-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="69b74-128">Você pode definir permissões em tabelas para restringir o acesso a operações específicas apenas para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="69b74-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="69b74-129">Você também pode usar a identidade de usuários autenticados para implementar regras de autorização em scripts do servidor.</span><span class="sxs-lookup"><span data-stu-id="69b74-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="69b74-130">Para obter mais informações, consulte o tutorial [Introdução à autenticação] .</span><span class="sxs-lookup"><span data-stu-id="69b74-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="69b74-131">Ao usar a autenticação em um aplicativo Apache Cordova, os seguintes plugins Cordova devem estar disponíveis:</span><span class="sxs-lookup"><span data-stu-id="69b74-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="69b74-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="69b74-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="69b74-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="69b74-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="69b74-134">Dois fluxos de autenticação são suportados: um server flow e um client flow.</span><span class="sxs-lookup"><span data-stu-id="69b74-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="69b74-135">O fluxo de servidor fornece a experiência de autenticação mais simples, pois depende da interface de autenticação da web do provedor.</span><span class="sxs-lookup"><span data-stu-id="69b74-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="69b74-136">O fluxo de cliente permite uma integração mais profunda com recursos específicos do dispositivo, como logon único, uma vez que depende de provedores específicos e SDKs específicos do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69b74-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="69b74-137"><a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.</span><span class="sxs-lookup"><span data-stu-id="69b74-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="69b74-138">Vários tipos de aplicativos do Apache Cordova usam uma funcionalidade de loopback para manipular fluxos de Interface do usuário do OAuth.</span><span class="sxs-lookup"><span data-stu-id="69b74-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="69b74-139">Fluxos de interface do usuário OAuth causam problemas, pois o serviço de autenticação só sabe utilizar seu serviço por padrão.</span><span class="sxs-lookup"><span data-stu-id="69b74-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="69b74-140">Exemplos de fluxos de interface do usuário OAuth problemáticos incluem:</span><span class="sxs-lookup"><span data-stu-id="69b74-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="69b74-141">O emulador Ripple.</span><span class="sxs-lookup"><span data-stu-id="69b74-141">The Ripple emulator.</span></span>
* <span data-ttu-id="69b74-142">Recarregamento dinâmico com Ionic.</span><span class="sxs-lookup"><span data-stu-id="69b74-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="69b74-143">Executando o back-end móvel localmente</span><span class="sxs-lookup"><span data-stu-id="69b74-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="69b74-144">A execução do back-end móvel em um Serviço de Aplicativo do Azure diferente que forneceu a autenticação.</span><span class="sxs-lookup"><span data-stu-id="69b74-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="69b74-145">Siga estas instruções para adicionar as definições locais à configuração:</span><span class="sxs-lookup"><span data-stu-id="69b74-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="69b74-146">Faça logon no [Portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="69b74-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="69b74-147">Selecione **Todos os recursos** ou **Serviços de Aplicativos** e clique no nome do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="69b74-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="69b74-148">Clique em **Ferramentas**</span><span class="sxs-lookup"><span data-stu-id="69b74-148">Click **Tools**</span></span>
4. <span data-ttu-id="69b74-149">Clique em **Gerenciador de Recursos** no menu OBSERVAR e clique em **Ir**.</span><span class="sxs-lookup"><span data-stu-id="69b74-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="69b74-150">Uma nova janela ou guia é aberta.</span><span class="sxs-lookup"><span data-stu-id="69b74-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="69b74-151">Expanda os nós **config**, **authsettings** do seu site no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="69b74-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="69b74-152">Clique em **Editar**</span><span class="sxs-lookup"><span data-stu-id="69b74-152">Click **Edit**</span></span>
7. <span data-ttu-id="69b74-153">Procure o elemento "allowedExternalRedirectUrls".</span><span class="sxs-lookup"><span data-stu-id="69b74-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="69b74-154">Ele pode ser definido como nulo ou uma matriz de valores.</span><span class="sxs-lookup"><span data-stu-id="69b74-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="69b74-155">Altere o valor para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="69b74-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="69b74-156">Substitua as URLs pelas URLs do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="69b74-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="69b74-157">Exemplos incluem "http://localhost:3000" (para o serviço de exemplo do Node.js) ou "http://localhost:4400" (para o serviço Ripple).</span><span class="sxs-lookup"><span data-stu-id="69b74-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="69b74-158">No entanto, essas URLs são exemplos – sua situação, incluindo para os serviços mencionados nos exemplos, pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="69b74-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="69b74-159">Clique no botão **Leitura/Gravação** no canto superior direito da tela.</span><span class="sxs-lookup"><span data-stu-id="69b74-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="69b74-160">Clique no botão verde **PUT** .</span><span class="sxs-lookup"><span data-stu-id="69b74-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="69b74-161">As configurações são salvas neste momento.</span><span class="sxs-lookup"><span data-stu-id="69b74-161">The settings are saved at this point.</span></span>  <span data-ttu-id="69b74-162">Não feche a janela do navegador até que as configurações sejam salvas.</span><span class="sxs-lookup"><span data-stu-id="69b74-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="69b74-163">Além disso, adicione essas URLs de loopback às configurações de CORS para o Serviço de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="69b74-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="69b74-164">Faça logon no [Portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="69b74-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="69b74-165">Selecione **Todos os recursos** ou **Serviços de Aplicativos** e clique no nome do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="69b74-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="69b74-166">A folha Configurações abre automaticamente.</span><span class="sxs-lookup"><span data-stu-id="69b74-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="69b74-167">Se não for, clique em **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="69b74-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="69b74-168">Clique em **CORS** no menu de API.</span><span class="sxs-lookup"><span data-stu-id="69b74-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="69b74-169">Digite a URL que você deseja adicionar na caixa fornecida e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="69b74-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="69b74-170">Insira URLs adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="69b74-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="69b74-171">Clique em **Salvar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="69b74-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="69b74-172">É necessário cerca de 10 a 15 segundos para que as novas configurações tenham efeito.</span><span class="sxs-lookup"><span data-stu-id="69b74-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="69b74-173"><a name="register-for-push"></a>Como registrar notificações por push</span><span class="sxs-lookup"><span data-stu-id="69b74-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="69b74-174">Instale o [phonegap-plugin-push] para manipular notificações por push.</span><span class="sxs-lookup"><span data-stu-id="69b74-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="69b74-175">Esse plug-in pode ser facilmente adicionado usando o comando `cordova plugin add` na linha de comando ou por meio do instalador de plug-ins do Git no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69b74-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="69b74-176">O código a seguir em seu aplicativo Apache Cordova registra seu dispositivo para notificações por push:</span><span class="sxs-lookup"><span data-stu-id="69b74-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="69b74-177">Use o SDK dos Hubs de Notificação para enviar notificações por push do servidor.</span><span class="sxs-lookup"><span data-stu-id="69b74-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="69b74-178">Nunca envie notificações por push diretamente dos clientes.</span><span class="sxs-lookup"><span data-stu-id="69b74-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="69b74-179">Isso pode ser usado para disparar um ataque de negação de serviço contra os Hubs de Notificação ou o PNS.</span><span class="sxs-lookup"><span data-stu-id="69b74-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="69b74-180">O PNS pode proibir o tráfego como resultado desses ataques.</span><span class="sxs-lookup"><span data-stu-id="69b74-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="69b74-181">Mais informações</span><span class="sxs-lookup"><span data-stu-id="69b74-181">More information</span></span>

<span data-ttu-id="69b74-182">Você pode encontrar detalhes de API detalhadas em nossa [Documentação da API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="69b74-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="69b74-183">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="69b74-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="69b74-184">[Início Rápido dos Aplicativos Móveis do Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="69b74-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="69b74-185">[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="69b74-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="69b74-186">[Plug-in do Apache Cordova para os Aplicativos Móveis do Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="69b74-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="69b74-187">[seu primeiro aplicativo do Apache Cordova]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="69b74-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="69b74-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="69b74-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="69b74-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="69b74-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="69b74-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="69b74-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
