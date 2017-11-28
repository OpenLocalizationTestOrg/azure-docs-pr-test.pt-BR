---
title: Flask e Tabela de Armazenamento do Azure com Ferramentas Python 2.2 para Visual Studio
description: "Aprenda a usar o Python Tools para Visual Studio para criar um aplicativo Flask que armazena dados Armazenamento de Dados do Azure e o implanta em Aplicativos Web do Serviço de Aplicativo do Azure."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="a19c7-103">Flask e Tabela de Armazenamento do Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a19c7-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="a19c7-104">Neste tutorial, usaremos o [Python Tools para Visual Studio] para criar um aplicativo Web de votação simples, usando um dos modelos de exemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="a19c7-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="a19c7-105">Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="a19c7-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="a19c7-106">O aplicativo Web de votação define uma abstração para seu repositório, para que você possa alternar facilmente entre diferentes tipos de repositórios (In-Memory, Azure Table Storage, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="a19c7-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="a19c7-107">Aprenderemos como criar uma conta de Armazenamento do Azure, como configurar o aplicativo Web para usar o Armazenamento de Tabela do Azure e como publicar o aplicativo Web nos [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a19c7-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a19c7-108">Confira o [Python Developer Center] para obter mais artigos que abrangem o desenvolvimento de Aplicativos Web do Serviço de Aplicativo do Azure com PTVS usando estruturas da Web Bottle, Flask e Django, com serviços MongoDB, Azure Table Storage, MySQL e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a19c7-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="a19c7-109">Embora este artigo se concentre no Serviço de Aplicativo, as etapas são semelhantes ao desenvolvimento de [Serviços de Nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="a19c7-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a19c7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a19c7-110">Prerequisites</span></span>
* <span data-ttu-id="a19c7-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a19c7-111">Visual Studio 2015</span></span>
* <span data-ttu-id="a19c7-112">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a19c7-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="a19c7-113">[VSIX de amostra de Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a19c7-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="a19c7-114">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="a19c7-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="a19c7-115">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="a19c7-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a19c7-116">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a19c7-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a19c7-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="a19c7-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="a19c7-118">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="a19c7-118">Create the Project</span></span>
<span data-ttu-id="a19c7-119">Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="a19c7-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="a19c7-120">Criaremos um ambiente virtual e instalaremos pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="a19c7-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="a19c7-121">Em seguida, executaremos o aplicativo localmente usando o repositório da memória padrão.</span><span class="sxs-lookup"><span data-stu-id="a19c7-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="a19c7-122">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="a19c7-123">Os modelos de projeto das [VSIX de amostra de Ferramentas Python 2.2 para Visual Studio] estão disponíveis em **Python**, **Amostras**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="a19c7-124">Selecione **Projeto Web Flask de Votações** e clique em OK para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="a19c7-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="a19c7-126">Você será solicitado a instalar pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="a19c7-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="a19c7-127">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-127">Select **Install into a virtual environment**.</span></span>
   
     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="a19c7-129">Selecione **Python 2.7** ou **Python 3.4** como o interpretador base.</span><span class="sxs-lookup"><span data-stu-id="a19c7-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="a19c7-131">Confirme se o aplicativo funciona pressionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="a19c7-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="a19c7-132">Por padrão, o aplicativo usa um repositório da memória que não requer configuração.</span><span class="sxs-lookup"><span data-stu-id="a19c7-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="a19c7-133">Todos os dados são perdidos quando o servidor Web é interrompido.</span><span class="sxs-lookup"><span data-stu-id="a19c7-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="a19c7-134">Clique em **Criar Votações de Exemplo**e, em seguida, clique em uma votação e vote.</span><span class="sxs-lookup"><span data-stu-id="a19c7-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a19c7-136">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a19c7-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="a19c7-137">Para usar as operações de armazenamento, você precisa de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a19c7-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="a19c7-138">Você pode criar uma conta de armazenamento seguindo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="a19c7-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="a19c7-139">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a19c7-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a19c7-140">Clique no ícone **Novo** no canto superior esquerdo do Portal. Em seguida, clique em **Dados + Armazenamento** > **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="a19c7-141">Clique em **Criar**, dê um nome exclusivo à conta de armazenamento e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ela.</span><span class="sxs-lookup"><span data-stu-id="a19c7-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Criação Rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="a19c7-143">Quando a conta de armazenamento for criada, o botão **Notificações** piscará **ÊXITO** em verde e a folha da conta de armazenamento será aberta para mostrar que pertence ao novo grupo de recursos criado.</span><span class="sxs-lookup"><span data-stu-id="a19c7-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="a19c7-144">Clique na parte **Chaves de Acesso** na folha da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a19c7-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="a19c7-145">Anote o nome da conta e a key1.</span><span class="sxs-lookup"><span data-stu-id="a19c7-145">Take note of the account name and the key1.</span></span>
   
      ![simétricas](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="a19c7-147">Precisaremos dessas informações para configurar seu projeto na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="a19c7-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="a19c7-148">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="a19c7-148">Configure the Project</span></span>
<span data-ttu-id="a19c7-149">Nesta seção, configuraremos nosso aplicativo para usar a conta de armazenamento que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="a19c7-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="a19c7-150">Veremos como obter configurações de conexão do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a19c7-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="a19c7-151">Em seguida, executaremos o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="a19c7-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="a19c7-152">No Visual Studio, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="a19c7-153">Clique na guia **Depurar** .</span><span class="sxs-lookup"><span data-stu-id="a19c7-153">Click on the **Debug** tab.</span></span>
   
     ![Configurações de depuração do projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="a19c7-155">Defina os valores de variáveis de ambiente necessários para o aplicativo em **Depurar Comando do Servidor**, **Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="a19c7-156">Isso definirá as variáveis de ambiente quando você **Iniciar a Depuração**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="a19c7-157">Se quiser que as variáveis sejam definidas quando você **Iniciar sem Depurar**, configure também os mesmos valores em **Executar Comando do Servidor**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="a19c7-158">Como alternativa, é possível definir variáveis de ambiente usando o Painel de Controle do Windows.</span><span class="sxs-lookup"><span data-stu-id="a19c7-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="a19c7-159">Esta é uma opção melhor se desejar evitar armazenar credenciais no código-fonte/arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a19c7-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="a19c7-160">Observe que você precisará reiniciar o Visual Studio para que os novos valores de ambiente estejam disponíveis ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a19c7-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="a19c7-161">O código que implementa o repositório do Armazenamento de Tabela do Azure está em **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="a19c7-162">Consulte a [documentação] para obter mais informações sobre como usar o Serviço de Tabela do Python.</span><span class="sxs-lookup"><span data-stu-id="a19c7-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="a19c7-163">Execute o aplicativo com `F5`.</span><span class="sxs-lookup"><span data-stu-id="a19c7-163">Run the application with `F5`.</span></span> <span data-ttu-id="a19c7-164">As votações que são criadas com **Criar Votações de Exemplo** e os dados enviados por voto serão serializados no Armazenamento de Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="a19c7-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a19c7-165">O Ambiente Virtual do Python 2.7 pode causar uma interrupção de exceção no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a19c7-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="a19c7-166">Pressione `F5` para continuar carregando o projeto Web.</span><span class="sxs-lookup"><span data-stu-id="a19c7-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="a19c7-167">Navegue até a página **Sobre** para verificar se o aplicativo está usando o repositório do **Armazenamento de Tabelas do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="a19c7-169">Explorar o Armazenamento de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="a19c7-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="a19c7-170">É fácil exibir e editar tabelas de armazenamento usando o Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a19c7-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="a19c7-171">Nesta seção, usaremos o Gerenciador de Servidores para visualizar o conteúdo das tabelas do aplicativo de pesquisas.</span><span class="sxs-lookup"><span data-stu-id="a19c7-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="a19c7-172">Isso requer que o Microsoft Azure Tools seja instalado, disponível como parte do [SDK do Azure para .NET].</span><span class="sxs-lookup"><span data-stu-id="a19c7-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="a19c7-173">Abra o **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="a19c7-174">Expanda **Contas de Armazenamento**, sua conta de armazenamento e, em seguida, **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="a19c7-176">Clique duas vezes na tabela **votações** ou **opções** para exibir o conteúdo da tabela em uma janela do documento, bem como adicionar/remover/editar entidades.</span><span class="sxs-lookup"><span data-stu-id="a19c7-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="a19c7-178">Publicar aplicativo Web para Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a19c7-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="a19c7-179">O SDK .NET do Azure fornece uma forma fácil de implantar seu aplicativo Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a19c7-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="a19c7-180">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="a19c7-182">Clique em **Aplicativos Web do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="a19c7-183">Clique em **Novo** para criar um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a19c7-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="a19c7-184">Preencha os campos a seguir e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="a19c7-185">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="a19c7-185">**Web App name**</span></span>
   * <span data-ttu-id="a19c7-186">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="a19c7-186">**App Service plan**</span></span>
   * <span data-ttu-id="a19c7-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="a19c7-187">**Resource group**</span></span>
   * <span data-ttu-id="a19c7-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="a19c7-188">**Region**</span></span>
   * <span data-ttu-id="a19c7-189">Deixe **Servidor de banco de dados** definido como **Nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="a19c7-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="a19c7-190">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="a19c7-191">Seu navegador da Web será aberto automaticamente para o aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="a19c7-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="a19c7-192">Se navegar até a página Sobre, você verá que ela usa o repositório **Na memória**, não o repositório do **Armazenamento de Tabelas do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="a19c7-193">Isso ocorre porque as variáveis de ambiente não estão configuradas na instância Aplicativos Web no Serviço de Aplicativo do Azure. Portanto, ele usa os valores padrão especificados em **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="a19c7-194">Configurar a instância Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="a19c7-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="a19c7-195">Nesta seção, configuraremos variáveis do ambiente para a instância de Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="a19c7-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="a19c7-196">No [Portal do Azure](https://portal.azure.com), abra a folha do aplicativo Web clicando em **Procurar** > **Serviços de Aplicativos** > nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a19c7-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="a19c7-197">Na folha do seu aplicativo Web, clique em **Todas as configurações** depois clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="a19c7-198">Role para baixo até a seção **Configurações do aplicativo** e defina os valores para **REPOSITORY\_NAME**, **STORAGE\_NAME** e **STORAGE\_KEY**, conforme descrito na seção **Configurar o projeto** acima.</span><span class="sxs-lookup"><span data-stu-id="a19c7-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Configurações do aplicativo](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="a19c7-200">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="a19c7-200">Click on **Save**.</span></span> <span data-ttu-id="a19c7-201">Depois de receber as notificações indicando que as alterações foram aplicadas, clique em **Procurar** na folha principal do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a19c7-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="a19c7-202">Você deve ver o aplicativo funcionando conforme o esperado, usando o repositório do **Armazenamento de Tabela do Azure** .</span><span class="sxs-lookup"><span data-stu-id="a19c7-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="a19c7-203">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a19c7-203">Congratulations!</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="a19c7-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a19c7-205">Next steps</span></span>
<span data-ttu-id="a19c7-206">Siga estes links para saber mais sobre as ferramentas Python para Visual Studio, Flask e armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="a19c7-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="a19c7-207">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a19c7-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="a19c7-208">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="a19c7-208">[Web Projects]</span></span>
  * <span data-ttu-id="a19c7-209">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="a19c7-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="a19c7-210">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a19c7-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="a19c7-211">[Documentação do Flask]</span><span class="sxs-lookup"><span data-stu-id="a19c7-211">[Flask Documentation]</span></span>
* <span data-ttu-id="a19c7-212">[Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="a19c7-212">[Azure Storage]</span></span>
* <span data-ttu-id="a19c7-213">[SDK do Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="a19c7-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="a19c7-214">[Como usar o serviço de armazenamento de tabela por meio do Python]</span><span class="sxs-lookup"><span data-stu-id="a19c7-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a19c7-215">O que mudou</span><span class="sxs-lookup"><span data-stu-id="a19c7-215">What's changed</span></span>
* <span data-ttu-id="a19c7-216">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a19c7-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Serviços de Nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como usar o serviço de armazenamento de tabela por meio do Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[SDK do Azure para .NET]: http://azure.microsoft.com/downloads/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX de amostra de Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do Flask]: http://flask.pocoo.org/
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Armazenamento do Azure]: http://azure.microsoft.com/documentation/services/storage/
[SDK do Azure para Python]: https://github.com/Azure/azure-sdk-for-python
