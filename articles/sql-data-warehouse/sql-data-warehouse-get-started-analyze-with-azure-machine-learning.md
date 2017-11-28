---
title: Analisar dados com o Azure Machine Learning | Microsoft Docs
description: "Use o Azure Machine Learning para compilar um modelo de aprendizado de máquina preditivo com base nos dados armazenados no SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="3400e-103">Analisar dados com o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3400e-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3400e-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="3400e-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="3400e-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="3400e-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="3400e-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3400e-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="3400e-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="3400e-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="3400e-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="3400e-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="3400e-109">Este tutorial usa o Azure Machine Learning para compilar um modelo de aprendizado de máquina preditivo com base nos dados armazenados no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="3400e-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3400e-110">Especificamente, isso compila uma campanha de marketing direcionado da Adventure Works, uma loja de bicicletas, prevendo se um cliente tem probabilidade de comprar uma bicicleta ou não.</span><span class="sxs-lookup"><span data-stu-id="3400e-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3400e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3400e-111">Prerequisites</span></span>
<span data-ttu-id="3400e-112">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="3400e-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="3400e-113">Um SQL Data Warehouse pré-carregado com os dados de exemplo do AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3400e-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="3400e-114">Para provisionar isso, consulte [Criar um SQL Data Warehouse][Create a SQL Data Warehouse] e opte por carregar os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3400e-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="3400e-115">Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="3400e-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="3400e-116">1. Obter os dados</span><span class="sxs-lookup"><span data-stu-id="3400e-116">1. Get the data</span></span>
<span data-ttu-id="3400e-117">Os dados estão na exibição dbo.vTargetMail no banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3400e-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="3400e-118">Para ler esses dados:</span><span class="sxs-lookup"><span data-stu-id="3400e-118">To read this data:</span></span>

1. <span data-ttu-id="3400e-119">Entre no [Azure Machine Learning Studio][Azure Machine Learning studio] e clique em Meus Testes.</span><span class="sxs-lookup"><span data-stu-id="3400e-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="3400e-120">Clique em **+NOVO** e selecione **Teste em Branco**.</span><span class="sxs-lookup"><span data-stu-id="3400e-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="3400e-121">Insira um nome para o seu teste: Marketing Direcionado.</span><span class="sxs-lookup"><span data-stu-id="3400e-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="3400e-122">Arraste o módulo **Leitor** do painel de módulos na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="3400e-123">Especifique os detalhes do seu banco de dados do SQL Data Warehouse no painel Propriedades.</span><span class="sxs-lookup"><span data-stu-id="3400e-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="3400e-124">Especifique a **consulta** do banco de dados para ler os dados de interesse.</span><span class="sxs-lookup"><span data-stu-id="3400e-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="3400e-125">Execute o teste clicando em **Executar** na tela do teste.</span><span class="sxs-lookup"><span data-stu-id="3400e-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="3400e-126">![Executar o teste][1]</span><span class="sxs-lookup"><span data-stu-id="3400e-126">![Run the experiment][1]</span></span>

<span data-ttu-id="3400e-127">Após o teste terminar de ser executado com êxito, clique na porta de saída na parte inferior do módulo Leitor e selecione **Visualizar** para ver os dados importados.</span><span class="sxs-lookup"><span data-stu-id="3400e-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="3400e-128">![Exibir dados importados][3]</span><span class="sxs-lookup"><span data-stu-id="3400e-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="3400e-129">2. Limpar os dados</span><span class="sxs-lookup"><span data-stu-id="3400e-129">2. Clean the data</span></span>
<span data-ttu-id="3400e-130">Para limpar os dados, remova algumas colunas que não são relevantes para o modelo.</span><span class="sxs-lookup"><span data-stu-id="3400e-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="3400e-131">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="3400e-131">To do this:</span></span>

1. <span data-ttu-id="3400e-132">Arraste o módulo **Colunas do Projeto** na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="3400e-133">Clique em **Iniciar seletor de colunas** no painel Propriedades para especificar quais colunas você deseja remover.</span><span class="sxs-lookup"><span data-stu-id="3400e-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="3400e-134">![Colunas do Projeto][4]</span><span class="sxs-lookup"><span data-stu-id="3400e-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="3400e-135">Exclua duas colunas: CustomerAlternateKey e GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="3400e-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="3400e-136">![Remover colunas desnecessárias][5]</span><span class="sxs-lookup"><span data-stu-id="3400e-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="3400e-137">3. Compilar o modelo</span><span class="sxs-lookup"><span data-stu-id="3400e-137">3. Build the model</span></span>
<span data-ttu-id="3400e-138">Dividiremos os dados 80-20: 80% para treinar um modelo de aprendizado de máquina e 20% para testar o modelo.</span><span class="sxs-lookup"><span data-stu-id="3400e-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="3400e-139">Usaremos os algoritmos de “Duas Classes” para esse problema de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="3400e-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="3400e-140">Arraste o módulo **Divisão** na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="3400e-141">Insira 0.8 para a Fração de linhas no primeiro conjunto de dados de saída no painel Propriedades.</span><span class="sxs-lookup"><span data-stu-id="3400e-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="3400e-142">![Dividir os dados em conjuntos de treinamento e teste][6]</span><span class="sxs-lookup"><span data-stu-id="3400e-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="3400e-143">Arraste o módulo **Árvore de Decisão Aumentada de duas classes** na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="3400e-144">Arraste o módulo **Modelo de Treinamento** na tela e especifique as entradas.</span><span class="sxs-lookup"><span data-stu-id="3400e-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="3400e-145">Depois, clique em **Iniciar seletor de coluna** no painel de Propriedades.</span><span class="sxs-lookup"><span data-stu-id="3400e-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="3400e-146">Primeira entrada: algoritmo de ML.</span><span class="sxs-lookup"><span data-stu-id="3400e-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="3400e-147">Segunda entrada: dados para treinar o algoritmo.</span><span class="sxs-lookup"><span data-stu-id="3400e-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="3400e-148">![Conectar o módulo Treinar Modelo][7]</span><span class="sxs-lookup"><span data-stu-id="3400e-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="3400e-149">Selecione a coluna **BikeBuyer** como a coluna a ser prevista.</span><span class="sxs-lookup"><span data-stu-id="3400e-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="3400e-150">![Selecionar a Coluna a prever][8]</span><span class="sxs-lookup"><span data-stu-id="3400e-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="3400e-151">4. Pontuar o modelo</span><span class="sxs-lookup"><span data-stu-id="3400e-151">4. Score the model</span></span>
<span data-ttu-id="3400e-152">Agora, testaremos o desempenho do modelo nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3400e-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="3400e-153">Vamos comparar o algoritmo de nossa escolha com um algoritmo diferente para ver que tem um desempenho melhor.</span><span class="sxs-lookup"><span data-stu-id="3400e-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="3400e-154">Arraste o módulo **Modelo de Pontuação** na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="3400e-155">Primeira entrada: modelo treinado Segunda entrada: dados de teste ![Pontuar o modelo][9]</span><span class="sxs-lookup"><span data-stu-id="3400e-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="3400e-156">Arraste o **Computador de Ponto de Bayes de Duas Classes** na tela de teste.</span><span class="sxs-lookup"><span data-stu-id="3400e-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="3400e-157">Vamos comparar o desempenho desse algoritmo em comparação com a Árvore de Decisão Aumentada de Duas Classes.</span><span class="sxs-lookup"><span data-stu-id="3400e-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="3400e-158">Copie e cole os módulos Modelo de Treinamento e Modelo de Pontuação na tela.</span><span class="sxs-lookup"><span data-stu-id="3400e-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="3400e-159">Arraste o módulo **Avaliar Modelo** na tela para comparar os dois algoritmos.</span><span class="sxs-lookup"><span data-stu-id="3400e-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="3400e-160">**Execute** o teste.</span><span class="sxs-lookup"><span data-stu-id="3400e-160">**Run** the experiment.</span></span>
   <span data-ttu-id="3400e-161">![Executar o teste][10]</span><span class="sxs-lookup"><span data-stu-id="3400e-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="3400e-162">Clique na porta de saída na parte inferior do módulo Avaliar Modelo e clique em Visualizar.</span><span class="sxs-lookup"><span data-stu-id="3400e-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="3400e-163">![Visualizar os resultados de avaliação][11]</span><span class="sxs-lookup"><span data-stu-id="3400e-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="3400e-164">As métricas fornecidas são a curva ROC, o diagrama de comparação de precisão e recolhimento e a curva de comparação de precisão.</span><span class="sxs-lookup"><span data-stu-id="3400e-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="3400e-165">Ao examinar essas métricas, podemos ver que o primeiro modelo teve um desempenho melhor do que o segundo.</span><span class="sxs-lookup"><span data-stu-id="3400e-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="3400e-166">Para ver o que o primeiro modelo previu, clique na porta de saída do Modelo de Pontuação e clique em Visualizar.</span><span class="sxs-lookup"><span data-stu-id="3400e-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="3400e-167">![Visualizar os resultados da pontuação][12]</span><span class="sxs-lookup"><span data-stu-id="3400e-167">![Visualize score results][12]</span></span>

<span data-ttu-id="3400e-168">Você verá duas ou mais colunas adicionadas ao seu conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3400e-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="3400e-169">Probabilidades Pontuadas: a probabilidade de que um cliente é um comprador de bicicleta.</span><span class="sxs-lookup"><span data-stu-id="3400e-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="3400e-170">Rótulos Pontuados: a classificação feita pelo modelo – comprador de bicicleta (1) ou não (0).</span><span class="sxs-lookup"><span data-stu-id="3400e-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="3400e-171">Esse limite de probabilidade para a rotulagem é definido como 50% e pode ser ajustado.</span><span class="sxs-lookup"><span data-stu-id="3400e-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="3400e-172">Ao comparar a coluna BikeBuyer (real) com os Rótulos Pontuados (previsão), é possível ver o desempenho do modelo.</span><span class="sxs-lookup"><span data-stu-id="3400e-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="3400e-173">Como as próximas etapas, você pode usar esse modelo para fazer previsões para novos clientes e publicar esse modelo como um serviço Web ou gravar os resultados de volta no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3400e-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3400e-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3400e-174">Next steps</span></span>
<span data-ttu-id="3400e-175">Para saber mais sobre a criação de modelos de aprendizado de máquina de previsão, consulte [Introdução ao Machine Learning no Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="3400e-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
