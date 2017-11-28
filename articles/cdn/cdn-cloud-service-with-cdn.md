---
title: "aaaIntegrate um serviço de nuvem do Azure com o Azure CDN | Microsoft Docs"
description: "Saiba como toodeploy um serviço de nuvem que serve o conteúdo de um ponto de extremidade CDN do Azure integrado"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="cf1f7-103"><a name="intro"></a> Integrar um serviço de nuvem à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="cf1f7-104">Um serviço de nuvem pode ser integrado com a CDN do Azure, que serve o conteúdo do local do serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="cf1f7-105">Isso proporciona abordagem Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="cf1f7-106">Implantar e atualizar, de maneira fácil, imagens, scripts e folhas de estilo nos diretórios de projetos de seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="cf1f7-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="cf1f7-107">Atualizar facilmente os pacotes do NuGet Olá em seu serviço de nuvem, como jQuery ou versões de inicialização</span><span class="sxs-lookup"><span data-stu-id="cf1f7-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="cf1f7-108">Gerenciar seu aplicativo Web o servido de CDN conteúdo e todos os do hello mesma interface do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf1f7-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="cf1f7-109">Fluxo de trabalho de implantação unificado para seu aplicativo Web e o conteúdo fornecido por CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="cf1f7-110">Integrar agrupamento e minificação ASP.NET à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cf1f7-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="cf1f7-111">What you will learn</span></span>
<span data-ttu-id="cf1f7-112">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="cf1f7-113">Integrar um ponto de extremidade da CDN do Azure a seu serviço de nuvem e fornecer conteúdo estático em suas páginas Web por meio da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="cf1f7-114">Definir configurações de cache para conteúdo estático em seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="cf1f7-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="cf1f7-115">Fornecer conteúdo por ações do controlador na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="cf1f7-116">Sirvam agrupados e minimizada conteúdo por meio do Azure CDN enquanto preserva a experiência no Visual Studio de depuração de script hello</span><span class="sxs-lookup"><span data-stu-id="cf1f7-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="cf1f7-117">Configurar o fallback de seus scripts e CSS quando a CDN do Azure estiver offline</span><span class="sxs-lookup"><span data-stu-id="cf1f7-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="cf1f7-118">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="cf1f7-118">What you will build</span></span>
<span data-ttu-id="cf1f7-119">Você implantar uma função Web de serviço de nuvem usando o padrão de saudação modelo do ASP.NET MVC, adicionar conteúdo tooserve do código de uma CDN do Azure integrados, como uma imagem, resultados de ação do controlador e saudação padrão arquivos JavaScript e CSS e também gravar saudação de tooconfigure de código mecanismo de fallback para pacotes atendidas no evento de saudação que Olá CDN está offline.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="cf1f7-120">O que será necessário</span><span class="sxs-lookup"><span data-stu-id="cf1f7-120">What you will need</span></span>
<span data-ttu-id="cf1f7-121">Este tutorial tem Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="cf1f7-122">Uma [conta do Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="cf1f7-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="cf1f7-123">Visual Studio 2015 com [SDK do Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="cf1f7-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="cf1f7-124">Você precisa de uma conta do Azure toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="cf1f7-125">Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados até você pode manter a conta de saudação e usar serviços do Azure, como sites de livre.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="cf1f7-126">Você pode [ativar benefícios para assinantes do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Todos os meses, sua assinatura do MSDN oferece créditos que podem ser usados para serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="cf1f7-127">Implantar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="cf1f7-127">Deploy a cloud service</span></span>
<span data-ttu-id="cf1f7-128">Nesta seção, você implantar o modelo de aplicativo do ASP.NET MVC na função de Web do serviço de nuvem do Visual Studio 2015 tooa de padrão de saudação e, em seguida, integrá-lo com um novo ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="cf1f7-129">Siga as instruções de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="cf1f7-130">No Visual Studio 2015, crie um novo serviço de nuvem do Azure na barra de menus Olá indo muito**arquivo > Novo > projeto > nuvem > serviço de nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="cf1f7-131">Dê um nome a ele e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="cf1f7-132">Selecione **função Web ASP.NET** e clique em Olá  **>**  botão.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="cf1f7-133">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="cf1f7-134">Selecione **MVC** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="cf1f7-135">Agora, publica este tooan de função Web serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="cf1f7-136">Projeto de serviço de nuvem hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="cf1f7-137">Se você ainda não entrou no Microsoft Azure, clique em Olá **adicionar uma conta...**  Olá suspensa e clique em **adicionar uma conta** item de menu.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="cf1f7-138">Em Olá página de entrada, entrar com hello conta da Microsoft usada tooactivate sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="cf1f7-139">Após ter entrado, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="cf1f7-140">Se você ainda não tiver criado uma conta de armazenamento ou um serviço de nuvem, o Visual Studio o ajudará a criar ambos.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="cf1f7-141">Em Olá **criar serviço de nuvem e conta** caixa de diálogo, nome do tipo hello serviço desejado e região desejada Olá select.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="cf1f7-142">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="cf1f7-143">No hello página de configurações de publicação, verifique se a configuração de saudação e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="cf1f7-144">o processo de publicação Olá para serviços de nuvem demora muito.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="cf1f7-145">Olá habilitar a implantação da Web para a opção de todas as funções pode tornar a depuração muito mais rápido de serviço de nuvem, fornecendo atualizações rápida (mas temporária) tooyour funções da Web.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="cf1f7-146">Para obter mais informações sobre essa opção, consulte [publicando um serviço de nuvem usando ferramentas do Azure Olá](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="cf1f7-147">Olá quando **Log de atividades do Microsoft Azure** mostra que o status de publicação está **concluído**, você criará um ponto de extremidade CDN que esteja integrado com esse serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="cf1f7-148">Se, após a publicação, o serviço de nuvem Olá implantado exibe uma tela de erro, é provável que porque está usando o serviço de nuvem Olá que você implantou um [sistema operacional que não inclui o .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="cf1f7-149">Você pode contornar esse problema [Implantando o .NET 4.5.2 como uma tarefa de inicialização](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="cf1f7-150">Criar um novo perfil CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-150">Create a new CDN profile</span></span>
<span data-ttu-id="cf1f7-151">Um perfil CDN é um conjunto de pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="cf1f7-152">Cada perfil contém um ou mais pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="cf1f7-153">Você poderá toouse tooorganize de vários perfis seus pontos de extremidade CDN, o domínio da internet, aplicativo web ou algum outro critério.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="cf1f7-154">Se você já tiver um perfil CDN que você deseja toouse para este tutorial, vá muito[criar um novo ponto de extremidade CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="cf1f7-155">Criar um novo ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="cf1f7-156">**toocreate um novo ponto de extremidade CDN para sua conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="cf1f7-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="cf1f7-157">Em Olá [Portal de gerenciamento](https://portal.azure.com), navegar tooyour perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="cf1f7-158">Você pode ter-fixado toohello painel na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="cf1f7-159">Se você não, você pode encontrá-lo clicando **procurar**, em seguida, **perfis CDN**, e clicando no perfil Olá planejar tooadd seu ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="cf1f7-160">folha de perfil CDN Olá aparece.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-160">hello CDN profile blade appears.</span></span>
   
    ![Perfil CDN][cdn-profile-settings]
2. <span data-ttu-id="cf1f7-162">Clique em Olá **Adicionar ponto de extremidade** botão.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Adicionar botão de ponto de extremidade][cdn-new-endpoint-button]
   
    <span data-ttu-id="cf1f7-164">Olá **adicionar um ponto de extremidade** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Adicionar folha de ponto de extremidade][cdn-add-endpoint]
3. <span data-ttu-id="cf1f7-166">Insira um **Nome** para esse ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="cf1f7-167">Esse nome será usado tooaccess seus recursos armazenados em cache no domínio Olá `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="cf1f7-168">Em Olá **tipo de origem** lista suspensa, selecione *serviço de nuvem*.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="cf1f7-169">Em Olá **nome de host de origem** lista suspensa, selecione o seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="cf1f7-170">Mantenha os padrões de saudação para **caminho de origem**, **cabeçalho de host de origem**, e **porta de origem/protocolo**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="cf1f7-171">Você deve especificar pelo menos um protocolo (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="cf1f7-172">Clique em Olá **adicionar** toocreate botão Olá novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="cf1f7-173">Depois que o ponto de extremidade de saudação é criado, ele aparece em uma lista de pontos de extremidade para o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="cf1f7-174">modo de exibição de lista Olá mostra Olá URL toouse tooaccess em cache o conteúdo, bem como domínio de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Ponto de extremidade CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="cf1f7-176">ponto de extremidade de saudação não estará imediatamente disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="cf1f7-177">Pode demorar até minutos too90 para Olá toopropagate de registro por meio da rede CDN hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="cf1f7-178">Os usuários que tente imediatamente o nome de domínio toouse Olá CDN podem receber o código de status 404 até que o conteúdo de saudação está disponível por meio de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="cf1f7-179">Saudação de teste ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="cf1f7-180">Quando a saudação status de publicação é **concluído**, abra uma janela do navegador e navegue muito**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="cf1f7-181">Em minha configuração, essa URL é:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="cf1f7-182">Que corresponde a toohello URL de origem no ponto de extremidade CDN Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="cf1f7-183">Quando você navega muito**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, dependendo de seu navegador, será toodownload solicitada ou abra Olá bootstrap.css que origem do seu aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="cf1f7-184">De maneira semelhante, você pode acessar qualquer URL acessível publicamente em **http://*&lt;nomedoServiço>*.cloudapp.net/**, diretamente de seu ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="cf1f7-185">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-185">For example:</span></span>

* <span data-ttu-id="cf1f7-186">Um arquivo. js do caminho de /Script Olá</span><span class="sxs-lookup"><span data-stu-id="cf1f7-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="cf1f7-187">Qualquer arquivo de conteúdo de saudação /Content caminho</span><span class="sxs-lookup"><span data-stu-id="cf1f7-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="cf1f7-188">Qualquer controller/action</span><span class="sxs-lookup"><span data-stu-id="cf1f7-188">Any controller/action</span></span>
* <span data-ttu-id="cf1f7-189">Se a cadeia de caracteres de consulta hello está habilitada no ponto de extremidade CDN, qualquer URL com cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="cf1f7-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="cf1f7-190">Na verdade, com hello acima de configuração, você pode hospedar o serviço de nuvem inteiro de saudação do  **http://*&lt;cdnName >*.azureedge.net/**. Se navegar muito**http://camservice.azureedge.net/ * *, obter resultado de ação de saudação da casa/índice.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="cf1f7-191">Isso não significa, no entanto, que é sempre uma boa ideia tooserve um serviço de nuvem inteira por meio da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="cf1f7-192">Um CDN com otimização de entrega estático não necessariamente acelerar a entrega de ativos dinâmicos que não devem toobe armazenado em cache ou são atualizados com muita frequência, desde que Olá CDN deve puxar uma nova versão do ativo de saudação do servidor de origem Olá frequentemente.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="cf1f7-193">Para este cenário, você pode habilitar [aceleração de Site dinâmico](cdn-dynamic-site-acceleration.md) otimização (DSA) no ponto de extremidade CDN que usa vários toospeed técnicas a entrega de ativos dinâmicos não armazenável em cache.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="cf1f7-194">Se você tiver um site com uma mistura de conteúdo estático e dinâmico, você pode escolher tooserve seu conteúdo estático de CDN com um tipo de otimização estáticas (por exemplo, entrega geral web) e o conteúdo dinâmico tooserve diretamente do servidor de origem hello, ou por meio de uma CDN ponto de extremidade com otimização de DSA ativado caso a caso.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="cf1f7-195">toothat final, você já viu como arquivos de conteúdo individuais tooaccess do ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="cf1f7-196">Vou mostrar como tooserve uma ação do controlador específico por meio de um ponto de extremidade CDN específico no servir conteúdo de ações do controlador por meio da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="cf1f7-197">alternativa de saudação é toodetermine que conteúdo tooserve da CDN do Azure em uma base por caso no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="cf1f7-198">toothat final, você já viu como arquivos de conteúdo individuais tooaccess do ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="cf1f7-199">Vou mostrar como tooserve uma ação do controlador específico por meio de Olá ponto de extremidade CDN na [oferecer conteúdo de ações do controlador por meio do Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="cf1f7-200">Configurar opções de cache para arquivos estáticos em seu serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="cf1f7-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="cf1f7-201">Com a integração do Azure CDN no serviço de nuvem, você pode especificar como deseja estático toobe conteúdo armazenado em cache no ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="cf1f7-202">toodo isso, abra *Web. config* de sua função Web do projeto (por exemplo, WebRole1) e adicionar um `<staticContent>` elemento muito`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="cf1f7-203">Olá XML abaixo configura Olá cache tooexpire em 3 dias.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="cf1f7-204">Quando você faz isso, todos os arquivos estáticos em seu serviço de nuvem observará Olá mesma regra em seu cache CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="cf1f7-205">Para ter um controle mais granular das configurações de cache, adicione um arquivo *Web.config* a uma pasta e adicione suas configurações.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="cf1f7-206">Por exemplo, adicionar um *Web. config* arquivo toohello *\Content* pasta e substitua Olá conteúdo com hello XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="cf1f7-207">Essa configuração faz com que todos os arquivos estáticos do hello *\Content* toobe pasta armazenada em cache por 15 dias.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="cf1f7-208">Para obter mais informações sobre como Olá tooconfigure `<clientCache>` elemento, consulte [Cache do cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="cf1f7-209">Em [oferecer conteúdo de ações do controlador por meio do Azure CDN](#controller), também mostrarei como você pode definir configurações de cache para resultados de ação do controlador no hello cache CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="cf1f7-210">Fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="cf1f7-211">Quando você integra uma função de Web do serviço de nuvem com o Azure CDN, é relativamente fácil tooserve conteúdo de ações do controlador por meio de saudação do Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="cf1f7-212">Diferente que atende a sua nuvem de serviço diretamente por meio do Azure CDN (mostrado acima), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra como toodo com divertido controlador MemeGenerator [reduzindo a latência em Olá web com hello CDN do Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="cf1f7-213">Eu vou somente reproduzir isso aqui.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="cf1f7-214">Suponha que no seu serviço de nuvem você deseja memes toogenerate com base em uma imagem Chuck Norris jovens (foto por [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="cf1f7-215">Você tem um simples `Index` ação que permite que os clientes de saudação toospecify superlativos de saudação na imagem hello, gera Olá meme depois que eles lançar toohello ação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="cf1f7-216">Como é Chuck Norris, você esperaria toobecome essa página totalmente populares globalmente.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="cf1f7-217">Este é um bom exemplo do fornecimento de conteúdo semidinâmico com a CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="cf1f7-218">Siga as etapas de saudação acima toosetup esta ação de controlador:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="cf1f7-219">Em Olá *\Controllers* pasta, crie um novo arquivo. cs chamado *MemeGeneratorController.cs* e substituir Olá conteúdo com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="cf1f7-220">Ser-se parte destacada Olá de tooreplace com seu nome CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="cf1f7-221">Clique com botão direito no padrão de saudação `Index()` ação e selecione **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="cf1f7-222">Aceite as configurações de saudação abaixo e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="cf1f7-223">Olá abrir nova *Views\MemeGenerator\Index.cshtml* e substitua conteúdo Olá Olá HTML simple a seguir para enviar superlativos hello:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="cf1f7-224">Publicar novamente o serviço de nuvem hello e navegue muito**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="cf1f7-225">Quando você enviar valores de formulário Olá muito`/MemeGenerator/Index`, Olá `Index_Post` método de ação retorna um link toohello `Show` método de ação com o identificador de entrada respectivos hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="cf1f7-226">Quando você clica em um link de hello, atingir Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="cf1f7-227">Se o depurador local estiver conectado, você obterá Olá experiência de depuração normal com um local de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="cf1f7-228">Se ele estiver em execução no serviço de nuvem hello, ele será redirecionado para:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="cf1f7-229">Que corresponde a toohello URL de origem no ponto de extremidade CDN a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="cf1f7-230">Você pode usar Olá `OutputCacheAttribute` atributo Olá `Generate` toospecify de método como resultado da ação Olá deve ser armazenada em cache, que aceita a CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="cf1f7-231">código de saudação abaixo especificar uma expiração de cache de 1 hora (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="cf1f7-232">Da mesma forma, você pode servir o conteúdo de qualquer ação do controlador em seu serviço de nuvem por meio de seu CDN do Azure, com a opção de cache de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="cf1f7-233">Na próxima seção, Olá, mostrarei como tooserve Olá agrupadas e minimizada CSS por meio da CDN do Azure e scripts.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="cf1f7-234">Integrar agrupamento e minificação ASP.NET à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf1f7-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="cf1f7-235">Folhas de estilo CSS e scripts alterados com frequência e são fortes candidatas à saudação cache de CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="cf1f7-236">Atendendo Olá toda função Web por meio de seu Azure CDN é toointegrate de maneira mais fácil de saudação empacotamento e minimização com CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="cf1f7-237">No entanto, você não pode desejar toodo isso, mostrarei como toodo, preservando Olá desejado develper experiência de ASP.NET empacotamento e minimização, como:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="cf1f7-238">Ótima experiência no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="cf1f7-238">Great debug mode experience</span></span>
* <span data-ttu-id="cf1f7-239">Implantação simplificada</span><span class="sxs-lookup"><span data-stu-id="cf1f7-239">Streamlined deployment</span></span>
* <span data-ttu-id="cf1f7-240">Atualizações imediatas tooclients para atualizações de versão de script/CSS</span><span class="sxs-lookup"><span data-stu-id="cf1f7-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="cf1f7-241">Mecanismo de fallback quando ocorre falha em seu ponto de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="cf1f7-242">Minimizar modificações de código</span><span class="sxs-lookup"><span data-stu-id="cf1f7-242">Minimize code modification</span></span>

<span data-ttu-id="cf1f7-243">Em Olá **WebRole1** projeto que você criou no [integrar um ponto de extremidade CDN do Azure com seu site do Azure e servir conteúdo estático das páginas da Web do Azure CDN](#deploy), abra *App_Start\ BundleConfig.cs* e dar uma olhada Olá `bundles.Add()` chamadas de método.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="cf1f7-244">Olá primeiro `bundles.Add()` instrução adiciona um pacote de script no diretório virtual Olá `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="cf1f7-245">Em seguida, abra *exibições \ compartilhadas\_cshtml* toosee como marca de pacote de script hello é renderizada.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="cf1f7-246">Você deve ser capaz de toofind Olá seguinte linha de código Razor:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="cf1f7-247">Quando esse código Razor é executado na função de Web do Azure hello, ele processará uma `<script>` marca Olá script a seguir toohello semelhante pacote:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="cf1f7-248">No entanto, quando ele é executado no Visual Studio digitando `F5`, ele processará individualmente a cada arquivo de script no pacote de saudação (no caso de Olá acima, somente um arquivo de script está no pacote de saudação):</span><span class="sxs-lookup"><span data-stu-id="cf1f7-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="cf1f7-249">Isso permite que você toodebug Olá código JavaScript do ambiente de desenvolvimento (agrupamento) de conexões de cliente simultâneas e melhorando arquivo download desempenho (minimização) em produção.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="cf1f7-250">É toopreserve um ótimo recurso com integração do Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="cf1f7-251">Além disso, desde que o pacote de saudação renderizada já contém uma cadeia de caracteres de versão gerado automaticamente, você deseja tooreplicate funcionalidade assim Olá sempre que você atualize sua versão de jQuery através do NuGet, ele pode ser atualizado no lado do cliente hello, assim como é possível.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="cf1f7-252">Siga as próximas etapas Olá toointegration ASP.NET empacotamento e minimização com seu ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="cf1f7-253">Em *App_Start\BundleConfig.cs*, modificar Olá `bundles.Add()` métodos toouse outro [construtor pacote](http://msdn.microsoft.com/library/jj646464.aspx), que especifica um endereço CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="cf1f7-254">toodo Olá isso, substitua `RegisterBundles` definição de método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="cf1f7-255">Ser tooreplace se `<yourCDNName>` com nome de saudação do seu CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="cf1f7-256">Em palavras simples, você está definindo `bundles.UseCdn = true` e adicionados a um pacote de tooeach URL CDN concebido cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="cf1f7-257">Por exemplo, Olá primeiro construtor no código hello:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="cf1f7-258">Olá igual é:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="cf1f7-259">Este construtor informa ASP.NET empacotamento e minimização toorender arquivos de script individuais quando depurado localmente, mas use Olá especificado script tooaccess de saudação do endereço CDN em questão.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="cf1f7-260">No entanto, observe duas importantes características dessa URL da CDN criada cuidadosamente:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="cf1f7-261">saudação de origem para esta URL CDN é `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que é realmente Olá diretório virtual do pacote de script hello em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="cf1f7-262">Como você está usando o construtor CDN, Olá marca de script CDN para o pacote de saudação não contém Olá gerado automaticamente a cadeia de caracteres de versão no hello renderizado URL.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="cf1f7-263">Você deve gerar uma cadeia de caracteres de versão exclusivo manualmente sempre que o pacote de script hello é modificado tooforce perder um cache em seu CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="cf1f7-264">AT Olá mesmo tempo, essa cadeia de caracteres de versão exclusivo deve permanecem constante durante a vida Olá Olá implantação toomaximize de acertos do cache em seu CDN do Azure após a implantação do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="cf1f7-265">Olá a cadeia de caracteres de consulta v = < w.x.y. z > recebimentos de *Properties\AssemblyInfo.cs* em seu projeto de função Web.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="cf1f7-266">Você pode ter um fluxo de trabalho de implantação que inclui incrementando a versão do assembly hello toda vez que você publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="cf1f7-267">Ou, você pode modificar apenas *Properties\AssemblyInfo.cs* em sua cadeia de versão do projeto tooautomatically incremento Olá sempre que você criar, usando o caractere curinga de saudação ' *'.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="cf1f7-268">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-268">For example:</span></span>
     
        <span data-ttu-id="cf1f7-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="cf1f7-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="cf1f7-270">Qualquer outra estratégia toostreamline gerar uma cadeia de caracteres exclusiva durante saudação de uma implantação funcionará aqui.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="cf1f7-271">Republicar Olá nuvem acesso e serviço Olá página inicial.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="cf1f7-272">Saudação de modo de exibição código HTML para a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="cf1f7-273">Você deve ser capaz de toosee Olá URL CDN renderizado com uma cadeia de caracteres de versão exclusivo toda vez que você publicar novamente o serviço de nuvem tooyour alterações.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="cf1f7-274">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="cf1f7-275">No Visual Studio, depurar o serviço em nuvem no Visual Studio Olá digitando `F5`.,</span><span class="sxs-lookup"><span data-stu-id="cf1f7-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="cf1f7-276">Saudação de modo de exibição código HTML para a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="cf1f7-277">Você ainda verá cada arquivo de script renderizado individualmente, para que possa ter uma experiência de depuração consistente no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="cf1f7-278">Mecanismo de fallback para URLs da CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="cf1f7-279">Quando o ponto de extremidade CDN do Azure falha por algum motivo, você deseja que sua página da Web toobe inteligente suficiente tooaccess seu servidor da Web de origem como opção de fallback Olá para carregar JavaScript ou inicialização.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="cf1f7-280">É grave o suficiente toolose imagens no seu site devido a indisponibilidade de tooCDN, mas a funcionalidade de página fundamental de toolose muito mais grave fornecidos por seus scripts e folhas de estilo.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="cf1f7-281">Olá [pacote](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contém uma propriedade chamada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que habilita o mecanismo de fallback tooconfigure Olá para falha CDN.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="cf1f7-282">toouse essa propriedade, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="cf1f7-283">No seu projeto de função Web, abra *App_Start\BundleConfig.cs*, em que você adicionou uma URL de CDN em cada [construtor pacote](http://msdn.microsoft.com/library/jj646464.aspx)e faça o seguinte Olá realçado altera tooadd toohello de mecanismo de fallback pacotes padrão:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="cf1f7-284">Quando `CdnFallbackExpression` é não nulo, script é injetado tootest Olá HTML se o pacote de saudação é carregado com êxito e, se não, acessar Olá pacote diretamente do servidor de Web de origem hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="cf1f7-285">Essa propriedade deve toobe tooa JavaScript expressão de conjunto testa se o respectivo pacote CDN Olá é carregado corretamente.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="cf1f7-286">expressão de saudação necessário tootest difere de cada pacote de conteúdo de acordo toohello.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="cf1f7-287">Para pacotes de padrão de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="cf1f7-288">`window.jquery` é definido em jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="cf1f7-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="cf1f7-289">`$.validator` é definido em jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="cf1f7-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="cf1f7-290">`window.Modernizr` é definido em modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="cf1f7-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="cf1f7-291">`$.fn.modal` é definido em bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cf1f7-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="cf1f7-292">Você deve ter notado que eu não definiu CdnFallbackExpression para Olá `~/Cointent/css` pacote.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="cf1f7-293">Isso ocorre porque atualmente não há uma [bug na otimização](https://aspnetoptimization.codeplex.com/workitem/104) que insere um `<script>` marca Olá esperado do CSS fallback em vez da saudação `<link>` marca.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="cf1f7-294">Há, no entanto, um bom [Fallback de Grupo de Estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferecido pelo [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="cf1f7-295">solução alternativa de saudação toouse para CSS, crie um novo arquivo. cs no seu projeto de função Web *App_Start* pasta chamada *StyleBundleExtensions.cs*e substituir seu conteúdo com hello [código de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="cf1f7-296">Em *App_Start\StyleFundleExtensions.cs*, renomeie o nome da função do hello namespace tooyour da Web (por exemplo, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="cf1f7-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="cf1f7-297">Voltar muito`App_Start\BundleConfig.cs` e modificar Olá última `bundles.Add` instrução com hello código realçado a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="cf1f7-298">Esse novo método de extensão usa Olá ideia mesmo tooinject script hello HTML toocheck Olá DOM para Olá um nome de classe correspondente, o nome da regra e o valor de regra definida no hello CSS pacote e o servidor vão toohello back origem Web se ele falhar toofind correspondência de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="cf1f7-299">Publica serviço de nuvem Olá novamente e acesso Olá home page.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="cf1f7-300">Saudação de modo de exibição código HTML para a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="cf1f7-301">Você deve encontrar injetado scripts semelhantes toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="cf1f7-302">Observe que o script inserido para o pacote CSS Olá ainda contém vestígios errôneo de saudação do hello `CdnFallbackExpression` propriedade na linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="cf1f7-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="cf1f7-303">Mas como a primeira parte Olá Olá | | expressão sempre retornará verdadeira (na linha de saudação diretamente acima), a função de Document hello nunca será executado.</span><span class="sxs-lookup"><span data-stu-id="cf1f7-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="cf1f7-304">Mais informações</span><span class="sxs-lookup"><span data-stu-id="cf1f7-304">More Information</span></span>
* [<span data-ttu-id="cf1f7-305">Visão geral de hello Azure Content Delivery Network (CDN)</span><span class="sxs-lookup"><span data-stu-id="cf1f7-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="cf1f7-306">Usando o Azure CDN</span><span class="sxs-lookup"><span data-stu-id="cf1f7-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="cf1f7-307">Agrupamento e minificação ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf1f7-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
