---
title: Mover dados - Gateway de Gerenciamento de Dados | Microsoft Docs
description: Configure um gateway de dados para mover dados entre o local e a nuvem. Use o Gateway de Gerenciamento de Dados no Azure Data Factory para mover os dados.
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
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="abd1b-105">Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="abd1b-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="abd1b-106">Este artigo fornece uma visão geral da integração de dados entre os armazenamentos de dados locais e os armazenamentos de dados na nuvem usando o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="abd1b-107">Ele se baseia no artigo [Atividades de Movimentação de Dados](data-factory-data-movement-activities.md) e em outros artigos de conceitos principais de data factory: [conjuntos de dados](data-factory-create-datasets.md) e [pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="abd1b-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="abd1b-108">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="abd1b-108">Data Management Gateway</span></span>
<span data-ttu-id="abd1b-109">Você deve instalar o Gateway de Gerenciamento de Dados em seu computador local para habilitar a movimentação de dados de/para um armazenamento de dados local.</span><span class="sxs-lookup"><span data-stu-id="abd1b-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="abd1b-110">O gateway pode ser instalado no mesmo computador que o armazenamento de dados ou em outro computador, desde que o gateway possa se conectar com o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abd1b-111">Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="abd1b-112">O passo a passo a seguir mostra como você pode criar uma Data Factory com um pipeline que move dados de um banco de dados local do **SQL Server** para um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="abd1b-113">Como parte do passo a passo, você instala e configura o Gateway de Gerenciamento de Dados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="abd1b-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="abd1b-114">Passo a passo: copiar os dados locais para a nuvem</span><span class="sxs-lookup"><span data-stu-id="abd1b-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="abd1b-115">Neste passo a passo, você realizará as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="abd1b-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="abd1b-116">Criar uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-116">Create a data factory.</span></span>
2. <span data-ttu-id="abd1b-117">Criar um Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="abd1b-118">Criar serviços vinculados para armazenamentos de dados de origem e de coletor.</span><span class="sxs-lookup"><span data-stu-id="abd1b-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="abd1b-119">Nesta etapa, você cria conjuntos de dados para representar a entrada e a saída de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="abd1b-120">Criar um pipeline com uma atividade de cópia para mover os dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="abd1b-121">Pré-requisitos para o tutorial</span><span class="sxs-lookup"><span data-stu-id="abd1b-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="abd1b-122">Antes de iniciar este passo a passo, é necessário ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="abd1b-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="abd1b-123">**Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-123">**Azure subscription**.</span></span>  <span data-ttu-id="abd1b-124">Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="abd1b-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="abd1b-125">Consulte o artigo [Avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="abd1b-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="abd1b-126">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-126">**Azure Storage Account**.</span></span> <span data-ttu-id="abd1b-127">Você utiliza o armazenamento de Blobs como um armazenamento de dados **destino/coletor** neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="abd1b-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="abd1b-128">Se você não tiver uma conta de armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para conhecer as etapas para criar um.</span><span class="sxs-lookup"><span data-stu-id="abd1b-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="abd1b-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-129">**SQL Server**.</span></span> <span data-ttu-id="abd1b-130">Neste tutorial, você utiliza um Banco de Dados do SQL Server local como um armazenamento de dados de **origem**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="abd1b-131">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="abd1b-131">Create data factory</span></span>
<span data-ttu-id="abd1b-132">Nesta etapa, você usa o Portal do Azure para criar uma instância do Azure Data Factory chamada **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="abd1b-133">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abd1b-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abd1b-134">Clique em **+ NOVO**, clique em **Inteligência + análise** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Novo -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="abd1b-136">Na página **Novo data factory**, insira **ADFTutorialOnPremDF** como o Nome.</span><span class="sxs-lookup"><span data-stu-id="abd1b-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Adicionar ao quadro inicial](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="abd1b-138">O nome da data factory do Azure deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="abd1b-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="abd1b-139">Se você receber o erro: **O nome da data factory “ADFTutorialOnPremDF” não está disponível**, altere o nome da data factory (por exemplo, yournameADFTutorialOnPremDF) e tente criá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="abd1b-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="abd1b-140">Use esse nome em vez de ADFTutorialOnPremDF ao executar as etapas restantes neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="abd1b-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="abd1b-141">O nome do data factory pode ser registrado futuramente como um nome **DNS** e tornar-se publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="abd1b-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="abd1b-142">Escolha a **assinatura do Azure** onde você deseja que o data factory seja criado.</span><span class="sxs-lookup"><span data-stu-id="abd1b-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="abd1b-143">Selecione um **grupo de recursos** existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="abd1b-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="abd1b-144">Para o tutorial, crie um grupo de recursos chamado: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="abd1b-145">Clique em **Criar** na página **Novo data factory**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="abd1b-146">Para criar instâncias de Data Factory, você deve ser um membro da função [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) no nível de assinatura/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="abd1b-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="abd1b-147">Depois que a criação estiver concluída, você verá a página **Data Factory** conforme mostrado na imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="abd1b-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Página inicial do Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="abd1b-149">Criar gateway</span><span class="sxs-lookup"><span data-stu-id="abd1b-149">Create gateway</span></span>
1. <span data-ttu-id="abd1b-150">Na página **Data Factory**, clique no bloco **Criar e implantar** para iniciar o **Editor** do data factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Bloco Criar e implantar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="abd1b-152">No Editor de Data Factory, clique em **... Mais** na barra de ferramentas e clique em **Novo gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="abd1b-153">Como alternativa, você pode clicar com o botão direito em **Gateways de Dados** no modo de exibição de árvore e clicar em **Novo gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Novo gateway de dados na barra de ferramentas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="abd1b-155">Na página **Criar**, digite **adftutorialgateway** como **nome** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Página Criar Gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="abd1b-157">Neste passo a passo, você cria o gateway lógico com apenas um nó (computador do Windows local).</span><span class="sxs-lookup"><span data-stu-id="abd1b-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="abd1b-158">Você pode escalar horizontalmente um Gateway de Gerenciamento de Dados por meio da associação de vários computadores locais com o gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="abd1b-159">Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó.</span><span class="sxs-lookup"><span data-stu-id="abd1b-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="abd1b-160">Esse recurso também está disponível para um gateway lógico com um único nó.</span><span class="sxs-lookup"><span data-stu-id="abd1b-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="abd1b-161">Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="abd1b-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="abd1b-162">Na página **Configurar**, clique em **Instalar diretamente neste computador**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="abd1b-163">Essa ação baixará o pacote de instalação para o gateway, instalará, configurará e registrará o gateway no computador.</span><span class="sxs-lookup"><span data-stu-id="abd1b-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="abd1b-164">Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="abd1b-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="abd1b-165">Se você estiver usando o Chrome, vá para a [loja na Web do Chrome](https://chrome.google.com/webstore/), pesquise a palavra-chave "ClickOnce", escolha uma das extensões do ClickOnce e instale-a.</span><span class="sxs-lookup"><span data-stu-id="abd1b-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="abd1b-166">Faça o mesmo para o Firefox (instalar o suplemento).</span><span class="sxs-lookup"><span data-stu-id="abd1b-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="abd1b-167">Clique no botão **Abrir menu** na barra de ferramentas (**três linhas horizontais** no canto superior direito), clique em **Complementos**, pesquise a palavra-chave "ClickOnce", escolha uma das extensões do ClickOnce e instale-a.</span><span class="sxs-lookup"><span data-stu-id="abd1b-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Página Gateway – Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="abd1b-169">Essa é a maneira mais fácil (um clique) de baixar, instalar, configurar e registrar o gateway em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="abd1b-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="abd1b-170">Você pode ver que o aplicativo **Gerenciador de Configuração de Gateway de gerenciamento de dados da Microsoft** está instalado no computador.</span><span class="sxs-lookup"><span data-stu-id="abd1b-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="abd1b-171">Você também pode encontrar o executável **ConfigManager.exe** na pasta: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="abd1b-172">Você também pode baixar e instalar o gateway manualmente usando os links nessa página e registrá-lo usando a chave mostrada na caixa de texto **NOVA CHAVE** .</span><span class="sxs-lookup"><span data-stu-id="abd1b-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="abd1b-173">Confira o artigo [Data Management Gateway](data-factory-data-management-gateway.md) (Gateway de Gerenciamento de Dados) para obter todos os detalhes sobre o gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="abd1b-174">Você deve ser um administrador no computador local para instalar e configurar com êxito o Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="abd1b-175">Você pode acrescentar usuários adicionais ao grupo local de usuários do **Gateway de Gerenciamento de dados do Windows** .</span><span class="sxs-lookup"><span data-stu-id="abd1b-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="abd1b-176">Os membros desse grupo podem usar a ferramenta Gerenciador de Configuração de Gateway de Gerenciamento de Dados para configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="abd1b-177">Aguarde alguns minutos ou até ver a seguinte mensagem de notificação:</span><span class="sxs-lookup"><span data-stu-id="abd1b-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Instalação do gateway bem-sucedida](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="abd1b-179">Inicie o aplicativo **Gerenciador de Configuração de Gateway de gerenciamento de dados** no computador.</span><span class="sxs-lookup"><span data-stu-id="abd1b-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="abd1b-180">Na janela **Search**, digite **Gateway de Gerenciamento de Dados** para acessar esse utilitário.</span><span class="sxs-lookup"><span data-stu-id="abd1b-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="abd1b-181">Você também pode encontrar o executável **ConfigManager.exe** na pasta: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="abd1b-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gerenciador de configuração de gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="abd1b-183">Confirme que você vê a mensagem `adftutorialgateway is connected to the cloud service`.</span><span class="sxs-lookup"><span data-stu-id="abd1b-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="abd1b-184">A barra de status inferior exibe a mensagem **Conectado ao serviço de nuvem** junto com uma **marca de seleção verde**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="abd1b-185">Na guia **Página inicial**, você também pode fazer as seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="abd1b-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="abd1b-186">**Registrar** um gateway com uma chave do Portal do Azure usando o botão Registrar.</span><span class="sxs-lookup"><span data-stu-id="abd1b-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="abd1b-187">**Parar** o Serviço de Host do Gateway de Gerenciamento de Dados em execução no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="abd1b-188">**Agendar atualizações** para serem instaladas em uma hora específica do dia.</span><span class="sxs-lookup"><span data-stu-id="abd1b-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="abd1b-189">Exibir quando o gateway foi **atualizado pela última vez**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="abd1b-190">Especifique a hora em que uma atualização para o gateway pode ser instalada.</span><span class="sxs-lookup"><span data-stu-id="abd1b-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="abd1b-191">Alterne para a guia **Configurações** . O certificado especificado na seção **Certificado** é usado para criptografar/descriptografar as credenciais do armazenamento de dados local que você especifica no portal.</span><span class="sxs-lookup"><span data-stu-id="abd1b-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="abd1b-192">(opcional) Como alternativa, clique em **Alterar** para usar seu próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="abd1b-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="abd1b-193">Por padrão, o gateway usa o certificado que é gerado automaticamente pelo serviço de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Configuração do certificado do gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="abd1b-195">Você também pode executar as seguintes ações na guia **Configurações**:</span><span class="sxs-lookup"><span data-stu-id="abd1b-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="abd1b-196">Exibir ou exportar o certificado que está sendo usado pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="abd1b-197">Alterar o ponto de extremidade HTTPS usado pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="abd1b-198">Defina um proxy de HTTP para ser usado pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="abd1b-199">(opcional) Mude para a guia **Diagnóstico** e marque a opção **Habilitar log detalhado** se você quiser habilitar o log detalhado que pode ser usado para solucionar problemas com o gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="abd1b-200">As informações de log podem ser encontradas no **Visualizador de Eventos** em **Logs de Aplicativos e Serviços** -> **nó Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Guia Diagnósticos](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="abd1b-202">Você também pode executar as seguintes ações na guia **Diagnóstico** :</span><span class="sxs-lookup"><span data-stu-id="abd1b-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="abd1b-203">Use a seção **Testar Conexão** para uma fonte de dados local usando o gateway.</span><span class="sxs-lookup"><span data-stu-id="abd1b-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="abd1b-204">Clique em **Exibir Logs** para ver o log de Gateway de Gerenciamento de Dados em uma janela do Visualizador de Eventos.</span><span class="sxs-lookup"><span data-stu-id="abd1b-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="abd1b-205">Clique em **Enviar Logs** para carregar um arquivo zip com logs dos últimos sete dias para a Microsoft a fim de facilitar a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="abd1b-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="abd1b-206">Na guia **Diagnóstico**, na seção **Testar Conexão**, selecione **SqlServer** para o tipo do armazenamento de dados, insira o nome do servidor de banco de dados, o nome do banco de dados, especifique o tipo de autenticação, digite o nome de usuário e a senha, e clique em **Testar** para testar se o gateway pode se conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="abd1b-207">Mude para o navegador da Web e, no **Portal do Azure**, clique em **OK** na página **Configurar** e na página **Novo gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="abd1b-208">Você deve consultar **adftutorialgateway** em **Gateways de Dados** no modo de exibição de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="abd1b-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="abd1b-209">Se você clicar nisso, verá o JSON associado.</span><span class="sxs-lookup"><span data-stu-id="abd1b-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="abd1b-210">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="abd1b-210">Create linked services</span></span>
<span data-ttu-id="abd1b-211">Nesta etapa, você cria dois serviços vinculados: **AzureStorageLinkedService** e **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="abd1b-212">O **SqlServerLinkedService** vincula um banco de dados local SQL Server e o serviço vinculado **AzureStorageLinkedService** vincula um repositório de blob do Azure ao Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="abd1b-213">Você criará um pipeline posteriormente neste passo a passo que copia dados do banco de dados SQL Server local para o repositório de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="abd1b-214">Adicionar um serviço vinculado a um banco de dados SQL Server local</span><span class="sxs-lookup"><span data-stu-id="abd1b-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="abd1b-215">No **Editor do Data Factory**, clique em **Novo armazenamento de dados** na barra de ferramentas e selecione **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Serviço vinculado do SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="abd1b-217">No **Editor JSON** à direita, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="abd1b-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="abd1b-218">Em **gatewayName**, especifique **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="abd1b-219">Em **connectionString**, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="abd1b-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="abd1b-220">Para **nomedoservidor**, insira o nome do servidor que hospeda o banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="abd1b-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="abd1b-221">Para **nomedobancodedados**, insira o nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="abd1b-222">Clique no botão **Criptografar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="abd1b-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="abd1b-223">Você vê o aplicativo do Gerenciador de Credenciais.</span><span class="sxs-lookup"><span data-stu-id="abd1b-223">You see the Credentials Manager application.</span></span>

         ![Aplicativo do Gerenciador de credenciais](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="abd1b-225">Na caixa de diálogo **Definindo Credenciais**, especifique o tipo de autenticação, nome de usuário e senha, e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="abd1b-226">Se a conexão for bem-sucedida, as credenciais criptografadas serão armazenadas no JSON e a caixa de diálogo é fechada.</span><span class="sxs-lookup"><span data-stu-id="abd1b-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="abd1b-227">Feche a guia vazia do navegador que iniciou a caixa de diálogo se ela não tiver sido fechada automaticamente e volte à guia com o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="abd1b-228">Na máquina de gateway, essas credenciais são **criptografadas** usando um certificado que o serviço Data Factory detém.</span><span class="sxs-lookup"><span data-stu-id="abd1b-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="abd1b-229">Como alternativa, se você quiser usar o certificado associado ao Gateway de Gerenciamento de Dados, confira [Set credentials securely (Definir credenciais com segurança)](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="abd1b-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="abd1b-230">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="abd1b-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="abd1b-231">Você deverá ver o serviço vinculado na exibição de árvore.</span><span class="sxs-lookup"><span data-stu-id="abd1b-231">You should see the linked service in the tree view.</span></span>

      ![Serviço vinculado do SQL Server na exibição de árvore](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="abd1b-233">Adicionar um serviço vinculado para uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="abd1b-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="abd1b-234">No **Editor do Data Factory**, clique em **Novo armazenamento de dados** na barra de comandos e clique em **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="abd1b-235">Insira o nome da sua conta de armazenamento do Azure em **Nome da conta**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="abd1b-236">Insira a chave da sua conta de armazenamento do Azure em **Chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="abd1b-237">Clique em **Implantar** para implantar o **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="abd1b-238">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="abd1b-238">Create datasets</span></span>
<span data-ttu-id="abd1b-239">Nesta etapa, você cria conjuntos de dados de entrada e saída que representam dados de entrada e saída da operação de cópia (banco de dados SQL Server local = > armazenamento de blobs do Azure).</span><span class="sxs-lookup"><span data-stu-id="abd1b-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="abd1b-240">Antes de criar conjuntos de dados, primeiro é necessário fazer o seguinte (etapas detalhadas seguem a lista):</span><span class="sxs-lookup"><span data-stu-id="abd1b-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="abd1b-241">Criar uma tabela chamada **emp** no banco de dados SQL Server adicionado como um serviço vinculado à data factory e inserir alguns exemplos de entradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="abd1b-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="abd1b-242">Crie um contêiner de blob chamado **adftutorial** na conta de armazenamento de blob do Azure que você adicionou como um serviço vinculado à data factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="abd1b-243">Preparar o SQL Server local para o tutorial</span><span class="sxs-lookup"><span data-stu-id="abd1b-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="abd1b-244">No banco de dados especificado para o serviço vinculado do SQL Server local (**SqlServerLinkedService**), use o seguinte script SQL para criar a tabela **emp** no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

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
2. <span data-ttu-id="abd1b-245">Insira algum exemplo na tabela:</span><span class="sxs-lookup"><span data-stu-id="abd1b-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="abd1b-246">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="abd1b-246">Create input dataset</span></span>

1. <span data-ttu-id="abd1b-247">No **Editor de Data Factory**, clique em **... Mais**, clique em **Novo conjunto de dados** na barra de comandos e clique em **tabela SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="abd1b-248">Substitua o JSON no painel direito pelo texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="abd1b-248">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="abd1b-249">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="abd1b-249">Note the following points:</span></span>

   * <span data-ttu-id="abd1b-250">**type** é definido como **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="abd1b-251">**tablename** está definido como **emp**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="abd1b-252">**linkedServiceName** está definido como **SqlServerLinkedService** (você criou esse serviço vinculado na Etapa anteriormente neste passo a passo).</span><span class="sxs-lookup"><span data-stu-id="abd1b-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="abd1b-253">Para um conjunto de dados de entrada que não é gerada por outro pipeline na Azure Data Factory, você deve configurar **external** como **true**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="abd1b-254">Ela indica que os dados de entrada são produzidos externos ao serviço Data Factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="abd1b-255">Opcionalmente, você pode especificar quaisquer políticas de dados externas usando o elemento **externalData** na seção **Policy**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="abd1b-256">Confira [Mover dados para/de SQL Server](data-factory-sqlserver-connector.md) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="abd1b-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="abd1b-257">Clique em **Implantar** na barra de comando para implantar o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="abd1b-258">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="abd1b-258">Create output dataset</span></span>

1. <span data-ttu-id="abd1b-259">No **Editor Data Factory**, clique em **Novo conjunto de dados** na barra de comandos e clique em **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="abd1b-260">Substitua o JSON no painel direito pelo texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="abd1b-260">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="abd1b-261">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="abd1b-261">Note the following points:</span></span>

   * <span data-ttu-id="abd1b-262">**type** é definido como **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="abd1b-263">O **linkedServiceName** é definido como **AzureStorageLinkedService** (você criou esse serviço vinculado na Etapa 2).</span><span class="sxs-lookup"><span data-stu-id="abd1b-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="abd1b-264">**folderPath** é definido como **adftutorial/outfromonpremdf**, em que outfromonpremdf é a pasta no contêiner adftutorial.</span><span class="sxs-lookup"><span data-stu-id="abd1b-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="abd1b-265">Crie o contêiner **adftutorial** se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="abd1b-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="abd1b-266">A **availability** é definida como **hourly** (**frequency** definida como **hour** e **interval** definido como **1**).</span><span class="sxs-lookup"><span data-stu-id="abd1b-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="abd1b-267">O serviço Data Factory gera uma fatia de dados de saída a cada hora na tabela **emp** no banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="abd1b-268">Se você não especificar um **fileName** para uma **tabela de saída**, os arquivos gerados no **folderPath** serão nomeados no seguinte formato: Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt).</span><span class="sxs-lookup"><span data-stu-id="abd1b-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="abd1b-269">Para definir **folderPath** e **fileName** dinamicamente com base no horário **SliceStart**, use a propriedade partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="abd1b-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="abd1b-270">No exemplo a seguir, folderPath usa o ano, mês e dia de SliceStart (hora de início da fatia que está sendo processada) e fileName usa a hora de SliceStart.</span><span class="sxs-lookup"><span data-stu-id="abd1b-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="abd1b-271">Por exemplo, se uma fatia é produzida para 2014-10-20T08:00:00, o folderName é definido como wikidatagateway/wikisampledataout/2014/10/20 e o fileName é definido como 08.csv.</span><span class="sxs-lookup"><span data-stu-id="abd1b-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

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

    <span data-ttu-id="abd1b-272">Confira [Mover dados para/de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="abd1b-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="abd1b-273">Clique em **Implantar** na barra de comando para implantar o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="abd1b-274">Confirme que você vê os conjuntos de dados na exibição de árvore.</span><span class="sxs-lookup"><span data-stu-id="abd1b-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="abd1b-275">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="abd1b-275">Create pipeline</span></span>
<span data-ttu-id="abd1b-276">Nesta etapa, você criará um **pipeline** com uma **Atividade de Cópia** que usa **EmpOnPremSQLTable** como entrada e **OutputBlobTable** como saída.</span><span class="sxs-lookup"><span data-stu-id="abd1b-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="abd1b-277">No Editor de Data Factory, clique em **... Mais** e clique em **Novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="abd1b-278">Substitua o JSON no painel direito pelo texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="abd1b-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
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
   > <span data-ttu-id="abd1b-279">Substitua o valor da propriedade **start** pelo dia atual e o valor de **end** pelo dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="abd1b-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="abd1b-280">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="abd1b-280">Note the following points:</span></span>

   * <span data-ttu-id="abd1b-281">Na seção de atividades, há somente uma atividade cujo **type** é definido como **Copy**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="abd1b-282">A **entrada** da atividade é definida como **EmpOnPremSQLTable** e a **saída** da atividade é definida como **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="abd1b-283">na seção **typeProperties**, **SqlSource** é especificado como o **tipo de origem** e **BlobSink **é especificado como o **tipo de coletor**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="abd1b-284">A consulta SQL `select * from emp` é especificada para a propriedade **sqlReaderQuery** de **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="abd1b-285">Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="abd1b-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="abd1b-286">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="abd1b-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="abd1b-287">A hora **final** é opcional, mas nós a usaremos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="abd1b-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="abd1b-288">Se você não especificar o valor para a propriedade **end**, ele será calculado como "**início + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="abd1b-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="abd1b-289">Para executar o pipeline indefinidamente, especifique **9/9/9999** como o valor para a propriedade **end**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="abd1b-290">Especificando o período ativo de um pipeline, você está definindo a duração de tempo em que as fatias de dados serão processadas com base nas propriedades de **Disponibilidade** que foram definidas para cada conjunto de dados da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abd1b-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="abd1b-291">No exemplo, como cada fatia de dados é produzida por hora, existem 24 fatias de dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="abd1b-292">Clique em **Implantar** na barra de comandos para implantar o conjunto de dados (a tabela é um conjunto de dados retangular).</span><span class="sxs-lookup"><span data-stu-id="abd1b-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="abd1b-293">Confirme que o pipeline aparece na exibição em árvore no nó **Pipelines**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="abd1b-294">Agora, clique em **X** duas vezes para fechar as páginas até que você volte à página **Data Factory** para o **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="abd1b-295">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="abd1b-295">**Congratulations!**</span></span> <span data-ttu-id="abd1b-296">Você criou um data factory do Azure, serviços vinculados, conjuntos de dados e uma pipeline e a pipeline agendada com êxito.</span><span class="sxs-lookup"><span data-stu-id="abd1b-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="abd1b-297">Exibir a data factory em um Modo de Exibição de Diagrama</span><span class="sxs-lookup"><span data-stu-id="abd1b-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="abd1b-298">No **portal do Azure**, clique no bloco **Diagrama** na página inicial do data factory **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="abd1b-299">:</span><span class="sxs-lookup"><span data-stu-id="abd1b-299">:</span></span>

    ![Link do diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="abd1b-301">Você deverá ver o diagrama semelhante à imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="abd1b-301">You should see the diagram similar to the following image:</span></span>

    ![Exibição de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="abd1b-303">É possível ampliar, reduzir, aplicar zoom de 100%, ajustar nível de zoom, posicionar pipelines e conjuntos de dados automaticamente, bem como mostrar informações de linhagem (realça itens upstream e downstream dos itens selecionados).</span><span class="sxs-lookup"><span data-stu-id="abd1b-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="abd1b-304">Você pode clicar duas vezes em um objeto (pipeline ou conjunto de dados de entrada/saída) para ver as propriedades dele.</span><span class="sxs-lookup"><span data-stu-id="abd1b-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="abd1b-305">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="abd1b-305">Monitor pipeline</span></span>
<span data-ttu-id="abd1b-306">Nesta etapa, você utiliza o portal do Azure para monitorar o que está acontecendo em um data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="abd1b-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="abd1b-307">Você também pode usar os cmdlets do PowerShell para monitorar conjuntos de dados e pipelines.</span><span class="sxs-lookup"><span data-stu-id="abd1b-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="abd1b-308">Para obter detalhes sobre monitoramento, consulte [Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="abd1b-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="abd1b-309">No diagrama, clique duas vezes em **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Fatias de EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="abd1b-311">Observe que todas as fatias de dados estão no estado **Pronto** porque a duração do pipeline (hora de início até a hora de término) está no passado.</span><span class="sxs-lookup"><span data-stu-id="abd1b-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="abd1b-312">Isso também ocorre porque você inseriu os dados no banco de dados SQL Server e eles estão lá está o tempo todo.</span><span class="sxs-lookup"><span data-stu-id="abd1b-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="abd1b-313">Confirme se nenhuma fatia aparecerá na seção **Fatias com problema** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="abd1b-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="abd1b-314">Para exibir todas as fatias, clique em **Ver mais** na parte inferior da lista de fatias.</span><span class="sxs-lookup"><span data-stu-id="abd1b-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="abd1b-315">Agora, na página **Conjuntos de Dados**, clique em **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Fatias de OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="abd1b-317">Clique em qualquer fatia de dados na lista e você deverá ver a página **Fatia de Dados**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="abd1b-318">Você vê as execuções de atividade para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="abd1b-318">You see activity runs for the slice.</span></span> <span data-ttu-id="abd1b-319">Você normalmente vê apenas uma atividade sendo executada.</span><span class="sxs-lookup"><span data-stu-id="abd1b-319">You see only one activity run usually.</span></span>  

    ![Folha Fatia de dados](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="abd1b-321">Quando a fatia não está no estado **Pronto**, você pode ver as fatias upstream que não estão Prontas e estão impedindo a execução da fatia atual na lista **Fatias upstream que não estão prontas**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="abd1b-322">Clique na **execução de atividade** na lista na parte inferior para ver **detalhes de execução da atividade**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Página Detalhes da Execução da Atividade](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="abd1b-324">Você veria informações como taxa de transferência, duração e o gateway usado para transferir os dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="abd1b-325">Clique no **X** para fechar todas as páginas até você</span><span class="sxs-lookup"><span data-stu-id="abd1b-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="abd1b-326">voltar para a home page do **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="abd1b-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="abd1b-327">(opcional) Clique em **Pipelines**, clique em **ADFTutorialOnPremDF** e execute uma consulta drill-through nas tabelas de entrada (**Consumed**) ou nos conjuntos de dados de saída (**Produced**).</span><span class="sxs-lookup"><span data-stu-id="abd1b-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="abd1b-328">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para verificar se um arquivo/blob é criado para cada hora.</span><span class="sxs-lookup"><span data-stu-id="abd1b-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Gerenciador de Armazenamento do Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="abd1b-330">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abd1b-330">Next steps</span></span>
* <span data-ttu-id="abd1b-331">Confira o artigo [Data Management Gateway](data-factory-data-management-gateway.md) (Gateway de Gerenciamento de Dados) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="abd1b-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="abd1b-332">Confira [Copiar dados do Blob do Azure para o SQL Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para saber mais sobre como usar a Atividade de Cópia para mover dados de um repositório de dados de origem para um repositório de dados de coletor.</span><span class="sxs-lookup"><span data-stu-id="abd1b-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
