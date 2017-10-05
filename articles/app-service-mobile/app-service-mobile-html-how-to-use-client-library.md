---
title: "Como usar o SDK do JavaScript para os Aplicativos Móveis do Azure"
description: "Como usar o v para os Aplicativos Móveis do Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="8e61a-103">Como usar a biblioteca de cliente JavaScript para os Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="8e61a-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="8e61a-104">Este guia ensina a executar cenários comuns usando o mais recente [SDK do JavaScript para os Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="8e61a-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="8e61a-105">Se não estiver familiarizado com os Aplicativos Móveis do Azure, primeiro conclua o [Início Rápido dos Aplicativos Móveis do Azure] para criar um back-end e uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8e61a-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="8e61a-106">Neste guia, vamos nos concentrar no uso do back-end móvel em aplicativos Web em HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8e61a-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="8e61a-107">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="8e61a-107">Supported platforms</span></span>
<span data-ttu-id="8e61a-108">Limitamos o suporte de navegador às versões atuais e mais recentes dos principais navegadores: Google Chrome, Microsoft Edge, Microsoft Internet Explorer e Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="8e61a-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="8e61a-109">Esperamos que o SDK funcione com todos os navegadores relativamente modernos.</span><span class="sxs-lookup"><span data-stu-id="8e61a-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="8e61a-110">O pacote é distribuído como um Módulo de JavaScript Universal e, portanto, ele dá suporte aos formatos AMD, CommonJS e globais.</span><span class="sxs-lookup"><span data-stu-id="8e61a-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="8e61a-111"><a name="Setup"></a>Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8e61a-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="8e61a-112">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8e61a-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="8e61a-113">Este guia pressupõe que a tabela tem o mesmo esquema das tabelas desses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="8e61a-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="8e61a-114">A instalação do SDK do JavaScript para Aplicativos Móveis do Azure pode ser feita por meio do comando `npm` :</span><span class="sxs-lookup"><span data-stu-id="8e61a-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="8e61a-115">A biblioteca também pode ser usada como um módulo ES2015, em ambientes de CommonJS como Browserify e Webpack e como uma biblioteca AMD.</span><span class="sxs-lookup"><span data-stu-id="8e61a-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="8e61a-116">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e61a-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="8e61a-117">Você também pode usar uma versão pré-criada do SDK baixando diretamente do nosso CDN:</span><span class="sxs-lookup"><span data-stu-id="8e61a-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="8e61a-118"><a name="auth"></a>Como autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="8e61a-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="8e61a-119">O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="8e61a-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="8e61a-120">Você pode definir permissões em tabelas para restringir o acesso a operações específicas apenas para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="8e61a-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="8e61a-121">Você também pode usar a identidade de usuários autenticados para implementar regras de autorização em scripts do servidor.</span><span class="sxs-lookup"><span data-stu-id="8e61a-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="8e61a-122">Para obter mais informações, consulte o tutorial [Introdução à autenticação] .</span><span class="sxs-lookup"><span data-stu-id="8e61a-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="8e61a-123">Dois fluxos de autenticação são suportados: um server flow e um client flow.</span><span class="sxs-lookup"><span data-stu-id="8e61a-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="8e61a-124">O fluxo de servidor fornece a experiência de autenticação mais simples, pois depende da interface de autenticação da web do provedor.</span><span class="sxs-lookup"><span data-stu-id="8e61a-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="8e61a-125">O fluxo de cliente permite uma integração mais profunda com funcionalidades específicas do dispositivo, como logon único, uma vez que depende de SDKs específicos do provedor.</span><span class="sxs-lookup"><span data-stu-id="8e61a-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="8e61a-126"><a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.</span><span class="sxs-lookup"><span data-stu-id="8e61a-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="8e61a-127">Vários tipos de aplicativo JavaScript usam uma funcionalidade de loopback para manipular fluxos de interface do usuário do OAuth.</span><span class="sxs-lookup"><span data-stu-id="8e61a-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="8e61a-128">Esses recursos incluem:</span><span class="sxs-lookup"><span data-stu-id="8e61a-128">These capabilities include:</span></span>

* <span data-ttu-id="8e61a-129">Executar o serviço localmente</span><span class="sxs-lookup"><span data-stu-id="8e61a-129">Running your service locally</span></span>
* <span data-ttu-id="8e61a-130">Usar o Live Reload com o Ionic Framework</span><span class="sxs-lookup"><span data-stu-id="8e61a-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="8e61a-131">Redirecionar para o Serviço de Aplicativo para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8e61a-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="8e61a-132">A execução local pode causar problemas porque, por padrão, a autenticação de Serviço de Aplicativo só está configurada para permitir o acesso do back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="8e61a-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="8e61a-133">Use as seguintes etapas para alterar as configurações de Serviço de Aplicativo de modo a habilitar a autenticação ao executar o servidor localmente:</span><span class="sxs-lookup"><span data-stu-id="8e61a-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="8e61a-134">Faça logon no [Portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="8e61a-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="8e61a-135">Navegue até o back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="8e61a-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="8e61a-136">Escolha **Gerenciador de recursos** no menu **FERRAMENTAS DE DESENVOLVIMENTO**.</span><span class="sxs-lookup"><span data-stu-id="8e61a-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="8e61a-137">Clique em **Ir** para abrir o gerenciador de recursos para o back-end do Aplicativo Móvel em uma nova janela ou guia.</span><span class="sxs-lookup"><span data-stu-id="8e61a-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="8e61a-138">Expanda o nó **config** > **authsettings** do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e61a-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="8e61a-139">Clique no botão **Editar** para habilitar a edição do recurso.</span><span class="sxs-lookup"><span data-stu-id="8e61a-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="8e61a-140">Encontre o elemento **allowedExternalRedirectUrls** , que deve ser nulo.</span><span class="sxs-lookup"><span data-stu-id="8e61a-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="8e61a-141">Adicione as URLs em uma matriz:</span><span class="sxs-lookup"><span data-stu-id="8e61a-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="8e61a-142">Substitua as URLs na matriz pelas URLs do serviço, que neste exemplo é `http://localhost:3000` para o serviço local de exemplo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="8e61a-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="8e61a-143">Você também pode usar `http://localhost:4400` para o serviço Ripple ou alguma outra URL, dependendo de como seu aplicativo é configurado.</span><span class="sxs-lookup"><span data-stu-id="8e61a-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="8e61a-144">Na parte superior da página, clique em **Leitura/Gravação** e clique em **PUT** para salvar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="8e61a-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="8e61a-145">Você também precisa adicionar as mesmas URLs de loopback às configurações de lista branca do CORS:</span><span class="sxs-lookup"><span data-stu-id="8e61a-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="8e61a-146">Navegue até o [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="8e61a-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="8e61a-147">Navegue até o back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="8e61a-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="8e61a-148">Clique em **CORS** no menu **API**.</span><span class="sxs-lookup"><span data-stu-id="8e61a-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="8e61a-149">Insira cada URL na caixa de texto **Origens Permitidas** vazia.</span><span class="sxs-lookup"><span data-stu-id="8e61a-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="8e61a-150">Uma nova caixa de texto é criada.</span><span class="sxs-lookup"><span data-stu-id="8e61a-150">A new text box is created.</span></span>
5. <span data-ttu-id="8e61a-151">Clique em **SALVAR**</span><span class="sxs-lookup"><span data-stu-id="8e61a-151">Click **SAVE**</span></span>

<span data-ttu-id="8e61a-152">Após a atualização do back-end, você poderá usar as novas URLs de loopback em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e61a-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="8e61a-153">[Início Rápido dos Aplicativos Móveis do Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="8e61a-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="8e61a-154">[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="8e61a-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="8e61a-155">[Portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="8e61a-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="8e61a-156">[SDK do JavaScript para os Aplicativos Móveis do Azure]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="8e61a-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
