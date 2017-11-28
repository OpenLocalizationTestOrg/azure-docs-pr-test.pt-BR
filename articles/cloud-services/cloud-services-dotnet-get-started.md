---
title: "aaaGet iniciado com serviços de nuvem do Azure e ASP.NET | Microsoft Docs"
description: "Saiba como toocreate um aplicativo de várias camado usando o ASP.NET MVC e o Azure. saudação de aplicativo é executado em um serviço de nuvem, com a função web e função de trabalho. Ele utiliza Entity Framework, o Banco de Dados SQL e filas e blobs de Armazenamento do Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="b4f07-105">Introdução aos Serviços de Nuvem do Azure e ao ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b4f07-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="b4f07-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b4f07-106">Overview</span></span>
<span data-ttu-id="b4f07-107">Este tutorial mostra como toocreate um aplicativo .NET de multicamadas com um front-end, o ASP.NET MVC e implantá-lo tooan [serviço de nuvem do Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="b4f07-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="b4f07-108">Olá aplicativo usa [banco de dados do SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), Olá [serviço Blob do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)e hello [serviço de fila do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="b4f07-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="b4f07-109">Você pode [baixar o projeto do Visual Studio Olá](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de saudação Galeria de códigos do MSDN.</span><span class="sxs-lookup"><span data-stu-id="b4f07-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="b4f07-110">Olá tutorial mostra como aplicativo hello toobuild e executar localmente, como toodeploy-tooAzure e hello execução na nuvem e como toobuild-lo a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="b4f07-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="b4f07-111">Você pode iniciar Compilando a partir do zero Olá teste e implante etapas posteriormente se você preferir.</span><span class="sxs-lookup"><span data-stu-id="b4f07-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="b4f07-112">O aplicativo Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="b4f07-112">Contoso Ads application</span></span>
<span data-ttu-id="b4f07-113">aplicativo Hello é um quadro de avisos de publicidade.</span><span class="sxs-lookup"><span data-stu-id="b4f07-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="b4f07-114">Os usuários criam um anúncio inserindo texto e carregando uma imagem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="b4f07-115">Eles podem ver uma lista de anúncios com imagens em miniatura e eles podem ver imagem em tamanho normal hello quando eles selecionam um ad toosee Olá os detalhes.</span><span class="sxs-lookup"><span data-stu-id="b4f07-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Lista de anúncios](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="b4f07-117">usa o aplicativo Hello Olá [centrado em fila de trabalho padrão](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga trabalho de saudação com uso intensivo de CPU de criação de processo de back-end tooa miniaturas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="b4f07-118">Arquitetura alternativa: sites e trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="b4f07-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="b4f07-119">Este tutorial mostra como toorun front-end e back-end em um Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="b4f07-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="b4f07-120">Uma alternativa é toorun Olá front-end em um [site do Azure](/services/web-sites/) e usar Olá [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) recurso (atualmente na visualização) para Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="b4f07-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="b4f07-121">Para obter um tutorial que usa trabalhos Web, consulte [Introdução ao SDK do Azure WebJobs de saudação](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4f07-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="b4f07-122">Para obter informações sobre como toochoose Olá os serviços que melhor se ajustar seu cenário, consulte [comparação de sites do Azure, serviços de nuvem e máquinas virtuais](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b4f07-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b4f07-123">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="b4f07-123">What you'll learn</span></span>
* <span data-ttu-id="b4f07-124">Como tooenable sua máquina de desenvolvimento do Azure instalando Olá SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="b4f07-125">Como toocreate um Visual Studio nuvem projeto de serviço com uma função web do ASP.NET MVC e uma função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f07-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="b4f07-126">Como tootest Olá nuvem projeto de serviço localmente, usando o emulador de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="b4f07-127">Como o tooan de projeto em nuvem toopublish hello Azure serviço de nuvem e teste usando uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="b4f07-128">Como tooupload arquivos e armazená-los no serviço de Blob do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="b4f07-129">Como toouse Olá serviço de fila do Azure para comunicação entre camadas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4f07-130">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b4f07-130">Prerequisites</span></span>
<span data-ttu-id="b4f07-131">Olá tutorial assume que você entende [serviços de nuvem de conceitos básicos sobre o Azure](cloud-services-choose-me.md) como *função web* e *função de trabalho* terminologia.</span><span class="sxs-lookup"><span data-stu-id="b4f07-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="b4f07-132">Ele também pressupõe que você sabe como toowork com [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) ou [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projetos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="b4f07-133">aplicativo de exemplo Hello usa MVC, mas a maioria das tutorial Olá também se aplica a formulários tooWeb.</span><span class="sxs-lookup"><span data-stu-id="b4f07-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="b4f07-134">Você pode executar o aplicativo hello localmente sem uma assinatura do Azure, mas você precisará de uma nuvem de toohello toodeploy Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="b4f07-135">Se não tem uma conta, você pode [ativar os benefícios de assinante MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) ou [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="b4f07-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="b4f07-136">instruções de tutorial Olá trabalham com uma saudação produtos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="b4f07-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b4f07-137">Visual Studio 2013</span></span>
* <span data-ttu-id="b4f07-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b4f07-138">Visual Studio 2015</span></span>
* <span data-ttu-id="b4f07-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b4f07-139">Visual Studio 2017</span></span>

<span data-ttu-id="b4f07-140">Se você não tiver um desses, Visual Studio pode ser instalado automaticamente quando você instala o SDK do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="b4f07-141">Arquitetura do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b4f07-141">Application architecture</span></span>
<span data-ttu-id="b4f07-142">aplicativo Hello armazena anúncios em um banco de dados SQL, usando tabelas de saudação do Entity Framework Code First toocreate e acessar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="b4f07-143">Para cada anúncio Olá banco de dados armazena duas URLs, uma para Olá imagem em tamanho normal e outra para a miniatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Tabela de anúncios](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="b4f07-145">Quando um usuário carrega uma imagem, Olá front-end em execução em uma função web armazena a imagem de saudação em uma [BLOBs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e armazena informações de ad Olá no banco de dados de saudação com uma URL que aponta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="b4f07-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="b4f07-146">AT Olá mesmo tempo, ele grava um tooan de mensagem da fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="b4f07-147">Um processo de back-end em execução em uma função de trabalho periodicamente sonda fila Olá novas mensagens.</span><span class="sxs-lookup"><span data-stu-id="b4f07-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="b4f07-148">Quando uma nova mensagem for exibida, função de trabalho Olá cria uma miniatura para essa imagem e atualizações Olá campo de banco de dados em miniatura do URL para que o ad.</span><span class="sxs-lookup"><span data-stu-id="b4f07-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="b4f07-149">Olá diagrama a seguir mostra como partes de saudação do aplicativo hello interagem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Arquitetura do Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="b4f07-151">Baixe e execute a solução de saudação concluída</span><span class="sxs-lookup"><span data-stu-id="b4f07-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="b4f07-152">Baixe e descompacte Olá [concluído solução](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="b4f07-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="b4f07-153">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="b4f07-154">De saudação **arquivo** menu escolha **Abrir projeto**, navegue toowhere baixado solução hello e, em seguida, abra o arquivo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="b4f07-155">Pressione a solução de saudação toobuild CTRL + SHIFT + B.</span><span class="sxs-lookup"><span data-stu-id="b4f07-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="b4f07-156">Por padrão, o Visual Studio automaticamente restaura Olá NuGet conteúdo do pacote, que não foi incluído no hello *. zip* arquivo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="b4f07-157">Se não restaurar os pacotes de saudação, instalá-los manualmente por vai toohello **gerenciar pacotes NuGet para solução** caixa de diálogo e clicar em Olá **restaurar** botão na parte superior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="b4f07-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="b4f07-158">Em **Solution Explorer**, certifique-se de que **ContosoAdsCloudService** é selecionado como projeto de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="b4f07-159">Se você estiver usando o Visual Studio 2015 ou superior, altere a cadeia de conexão do SQL Server Olá no aplicativo hello *Web. config* arquivo de projeto de ContosoAdsWeb hello e em Olá *ServiceConfiguration* arquivo de projeto de ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="b4f07-160">Em cada caso, altere "(localdb) \v11.0" muito "(localdb) \MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="b4f07-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="b4f07-161">Pressione CTRL + F5 aplicativo de hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="b4f07-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="b4f07-162">Quando você executar um projeto de serviço de nuvem localmente, o Visual Studio automaticamente invoca hello Azure *emulador de computação* e o Azure *emulador de armazenamento*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="b4f07-163">Olá compute emulator usa função web do seu computador recursos toosimulate hello e ambientes de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f07-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="b4f07-164">emulador de armazenamento Olá usa um [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate armazenamento em nuvem do Azure do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b4f07-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="b4f07-165">Olá primeira vez que executar um projeto de serviço de nuvem, que leva cerca de um minuto para Olá emuladores toostart backup.</span><span class="sxs-lookup"><span data-stu-id="b4f07-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="b4f07-166">Quando a inicialização do emulador for concluída, o navegador de padrão de saudação abre toohello home page do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Arquitetura do Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="b4f07-168">Clique em **Criar um Anúncio**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="b4f07-169">Insira alguns dados de teste e selecione um *. jpg* tooupload da imagem e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Criar página](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="b4f07-171">aplicativo Hello vai toohello página de índice, mas ela não mostra uma miniatura para ad novo Olá porque não foi feito ainda que o processamento.</span><span class="sxs-lookup"><span data-stu-id="b4f07-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="b4f07-172">Aguarde um momento e, em seguida, atualize Olá índice toosee Olá miniatura.</span><span class="sxs-lookup"><span data-stu-id="b4f07-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Página de índice](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="b4f07-174">Clique em **detalhes** para a imagem em tamanho normal do ad toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Página de detalhes](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="b4f07-176">Executa aplicativo hello inteiramente no computador local, sem nuvem toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f07-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="b4f07-177">emulador de armazenamento Olá armazena fila hello e dados blob em um banco de dados do SQL Server Express LocalDB e o aplicativo hello armazena dados do ad de saudação em outro banco de dados LocalDB.</span><span class="sxs-lookup"><span data-stu-id="b4f07-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="b4f07-178">Entity Framework Code First Olá recém-criados banco de dados ad Olá primeira vez Olá web aplicativo tentou tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="b4f07-179">Olá seção a seguir, você configurará recursos da nuvem do Azure toouse Olá solução para filas, blobs e banco de dados de aplicativo hello quando ele é executado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="b4f07-180">Se você quisesse toocontinue toorun localmente, mas usa os recursos de armazenamento e o banco de dados de nuvem, você pode fazer isso.</span><span class="sxs-lookup"><span data-stu-id="b4f07-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="b4f07-181">Ele é apenas uma questão de configuração de cadeias de caracteres de conexão, você verá como toodo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="b4f07-182">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="b4f07-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="b4f07-183">Isso será feito Olá aplicativo de hello toorun etapas na nuvem Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="b4f07-184">Criar um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="b4f07-185">Criar um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="b4f07-186">Crie uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="b4f07-187">Configure Olá solução toouse seu banco de dados SQL do Azure quando ele é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="b4f07-188">Configure Olá solução toouse sua conta de armazenamento do Azure quando ele é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="b4f07-189">Implante o serviço de nuvem do Azure Olá projeto tooyour.</span><span class="sxs-lookup"><span data-stu-id="b4f07-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="b4f07-190">Criar um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-190">Create an Azure cloud service</span></span>
<span data-ttu-id="b4f07-191">Um serviço de nuvem do Azure é Olá ambiente Olá aplicativo será executado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="b4f07-192">No navegador, abra Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4f07-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b4f07-193">Clique em **Novo > Computação > Serviço de Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="b4f07-194">Na caixa entrada do nome do DNS de hello, digite um prefixo de URL para serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="b4f07-195">Esse URL tem toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-195">This URL has toobe unique.</span></span>  <span data-ttu-id="b4f07-196">Você obterá uma mensagem de erro se você escolher de prefixo de saudação já está em uso.</span><span class="sxs-lookup"><span data-stu-id="b4f07-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="b4f07-197">Especifique um novo grupo de recursos para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="b4f07-198">Clique em **criar novo** e, em seguida, digite um nome na Olá recurso grupo caixa de entrada, como CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="b4f07-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="b4f07-199">Escolha a região Olá onde você deseja que o aplicativo de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b4f07-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="b4f07-200">Este campo especifica em qual datacenter seu serviço de nuvem será hospedado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="b4f07-201">Para um aplicativo de produção, você escolheria Olá região mais próxima tooyour os clientes.</span><span class="sxs-lookup"><span data-stu-id="b4f07-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="b4f07-202">Para este tutorial, escolha Olá região mais próxima tooyou.</span><span class="sxs-lookup"><span data-stu-id="b4f07-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="b4f07-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-203">Click **Create**.</span></span>

    <span data-ttu-id="b4f07-204">Em Olá a imagem a seguir, um serviço de nuvem é criado com hello CSvccontosoads.cloudapp.net de URL.</span><span class="sxs-lookup"><span data-stu-id="b4f07-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Novo serviço de nuvem](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="b4f07-206">Criar um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-206">Create an Azure SQL database</span></span>
<span data-ttu-id="b4f07-207">Quando o aplicativo hello é executado na nuvem hello, ele usará um banco de dados baseado em nuvem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="b4f07-208">Em Olá [portal do Azure](https://portal.azure.com), clique em **Novo > bancos de dados > banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="b4f07-209">Em Olá **nome do banco de dados** , digite *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="b4f07-210">Em Olá **grupo de recursos**, clique em **usar existente** Olá selecione grupo de recursos usados para o serviço de nuvem hello e.</span><span class="sxs-lookup"><span data-stu-id="b4f07-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="b4f07-211">No hello após a imagem, clique em **Server - definir configurações obrigatórias** e **criar um novo servidor**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Servidor de encapsulamento de toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="b4f07-213">Como alternativa, se a sua assinatura já tem um servidor, você pode selecionar o servidor da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="b4f07-214">Em Olá **nome do servidor** , digite *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="b4f07-215">Insira um **Nome de Logon** e **Senha** de administrador.</span><span class="sxs-lookup"><span data-stu-id="b4f07-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="b4f07-216">Se você selecionou **Criar um novo servidor**, não digitará um nome e senha existentes aqui.</span><span class="sxs-lookup"><span data-stu-id="b4f07-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="b4f07-217">Você está inserindo um novo nome e uma senha que você está definindo agora toouse posterior ao acessar o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="b4f07-218">Se você tiver selecionado um servidor que você criou anteriormente, você será solicitado a fornecer as conta de usuário administrativo toohello senha Olá já criado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="b4f07-219">Escolha Olá mesmo **local** que você escolheu para o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="b4f07-220">Quando o serviço de nuvem hello e banco de dados estão em diferentes datacenters (regiões diferentes), a latência aumentará e você será cobrado por largura de banda fora Olá data center.</span><span class="sxs-lookup"><span data-stu-id="b4f07-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="b4f07-221">A largura de banda em um data center é gratuita.</span><span class="sxs-lookup"><span data-stu-id="b4f07-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="b4f07-222">Verificar **permitir servidor de tooaccess de serviços do azure**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="b4f07-223">Clique em **selecione** para novo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-223">Click **Select** for hello new server.</span></span>

    ![Novo servidor do Banco de Dados SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="b4f07-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="b4f07-226">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-226">Create an Azure storage account</span></span>
<span data-ttu-id="b4f07-227">Uma conta de armazenamento do Azure fornece recursos para armazenar dados blob e fila na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="b4f07-228">Em um aplicativo do mundo real, geralmente você cria contas separadas para dados de aplicativos e dados de log, e contas separadas para dados de teste e dados de produção.</span><span class="sxs-lookup"><span data-stu-id="b4f07-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="b4f07-229">Neste tutorial você usará apenas uma conta.</span><span class="sxs-lookup"><span data-stu-id="b4f07-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="b4f07-230">Em Olá [portal do Azure](https://portal.azure.com), clique em **Novo > armazenamento > conta de armazenamento - blob, arquivo, tabela, fila**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="b4f07-231">Em Olá **nome** , digite um prefixo de URL.</span><span class="sxs-lookup"><span data-stu-id="b4f07-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="b4f07-232">Esse texto de prefixo mais Olá que consulte caixa Olá será Olá exclusivos URL tooyour armazenamento de conta.</span><span class="sxs-lookup"><span data-stu-id="b4f07-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="b4f07-233">Se o prefixo Olá que inserir já foi usado por outra pessoa, você terá toochoose um prefixo diferente.</span><span class="sxs-lookup"><span data-stu-id="b4f07-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="b4f07-234">Saudação de conjunto **modelo de implantação** muito*clássico*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="b4f07-235">Saudação de conjunto **replicação** suspensa lista muito**armazenamento redundante localmente**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="b4f07-236">Quando a replicação geográfica é habilitada para uma conta de armazenamento, o conteúdo de Olá armazenado é replicado tooa datacenter secundário tooenable failover se ocorrer um desastre grave no local primário hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="b4f07-237">A replicação geográfica pode incorrer em custos adicionais.</span><span class="sxs-lookup"><span data-stu-id="b4f07-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="b4f07-238">Para contas de teste e desenvolvimento, geralmente você não quiser toopay para replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="b4f07-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="b4f07-239">Para saber mais, confira [Criar, gerenciar ou excluir uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b4f07-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="b4f07-240">Em Olá **grupo de recursos**, clique em **usar existente** Olá selecione grupo de recursos usados para o serviço de nuvem hello e.</span><span class="sxs-lookup"><span data-stu-id="b4f07-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="b4f07-241">Saudação de conjunto **local** toohello da lista suspensa mesma região que você escolheu para o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="b4f07-242">Quando a conta de serviço e armazenamento de nuvem Olá estão em data centers diferentes (regiões diferentes), a latência aumentará e você será cobrado por largura de banda fora Olá data center.</span><span class="sxs-lookup"><span data-stu-id="b4f07-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="b4f07-243">A largura de banda em um data center é gratuita.</span><span class="sxs-lookup"><span data-stu-id="b4f07-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="b4f07-244">Grupos de afinidade do Azure fornecem uma distância de saudação do mecanismo toominimize entre os recursos em um data center, que pode reduzir a latência.</span><span class="sxs-lookup"><span data-stu-id="b4f07-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="b4f07-245">Este tutorial não usa grupos de afinidade.</span><span class="sxs-lookup"><span data-stu-id="b4f07-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="b4f07-246">Para obter mais informações, consulte [como tooCreate uma grupo de afinidade no Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4f07-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="b4f07-247">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-247">Click **Create**.</span></span>

    ![Nova conta de armazenamento](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="b4f07-249">Na imagem hello, uma conta de armazenamento é criada com a URL de saudação `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="b4f07-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="b4f07-250">Configurar Olá solução toouse seu banco de dados SQL do Azure quando ele é executado no Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="b4f07-251">Olá projeto web e trabalhador projeto de função de cada hello tem sua própria cadeia de caracteres de conexão do banco de dados, e cada precisa de banco de dados do SQL Azure toopoint toohello quando o aplicativo hello é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="b4f07-252">Você usará um [transformação do Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) para função de web hello e uma configuração de ambiente de serviço de nuvem para função de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="b4f07-253">Nesta seção e a próxima seção do hello, você armazenar credenciais em arquivos de projeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="b4f07-254">[Não armazene dados confidenciais em repositórios de código-fonte público](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="b4f07-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="b4f07-255">No projeto de ContosoAdsWeb Olá, abra Olá *Web.Release.config* arquivo de transformação para o aplicativo hello *Web. config* de arquivos, excluir o bloco de comentário hello que contém um `<connectionStrings>` elemento e colar Olá seguindo o código em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="b4f07-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="b4f07-256">Deixe o arquivo hello abertos para edição.</span><span class="sxs-lookup"><span data-stu-id="b4f07-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="b4f07-257">Em Olá [portal do Azure](https://portal.azure.com), clique em **bancos de dados SQL** no painel esquerdo do hello, clique Olá banco de dados criado para este tutorial e, em seguida, clique em **Mostrar cadeias de conexão**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Mostrar cadeias de conexão](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="b4f07-259">o portal de saudação exibe cadeias de caracteres de conexão, com um espaço reservado para senha hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Cadeias de conexão](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="b4f07-261">Em Olá *Web.Release.config* arquivo de transformação, exclua `{connectionstring}` e colar no seu Olá local cadeia de conexão ADO.NET do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="b4f07-262">Na cadeia de caracteres de conexão de saudação que você colou no hello *Web.Release.config* transformar o arquivo, substitua `{your_password_here}` com senha Olá criada para o novo SQL database hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="b4f07-263">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-263">Save hello file.</span></span>  
6. <span data-ttu-id="b4f07-264">Selecione e copie a cadeia de caracteres de conexão de saudação (sem Olá ao redor aspas) para uso em Olá seguindo as etapas para configurar o projeto de função de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="b4f07-265">Em **Solution Explorer**, em **funções** no projeto de serviço de nuvem hello, clique com botão direito **ContosoAdsWorker** e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="b4f07-267">Clique em Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="b4f07-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="b4f07-268">Alterar **configuração do serviço** muito**nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="b4f07-269">Selecione Olá **valor** campo Olá `ContosoAdsDbConnectionString` configuração e, em seguida, cole a cadeia de caracteres de conexão de saudação que você copiou da seção anterior de saudação do tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Cadeia de conexão de banco de dados para função de trabalho](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="b4f07-271">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b4f07-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="b4f07-272">Configurar Olá solução toouse sua conta de armazenamento do Azure quando ele é executado no Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="b4f07-273">Cadeias de caracteres de conexão conta de armazenamento do Azure para o projeto de função web hello e projeto de função de trabalho Olá são armazenadas nas configurações do ambiente no projeto de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="b4f07-274">Para cada projeto, há um conjunto separado de configurações toobe usado quando o aplicativo hello é executado localmente e quando ele é executado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="b4f07-275">Você atualizará as configurações de ambiente de nuvem Olá para projetos de função da web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f07-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="b4f07-276">Em **Solution Explorer**, clique com botão direito **ContosoAdsWeb** em **funções** em hello **ContosoAdsCloudService** do projeto e, em seguida, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="b4f07-278">Clique em Olá **configurações** guia. Em Olá **configuração do serviço** suspensa caixa, escolha **nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Configuração de nuvem](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="b4f07-280">Selecione Olá **StorageConnectionString** entrada e você verá um botão de reticências (**...** ) botão final saudação à direita da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="b4f07-281">Clique em Olá Olá de tooopen do botão de reticências **criar cadeia de Conexão de conta de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Abra a caixa Criar Cadeia de Conexão](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="b4f07-283">Em Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo, clique em **sua assinatura**, escolha a conta de armazenamento Olá que você criou anteriormente e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="b4f07-284">Se você não tiver feito logon, suas credenciais da conta do Azure serão solicitadas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Criar cadeia de conexão de armazenamento](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="b4f07-286">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b4f07-286">Save your changes.</span></span>
6. <span data-ttu-id="b4f07-287">Siga Olá mesmo procedimento usado para Olá `StorageConnectionString` Olá de tooset de cadeia de caracteres de conexão `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f07-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="b4f07-288">Essa cadeia de conexão é usada para o log.</span><span class="sxs-lookup"><span data-stu-id="b4f07-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="b4f07-289">Siga Olá mesmo procedimento usado para Olá **ContosoAdsWeb** tooset função ambas as cadeias de caracteres de conexão para Olá **ContosoAdsWorker** função.</span><span class="sxs-lookup"><span data-stu-id="b4f07-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="b4f07-290">Não se esqueça de tooset **configuração do serviço** muito**nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="b4f07-291">configurações de ambiente de função Hello que você configurou usando Olá IU do Visual Studio são armazenadas no hello arquivos Olá ContosoAdsCloudService projeto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="b4f07-292">*Servicedefinition. Csdef* -define os nomes de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="b4f07-293">*ServiceConfiguration* -fornece valores para quando o aplicativo hello é executado na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="b4f07-294">*ServiceConfiguration* -fornece valores para quando o aplicativo hello é executado localmente.</span><span class="sxs-lookup"><span data-stu-id="b4f07-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="b4f07-295">Por exemplo, Olá servicedefinition. Csdef inclui Olá definições a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="b4f07-296">E hello *ServiceConfiguration* arquivo inclui valores hello inserido para essas configurações no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="b4f07-297">Olá `<Instances>` configuração especifica o número de saudação de máquinas virtuais Azure executará o trabalho Olá código da função no.</span><span class="sxs-lookup"><span data-stu-id="b4f07-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="b4f07-298">Olá [próximas etapas](#next-steps) seção inclui links toomore informações sobre como dimensionar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="b4f07-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="b4f07-299">Implantar Olá projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="b4f07-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="b4f07-300">No **Solution Explorer**, Olá atalho **ContosoAdsCloudService** projeto em nuvem e, em seguida, selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Menu Publicar](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="b4f07-302">Em Olá **entrar** etapa Olá **publicar aplicativo do Azure** assistente, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Etapa de entrada](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="b4f07-304">Em Olá **configurações** etapa do Assistente de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Etapa configurações](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="b4f07-306">Olá configurações padrão do hello **avançado** guia são permitidas para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4f07-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="b4f07-307">Para obter informações sobre a guia Avançado hello, consulte [Assistente de aplicativo do Azure publicação](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4f07-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="b4f07-308">Em Olá **resumo** etapa, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Etapa de resumo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="b4f07-310">Olá **o Log de atividades do Azure** janela será aberta no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="b4f07-311">Clique em detalhes da implantação do hello ícone tooexpand Olá seta para a direita.</span><span class="sxs-lookup"><span data-stu-id="b4f07-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="b4f07-312">implantação de saudação pode demorar até too5 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b4f07-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Janela Log de atividade do Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="b4f07-314">Quando o status da implantação Olá for concluída, clique em Olá **URL do aplicativo Web** aplicativo hello de toostart.</span><span class="sxs-lookup"><span data-stu-id="b4f07-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="b4f07-315">Agora você pode testar o aplicativo hello por criar, exibir e editar alguns anúncios, como você fez quando você executou o aplicativo hello localmente.</span><span class="sxs-lookup"><span data-stu-id="b4f07-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="b4f07-316">Quando concluir teste, excluir ou parar serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="b4f07-317">Mesmo se você não estiver usando o serviço de nuvem hello, ele é acúmulo de encargos porque os recursos de máquina virtual são reservados para ele.</span><span class="sxs-lookup"><span data-stu-id="b4f07-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="b4f07-318">E se você deixá-lo em execução, qualquer um que encontrar sua URL poderá criar e exibir anúncios.</span><span class="sxs-lookup"><span data-stu-id="b4f07-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="b4f07-319">Em Olá [portal do Azure](https://portal.azure.com), vá toohello **visão geral** guia para seu serviço de nuvem e, em seguida, clique em hello **excluir** botão na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="b4f07-320">Se você quiser apenas tootemporarily impedir que outros usuários acessem o site de saudação, clique em **parar** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="b4f07-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="b4f07-321">Nesse caso, os encargos continuarão tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="b4f07-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="b4f07-322">Você pode seguir uma saudação de toodelete procedimento semelhante conta de armazenamento e de banco de dados SQL quando você não precisa mais deles.</span><span class="sxs-lookup"><span data-stu-id="b4f07-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="b4f07-323">Criar aplicativo hello a partir do zero</span><span class="sxs-lookup"><span data-stu-id="b4f07-323">Create hello application from scratch</span></span>
<span data-ttu-id="b4f07-324">Se você ainda não tiver baixado [aplicativo hello concluída](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="b4f07-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="b4f07-325">Você vai copiar arquivos de projeto Olá baixado no novo projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="b4f07-326">Criando aplicativo da Contoso anúncios hello envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="b4f07-327">Criar um serviço de nuvem na solução Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="b4f07-328">Atualizar e adicionar pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="b4f07-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="b4f07-329">Definir referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-329">Set project references.</span></span>
* <span data-ttu-id="b4f07-330">Configurar cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f07-330">Configure connection strings.</span></span>
* <span data-ttu-id="b4f07-331">Adicionar arquivos de código.</span><span class="sxs-lookup"><span data-stu-id="b4f07-331">Add code files.</span></span>

<span data-ttu-id="b4f07-332">Após a solução Olá é criada, você revisará código Olá projetos de serviço exclusivo toocloud e blobs do Azure e filas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="b4f07-333">Criar um serviço de nuvem na solução Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4f07-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="b4f07-334">No Visual Studio, escolha **novo projeto** de saudação **arquivo** menu.</span><span class="sxs-lookup"><span data-stu-id="b4f07-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="b4f07-335">No painel esquerdo de saudação do hello **novo projeto** caixa de diálogo caixa, expanda **Visual C#** e escolha **nuvem** modelos e, em seguida, escolha Olá **serviço de nuvem do Azure** modelo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="b4f07-336">Nome do projeto hello e solução ContosoAdsCloudService e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Novo Projeto](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="b4f07-338">Em Olá **novo serviço de nuvem do Azure** caixa de diálogo caixa, adicione uma função web e uma função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f07-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="b4f07-339">Nome de função de web hello ContosoAdsWeb e nome de função de trabalho Olá ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="b4f07-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="b4f07-340">(Use o ícone de lápis Olá em nomes de padrão de Olá Olá painel direito toochange das funções hello.)</span><span class="sxs-lookup"><span data-stu-id="b4f07-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Novo Projeto de Serviço de Nuvem](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="b4f07-342">Quando você vir Olá **novo projeto ASP.NET** caixa de diálogo função de web hello, escolha o modelo MVC hello e, em seguida, clique em **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Alterar Autenticação](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="b4f07-344">Em Olá **alterar autenticação** caixa de diálogo caixa, escolha **sem autenticação**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Sem Autenticação](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="b4f07-346">Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="b4f07-347">Em **Solution Explorer**, com o botão direito solução hello (não um dos projetos de saudação) e escolha **Add - novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="b4f07-348">Em Olá **adicionar novo projeto** caixa de diálogo caixa, escolha **Windows** em **Visual C#** em Olá painel esquerdo e clique em Olá **biblioteca de classes** modelo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="b4f07-349">Projeto de saudação do nome *ContosoAdsCommon*e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="b4f07-350">É necessário tooreference saudação do Entity Framework contexto e hello modelo de dados de projetos de função da web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f07-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="b4f07-351">Como alternativa, você poderia definir classes de relacionada ao EF Olá no projeto de função web hello e referência de projeto do projeto de função de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="b4f07-352">Mas na abordagem alternativa de saudação, seu projeto de função de trabalho terá uma referência tooweb os assemblies que não precisa.</span><span class="sxs-lookup"><span data-stu-id="b4f07-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="b4f07-353">Atualizar e adicionar pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="b4f07-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="b4f07-354">Olá abrir **gerenciar pacotes NuGet** caixa de diálogo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="b4f07-355">Na parte superior de saudação da janela hello, selecione **atualizações**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="b4f07-356">Procure Olá *windowsazure* do pacote e se ele estiver na lista de Olá, selecioná-la e escolha tooupdate de projetos da web e de trabalho Olá nele e clique **atualização**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="b4f07-357">biblioteca de cliente de armazenamento Olá é atualizada com mais frequência do que os modelos de projeto do Visual Studio, você geralmente encontrará versão Olá toobe de necessidades de um projeto recém-criado atualizado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="b4f07-358">Na parte superior de saudação da janela hello, selecione **procurar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="b4f07-359">Localize Olá *EntityFramework* NuGet do pacote e instalá-lo em todos os três projetos.</span><span class="sxs-lookup"><span data-stu-id="b4f07-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="b4f07-360">Localize Olá *Microsoft.WindowsAzure.ConfigurationManager* NuGet empacotar e instale-o no projeto de função de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="b4f07-361">Definir referências de projeto</span><span class="sxs-lookup"><span data-stu-id="b4f07-361">Set project references</span></span>
1. <span data-ttu-id="b4f07-362">No projeto de ContosoAdsWeb de saudação, defina uma referência de projeto do ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="b4f07-363">Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **referências** - **adicionar referências**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="b4f07-364">Em Olá **Gerenciador de referências** caixa de diálogo, selecione **solução – projetos** no painel esquerdo do hello, selecione **ContosoAdsCommon**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="b4f07-365">No projeto de ContosoAdsWorker de saudação, defina uma referência de projeto do ContosAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="b4f07-366">ContosoAdsCommon conterá saudação do Entity Framework dados modelo e o contexto de classe, que será usado por ambos os Olá front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b4f07-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="b4f07-367">No projeto de ContosoAdsWorker hello, defina uma referência muito`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="b4f07-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="b4f07-368">Este assembly é usado pelo toothumbnails de imagens do hello tooconvert de back-end.</span><span class="sxs-lookup"><span data-stu-id="b4f07-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="b4f07-369">Configurar cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="b4f07-369">Configure connection strings</span></span>
<span data-ttu-id="b4f07-370">Nesta seção iremos configurar o Armazenamento do Azure e as cadeias de conexão do SQL para o teste local.</span><span class="sxs-lookup"><span data-stu-id="b4f07-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="b4f07-371">instruções de implantação Olá anteriormente no tutorial Olá explicam como tooset a conexão Olá cadeias de caracteres para quando hello aplicativo é executado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="b4f07-372">No projeto de ContosoAdsWeb hello, Olá Abrir aplicativo Web. config e inserir a seguir Olá `connectionStrings` elemento após Olá `configSections` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4f07-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="b4f07-373">Se você estiver usando o Visual Studio 2015 ou superior, substitua "v11.0" por "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="b4f07-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="b4f07-374">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b4f07-374">Save your changes.</span></span>
3. <span data-ttu-id="b4f07-375">No projeto de ContosoAdsCloudService hello, clique com botão direito ContosoAdsWeb em **funções**e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="b4f07-377">Em Olá **ContosAdsWeb [função]** janela Propriedades, clique em Olá **configurações** guia e, em seguida, clique em **Adicionar configuração**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="b4f07-378">Deixe **configuração do serviço** definido muito**todas as configurações de**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="b4f07-379">Adicione uma configuração chamada *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="b4f07-380">Definir **tipo** muito*ConnectionString*e defina **valor** muito*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Nova cadeia de conexão](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="b4f07-382">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b4f07-382">Save your changes.</span></span>
7. <span data-ttu-id="b4f07-383">Siga Olá tooadd do mesmo procedimento uma cadeia de caracteres de conexão de armazenamento nas propriedades da função ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="b4f07-384">Ainda no hello **ContosoAdsWorker [função]** janela Propriedades, adicione outra cadeia de caracteres de conexão:</span><span class="sxs-lookup"><span data-stu-id="b4f07-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="b4f07-385">Nome: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="b4f07-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="b4f07-386">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b4f07-386">Type: String</span></span>
   * <span data-ttu-id="b4f07-387">Valor: Colar Olá a mesma cadeia de caracteres de conexão usada para o projeto de função web hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="b4f07-388">(Olá exemplo a seguir é para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b4f07-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="b4f07-389">Não se esqueça de saudação toochange fonte de dados se você copiar esse exemplo e você estiver usando o Visual Studio 2015 ou superior.)</span><span class="sxs-lookup"><span data-stu-id="b4f07-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="b4f07-390">Adicionar arquivos de código</span><span class="sxs-lookup"><span data-stu-id="b4f07-390">Add code files</span></span>
<span data-ttu-id="b4f07-391">Nesta seção, você copiar arquivos de código da solução Olá baixado em nova solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="b4f07-392">Olá seções a seguir mostrará e explicar as principais partes do código.</span><span class="sxs-lookup"><span data-stu-id="b4f07-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="b4f07-393">tooadd arquivos tooa projeto ou uma pasta, projeto de saudação do botão direito do mouse ou pasta e clique em **adicionar** - **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="b4f07-394">Selecione os arquivos de saudação desejado e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="b4f07-395">Se for perguntado se deseja tooreplace os arquivos existentes, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="b4f07-396">No projeto de ContosoAdsCommon hello, exclua Olá *Class1. CS* de arquivos e adicionar em seu lugar Olá *Ad.cs* e *ContosoAdscontext.cs* arquivos de saudação baixou o projeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="b4f07-397">No projeto de ContosoAdsWeb Olá, adicione Olá seguintes arquivos de projeto Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="b4f07-398">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="b4f07-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="b4f07-399">Em Olá *exibições \ compartilhadas* pasta:  *\_cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="b4f07-400">Em Olá *Views\Home* pasta: *cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="b4f07-401">Em Olá *controladores* pasta: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="b4f07-402">Em Olá *Views\Ad* pasta (criar pasta Olá primeiro): cinco *. cshtml* arquivos.</span><span class="sxs-lookup"><span data-stu-id="b4f07-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="b4f07-403">No projeto de ContosoAdsWorker hello, adicione *WorkerRole.cs* de saudação baixou o projeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="b4f07-404">Você agora pode compilar e executar o aplicativo hello conforme instruído anteriormente no tutorial hello e aplicativo hello usará recursos de emulador de armazenamento e de banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="b4f07-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="b4f07-405">Olá, seções a seguir explicam o código de Olá Olá de tooworking relacionado com o ambiente do Azure, blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="b4f07-406">Este tutorial não explica como controladores MVC toocreate e modos de exibição usando o scaffolding, como toowrite código do Entity Framework que funciona com bancos de dados do SQL Server ou Noções básicas de saudação de programação assíncrona no ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="b4f07-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="b4f07-407">Para obter informações sobre esses tópicos, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="b4f07-408">Introdução ao MVC 5</span><span class="sxs-lookup"><span data-stu-id="b4f07-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="b4f07-409">Introdução ao EF 6 e ao MVC 5</span><span class="sxs-lookup"><span data-stu-id="b4f07-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="b4f07-410">[Programação de tooasynchronous de Introdução no .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="b4f07-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="b4f07-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="b4f07-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="b4f07-412">arquivo de Ad.cs de saudação define um enum de categorias do ad e uma classe de entidade POCO para obter informações do ad.</span><span class="sxs-lookup"><span data-stu-id="b4f07-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="b4f07-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="b4f07-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="b4f07-414">Olá classe ContosoAdsContext Especifica que a classe de Ad de saudação é usada em uma coleção de DbSet, que armazena em um banco de dados SQL do Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="b4f07-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="b4f07-415">classe de saudação tem dois construtores.</span><span class="sxs-lookup"><span data-stu-id="b4f07-415">hello class has two constructors.</span></span> <span data-ttu-id="b4f07-416">Olá primeiro deles é usado pelo projeto da web de saudação e especifica o nome de saudação de uma cadeia de conexão que é armazenada no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="b4f07-417">construtor segundo Olá permite que você toopass na cadeia de caracteres de conexão real Olá usada pelo projeto de função de trabalho hello, pois ele não tem um arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="b4f07-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="b4f07-418">Você viu anteriormente em que essa cadeia de caracteres de conexão foi armazenada, e você verá posteriormente como código Olá recupera a cadeia de caracteres de conexão de saudação quando ele cria a classe DbContext de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="b4f07-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="b4f07-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="b4f07-420">Código que é chamado de hello `Application_Start` método cria um *imagens* contêiner de blob e uma *imagens* fila se ainda não existirem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="b4f07-421">Isso garante que sempre que você começar a usar uma nova conta de armazenamento, ou começar a usar o emulador de armazenamento Olá em um novo computador, fila e o contêiner de blob necessários Olá serão criados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b4f07-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="b4f07-422">Olá conta de armazenamento do código obtém acesso toohello usando a cadeia de conexão de armazenamento de saudação do hello *. cscfg* arquivo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="b4f07-423">Em seguida, ele obtém uma referência toohello *imagens* contêiner de blob, cria o contêiner de saudação se ele ainda não existir, conjuntos de permissões e acesso no novo contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="b4f07-424">Por padrão, novos contêineres somente permitir que os clientes com a conta de armazenamento blobs de tooaccess de credenciais.</span><span class="sxs-lookup"><span data-stu-id="b4f07-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="b4f07-425">site de saudação precisa Olá blobs toobe público para que ele possa exibir imagens usando URLs que blobs de imagem toohello ponto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="b4f07-426">Um código semelhante obtém uma referência toohello *imagens* fila e cria uma nova fila.</span><span class="sxs-lookup"><span data-stu-id="b4f07-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="b4f07-427">Nesse caso, nenhuma alteração de permissão é necessária.</span><span class="sxs-lookup"><span data-stu-id="b4f07-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="b4f07-428">ContosoAdsWeb – \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="b4f07-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="b4f07-429">Olá *cshtml* arquivo define o nome do aplicativo Olá Olá cabeçalho e rodapé e cria uma entrada de menu "Anúncios".</span><span class="sxs-lookup"><span data-stu-id="b4f07-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="b4f07-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="b4f07-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="b4f07-431">Olá *Views\Home\Index.cshtml* arquivo exibe links de categoria na home page do hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="b4f07-432">Olá links passam o valor inteiro Olá Olá `Category` enum em uma página de índice de anúncios de toohello variável de querystring.</span><span class="sxs-lookup"><span data-stu-id="b4f07-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="b4f07-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="b4f07-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="b4f07-434">Em Olá *AdController.cs* arquivo, chamadas de construtor Olá Olá `InitializeStorage` objetos de biblioteca de cliente de armazenamento do Azure do método toocreate que fornecem uma API para trabalhar com blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="b4f07-435">Em seguida, o código de saudação obtém uma referência toohello *imagens* contêiner de blob que você viu anteriormente na *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="b4f07-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="b4f07-436">Enquanto faz isso ele define uma [política de recuperação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) padrão apropriada para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b4f07-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="b4f07-437">política de repetição de retirada exponencial saudação padrão pode travar Olá web app para mais de um minuto em várias tentativas para uma falha temporária.</span><span class="sxs-lookup"><span data-stu-id="b4f07-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="b4f07-438">política de repetição de saudação especificada aqui aguarda três segundos após cada tente para backup toothree tentativas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="b4f07-439">Um código semelhante obtém uma referência toohello *imagens* fila.</span><span class="sxs-lookup"><span data-stu-id="b4f07-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="b4f07-440">A maioria do código do controlador Olá é comum para trabalhar com um modelo de dados do Entity Framework usando uma classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="b4f07-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="b4f07-441">Uma exceção é hello HttpPost `Create` método, que carrega um arquivo e o salva no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="b4f07-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="b4f07-442">associador de modelo Olá fornece um [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método do objeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="b4f07-443">Se o usuário Olá selecionado tooupload um arquivo, código Olá carrega o arquivo hello, salva-o em um blob e atualiza o registro de banco de dados do Ad Olá com uma URL que aponta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="b4f07-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="b4f07-444">Olá código Olá carregamento está em Olá `UploadAndSaveBlobAsync` método.</span><span class="sxs-lookup"><span data-stu-id="b4f07-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="b4f07-445">Ele cria um nome GUID para o blob de hello, carrega e salva Olá arquivo e retorna um blob de referência toohello salvada.</span><span class="sxs-lookup"><span data-stu-id="b4f07-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="b4f07-446">Depois de saudação HttpPost `Create` método carrega um blob e atualizações Olá banco de dados, ele cria um tooinform de mensagem da fila desse processo de back-end que uma imagem está pronta para a miniatura de tooa de conversão.</span><span class="sxs-lookup"><span data-stu-id="b4f07-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="b4f07-447">Olá código para hello HttpPost `Edit` método é semelhante, exceto que se o usuário Olá seleciona um novo arquivo de imagem devem ser excluídos todos os blobs que já existem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="b4f07-448">Olá próximo exemplo mostra o código de saudação que exclui os blobs quando você exclui um anúncio.</span><span class="sxs-lookup"><span data-stu-id="b4f07-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="b4f07-449">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="b4f07-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="b4f07-450">Olá *cshtml* arquivo exibe miniaturas com hello outros dados do ad.</span><span class="sxs-lookup"><span data-stu-id="b4f07-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="b4f07-451">Olá *Details.cshtml* arquivo exibe a imagem em tamanho normal hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="b4f07-452">ContosoAdsWeb - Views\Ad\Create.cshtml e Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="b4f07-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="b4f07-453">Olá *Create.cshtml* e *Edit.cshtml* arquivos especificam que habilita Olá Olá do controlador tooget de codificação de formulário `HttpPostedFileBase` objeto.</span><span class="sxs-lookup"><span data-stu-id="b4f07-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="b4f07-454">Um `<input>` elemento informa Olá navegador tooprovide uma caixa de diálogo de seleção de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="b4f07-455">ContosoAdsWorker - WorkerRole.cs - Método OnStart</span><span class="sxs-lookup"><span data-stu-id="b4f07-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="b4f07-456">ambiente de função de trabalho do Azure Olá chama Olá `OnStart` método hello `WorkerRole` classe quando a função de trabalho Olá é Introdução e chama Olá `Run` método quando hello `OnStart` conclusão do método.</span><span class="sxs-lookup"><span data-stu-id="b4f07-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="b4f07-457">Olá `OnStart` método obtém a cadeia de conexão de banco de dados de saudação do hello *. cscfg* de arquivo e o transmite toohello Entity Framework DbContext classe.</span><span class="sxs-lookup"><span data-stu-id="b4f07-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="b4f07-458">provedor de SQLClient Olá é usado por padrão, portanto Olá provedor não tem toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="b4f07-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="b4f07-459">Depois disso, o método hello obtém uma conta de armazenamento do toohello de referência e cria a fila e o contêiner de blob Olá se não existirem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="b4f07-460">saudação de código que está toowhat semelhante que já vimos na função de web hello `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="b4f07-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="b4f07-461">ContosoAdsWorker - WorkerRole.cs - Método de execução</span><span class="sxs-lookup"><span data-stu-id="b4f07-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="b4f07-462">Olá `Run` método é chamado quando hello `OnStart` método termina o trabalho de inicialização.</span><span class="sxs-lookup"><span data-stu-id="b4f07-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="b4f07-463">método Hello executa um loop infinito que observa para novas mensagens de fila e processa-os quando elas chegam.</span><span class="sxs-lookup"><span data-stu-id="b4f07-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="b4f07-464">Após cada iteração do loop Olá, não se foi encontrada nenhuma mensagem de fila, o programa hello suspenso por um segundo.</span><span class="sxs-lookup"><span data-stu-id="b4f07-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="b4f07-465">Isso impede que funções de trabalho Olá incorrer em custos de transações de armazenamento e tempo excessivos do CPU.</span><span class="sxs-lookup"><span data-stu-id="b4f07-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="b4f07-466">Olá Microsoft Customer Advisory Team informa uma história sobre um desenvolvedor que esqueceu tooinclude isso, implantado tooproduction e à esquerda para férias.</span><span class="sxs-lookup"><span data-stu-id="b4f07-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="b4f07-467">Quando ele foi retornado, sua supervisão custo mais de férias hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="b4f07-468">Às vezes, conteúdo de saudação de uma mensagem da fila causa um erro no processamento.</span><span class="sxs-lookup"><span data-stu-id="b4f07-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="b4f07-469">Isso é chamado de um *mensagem suspeita*, e se você acabou de registrou um erro e reiniciado loop hello, infinitamente tente tooprocess essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="b4f07-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="b4f07-470">Portanto o bloco catch de saudação inclui um se instrução que verifica toosee quantas vezes Olá aplicativo tentou tooprocess Olá mensagem atual e se foram mais de 5 vezes, mensagem de saudação será excluída da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="b4f07-471">`ProcessQueueMessage` é chamado quando uma mensagem em fila é encontrada.</span><span class="sxs-lookup"><span data-stu-id="b4f07-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="b4f07-472">Esse código lê a URL da imagem Olá Olá banco de dados tooget, converte a miniatura da saudação imagem tooa, salva a miniatura de saudação em um blob, atualiza o banco de dados de saudação com URL de blob em miniatura hello e exclui a mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="b4f07-473">Olá código Olá `ConvertImageToThumbnailJPG` método usa classes no namespace System Drawing Olá para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="b4f07-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="b4f07-474">No entanto, as classes nesse namespace Olá foram projetados para uso com o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="b4f07-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="b4f07-475">Elas não têm suporte para uso em um serviço Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b4f07-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="b4f07-476">Para obter mais informações sobre opções de processamento de imagem, consulte [Geração dinâmica de imagem](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Visão aprofundada de redimensionamento de imagens](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="b4f07-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="b4f07-477">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b4f07-477">Troubleshooting</span></span>
<span data-ttu-id="b4f07-478">Caso algo não funciona enquanto você estiver seguindo as instruções de saudação neste tutorial, aqui estão alguns erros comuns e como tooresolve-los.</span><span class="sxs-lookup"><span data-stu-id="b4f07-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="b4f07-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="b4f07-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="b4f07-480">Olá `RoleEnvironment` objeto é fornecido pelo Azure quando você executar um aplicativo no Azure ou ao executar localmente usando o emulador de computação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="b4f07-481">Se você receber esse erro quando você estiver executando localmente, certifique-se de que você definiu o projeto de ContosoAdsCloudService hello como projeto de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="b4f07-482">Isso configura Olá toorun de projeto usando o emulador de computação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="b4f07-483">Uma das coisas Olá Olá usada pelo aplicativo hello Azure RoleEnvironment para é tooget Olá conexão valores de cadeia que são armazenados no hello *. cscfg* arquivos, portanto, outra causa dessa exceção é uma cadeia de caracteres de conexão ausente.</span><span class="sxs-lookup"><span data-stu-id="b4f07-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="b4f07-484">Certifique-se de que você criou configuração StorageConnectionString Olá tanto de nuvem e configurações locais no projeto de ContosoAdsWeb hello e que você criou duas cadeias de caracteres de conexão para ambas as configurações no projeto de ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="b4f07-485">Se você fizer uma **Localizar tudo** pesquisa para StorageConnectionString na solução inteira hello, você verá ele 9 vezes nos arquivos de 6.</span><span class="sxs-lookup"><span data-stu-id="b4f07-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="b4f07-486">Não é possível substituir tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="b4f07-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="b4f07-487">O valor abaixo do mínimo permitido para a nova porta é de 8080 para o protocolo http</span><span class="sxs-lookup"><span data-stu-id="b4f07-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="b4f07-488">Tente alterar o número da porta Olá usado pelo projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="b4f07-489">Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="b4f07-490">Clique em Olá **Web** guia e, em seguida, altere o número da porta de saudação em Olá **Url do projeto** configuração.</span><span class="sxs-lookup"><span data-stu-id="b4f07-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="b4f07-491">Para outra alternativa que pode resolver o problema de hello, consulte Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4f07-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="b4f07-492">Outros erros que podem ocorrer ao executar localmente</span><span class="sxs-lookup"><span data-stu-id="b4f07-492">Other errors when running locally</span></span>
<span data-ttu-id="b4f07-493">Por nuvem novo padrão projetos de serviço usam Olá computação do Azure emulator express toosimulate Olá ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f07-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="b4f07-494">Esta é uma versão leve do emulador de computação completo hello e em Olá algumas condições emulador completo funcionará quando a versão express Olá não.</span><span class="sxs-lookup"><span data-stu-id="b4f07-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="b4f07-495">toochange Olá emulador completo do projeto toouse hello, clique com botão direito Olá ContosoAdsCloudService e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4f07-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="b4f07-496">Em Olá **propriedades** clique Olá **Web** guia e, em seguida, clique em Olá **emulador completo Use** botão de opção.</span><span class="sxs-lookup"><span data-stu-id="b4f07-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="b4f07-497">No aplicativo de hello ordem toorun com o emulador completo hello, você tem tooopen Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="b4f07-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4f07-498">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4f07-498">Next steps</span></span>
<span data-ttu-id="b4f07-499">Olá aplicativo Contoso anúncios intencionalmente foi mantida simple para obter um tutorial de Introdução.</span><span class="sxs-lookup"><span data-stu-id="b4f07-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="b4f07-500">Por exemplo, ele não implementa [injeção de dependência](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ou hello [repositório e unidade de trabalho padrões](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), não [usam uma interface para registro em log](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), ele não use [ Migrações do Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) alterações do modelo de dados de toomanage ou [resiliência de Conexão EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transitório erros de rede e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b4f07-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="b4f07-501">Aqui estão alguns aplicativos de exemplo de serviço de nuvem que demonstram mais práticas de codificação reais, listadas do menos complexo toomore complexo:</span><span class="sxs-lookup"><span data-stu-id="b4f07-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="b4f07-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="b4f07-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="b4f07-503">Semelhante ao conceito tooContoso anúncios mas implementa recursos mais e mais práticas de codificação do mundo real.</span><span class="sxs-lookup"><span data-stu-id="b4f07-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="b4f07-504">[Aplicativo multicamada de serviço de nuvem do Azure com tabelas, filas e blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="b4f07-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="b4f07-505">Introduz as tabelas do Armazenamento do Azure, bem como blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="b4f07-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="b4f07-506">Com base em uma versão anterior de saudação do SDK do Azure para .NET, exigirá toowork algumas modificações com a versão atual do hello.</span><span class="sxs-lookup"><span data-stu-id="b4f07-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="b4f07-507">[Noções Básicas sobre Serviço de Nuvem no Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="b4f07-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="b4f07-508">Um exemplo abrangente que demonstra uma ampla variedade de práticas recomendadas, produzido pelo grupo Microsoft Patterns e práticas recomendadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f07-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="b4f07-509">Para obter informações gerais sobre o desenvolvimento para a nuvem hello, consulte [criando aplicativos de nuvem do mundo Real com o Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="b4f07-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="b4f07-510">Para um vídeo de Introdução tooAzure armazenamento práticas recomendadas e padrões, consulte [armazenamento do Microsoft Azure – o que há de novo, práticas recomendadas e padrões](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="b4f07-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="b4f07-511">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f07-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="b4f07-512">Serviços de nuvem do Azure Parte 1: Introdução</span><span class="sxs-lookup"><span data-stu-id="b4f07-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="b4f07-513">Como os serviços de nuvem toomanage</span><span class="sxs-lookup"><span data-stu-id="b4f07-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="b4f07-514">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b4f07-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="b4f07-515">Como o provedor de serviço toochoose uma nuvem</span><span class="sxs-lookup"><span data-stu-id="b4f07-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
