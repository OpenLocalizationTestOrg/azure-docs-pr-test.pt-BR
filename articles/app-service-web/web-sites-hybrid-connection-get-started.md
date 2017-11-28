---
title: "recursos de locais de aaaAccess usando conexões híbridas no serviço de aplicativo do Azure"
description: "Criar uma conexão entre um aplicativo Web no Serviço de Aplicativo do Azure e um recurso local que usa uma porta TCP estática"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="964ac-103">Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="964ac-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="964ac-104">Você pode se conectar a um recurso de local de tooany de aplicativo do serviço de aplicativo do Azure que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP e a maioria dos serviços da Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="964ac-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="964ac-105">Este artigo mostra como toocreate uma conexão híbrida entre o serviço de aplicativo e um banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="964ac-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="964ac-106">parte de aplicativos Web de saudação do recurso de conexões híbridas hello está disponível apenas no hello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="964ac-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="964ac-107">toocreate uma conexão nos serviços do BizTalk, consulte [conexões híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="964ac-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="964ac-108">Este conteúdo também se aplica a aplicativos tooMobile no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="964ac-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="964ac-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="964ac-109">Prerequisites</span></span>
* <span data-ttu-id="964ac-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="964ac-110">An Azure subscription.</span></span> <span data-ttu-id="964ac-111">Para uma assinatura gratuita, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="964ac-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="964ac-112">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="964ac-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="964ac-113">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="964ac-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="964ac-114">toouse um SQL Server no local ou no banco de dados do SQL Server Express com uma conexão híbrida, TCP/IP precisa toobe habilitado em uma porta estática.</span><span class="sxs-lookup"><span data-stu-id="964ac-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="964ac-115">É recomendado usar uma instância padrão no SQL Server porque ele usa a porta estática 1433.</span><span class="sxs-lookup"><span data-stu-id="964ac-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="964ac-116">Para obter informações sobre como instalar e configurar o SQL Server Express para uso com conexões híbridas, consulte [tooan de conexão local do SQL Server de um site do Azure usando conexões híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="964ac-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="964ac-117">computador Olá no qual você instalar agente de Gerenciador de Conexão híbrida local Olá descrito neste artigo:</span><span class="sxs-lookup"><span data-stu-id="964ac-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="964ac-118">Deve ser capaz de tooconnect tooAzure pela porta 5671</span><span class="sxs-lookup"><span data-stu-id="964ac-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="964ac-119">Deve ser capaz de tooreach Olá *hostname*:*portnumber* do recurso local.</span><span class="sxs-lookup"><span data-stu-id="964ac-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="964ac-120">Olá etapas neste artigo presumem que você está usando o navegador de saudação do computador Olá que hospedará o agente de conexão híbrida do hello local.</span><span class="sxs-lookup"><span data-stu-id="964ac-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="964ac-121">Criar um aplicativo web no hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="964ac-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="964ac-122">Se você já tiver criado um aplicativo web ou aplicativo móvel back-end em Olá Portal do Azure que você deseja toouse para este tutorial, você poderá pular muito[criar uma Conexão híbrida e um BizTalk Service](#CreateHC) e iniciar de lá.</span><span class="sxs-lookup"><span data-stu-id="964ac-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="964ac-123">No canto superior esquerdo de saudação da saudação [Portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel** > **aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="964ac-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Novo aplicativo Web][NewWebsite]
2. <span data-ttu-id="964ac-125">Em Olá **aplicativo Web** folha, forneça uma URL e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="964ac-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Nome do site][WebsiteCreationBlade]
3. <span data-ttu-id="964ac-127">Após alguns instantes, Olá web app é criado e aparece de folha do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="964ac-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="964ac-128">folha de saudação é um painel rolável verticalmente que lhe permite gerenciar seu site.</span><span class="sxs-lookup"><span data-stu-id="964ac-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website executando][WebSiteRunningBlade]
4. <span data-ttu-id="964ac-130">site de saudação tooverify está ativo, você pode clicar em Olá **procurar** página padrão do ícone toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="964ac-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Clique em Procurar toosee seu aplicativo web][Browse]
   
    ![Página de aplicativo Web padrão][DefaultWebSitePage]

<span data-ttu-id="964ac-133">Em seguida, você criará uma conexão híbrida e um serviço BizTalk para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="964ac-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="964ac-134">Criar uma Conexão Híbrida e um Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="964ac-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="964ac-135">Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Rede** > **Configurar seus pontos de extremidade de conexão híbrida**.</span><span class="sxs-lookup"><span data-stu-id="964ac-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexões Híbridas][CreateHCHCIcon]
2. <span data-ttu-id="964ac-137">Na folha de conexões do hello híbrida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="964ac-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="964ac-138">Olá **adicionar uma conexão híbrida** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="964ac-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="964ac-139">Como esta é sua primeira conexão de híbrida, Olá **nova conexão de híbrida** opção é pré-selecionada e Olá **criar conexão híbrida** folha é aberto para você.</span><span class="sxs-lookup"><span data-stu-id="964ac-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Criar uma Conexão Híbrida][TwinCreateHCBlades]
   
    <span data-ttu-id="964ac-141">Em Olá **folha de conexão híbrida criar**:</span><span class="sxs-lookup"><span data-stu-id="964ac-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="964ac-142">Para **nome**, forneça um nome para a conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="964ac-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="964ac-143">Para **Hostname**, insira nome de saudação do computador local Olá que hospeda o recurso.</span><span class="sxs-lookup"><span data-stu-id="964ac-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="964ac-144">Para **porta**, digite Olá número da porta que o recurso local (1433 para uma instância do SQL Server padrão).</span><span class="sxs-lookup"><span data-stu-id="964ac-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="964ac-145">Clique em **Serviço Biz Talk**</span><span class="sxs-lookup"><span data-stu-id="964ac-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="964ac-146">Olá **criar serviço de BizTalk** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="964ac-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="964ac-147">Insira um nome para Olá serviço BizTalk e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="964ac-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Criar serviço BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="964ac-149">Olá **criar serviço de BizTalk** folha fecha e você retorna toohello **criar conexão híbrida** folha.</span><span class="sxs-lookup"><span data-stu-id="964ac-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="964ac-150">Na folha de conexão híbrida do criar hello, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="964ac-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Clique em OK][CreateBTScomplete]
6. <span data-ttu-id="964ac-152">Quando Olá processo for concluído, área de notificações de saudação em Olá Portal informa conexão Olá foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="964ac-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="964ac-153">Na folha de seu aplicativo da web Olá Olá **conexões híbridas** ícone agora mostra que 1 conexão de híbrida foi criado.</span><span class="sxs-lookup"><span data-stu-id="964ac-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Uma conexão híbrida criada][CreateHCOneConnectionCreated]

<span data-ttu-id="964ac-155">Neste ponto, você concluiu uma parte importante da infraestrutura de conexão Olá nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="964ac-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="964ac-156">Em seguida, você criará uma parte local correspondente.</span><span class="sxs-lookup"><span data-stu-id="964ac-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="964ac-157">Instalar Olá conexão do Gerenciador de Conexão híbrida toocomplete Olá local</span><span class="sxs-lookup"><span data-stu-id="964ac-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="964ac-158">Na folha do seu aplicativo da web hello, clique em **todas as configurações** > **rede** > **configurar seus pontos de extremidade de conexão híbrida**.</span><span class="sxs-lookup"><span data-stu-id="964ac-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Ícone Conexões Híbridas][HCIcon]
2. <span data-ttu-id="964ac-160">Em Olá **conexões híbridas** folha, Olá **Status** coluna Olá adicionado recentemente mostra de ponto de extremidade **não conectado**.</span><span class="sxs-lookup"><span data-stu-id="964ac-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="964ac-161">Clique em Olá conexão tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="964ac-161">Click hello connection tooconfigure it.</span></span>
   
    ![Não conectado][NotConnected]
   
    <span data-ttu-id="964ac-163">Abre a folha de conexão híbrida Hello.</span><span class="sxs-lookup"><span data-stu-id="964ac-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="964ac-165">Na folha de saudação, clique em **configuração de ouvinte**.</span><span class="sxs-lookup"><span data-stu-id="964ac-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Clique em Configuração do Ouvinte][ClickListenerSetup]
4. <span data-ttu-id="964ac-167">Olá **propriedades da conexão híbrida** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="964ac-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="964ac-168">Em **Gerenciador de Conexão híbrida local**, escolha **clique aqui tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="964ac-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Clique aqui tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="964ac-170">Olá aplicativo executado segurança aviso caixa de diálogo, escolha **executar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="964ac-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Escolha Executar toocontinue][ApplicationRunWarning]
6. <span data-ttu-id="964ac-172">Em Olá **User Account Control** caixa de diálogo, escolha **Sim**.</span><span class="sxs-lookup"><span data-stu-id="964ac-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Selecione Sim][UAC]
7. <span data-ttu-id="964ac-174">Olá Gerenciador de Conexão híbrida é baixado e instalado para você.</span><span class="sxs-lookup"><span data-stu-id="964ac-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalando][HCMInstalling]
8. <span data-ttu-id="964ac-176">Quando a saudação instalação for concluída, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="964ac-176">When hello install completes, click **Close**.</span></span>
   
    ![Clique em Fechar][HCMInstallComplete]
   
    <span data-ttu-id="964ac-178">Em Olá **conexões híbridas** folha, Olá **Status** coluna agora mostra **conectado**.</span><span class="sxs-lookup"><span data-stu-id="964ac-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Status Conectado][HCStatusConnected]

<span data-ttu-id="964ac-180">Essa infra-estrutura de conexão híbrida Olá é concluída, você pode criar um aplicativo híbrido que utiliza.</span><span class="sxs-lookup"><span data-stu-id="964ac-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="964ac-181">Olá seções a seguir mostram como toouse uma conexão híbrida com um projeto de back-end .NET de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="964ac-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="964ac-182">Configurar Olá .NET de aplicativo móvel back-end projeto tooconnect toohello banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="964ac-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="964ac-183">No Serviço de Aplicativo, um projeto de back-end .NET dos Aplicativos Móveis é apenas um aplicativo Web ASP.NET com um SDK de Aplicativos Móveis adicional instalado e inicializado.</span><span class="sxs-lookup"><span data-stu-id="964ac-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="964ac-184">toouse seu aplicativo da web como um back-end de aplicativos móveis, você deve [baixar e inicializar o back-end .NET de aplicativos móveis Olá SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="964ac-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="964ac-185">Para aplicativos móveis, você também precisa toodefine uma cadeia de caracteres de conexão para o banco de dados de local de saudação e modificar Olá back-end toouse essa conexão.</span><span class="sxs-lookup"><span data-stu-id="964ac-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="964ac-186">No Gerenciador de soluções do Visual Studio, o arquivo Web. config Olá abrir seu back-end .NET de aplicativo móvel, localize Olá **connectionStrings** seção, adicione uma nova entrada SqlClient como Olá seguintes, quais pontos toohello SQL local Banco de dados do servidor:</span><span class="sxs-lookup"><span data-stu-id="964ac-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="964ac-187">Lembre-se de tooreplace `<**secure_password**>` na cadeia de caracteres com senha Olá criada para *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="964ac-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="964ac-188">Clique em **salvar** no arquivo Web. config do Visual Studio toosave hello.</span><span class="sxs-lookup"><span data-stu-id="964ac-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="964ac-189">Essa configuração de conexão é usada quando em execução no computador local hello.</span><span class="sxs-lookup"><span data-stu-id="964ac-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="964ac-190">Quando em execução no Azure, essa configuração é substituída pela configuração de conexão Olá definida no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="964ac-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="964ac-191">Expanda Olá **modelos** pasta e arquivo de modelo de dados Olá abertos, que termina em *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="964ac-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="964ac-192">Modificar Olá **DbContext** toopass do construtor de instância Olá valor `OnPremisesDBConnection` toohello base **DbContext** construtor, toohello semelhante trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="964ac-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="964ac-193">serviço de saudação agora usará o banco de dados do hello nova conexão toohello do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="964ac-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="964ac-194">Atualizar a cadeia de conexão Olá aplicativo móvel back-end toouse Olá local</span><span class="sxs-lookup"><span data-stu-id="964ac-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="964ac-195">Em seguida, você precisa tooadd uma configuração de aplicativo para essa nova cadeia de caracteres de conexão para que ele pode ser usado do Azure.</span><span class="sxs-lookup"><span data-stu-id="964ac-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="964ac-196">Em Olá [portal do Azure](https://portal.azure.com) no código de back-end Olá web app para o seu aplicativo móvel, clique em **todas as configurações**, em seguida, **configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="964ac-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="964ac-197">Em Olá **configurações de aplicativo da Web** folha, role para baixo demais**cadeias de caracteres de Conexão** e adicione um novo **do SQL Server** cadeia de caracteres de conexão denominada `OnPremisesDBConnection` com um valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="964ac-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="964ac-198">Substituir `<**secure_password**>` com a senha segura Olá para seu banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="964ac-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Cadeia de conexão para banco de dados local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="964ac-200">Pressione **salvar** conexão do toosave Olá híbrida e a cadeia de caracteres de conexão que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="964ac-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="964ac-201">Neste ponto, você pode republicar o projeto do servidor de saudação e testar conexão nova Olá com os clientes de aplicativos móveis existentes.</span><span class="sxs-lookup"><span data-stu-id="964ac-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="964ac-202">Dados serão leiam e gravados o banco de dados local toohello usando a conexão do hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="964ac-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="964ac-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="964ac-203">Next Steps</span></span>
* <span data-ttu-id="964ac-204">Para obter informações sobre como criar um aplicativo web ASP.NET que usa uma conexão híbrida, consulte [tooan de conexão local do SQL Server de um site do Azure usando conexões híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="964ac-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="964ac-205">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="964ac-205">Additional Resources</span></span>
[<span data-ttu-id="964ac-206">Visão geral de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="964ac-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="964ac-207">Josh Twist apresenta conexões híbridas (vídeo do Channel 9)</span><span class="sxs-lookup"><span data-stu-id="964ac-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="964ac-208">Site de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="964ac-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="964ac-209">Serviços BizTalk: guias Painel, Monitor, Escala, Configurar e Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="964ac-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="964ac-210">Criando uma nuvem híbrida no mundo real com portabilidade perfeita com aplicativo (vídeo no Channel 9)</span><span class="sxs-lookup"><span data-stu-id="964ac-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="964ac-211">Conecte-se tooan do SQL Server de serviços móveis do Azure usando conexões híbridas (vídeo do Channel 9) local</span><span class="sxs-lookup"><span data-stu-id="964ac-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="964ac-212">O que mudou</span><span class="sxs-lookup"><span data-stu-id="964ac-212">What's changed</span></span>
* <span data-ttu-id="964ac-213">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="964ac-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
