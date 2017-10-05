---
title: 'Etapa 2: carregar dados em um experimento do Machine Learning | Microsoft Docs'
description: "Etapa 2 - desenvolver um passo a passo de solução de previsão: carregamento armazenado de dados públicos no Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="5a66a-103">Etapa 2 do passo a passo: carregar dados existentes no experimento de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a66a-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="5a66a-104">Esta é a segunda etapa do passo a passo, [Desenvolver uma solução de análise preditiva com o Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="5a66a-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="5a66a-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="5a66a-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. <span data-ttu-id="5a66a-106">**Carregar dados existentes**</span><span class="sxs-lookup"><span data-stu-id="5a66a-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="5a66a-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="5a66a-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="5a66a-108">Treinar e avaliar os modelos</span><span class="sxs-lookup"><span data-stu-id="5a66a-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="5a66a-109">Implantar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="5a66a-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="5a66a-110">Acessar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="5a66a-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="5a66a-111">Para desenvolver um modelo preditivo para risco de crédito, precisamos de dados que podemos usar para treinar e testar o modelo.</span><span class="sxs-lookup"><span data-stu-id="5a66a-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="5a66a-112">Para este passo a passo, usaremos o “Conjunto de Dados Statlog (Dados de Crédito Alemão) UCI” do repositório UC Irvine Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a66a-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="5a66a-113">Você pode encontrá-lo aqui: </span><span class="sxs-lookup"><span data-stu-id="5a66a-113">You can find it here:</span></span>  
<span data-ttu-id="5a66a-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="5a66a-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="5a66a-115">Usaremos o arquivo chamado **german.data**.</span><span class="sxs-lookup"><span data-stu-id="5a66a-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="5a66a-116">Baixe esse arquivo em sua unidade de disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="5a66a-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="5a66a-117">O conjunto de dados **german.data** contém linhas de 20 variáveis para 1000 candidatos antigos de crédito.</span><span class="sxs-lookup"><span data-stu-id="5a66a-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="5a66a-118">Essas 20 variáveis representam o conjunto de recursos do conjunto de dados (o *vetor de recurso*), que fornece características de identificação para cada candidato de crédito.</span><span class="sxs-lookup"><span data-stu-id="5a66a-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="5a66a-119">Uma coluna adicional em cada linha representa o risco de crédito calculado do candidato, com 700 candidatos identificados como um risco de crédito baixo e 300 como um alto risco.</span><span class="sxs-lookup"><span data-stu-id="5a66a-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="5a66a-120">O website do UCI fornece uma descrição dos atributos do vetor de recurso para esses dados.</span><span class="sxs-lookup"><span data-stu-id="5a66a-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="5a66a-121">Isso inclui informações financeiras, histórico de crédito, status de emprego e informações pessoais.</span><span class="sxs-lookup"><span data-stu-id="5a66a-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="5a66a-122">Para cada candidato, foi dada uma classificação binária indicando se são um risco baixo ou alto de crédito.</span><span class="sxs-lookup"><span data-stu-id="5a66a-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="5a66a-123">Usaremos estes dados para treinar um modelo analítico preditivo.</span><span class="sxs-lookup"><span data-stu-id="5a66a-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="5a66a-124">Quando tivermos concluído, nosso modelo deverá ser capaz de aceitar um vetor de recurso para uma nova pessoa e prever se ela é um risco de crédito alto ou baixo.</span><span class="sxs-lookup"><span data-stu-id="5a66a-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="5a66a-125">Aqui está uma mudança interessante.</span><span class="sxs-lookup"><span data-stu-id="5a66a-125">Here's an interesting twist.</span></span> <span data-ttu-id="5a66a-126">A descrição do conjunto de dados no site do UCI menciona quanto custa se classificarmos incorretamente o risco de crédito de uma pessoa.</span><span class="sxs-lookup"><span data-stu-id="5a66a-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="5a66a-127">Se o modelo previr um alto risco de crédito para alguém que, de fato, é de baixo risco de crédito, o modelo terá feito uma classificação incorreta.</span><span class="sxs-lookup"><span data-stu-id="5a66a-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="5a66a-128">Porém, a classificação incorreta inversa é cinco vezes mais onerosa para a instituição financeira: se o modelo previr um baixo risco de crédito para alguém que, de fato, é de alto risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="5a66a-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="5a66a-129">Dessa forma, queremos treinar nosso modelo para que o custo desse último tipo de classificação incorreta seja cinco vezes mais alto do que o outro tipo de classificação incorreta.</span><span class="sxs-lookup"><span data-stu-id="5a66a-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="5a66a-130">Uma maneira simples de fazer isso ao treinar o modelo em nossa experiência é duplicando (cinco vezes) essas entradas que representam alguém com um alto risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="5a66a-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="5a66a-131">Assim, se o modelo classificar incorretamente alguém como de baixo risco de crédito, quando ele for de fato de risco alto, o modelo fará a mesma classificação incorreta cinco vezes, uma para cada duplicação.</span><span class="sxs-lookup"><span data-stu-id="5a66a-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="5a66a-132">Isso aumentará o custo deste erro nos resultados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="5a66a-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="5a66a-133">Converter o formato do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="5a66a-133">Convert the dataset format</span></span>
<span data-ttu-id="5a66a-134">O conjunto de dados original usa um formato separado por espaço em branco.</span><span class="sxs-lookup"><span data-stu-id="5a66a-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="5a66a-135">O Machine Learning Studio trabalha melhor com um arquivo CSV (de valores separados por vírgula). Então, converteremos o conjunto de dados substituindo espaços por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="5a66a-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="5a66a-136">Há muitas maneiras de converter esses dados.</span><span class="sxs-lookup"><span data-stu-id="5a66a-136">There are many ways to convert this data.</span></span> <span data-ttu-id="5a66a-137">Uma maneira é usar o seguinte comando do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a66a-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="5a66a-138">Outra maneira é usar o comando Unix sed:</span><span class="sxs-lookup"><span data-stu-id="5a66a-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="5a66a-139">Em ambos os casos, criamos uma versão separada por vírgulas dos dados em um arquivo chamado **german.csv** que usaremos em nosso teste.</span><span class="sxs-lookup"><span data-stu-id="5a66a-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="5a66a-140">Carregar o conjunto de dados para o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5a66a-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="5a66a-141">Depois que os dados tiverem sido convertidos no formato CSV, precisaremos carregá-los no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a66a-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="5a66a-142">Abra a home page do Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="5a66a-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="5a66a-143">Clique em ![Menu][1] no canto superior esquerdo da janela, clique em **Azure Machine Learning**, selecione **Estúdio** e entre.</span><span class="sxs-lookup"><span data-stu-id="5a66a-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="5a66a-144">Clique em **+NOVO** na parte inferior da janela.</span><span class="sxs-lookup"><span data-stu-id="5a66a-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="5a66a-145">Selecione **CONJUNTO DE DADOS**.</span><span class="sxs-lookup"><span data-stu-id="5a66a-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="5a66a-146">Selecione **DO ARQUIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="5a66a-146">Select **FROM LOCAL FILE**.</span></span>

    ![Adicionar um conjunto de dados de um arquivo local][2]

6. <span data-ttu-id="5a66a-148">No diálogo **Carregar um novo conjunto de dados**, clique em **Pesquisar** e localize o arquivo **german.csv** criado.</span><span class="sxs-lookup"><span data-stu-id="5a66a-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="5a66a-149">Insira um nome para o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="5a66a-149">Enter a name for the dataset.</span></span> <span data-ttu-id="5a66a-150">Para este passo a passo, vamos chamá-lo de "Dados do cartão de crédito alemão UCI".</span><span class="sxs-lookup"><span data-stu-id="5a66a-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="5a66a-151">Para tipo de dados, selecione **Arquivo CSV genérico sem cabeçalho (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="5a66a-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="5a66a-152">Inclua uma descrição se desejar.</span><span class="sxs-lookup"><span data-stu-id="5a66a-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="5a66a-153">Clique na marca de seleção **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a66a-153">Click the **OK** check mark.</span></span>  

    ![Carregar o conjunto de dados][3]

<span data-ttu-id="5a66a-155">Isso carrega os dados em um módulo de conjunto de dados que podemos usar em um experimento.</span><span class="sxs-lookup"><span data-stu-id="5a66a-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="5a66a-156">É possível gerenciar conjuntos de dados que você carregou no Estúdio clicando na guia **CONJUNTOS DE DADOS** à esquerda da janela do Estúdio.</span><span class="sxs-lookup"><span data-stu-id="5a66a-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Gerenciar conjuntos de dados][4]

<span data-ttu-id="5a66a-158">Para obter mais informações sobre como importar outros tipos de dados para um teste, consulte [Importar dados de treinamento para o Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="5a66a-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="5a66a-159">**A seguir: [criar um novo experimento](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="5a66a-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
