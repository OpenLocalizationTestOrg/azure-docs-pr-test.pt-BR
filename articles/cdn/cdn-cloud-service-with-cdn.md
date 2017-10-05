---
title: "Integrar um serviço de nuvem do Azure com a CDN do Azure | Microsoft Docs"
description: "Aprenda como implantar um serviço de nuvem que serve o conteúdo de um ponto de extremidade CDN do Azure integrado"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="0ebaa-103"><a name="intro"></a> Integrar um serviço de nuvem à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="0ebaa-104">Um serviço de nuvem pode ser integrado com o CDN do Azure, fornecendo qualquer conteúdo do local do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="0ebaa-105">Esta abordagem lhe dá as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="0ebaa-106">Implantar e atualizar, de maneira fácil, imagens, scripts e folhas de estilo nos diretórios de projetos de seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="0ebaa-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="0ebaa-107">Atualizar de maneira fácil os pacotes NuGet em seu serviço de nuvem, como as versões jQuery ou Bootstrap</span><span class="sxs-lookup"><span data-stu-id="0ebaa-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="0ebaa-108">Gerenciar seu aplicativo Web e o conteúdo fornecido por CDN por meio da mesma interface do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ebaa-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="0ebaa-109">Fluxo de trabalho de implantação unificado para seu aplicativo Web e o conteúdo fornecido por CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="0ebaa-110">Integrar agrupamento e minificação ASP.NET à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0ebaa-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0ebaa-111">What you will learn</span></span>
<span data-ttu-id="0ebaa-112">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="0ebaa-113">Integrar um ponto de extremidade da CDN do Azure a seu serviço de nuvem e fornecer conteúdo estático em suas páginas Web por meio da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="0ebaa-114">Definir configurações de cache para conteúdo estático em seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="0ebaa-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="0ebaa-115">Fornecer conteúdo por ações do controlador na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="0ebaa-116">Fornecer conteúdo agrupado e minificado por meio da CDN do Azure enquanto preserva a experiência de depuração de script no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ebaa-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="0ebaa-117">Configurar o fallback de seus scripts e CSS quando a CDN do Azure estiver offline</span><span class="sxs-lookup"><span data-stu-id="0ebaa-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="0ebaa-118">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="0ebaa-118">What you will build</span></span>
<span data-ttu-id="0ebaa-119">Você implantará uma função Web de serviço de nuvem usando o modelo ASP.NET MVC padrão, adicionará código para fornecer conteúdo de uma CDN do Azure integrada, como uma imagem, resultados de ação do controlador e os arquivos JavaScript e CSS padrão, e também escreverá código para configurar o mecanismo de fallback para grupos fornecidos caso o CDN esteja offline.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="0ebaa-120">O que será necessário</span><span class="sxs-lookup"><span data-stu-id="0ebaa-120">What you will need</span></span>
<span data-ttu-id="0ebaa-121">Este tutorial tem os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="0ebaa-122">Uma [conta do Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="0ebaa-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="0ebaa-123">Visual Studio 2015 com [SDK do Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="0ebaa-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="0ebaa-124">Você de uma conta do Azure para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="0ebaa-125">Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) - Você obtém créditos que podem ser usados para experimentar serviços pagos do Azure e, mesmo após eles serem utilizados, você pode manter a conta e utilizar os serviços gratuitos do Azure, como os Sites.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="0ebaa-126">Você pode [ativar benefícios para assinantes do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Todos os meses, sua assinatura do MSDN oferece créditos que podem ser usados para serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="0ebaa-127">Implantar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="0ebaa-127">Deploy a cloud service</span></span>
<span data-ttu-id="0ebaa-128">Nesta seção, você vai implantar o modelo de aplicativo MVC ASP.NET padrão no Visual Studio 2015 para uma função de Web do serviço de nuvem e, em seguida, integrá-la a um novo ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="0ebaa-129">Siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="0ebaa-130">No Visual Studio 2015, crie um novo serviço de nuvem do Azure na barra de menu acessando **Arquivo > Novo > Projeto > Nuvem > Serviço de Nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="0ebaa-131">Dê um nome a ele e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="0ebaa-132">Selecione **Função Web ASP.NET** e clique no botão **>**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="0ebaa-133">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="0ebaa-134">Selecione **MVC** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="0ebaa-135">Agora, publique esta função Web em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="0ebaa-136">Clique com o botão direito do mouse no projeto do serviço de nuvem e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="0ebaa-137">Se você ainda não entrou no Microsoft Azure, clique em **Adicionar uma conta...** na lista suspensa e clique no item de menu **Adicionar uma conta**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="0ebaa-138">Na página de entrada, entre com a conta da Microsoft que você utilizou para ativar a conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="0ebaa-139">Após ter entrado, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="0ebaa-140">Se você ainda não tiver criado uma conta de armazenamento ou um serviço de nuvem, o Visual Studio o ajudará a criar ambos.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="0ebaa-141">Na caixa de diálogo **Criar Serviço de Nuvem e Conta** , digite o nome do serviço desejado e selecione a região desejada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="0ebaa-142">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="0ebaa-143">Na página de configurações de publicação, verifique a configuração e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="0ebaa-144">O processo de publicação para serviços de nuvem leva muito tempo.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="0ebaa-145">A opção Habilitar Implantação da Web para todas as funções pode acelerar muito a depuração do serviço de nuvem fornecendo atualizações rápidas (mas temporárias) para suas funções Web.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="0ebaa-146">Para saber mais sobre esta opção, consulte [Publicando um Serviço de Nuvem usando as Ferramentas do Azure](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="0ebaa-147">Quando o **Log de atividades do Microsoft Azure** mostrar que o status da publicação é **Concluído**, crie um ponto de extremidade CDN que esteja integrado a esse serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="0ebaa-148">Se após a publicação o serviço de nuvem implantado exibir uma tela de erro, provavelmente é porque o serviço de nuvem que você implantou está usando um [SO convidado que não inclui o .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="0ebaa-149">Você pode contornar esse problema [Implantando o .NET 4.5.2 como uma tarefa de inicialização](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="0ebaa-150">Criar um novo perfil CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-150">Create a new CDN profile</span></span>
<span data-ttu-id="0ebaa-151">Um perfil CDN é um conjunto de pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="0ebaa-152">Cada perfil contém um ou mais pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="0ebaa-153">Você pode usar vários perfis para organizar seus pontos de extremidade CDN por domínio de Internet, aplicativo Web ou algum outro critério.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="0ebaa-154">Se já tiver um perfil CDN que deseja usar para este tutorial, vá para [Criar um novo ponto de extremidade CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="0ebaa-155">Criar um novo ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="0ebaa-156">**Para criar um novo ponto de extremidade CDN para sua conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="0ebaa-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="0ebaa-157">No [Portal de Gerenciamento do Azure](https://portal.azure.com), navegue até o seu perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="0ebaa-158">Você pode ter fixado ao painel na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="0ebaa-159">Se não, você poderá encontrá-lo clicando em **Procurar**, em **Perfis CDN** e clicando no perfil ao qual você pretende adicionar o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="0ebaa-160">A folha do perfil CDN é exibida.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-160">The CDN profile blade appears.</span></span>
   
    ![Perfil CDN][cdn-profile-settings]
2. <span data-ttu-id="0ebaa-162">Clique no botão **Adicionar Ponto de Extremidade** .</span><span class="sxs-lookup"><span data-stu-id="0ebaa-162">Click the **Add Endpoint** button.</span></span>
   
    ![Adicionar botão de ponto de extremidade][cdn-new-endpoint-button]
   
    <span data-ttu-id="0ebaa-164">A folha **Adicionar um ponto de extremidade** é exibida.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Adicionar folha de ponto de extremidade][cdn-add-endpoint]
3. <span data-ttu-id="0ebaa-166">Insira um **Nome** para esse ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="0ebaa-167">Esse nome será usado para acessar os recursos armazenados em cache no domínio `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="0ebaa-168">No menu suspenso **Tipo de origem** , selecione *Serviço de nuvem*.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="0ebaa-169">No menu suspenso **Nome do host de origem** , selecione Serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="0ebaa-170">Mantenha os padrões para **Caminho de origem**, **Cabeçalho de host de origem** e **Porta de protocolo/origem**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="0ebaa-171">Você deve especificar pelo menos um protocolo (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="0ebaa-172">Clique no botão **Adicionar** para criar um novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="0ebaa-173">Depois que o ponto de extremidade é criado, ele aparece em uma lista de pontos de extremidade do perfil.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="0ebaa-174">O modo de exibição de lista mostra a URL a ser usada para acessar o conteúdo armazenado em cache, bem como o domínio de origem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![Ponto de extremidade CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="0ebaa-176">O ponto de extremidade não estará imediatamente disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="0ebaa-177">Pode levar até 90 minutos para que o registro seja propagado pela rede CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="0ebaa-178">Os usuários que tentarem usar imediatamente o nome de domínio CDN poderão receber o código de status 404 até que o conteúdo esteja disponível pela CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="0ebaa-179">Testar o ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-179">Test the CDN endpoint</span></span>
<span data-ttu-id="0ebaa-180">Quando o status da publicação for **Concluído**, abra uma janela do navegador e vá para **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="0ebaa-181">Em minha configuração, essa URL é:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="0ebaa-182">Que corresponde à seguinte URL de origem no ponto de extremidade da CDN:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="0ebaa-183">Quando você navega para **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, dependendo do navegador, receberá uma solicitação para baixar ou abrir o bootstrap.css proveniente de seu aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="0ebaa-184">De maneira semelhante, você pode acessar qualquer URL acessível publicamente em **http://*&lt;nomedoServiço>*.cloudapp.net/**, diretamente de seu ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="0ebaa-185">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-185">For example:</span></span>

* <span data-ttu-id="0ebaa-186">Um arquivo .js do caminho /Script</span><span class="sxs-lookup"><span data-stu-id="0ebaa-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="0ebaa-187">Qualquer arquivo de conteúdo do caminho /Content</span><span class="sxs-lookup"><span data-stu-id="0ebaa-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="0ebaa-188">Qualquer controller/action</span><span class="sxs-lookup"><span data-stu-id="0ebaa-188">Any controller/action</span></span>
* <span data-ttu-id="0ebaa-189">Se cadeias de consulta estiverem habilitadas em seu ponto de extremidade da CDN, qualquer URL com cadeias de consulta</span><span class="sxs-lookup"><span data-stu-id="0ebaa-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="0ebaa-190">Na verdade, com a configuração acima, você pode hospedar todo o serviço de nuvem por meio de **http://*&lt;nome_da_CDN>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="0ebaa-191">Se navegar até **http://camservice.azureedge.net/**, eu obtenho o resultado da ação de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="0ebaa-192">No entanto, isso não significa que sempre é uma boa ideia fornecer um serviço de nuvem inteiro por meio da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="0ebaa-193">Uma CDN com otimização de entrega estática não acelera, necessariamente, a entrega de ativos dinâmicos que não devem ser armazenados em cache ou são atualizados com muita frequência, pois a CDN deve efetuar pull de uma nova versão do ativo do servidor de origem com bastante frequência.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="0ebaa-194">Para este cenário, você pode habilitar a otimização [DSA](cdn-dynamic-site-acceleration.md) (aceleração de site dinâmico), em seu ponto de extremidade da CDN, que usa várias técnicas para acelerar a entrega de ativos dinâmicos não armazenáveis em cache.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="0ebaa-195">Se você tem um site com uma mistura de conteúdo estático e dinâmico, você pode escolher distribuir o conteúdo estático da CDN com um tipo de otimização estática (por exemplo, a entrega da Web geral) e distribuir o conteúdo dinâmico diretamente do servidor de origem ou por meio de um ponto de extremidade de CDN com otimização DSA ativada de acordo com cada caso.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="0ebaa-196">Para isso, você já viu como acessar arquivos de conteúdo individuais do ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="0ebaa-197">Você verá como fornecer uma ação de controlador específica por meio de um ponto de extremidade de CDN específico em Fornecer conteúdo por meio de ações do controlador na CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="0ebaa-198">A alternativa é determinar que conteúdo fornecer por meio da CDN do Azure caso a caso, em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="0ebaa-199">Para isso, você já viu como acessar arquivos de conteúdo individuais do ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="0ebaa-200">Você verá como fornecer uma ação de controlador específica por meio do ponto de extremidade CDN em [Fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure](#controller).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="0ebaa-201">Configurar opções de cache para arquivos estáticos em seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="0ebaa-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="0ebaa-202">Com a integração da CDN do Azure a seu serviço de nuvem, você pode especificar como quer que o conteúdo estático seja armazenado em cache no ponto de extremidade da CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="0ebaa-203">Para fazer isso, abra *Web.config* em seu projeto de função Web (por exemplo, FunçãodaWeb1) e adicione um elemento `<staticContent>` a `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="0ebaa-204">O XML configura o cache para expirar em 3 dias.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="0ebaa-205">Após você ter feito isso, todos os arquivos estáticos do serviço de nuvem obedecerão à mesma regra do seu cache de CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="0ebaa-206">Para ter um controle mais granular das configurações de cache, adicione um arquivo *Web.config* a uma pasta e adicione suas configurações.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="0ebaa-207">Por exemplo, adicione um arquivo *Web.config* à pasta *\Content* e substitua o conteúdo pelo seguinte XML:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="0ebaa-208">Esta configuração faz com que todos os arquivos estáticos da pasta *\Content* sejam armazenados em cache por 15 dias.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="0ebaa-209">Para saber mais sobre como configurar o elemento `<clientCache>`, consulte [Cache do cliente&lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="0ebaa-210">Em [Fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure](#controller), eu também mostrarei como você pode definir as configurações de cache para os resultados de ações do controlados no cache de CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="0ebaa-211">Fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="0ebaa-212">Quando você integra uma função Web de um serviço de nuvem à CDN do Azure, é relativamente fácil fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="0ebaa-213">Além de fornecer o serviço de nuvem diretamente da CDN do Azure (demonstrado acima), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra como fazer isso com um divertido controlador MemeGenerator em [Reduzindo a latência na Web com a CDN do Azure](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="0ebaa-214">Eu vou somente reproduzir isso aqui.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="0ebaa-215">Suponha que, em seu serviço de nuvem, você queira gerar memes com base em uma imagem de Chuck Norris jovem (foto de [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) como esta:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="0ebaa-216">Você tem uma ação `Index` simples que permite que os clientes especifiquem os superlativos na imagem e gera o meme quando eles postam a ação.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="0ebaa-217">Como se trata de Chuck Norris, você esperaria que esta página se tornasse extremamente popular globalmente.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="0ebaa-218">Este é um bom exemplo do fornecimento de conteúdo semidinâmico com a CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="0ebaa-219">Siga as etapas acima para configurar esta ação do controlador:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="0ebaa-220">Na pasta *\Controllers*, crie um novo arquivo .cs chamado *MemeGeneratorController.cs* e substitua o conteúdo pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="0ebaa-221">Certifique-se de substituir a porção destacada pelo nome de sua CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="0ebaa-222">Clique com o botão direito na ação `Index()` padrão e selecione **Adicionar Exibição**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="0ebaa-223">Aceite as configurações acima e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="0ebaa-224">Abra o novo *Views\MemeGenerator\Index.cshtml* e substitua o conteúdo pelo HTML simples a seguir para enviar os superlativos:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="0ebaa-225">Publique o serviço de nuvem novamente e navegue até **http://*&lt;NomedoServiço>*.cloudapp.net/MemeGenerator/Index** em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="0ebaa-226">Quando você envia os valores de formulário a `/MemeGenerator/Index`, o método de ação `Index_Post` retorna um link para o método de ação `Show` com o respectivo identificador de entrada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="0ebaa-227">Quando clicar em senha, você chegará ao seguinte código:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="0ebaa-228">Se o seu depurador local estiver anexado, você terá a experiência de depuração normal com um redirecionamento local.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="0ebaa-229">Se estiver sendo executado no serviço de nuvem, será redirecionado para:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="0ebaa-230">Que corresponde ao seguinte URL de origem no ponto de extremidade da CDN:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="0ebaa-231">Você então pode usar o atributo `OutputCacheAttribute` no método `Generate` para especificar como o resultado da ação deve ser armazenado em cache, e a CDN do Azure seguirá a especificação.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="0ebaa-232">O código abaixo especifica uma validade de cache de 1 hora (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="0ebaa-233">Da mesma forma, você pode fornecer conteúdo de qualquer ação de controlador no serviço de nuvem por meio da CDN do Azure, com a opção de cache desejada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="0ebaa-234">Na próxima seção, eu mostrarei como fornecer o CSS e scripts agrupados e minificados por meio da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="0ebaa-235">Integrar agrupamento e minificação ASP.NET à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="0ebaa-236">Scripts e folhas de estilo CSS são alterados com pouca frequência e são candidatos ideais para o cache da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="0ebaa-237">Fornecer toda a função Web por meio da CDN do Azure é a maneira mais fácil de integrar agrupamento e minificação à CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="0ebaa-238">No entanto, como talvez você não queira fazer isso, eu vou mostrar como fazê-lo enquanto preserva a experiência do desenvolvedor desejada de agrupamento e minificação ASP.NET, como:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="0ebaa-239">Ótima experiência no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="0ebaa-239">Great debug mode experience</span></span>
* <span data-ttu-id="0ebaa-240">Implantação simplificada</span><span class="sxs-lookup"><span data-stu-id="0ebaa-240">Streamlined deployment</span></span>
* <span data-ttu-id="0ebaa-241">Atualizações imediatas para clientes para atualizações de versão de script/CSS</span><span class="sxs-lookup"><span data-stu-id="0ebaa-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="0ebaa-242">Mecanismo de fallback quando ocorre falha em seu ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="0ebaa-243">Minimizar modificações de código</span><span class="sxs-lookup"><span data-stu-id="0ebaa-243">Minimize code modification</span></span>

<span data-ttu-id="0ebaa-244">No projeto **FunçãoDaWeb1** criado em [Integrar um ponto de extremidade da CDN do Azure ao seu site do Azure e fornecer conteúdo estático em suas páginas Web na CDN do Azure](#deploy), abra *App_Start\BundleConfig.cs* e examine as chamadas de método `bundles.Add()`.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="0ebaa-245">A primeira instrução `bundles.Add()` adiciona um grupo de script ao diretório virtual `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="0ebaa-246">Depois, abra *Views\Shared\_Layout.cshtml* para ver como a marcação do grupo de script é renderizada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="0ebaa-247">Você deve encontrar a seguinte linha de código Razor:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="0ebaa-248">Quando for executado na função Web do Azure, este código Razor renderizará uma marca `<script>` para o grupo de script semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="0ebaa-249">No entanto, quando for executado no Visual Studio digitando `F5`, ele renderizará cada arquivo de script do grupo individualmente (no caso acima, somente o arquivo de script está no grupo):</span><span class="sxs-lookup"><span data-stu-id="0ebaa-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="0ebaa-250">Isso permite que você depure o código JavaScript em seu ambiente de desenvolvimento enquanto reduz conexões clientes simultâneas (agrupamento) e melhora o desempenho do download de arquivos (minificação) em produção.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="0ebaa-251">É um ótimo recurso a ser preservado com a integração à CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="0ebaa-252">Além disso, como o grupo renderizado já contém uma cadeia da versão gerada automaticamente, é aconselhável replicar essa funcionalidade para que sempre que você atualizar sua versão do jQuery por meio do NuGet, ela possa ser atualizada no lado do cliente assim que possível.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="0ebaa-253">Siga as etapas abaixo para integrar agrupamento e minificação ASP.NET ao ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="0ebaa-254">Em *App_Start\BundleConfig.cs*, modifique os métodos `bundles.Add()` para usar um [Construtor de pacotes](http://msdn.microsoft.com/library/jj646464.aspx) diferente, um que especifique um endereço CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="0ebaa-255">Para fazer isso, substitua a `RegisterBundles` definição do método pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="0ebaa-256">Substitua `<yourCDNName>` pelo nome da sua CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="0ebaa-257">De maneira simples, você está definindo `bundles.UseCdn = true` e adicionou uma URL da CDN criada cuidadosamente a cada grupo.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="0ebaa-258">Por exemplo, o primeiro construtor do código:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="0ebaa-259">é igual a:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="0ebaa-260">Este construtor instrui o agrupamento e minificação ASP.NET a renderizar arquivos de script individuais quando depurados localmente, mas usar o endereço CDN especificado para acessar o script em questão.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="0ebaa-261">No entanto, observe duas importantes características dessa URL da CDN criada cuidadosamente:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="0ebaa-262">A origem do URL da CDN é `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que é na realidade o diretório virtual do grupo de scripts em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="0ebaa-263">Como você está usando um construtor CDN, a marcação do script CDN para o grupo não contém mais a cadeia da versão gerada automaticamente na URL renderizada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="0ebaa-264">Você deve gerar manualmente uma cadeia de versão única sempre que o grupo de scripts for modificado para gerar uma perda de cache em sua CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="0ebaa-265">Ao mesmo tempo, essa cadeia de versão única deve permanecer constante ao longo da vida útil da implantação para maximizar as ocorrências no cache na CDN do Azure após a implantação do grupo.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="0ebaa-266">A cadeia de consulta v=<W.X.Y.Z> efetua pull em *Properties\AssemblyInfo.cs* no projeto da função Web.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="0ebaa-267">Você pode ter um fluxo de trabalho de implantação que inclua o incremento da versão de assembly sempre que você publicar no Azure.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="0ebaa-268">Ou pode apenar modificar *Properties\AssemblyInfo.cs* em seu projeto para incrementar automaticamente a cadeia da versão sempre que compilar, usando o caractere curinga “*”.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="0ebaa-269">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-269">For example:</span></span>
     
        <span data-ttu-id="0ebaa-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="0ebaa-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="0ebaa-271">Qualquer outra estratégia para simplificar a geração de uma cadeia única para a vida útil de uma implantação funcionará aqui.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="0ebaa-272">Publique o serviço de nuvem novamente e acesse a página inicial.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="0ebaa-273">Exiba o código HTML da página.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-273">View the HTML code for the page.</span></span> <span data-ttu-id="0ebaa-274">Você deverá ver a URL da CDN renderizada, com uma cadeia de versão única sempre que republicar mudanças em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="0ebaa-275">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="0ebaa-276">No Visual Studio, depure o serviço de nuvem no Visual Studio digitando `F5`.,</span><span class="sxs-lookup"><span data-stu-id="0ebaa-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="0ebaa-277">Exiba o código HTML da página.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-277">View the HTML code for the page.</span></span> <span data-ttu-id="0ebaa-278">Você ainda verá cada arquivo de script renderizado individualmente, para que possa ter uma experiência de depuração consistente no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="0ebaa-279">Mecanismo de fallback para URLs da CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="0ebaa-280">Quando seu ponto de extremidade da CDN do Azure falhar por qualquer motivo, é melhor que sua página da Web seja inteligente o suficiente para acessar o servidor Web de origem como a opção de fallback para carregar JavaScript ou Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="0ebaa-281">Perder imagens do site devido à indisponibilidade da CDN já é grave, mas perder funcionalidades fundamentais da página fornecidas por seus scripts e folhas de estilo é ainda muito mais.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="0ebaa-282">A classe [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) contém uma propriedade chamada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que permite que você configure o mecanismo de fallback para falha da CDN.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="0ebaa-283">Para usar essa propriedade, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="0ebaa-284">No projeto de função Web, abra *App_Start\BundleConfig.cs*, onde você adicionou uma URL da CDN a cada [Construtor de grupo](http://msdn.microsoft.com/library/jj646464.aspx) e faça as seguintes alterações em destaque para adicionar um mecanismo de fallback aos grupos padrão:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="0ebaa-285">Quando `CdnFallbackExpression` não é nulo, o script é injetado no HTML para testar se o grupo é carregado com sucesso e, se não, acessar o grupo diretamente por meio do servidor Web de origem.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="0ebaa-286">Esta propriedade precisa ser definida como uma expressão JavaScript que testa se o grupo CDN respectivo é carregado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="0ebaa-287">A expressão necessária para testar cada grupo difere de acordo com o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="0ebaa-288">Para os grupos padrão acima:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="0ebaa-289">`window.jquery` é definido em jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="0ebaa-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="0ebaa-290">`$.validator` é definido em jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="0ebaa-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="0ebaa-291">`window.Modernizr` é definido em modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="0ebaa-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="0ebaa-292">`$.fn.modal` é definido em bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="0ebaa-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="0ebaa-293">Você pode ter notado que não defini CdnFallbackExpression para o grupo `~/Cointent/css` .</span><span class="sxs-lookup"><span data-stu-id="0ebaa-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="0ebaa-294">Isso ocorre porque no momento há um [bug no System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que injeta uma marcação `<script>` para o CSS de fallback em vez da marcação `<link>` esperada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="0ebaa-295">Há, no entanto, um bom [Fallback de Grupo de Estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferecido pelo [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="0ebaa-296">Para usar a solução alternativa para CSS, crie um novo arquivo .cs na pasta *App_Start* de seu projeto de função Web, nomeie esse arquivo como *StyleBundleExtensions.cs* e substitua seu conteúdo pelo [código do GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="0ebaa-297">Em *App_Start\StyleFundleExtensions.cs*, renomeie o namespace como nome da sua função Web (por exemplo, **FunçãoDaWeb1**).</span><span class="sxs-lookup"><span data-stu-id="0ebaa-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="0ebaa-298">Volte para e `App_Start\BundleConfig.cs` modifique a última `bundles.Add` instrução com o seguinte código em destaque:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="0ebaa-299">Este novo método de extensão usa a mesma ideia para injetar script no HTML para verificar o DOM para um nome de classe, nome de regra e valor de regra correspondente no grupo CSS, e retorna ao servidor Web original se não encontrar um resultado correspondente.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="0ebaa-300">Publique o serviço de nuvem novamente e acesse a página inicial.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="0ebaa-301">Exiba o código HTML da página.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-301">View the HTML code for the page.</span></span> <span data-ttu-id="0ebaa-302">Você deve encontrar scripts injetados semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="0ebaa-303">Observe que o script injetado para o grupo CSS ainda contém o excedente errante da propriedade `CdnFallbackExpression` na linha:</span><span class="sxs-lookup"><span data-stu-id="0ebaa-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="0ebaa-304">Mas como a primeira parte da expressão || sempre retornará o valor verdadeiro (na linha diretamente acima), a função document.write() nunca será executada.</span><span class="sxs-lookup"><span data-stu-id="0ebaa-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="0ebaa-305">Mais informações</span><span class="sxs-lookup"><span data-stu-id="0ebaa-305">More Information</span></span>
* [<span data-ttu-id="0ebaa-306">Visão geral da Rede de Distribuição de Conteúdo (CDN) do Azure</span><span class="sxs-lookup"><span data-stu-id="0ebaa-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="0ebaa-307">Usando o Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0ebaa-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="0ebaa-308">Agrupamento e minificação ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0ebaa-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
