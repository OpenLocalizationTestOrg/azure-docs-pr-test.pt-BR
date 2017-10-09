---
title: "Aprendizado de máquina do Azure SQL Data warehouse de aaaUse | Microsoft Docs"
description: "Tutorial para usar o Azure Machine Learning com o Data Warehouse do SQL Azure para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="571a6-103">Use o Azure Machine Learning com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="571a6-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="571a6-104">O aprendizado de máquina do Azure é um serviço de análise preditiva totalmente gerenciado que você pode usar modelos de previsão toocreate em relação aos dados no SQL Data Warehouse e, em seguida, publicar como serviços web pronto para consumo.</span><span class="sxs-lookup"><span data-stu-id="571a6-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="571a6-105">Você pode Conheça os fundamentos de saudação da análise de previsão e aprendizado de máquina lendo [tooMachine Introdução aprendizado no Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="571a6-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="571a6-106">Em seguida, você pode aprender como toocreate, treinamento, pontuação e testar um modelo de aprendizado de máquina usando Olá [criar experiência tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="571a6-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="571a6-107">Neste artigo, você aprenderá como Olá toodo usando Olá a seguir [estúdio de aprendizado de máquina do Azure][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="571a6-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="571a6-108">Ler dados de seu banco de dados toocreate, treinar e pontuação de um modelo de previsão</span><span class="sxs-lookup"><span data-stu-id="571a6-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="571a6-109">Gravar dados tooyour banco de dados</span><span class="sxs-lookup"><span data-stu-id="571a6-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="571a6-110">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="571a6-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="571a6-111">Podemos lê dados da tabela Produtos no banco de dados do hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="571a6-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="571a6-112">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="571a6-112">Step 1</span></span>
<span data-ttu-id="571a6-113">Iniciar um novo teste, clique em + novo final Olá Olá janela estúdio de aprendizado de máquina, selecione EXPERIMENTO e experiências em branco.</span><span class="sxs-lookup"><span data-stu-id="571a6-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="571a6-114">Padrão de Select Olá experimentar nome hello superior da tela hello e renomeie-a como toosomething significativo, por exemplo, previsão de preço de bicicleta.</span><span class="sxs-lookup"><span data-stu-id="571a6-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="571a6-115">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="571a6-115">Step 2</span></span>
<span data-ttu-id="571a6-116">Procure por módulo de leitor de saudação na paleta de saudação de conjuntos de dados e módulos esquerda Olá da tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="571a6-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="571a6-117">Arraste a tela de experimento Olá módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="571a6-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="571a6-118">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="571a6-118">Step 3</span></span>
<span data-ttu-id="571a6-119">Selecione o módulo do leitor de saudação e preencher o painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="571a6-120">Selecione o banco de dados do SQL Azure como Olá fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="571a6-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="571a6-121">Nome do servidor de banco de dados: nome do servidor de saudação de tipo.</span><span class="sxs-lookup"><span data-stu-id="571a6-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="571a6-122">Você pode usar o hello [portal do Azure] [ Azure portal] toofind isso.</span><span class="sxs-lookup"><span data-stu-id="571a6-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="571a6-123">Nome do banco de dados: nome de saudação do tipo de banco de dados no servidor de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="571a6-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="571a6-124">Nome de conta de usuário do servidor: nome de usuário de saudação do tipo de uma conta que tenha permissões de acesso para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="571a6-125">Senha de conta de usuário do servidor: fornecer senha Olá Olá especificar conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="571a6-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="571a6-126">Aceitar qualquer certificado de servidor: Use esta opção (menos segura), se você quiser tooskip revisando o certificado de saudação do site antes de ler os dados.</span><span class="sxs-lookup"><span data-stu-id="571a6-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="571a6-127">Consulta de banco de dados: insira uma instrução SQL que descreve dados Olá deseja tooread.</span><span class="sxs-lookup"><span data-stu-id="571a6-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="571a6-128">Nesse caso, estamos lê dados da tabela de produto usando Olá consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="571a6-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="571a6-129">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="571a6-129">Step 4</span></span>
1. <span data-ttu-id="571a6-130">Execute o teste de saudação clicando em execução em tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="571a6-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="571a6-131">Quando termina de experiência hello, módulo de leitor de saudação terá tooindicate uma marca de seleção verde que ela foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="571a6-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="571a6-132">Observe também Olá concluído status de execução no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="571a6-133">toosee Olá dados importados, clique Olá a porta de saída na parte inferior de saudação do automóvel Olá de conjunto de dados e selecione Visualizar.</span><span class="sxs-lookup"><span data-stu-id="571a6-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="571a6-134">Crie, treine e pontue um modelo</span><span class="sxs-lookup"><span data-stu-id="571a6-134">Create, train and score a model</span></span>
<span data-ttu-id="571a6-135">Agora você pode usar esse conjunto de dados para:</span><span class="sxs-lookup"><span data-stu-id="571a6-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="571a6-136">Criar um modelo: processar dados e definir recursos</span><span class="sxs-lookup"><span data-stu-id="571a6-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="571a6-137">Treinar modelo de saudação: escolha e aplicar um algoritmo de aprendizado</span><span class="sxs-lookup"><span data-stu-id="571a6-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="571a6-138">Pontuação e teste Olá modelo: prever o novo preço de bicicleta</span><span class="sxs-lookup"><span data-stu-id="571a6-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="571a6-139">mais informações sobre como toocreate, treinamento, pontuação e testar uma saudação de uso do modelo de aprendizado de máquina do toolearn [criar experiência tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="571a6-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="571a6-140">Gravar dados tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="571a6-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="571a6-141">Podemos gravará Olá tabela de tooProductPriceForecast de conjunto de resultados no banco de dados do hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="571a6-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="571a6-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="571a6-142">Step 1</span></span>
<span data-ttu-id="571a6-143">Procure o módulo de gravador Olá na paleta de saudação de conjuntos de dados e módulos esquerda Olá da tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="571a6-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="571a6-144">Arraste a tela de experimento Olá módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="571a6-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="571a6-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="571a6-145">Step 2</span></span>
<span data-ttu-id="571a6-146">Selecione o módulo de gravador hello e preencher o painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="571a6-147">Selecione o banco de dados do SQL Azure como Olá destino de dados.</span><span class="sxs-lookup"><span data-stu-id="571a6-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="571a6-148">Nome do servidor de banco de dados: nome do servidor de saudação de tipo.</span><span class="sxs-lookup"><span data-stu-id="571a6-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="571a6-149">Você pode usar o hello [portal do Azure] [ Azure portal] toofind isso.</span><span class="sxs-lookup"><span data-stu-id="571a6-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="571a6-150">Nome do banco de dados: nome de saudação do tipo de banco de dados no servidor de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="571a6-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="571a6-151">Nome de conta de usuário do servidor: nome de usuário de saudação do tipo de uma conta que tenha permissões de gravação para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="571a6-152">Senha de conta de usuário do servidor: fornecer senha Olá Olá especificar conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="571a6-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="571a6-153">Aceitar qualquer certificado de servidor (mínimo): Selecione esta opção se você não deseja o certificado de saudação tooview.</span><span class="sxs-lookup"><span data-stu-id="571a6-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="571a6-154">Lista separada por vírgulas de colunas toobe salvada: forneça uma lista de colunas de conjunto de dados ou o resultado de saudação que você deseja toooutput.</span><span class="sxs-lookup"><span data-stu-id="571a6-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="571a6-155">Nome da tabela de dados: especifique nome Olá Olá da tabela de dados.</span><span class="sxs-lookup"><span data-stu-id="571a6-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="571a6-156">Lista separada por vírgulas de colunas da datatable: especificar Olá toouse de nomes de coluna na nova tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="571a6-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="571a6-157">Olá nomes de coluna podem ser diferentes da saudação aqueles no conjunto de dados de origem hello, mas você deve listar Olá o mesmo número de colunas aqui que você definir para a tabela de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="571a6-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="571a6-158">Número de linhas gravadas por operação do SQL Azure: você pode configurar Olá número de linhas que são gravados tooa banco de dados SQL em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="571a6-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="571a6-159">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="571a6-159">Step 3</span></span>
1. <span data-ttu-id="571a6-160">Execute o teste de saudação clicando em execução em tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="571a6-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="571a6-161">Quando termina de experiência hello, todos os módulos terá tooindicate uma marca de seleção verde que eles foi concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="571a6-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="571a6-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="571a6-162">Next steps</span></span>
<span data-ttu-id="571a6-163">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="571a6-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
