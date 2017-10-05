---
title: "Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="03386-103">Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="03386-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="03386-104">Você pode conectar um aplicativo do Serviço de Aplicativo do Azure a qualquer recurso local que utilize uma porta TCP estática, como o SQL Server, MySQL, APIs Web HTTP e a maioria dos serviços Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="03386-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="03386-105">Este artigo mostra como criar uma conexão híbrida entre um Serviço de Aplicativo e um banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="03386-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="03386-106">A parte de aplicativos Web do recurso de conexões híbridas está disponível apenas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03386-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="03386-107">Para criar uma conexão nos Serviços BizTalk, consulte [Conexões Híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="03386-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="03386-108">Este conteúdo também se aplica aos Aplicativos Móveis no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="03386-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="03386-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03386-109">Prerequisites</span></span>
* <span data-ttu-id="03386-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="03386-110">An Azure subscription.</span></span> <span data-ttu-id="03386-111">Para uma assinatura gratuita, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03386-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="03386-112">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03386-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="03386-113">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="03386-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="03386-114">Para usar um banco de dados local SQL Server ou SQL Server Express com uma conexão híbrida, o TCP/IP precisa ser habilitado em uma porta estática.</span><span class="sxs-lookup"><span data-stu-id="03386-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="03386-115">É recomendado usar uma instância padrão no SQL Server porque ele usa a porta estática 1433.</span><span class="sxs-lookup"><span data-stu-id="03386-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="03386-116">Para informações sobre a instalação e a configuração do SQL Server Express para uso com conexões híbridas, consulte [Conectar-se a um SQL Server local por meio de um Site do Azure usando Conexões Híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="03386-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="03386-117">O computador no qual você instala o agente do Hybrid Connection Manager local, descrito posteriormente neste artigo:</span><span class="sxs-lookup"><span data-stu-id="03386-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="03386-118">Precisa ser capaz de conectar-se ao Azure pela porta 5671</span><span class="sxs-lookup"><span data-stu-id="03386-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="03386-119">Precisa ser capaz de atingir o *hostname*:*portnumber* do seu recurso local.</span><span class="sxs-lookup"><span data-stu-id="03386-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="03386-120">As etapas neste artigo pressupõem que você está utilizando o navegador a partir do computador que hospedará o agente local de conexão híbrida.</span><span class="sxs-lookup"><span data-stu-id="03386-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="03386-121">Criar um aplicativo Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="03386-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="03386-122">Se já criou no Portal do Azure um back-end de Aplicativo Móvel ou aplicativo Web que deseja utilizar para este tutorial, você pode pular para [Criar uma Conexão Híbrida e um Serviço do BizTalk](#CreateHC) e começar de lá.</span><span class="sxs-lookup"><span data-stu-id="03386-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="03386-123">No canto superior esquerdo do [Portal do Azure](https://portal.azure.com), clique em **Novo** > **Web + Móvel** > **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="03386-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Novo aplicativo Web][NewWebsite]
2. <span data-ttu-id="03386-125">Na folha **Aplicativo Web**, forneça uma URL e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="03386-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Nome do site][WebsiteCreationBlade]
3. <span data-ttu-id="03386-127">Após alguns momentos, o aplicativo Web é criado e sua folha de aplicativo Web aparece.</span><span class="sxs-lookup"><span data-stu-id="03386-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="03386-128">A lâmina é um painel com rolagem vertical, que permite a você gerenciar o seu site.</span><span class="sxs-lookup"><span data-stu-id="03386-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website executando][WebSiteRunningBlade]
4. <span data-ttu-id="03386-130">Para verificar se o site está funcionando, você pode clicar no ícone **Procurar** para exibir a página padrão.</span><span class="sxs-lookup"><span data-stu-id="03386-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Clique em Procurar para ver seu aplicativo Web][Browse]
   
    ![Página de aplicativo Web padrão][DefaultWebSitePage]

<span data-ttu-id="03386-133">Em seguida, você criará uma conexão híbrida e um serviço do BizTalk para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03386-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="03386-134">Criar uma Conexão Híbrida e um Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="03386-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="03386-135">Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Rede** > **Configurar seus pontos de extremidade de conexão híbrida**.</span><span class="sxs-lookup"><span data-stu-id="03386-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexões Híbridas][CreateHCHCIcon]
2. <span data-ttu-id="03386-137">Na lâmina Conexões Híbridas, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="03386-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="03386-138">A lâmina **Adicionar uma conexão híbrida** se abre.</span><span class="sxs-lookup"><span data-stu-id="03386-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="03386-139">Como essa é sua primeira conexão híbrida, a opção **Nova Conexão Híbrida** fica pré-selecionada e a folha **Criar Conexão Híbrida** se abre para você.</span><span class="sxs-lookup"><span data-stu-id="03386-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Criar uma Conexão Híbrida][TwinCreateHCBlades]
   
    <span data-ttu-id="03386-141">Na lâmina **Criar Conexão Híbrida**:</span><span class="sxs-lookup"><span data-stu-id="03386-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="03386-142">Como **Nome**, forneça um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="03386-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="03386-143">Como **Nome de host**, insira o nome do computador local que hospeda seu recurso.</span><span class="sxs-lookup"><span data-stu-id="03386-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="03386-144">Como **Porta**, insira o número da porta que o seu recurso local utiliza (1433 para uma instância padrão de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="03386-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="03386-145">Clique em **Serviço Biz Talk**</span><span class="sxs-lookup"><span data-stu-id="03386-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="03386-146">A folha **Criar serviço BizTalk** será aberta.</span><span class="sxs-lookup"><span data-stu-id="03386-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="03386-147">Insira um nome para o serviço BizTalk, então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03386-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Criar serviço BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="03386-149">A folha **Criar Serviço BizTalk** é fechada e você retorna à folha **Criar Conexão Híbrida**.</span><span class="sxs-lookup"><span data-stu-id="03386-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="03386-150">Na lâmina Criar Conexão Híbrida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03386-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Clique em OK][CreateBTScomplete]
6. <span data-ttu-id="03386-152">Quando o processo for concluído, a área de notificações no Portal informa a você que a conexão foi criada com sucesso.</span><span class="sxs-lookup"><span data-stu-id="03386-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="03386-153">Na folha do aplicativo Web, o ícone **Conexões híbridas** agora mostra que uma conexão híbrida foi criada.</span><span class="sxs-lookup"><span data-stu-id="03386-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Uma conexão híbrida criada][CreateHCOneConnectionCreated]

<span data-ttu-id="03386-155">Nesse ponto, você concluiu uma parte importante da infraestrutura de conexão híbrida de nuvem.</span><span class="sxs-lookup"><span data-stu-id="03386-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="03386-156">Em seguida, você criará uma parte local correspondente.</span><span class="sxs-lookup"><span data-stu-id="03386-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="03386-157">Instalar o Gerenciador de Conexões Híbridas local para completar a conexão</span><span class="sxs-lookup"><span data-stu-id="03386-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="03386-158">Na folha do aplicativo Web, clique em **Todas as configurações** > **Rede** > **Configurar seus pontos de extremidade de conexão híbrida**.</span><span class="sxs-lookup"><span data-stu-id="03386-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Ícone Conexões Híbridas][HCIcon]
2. <span data-ttu-id="03386-160">Na folha **Conexões Híbridas** a coluna **Status** para o ponto de extremidade adicionado recentemente exibe **Não conectado**.</span><span class="sxs-lookup"><span data-stu-id="03386-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="03386-161">Clique na conexão para configurá-la.</span><span class="sxs-lookup"><span data-stu-id="03386-161">Click the connection to configure it.</span></span>
   
    ![Não conectado][NotConnected]
   
    <span data-ttu-id="03386-163">A lâmina Conexão Híbrida se abre.</span><span class="sxs-lookup"><span data-stu-id="03386-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="03386-165">Na lâmina, clique em **Configuração do Ouvinte**.</span><span class="sxs-lookup"><span data-stu-id="03386-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Clique em Configuração do Ouvinte][ClickListenerSetup]
4. <span data-ttu-id="03386-167">A lâmina **Propriedades da Conexão Híbrida** se abre.</span><span class="sxs-lookup"><span data-stu-id="03386-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="03386-168">Em **Gerenciador de Conexão Híbrida Local**, escolha **Clique aqui para instalar**.</span><span class="sxs-lookup"><span data-stu-id="03386-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Clique aqui para instalar][ClickToInstallHCM]
5. <span data-ttu-id="03386-170">Na caixa de diálogo de aviso de segurança Executar Aplicativo, selecione **Executar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="03386-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Selecione Executar para continuar][ApplicationRunWarning]
6. <span data-ttu-id="03386-172">Na caixa de diálogo **Controle de Conta de Usuário**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="03386-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Selecione Sim][UAC]
7. <span data-ttu-id="03386-174">O Gerenciador de Conexão Híbrida é baixado e instalado para você.</span><span class="sxs-lookup"><span data-stu-id="03386-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalando][HCMInstalling]
8. <span data-ttu-id="03386-176">Quando a instalação é concluída, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="03386-176">When the install completes, click **Close**.</span></span>
   
    ![Clique em Fechar][HCMInstallComplete]
   
    <span data-ttu-id="03386-178">Na folha **Conexões Híbridas**, a coluna **Status** agora exibe **Conectado**.</span><span class="sxs-lookup"><span data-stu-id="03386-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Status Conectado][HCStatusConnected]

<span data-ttu-id="03386-180">Agora que a infraestrutura de conexão híbrida está concluída, você criará um aplicativo híbrido que a utilize.</span><span class="sxs-lookup"><span data-stu-id="03386-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="03386-181">As seções a seguir mostram como usar uma conexão híbrida com um projeto de back-end .NET doa Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="03386-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="03386-182">Configurar o projeto de back-end .NET de aplicativo móvel para se conectar ao banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="03386-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="03386-183">No Serviço de Aplicativo, um projeto de back-end .NET dos Aplicativos Móveis é apenas um aplicativo Web ASP.NET com um SDK de Aplicativos Móveis adicional instalado e inicializado.</span><span class="sxs-lookup"><span data-stu-id="03386-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="03386-184">Para usar seu aplicativo Web como um back-end de Aplicativos Móveis, você deve [baixar e inicializar o SDK de back-end .NET dos Aplicativos Móveis](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="03386-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="03386-185">Para os Aplicativos Móveis, você também precisa definir uma cadeia de conexão do banco de dados local e modifica o back-end para usar essa conexão.</span><span class="sxs-lookup"><span data-stu-id="03386-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="03386-186">No Gerenciador de Soluções no Visual Studio, abra o arquivo Web.config para o back-end .NET do Aplicativos Móveis, localize a seção **connectionStrings** e adicione uma nova entrada do SqlClient semelhante à seguinte, que aponta para o banco de dados do SQL Server local:</span><span class="sxs-lookup"><span data-stu-id="03386-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="03386-187">Lembre-se de substituir `<**secure_password**>` na cadeia de caracteres pela senha que você criou para *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="03386-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="03386-188">Clique em **Salvar** , no Visual Studio, para salvar o arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="03386-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03386-189">Essa configuração de conexão é usada quando a execução ocorre no computador local.</span><span class="sxs-lookup"><span data-stu-id="03386-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="03386-190">Quando a execução é realizada no Azure, essa configuração é substituída pela configuração de conexão definida no portal.</span><span class="sxs-lookup"><span data-stu-id="03386-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="03386-191">Expanda a pasta **Modelos** e abra o arquivo de modelo de dados, que termina em *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="03386-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="03386-192">Modifique o construtor de instância **DbContext** para passar o valor `OnPremisesDBConnection` para o construtor **DbContext** base, como o trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="03386-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="03386-193">O serviço usará a nova conexão para o banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="03386-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="03386-194">Atualize o back-end dos Aplicativos Móveis para usar a cadeia de conexão local</span><span class="sxs-lookup"><span data-stu-id="03386-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="03386-195">Em seguida, você precisa adicionar uma configuração de aplicativo para essa nova cadeia de conexão para que possa ser usado no Azure.</span><span class="sxs-lookup"><span data-stu-id="03386-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="03386-196">No [portal do Azure](https://portal.azure.com) no código do back-end de aplicativo Web do seu Aplicativo Móvel, clique em **Todas as configurações** e em **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="03386-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="03386-197">Na folha **Configurações do aplicativo Web**, role para baixo até **Cadeias de conexão** e adicione uma nova cadeia de conexão do **SQL Server** chamada `OnPremisesDBConnection`, com um valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="03386-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="03386-198">Substitua `<**secure_password**>` pela senha segura do seu banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="03386-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Cadeia de conexão para banco de dados local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="03386-200">Pressione **Salvar** para salvar a conexão híbrida e a cadeia de conexão que acabaram de ser criadas.</span><span class="sxs-lookup"><span data-stu-id="03386-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="03386-201">Neste ponto, você pode publicar novamente o projeto do servidor e testar a nova conexão com os clientes existentes dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="03386-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="03386-202">Os dados serão lidos e gravados no banco de dados local usando a conexão híbrida.</span><span class="sxs-lookup"><span data-stu-id="03386-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="03386-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03386-203">Next Steps</span></span>
* <span data-ttu-id="03386-204">Para obter informações sobre como criar um aplicativo Web ASP.NET que utiliza uma conexão híbrida, consulte [Conectar-se a um SQL Server local a partir de um Site do Azure usando Conexões Híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="03386-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="03386-205">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="03386-205">Additional Resources</span></span>
[<span data-ttu-id="03386-206">Visão geral de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="03386-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="03386-207">Josh Twist apresenta conexões híbridas (vídeo do Channel 9)</span><span class="sxs-lookup"><span data-stu-id="03386-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="03386-208">Site de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="03386-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="03386-209">Serviços BizTalk: guias Painel, Monitor, Escala, Configurar e Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="03386-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="03386-210">Criando uma nuvem híbrida no mundo real com portabilidade perfeita com aplicativo (vídeo no Channel 9)</span><span class="sxs-lookup"><span data-stu-id="03386-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="03386-211">Conectar-se a um SQL Server local a partir de serviços móveis do Azure utilizando Conexões Híbridas (vídeo no Channel 9)</span><span class="sxs-lookup"><span data-stu-id="03386-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="03386-212">O que mudou</span><span class="sxs-lookup"><span data-stu-id="03386-212">What's changed</span></span>
* <span data-ttu-id="03386-213">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="03386-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
