---
title: "aaaAdd tooan um CDN do serviço de aplicativo do Azure | Microsoft Docs"
description: "Adicionar um toocache de serviço de aplicativo do Azure Content Delivery Network (CDN) tooan e entregar seus arquivos estáticos de servidores clientes tooyour Fechar ao redor Olá, mundo."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="aabbc-103">Adicionar uma tooan de rede de fornecimento de conteúdo (CDN) do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="aabbc-104">[Rede de fornecimento de conteúdo do Azure (CDN)](../cdn/cdn-overview.md) armazena em cache o conteúdo estático da web em locais estrategicamente colocados tooprovide taxa de transferência máxima para entregar conteúdo toousers.</span><span class="sxs-lookup"><span data-stu-id="aabbc-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="aabbc-105">Olá CDN também reduz a carga do servidor em seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="aabbc-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="aabbc-106">Este tutorial mostra como tooadd Azure CDN tooa [aplicativo web no serviço de aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="aabbc-107">Aqui está o hello home page do hello exemplo site HTML estático que você trabalhará com:</span><span class="sxs-lookup"><span data-stu-id="aabbc-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="aabbc-109">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="aabbc-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aabbc-110">Criar um novo ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="aabbc-111">Atualizar ativos em cache.</span><span class="sxs-lookup"><span data-stu-id="aabbc-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="aabbc-112">Usar consulta de cadeias de caracteres versões toocontrol armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="aabbc-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="aabbc-113">Use um domínio personalizado para o ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aabbc-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aabbc-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aabbc-114">Prerequisites</span></span>

<span data-ttu-id="aabbc-115">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="aabbc-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="aabbc-116">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="aabbc-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="aabbc-117">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="aabbc-118">Criar aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="aabbc-118">Create hello web app</span></span>

<span data-ttu-id="aabbc-119">aplicativo web do toocreate Olá que você trabalhará com hello siga [início rápido HTML estático](app-service-web-get-started-html.md) por meio de saudação **procurar toohello aplicativo** etapa.</span><span class="sxs-lookup"><span data-stu-id="aabbc-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="aabbc-120">Tenha um domínio personalizado pronto</span><span class="sxs-lookup"><span data-stu-id="aabbc-120">Have a custom domain ready</span></span>

<span data-ttu-id="aabbc-121">etapa de domínio personalizado Olá toocomplete deste tutorial, você precisa tooown um domínio personalizado e ter acessar tooyour o registro DNS para o seu provedor de domínio (como GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="aabbc-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="aabbc-122">Por exemplo, as entradas DNS tooadd para `contoso.com` e `www.contoso.com`, você deve ter acesso tooconfigure Olá as configurações de DNS para Olá `contoso.com` domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="aabbc-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="aabbc-123">Se você ainda não tiver um nome de domínio, considere a seguir Olá [tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) toopurchase usando um domínio Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aabbc-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="aabbc-124">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="aabbc-125">Abra um navegador e navegue toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aabbc-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="aabbc-126">Como criar um perfil do CDN e um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="aabbc-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="aabbc-127">No hello barra de navegação esquerda, selecione **serviços de aplicativos**e em seguida, selecione o aplicativo hello que você criou no hello [início rápido HTML estático](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Selecione o aplicativo de serviço de aplicativo no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="aabbc-129">Em Olá **do serviço de aplicativo** página Olá **configurações** seção, selecione **rede > configurar o Azure CDN para seu aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Selecione a CDN no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="aabbc-131">Em Olá **rede de fornecimento de conteúdo do Azure** , forneça Olá **novo ponto de extremidade** configurações conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Criar perfil e o ponto de extremidade no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="aabbc-133">Configuração</span><span class="sxs-lookup"><span data-stu-id="aabbc-133">Setting</span></span> | <span data-ttu-id="aabbc-134">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="aabbc-134">Suggested value</span></span> | <span data-ttu-id="aabbc-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="aabbc-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="aabbc-136">**Perfil do CDN**</span><span class="sxs-lookup"><span data-stu-id="aabbc-136">**CDN profile**</span></span> | <span data-ttu-id="aabbc-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="aabbc-137">myCDNProfile</span></span> | <span data-ttu-id="aabbc-138">Selecione **criar novo** toocreate perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="aabbc-139">Perfil CDN é uma coleção de pontos de extremidade CDN com hello mesma camada de preços.</span><span class="sxs-lookup"><span data-stu-id="aabbc-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="aabbc-140">**Tipo de preços**</span><span class="sxs-lookup"><span data-stu-id="aabbc-140">**Pricing tier**</span></span> | <span data-ttu-id="aabbc-141">Akamai Standard</span><span class="sxs-lookup"><span data-stu-id="aabbc-141">Standard Akamai</span></span> | <span data-ttu-id="aabbc-142">Olá [preço](../cdn/cdn-overview.md#azure-cdn-features) Especifica o provedor de saudação e recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aabbc-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="aabbc-143">Neste tutorial, estamos usando o Akamai padrão.</span><span class="sxs-lookup"><span data-stu-id="aabbc-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="aabbc-144">**Nome do ponto de extremidade do CDN**</span><span class="sxs-lookup"><span data-stu-id="aabbc-144">**CDN endpoint name**</span></span> | <span data-ttu-id="aabbc-145">Qualquer nome que seja exclusivo no domínio de azureedge.net Olá</span><span class="sxs-lookup"><span data-stu-id="aabbc-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="aabbc-146">Acessar os recursos armazenados em cache no domínio Olá  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="aabbc-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="aabbc-147">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-147">Select **Create**.</span></span>

<span data-ttu-id="aabbc-148">O Azure cria o ponto de extremidade e perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="aabbc-149">novo ponto de extremidade de saudação aparece no hello **pontos de extremidade** lista Olá a mesma página, e quando ela é provisionada status Olá é **executando**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Ponto de extremidade novo na lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="aabbc-151">Saudação de teste ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="aabbc-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="aabbc-152">Se você selecionou o tipo de preços da Verizon, normalmente demora cerca de 90 minutos para a propagação de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="aabbc-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="aabbc-153">Para Akamai, leva alguns minutos para ocorrer a propagação</span><span class="sxs-lookup"><span data-stu-id="aabbc-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="aabbc-154">aplicativo de exemplo Hello tem um `index.html` arquivo e *css*, *img*, e *js* pastas que contêm outros ativos estáticos.</span><span class="sxs-lookup"><span data-stu-id="aabbc-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="aabbc-155">Olá conteúdo de caminhos para todos esses arquivos são Olá mesmo ponto de extremidade de CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aabbc-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="aabbc-156">Por exemplo, ambos Olá seguintes URLs acessam Olá *bootstrap.css* arquivo hello *css* pasta:</span><span class="sxs-lookup"><span data-stu-id="aabbc-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="aabbc-157">Navegue até um toohello de navegador a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="aabbc-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Home page do aplicativo de exemplo distribuídos a partir do CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="aabbc-159">Você verá Olá mesma página que você executou anteriormente em um aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="aabbc-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="aabbc-160">CDN do Azure recuperou ativos do aplicativo de web para a origem hello e está servindo-los do ponto de extremidade CDN Olá</span><span class="sxs-lookup"><span data-stu-id="aabbc-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="aabbc-161">tooensure que esta página é armazenada em cache no hello CDN, página de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="aabbc-162">Duas solicitações para hello mesmo ativo às vezes são necessárias para CDN toocache Olá Olá conteúdo solicitado.</span><span class="sxs-lookup"><span data-stu-id="aabbc-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="aabbc-163">Para obter mais informações sobre como criar perfis do CDN do Azure e pontos de extremidade, confira [Introdução ao CDN do Azure](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="aabbc-164">Limpar Olá CDN</span><span class="sxs-lookup"><span data-stu-id="aabbc-164">Purge hello CDN</span></span>

<span data-ttu-id="aabbc-165">Olá CDN atualiza periodicamente seus recursos do aplicativo de web de origem Olá com base na configuração do hello time-to-live (TTL).</span><span class="sxs-lookup"><span data-stu-id="aabbc-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="aabbc-166">TTL padrão de saudação é de sete dias.</span><span class="sxs-lookup"><span data-stu-id="aabbc-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="aabbc-167">Às vezes pode ser necessário toorefresh Olá CDN antes Olá expiração do tempo de vida – por exemplo, quando você implanta o aplicativo da web de toohello conteúdo atualizado.</span><span class="sxs-lookup"><span data-stu-id="aabbc-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="aabbc-168">tootrigger uma atualização, você pode limpar manualmente recursos CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aabbc-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="aabbc-169">Nesta seção do tutorial hello, implantar um aplicativo da web toohello alteração e limpar Olá CDN tootrigger Olá CDN toorefresh seu cache.</span><span class="sxs-lookup"><span data-stu-id="aabbc-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="aabbc-170">Implantar um aplicativo de web de toohello de alteração</span><span class="sxs-lookup"><span data-stu-id="aabbc-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="aabbc-171">Olá abra `index.html` e adicione "-V2" toohello H1 título, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="aabbc-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="aabbc-172">Confirmar suas alterações e implantá-lo toohello web app.</span><span class="sxs-lookup"><span data-stu-id="aabbc-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="aabbc-173">Depois que a implantação for concluída, a URL de aplicativo de web toohello procurar e você verá Olá alterar.</span><span class="sxs-lookup"><span data-stu-id="aabbc-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 no título no aplicativo web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="aabbc-175">Procurar toohello URL de ponto de extremidade CDN para a home page do hello e você não vir Olá alterar porque a versão armazenada em cache Olá no hello CDN ainda não expirou.</span><span class="sxs-lookup"><span data-stu-id="aabbc-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Nenhum V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="aabbc-177">Limpar Olá CDN no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="aabbc-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="aabbc-178">tootrigger Olá CDN tooupdate sua versão armazenada em cache, limpe Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="aabbc-179">No hello portal de navegação esquerdo, selecione **grupos de recursos**e, em seguida, selecione o grupo de recursos de saudação que você criou para seu aplicativo web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="aabbc-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Escolha o grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="aabbc-181">Na lista de saudação de recursos, selecione o ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-181">In hello list of resources, select your CDN endpoint.</span></span>

![Selecione o ponto de extremidade](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="aabbc-183">Na parte superior de saudação do hello **ponto de extremidade** , clique em **limpar**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Selecione Limpar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="aabbc-185">Insira os caminhos de conteúdo Olá desejar toopurge.</span><span class="sxs-lookup"><span data-stu-id="aabbc-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="aabbc-186">Você pode passar um toopurge de caminho de arquivo completo de um arquivo individual ou um toopurge de segmento de caminho e atualizar todo o conteúdo em uma pasta.</span><span class="sxs-lookup"><span data-stu-id="aabbc-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="aabbc-187">Como você alterou `index.html`, certifique-se de que é um dos caminhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="aabbc-188">Final Olá Olá página, selecione **limpar**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-188">At hello bottom of hello page, select **Purge**.</span></span>

![Limpar página](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="aabbc-190">Verifique se esse Olá que CDN é atualizada</span><span class="sxs-lookup"><span data-stu-id="aabbc-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="aabbc-191">Aguarde até que a solicitação de limpeza Olá termina de processar, normalmente de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="aabbc-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="aabbc-192">toosee Olá o status atual, ícone de sino Olá select na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Limpar notificação](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="aabbc-194">Procurar toohello URL de ponto de extremidade CDN para `index.html`, e agora você verá Olá V2 que você adicionou toohello título na home page do hello.</span><span class="sxs-lookup"><span data-stu-id="aabbc-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="aabbc-195">Isso mostra que o cache CDN Olá foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="aabbc-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="aabbc-197">Para obter mais informações, confira [Como limpar um ponto de extremidade do CDN do Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="aabbc-198">Usar o conteúdo de tooversion de cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="aabbc-198">Use query strings tooversion content</span></span>

<span data-ttu-id="aabbc-199">Olá CDN do Azure oferece Olá cache comportamento as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="aabbc-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="aabbc-200">Ignorar as cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="aabbc-200">Ignore query strings</span></span>
* <span data-ttu-id="aabbc-201">Ignorar o cache para cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="aabbc-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="aabbc-202">Armazenar em cache todas as URLs exclusivas</span><span class="sxs-lookup"><span data-stu-id="aabbc-202">Cache every unique URL</span></span> 

<span data-ttu-id="aabbc-203">Olá primeiro deles é padrão hello, o que significa que há somente uma versão em cache de um ativo, independentemente da cadeia de caracteres de consulta de Olá Olá URL.</span><span class="sxs-lookup"><span data-stu-id="aabbc-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="aabbc-204">Nesta seção do tutorial hello, você alterar Olá cache comportamento toocache todas as URLs exclusivas.</span><span class="sxs-lookup"><span data-stu-id="aabbc-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="aabbc-205">Alterar o comportamento do cache Olá</span><span class="sxs-lookup"><span data-stu-id="aabbc-205">Change hello cache behavior</span></span>

<span data-ttu-id="aabbc-206">No portal do Azure de saudação **ponto de extremidade CDN** página, selecione **Cache**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="aabbc-207">Selecione **armazenar em Cache todas as URLs exclusivas** de saudação **comportamento do cache de cadeia de consulta** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aabbc-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="aabbc-208">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-208">Select **Save**.</span></span>

![Selecione o comportamento do armazenamento em cache da cadeia de caracteres de consulta](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="aabbc-210">Verifique se as URLs exclusivas são armazenadas em cache separadamente</span><span class="sxs-lookup"><span data-stu-id="aabbc-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="aabbc-211">Em um navegador, navegue toohello home page no ponto de extremidade CDN hello, mas incluir uma cadeia de caracteres de consulta:</span><span class="sxs-lookup"><span data-stu-id="aabbc-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="aabbc-212">Olá CDN retorna Olá atual conteúdo da web app, que inclui "V2" no título da saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="aabbc-213">tooensure que esta página é armazenada em cache no hello CDN, página de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="aabbc-214">Abra `index.html` e alterar "V2" muito "V3" e implantar a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="aabbc-215">Em um navegador, vá toohello URL de ponto de extremidade CDN com uma nova cadeia de caracteres de consulta, como `q=2`.</span><span class="sxs-lookup"><span data-stu-id="aabbc-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="aabbc-216">Olá CDN obtém Olá atual `index.html` de arquivos e exibe "V3".</span><span class="sxs-lookup"><span data-stu-id="aabbc-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="aabbc-217">Porém, se você navegar toohello o ponto de extremidade CDN com hello `q=1` cadeia de caracteres, consulte "V2".</span><span class="sxs-lookup"><span data-stu-id="aabbc-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 no título no CDN, cadeia de caracteres de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 no título no CDN, cadeia de caracteres de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="aabbc-220">A saída mostra que cada cadeia de caracteres de consulta é tratada de maneira diferente:</span><span class="sxs-lookup"><span data-stu-id="aabbc-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="aabbc-221">p = 1 foi usada antes e, portanto, o conteúdo em cache é retornado (V2).</span><span class="sxs-lookup"><span data-stu-id="aabbc-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="aabbc-222">p = 2 é novo, portanto, conteúdo de aplicativo da web mais recente Olá é recuperado e retornado (V3).</span><span class="sxs-lookup"><span data-stu-id="aabbc-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="aabbc-223">Para obter mais informações, confira [controle do comportamento do armazenamento em cache do CDN do Azure com cadeias de caracteres de consulta](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="aabbc-224">Mapear um ponto de extremidade CDN do domínio personalizado tooa</span><span class="sxs-lookup"><span data-stu-id="aabbc-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="aabbc-225">Criando um registro CNAME, você vai mapear seu domínio personalizado de tooyour ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="aabbc-226">Um registro CNAME é um recurso DNS que mapeia um domínio de destino de tooa de domínio de origem.</span><span class="sxs-lookup"><span data-stu-id="aabbc-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="aabbc-227">Por exemplo, você pode mapear `cdn.contoso.com` ou `static.contoso.com` muito`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="aabbc-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="aabbc-228">Se você não tiver um domínio personalizado, considere a seguir Olá [tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) toopurchase usando um domínio Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aabbc-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="aabbc-229">Localizar Olá hostname toouse com hello CNAME</span><span class="sxs-lookup"><span data-stu-id="aabbc-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="aabbc-230">No portal do Azure de saudação **ponto de extremidade** página, certifique-se de **visão geral** está selecionado na saudação à esquerda de navegação e, em seguida, selecione hello **+ domínio personalizado** botão na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Selecione Adicionar domínio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="aabbc-232">Em Olá **adicionar um domínio personalizado** página, você verá toouse de nome de host Olá ponto de extremidade na criação de um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="aabbc-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="aabbc-233">nome de host de saudação é derivado da sua URL de ponto de extremidade CDN:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Adicionar página de domínio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="aabbc-235">Configurar Olá CNAME com seu registrador de domínio</span><span class="sxs-lookup"><span data-stu-id="aabbc-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="aabbc-236">Navegue de site do registrador de domínio tooyour e localize a seção Olá para criar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="aabbc-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="aabbc-237">Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.</span><span class="sxs-lookup"><span data-stu-id="aabbc-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="aabbc-238">Localize seção Olá para gerenciar CNAMEs.</span><span class="sxs-lookup"><span data-stu-id="aabbc-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="aabbc-239">Você pode ter a página de configurações avançadas de tooan toogo e procure palavras Olá CNAME, Alias ou subdomínios.</span><span class="sxs-lookup"><span data-stu-id="aabbc-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="aabbc-240">Criar um registro CNAME que mapeie o subdomínio escolhido (por exemplo, **estático** ou **cdn**) toohello **nome de host do ponto de extremidade** mostrado anteriormente no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="aabbc-241">Digite o domínio personalizado Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="aabbc-242">Retornar toohello **adicionar um domínio personalizado** página e, em seguida, digite seu domínio personalizado, incluindo o subdomínio hello, na caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aabbc-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="aabbc-243">Por exemplo, insira: `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aabbc-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="aabbc-244">Azure verifica se o registro CNAME Olá existe para nome de domínio Olá que você inseriu.</span><span class="sxs-lookup"><span data-stu-id="aabbc-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="aabbc-245">Se Olá CNAME estiver correto, seu domínio personalizado será validado.</span><span class="sxs-lookup"><span data-stu-id="aabbc-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="aabbc-246">Pode levar tempo para Olá CNAME toopropagate registro tooname servidores em Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="aabbc-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="aabbc-247">Se o domínio não for validado imediatamente, aguarde alguns minutos e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="aabbc-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="aabbc-248">Domínio personalizado de saudação de teste</span><span class="sxs-lookup"><span data-stu-id="aabbc-248">Test hello custom domain</span></span>

<span data-ttu-id="aabbc-249">Em um navegador, navegue toohello `index.html` arquivo usando seu domínio personalizado (por exemplo, `cdn.contoso.com/index.html`) tooverify é resultado de Olá Olá mesmo como quando você entrar diretamente muito`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="aabbc-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Home page do aplicativo de exemplo usando a URL do domínio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="aabbc-251">Para obter mais informações, consulte [domínio personalizado do mapa do Azure CDN tooa conteúdo](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aabbc-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="aabbc-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aabbc-252">Next steps</span></span>

<span data-ttu-id="aabbc-253">O que você aprendeu:</span><span class="sxs-lookup"><span data-stu-id="aabbc-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aabbc-254">Criar um novo ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="aabbc-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="aabbc-255">Atualizar ativos em cache.</span><span class="sxs-lookup"><span data-stu-id="aabbc-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="aabbc-256">Usar consulta de cadeias de caracteres versões toocontrol armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="aabbc-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="aabbc-257">Use um domínio personalizado para o ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aabbc-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="aabbc-258">Saiba como toooptimize desempenho CDN Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="aabbc-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aabbc-259">Melhorar o desempenho compactando os arquivos na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="aabbc-260">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="aabbc-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
