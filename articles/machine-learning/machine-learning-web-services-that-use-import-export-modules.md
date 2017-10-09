---
title: "aaaUsing importação/exportação de dados nos serviços web do aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como toouse Olá toosend de módulos de importação de dados e exportar dados e receber dados de um serviço web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="29362-103">Implantação de serviços Web do Azure AM que usam módulos Importar Dados e Exportar Dados</span><span class="sxs-lookup"><span data-stu-id="29362-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="29362-104">Quando você cria um experimento de previsão, normalmente adiciona uma entrada e uma saída de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="29362-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="29362-105">Quando você implanta um experimento hello, os consumidores podem enviar e receber dados do serviço web de saudação por meio de saudação entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="29362-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="29362-106">Para alguns aplicativos, os dados do cliente podem estar disponíveis a partir de um feed de dados ou já residirem em uma fonte de dados externa, como o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="29362-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="29362-107">Nesses casos, eles não precisam de dados de leitura e gravação usando saídas e entradas do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="29362-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="29362-108">Em vez disso, eles podem usar dados de tooread do serviço de execução de lote (BES) saudação da fonte de dados hello usando um módulo de importação de dados e gravar Olá tooa outro local de dados usando um módulo de exportar dados de resultados de pontuação.</span><span class="sxs-lookup"><span data-stu-id="29362-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="29362-109">Olá dados de importação e exportação módulos de dados, pode ler e gravar dados toovarious fornecem locais, como uma URL da Web via HTTP, uma consulta de Hive, um banco de dados SQL do Azure, armazenamento de tabela do Azure, armazenamento de BLOBs do Azure, um Feed de dados ou um banco de dados do SQL no local.</span><span class="sxs-lookup"><span data-stu-id="29362-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="29362-110">Este tópico usa hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" de exemplo e pressupõe Olá dataset já foi carregado em uma tabela do SQL Azure denominada censusdata.</span><span class="sxs-lookup"><span data-stu-id="29362-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="29362-111">Criar um teste de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="29362-111">Create hello training experiment</span></span>
<span data-ttu-id="29362-112">Quando você abre hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" exemplo de conjunto de dados do usa Olá exemplo adulto classificação binária de renda de censo.</span><span class="sxs-lookup"><span data-stu-id="29362-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="29362-113">E experiência Olá na tela hello terá aparência semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="29362-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Configuração inicial do experimento hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="29362-115">dados de saudação tooread da tabela do SQL Azure hello:</span><span class="sxs-lookup"><span data-stu-id="29362-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="29362-116">Exclua Olá módulo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="29362-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="29362-117">Na caixa de pesquisa de componentes hello, tipo de importação.</span><span class="sxs-lookup"><span data-stu-id="29362-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="29362-118">Saudação da lista de resultados, adicionar um *importar dados* toohello módulo experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="29362-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="29362-119">Conecte a saída de hello *importar dados* entrada de saudação do módulo de saudação *limpar dados ausentes* módulo.</span><span class="sxs-lookup"><span data-stu-id="29362-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="29362-120">No painel Propriedades, selecione **banco de dados do SQL Azure** em Olá **fonte de dados** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="29362-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="29362-121">Em Olá **nome do servidor de banco de dados**, **nome do banco de dados**, **nome de usuário**, e **senha** campos, insira as informações adequadas para Olá o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="29362-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="29362-122">No campo de consulta de banco de dados hello, digite Olá consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="29362-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="29362-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="29362-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="29362-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="29362-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="29362-125">Na parte inferior de saudação da tela de experimento hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="29362-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="29362-126">Criar experiência previsível Olá</span><span class="sxs-lookup"><span data-stu-id="29362-126">Create hello predictive experiment</span></span>
<span data-ttu-id="29362-127">Em seguida Configure experimento previsão de saudação do qual você implanta o serviço da web.</span><span class="sxs-lookup"><span data-stu-id="29362-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="29362-128">Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **serviço Web de previsão [recomendado]**.</span><span class="sxs-lookup"><span data-stu-id="29362-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="29362-129">Remover Olá *entrada de serviço Web* e *módulos de saída do serviço Web* de experiência de previsão hello.</span><span class="sxs-lookup"><span data-stu-id="29362-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="29362-130">Na caixa de pesquisa de componentes hello, tipo de exportação.</span><span class="sxs-lookup"><span data-stu-id="29362-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="29362-131">Saudação da lista de resultados, adicionar um *exportar dados* toohello módulo experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="29362-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="29362-132">Conecte a saída de hello *modelo de pontuação* entrada de saudação do módulo de saudação *exportar dados* módulo.</span><span class="sxs-lookup"><span data-stu-id="29362-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="29362-133">No painel Propriedades, selecione **banco de dados do SQL Azure** na lista suspensa de destino de dados hello.</span><span class="sxs-lookup"><span data-stu-id="29362-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="29362-134">Em Olá **nome do servidor de banco de dados**, **nome do banco de dados**, **nome de conta de usuário do servidor**, e **senha de conta de usuário do servidor** campos, digite informações adequadas Olá para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="29362-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="29362-135">Em Olá **lista de colunas toobe salvada separada por vírgulas** , digite os rótulos de pontuação.</span><span class="sxs-lookup"><span data-stu-id="29362-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="29362-136">Em Olá **campo de nome de tabela de dados**, digite dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="29362-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="29362-137">Se a tabela de saudação não existir, ele é criado quando o experimento hello está em execução ou serviço da web de saudação é chamado.</span><span class="sxs-lookup"><span data-stu-id="29362-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="29362-138">Em Olá **lista de colunas da datatable separada por vírgulas** campo, digite ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="29362-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="29362-139">Quando você escreve um aplicativo que chama Olá serviço web final, talvez você queira toospecify uma tabela diferente e entrada de consulta ou de destino em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="29362-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="29362-140">tooconfigure essas entradas e saídas, use Olá Olá de tooset de recurso de parâmetros do Web Service *importar dados* módulo *fonte de dados* propriedade e hello *exportar dados* modo propriedade de destino de dados.</span><span class="sxs-lookup"><span data-stu-id="29362-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="29362-141">Para obter mais informações sobre parâmetros de serviço da Web, consulte Olá [entrada de parâmetros de serviço Web AzureML](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) em hello Intelligence Cortana e o Blog de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="29362-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="29362-142">Olá tooconfigure parâmetros de serviço da Web para consulta de importação de saudação e a tabela de destino de saudação:</span><span class="sxs-lookup"><span data-stu-id="29362-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="29362-143">No painel de propriedades de saudação de saudação *importar dados* módulo, clique ícone Olá no hello parte superior direita da saudação **consulta de banco de dados** campo e selecione **definido como parâmetro de serviço web**.</span><span class="sxs-lookup"><span data-stu-id="29362-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="29362-144">No painel de propriedades de saudação de saudação *exportar dados* módulo, clique ícone Olá no hello parte superior direita da saudação **nome da tabela de dados** campo e selecione **definido como parâmetro de serviço web**.</span><span class="sxs-lookup"><span data-stu-id="29362-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="29362-145">Na parte inferior de saudação do hello *exportar dados* painel de propriedades do módulo, no hello **parâmetros de serviço Web** seção, clique em consulta de banco de dados e renomeie-a consulta.</span><span class="sxs-lookup"><span data-stu-id="29362-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="29362-146">Clique em **Nome da tabela de dados** e troque seu nome para **Tabela**.</span><span class="sxs-lookup"><span data-stu-id="29362-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="29362-147">Quando terminar, sua experiência deve ter aparência semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="29362-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Aparência final do experimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="29362-149">Agora você pode implantar Olá experiência como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="29362-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="29362-150">Implantar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="29362-150">Deploy hello web service</span></span>
<span data-ttu-id="29362-151">Você pode implantar um serviço web clássico ou novo tooeither.</span><span class="sxs-lookup"><span data-stu-id="29362-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="29362-152">Implantar um Serviço Web Clássico</span><span class="sxs-lookup"><span data-stu-id="29362-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="29362-153">toodeploy como um serviço Web clássico e criar um aplicativo tooconsume-lo:</span><span class="sxs-lookup"><span data-stu-id="29362-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="29362-154">Na parte inferior de saudação da tela de experimento hello, clique em executar.</span><span class="sxs-lookup"><span data-stu-id="29362-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="29362-155">Quando a saudação executar for concluída, clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]**.</span><span class="sxs-lookup"><span data-stu-id="29362-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="29362-156">No painel de serviço web hello, localize sua chave de API.</span><span class="sxs-lookup"><span data-stu-id="29362-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="29362-157">Copiar e salvar toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="29362-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="29362-158">Em hello **ponto de extremidade padrão** da tabela, clique em Olá **Batch Execution** Olá tooopen de link a página de ajuda de API.</span><span class="sxs-lookup"><span data-stu-id="29362-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="29362-159">No Visual Studio, crie um aplicativo de console C#: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="29362-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="29362-160">Na página de Ajuda da API do hello, localize Olá **código de exemplo** seção final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="29362-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="29362-161">Copie e cole Olá código c# de exemplo no arquivo Program.cs e remover todas as referências toohello blob storage.</span><span class="sxs-lookup"><span data-stu-id="29362-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="29362-162">Atualizar o valor Olá Olá *apiKey* variável com chave Olá API salvo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="29362-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="29362-163">Localizar Olá solicitação declaração e atualização Olá valores de parâmetros de serviço da Web que são passados toohello *importar dados* e *exportar dados* módulos.</span><span class="sxs-lookup"><span data-stu-id="29362-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="29362-164">Nesse caso, use a consulta original hello, mas definir um novo nome de tabela.</span><span class="sxs-lookup"><span data-stu-id="29362-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="29362-165">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="29362-165">Run hello application.</span></span> 

<span data-ttu-id="29362-166">Após a conclusão da saudação executar, uma nova tabela será adicionada toohello banco de dados que contém a saudação resultados de pontuação.</span><span class="sxs-lookup"><span data-stu-id="29362-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="29362-167">Implantar um serviço Web Novo</span><span class="sxs-lookup"><span data-stu-id="29362-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="29362-168">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="29362-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="29362-169">Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="29362-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="29362-170">toodeploy como um novo serviço da Web e criar um aplicativo tooconsume-lo:</span><span class="sxs-lookup"><span data-stu-id="29362-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="29362-171">Na parte inferior de saudação da tela de experimento hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="29362-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="29362-172">Quando a saudação executar for concluída, clique em **implantar o serviço da Web** e selecione **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="29362-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="29362-173">Na página de teste implantar hello, insira um nome para o serviço web, selecione um plano de preços e clique em **implantar**.</span><span class="sxs-lookup"><span data-stu-id="29362-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="29362-174">Em Olá **Quickstart** , clique em **consumir**.</span><span class="sxs-lookup"><span data-stu-id="29362-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="29362-175">Em Olá **código de exemplo** seção, clique em **lote**.</span><span class="sxs-lookup"><span data-stu-id="29362-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="29362-176">No Visual Studio, crie um aplicativo de console C#: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="29362-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="29362-177">Copie e cole o código de exemplo hello c# em seu arquivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="29362-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="29362-178">Atualizar o valor Olá Olá *apiKey* variável com hello **chave primária** localizado em Olá **informações básicas de consumo** seção.</span><span class="sxs-lookup"><span data-stu-id="29362-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="29362-179">Localizar Olá *scoreRequest* declaração e atualizar valores de saudação de parâmetros de serviço da Web que são passados toohello *importar dados* e *exportar dados* módulos.</span><span class="sxs-lookup"><span data-stu-id="29362-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="29362-180">Nesse caso, use a consulta original hello, mas definir um novo nome de tabela.</span><span class="sxs-lookup"><span data-stu-id="29362-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="29362-181">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="29362-181">Run hello application.</span></span> 

