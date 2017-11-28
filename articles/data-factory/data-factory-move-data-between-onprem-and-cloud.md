---
title: dados aaaMove - Data Management Gateway | Microsoft Docs
description: Configurar um gateway toomove de dados entre locais e hello nuvem. Use o Gateway de gerenciamento de dados no Azure Data Factory toomove seus dados.
keywords: "gateway de dados, integração de dados, mover dados, credenciais de gateway"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="98318-105">Mover dados entre fontes locais e na nuvem de saudação com Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="98318-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="98318-106">Este artigo fornece uma visão geral da integração de dados entre os armazenamentos de dados locais e os armazenamentos de dados na nuvem usando o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98318-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="98318-107">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo e outros artigos de conceitos principais data factory: [conjuntos de dados](data-factory-create-datasets.md) e [pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="98318-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="98318-108">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="98318-108">Data Management Gateway</span></span>
<span data-ttu-id="98318-109">Você deve instalar o Gateway de gerenciamento de dados em seu tooenable de máquina local a movimentação de dados para/de um repositório de dados local.</span><span class="sxs-lookup"><span data-stu-id="98318-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="98318-110">gateway de saudação pode ser instalado no mesmo computador como armazenamento de dados hello, ou em um computador diferente como gateway Olá pode se conectar o armazenamento de dados toohello de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98318-111">Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="98318-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="98318-112">Olá seguir instruções passo a passo mostra como uma fábrica de dados com um pipeline que move dados de um local de toocreate **do SQL Server** tooan armazenamento de BLOBs do Azure do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="98318-113">Como parte da saudação passo a passo, você instale e configure Olá Data Management Gateway em seu computador.</span><span class="sxs-lookup"><span data-stu-id="98318-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="98318-114">Passo a passo: copiar toocloud de dados local</span><span class="sxs-lookup"><span data-stu-id="98318-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="98318-115">Neste passo a passo, você Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="98318-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="98318-116">Criar uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-116">Create a data factory.</span></span>
2. <span data-ttu-id="98318-117">Criar um Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="98318-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="98318-118">Criar serviços vinculados para armazenamentos de dados de origem e de coletor.</span><span class="sxs-lookup"><span data-stu-id="98318-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="98318-119">Criar conjuntos de dados toorepresent entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="98318-120">Crie um pipeline com um copiar atividade toomove Olá dados.</span><span class="sxs-lookup"><span data-stu-id="98318-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="98318-121">Pré-requisitos para o tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="98318-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="98318-122">Antes de começar este passo a passo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="98318-123">**Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="98318-123">**Azure subscription**.</span></span>  <span data-ttu-id="98318-124">Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="98318-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="98318-125">Consulte Olá [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="98318-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="98318-126">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="98318-126">**Azure Storage Account**.</span></span> <span data-ttu-id="98318-127">Use o armazenamento de blob hello como um **destino/coletor** repositório de dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="98318-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="98318-128">Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.</span><span class="sxs-lookup"><span data-stu-id="98318-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="98318-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="98318-129">**SQL Server**.</span></span> <span data-ttu-id="98318-130">Neste tutorial, você utiliza um Banco de Dados do SQL Server local como um armazenamento de dados de **origem**.</span><span class="sxs-lookup"><span data-stu-id="98318-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="98318-131">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="98318-131">Create data factory</span></span>
<span data-ttu-id="98318-132">Nesta etapa, você usa Olá toocreate portal do Azure que uma instância do Azure Data Factory chamado **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="98318-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="98318-133">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98318-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98318-134">Clique em **+ NOVO**, clique em **Inteligência + análise** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="98318-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Novo -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="98318-136">Em Olá **nova fábrica de dados** insira **ADFTutorialOnPremDF** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="98318-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Adicionar tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="98318-138">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="98318-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="98318-139">Se você receber o erro Olá: **"ADFTutorialOnPremDF" nome da fábrica de dados não está disponível**, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFTutorialOnPremDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="98318-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="98318-140">Use esse nome em vez de ADFTutorialOnPremDF ao executar as etapas restantes neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="98318-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="98318-141">nome de Olá Olá da fábrica de dados pode ser registrado como um **DNS** nome no futuro hello e, portanto, se tornarão visíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="98318-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="98318-142">Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="98318-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="98318-143">Selecione um **grupo de recursos** existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98318-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="98318-144">Tutorial de hello, crie um grupo de recursos chamado: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="98318-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="98318-145">Clique em **criar** em Olá **nova fábrica de dados** página.</span><span class="sxs-lookup"><span data-stu-id="98318-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="98318-146">toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.</span><span class="sxs-lookup"><span data-stu-id="98318-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="98318-147">Após a conclusão da criação, você ver Olá **Data Factory** página conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Página inicial do Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="98318-149">Criar gateway</span><span class="sxs-lookup"><span data-stu-id="98318-149">Create gateway</span></span>
1. <span data-ttu-id="98318-150">Em Olá **Data Factory** , clique em **autor e implantar** bloco toolaunch Olá **Editor** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Bloco Criar e implantar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="98318-152">No hello Editor da fábrica de dados, clique em **... Mais** Olá barra de ferramentas e, em seguida, clique em **novo gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="98318-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="98318-153">Como alternativa, clique **Gateways de dados** no Olá a exibição de árvore e clique em **novo gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="98318-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Novo gateway de dados na barra de ferramentas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="98318-155">Em Olá **criar** insira **adftutorialgateway** para Olá **nome**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="98318-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Página Criar Gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="98318-157">Neste passo a passo, você pode criar gateway lógico Olá com apenas um nó (máquina do Windows local).</span><span class="sxs-lookup"><span data-stu-id="98318-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="98318-158">Você pode expandir um gateway de gerenciamento de dados por meio da associação várias máquinas locais com o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="98318-159">Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó.</span><span class="sxs-lookup"><span data-stu-id="98318-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="98318-160">Esse recurso também está disponível para um gateway lógico com um único nó.</span><span class="sxs-lookup"><span data-stu-id="98318-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="98318-161">Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="98318-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="98318-162">Em Olá **configurar** , clique em **instalar diretamente no computador**.</span><span class="sxs-lookup"><span data-stu-id="98318-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="98318-163">Essa ação baixa o pacote de instalação de saudação para gateway hello, instala, configura e registra o gateway Olá no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="98318-164">Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="98318-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="98318-165">Se você estiver usando o Chrome, vá toohello [repositório na web do Chrome](https://chrome.google.com/webstore/), pesquisar "ClickOnce" palavra-chave with, escolha uma das extensões de ClickOnce hello e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="98318-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="98318-166">Olá mesmo para o Firefox (instalação do suplemento).</span><span class="sxs-lookup"><span data-stu-id="98318-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="98318-167">Clique em **Abrir Menu** botão na barra de ferramentas da saudação (**três linhas horizontais** no canto superior direito de saudação), clique em **complementos**, pesquisar "ClickOnce" palavra-chave with, escolha uma saudação Extensões de ClickOnce e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="98318-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Página Gateway – Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="98318-169">Dessa maneira é mais fácil toodownload de forma (um clique) hello, instalar, configurar e registrar o gateway de saudação em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="98318-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="98318-170">Você pode ver Olá **Gerenciador de configuração do Gateway de gerenciamento de dados Microsoft** aplicativo está instalado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="98318-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="98318-171">Você também pode encontrar hello executável **ConfigManager.exe** na pasta Olá: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="98318-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="98318-172">Você também pode baixar e instalar o gateway manualmente usando os links de saudação nesta página e registrá-lo usando a chave Olá mostrado no hello **nova chave** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="98318-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="98318-173">Consulte [Data Management Gateway](data-factory-data-management-gateway.md) para todos Olá detalhes sobre o gateway de saudação do artigo.</span><span class="sxs-lookup"><span data-stu-id="98318-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98318-174">Você deve ser um administrador no hello tooinstall de computador local e configurar Olá Data Management Gateway com êxito.</span><span class="sxs-lookup"><span data-stu-id="98318-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="98318-175">Você pode adicionar usuários adicionais toohello **usuários do Gateway de gerenciamento de dados** grupo local do Windows.</span><span class="sxs-lookup"><span data-stu-id="98318-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="98318-176">membros desse grupo Olá podem usar o gateway de saudação do hello Gerenciador de configuração de Gateway de gerenciamento de dados ferramenta tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="98318-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="98318-177">Aguarde alguns minutos ou aguarde até que você veja Olá mensagem de notificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Instalação do gateway bem-sucedida](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="98318-179">Inicie o aplicativo **Gerenciador de Configuração de Gateway de gerenciamento de dados** no computador.</span><span class="sxs-lookup"><span data-stu-id="98318-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="98318-180">Em Olá **pesquisa** , digite **Data Management Gateway** tooaccess este utilitário.</span><span class="sxs-lookup"><span data-stu-id="98318-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="98318-181">Você também pode encontrar hello executável **ConfigManager.exe** na pasta Olá: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="98318-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gerenciador de configuração de gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="98318-183">Confirme que você vê a mensagem `adftutorialgateway is connected toohello cloud service`.</span><span class="sxs-lookup"><span data-stu-id="98318-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="98318-184">Olá Olá inferior exibe da barra de status **conectado serviço de nuvem toohello** juntamente com um **marca de seleção verde**.</span><span class="sxs-lookup"><span data-stu-id="98318-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="98318-185">Em Olá **início** guia, você também pode fazer Olá seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="98318-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="98318-186">**Registrar** um gateway com uma chave de saudação portal do Azure usando o botão de registrar hello.</span><span class="sxs-lookup"><span data-stu-id="98318-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="98318-187">**Parar** Olá dados serviço Gateway de gerenciamento Host em execução no seu computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="98318-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="98318-188">**Agendar atualizações** toobe instalado em uma hora específica do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="98318-189">Exibir quando o gateway Olá foi **atualizado pela última vez**.</span><span class="sxs-lookup"><span data-stu-id="98318-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="98318-190">Especifique a hora em que um gateway de toohello de atualização pode ser instalado.</span><span class="sxs-lookup"><span data-stu-id="98318-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="98318-191">Alternar toohello **configurações** certificado de saudação do guia especificado no hello **certificado** seção é usada tooencrypt/descriptografar credenciais para armazenamento de dados do hello local que você especificar no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="98318-192">(opcional) Clique em **alteração** toouse seu próprio certificado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="98318-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="98318-193">Por padrão, o gateway Olá usa Olá certificado é gerado automaticamente pelo Olá serviço da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Configuração do certificado do gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="98318-195">Você também pode fazer Olá seguintes ações no hello **configurações** guia:</span><span class="sxs-lookup"><span data-stu-id="98318-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="98318-196">Exibir ou exportar certificado hello está sendo usado pelo gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="98318-197">Alterar o ponto de extremidade HTTPS de saudação usado pelo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="98318-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="98318-198">Defina um toobe de proxy HTTP usado pelo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="98318-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="98318-199">(opcional) Alternar toohello **diagnóstico** guia, verifique Olá **Habilitar log detalhado** opção se você quiser tooenable detalhado de log que você pode usar tootroubleshoot quaisquer problemas com o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="98318-200">Olá informações de log podem ser encontradas em **Visualizador de eventos** em **Applications and Services Logs** -> **Data Management Gateway** nó.</span><span class="sxs-lookup"><span data-stu-id="98318-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Guia Diagnósticos](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="98318-202">Você também pode executar Olá seguintes ações no hello **diagnóstico** guia:</span><span class="sxs-lookup"><span data-stu-id="98318-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="98318-203">Use **Conexão de teste** fonte de dados seção tooan local usando Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="98318-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="98318-204">Clique em **Exibir Logs** toosee Olá Gateway de gerenciamento de dados de log em uma janela do Visualizador de eventos.</span><span class="sxs-lookup"><span data-stu-id="98318-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="98318-205">Clique em **enviar Logs de** tooupload um arquivo zip com logs dos últimos sete dias tooMicrosoft toofacilitate de solução de problemas de seus problemas.</span><span class="sxs-lookup"><span data-stu-id="98318-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="98318-206">Em Olá **diagnóstico** guia Olá **Conexão de teste** seção, selecione **SqlServer** para o tipo de saudação de dados Olá armazenar, insira o nome de saudação do servidor de banco de dados Olá, nome do Olá banco de dados, especifique o tipo de autenticação, digite o nome de usuário e senha e clique em **teste** tootest se gateway Olá pode se conectar a banco de dados toohello.</span><span class="sxs-lookup"><span data-stu-id="98318-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="98318-207">Navegador do toohello de comutador e em Olá **portal do Azure**, clique em **Okey** em Olá **configurar** página e, em seguida, em Olá **novo gateway de dados** página.</span><span class="sxs-lookup"><span data-stu-id="98318-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="98318-208">Você deve ver **adftutorialgateway** em **Gateways de dados** na exibição de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="98318-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="98318-209">Se você clicar nele, você verá Olá associados JSON.</span><span class="sxs-lookup"><span data-stu-id="98318-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="98318-210">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="98318-210">Create linked services</span></span>
<span data-ttu-id="98318-211">Nesta etapa, você cria dois serviços vinculados: **AzureStorageLinkedService** e **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="98318-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="98318-212">Olá **SqlServerLinkedService** vincula um banco de dados do SQL Server local e hello **AzureStorageLinkedService** serviço vinculado vincula uma fábrica de dados de toohello de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="98318-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="98318-213">Você pode criar um pipeline posteriormente neste passo a passo que copia dados de armazenamento de BLOBs do Azure de toohello Olá local do SQL Server banco de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="98318-214">Adicionar um banco de dados do serviço vinculado tooan local do SQL Server</span><span class="sxs-lookup"><span data-stu-id="98318-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="98318-215">Em Olá **Editor da fábrica de dados**, clique em **novo repositório de dados** na barra de ferramentas hello e selecione **do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="98318-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Serviço vinculado do SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="98318-217">Em Olá **editor de JSON** em Olá direita, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="98318-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="98318-218">Para Olá **gatewayName**, especifique **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="98318-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="98318-219">Em Olá **connectionString**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="98318-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="98318-220">Para **servername**, digite nome de saudação do servidor de saudação que hospeda o banco de dados do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="98318-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="98318-221">Para **databasename**, insira o nome de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="98318-222">Clique em **Encrypt** botão na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="98318-223">Consulte o aplicativo do Gerenciador de credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="98318-223">You see hello Credentials Manager application.</span></span>

         ![Aplicativo do Gerenciador de credenciais](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="98318-225">Em Olá **definindo credenciais** caixa de diálogo, especifique o tipo de autenticação, nome de usuário e senha e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="98318-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="98318-226">Se a conexão de saudação for bem-sucedida, credenciais Olá criptografado são armazenadas em Olá JSON e Olá caixa de diálogo é fechada.</span><span class="sxs-lookup"><span data-stu-id="98318-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="98318-227">Fechar Guia do navegador vazia Olá que iniciou a caixa de diálogo Olá se não for fechada automaticamente e voltar à guia toohello com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98318-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="98318-228">No computador do gateway hello, essas credenciais são **criptografado** usando um certificado que Olá fábrica de dados de serviço possui.</span><span class="sxs-lookup"><span data-stu-id="98318-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="98318-229">Se você quiser toouse Olá certificado associado com hello Gateway de gerenciamento de dados em vez disso, consulte [definir credenciais com segurança](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="98318-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="98318-230">Clique em **implantar** no comando Olá barra toodeploy Olá serviço vinculado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98318-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="98318-231">Você deve ver o serviço Olá vinculado na exibição de árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-231">You should see hello linked service in hello tree view.</span></span>

      ![Serviço vinculado do SQL Server no modo de exibição de árvore de saudação](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="98318-233">Adicionar um serviço vinculado para uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="98318-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="98318-234">Em Olá **Editor da fábrica de dados**, clique em **novo repositório de dados** Olá barra de comandos e clique em **armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="98318-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="98318-235">Inserir nome de saudação da sua conta de armazenamento do Azure para Olá **nome da conta**.</span><span class="sxs-lookup"><span data-stu-id="98318-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="98318-236">Insira a chave de saudação para sua conta de armazenamento do Azure para Olá **chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="98318-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="98318-237">Clique em **implantar** toodeploy Olá **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="98318-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="98318-238">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="98318-238">Create datasets</span></span>
<span data-ttu-id="98318-239">Nesta etapa, você pode criar entrada e saída de conjuntos de dados que representam dados de entrada e saídos para a operação de cópia de saudação (banco de dados do SQL Server no local = > armazenamento de BLOBs do Azure).</span><span class="sxs-lookup"><span data-stu-id="98318-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="98318-240">Antes de criar conjuntos de dados, Olá etapas (etapas detalhadas segue lista Olá):</span><span class="sxs-lookup"><span data-stu-id="98318-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="98318-241">Criar uma tabela chamada **emp** em Olá banco de dados do servidor SQL é adicionado como uma fábrica de dados do serviço vinculado toohello e inserir alguns exemplos de entradas na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="98318-242">Criar um contêiner de blob denominado **adftutorial** em hello Azure adicionada como uma fábrica de dados do serviço vinculado toohello de conta de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="98318-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="98318-243">Preparar SQL Server no local para o tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="98318-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="98318-244">No banco de dados de saudação especificada para saudação do SQL Server local de serviço vinculado (**SqlServerLinkedService**), use Olá Olá de toocreate de script SQL a seguir **emp** tabela no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="98318-245">Insira algum exemplo na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="98318-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="98318-246">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="98318-246">Create input dataset</span></span>

1. <span data-ttu-id="98318-247">Em Olá **Editor da fábrica de dados**, clique em **... Mais**, clique em **novo conjunto de dados** Olá barra de comandos e clique em **tabela do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="98318-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="98318-248">Substitua Olá JSON no painel direito Olá Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-248">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="98318-249">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-249">Note hello following points:</span></span>

   * <span data-ttu-id="98318-250">**tipo** está definido muito**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="98318-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="98318-251">**tableName** está definido muito**emp**.</span><span class="sxs-lookup"><span data-stu-id="98318-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="98318-252">**linkedServiceName** está definido muito**SqlServerLinkedService** (você tinha criou esse serviço vinculado anteriormente neste passo a passo.).</span><span class="sxs-lookup"><span data-stu-id="98318-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="98318-253">Para um conjunto de dados entrado que não é gerado por outro pipeline na fábrica de dados do Azure, você deve definir **externo** muito**true**.</span><span class="sxs-lookup"><span data-stu-id="98318-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="98318-254">Ele indica que os dados de entrada hello estão toohello externo produzido serviço do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98318-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="98318-255">Você pode opcionalmente especificar quaisquer políticas de dados externa usando Olá **externalData** elemento Olá **política** seção.</span><span class="sxs-lookup"><span data-stu-id="98318-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="98318-256">Confira [Mover dados para/de SQL Server](data-factory-sqlserver-connector.md) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="98318-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="98318-257">Clique em **implantar** no comando Olá barra toodeploy Olá dataset.</span><span class="sxs-lookup"><span data-stu-id="98318-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="98318-258">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="98318-258">Create output dataset</span></span>

1. <span data-ttu-id="98318-259">Em Olá **Editor da fábrica de dados**, clique em **novo conjunto de dados** Olá barra de comandos e clique em **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="98318-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="98318-260">Substitua Olá JSON no painel direito Olá Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-260">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="98318-261">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-261">Note hello following points:</span></span>

   * <span data-ttu-id="98318-262">**tipo** está definido muito**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="98318-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="98318-263">**linkedServiceName** está definido muito**AzureStorageLinkedService** (você tivesse criado esse serviço vinculado na etapa 2).</span><span class="sxs-lookup"><span data-stu-id="98318-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="98318-264">**folderPath** está definido muito**adftutorial/outfromonpremdf** onde outfromonpremdf é pasta Olá no contêiner de adftutorial hello.</span><span class="sxs-lookup"><span data-stu-id="98318-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="98318-265">Criar hello **adftutorial** contêiner se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="98318-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="98318-266">Olá **disponibilidade** está definido muito**por hora** (**frequência** definido muito**hora** e **intervalo** definido muito **1**).</span><span class="sxs-lookup"><span data-stu-id="98318-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="98318-267">Olá serviço da fábrica de dados gera uma fatia de dados de saída a cada hora Olá **emp** tabela hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="98318-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="98318-268">Se você não especificar um **fileName** para um **tabela de saída**, arquivos Olá Olá gerado **folderPath** são nomeados em Olá formato a seguir: dados.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="98318-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="98318-269">tooset **folderPath** e **fileName** dinamicamente com base nas Olá **SliceStart** de tempo, use a propriedade de partitionedBy hello.</span><span class="sxs-lookup"><span data-stu-id="98318-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="98318-270">No hello exemplo a seguir, folderPath usa o ano, mês e dia de saudação SliceStart (hora de início da fatia Olá processada) e fileName usa a hora de SliceStart de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="98318-271">Por exemplo, se uma fatia está sendo produzida para 2014-10-20T08:00:00, Olá folderName é definido toowikidatagateway/wikisampledataout/2014/10/20 e nome de arquivo hello é definido too08.csv.</span><span class="sxs-lookup"><span data-stu-id="98318-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="98318-272">Confira [Mover dados para/de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="98318-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="98318-273">Clique em **implantar** no comando Olá barra toodeploy Olá dataset.</span><span class="sxs-lookup"><span data-stu-id="98318-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="98318-274">Confirme se os dois conjuntos de dados Olá na exibição de árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="98318-275">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="98318-275">Create pipeline</span></span>
<span data-ttu-id="98318-276">Nesta etapa, você criará um **pipeline** com uma **Atividade de Cópia** que usa **EmpOnPremSQLTable** como entrada e **OutputBlobTable** como saída.</span><span class="sxs-lookup"><span data-stu-id="98318-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="98318-277">No Editor de Data Factory, clique em **... Mais** e clique em **Novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="98318-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="98318-278">Substitua Olá JSON no painel direito Olá Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="98318-279">Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="98318-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="98318-280">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-280">Note hello following points:</span></span>

   * <span data-ttu-id="98318-281">Na seção de atividades hello, há apenas atividades cujo **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="98318-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="98318-282">**Entrada** para atividade de saudação é definida muito**EmpOnPremSQLTable** e **saída** para atividade de saudação é definida muito**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="98318-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="98318-283">Em Olá **typeProperties** seção, **SqlSource** é especificado como Olá **tipo de fonte** e * * BlobSink * * é especificado como Olá **dotipodecoletor**.</span><span class="sxs-lookup"><span data-stu-id="98318-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="98318-284">Consulta SQL `select * from emp` é especificado para Olá **sqlReaderQuery** propriedade **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="98318-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="98318-285">Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="98318-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="98318-286">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="98318-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="98318-287">Olá **final** tempo é opcional, mas usamos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="98318-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="98318-288">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="98318-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="98318-289">pipeline de saudação toorun indefinidamente, especifique **9/9/9999** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="98318-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="98318-290">Você está definindo tempo de duração na qual Olá fatias de dados são processadas com base em Olá Olá **disponibilidade** propriedades que foram definidas para cada conjunto de dados do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98318-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="98318-291">No exemplo hello, há 24 fatias de dados como cada fatia de dados é produzida por hora.</span><span class="sxs-lookup"><span data-stu-id="98318-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="98318-292">Clique em **implantar** no comando Olá barra toodeploy Olá dataset (tabela é um conjunto de dados retangular).</span><span class="sxs-lookup"><span data-stu-id="98318-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="98318-293">Confirmar esse pipeline Olá aparece na exibição de árvore de saudação em **Pipelines** nó.</span><span class="sxs-lookup"><span data-stu-id="98318-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="98318-294">Agora, clique em **X** duas vezes tooclose Olá página tooget back toohello **Data Factory** página Olá **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="98318-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="98318-295">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="98318-295">**Congratulations!**</span></span> <span data-ttu-id="98318-296">Você criou com êxito uma fábrica de dados do Azure, serviços vinculados, conjuntos de dados e um pipeline e pipeline de saudação agendado.</span><span class="sxs-lookup"><span data-stu-id="98318-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="98318-297">Fábrica de dados de saudação de exibição em uma exibição de diagrama</span><span class="sxs-lookup"><span data-stu-id="98318-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="98318-298">Em Olá **portal do Azure**, clique em **diagrama** lado a lado na página inicial Olá Olá **ADFTutorialOnPremDF** fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="98318-299">:</span><span class="sxs-lookup"><span data-stu-id="98318-299">:</span></span>

    ![Link do diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="98318-301">Você deve ver toohello semelhante do diagrama Olá imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="98318-301">You should see hello diagram similar toohello following image:</span></span>

    ![Exibição de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="98318-303">Você pode ampliar, zoom, zoom too100%, toofit de zoom, automaticamente pipelines de posição e conjuntos de dados e mostrar informações de linhagem (realça os itens de upstream e downstream dos itens selecionados).</span><span class="sxs-lookup"><span data-stu-id="98318-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="98318-304">Clique duas vezes em Propriedades de toosee um objeto (ou pipeline de conjunto de dados de entrada/saída) para ele.</span><span class="sxs-lookup"><span data-stu-id="98318-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="98318-305">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="98318-305">Monitor pipeline</span></span>
<span data-ttu-id="98318-306">Nesta etapa, você deve usar Olá toomonitor de portal do Azure que está acontecendo em uma fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="98318-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="98318-307">Você também pode usar pipelines e conjuntos de dados de toomonitor de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98318-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="98318-308">Para obter detalhes sobre monitoramento, consulte [Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="98318-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="98318-309">No diagrama de saudação, clique duas vezes em **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="98318-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Fatias de EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="98318-311">Observe que todos os dados de saudação fatias de backup estão em **pronto** estado porque duração de pipeline hello (hora de tooend de tempo de início) está em Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="98318-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="98318-312">Também é porque você inseriu dados saudação no banco de dados do SQL Server hello e haja todo o tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="98318-313">Confirme que nenhuma fatia aparecerão em Olá **fatias problema** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="98318-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="98318-314">tooview todas as fatias hello, clique **consulte mais** final Olá Olá lista das fatias.</span><span class="sxs-lookup"><span data-stu-id="98318-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="98318-315">Agora, em Olá **conjuntos de dados** , clique em **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="98318-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Fatias de OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="98318-317">Clique em qualquer fatia de dados da lista de saudação e você deverá ver Olá **fatia de dados** página.</span><span class="sxs-lookup"><span data-stu-id="98318-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="98318-318">Você verá a atividade for executada por fatia hello.</span><span class="sxs-lookup"><span data-stu-id="98318-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="98318-319">Você normalmente vê apenas uma atividade sendo executada.</span><span class="sxs-lookup"><span data-stu-id="98318-319">You see only one activity run usually.</span></span>  

    ![Folha Fatia de dados](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="98318-321">Se fatia Olá não está em Olá **pronto** estado, você pode ver fatias de upstream Olá que não estão prontos e estão bloqueando a fatia atual Olá executadas em Olá **fatias de Upstream que não estão prontas** lista.</span><span class="sxs-lookup"><span data-stu-id="98318-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="98318-322">Clique em Olá **execução da atividade** de lista Olá Olá inferior toosee **detalhes da execução de atividade**.</span><span class="sxs-lookup"><span data-stu-id="98318-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Página Detalhes da Execução da Atividade](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="98318-324">Você verá informações como taxa de transferência, a duração e o gateway Olá usados dados de saudação tootransfer.</span><span class="sxs-lookup"><span data-stu-id="98318-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="98318-325">Clique em **X** tooclose todos Olá páginas até que você</span><span class="sxs-lookup"><span data-stu-id="98318-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="98318-326">Voltar home page do toohello Olá **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="98318-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="98318-327">(opcional) Clique em **Pipelines**, clique em **ADFTutorialOnPremDF** e execute uma consulta drill-through nas tabelas de entrada (**Consumed**) ou nos conjuntos de dados de saída (**Produced**).</span><span class="sxs-lookup"><span data-stu-id="98318-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="98318-328">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) tooverify que um blob/arquivo é criado para cada hora.</span><span class="sxs-lookup"><span data-stu-id="98318-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Gerenciador de Armazenamento do Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="98318-330">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98318-330">Next steps</span></span>
* <span data-ttu-id="98318-331">Consulte [Data Management Gateway](data-factory-data-management-gateway.md) artigo para todos os Olá detalhes sobre Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="98318-332">Consulte [copiar dados de Blob do Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn sobre como repositório de dados do coletor tooa do repositório de dados de toomove de atividade de cópia toouse de uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="98318-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
