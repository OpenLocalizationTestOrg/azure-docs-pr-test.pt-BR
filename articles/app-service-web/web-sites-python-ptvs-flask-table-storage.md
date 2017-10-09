---
title: aaaFlask e armazenamento de tabela do Azure no Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo web bulbo que armazena dados no armazenamento de tabela do Azure e implantá-lo tooAzure aplicativos de Web do serviço de aplicativo."
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
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e993c-103">Flask e Tabela de Armazenamento do Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e993c-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="e993c-104">Neste tutorial, vamos usar [ferramentas Python para Visual Studio] toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="e993c-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="e993c-105">Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="e993c-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="e993c-106">Olá sondagens web aplicativo define uma abstração para seu repositório, assim você pode alternar facilmente entre tipos diferentes de repositórios (na memória, armazenamento de tabela do Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e993c-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="e993c-107">Aprenderá como toocreate um armazenamento do Azure a conta, como tooconfigure Olá web aplicativo toouse armazenamento de tabela do Azure e toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e993c-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e993c-108">Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com os serviços do MongoDB, armazenamento de tabela do Azure, MySQL e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e993c-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="e993c-109">Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="e993c-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e993c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e993c-110">Prerequisites</span></span>
* <span data-ttu-id="e993c-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e993c-111">Visual Studio 2015</span></span>
* <span data-ttu-id="e993c-112">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e993c-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e993c-113">[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e993c-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e993c-114">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="e993c-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e993c-115">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="e993c-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e993c-116">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e993c-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e993c-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e993c-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="e993c-118">Criar hello projeto</span><span class="sxs-lookup"><span data-stu-id="e993c-118">Create hello Project</span></span>
<span data-ttu-id="e993c-119">Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="e993c-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e993c-120">Criaremos um ambiente virtual e instalaremos pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="e993c-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e993c-121">Em seguida, vamos executar aplicativo hello localmente usando o repositório do saudação padrão em memória.</span><span class="sxs-lookup"><span data-stu-id="e993c-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="e993c-122">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e993c-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e993c-123">Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**.</span><span class="sxs-lookup"><span data-stu-id="e993c-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e993c-124">Selecione **sondagens bulbo Web projeto** e clique em projeto de saudação toocreate Okey.</span><span class="sxs-lookup"><span data-stu-id="e993c-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="e993c-126">Você será pacotes externos tooinstall solicitada.</span><span class="sxs-lookup"><span data-stu-id="e993c-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="e993c-127">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="e993c-127">Select **Install into a virtual environment**.</span></span>
   
     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="e993c-129">Selecione **Python 2.7** ou **Python 3.4** como interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="e993c-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e993c-131">Confirme se o aplicativo hello funciona pressionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="e993c-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="e993c-132">Por padrão, o aplicativo hello usa um repositório de memória que não exige qualquer configuração.</span><span class="sxs-lookup"><span data-stu-id="e993c-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="e993c-133">Todos os dados são perdidos quando o servidor de web hello é interrompido.</span><span class="sxs-lookup"><span data-stu-id="e993c-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="e993c-134">Clique em **Criar Votações de Exemplo**e, em seguida, clique em uma votação e vote.</span><span class="sxs-lookup"><span data-stu-id="e993c-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e993c-136">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e993c-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="e993c-137">toouse operações de armazenamento, você precisa de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e993c-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="e993c-138">Você pode criar uma conta de armazenamento seguindo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="e993c-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="e993c-139">Faça logon no hello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e993c-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e993c-140">Clique em Olá **novo** ícone no início de saudação à esquerda da saudação Portal, clique em **dados + armazenamento** > **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e993c-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="e993c-141">Clique em **criar**, dê um nome exclusivo de conta de armazenamento hello e criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ele.</span><span class="sxs-lookup"><span data-stu-id="e993c-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Criação Rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="e993c-143">Quando tiver sido criada a conta de armazenamento hello, Olá **notificações** botão pisca uma verde **êxito** e folha da conta de armazenamento hello está aberta tooshow que ele pertence toohello novo recurso de grupo criado.</span><span class="sxs-lookup"><span data-stu-id="e993c-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="e993c-144">Clique em Olá **chaves de acesso** parte na folha da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e993c-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="e993c-145">Tome nota do nome da conta hello e key1 hello.</span><span class="sxs-lookup"><span data-stu-id="e993c-145">Take note of hello account name and hello key1.</span></span>
   
      ![simétricas](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="e993c-147">Precisaremos este tooconfigure informações seu projeto na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="e993c-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="e993c-148">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="e993c-148">Configure hello Project</span></span>
<span data-ttu-id="e993c-149">Nesta seção, configuraremos nosso conta de armazenamento do aplicativo toouse Olá que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="e993c-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="e993c-150">Vamos ver como as configurações de conexão tooobtain do hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e993c-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="e993c-151">Em seguida, vamos executar aplicativo hello localmente.</span><span class="sxs-lookup"><span data-stu-id="e993c-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="e993c-152">No Visual Studio, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e993c-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="e993c-153">Clique em Olá **depurar** guia.</span><span class="sxs-lookup"><span data-stu-id="e993c-153">Click on hello **Debug** tab.</span></span>
   
     ![Configurações de depuração do projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="e993c-155">Definir valores de saudação de variáveis de ambiente exigidos pelo aplicativo hello em **depurar servidor comando**, **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="e993c-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="e993c-156">Isso definirá as variáveis de ambiente hello quando você **iniciar depuração**.</span><span class="sxs-lookup"><span data-stu-id="e993c-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="e993c-157">Se você quiser Olá variáveis toobe definida quando você **Start Without Debugging**, Olá conjunto mesmo valores em **executar comando de servidor** também.</span><span class="sxs-lookup"><span data-stu-id="e993c-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="e993c-158">Como alternativa, você pode definir variáveis de ambiente usando Olá painel de controle do Windows.</span><span class="sxs-lookup"><span data-stu-id="e993c-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="e993c-159">Isso é uma opção melhor se você quiser tooavoid credenciais de armazenagem no código-fonte / arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="e993c-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="e993c-160">Observe que você precisará toorestart Visual Studio para o aplicativo hello novo ambiente valores toobe toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e993c-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="e993c-161">Olá código que implementa o repositório de armazenamento de tabela do Azure hello está em **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="e993c-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="e993c-162">Consulte Olá [documentação] para obter mais informações sobre como toouse serviço de tabela do Python.</span><span class="sxs-lookup"><span data-stu-id="e993c-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="e993c-163">Executar o aplicativo hello com `F5`.</span><span class="sxs-lookup"><span data-stu-id="e993c-163">Run hello application with `F5`.</span></span> <span data-ttu-id="e993c-164">Pesquisas que são criadas com **criar pesquisas de exemplo** e dados de saudação enviados ao votar serão serializados no armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="e993c-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e993c-165">Olá ambiente Virtual do Python 2.7 pode causar uma interrupção de exceção no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e993c-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="e993c-166">Pressione `F5` toocontinue carregar Olá web projeto.</span><span class="sxs-lookup"><span data-stu-id="e993c-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="e993c-167">Procurar toohello **sobre** tooverify de página que Olá aplicativo está usando Olá **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="e993c-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="e993c-169">Explorar Olá armazenamento de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="e993c-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="e993c-170">É fácil tooview e editar tabelas de armazenamento usando o Gerenciador de nuvem no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e993c-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="e993c-171">Nesta seção, nós usaremos Server Explorer tooview Olá conteúdo Olá sondagens aplicativo tabelas.</span><span class="sxs-lookup"><span data-stu-id="e993c-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="e993c-172">Isso requer toobe de ferramentas do Microsoft Azure instalado, que estão disponíveis como parte da saudação [SDK do Azure para .NET].</span><span class="sxs-lookup"><span data-stu-id="e993c-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="e993c-173">Abra o **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e993c-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="e993c-174">Expanda **Contas de Armazenamento**, sua conta de armazenamento e, em seguida, **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="e993c-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Gerenciador de Nuvem](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="e993c-176">Clique duas vezes em Olá **sondagens** ou **opções** tooview conteúdo de saudação da tabela de saudação em uma janela de documento, bem como adicionar/remover/editar entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="e993c-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="e993c-178">Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e993c-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="e993c-179">Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e993c-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="e993c-180">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e993c-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e993c-182">Clique em **Aplicativos Web do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e993c-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="e993c-183">Clique em **novo** toocreate um novo aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e993c-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="e993c-184">Preencha Olá campos a seguir e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="e993c-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="e993c-185">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="e993c-185">**Web App name**</span></span>
   * <span data-ttu-id="e993c-186">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="e993c-186">**App Service plan**</span></span>
   * <span data-ttu-id="e993c-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="e993c-187">**Resource group**</span></span>
   * <span data-ttu-id="e993c-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="e993c-188">**Region**</span></span>
   * <span data-ttu-id="e993c-189">Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="e993c-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="e993c-190">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e993c-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e993c-191">Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados.</span><span class="sxs-lookup"><span data-stu-id="e993c-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="e993c-192">Se você procurar toohello sobre a página, você verá que ele usa Olá **na memória** repositório, Olá não **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="e993c-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e993c-193">Isso ocorre porque as variáveis de ambiente Olá não são definidas na instância de aplicativos Web de Olá no serviço de aplicativo do Azure, portanto, ele usa valores padrão de saudação especificados em **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="e993c-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="e993c-194">Configurar a instância de aplicativos Web Olá</span><span class="sxs-lookup"><span data-stu-id="e993c-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="e993c-195">Nesta seção, configuraremos variáveis de ambiente para a instância de aplicativos Web hello.</span><span class="sxs-lookup"><span data-stu-id="e993c-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="e993c-196">Em [Portal do Azure](https://portal.azure.com), abra a folha de seu aplicativo da web hello clicando **procurar** > **serviços de aplicativos** > nome do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e993c-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="e993c-197">Na folha do seu aplicativo Web, clique em **Todas as configurações** depois clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e993c-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="e993c-198">Role para baixo toohello **configurações do aplicativo** seção e definir valores de saudação para **repositório\_nome**, **armazenamento\_nome** e  **ARMAZENAMENTO\_chave** conforme descrito em Olá **projeto de saudação configurar** seção acima.</span><span class="sxs-lookup"><span data-stu-id="e993c-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Configurações do aplicativo](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="e993c-200">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="e993c-200">Click on **Save**.</span></span> <span data-ttu-id="e993c-201">Depois que você recebeu notificações de saudação que alterações Olá foram aplicadas, clique em **procurar** na folha principal do aplicativo Olá Web.</span><span class="sxs-lookup"><span data-stu-id="e993c-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="e993c-202">Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="e993c-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e993c-203">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e993c-203">Congratulations!</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="e993c-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e993c-205">Next steps</span></span>
<span data-ttu-id="e993c-206">Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, Bulbo e armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="e993c-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="e993c-207">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e993c-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e993c-208">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="e993c-208">[Web Projects]</span></span>
  * <span data-ttu-id="e993c-209">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="e993c-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e993c-210">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e993c-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e993c-211">[Documentação do Flask]</span><span class="sxs-lookup"><span data-stu-id="e993c-211">[Flask Documentation]</span></span>
* <span data-ttu-id="e993c-212">[Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="e993c-212">[Azure Storage]</span></span>
* <span data-ttu-id="e993c-213">[SDK do Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="e993c-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="e993c-214">[Como tooUse Olá serviço de armazenamento de tabela do Python]</span><span class="sxs-lookup"><span data-stu-id="e993c-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e993c-215">O que mudou</span><span class="sxs-lookup"><span data-stu-id="e993c-215">What's changed</span></span>
* <span data-ttu-id="e993c-216">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e993c-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como tooUse Olá serviço de armazenamento de tabela do Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[SDK do Azure para .NET]: http://azure.microsoft.com/downloads/
[ferramentas Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
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
