---
title: "aaaCreate um WebJob de .NET no serviço de aplicativo do Azure | Microsoft Docs"
description: "Criar um aplicativo de várias camadas usando o MVC ASP.NET e o Azure. Olá front-end executa em um aplicativo web no serviço de aplicativo do Azure e Olá back end executa como um trabalho Web. Olá aplicativo usa o Entity Framework, o banco de dados SQL e filas de armazenamento do Azure e blobs."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="acc46-105">Criar um Trabalho Web do .NET no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="acc46-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="acc46-106">Este tutorial mostra como toowrite código de um aplicativo ASP.NET MVC 5 multicamado simples que usa Olá [SDK do WebJobs](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="acc46-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="acc46-107">Olá finalidade Olá [SDK do WebJobs](websites-webjobs-resources.md) toosimplify Olá código gravar para tarefas comuns que pode executar um trabalho Web, como processamento de imagem, processamento de fila, agregação de RSS, manutenção de arquivo e enviar emails.</span><span class="sxs-lookup"><span data-stu-id="acc46-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="acc46-108">Olá SDK do WebJobs possui recursos internos para trabalhar com o armazenamento do Azure e o barramento de serviço, para o agendamento de tarefas e tratamento de erros e muitos outros cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="acc46-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="acc46-109">Além disso, ele tem projetado toobe extensível e há um [repositório do código-fonte aberto para extensões](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="acc46-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="acc46-110">aplicativo de exemplo Hello é um quadro de avisos de publicidade.</span><span class="sxs-lookup"><span data-stu-id="acc46-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="acc46-111">Os usuários podem carregar imagens para anúncios e um processo de back-end converte Olá imagens toothumbnails.</span><span class="sxs-lookup"><span data-stu-id="acc46-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="acc46-112">página de lista de ad Olá mostra miniaturas de saudação e página de detalhes do ad Olá mostra a imagem em tamanho normal Olá.</span><span class="sxs-lookup"><span data-stu-id="acc46-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="acc46-113">Esta é uma captura de tela:</span><span class="sxs-lookup"><span data-stu-id="acc46-113">Here's a screenshot:</span></span>

![Lista de anúncios](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="acc46-115">Este aplicativo de exemplo funciona com [filas do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) e [blobs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="acc46-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="acc46-116">Olá tutorial mostra como toodeploy Olá aplicativo muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e [banco de dados do SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="acc46-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="acc46-117"><a id="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="acc46-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="acc46-118">Olá tutorial presume que você sabe como toowork com [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projetos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acc46-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="acc46-119">tutorial de saudação foi gravado originalmente para Visual Studio 2013, mas pode ser usado com versões posteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acc46-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="acc46-120">Se você estiver usando o Visual Studio 2015 ou 2017, tome nota que, antes de executar o aplicativo hello localmente, você deve alterar Olá `Data Source` parte da cadeia de caracteres de conexão de LocalDB do SQL Server a saudação em arquivos Web. config e App. config de saudação de `Data Source=(localdb)\v11.0` muito`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="acc46-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="acc46-121"><a name="note"></a>Você deve ter uma conta do Azure toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="acc46-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="acc46-122">Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): você obtém créditos que você pode usar tootry out paga serviços do Azure e até mesmo depois que eles são usados para cima, você pode manter Olá conta e usar serviços do Azure gratuitos, como sites.</span><span class="sxs-lookup"><span data-stu-id="acc46-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="acc46-123">Seu cartão de crédito nunca será cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.</span><span class="sxs-lookup"><span data-stu-id="acc46-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="acc46-124">É possível [ativar os benefícios do Azure mensais para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): sua assinatura concede créditos todos os meses que podem ser usados para experimentar serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="acc46-125">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="acc46-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="acc46-126">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="acc46-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="acc46-127"><a id="learn"></a>O que você vai aprender</span><span class="sxs-lookup"><span data-stu-id="acc46-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="acc46-128">tutorial de saudação mostra como as tarefas de saudação toodo a seguir:</span><span class="sxs-lookup"><span data-stu-id="acc46-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="acc46-129">Habilite o computador para o desenvolvimento do Azure instalando Olá SDK do Azure (apenas para o Visual Studio 2013 e 2015 usuários).</span><span class="sxs-lookup"><span data-stu-id="acc46-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="acc46-130">Crie um projeto de aplicativo de Console que implanta automaticamente como um trabalho de Web do Azure, quando você implanta o projeto da web associados de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="acc46-131">Teste um back-end do SDK do WebJobs localmente no computador de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="acc46-132">Publica um aplicativo com um back-end tooa da web no aplicativo WebJobs no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="acc46-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="acc46-133">Carregar arquivos e armazená-las em Olá serviço Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="acc46-134">Use Olá SDK do Azure WebJobs toowork com blobs e filas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="acc46-135"><a id="contosoads"></a>Arquitetura do aplicativo</span><span class="sxs-lookup"><span data-stu-id="acc46-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="acc46-136">usa o aplicativo de exemplo Hello Olá [centrado em fila de trabalho padrão](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga trabalho de saudação com uso intensivo de CPU de criação de processo de back-end tooa miniaturas.</span><span class="sxs-lookup"><span data-stu-id="acc46-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="acc46-137">aplicativo Hello armazena anúncios em um banco de dados SQL, usando tabelas de saudação do Entity Framework Code First toocreate e acessar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="acc46-138">Para cada anúncio, o banco de dados de saudação armazena duas URLs: uma para imagem em tamanho normal hello e uma miniatura hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Tabela de anúncios](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="acc46-140">Quando um usuário carrega uma imagem, Olá web app armazena a imagem de saudação em uma [BLOBs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e armazena informações de ad Olá no banco de dados de saudação com uma URL que aponta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="acc46-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="acc46-141">AT Olá mesmo tempo, ele grava um tooan de mensagem da fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="acc46-142">Em um processo de back-end em execução como um trabalho de Web do Azure, Olá SDK do WebJobs sonda fila Olá novas mensagens.</span><span class="sxs-lookup"><span data-stu-id="acc46-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="acc46-143">Quando uma nova mensagem for exibida, Olá WebJob cria uma miniatura para essa imagem e atualizações Olá campo de banco de dados em miniatura do URL para que o ad.</span><span class="sxs-lookup"><span data-stu-id="acc46-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="acc46-144">Aqui está um diagrama que mostra como partes de saudação do aplicativo hello interagem:</span><span class="sxs-lookup"><span data-stu-id="acc46-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Arquitetura do Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="acc46-146">instruções de tutorial Olá aplicam tooAzure SDK para .NET 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="acc46-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="acc46-147"><a id="storage"></a>Criar uma conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="acc46-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="acc46-148">Uma conta de armazenamento do Azure fornece recursos para armazenar dados blob e fila na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="acc46-149">Ele também é usado por Olá dados de log de toostore do SDK do WebJobs para o painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="acc46-150">Em um aplicativo real, você normalmente cria contas à parte para dados de aplicativo em comparação com dados de registro em log e separa contas para dados de teste em comparação com dados de produção.</span><span class="sxs-lookup"><span data-stu-id="acc46-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="acc46-151">Neste tutorial você usará apenas uma conta.</span><span class="sxs-lookup"><span data-stu-id="acc46-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="acc46-152">Olá abrir **Server Explorer** janela no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acc46-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="acc46-153">Saudação de atalho **Azure** nó e, em seguida, clique **conectar tooMicrosoft assinatura do Azure...** .</span><span class="sxs-lookup"><span data-stu-id="acc46-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Conecte-se tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="acc46-155">Entre utilizando suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="acc46-156">Clique com botão direito **armazenamento** em Olá nó do Azure e, em seguida, clique em **criar conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="acc46-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Criar conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="acc46-158">Em Olá **criar conta de armazenamento** caixa de diálogo, digite um nome para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="acc46-159">nome da saudação deve ser exclusivo (nenhuma outra conta de armazenamento do Azure pode ter Olá mesmo nome).</span><span class="sxs-lookup"><span data-stu-id="acc46-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="acc46-160">Se nome hello inserido já está em uso, você obterá uma chance toochange-lo.</span><span class="sxs-lookup"><span data-stu-id="acc46-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="acc46-161">Olá URL tooaccess sua conta de armazenamento será *{name}*. t.</span><span class="sxs-lookup"><span data-stu-id="acc46-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="acc46-162">Saudação de conjunto **região ou grupo de afinidade** tooyou mais próximo da lista suspensa toohello região.</span><span class="sxs-lookup"><span data-stu-id="acc46-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="acc46-163">Essa configuração especifica qual datacenter do Azure hospedará a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="acc46-164">Para este tutorial, sua escolha não fará uma diferença notável.</span><span class="sxs-lookup"><span data-stu-id="acc46-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="acc46-165">No entanto, para um aplicativo da web de produção, você deseja o servidor web e o toobe de conta de armazenamento no hello encargos de saída de dados e latência de toominimize mesma região.</span><span class="sxs-lookup"><span data-stu-id="acc46-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="acc46-166">aplicativo web de saudação (que você criará mais tarde) datacenter deve estar o mais próximo possíveis navegadores toohello acessando Olá web app na latência de toominimize de ordem.</span><span class="sxs-lookup"><span data-stu-id="acc46-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="acc46-167">Saudação de conjunto **replicação** suspensa lista muito**localmente redundante**.</span><span class="sxs-lookup"><span data-stu-id="acc46-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="acc46-168">Quando a replicação geográfica é habilitada para uma conta de armazenamento, o conteúdo de Olá armazenado é replicado tooa datacenter secundário tooenable failover toothat local em caso de um grande desastre no local principal hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="acc46-169">A replicação geográfica pode incorrer em custos adicionais.</span><span class="sxs-lookup"><span data-stu-id="acc46-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="acc46-170">Para contas de teste e desenvolvimento, geralmente você não quiser toopay para replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="acc46-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="acc46-171">Para saber mais, confira [Criar, gerenciar ou excluir uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="acc46-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="acc46-172">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-172">Click **Create**.</span></span>

    ![Nova conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="acc46-174"><a id="download"></a>Baixar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="acc46-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="acc46-175">Baixe e descompacte Olá [concluído solução](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="acc46-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="acc46-176">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acc46-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="acc46-177">De saudação **arquivo** menu escolha **abrir > projeto/solução**, navegue toowhere baixado solução hello e, em seguida, abra o arquivo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="acc46-178">Pressione a solução de saudação toobuild CTRL + SHIFT + B.</span><span class="sxs-lookup"><span data-stu-id="acc46-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="acc46-179">Por padrão, o Visual Studio automaticamente restaura Olá NuGet conteúdo do pacote, que não foi incluído no hello *. zip* arquivo.</span><span class="sxs-lookup"><span data-stu-id="acc46-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="acc46-180">Se não restaurar os pacotes de saudação, instalá-los manualmente por vai toohello **gerenciar pacotes NuGet para solução** caixa de diálogo e clicar em Olá **restaurar** botão na parte superior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="acc46-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="acc46-181">Em **Solution Explorer**, certifique-se de que **ContosoAdsWeb** é selecionado como projeto de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="acc46-182"><a id="configurestorage"></a>Configurar Olá aplicativo toouse sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="acc46-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="acc46-183">Abra o aplicativo hello *Web. config* arquivo hello ContosoAdsWeb projeto.</span><span class="sxs-lookup"><span data-stu-id="acc46-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="acc46-184">arquivo Hello contém uma cadeia de caracteres de conexão SQL e uma cadeia de caracteres de conexão de armazenamento do Azure para trabalhar com blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="acc46-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="acc46-185">saudação de cadeia de caracteres de conexão SQL pontos tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) banco de dados.</span><span class="sxs-lookup"><span data-stu-id="acc46-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="acc46-186">cadeia de caracteres de conexão de armazenamento Olá é um exemplo que tem espaços reservados para a chave de acesso e do nome de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="acc46-187">Isso será substituído com uma cadeia de caracteres de conexão que tem o nome de saudação e a chave da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="acc46-188">cadeia de caracteres de conexão de armazenamento Olá é chamada AzureWebJobsStorage porque é Olá Olá de nome que SDK do WebJobs usa por padrão.</span><span class="sxs-lookup"><span data-stu-id="acc46-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="acc46-189">saudação de mesmo nome é usado aqui para que você tenha tooset valor de cadeia de caracteres de apenas uma conexão em Olá ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="acc46-190">Em **Server Explorer**, com o botão direito sua conta de armazenamento em Olá **armazenamento** nó e, em seguida, clique **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="acc46-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Clique em Propriedades da Conta de Armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="acc46-192">Em Olá **propriedades** janela, clique em **chaves da conta de armazenamento**e em seguida, clique nas reticências de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Chaves da conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="acc46-194">Saudação de cópia **cadeia de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="acc46-194">Copy hello **Connection String**.</span></span>

    ![Caixa de diálogo Chaves da Conta de Armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="acc46-196">Substitua a cadeia de caracteres de conexão de armazenamento a saudação em Olá *Web. config* arquivo com a cadeia de caracteres de conexão de saudação copiado.</span><span class="sxs-lookup"><span data-stu-id="acc46-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="acc46-197">Certifique-se de que selecionar todos os itens dentro de aspas hello, mas não incluindo Olá aspas antes de colá-lo.</span><span class="sxs-lookup"><span data-stu-id="acc46-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="acc46-198">Olá abrir *App. config* arquivo hello ContosoAdsWebJob projeto.</span><span class="sxs-lookup"><span data-stu-id="acc46-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="acc46-199">Esse arquivo tem duas cadeias de conexão de armazenamento: uma para dados do aplicativo e outra para registro em log.</span><span class="sxs-lookup"><span data-stu-id="acc46-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="acc46-200">Você pode usar contas de armazenamento separadas para dados de aplicativo e registro em log, além de usar [várias contas de armazenamento para dados](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="acc46-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="acc46-201">Neste tutorial, você usará uma única conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="acc46-202">cadeias de caracteres de conexão Olá tem espaços reservados para chaves de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="acc46-203">Por padrão, a saudação SDK do WebJobs procura cadeias de caracteres de conexão chamadas AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="acc46-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="acc46-204">Como alternativa, você pode [armazenar a cadeia de caracteres de conexão de saudação no entanto, você deseja e passá-lo no explicitamente toohello `JobHost` objeto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="acc46-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="acc46-205">Substitua ambas as cadeias de caracteres de conexão de armazenamento com a cadeia de caracteres de conexão de saudação copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="acc46-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="acc46-206">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="acc46-206">Save your changes.</span></span>

## <span data-ttu-id="acc46-207"><a id="run"></a>Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="acc46-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="acc46-208">web toostart Olá front-end do aplicativo hello, pressione CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="acc46-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="acc46-209">navegador padrão de saudação abre toohello home page.</span><span class="sxs-lookup"><span data-stu-id="acc46-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="acc46-210">(projeto da web de saudação é executado porque você fez o projeto de inicialização hello.)</span><span class="sxs-lookup"><span data-stu-id="acc46-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Home page dos Anúncios da Contoso](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="acc46-212">toostart Olá WebJob back-end do aplicativo hello, clique com botão direito Olá ContosoAdsWebJob em **Solution Explorer**e, em seguida, clique em **depurar** > **iniciar nova instância** .</span><span class="sxs-lookup"><span data-stu-id="acc46-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="acc46-213">Uma janela do aplicativo de console é aberto e exibe mensagens de log que indica o objeto de trabalhos Web SDK JobHost Olá iniciou toorun.</span><span class="sxs-lookup"><span data-stu-id="acc46-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Janela de aplicativo de console mostrando que back-end hello está em execução](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="acc46-215">No navegador, clique em **Criar um anúncio**.</span><span class="sxs-lookup"><span data-stu-id="acc46-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="acc46-216">Insira alguns dados de teste, selecione um tooupload de imagem e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Criar página](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="acc46-218">aplicativo Hello vai toohello página de índice, mas ela não mostra uma miniatura para ad novo Olá porque não foi feito ainda que o processamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="acc46-219">Enquanto isso, após uma curta espera uma mensagem de log na janela de aplicativo de console Olá mostra que uma mensagem da fila foi recebida e foi processada.</span><span class="sxs-lookup"><span data-stu-id="acc46-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Janela do aplicativo de console mostrando que uma mensagem da fila foi processada](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="acc46-221">Depois de ver Olá Registrando as mensagens na janela de aplicativo de console hello, atualize Olá índice toosee Olá miniatura.</span><span class="sxs-lookup"><span data-stu-id="acc46-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Página de índice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="acc46-223">Clique em **detalhes** para a imagem em tamanho normal do ad toosee hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Página de detalhes](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="acc46-225">Executa aplicativo hello no computador local e está usando um SQL Server banco de dados localizado em seu computador, mas está trabalhando com filas e blobs no hello nuvem.</span><span class="sxs-lookup"><span data-stu-id="acc46-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="acc46-226">Em Olá seção a seguir você executará aplicativo hello na nuvem hello, usando um banco de dados de nuvem, bem como filas e blobs de nuvem.</span><span class="sxs-lookup"><span data-stu-id="acc46-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="acc46-227"><a id="runincloud"></a>Executar o aplicativo hello na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="acc46-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="acc46-228">Isso será feito Olá aplicativo de hello toorun etapas na nuvem Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="acc46-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="acc46-229">Implante aplicativos tooWeb.</span><span class="sxs-lookup"><span data-stu-id="acc46-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="acc46-230">O Visual Studio cria automaticamente um novo aplicativo Web no Serviço de Aplicativo e uma instância do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="acc46-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="acc46-231">Configure Olá web aplicativo toouse sua conta de armazenamento e de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="acc46-232">Depois de criar alguns anúncios durante a execução na nuvem Olá, você verá Olá Olá toosee de painel de SDK do WebJobs avançado de recursos ele tem toooffer monitoramento.</span><span class="sxs-lookup"><span data-stu-id="acc46-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="acc46-233">Implantar aplicativos tooWeb</span><span class="sxs-lookup"><span data-stu-id="acc46-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="acc46-234">Feche o navegador hello e janela de aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="acc46-235">Siga as etapas de Olá Olá [publicar tooAzure com o banco de dados SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) seção.</span><span class="sxs-lookup"><span data-stu-id="acc46-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="acc46-236">Depois de concluir as etapas de saudação para implantar, continue com as tarefas restantes Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="acc46-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="acc46-237">Configurar Olá web aplicativo toouse sua conta de armazenamento e de banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="acc46-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="acc46-238">É uma prática recomendada de segurança muito[evitar que informações confidenciais, como cadeias de caracteres de conexão nos arquivos que são armazenados em repositórios de código fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="acc46-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="acc46-239">O Azure fornece uma maneira toodo: você pode definir a cadeia de caracteres de conexão e outros valores de configuração no hello ambiente do Azure e APIs de configuração do ASP.NET selecionar automaticamente esses valores quando o aplicativo hello é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="acc46-240">Você pode definir esses valores no Azure usando **Server Explorer**, Olá Portal do Azure, o Windows PowerShell, ou Olá interface de linha de comando de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="acc46-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="acc46-241">Para saber mais, veja [Como funcionam as cadeias de caracteres de aplicativos e de conexão](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="acc46-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="acc46-242">Nesta seção, você deve usar **Server Explorer** tooset valores de cadeia de caracteres de conexão no Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="acc46-243">No **Gerenciador de Servidores**, clique com o botão direito do mouse no aplicativo Web em **Azure > Serviço de Aplicativo > {seu grupo de recursos}** e clique em **Exibir Configurações**.</span><span class="sxs-lookup"><span data-stu-id="acc46-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="acc46-244">Olá **aplicativo Web do Azure** janela será aberta no hello **configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="acc46-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="acc46-245">Alterar o nome de saudação do nome de toohello de cadeia de caracteres de conexão do hello DefaultConnection escolhido quando você configurou o banco de dados SQL Olá no Olá [publicar tooAzure com o banco de dados SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artigo.</span><span class="sxs-lookup"><span data-stu-id="acc46-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="acc46-246">Azure criada automaticamente essa cadeia de caracteres de conexão quando você criou Olá web aplicativo com um banco de dados associado, portanto, já tem o valor de cadeia de caracteres de conexão à direita de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="acc46-247">Você está alterando apenas o hello nome toowhat que seu código está procurando.</span><span class="sxs-lookup"><span data-stu-id="acc46-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="acc46-248">Adicione duas novas cadeias de conexão, chamadas AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="acc46-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="acc46-249">Definir o tipo de banco de dados de saudação muito**personalizado**e o conjunto Olá conexão cadeia valor toohello mesmo valor que você usou anteriormente para Olá *Web. config* e *App. config* arquivos.</span><span class="sxs-lookup"><span data-stu-id="acc46-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="acc46-250">(Certifique-se incluir a cadeia de caracteres de conexão inteira de hello, não apenas chave de acesso do hello e não inclua aspas hello.)</span><span class="sxs-lookup"><span data-stu-id="acc46-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="acc46-251">Essas cadeias de caracteres de conexão são usadas pelo Olá SDK do WebJobs, um para dados de aplicativos e um para o log.</span><span class="sxs-lookup"><span data-stu-id="acc46-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="acc46-252">Como você viu anteriormente, Olá para dados de aplicativos também é usado pelo código do Olá web front-end.</span><span class="sxs-lookup"><span data-stu-id="acc46-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="acc46-253">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-253">Click **Save**.</span></span>

    ![Cadeias de conexão no Portal do Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="acc46-255">Em **Server Explorer**, clique com botão direito Olá web app e, em seguida, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="acc46-256">Depois de parar aplicativo web de saudação, clique novamente o aplicativo web de saudação e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="acc46-257">Olá trabalho Web é iniciado automaticamente quando você publicar, mas é interrompido quando você faz uma alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="acc46-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="acc46-258">toorestart-lo, você pode reiniciar o aplicativo web de saudação ou reiniciar Olá Olá WebJob [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="acc46-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="acc46-259">É geralmente recomendado toorestart Olá web aplicativo após uma alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="acc46-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="acc46-260">Atualize a janela do navegador de saudação que tem a URL do aplicativo web hello na sua barra de endereços.</span><span class="sxs-lookup"><span data-stu-id="acc46-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="acc46-261">Olá home page aparece.</span><span class="sxs-lookup"><span data-stu-id="acc46-261">hello home page appears.</span></span>
8. <span data-ttu-id="acc46-262">Criar um anúncio, como fez quando você [executado localmente o aplicativo hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="acc46-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="acc46-263">página de índice Olá mostra sem uma miniatura primeiro.</span><span class="sxs-lookup"><span data-stu-id="acc46-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="acc46-264">Atualize a página de saudação após alguns segundos e hello miniatura é exibida.</span><span class="sxs-lookup"><span data-stu-id="acc46-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="acc46-265">Se a miniatura Olá não aparecer, você poderá ter toowait aproximadamente um minuto para Olá WebJob toorestart.</span><span class="sxs-lookup"><span data-stu-id="acc46-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="acc46-266">Se após alguns instantes, você ainda não vir miniatura hello quando você atualiza a página hello, Olá trabalho Web pode não ter sido iniciado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="acc46-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="acc46-267">Nesse caso, vá toohello **serviços de aplicativos** folha em Olá [portal do Azure](https://portal.azure.com/), localize seu aplicativo web e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="acc46-268">Saudação de exibição dashboard do SDK do WebJobs</span><span class="sxs-lookup"><span data-stu-id="acc46-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="acc46-269">Em Olá [portal do Azure](https://portal.azure.com/), selecione Olá **folha de serviços de aplicativo**, localize seu aplicativo web e selecione **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="acc46-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="acc46-270">Selecione Olá **Logs** guia.</span><span class="sxs-lookup"><span data-stu-id="acc46-270">Select hello **Logs** tab.</span></span>

    ![Guia logs](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="acc46-272">Uma nova guia do navegador é aberto toohello painel do SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="acc46-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="acc46-273">Painel de saudação mostra que Olá trabalho Web está em execução e mostra uma lista de funções em seu código que Olá disparado do SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="acc46-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="acc46-274">Clique em um dos detalhes de toosee funções hello sobre sua execução.</span><span class="sxs-lookup"><span data-stu-id="acc46-274">Click one of hello functions toosee details about its execution.</span></span>

    ![Painel do SDK de Trabalhos Web](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Painel do SDK de Trabalhos Web](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="acc46-277">Olá **função reprodução** botão nesta página faz com que Olá SDK do WebJobs função do framework toocall hello novamente, e ele fornece uma oportunidade toochange Olá dados passados toohello função primeiro.</span><span class="sxs-lookup"><span data-stu-id="acc46-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="acc46-278">Quando tiver terminado de teste, considere a exclusão Olá web app, conta de armazenamento e sua instância de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="acc46-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="acc46-279">Olá web aplicativo é gratuito, mas hello conta de armazenamento do SQL e a instância de banco de dados acumulam cobranças (embora mínima devido tamanho pequeno toohello).</span><span class="sxs-lookup"><span data-stu-id="acc46-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="acc46-280">Além disso, se você deixar Olá web aplicativo em execução, qualquer pessoa que localiza a URL pode criar e exibir anúncios.</span><span class="sxs-lookup"><span data-stu-id="acc46-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="acc46-281">Excluir seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="acc46-281">Delete your web app</span></span>
<span data-ttu-id="acc46-282">No portal de hello, vá toohello **serviços de aplicativos** folha, localize e selecione o aplicativo web e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="acc46-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="acc46-283">Se você quiser apenas tootemporarily impedir que outros usuários de acessar o aplicativo da web de saudação, clique em **parar** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="acc46-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="acc46-284">Nesse caso, os encargos continuarão tooaccrue para Olá conta de armazenamento e de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="acc46-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="acc46-285">Excluir conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="acc46-285">Delete your storage account</span></span>
<span data-ttu-id="acc46-286">toodelete sua conta de armazenamento, consulte [excluir uma conta de armazenamento](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="acc46-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="acc46-287">Excluir banco de dados</span><span class="sxs-lookup"><span data-stu-id="acc46-287">Delete your database</span></span>
<span data-ttu-id="acc46-288">toodelete SQL de banco de dados, consulte Olá [API de REST de banco de dados SQL do Azure](https://docs.microsoft.com/rest/api/sql/) documentação.</span><span class="sxs-lookup"><span data-stu-id="acc46-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="acc46-289"><a id="create"></a>Criar aplicativo hello a partir do zero</span><span class="sxs-lookup"><span data-stu-id="acc46-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="acc46-290">Nesta seção, você fará Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="acc46-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="acc46-291">Criar uma solução do Visual Studio com um projeto Web.</span><span class="sxs-lookup"><span data-stu-id="acc46-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="acc46-292">Adicionar um projeto de biblioteca de classe para dados saudação camada de acesso que é compartilhada entre Olá front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="acc46-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="acc46-293">Adicione um projeto de aplicativo de Console para o back-end hello, com a implantação de trabalhos Web habilitada.</span><span class="sxs-lookup"><span data-stu-id="acc46-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="acc46-294">Adicionar pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="acc46-294">Add NuGet packages.</span></span>
* <span data-ttu-id="acc46-295">Definir referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="acc46-295">Set project references.</span></span>
* <span data-ttu-id="acc46-296">Copie arquivos de código e configuração do aplicativo de aplicativo hello baixado que trabalhou na seção anterior de saudação do tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="acc46-297">Examine as partes de saudação do código de saudação que funcionam com filas e blobs do Azure e Olá SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="acc46-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="acc46-298">Criar uma solução do Visual Studio com um projeto Web e um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="acc46-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="acc46-299">No Visual Studio, escolha **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="acc46-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="acc46-300">Em Olá **novo projeto** caixa de diálogo, escolha **Visual C#** > **Web** > **o aplicativo Web do ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="acc46-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="acc46-301">Nomeie o projeto de saudação ContosoAdsWeb, nomeie a solução Olá ContosoAdsWebJobsSDK (alterar o nome de solução de saudação se estiver colocando ele em Olá mesma pasta Olá baixado solução) e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="acc46-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Novo Projeto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="acc46-303">Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, escolha o modelo MVC hello e selecione **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="acc46-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Alterar Autenticação](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="acc46-305">Em Olá **alterar autenticação** caixa de diálogo, escolha **sem autenticação**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="acc46-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Sem Autenticação](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="acc46-307">Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="acc46-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="acc46-308">Visual Studio cria solução hello e o projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="acc46-309">Em **Solution Explorer**, com o botão direito solução hello (não o projeto de saudação) e escolha **adicionar** > **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="acc46-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="acc46-310">Em Olá **adicionar novo projeto** caixa de diálogo, escolha **Visual C#** > **área de trabalho clássica do Windows** > **(.NET da biblioteca de classe Framework)** modelo.</span><span class="sxs-lookup"><span data-stu-id="acc46-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="acc46-311">Projeto de saudação do nome *ContosoAdsCommon*e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="acc46-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="acc46-312">Este projeto contém contexto do Entity Framework hello e modelo de dados de saudação que Olá front-end e back-end usará.</span><span class="sxs-lookup"><span data-stu-id="acc46-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="acc46-313">Como alternativa, você poderia definir classes de relacionada ao EF Olá no projeto da web de saudação e referência de projeto do projeto do WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="acc46-314">Mas, em seguida, seu projeto WebJob teria um assemblies de tooweb de referência, que não precisa.</span><span class="sxs-lookup"><span data-stu-id="acc46-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="acc46-315">Adicionar um projeto de Aplicativo do Console com a implantação de Trabalhos Web habilitada</span><span class="sxs-lookup"><span data-stu-id="acc46-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="acc46-316">Clique com botão direito Olá web (não de saudação solução ou projeto de biblioteca de classe Olá) e, em seguida, clique em **adicionar** > **novo projeto do Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="acc46-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Seleção de menu de Novo Projeto de Trabalho Web do Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="acc46-318">Em hello **adicionar Azure WebJob** caixa de diálogo, digite ContosoAdsWebJob como ambos os Olá **nome do projeto** e hello **o nome do WebJob**.</span><span class="sxs-lookup"><span data-stu-id="acc46-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="acc46-319">Deixe **modo de execução do WebJob** definido muito**executar continuamente**.</span><span class="sxs-lookup"><span data-stu-id="acc46-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="acc46-320">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="acc46-320">Click **OK**.</span></span>

   <span data-ttu-id="acc46-321">Visual Studio cria um aplicativo de Console é toodeploy configurado como um trabalho Web sempre que você implantar o projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="acc46-322">toodo que, ela executada Olá tarefas a seguir depois de criar o projeto de saudação:</span><span class="sxs-lookup"><span data-stu-id="acc46-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="acc46-323">Adicionado um *settings.json publicar webjob* arquivo na pasta de propriedades de projeto Olá WebJob.</span><span class="sxs-lookup"><span data-stu-id="acc46-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="acc46-324">Adicionado um *webjobs list.json* arquivo na pasta de propriedades de projeto Olá web.</span><span class="sxs-lookup"><span data-stu-id="acc46-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="acc46-325">Instalado Olá pacote Microsoft.Web.WebJobs.Publish NuGet no projeto do WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="acc46-326">Para obter mais informações sobre essas alterações, consulte [como toodeploy trabalhos Web usando o Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="acc46-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="acc46-327">Adicionar pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="acc46-327">Add NuGet packages</span></span>
<span data-ttu-id="acc46-328">modelo de novo projeto de saudação para um projeto do WebJob instala automaticamente o pacote do NuGet do WebJobs SDK Olá [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="acc46-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="acc46-329">Uma saudação dependências SDK do WebJobs que é instalado automaticamente no projeto do WebJob Olá é Olá biblioteca de cliente de armazenamento do Azure (SCL).</span><span class="sxs-lookup"><span data-stu-id="acc46-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="acc46-330">No entanto, você precisa tooadd-toohello toowork de projeto da web com blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="acc46-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="acc46-331">Olá abrir **gerenciar pacotes NuGet** caixa de diálogo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="acc46-332">No painel esquerdo do hello, selecione **pacotes instalados**.</span><span class="sxs-lookup"><span data-stu-id="acc46-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="acc46-333">Localize Olá *armazenamento do Azure* do pacote e, em seguida, clique em **gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="acc46-334">Em Olá **selecione projetos** caixa, selecione Olá **ContosoAdsWeb** caixa de seleção e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="acc46-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="acc46-335">Todos os três projetos usam saudação do Entity Framework toowork com dados no banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="acc46-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="acc46-336">No painel esquerdo do hello, selecione **Online**.</span><span class="sxs-lookup"><span data-stu-id="acc46-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="acc46-337">Localize Olá *EntityFramework* NuGet do pacote e instalá-lo em todos os três projetos.</span><span class="sxs-lookup"><span data-stu-id="acc46-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="acc46-338">Definir referências de projeto</span><span class="sxs-lookup"><span data-stu-id="acc46-338">Set project references</span></span>
<span data-ttu-id="acc46-339">Web e projetos de trabalho Web trabalham com hello banco de dados SQL para que ambos precisam de uma referência de projeto do ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="acc46-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="acc46-340">No projeto de ContosoAdsWeb de saudação, defina uma referência de projeto do ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="acc46-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="acc46-341">(Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **adicionar** > **referência**.</span><span class="sxs-lookup"><span data-stu-id="acc46-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="acc46-342">Em Olá **Gerenciador de referências** caixa de diálogo, selecione **projetos** > **solução** > **ContosoAdsCommon**e, em seguida, clique em **Okey**.)</span><span class="sxs-lookup"><span data-stu-id="acc46-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="acc46-343">projeto do WebJob Olá precisa referências para trabalhar com imagens e para acessar as cadeias de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="acc46-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="acc46-344">No projeto de ContosoAdsWebJob hello, defina uma referência muito`System.Drawing` e `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="acc46-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="acc46-345">Adicionar código e arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="acc46-345">Add code and configuration files</span></span>
<span data-ttu-id="acc46-346">Este tutorial não mostra como muito[criar controladores MVC e modos de exibição usando o scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), como muito[escrever código do Entity Framework que funciona com bancos de dados do SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), ou [Olá Noções básicas de programação no ASP.NET 4.5 assíncrona](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="acc46-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="acc46-347">Portanto, tudo o que permanece toodo é copiar os arquivos de código e configuração de solução Olá baixado na solução novo hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="acc46-348">Depois de fazer isso, hello seções a seguir mostram e explicam as principais partes do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="acc46-349">tooadd arquivos tooa projeto ou uma pasta, projeto de saudação do botão direito do mouse ou pasta e clique em **adicionar** > **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="acc46-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="acc46-350">Selecione Olá arquivos que você deseja e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="acc46-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="acc46-351">Se for perguntado se deseja tooreplace os arquivos existentes, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="acc46-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="acc46-352">No projeto de ContosoAdsCommon hello, exclua Olá *Class1.cs* de arquivo e adicione seu Olá local seguintes arquivos de projeto Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="acc46-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="acc46-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-353">*Ad.cs*</span></span>
   * <span data-ttu-id="acc46-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="acc46-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="acc46-356">No projeto de ContosoAdsWeb Olá, adicione Olá seguintes arquivos de projeto Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="acc46-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="acc46-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="acc46-357">*Web.config*</span></span>
   * <span data-ttu-id="acc46-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="acc46-359">Em Olá *controladores* pasta: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="acc46-360">Em Olá *exibições \ compartilhadas* pasta: *cshtml* arquivo</span><span class="sxs-lookup"><span data-stu-id="acc46-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="acc46-361">Em Olá *Views\Home* pasta: *cshtml*</span><span class="sxs-lookup"><span data-stu-id="acc46-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="acc46-362">Em Olá *Views\Ad* pasta (criar pasta Olá primeiro): cinco *. cshtml* arquivos</span><span class="sxs-lookup"><span data-stu-id="acc46-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="acc46-363">No projeto de ContosoAdsWebJob Olá, adicione Olá seguintes arquivos de projeto Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="acc46-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="acc46-364">*App. config* (alterar o filtro de tipo de arquivo hello muito**todos os arquivos**)</span><span class="sxs-lookup"><span data-stu-id="acc46-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="acc46-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-365">*Program.cs*</span></span>
   * <span data-ttu-id="acc46-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="acc46-366">*Functions.cs*</span></span>

<span data-ttu-id="acc46-367">Você agora pode criar, executar e implantar o aplicativo hello conforme instruído anteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="acc46-368">Antes de fazer isso, no entanto, pare Olá WebJob ainda está em execução no aplicativo da web primeiro Olá implantada.</span><span class="sxs-lookup"><span data-stu-id="acc46-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="acc46-369">Caso contrário, esse trabalho Web serão processar mensagens da fila criadas localmente ou por aplicativo hello em execução em um novo aplicativo web, desde que todos estão usando Olá mesmo conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="acc46-370"><a id="code"></a>Examine o código do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="acc46-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="acc46-371">Olá, seções a seguir explicam o código de saudação relacionadas tooworking com hello SDK do WebJobs e blobs de armazenamento do Azure e filas.</span><span class="sxs-lookup"><span data-stu-id="acc46-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="acc46-372">Para Olá código específico toohello SDK do WebJobs, vá toohello [Program.cs e Functions.cs](#programcs) seções.</span><span class="sxs-lookup"><span data-stu-id="acc46-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="acc46-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="acc46-374">arquivo de Ad.cs de saudação define um enum de categorias do ad e uma classe de entidade POCO para obter informações do ad.</span><span class="sxs-lookup"><span data-stu-id="acc46-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="acc46-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="acc46-376">Olá classe ContosoAdsContext Especifica que a classe de Ad de saudação é usada em uma coleção DbSet, que armazena o Entity Framework em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="acc46-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="acc46-377">classe de saudação tem dois construtores.</span><span class="sxs-lookup"><span data-stu-id="acc46-377">hello class has two constructors.</span></span> <span data-ttu-id="acc46-378">Olá primeiro é usado pelo projeto da web de saudação e especifica Olá nome de uma cadeia de conexão que é armazenada no arquivo Web. config de saudação ou ambiente de tempo de execução do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="acc46-379">construtor segundo Olá permite que você toopass na cadeia de caracteres de conexão real hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="acc46-380">Necessário ao projeto do WebJob Olá porque ele não tem um arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="acc46-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="acc46-381">Você viu anteriormente em que essa cadeia de caracteres de conexão foi armazenada, e você verá posteriormente como código Olá recupera a cadeia de caracteres de conexão de saudação quando ele cria a classe DbContext de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="acc46-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="acc46-383">Olá `BlobInformation` classe é usada toostore informações sobre um blob de imagem em uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="acc46-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="acc46-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="acc46-385">Código que é chamado de hello `Application_Start` método cria um *imagens* contêiner de blob e uma *imagens* fila se ainda não existirem.</span><span class="sxs-lookup"><span data-stu-id="acc46-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="acc46-386">Isso garante que, sempre que você começar a usar uma nova conta de armazenamento, Olá necessários fila e o contêiner de blob são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="acc46-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="acc46-387">Olá conta de armazenamento do código obtém acesso toohello usando a cadeia de conexão de armazenamento de saudação do hello *Web. config* arquivo ou ambiente de tempo de execução do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="acc46-388">Em seguida, ele obtém uma referência toohello *imagens* contêiner de blob, cria o contêiner de saudação se ele ainda não existir, conjuntos de permissões e acesso no novo contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="acc46-389">Por padrão, novos contêineres permitem somente a clientes com blobs de tooaccess de credenciais de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acc46-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="acc46-390">aplicativo web de saudação precisa Olá blobs toobe público para que ele possa exibir imagens usando URLs que blobs de imagem toohello ponto.</span><span class="sxs-lookup"><span data-stu-id="acc46-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="acc46-391">Um código semelhante obtém uma referência toohello *thumbnailrequest* de fila e cria uma nova fila.</span><span class="sxs-lookup"><span data-stu-id="acc46-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="acc46-392">Nesse caso, nenhuma alteração de permissão é necessária.</span><span class="sxs-lookup"><span data-stu-id="acc46-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="acc46-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="acc46-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="acc46-394">Olá *cshtml* arquivo define o nome do aplicativo Olá Olá cabeçalho e rodapé e cria uma entrada de menu "Anúncios".</span><span class="sxs-lookup"><span data-stu-id="acc46-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="acc46-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="acc46-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="acc46-396">Olá *Views\Home\Index.cshtml* arquivo exibe links de categoria na home page do hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="acc46-397">Olá links passam o valor inteiro Olá Olá `Category` enum em uma página de índice de anúncios de toohello variável de querystring.</span><span class="sxs-lookup"><span data-stu-id="acc46-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="acc46-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="acc46-399">Em Olá *AdController.cs* arquivo, chamadas de construtor Olá Olá `InitializeStorage` objetos de biblioteca de cliente de armazenamento do Azure do método toocreate que fornecem uma API para trabalhar com blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="acc46-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="acc46-400">Em seguida, o código de Olá obtém uma referência toohello *imagens* contêiner de blob que você viu anteriormente na *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="acc46-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="acc46-401">Enquanto faz isso, ele define uma [política de repetição](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) padrão apropriada para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="acc46-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="acc46-402">política de repetição de retirada exponencial saudação padrão pode travar Olá web app para mais de um minuto em várias tentativas para uma falha temporária.</span><span class="sxs-lookup"><span data-stu-id="acc46-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="acc46-403">política de repetição de saudação especificada aqui aguarda três segundos após cada tente para backup toothree tentativas.</span><span class="sxs-lookup"><span data-stu-id="acc46-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="acc46-404">Um código semelhante obtém uma referência toohello *imagens* fila.</span><span class="sxs-lookup"><span data-stu-id="acc46-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="acc46-405">A maioria do código do controlador Olá é comum para trabalhar com um modelo de dados do Entity Framework usando uma classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="acc46-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="acc46-406">Uma exceção é hello HttpPost `Create` método, que carrega um arquivo e o salva no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="acc46-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="acc46-407">associador de modelo Olá fornece um [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método do objeto.</span><span class="sxs-lookup"><span data-stu-id="acc46-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="acc46-408">Se o usuário Olá selecionado tooupload um arquivo, código Olá carrega o arquivo hello, salva-o em um blob e atualiza o registro de banco de dados do Ad Olá com uma URL que aponta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="acc46-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="acc46-409">Olá código Olá carregamento está em Olá `UploadAndSaveBlobAsync` método.</span><span class="sxs-lookup"><span data-stu-id="acc46-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="acc46-410">Ele cria um nome GUID para o blob de hello, carrega e salva Olá arquivo e retorna um blob de referência toohello salvada.</span><span class="sxs-lookup"><span data-stu-id="acc46-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="acc46-411">Depois de saudação HttpPost `Create` método carrega um blob e atualizações Olá banco de dados, ele cria um fila mensagem tooinform Olá processo back-end que uma imagem está pronta para a miniatura de tooa de conversão.</span><span class="sxs-lookup"><span data-stu-id="acc46-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="acc46-412">Olá código para hello HttpPost `Edit` método é semelhante, exceto que se o usuário Olá seleciona um novo arquivo de imagem, todos os blobs que já existem para este anúncio devem ser excluídos.</span><span class="sxs-lookup"><span data-stu-id="acc46-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="acc46-413">Aqui está o código de saudação que exclui os blobs quando você exclui um anúncio:</span><span class="sxs-lookup"><span data-stu-id="acc46-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="acc46-414">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="acc46-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="acc46-415">Olá *cshtml* arquivo exibe miniaturas com hello outros dados do ad:</span><span class="sxs-lookup"><span data-stu-id="acc46-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="acc46-416">Olá *Details.cshtml* arquivo exibe a imagem em tamanho normal hello:</span><span class="sxs-lookup"><span data-stu-id="acc46-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="acc46-417">ContosoAdsWeb - Views\Ad\Create.cshtml e Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="acc46-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="acc46-418">Olá *Create.cshtml* e *Edit.cshtml* arquivos especificam que habilita Olá Olá do controlador tooget de codificação de formulário `HttpPostedFileBase` objeto.</span><span class="sxs-lookup"><span data-stu-id="acc46-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="acc46-419">Um `<input>` elemento informa Olá navegador tooprovide uma caixa de diálogo de seleção de arquivo.</span><span class="sxs-lookup"><span data-stu-id="acc46-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="acc46-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="acc46-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="acc46-421">Quando Olá WebJob inicia, hello `Main` chamadas de método hello SDK do WebJobs `JobHost.RunAndBlock` execução do método toobegin funções disparada no thread atual hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="acc46-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - método GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="acc46-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="acc46-423">Olá SDK do WebJobs chama este método quando é recebida uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="acc46-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="acc46-424">método Hello cria uma miniatura e coloca Olá miniatura URL no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="acc46-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="acc46-425">Olá `QueueTrigger` atributo direciona Olá SDK do WebJobs toocall este método quando uma nova mensagem é recebida na fila de thumbnailrequest hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="acc46-426">Olá `BlobInformation` objeto na mensagem da fila de saudação é automaticamente desserializado em Olá `blobInfo` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc46-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="acc46-427">Quando o método hello for concluído, mensagem de saudação do fila é excluída.</span><span class="sxs-lookup"><span data-stu-id="acc46-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="acc46-428">Se o método hello falhar antes da conclusão, mensagem de saudação do fila não será excluída; Depois que uma concessão de 10 minutos expira, mensagem de saudação é lançada toobe pegou novamente e processado.</span><span class="sxs-lookup"><span data-stu-id="acc46-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="acc46-429">Essa sequência não será repetida indefinidamente se uma mensagem sempre causar uma exceção.</span><span class="sxs-lookup"><span data-stu-id="acc46-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="acc46-430">Depois de 5 malsucedida tentativas tooprocess uma mensagem, mensagem de saudação é movido tooa fila denominada {queuename}-suspeitas.</span><span class="sxs-lookup"><span data-stu-id="acc46-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="acc46-431">Olá o número máximo de tentativas é configurável.</span><span class="sxs-lookup"><span data-stu-id="acc46-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="acc46-432">Olá dois `Blob` atributos fornecem objetos que estão associadas tooblobs: um blob de imagem existente toohello e um tooa novo em miniatura blob criado pelo método hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="acc46-433">Nomes de blob vêm de propriedades de saudação do `BlobInformation` objeto recebido na mensagem da fila de saudação (`BlobName` e `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="acc46-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="acc46-434">tooget Olá todas as funcionalidades de saudação biblioteca de cliente de armazenamento, você pode usar o hello `CloudBlockBlob` toowork de classe com blobs.</span><span class="sxs-lookup"><span data-stu-id="acc46-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="acc46-435">Se você quiser tooreuse código escrito toowork com `Stream` objetos, você pode usar o hello `Stream` classe.</span><span class="sxs-lookup"><span data-stu-id="acc46-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="acc46-436">Para obter mais informações sobre como toowrite funções que usam atributos de SDK do WebJobs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="acc46-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="acc46-437">Como o armazenamento com hello SDK do WebJobs de fila toouse do Azure</span><span class="sxs-lookup"><span data-stu-id="acc46-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="acc46-438">Como toouse Azure blob storage com hello SDK do WebJobs</span><span class="sxs-lookup"><span data-stu-id="acc46-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="acc46-439">Como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure</span><span class="sxs-lookup"><span data-stu-id="acc46-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="acc46-440">Como toouse de barramento de serviço do Azure com hello SDK do WebJobs</span><span class="sxs-lookup"><span data-stu-id="acc46-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="acc46-441">Se seu aplicativo web é executado em várias VMs, vários trabalhos de Web serão executados simultaneamente e em alguns cenários, isso pode resultar em Olá mesmo dados obtendo processados várias vezes.</span><span class="sxs-lookup"><span data-stu-id="acc46-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="acc46-442">Isso não é um problema se você usar fila interna hello, blob e gatilhos de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="acc46-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="acc46-443">Olá SDK garante que as funções serão processadas apenas uma vez para cada mensagem ou blob.</span><span class="sxs-lookup"><span data-stu-id="acc46-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="acc46-444">Para obter informações sobre como tooimplement de desligamento normal, consulte [desligamento](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="acc46-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="acc46-445">Olá código Olá `ConvertImageToThumbnailJPG` método (não mostrado) usa classes Olá `System.Drawing` namespace para simplificar.</span><span class="sxs-lookup"><span data-stu-id="acc46-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="acc46-446">No entanto, as classes nesse namespace Olá foram projetados para uso com o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="acc46-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="acc46-447">Elas não têm suporte para uso em um serviço Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="acc46-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="acc46-448">Para obter mais informações sobre opções de processamento de imagem, consulte [Geração dinâmica de imagem](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Visão aprofundada de redimensionamento de imagens](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="acc46-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="acc46-449">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="acc46-449">Next steps</span></span>
<span data-ttu-id="acc46-450">Neste tutorial, você viu um aplicativo de multicamada simples que usa Olá SDK do WebJobs para o processamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="acc46-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="acc46-451">Esta seção oferece algumas sugestões para saber mais sobre os aplicativos ASP.NET com várias camadas e Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="acc46-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="acc46-452">Recursos ausentes</span><span class="sxs-lookup"><span data-stu-id="acc46-452">Missing features</span></span>
<span data-ttu-id="acc46-453">aplicativo Hello foi mantido simple para obter um tutorial de Introdução.</span><span class="sxs-lookup"><span data-stu-id="acc46-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="acc46-454">Em um aplicativo do mundo real, você poderia implementar [injeção de dependência](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) e hello [repositório e unidade de trabalho padrões](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [uma interface para registro em log](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [ Migrações do Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dados alterações do modelo e usar [resiliência de Conexão EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage erros de rede transitório.</span><span class="sxs-lookup"><span data-stu-id="acc46-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="acc46-455">Dimensionamento de trabalhos</span><span class="sxs-lookup"><span data-stu-id="acc46-455">Scaling WebJobs</span></span>
<span data-ttu-id="acc46-456">Os trabalhos Web executado no contexto de saudação de um aplicativo web e não é escalonáveis separadamente.</span><span class="sxs-lookup"><span data-stu-id="acc46-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="acc46-457">Por exemplo, se você tiver uma instância de aplicativo da web padrão, você tem apenas uma instância do processo em segundo plano em execução e está usando alguns Olá recursos do servidor (CPU, memória, etc.) que de outro modo seria tooserve disponíveis de conteúdo web.</span><span class="sxs-lookup"><span data-stu-id="acc46-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="acc46-458">Se o tráfego varia por hora do dia ou dia da semana, e se Olá back-end de processamento é necessário toodo pode esperar, foi possível agendar o toorun WebJobs em momentos de pouco tráfego.</span><span class="sxs-lookup"><span data-stu-id="acc46-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="acc46-459">Se a carga de saudação ainda é muito alta para essa solução, você pode executar Olá back-end como um trabalho Web em um aplicativo web separado dedicado para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="acc46-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="acc46-460">Em seguida, você pode dimensionar seu aplicativo Web de back-end independentemente do seu aplicativo Web de front-end.</span><span class="sxs-lookup"><span data-stu-id="acc46-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="acc46-461">Para saber mais, veja [Dimensionando WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="acc46-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="acc46-462">Evitando desligamentos de tempo limite de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="acc46-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="acc46-463">toomake-se de que seus WebJobs sempre estão em execução e em execução em todas as instâncias de seu aplicativo web, você tem Olá tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) recurso.</span><span class="sxs-lookup"><span data-stu-id="acc46-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="acc46-464">Usando Olá SDK do WebJobs fora do WebJobs</span><span class="sxs-lookup"><span data-stu-id="acc46-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="acc46-465">Um programa que usa o SDK do WebJobs de saudação não tem toorun no Azure em um trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="acc46-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="acc46-466">Ele pode ser executado localmente e também pode ser executado em outros ambientes, como em uma função de trabalho do serviço de nuvem ou um serviço Windows.</span><span class="sxs-lookup"><span data-stu-id="acc46-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="acc46-467">No entanto, você pode acessar somente Olá painel do SDK do WebJobs por meio de um aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc46-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="acc46-468">Painel de saudação toouse ter tooconnect Olá web aplicativo toohello conta de armazenamento usada ao definir a cadeia de caracteres de conexão do hello AzureWebJobsDashboard em Olá **configurar** guia do portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="acc46-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="acc46-469">Em seguida, você pode obter toohello painel usando Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="acc46-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="acc46-470">https://{NomeDoAplicativoWeb}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="acc46-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="acc46-471">Para obter mais informações, consulte [obtendo um painel para desenvolvimento local com hello SDK do WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mas observe que ela mostra um nome de cadeia de caracteres de conexão antigo.</span><span class="sxs-lookup"><span data-stu-id="acc46-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="acc46-472">Mais documentação de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="acc46-472">More WebJobs documentation</span></span>
<span data-ttu-id="acc46-473">Para sabe r mais, consulte [Recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="acc46-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
