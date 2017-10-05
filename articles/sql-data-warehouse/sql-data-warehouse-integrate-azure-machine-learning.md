---
title: Use o Azure Machine Learning com o SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="7cb9e-103">Use o Azure Machine Learning com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7cb9e-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="7cb9e-104">O Azure Machine Learning é um serviço de análise preditiva totalmente gerenciado que você pode usar para criar modelos preditivos em relação aos dados do SQL Data Warehouse e publicá-los como serviços Web prontos para consumo.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="7cb9e-105">Você pode aprender os fundamentos da análise preditiva e aprendizado de máquina lendo [Introdução ao Machine Learning no Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="7cb9e-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="7cb9e-106">Em seguida, você pode aprender a criar, treinar, pontuar e testar um modelo de aprendizado de máquina usando [Tutorial de criação de teste][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="7cb9e-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="7cb9e-107">Neste artigo, você aprenderá a fazer o seguinte usando o [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="7cb9e-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="7cb9e-108">Ler dados de seu banco de dados para criar, treinar e pontuar um modelo de previsão</span><span class="sxs-lookup"><span data-stu-id="7cb9e-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="7cb9e-109">Gravar dados em seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="7cb9e-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="7cb9e-110">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7cb9e-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="7cb9e-111">Leremos dados da tabela Produtos no banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="7cb9e-112">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="7cb9e-112">Step 1</span></span>
<span data-ttu-id="7cb9e-113">Inicie um novo experimento clicando em +NOVO na parte inferior da janela do Machine Learning Studio, selecione EXPERIMENTO e selecione Experimento em branco.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="7cb9e-114">Selecione o nome de experimento padrão na parte superior da tela e renomeie para algo significativo, por exemplo, Previsão de preço de bicicleta.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="7cb9e-115">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="7cb9e-115">Step 2</span></span>
<span data-ttu-id="7cb9e-116">Procure o módulo Leitor na paleta de conjuntos de dados e módulos à esquerda da tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="7cb9e-117">Arraste o módulo à tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="7cb9e-118">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="7cb9e-118">Step 3</span></span>
<span data-ttu-id="7cb9e-119">Selecione o módulo Leitor e preencha o painel de propriedades.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="7cb9e-120">Selecione o Banco de Dados SQL do Azure como a Fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="7cb9e-121">Nome do servidor de banco de dados: digite o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-121">Database server name: Type the server name.</span></span> <span data-ttu-id="7cb9e-122">Você pode usar o [Portal do Azure][Azure portal] para encontrar isso.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="7cb9e-123">Nome do banco de dados: digite o nome do banco de dados no servidor especificado.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="7cb9e-124">Nome de conta de usuário do servidor: digite o nome de usuário da conta que tem permissões de acesso para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="7cb9e-125">Senha de conta de usuário do servidor: forneça a senha da conta de usuário especificada.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="7cb9e-126">Aceitar qualquer certificado do servidor: use essa opção (menos segura) se desejar ignorar a revisão do certificado do site antes de ler os dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="7cb9e-127">Consulta de banco de dados: insira uma instrução SQL que descreve os dados que você deseja ler.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="7cb9e-128">Nesse caso, vamos ler dados da tabela de produto usando a consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="7cb9e-129">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="7cb9e-129">Step 4</span></span>
1. <span data-ttu-id="7cb9e-130">Execute o experimento clicando em Executar abaixo da tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="7cb9e-131">Quando o teste for concluído, o módulo Leitor terá uma marca de seleção verde para indicar que foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="7cb9e-132">Observe também o status Execução concluída no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="7cb9e-133">Para ver os dados importados, clique na porta de saída na parte inferior do conjunto de dados automóvel e selecione Visualizar.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="7cb9e-134">Crie, treine e pontue um modelo</span><span class="sxs-lookup"><span data-stu-id="7cb9e-134">Create, train and score a model</span></span>
<span data-ttu-id="7cb9e-135">Agora você pode usar esse conjunto de dados para:</span><span class="sxs-lookup"><span data-stu-id="7cb9e-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="7cb9e-136">Criar um modelo: processar dados e definir recursos</span><span class="sxs-lookup"><span data-stu-id="7cb9e-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="7cb9e-137">Treinar o modelo: escolher e aplicar um algoritmo de aprendizado</span><span class="sxs-lookup"><span data-stu-id="7cb9e-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="7cb9e-138">Pontuar e testar o modelo: prever o novo preço de uma bicicleta</span><span class="sxs-lookup"><span data-stu-id="7cb9e-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="7cb9e-139">Para saber mais sobre como criar, treinar, pontuar e testar uma modelo de aprendizado de máquina, use o [Tutorial de criação de teste][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="7cb9e-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="7cb9e-140">Grave dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="7cb9e-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7cb9e-141">Gravaremos o conjunto de resultados na tabela ProductPriceForecast no banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="7cb9e-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="7cb9e-142">Step 1</span></span>
<span data-ttu-id="7cb9e-143">Procure o módulo Gravador na paleta de conjuntos de dados e módulos à esquerda da tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="7cb9e-144">Arraste o módulo à tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="7cb9e-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="7cb9e-145">Step 2</span></span>
<span data-ttu-id="7cb9e-146">Selecione o módulo Gravador e preencha o painel de propriedades.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="7cb9e-147">Selecione o Banco de Dados do SQL Azure como o Destino de Dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="7cb9e-148">Nome do servidor de banco de dados: digite o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-148">Database server name: Type the server name.</span></span> <span data-ttu-id="7cb9e-149">Você pode usar o [Portal do Azure][Azure portal] para encontrar isso.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="7cb9e-150">Nome do banco de dados: digite o nome do banco de dados no servidor especificado.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="7cb9e-151">Nome de conta de usuário do servidor: digite o nome de usuário de uma conta que tenha permissões de gravação para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="7cb9e-152">Senha de conta de usuário do servidor: forneça a senha da conta de usuário especificada.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="7cb9e-153">Aceitar qualquer certificado de servidor (não é seguro): selecione esta opção se você não deseja exibir o certificado.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="7cb9e-154">Lista separada por vírgulas de colunas a serem salvas: forneça uma lista das colunas de conjunto de dados ou o resultado de saída.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="7cb9e-155">Nome da tabela de dados: especifique o nome da tabela de dados.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="7cb9e-156">Lista separada por vírgulas de colunas da datatable: especifique os nomes de coluna a serem usados na nova tabela.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="7cb9e-157">Os nomes de coluna podem ser diferentes do conjunto de dados de origem, mas você deve listar o mesmo número de colunas aqui que você definir para a tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="7cb9e-158">Número de linhas gravadas por operação do SQL Azure: você pode configurar o número de linhas que são gravados em um banco de dados SQL em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="7cb9e-159">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="7cb9e-159">Step 3</span></span>
1. <span data-ttu-id="7cb9e-160">Execute o experimento clicando em Executar abaixo da tela do experimento.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="7cb9e-161">Quando o experimento for concluído, todos os módulos terão uma marca de seleção verde para indicar que foram concluídos com sucesso.</span><span class="sxs-lookup"><span data-stu-id="7cb9e-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cb9e-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7cb9e-162">Next steps</span></span>
<span data-ttu-id="7cb9e-163">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="7cb9e-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
