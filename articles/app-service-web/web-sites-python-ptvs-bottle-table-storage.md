---
title: aaaBottle e armazenamento de tabela do Azure no Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo de garrafa que armazena dados no armazenamento de tabela do Azure e implante Olá web aplicativo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="f6d05-103">Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6d05-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="f6d05-104">Neste tutorial, vamos usar [ferramentas Python para Visual Studio] toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6d05-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="f6d05-105">Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="f6d05-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="f6d05-106">Olá sondagens web aplicativo define uma abstração para seu repositório, assim você pode alternar facilmente entre tipos diferentes de repositórios (na memória, armazenamento de tabela do Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="f6d05-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="f6d05-107">Aprenderá como toocreate um armazenamento do Azure a conta, como tooconfigure Olá web aplicativo toouse armazenamento de tabela do Azure e toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f6d05-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="f6d05-108">Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com os serviços do MongoDB, armazenamento de tabela do Azure, MySQL e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f6d05-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="f6d05-109">Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="f6d05-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6d05-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6d05-110">Prerequisites</span></span>
* <span data-ttu-id="f6d05-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f6d05-111">Visual Studio 2015</span></span>
* <span data-ttu-id="f6d05-112">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f6d05-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="f6d05-113">[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f6d05-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="f6d05-114">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="f6d05-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="f6d05-115">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="f6d05-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f6d05-116">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6d05-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f6d05-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="f6d05-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="f6d05-118">Criar hello projeto</span><span class="sxs-lookup"><span data-stu-id="f6d05-118">Create hello Project</span></span>
<span data-ttu-id="f6d05-119">Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="f6d05-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="f6d05-120">Criaremos um ambiente virtual e instalaremos pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="f6d05-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="f6d05-121">Em seguida, vamos executar aplicativo hello localmente usando o repositório do saudação padrão em memória.</span><span class="sxs-lookup"><span data-stu-id="f6d05-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="f6d05-122">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="f6d05-123">Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="f6d05-124">Selecione **sondagens garrafa Web projeto** e clique em projeto de saudação toocreate Okey.</span><span class="sxs-lookup"><span data-stu-id="f6d05-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="f6d05-126">Você será pacotes externos tooinstall solicitada.</span><span class="sxs-lookup"><span data-stu-id="f6d05-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="f6d05-127">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-127">Select **Install into a virtual environment**.</span></span>
   
     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="f6d05-129">Selecione **Python 2.7** ou **Python 3.4** como interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="f6d05-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="f6d05-131">Confirme se o aplicativo hello funciona pressionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="f6d05-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="f6d05-132">Por padrão, o aplicativo hello usa um repositório de memória que não exige qualquer configuração.</span><span class="sxs-lookup"><span data-stu-id="f6d05-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="f6d05-133">Todos os dados são perdidos quando o servidor de web hello é interrompido.</span><span class="sxs-lookup"><span data-stu-id="f6d05-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="f6d05-134">Clique em **Criar Votações de Exemplo**e, em seguida, clique em uma votação e vote.</span><span class="sxs-lookup"><span data-stu-id="f6d05-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="f6d05-136">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f6d05-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="f6d05-137">toouse operações de armazenamento, você precisa de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6d05-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="f6d05-138">Você pode criar uma conta de armazenamento seguindo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="f6d05-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="f6d05-139">Faça logon no hello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6d05-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f6d05-140">Clique em Olá **novo** ícone no início de saudação à esquerda da saudação Portal, clique em **dados + armazenamento** > **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="f6d05-141">Clique em Olá **criar** botão, em seguida, dê um nome exclusivo de conta de armazenamento hello e criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ele.</span><span class="sxs-lookup"><span data-stu-id="f6d05-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Criação Rápida](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="f6d05-143">Quando tiver sido criada a conta de armazenamento hello, Olá **notificações** botão pisca uma verde **êxito** e folha da conta de armazenamento hello está aberta tooshow que ele pertence toohello novo recurso de grupo criado.</span><span class="sxs-lookup"><span data-stu-id="f6d05-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="f6d05-144">Clique em Olá **chaves de acesso** parte na folha da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="f6d05-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="f6d05-145">Anote o nome de conta hello e key1.</span><span class="sxs-lookup"><span data-stu-id="f6d05-145">Take note of hello account name and key1.</span></span>
   
      ![simétricas](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="f6d05-147">Precisaremos este tooconfigure informações seu projeto na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="f6d05-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="f6d05-148">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="f6d05-148">Configure hello Project</span></span>
<span data-ttu-id="f6d05-149">Nesta seção, configuraremos nosso conta de armazenamento do aplicativo toouse Olá que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="f6d05-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="f6d05-150">Em seguida, vamos executar aplicativo hello localmente.</span><span class="sxs-lookup"><span data-stu-id="f6d05-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="f6d05-151">No Visual Studio, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="f6d05-152">Clique em Olá **depurar** guia.</span><span class="sxs-lookup"><span data-stu-id="f6d05-152">Click on hello **Debug** tab.</span></span>
   
     ![Configurações de depuração do projeto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="f6d05-154">Definir valores de saudação de variáveis de ambiente exigidos pelo aplicativo hello em **depurar servidor comando**, **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="f6d05-155">Isso definirá as variáveis de ambiente hello quando você **iniciar depuração**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="f6d05-156">Se você quiser Olá variáveis toobe definida quando você **Start Without Debugging**, Olá conjunto mesmo valores em **executar comando de servidor** também.</span><span class="sxs-lookup"><span data-stu-id="f6d05-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="f6d05-157">Como alternativa, você pode definir variáveis de ambiente usando Olá painel de controle do Windows.</span><span class="sxs-lookup"><span data-stu-id="f6d05-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="f6d05-158">Isso é uma opção melhor se você quiser tooavoid credenciais de armazenagem no código-fonte / arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f6d05-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="f6d05-159">Observe que você precisará toorestart Visual Studio para o aplicativo hello novo ambiente valores toobe toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f6d05-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="f6d05-160">Olá código que implementa o repositório de armazenamento de tabela do Azure hello está em **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="f6d05-161">Consulte Olá [documentação] para obter mais informações sobre como toouse serviço de tabela do Python.</span><span class="sxs-lookup"><span data-stu-id="f6d05-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="f6d05-162">Executar o aplicativo hello com `F5`.</span><span class="sxs-lookup"><span data-stu-id="f6d05-162">Run hello application with `F5`.</span></span> <span data-ttu-id="f6d05-163">Pesquisas que são criadas com **criar pesquisas de exemplo** e dados de saudação enviados ao votar serão serializados no armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6d05-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f6d05-164">Olá ambiente Virtual do Python 2.7 pode causar uma interrupção de exceção no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6d05-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="f6d05-165">Pressione `F5` toocontinue carregar Olá web projeto.</span><span class="sxs-lookup"><span data-stu-id="f6d05-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="f6d05-166">Procurar toohello **sobre** tooverify de página que Olá aplicativo está usando Olá **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="f6d05-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="f6d05-168">Explorar Olá armazenamento de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="f6d05-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="f6d05-169">É fácil tooview e editar tabelas de armazenamento usando o Gerenciador de nuvem no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6d05-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="f6d05-170">Nesta seção, nós usaremos Server Explorer tooview Olá conteúdo Olá sondagens aplicativo tabelas.</span><span class="sxs-lookup"><span data-stu-id="f6d05-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="f6d05-171">Isso requer toobe de ferramentas do Microsoft Azure instalado, que estão disponíveis como parte da saudação [SDK do Azure para .NET].</span><span class="sxs-lookup"><span data-stu-id="f6d05-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="f6d05-172">Abra o **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="f6d05-173">Expanda **Contas de Armazenamento**, sua conta de armazenamento e, em seguida, **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Gerenciador de Nuvem](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="f6d05-175">Clique duas vezes em Olá **sondagens** ou **opções** tooview conteúdo de saudação da tabela de saudação em uma janela de documento, bem como adicionar/remover/editar entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="f6d05-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="f6d05-177">Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6d05-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="f6d05-178">Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6d05-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="f6d05-179">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="f6d05-181">Clique em **Aplicativos Web do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="f6d05-182">Clique em **novo** toocreate um novo aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f6d05-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="f6d05-183">Preencha Olá campos a seguir e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="f6d05-184">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="f6d05-184">**Web App name**</span></span>
   * <span data-ttu-id="f6d05-185">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="f6d05-185">**App Service plan**</span></span>
   * <span data-ttu-id="f6d05-186">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="f6d05-186">**Resource group**</span></span>
   * <span data-ttu-id="f6d05-187">**Região**</span><span class="sxs-lookup"><span data-stu-id="f6d05-187">**Region**</span></span>
   * <span data-ttu-id="f6d05-188">Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="f6d05-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="f6d05-189">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="f6d05-190">Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados.</span><span class="sxs-lookup"><span data-stu-id="f6d05-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="f6d05-191">Se você procurar toohello sobre a página, você verá que ele usa Olá **na memória** repositório, Olá não **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="f6d05-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="f6d05-192">Isso ocorre porque as variáveis de ambiente Olá não são definidas na instância de aplicativos Web de Olá no serviço de aplicativo do Azure, portanto, ele usa valores padrão de saudação especificados em **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="f6d05-193">Configurar a instância de aplicativos Web Olá</span><span class="sxs-lookup"><span data-stu-id="f6d05-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="f6d05-194">Nesta seção, configuraremos variáveis de ambiente para a instância de aplicativos Web hello.</span><span class="sxs-lookup"><span data-stu-id="f6d05-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="f6d05-195">Em [Portal do Azure], abra a folha de seu aplicativo da web hello clicando **procurar** > **serviços de aplicativos** > nome do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f6d05-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="f6d05-196">Na folha do seu aplicativo Web, clique em **Todas as configurações** depois clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="f6d05-197">Role para baixo toohello **configurações do aplicativo** seção e definir valores de saudação para **repositório\_nome**, **armazenamento\_nome** e  **ARMAZENAMENTO\_chave** conforme descrito em Olá **projeto de saudação configurar** seção acima.</span><span class="sxs-lookup"><span data-stu-id="f6d05-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Configurações do aplicativo](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="f6d05-199">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="f6d05-199">Click on **Save**.</span></span> <span data-ttu-id="f6d05-200">Depois que você recebeu notificações de saudação que alterações Olá foram aplicadas, clique em **procurar** na folha principal do aplicativo Olá Web.</span><span class="sxs-lookup"><span data-stu-id="f6d05-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="f6d05-201">Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **armazenamento de tabela do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="f6d05-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="f6d05-202">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f6d05-202">Congratulations!</span></span>
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="f6d05-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6d05-204">Next steps</span></span>
<span data-ttu-id="f6d05-205">Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, garrafa e armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6d05-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="f6d05-206">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f6d05-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="f6d05-207">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="f6d05-207">[Web Projects]</span></span>
  * <span data-ttu-id="f6d05-208">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="f6d05-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="f6d05-209">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="f6d05-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="f6d05-210">[Documentação do Bottle]</span><span class="sxs-lookup"><span data-stu-id="f6d05-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="f6d05-211">[Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="f6d05-211">[Azure Storage]</span></span>
* <span data-ttu-id="f6d05-212">[SDK do Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="f6d05-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="f6d05-213">[Como tooUse Olá serviço de armazenamento de tabela do Python]</span><span class="sxs-lookup"><span data-stu-id="f6d05-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f6d05-214">O que mudou</span><span class="sxs-lookup"><span data-stu-id="f6d05-214">What's changed</span></span>
* <span data-ttu-id="f6d05-215">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f6d05-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como tooUse Olá serviço de armazenamento de tabela do Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[SDK do Azure para .NET]: http://azure.microsoft.com/downloads/
[ferramentas Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do Bottle]: http://bottlepy.org/docs/dev/index.html
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Armazenamento do Azure]: http://azure.microsoft.com/documentation/services/storage/
[SDK do Azure para Python]: https://github.com/Azure/azure-sdk-for-python
