---
title: "Adicionar uma CDN a um Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Adicione uma rede de distribuição de conteúdo (CDN) para um serviço de aplicativo do Azure para armazenar em cache e entregar os arquivos estáticos de servidores perto de seus clientes em todo o mundo."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="b661a-103">Como adicionar uma Rede de distribuição de conteúdo (CDN) em um Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="b661a-104">[A Rede de distribuição de conteúdo (CDN) do Azure](../cdn/cdn-overview.md) armazena em cache conteúdo Web estático em locais estrategicamente posicionados para fornecer uma taxa de transferência máxima para a distribuição de conteúdo aos usuários.</span><span class="sxs-lookup"><span data-stu-id="b661a-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="b661a-105">O CDN também reduz a carga do servidor no seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b661a-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="b661a-106">Este tutorial mostra como adicionar o CDN do Azure para um [aplicativo web no serviço de aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="b661a-107">Segue a home page do site de exemplo estático em HTML que você usará para trabalhar:</span><span class="sxs-lookup"><span data-stu-id="b661a-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="b661a-109">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="b661a-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b661a-110">Criar um novo ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="b661a-111">Atualizar ativos em cache.</span><span class="sxs-lookup"><span data-stu-id="b661a-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="b661a-112">Usar cadeias de caracteres de consulta para controlar versões armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="b661a-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="b661a-113">Usar um domínio personalizado para o ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b661a-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b661a-114">Prerequisites</span></span>

<span data-ttu-id="b661a-115">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="b661a-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="b661a-116">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="b661a-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="b661a-117">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="b661a-118">Criar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b661a-118">Create the web app</span></span>

<span data-ttu-id="b661a-119">Para criar o aplicativo Web com que você trabalhará, execute o [Início rápido HTML estático](app-service-web-get-started-html.md) na etapa **Navegar até o aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b661a-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="b661a-120">Tenha um domínio personalizado pronto</span><span class="sxs-lookup"><span data-stu-id="b661a-120">Have a custom domain ready</span></span>

<span data-ttu-id="b661a-121">Para concluir a etapa de domínio personalizado deste tutorial, você precisa possuir um domínio personalizado e ter acesso ao registro DNS do seu provedor de domínio (como GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="b661a-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="b661a-122">Por exemplo, para adicionar entradas DNS para `contoso.com` e `www.contoso.com`, você deve ter acesso para definir as configurações de DNS para o `contoso.com` domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="b661a-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="b661a-123">Se você ainda não tiver um domínio de nome, considere concluir o [Tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) para adquirir um domínio usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b661a-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="b661a-124">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-124">Log in to the Azure portal</span></span>

<span data-ttu-id="b661a-125">Abra um navegador e navegue até o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b661a-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="b661a-126">Como criar um perfil do CDN e um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="b661a-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="b661a-127">No painel de navegação esquerdo, selecione **Serviços de aplicativos** e, em seguida, selecione o aplicativo que você criou no [Início rápido do HTML estático](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Selecione o aplicativo de serviço de aplicativo no portal](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="b661a-129">Na página **Serviço de aplicativo**, na seção **Configurações**, selecione **Rede > Configurar CDN do Azure para seu aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b661a-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Selecione CDN no portal](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="b661a-131">Na página da **Rede de distribuição de conteúdo do Azure**, forneça as configurações do **ponto de extremidade novo** conforme especificado na tabela.</span><span class="sxs-lookup"><span data-stu-id="b661a-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Como criar perfil e o ponto de extremidade no portal](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="b661a-133">Configuração</span><span class="sxs-lookup"><span data-stu-id="b661a-133">Setting</span></span> | <span data-ttu-id="b661a-134">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="b661a-134">Suggested value</span></span> | <span data-ttu-id="b661a-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="b661a-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="b661a-136">**Perfil do CDN**</span><span class="sxs-lookup"><span data-stu-id="b661a-136">**CDN profile**</span></span> | <span data-ttu-id="b661a-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="b661a-137">myCDNProfile</span></span> | <span data-ttu-id="b661a-138">Selecione **Criar novo** para criar um perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="b661a-139">Um perfil do CDN é uma coleção de pontos de extremidade do CDN com o mesmo tipo de preços.</span><span class="sxs-lookup"><span data-stu-id="b661a-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="b661a-140">**Tipo de preços**</span><span class="sxs-lookup"><span data-stu-id="b661a-140">**Pricing tier**</span></span> | <span data-ttu-id="b661a-141">Akamai Standard</span><span class="sxs-lookup"><span data-stu-id="b661a-141">Standard Akamai</span></span> | <span data-ttu-id="b661a-142">O [tipo de preços](../cdn/cdn-overview.md#azure-cdn-features) especifica o provedor e os recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b661a-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="b661a-143">Neste tutorial, estamos usando o Akamai padrão.</span><span class="sxs-lookup"><span data-stu-id="b661a-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="b661a-144">**Nome do ponto de extremidade do CDN**</span><span class="sxs-lookup"><span data-stu-id="b661a-144">**CDN endpoint name**</span></span> | <span data-ttu-id="b661a-145">Qualquer nome que seja exclusivo no domínio azureedge.net</span><span class="sxs-lookup"><span data-stu-id="b661a-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="b661a-146">Acesse os recursos armazenados em cache no domínio  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="b661a-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="b661a-147">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b661a-147">Select **Create**.</span></span>

<span data-ttu-id="b661a-148">O Azure cria o perfil e o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b661a-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="b661a-149">O ponto de extremidade novo aparece na lista de **pontos de extremidade** na mesma página e, quando ele tiver provisionado, o status será **Executando**.</span><span class="sxs-lookup"><span data-stu-id="b661a-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Ponto de extremidade novo na lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="b661a-151">Testar o ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="b661a-151">Test the CDN endpoint</span></span>

<span data-ttu-id="b661a-152">Se você selecionou o tipo de preços da Verizon, normalmente demora cerca de 90 minutos para a propagação de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b661a-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="b661a-153">Para Akamai, leva alguns minutos para ocorrer a propagação</span><span class="sxs-lookup"><span data-stu-id="b661a-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="b661a-154">O aplicativo de exemplo possui um arquivo `index.html` e as pastas *css*, *img* e *js* que contêm outros ativos estáticos.</span><span class="sxs-lookup"><span data-stu-id="b661a-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="b661a-155">Os caminhos de conteúdo para todos esses arquivos são os mesmos no ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="b661a-156">Por exemplo, as duas URLs a seguir acessam o arquivo *bootstrap.css* na pasta *css*:</span><span class="sxs-lookup"><span data-stu-id="b661a-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="b661a-157">Navegue em um navegador até a URL abaixo:</span><span class="sxs-lookup"><span data-stu-id="b661a-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Home page do aplicativo de exemplo distribuídos a partir do CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="b661a-159">Consulte a mesma página que você executou anteriormente em um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="b661a-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="b661a-160">A CDN do Azure recuperou os ativos do aplicativo web de origem e está servindo-os do ponto de extremidade da CDN</span><span class="sxs-lookup"><span data-stu-id="b661a-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="b661a-161">Para garantir que essa página está armazenada em cache no CDN, atualize a página.</span><span class="sxs-lookup"><span data-stu-id="b661a-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="b661a-162">Duas solicitações para o mesmo ativo, às vezes, são necessárias para que o CDN armazene em cache o conteúdo solicitado.</span><span class="sxs-lookup"><span data-stu-id="b661a-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="b661a-163">Para obter mais informações sobre como criar perfis do CDN do Azure e pontos de extremidade, confira [Introdução ao CDN do Azure](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="b661a-164">Limpar o CDN</span><span class="sxs-lookup"><span data-stu-id="b661a-164">Purge the CDN</span></span>

<span data-ttu-id="b661a-165">O CDN atualiza periodicamente seus recursos do aplicativo web de origem com base na configuração de tempo de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="b661a-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="b661a-166">A TTL padrão é de sete dias.</span><span class="sxs-lookup"><span data-stu-id="b661a-166">The default TTL is seven days.</span></span>

<span data-ttu-id="b661a-167">Às vezes você precisará atualizar o CDN antes da expiração do TTL, por exemplo, quando você implanta o conteúdo atualizado para o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b661a-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="b661a-168">Para disparar uma atualização, você pode limpar manualmente os recursos do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="b661a-169">Nesta seção do tutorial, você implanta uma alteração para o aplicativo web e limpa o CDN para disparar o CDN para que ele atualize seu cache.</span><span class="sxs-lookup"><span data-stu-id="b661a-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="b661a-170">Implantar uma alteração no aplicativo web</span><span class="sxs-lookup"><span data-stu-id="b661a-170">Deploy a change to the web app</span></span>

<span data-ttu-id="b661a-171">Abra o arquivo `index.html` e adicione "-V2" para o título H1, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b661a-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="b661a-172">Confirme as alterações para implantá-las no aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b661a-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="b661a-173">Depois de concluir a implantação, navegue até a URL do aplicativo web e confira a alteração.</span><span class="sxs-lookup"><span data-stu-id="b661a-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 no título no aplicativo web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="b661a-175">Navegue até a URL de ponto de extremidade do CDN da home page, você não visualizará a alteração porque a versão armazenada em cache no CDN ainda não expirou.</span><span class="sxs-lookup"><span data-stu-id="b661a-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Nenhum V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="b661a-177">Limpar o CDN no portal</span><span class="sxs-lookup"><span data-stu-id="b661a-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="b661a-178">Para disparar o CDN para atualizar sua versão armazenada em cache, limpe o CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="b661a-179">Na navegação à esquerda do portal, selecione **Grupos de recursos** e, em seguida, selecione o grupo de recursos que você criou para seu aplicativo web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="b661a-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Escolha o grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="b661a-181">Na lista de recursos, selecione o ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-181">In the list of resources, select your CDN endpoint.</span></span>

![Selecione o ponto de extremidade](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="b661a-183">Na parte superior da página **Ponto de extremidade**, clique em **Limpar**.</span><span class="sxs-lookup"><span data-stu-id="b661a-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Selecione Limpar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="b661a-185">Digite os caminhos de conteúdo que você deseja limpar.</span><span class="sxs-lookup"><span data-stu-id="b661a-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="b661a-186">Você pode passar um caminho de arquivo completo para limpar um arquivo específico ou um segmento de caminho para limpar e atualizar o conteúdo de uma pasta.</span><span class="sxs-lookup"><span data-stu-id="b661a-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="b661a-187">Como você alterou `index.html`, certifique-se de que seja um dos caminhos.</span><span class="sxs-lookup"><span data-stu-id="b661a-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="b661a-188">Na parte inferior da página, selecione **Limpar**.</span><span class="sxs-lookup"><span data-stu-id="b661a-188">At the bottom of the page, select **Purge**.</span></span>

![Limpar página](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="b661a-190">Verifique se o CDN está atualizado</span><span class="sxs-lookup"><span data-stu-id="b661a-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="b661a-191">Aguarde até que a solicitação de limpeza conclua o processamento, normalmente demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b661a-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="b661a-192">Para conferir o status atual, selecione o ícone de sino na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="b661a-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Limpar notificação](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="b661a-194">Navegue até a URL de ponto de extremidade do CDN para `index.html`, agora você pode ver o V2 que você adicionou ao título da home page.</span><span class="sxs-lookup"><span data-stu-id="b661a-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="b661a-195">Isso mostra que o cache do CDN foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="b661a-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="b661a-197">Para obter mais informações, confira [Como limpar um ponto de extremidade do CDN do Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="b661a-198">Use cadeias de caracteres de consulta para o conteúdo da versão</span><span class="sxs-lookup"><span data-stu-id="b661a-198">Use query strings to version content</span></span>

<span data-ttu-id="b661a-199">O CDN do Azure oferece as seguintes opções de comportamento do armazenamento em cache:</span><span class="sxs-lookup"><span data-stu-id="b661a-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="b661a-200">Ignorar as cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="b661a-200">Ignore query strings</span></span>
* <span data-ttu-id="b661a-201">Ignorar o cache para cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="b661a-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="b661a-202">Armazenar em cache todas as URLs exclusivas</span><span class="sxs-lookup"><span data-stu-id="b661a-202">Cache every unique URL</span></span> 

<span data-ttu-id="b661a-203">A primeira delas é o padrão, o que significa que há apenas uma versão em cache de um ativo, independentemente da cadeia de caracteres de consulta na URL.</span><span class="sxs-lookup"><span data-stu-id="b661a-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="b661a-204">Nesta seção do tutorial, você deve alterar o comportamento do armazenamento em cache para armazenar em cache todas as URLs exclusivas.</span><span class="sxs-lookup"><span data-stu-id="b661a-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="b661a-205">Alterar o comportamento do armazenamento em cache</span><span class="sxs-lookup"><span data-stu-id="b661a-205">Change the cache behavior</span></span>

<span data-ttu-id="b661a-206">Na página do **ponto de extremidade do CDN** do portal do Azure, selecione **Cache**.</span><span class="sxs-lookup"><span data-stu-id="b661a-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="b661a-207">Selecione **Armazenar em cache todas as URLs exclusivas** na lista suspensa do **comportamento do armazenamento em cache da cadeia de caracteres de consulta**.</span><span class="sxs-lookup"><span data-stu-id="b661a-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="b661a-208">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b661a-208">Select **Save**.</span></span>

![Selecione o comportamento do armazenamento em cache da cadeia de caracteres de consulta](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="b661a-210">Verifique se as URLs exclusivas são armazenadas em cache separadamente</span><span class="sxs-lookup"><span data-stu-id="b661a-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="b661a-211">Em um navegador, acesse a home page no ponto de extremidade do CDN, mas inclua uma cadeia de caracteres de consulta:</span><span class="sxs-lookup"><span data-stu-id="b661a-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="b661a-212">O CDN retorna o conteúdo do aplicativo web atual, que inclui "V2" no título.</span><span class="sxs-lookup"><span data-stu-id="b661a-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="b661a-213">Para garantir que essa página está armazenada em cache no CDN, atualize a página.</span><span class="sxs-lookup"><span data-stu-id="b661a-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="b661a-214">Abra `index.html` e altere "V2" para "V3" e implante a alteração.</span><span class="sxs-lookup"><span data-stu-id="b661a-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="b661a-215">Em um navegador, acesse a URL de ponto de extremidade do CDN com uma cadeia de caracteres de consulta nova, como `q=2`.</span><span class="sxs-lookup"><span data-stu-id="b661a-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="b661a-216">O CDN obtém o arquivo `index.html` atual e exibe "V3".</span><span class="sxs-lookup"><span data-stu-id="b661a-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="b661a-217">Mas se você navegar até o ponto de extremidade do CDN com a cadeia de caracteres de consulta `q=1`, confira "V2".</span><span class="sxs-lookup"><span data-stu-id="b661a-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 no título no CDN, cadeia de caracteres de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 no título no CDN, cadeia de caracteres de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="b661a-220">A saída mostra que cada cadeia de caracteres de consulta é tratada de maneira diferente:</span><span class="sxs-lookup"><span data-stu-id="b661a-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="b661a-221">p = 1 foi usada antes e, portanto, o conteúdo em cache é retornado (V2).</span><span class="sxs-lookup"><span data-stu-id="b661a-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="b661a-222">p = 2 é novo e, portanto, o conteúdo do aplicativo Web mais recente é recuperado e retornado (V3).</span><span class="sxs-lookup"><span data-stu-id="b661a-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="b661a-223">Para obter mais informações, confira [controle do comportamento do armazenamento em cache do CDN do Azure com cadeias de caracteres de consulta](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="b661a-224">Como mapear um domínio personalizado para um ponto de extremidade do CDN</span><span class="sxs-lookup"><span data-stu-id="b661a-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="b661a-225">Você mapeará seu domínio personalizado com o ponto de extremidade do CDN criando um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="b661a-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="b661a-226">Um Registro CNAME é um recurso do DNS que mapeia um domínio de origem a um domínio de destino.</span><span class="sxs-lookup"><span data-stu-id="b661a-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="b661a-227">Por exemplo, você pode mapear `cdn.contoso.com` ou `static.contoso.com` para `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="b661a-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="b661a-228">Se você não tiver um domínio personalizado, considere concluir o [Tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) para adquirir um domínio usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b661a-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="b661a-229">Localize o nome do host a ser usado com o CNAME</span><span class="sxs-lookup"><span data-stu-id="b661a-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="b661a-230">Na página de **Ponto de extremidade** do portal do Azure, certifique-se de que a **Visão geral** esteja selecionada na navegação esquerda e, em seguida, selecione o botão **+ domínio personalizado**, na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="b661a-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Selecione Adicionar domínio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="b661a-232">Na página **adicionar um domínio personalizado**, você pode visualizar o nome de host do ponto de extremidade para usar na criação de um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="b661a-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="b661a-233">O nome de host é derivado da sua URL de ponto de extremidade do CDN: **&lt;EndpointName>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="b661a-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Adicionar página de domínio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="b661a-235">Como configurar o CNAME com seu registrador de domínio</span><span class="sxs-lookup"><span data-stu-id="b661a-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="b661a-236">Navegue até o site do registrador do domínio e localize a seção para criar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="b661a-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="b661a-237">Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.</span><span class="sxs-lookup"><span data-stu-id="b661a-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="b661a-238">Localize a seção de gerenciamento de CNAMEs.</span><span class="sxs-lookup"><span data-stu-id="b661a-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="b661a-239">Talvez você precise acessar uma página de configurações avançadas e procurar as palavras CNAME, Alias ou Subdomínios.</span><span class="sxs-lookup"><span data-stu-id="b661a-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="b661a-240">Crie um registro CNAME que mapeia o subdomínio escolhido (por exemplo, **estático** ou **cdn**) para o **nome de host do ponto de extremidade** mostrado anteriormente no portal.</span><span class="sxs-lookup"><span data-stu-id="b661a-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="b661a-241">Digite o domínio personalizado no Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="b661a-242">Retorne à página **Adicionar domínios personalizados** e insira seu domínio personalizado, incluindo o subdomínio, na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b661a-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="b661a-243">Por exemplo, insira: `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b661a-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="b661a-244">O Azure verificará se o registro do CNAME existe para o nome de domínio que você digitou.</span><span class="sxs-lookup"><span data-stu-id="b661a-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="b661a-245">Se o CNAME estiver correto, seu domínio personalizado será validado.</span><span class="sxs-lookup"><span data-stu-id="b661a-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="b661a-246">Observe que, em alguns casos, pode levar algum tempo para que o registro CNAME se propague para servidores de nomes na Internet.</span><span class="sxs-lookup"><span data-stu-id="b661a-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="b661a-247">Se o domínio não for validado imediatamente, aguarde alguns minutos e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="b661a-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="b661a-248">Teste do domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="b661a-248">Test the custom domain</span></span>

<span data-ttu-id="b661a-249">Em um navegador, navegue até o arquivo `index.html` usando o seu domínio personalizado (por exemplo, `cdn.contoso.com/index.html`) para verificar se o resultado é o mesmo de quando você acessa `<endpointname>azureedge.net/index.html` diretamente.</span><span class="sxs-lookup"><span data-stu-id="b661a-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Home page do aplicativo de exemplo usando a URL do domínio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="b661a-251">Para obter mais informações, confira [Mapeamento do conteúdo do CDN do Azure para um domínio personalizado](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b661a-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b661a-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b661a-252">Next steps</span></span>

<span data-ttu-id="b661a-253">O que você aprendeu:</span><span class="sxs-lookup"><span data-stu-id="b661a-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b661a-254">Criar um novo ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="b661a-255">Atualizar ativos em cache.</span><span class="sxs-lookup"><span data-stu-id="b661a-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="b661a-256">Usar cadeias de caracteres de consulta para controlar versões armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="b661a-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="b661a-257">Usar um domínio personalizado para o ponto de extremidade do CDN.</span><span class="sxs-lookup"><span data-stu-id="b661a-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="b661a-258">Aprenda a otimizar o desempenho da CDN nos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b661a-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b661a-259">Melhorar o desempenho compactando os arquivos na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="b661a-260">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="b661a-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
