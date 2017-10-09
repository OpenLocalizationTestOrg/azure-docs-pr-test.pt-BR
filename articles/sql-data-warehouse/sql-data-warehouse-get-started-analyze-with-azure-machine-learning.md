---
title: "dados de aaaAnalyze com o aprendizado de máquina do Azure | Microsoft Docs"
description: "Use um modelo com base nos dados armazenados no Azure SQL Data Warehouse de aprendizado de máquina previsão de toobuild de aprendizado de máquina do Azure."
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
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="a5e44-103">Analisar dados com o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a5e44-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5e44-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="a5e44-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="a5e44-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="a5e44-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="a5e44-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5e44-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="a5e44-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a5e44-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="a5e44-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="a5e44-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="a5e44-109">Este tutorial usa um modelo com base nos dados armazenados no Azure SQL Data Warehouse de aprendizado de máquina previsão de toobuild de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a5e44-110">Especificamente, isso cria uma campanha de marketing para a Adventure Works, loja de bicicletas hello, por prever se um cliente é provavelmente toobuy uma bicicleta ou não.</span><span class="sxs-lookup"><span data-stu-id="a5e44-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a5e44-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5e44-111">Prerequisites</span></span>
<span data-ttu-id="a5e44-112">toostep este tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a5e44-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="a5e44-113">Um SQL Data Warehouse pré-carregado com os dados de exemplo do AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="a5e44-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="a5e44-114">tooprovision isso, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha dados de exemplo hello tooload.</span><span class="sxs-lookup"><span data-stu-id="a5e44-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="a5e44-115">Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="a5e44-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="a5e44-116">1. Obter dados de saudação</span><span class="sxs-lookup"><span data-stu-id="a5e44-116">1. Get hello data</span></span>
<span data-ttu-id="a5e44-117">dados saudação estão no modo de dbo.vTargetMail de saudação no banco de dados do hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="a5e44-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="a5e44-118">tooread esses dados:</span><span class="sxs-lookup"><span data-stu-id="a5e44-118">tooread this data:</span></span>

1. <span data-ttu-id="a5e44-119">Entre no [Azure Machine Learning Studio][Azure Machine Learning studio] e clique em Meus Testes.</span><span class="sxs-lookup"><span data-stu-id="a5e44-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="a5e44-120">Clique em **+NOVO** e selecione **Teste em Branco**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="a5e44-121">Insira um nome para o seu teste: Marketing Direcionado.</span><span class="sxs-lookup"><span data-stu-id="a5e44-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="a5e44-122">Saudação de arrastar **leitor** módulo no painel de módulos de saudação na tela hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="a5e44-123">Especifique os detalhes de saudação do banco de dados SQL Data Warehouse no painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="a5e44-124">Especifique o banco de dados de saudação **consulta** tooread dados de saudação de interesse.</span><span class="sxs-lookup"><span data-stu-id="a5e44-124">Specify hello database **query** tooread hello data of interest.</span></span>

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

<span data-ttu-id="a5e44-125">Executar o teste de saudação clicando **executar** em tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="a5e44-126">![Executar teste Olá][1]</span><span class="sxs-lookup"><span data-stu-id="a5e44-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="a5e44-127">Após a conclusão da experiência de saudação em execução com êxito, clique Olá a porta de saída na parte inferior de saudação do módulo do leitor de saudação e selecione **visualizar** toosee Olá importou dados.</span><span class="sxs-lookup"><span data-stu-id="a5e44-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="a5e44-128">![Exibir dados importados][3]</span><span class="sxs-lookup"><span data-stu-id="a5e44-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="a5e44-129">2. Dados saudação normal</span><span class="sxs-lookup"><span data-stu-id="a5e44-129">2. Clean hello data</span></span>
<span data-ttu-id="a5e44-130">dados de saudação tooclean, remova algumas colunas que não são relevantes para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="a5e44-131">toodo isso:</span><span class="sxs-lookup"><span data-stu-id="a5e44-131">toodo this:</span></span>

1. <span data-ttu-id="a5e44-132">Saudação de arrastar **colunas do projeto** módulo na tela hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="a5e44-133">Clique em **seletor de coluna iniciar** no toospecify de painel de propriedades Olá quais colunas você deseja toodrop.</span><span class="sxs-lookup"><span data-stu-id="a5e44-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="a5e44-134">![Colunas do Projeto][4]</span><span class="sxs-lookup"><span data-stu-id="a5e44-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="a5e44-135">Exclua duas colunas: CustomerAlternateKey e GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="a5e44-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="a5e44-136">![Remover colunas desnecessárias][5]</span><span class="sxs-lookup"><span data-stu-id="a5e44-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="a5e44-137">3. Criar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="a5e44-137">3. Build hello model</span></span>
<span data-ttu-id="a5e44-138">Podemos dividirá Olá dados 80-20: 80% tootrain um modelo de aprendizado de máquina e 20% tootest Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="a5e44-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="a5e44-139">Faremos usa algoritmos de "Duas classes" Olá para esse problema de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="a5e44-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="a5e44-140">Saudação de arrastar **divisão** módulo na tela hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="a5e44-141">Insira 0,8 da fração de linhas no primeiro conjunto de saída hello, no painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="a5e44-142">![Dividir os dados em conjuntos de treinamento e teste][6]</span><span class="sxs-lookup"><span data-stu-id="a5e44-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="a5e44-143">Saudação de arrastar **árvore de decisão ampliada de duas classes** módulo na tela hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="a5e44-144">Saudação de arrastar **treinar modelo** módulo em Olá tela e especificar Olá entradas.</span><span class="sxs-lookup"><span data-stu-id="a5e44-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="a5e44-145">Em seguida, clique em **seletor de coluna iniciar** no painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="a5e44-146">Primeira entrada: algoritmo de ML.</span><span class="sxs-lookup"><span data-stu-id="a5e44-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="a5e44-147">Segundo de entrada: algoritmo de saudação tootrain dados em.</span><span class="sxs-lookup"><span data-stu-id="a5e44-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="a5e44-148">![Conecte-se o módulo treinar modelo de saudação][7]</span><span class="sxs-lookup"><span data-stu-id="a5e44-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="a5e44-149">Selecione Olá **BikeBuyer** coluna como Olá toopredict de coluna.</span><span class="sxs-lookup"><span data-stu-id="a5e44-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="a5e44-150">![Selecione a coluna toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="a5e44-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="a5e44-151">4. Modelo de saudação de pontuação</span><span class="sxs-lookup"><span data-stu-id="a5e44-151">4. Score hello model</span></span>
<span data-ttu-id="a5e44-152">Agora, vamos testar como o modelo de saudação executa em dados de teste.</span><span class="sxs-lookup"><span data-stu-id="a5e44-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="a5e44-153">Podemos comparará algoritmo Olá nossa escolha com toosee um algoritmo diferente que tem um desempenho melhor.</span><span class="sxs-lookup"><span data-stu-id="a5e44-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="a5e44-154">Arraste **modelo de pontuação** módulo na tela hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="a5e44-155">Primeiro de entrada: treinado modelo segunda entrada: dados de teste ![modelo Olá de pontuação][9]</span><span class="sxs-lookup"><span data-stu-id="a5e44-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="a5e44-156">Saudação de arrastar **máquina do ponto de Bayes de duas classes** na tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="a5e44-157">Podemos comparará como esse algoritmo executa na comparação toohello árvore de decisão ampliada de duas classes.</span><span class="sxs-lookup"><span data-stu-id="a5e44-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="a5e44-158">Copiar e colar Olá módulos treinar modelo e o modelo de classificação no hello tela.</span><span class="sxs-lookup"><span data-stu-id="a5e44-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="a5e44-159">Saudação de arrastar **avaliar modelo** módulo em algoritmos de saudação dois Olá tela toocompare.</span><span class="sxs-lookup"><span data-stu-id="a5e44-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="a5e44-160">**Executar** Olá experimento.</span><span class="sxs-lookup"><span data-stu-id="a5e44-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="a5e44-161">![Executar teste Olá][10]</span><span class="sxs-lookup"><span data-stu-id="a5e44-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="a5e44-162">Clique em Olá a porta de saída na parte inferior de Olá Olá avaliar do módulo do modelo e clique em Visualizar.</span><span class="sxs-lookup"><span data-stu-id="a5e44-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="a5e44-163">![Visualizar os resultados de avaliação][11]</span><span class="sxs-lookup"><span data-stu-id="a5e44-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="a5e44-164">métricas de saudação fornecidas são curva de ROC hello, lembre-se de precisão de diagrama e levante curva.</span><span class="sxs-lookup"><span data-stu-id="a5e44-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="a5e44-165">Observando essas métricas, podemos ver esse modelo primeiro Olá executado melhor do que Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="a5e44-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="a5e44-166">toolook em Olá que Olá primeiro modelo previsto, clique na porta de saída do hello modelo de classificação e clique em Visualizar.</span><span class="sxs-lookup"><span data-stu-id="a5e44-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="a5e44-167">![Visualizar os resultados da pontuação][12]</span><span class="sxs-lookup"><span data-stu-id="a5e44-167">![Visualize score results][12]</span></span>

<span data-ttu-id="a5e44-168">Você verá que mais duas colunas adicionadas tooyour conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="a5e44-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="a5e44-169">Das probabilidades pontuadas: probabilidade de saudação que um cliente é um comprador de bicicletas.</span><span class="sxs-lookup"><span data-stu-id="a5e44-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="a5e44-170">Rótulos de pontuação: Olá classificação feita pelo modelo hello – comprador de bicicleta (1) ou não (0).</span><span class="sxs-lookup"><span data-stu-id="a5e44-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="a5e44-171">Esse limite de probabilidade para rotular é definida too50% e pode ser ajustado.</span><span class="sxs-lookup"><span data-stu-id="a5e44-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="a5e44-172">Comparando coluna Olá comprador de bicicleta (real) com rótulos de pontuação de saudação (previsão), você pode ver como o modelo Olá executou.</span><span class="sxs-lookup"><span data-stu-id="a5e44-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="a5e44-173">Próximas etapas, você pode usar previsões de toomake este modelo para novos clientes e publicar este modelo como um serviço web ou gravar resultados back tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a5e44-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5e44-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5e44-174">Next steps</span></span>
<span data-ttu-id="a5e44-175">toolearn mais sobre como criar modelos de aprendizado de máquina previsão consulte muito[tooMachine introdução de aprendizagem no Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e44-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

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
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
