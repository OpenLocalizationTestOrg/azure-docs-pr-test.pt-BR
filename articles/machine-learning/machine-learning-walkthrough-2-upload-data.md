---
title: 'Etapa 2: carregar dados em um experimento do Machine Learning | Microsoft Docs'
description: "Etapa 2 de saudação desenvolver um passo a passo de solução de previsão: carregamento armazenado dados públicos no estúdio de aprendizado de máquina do Azure."
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
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="a22a2-103">Etapa 2 do passo a passo: carregar dados existentes no experimento de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a22a2-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="a22a2-104">Esta é a segunda etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a22a2-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="a22a2-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="a22a2-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. <span data-ttu-id="a22a2-106">**Carregar dados existentes**</span><span class="sxs-lookup"><span data-stu-id="a22a2-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="a22a2-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="a22a2-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a22a2-108">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="a22a2-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a22a2-109">Implantar o serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="a22a2-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a22a2-110">Acessar o serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="a22a2-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a22a2-111">toodevelop um modelo de previsão para o risco de crédito, precisamos de dados que podemos usar tootrain e, em seguida, testar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a22a2-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="a22a2-112">Para este passo a passo, usaremos hello "Conjunto de dados do UCI Statlog (dados de crédito alemão)" do repositório de aprendizado de máquina do UC Irvine hello.</span><span class="sxs-lookup"><span data-stu-id="a22a2-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="a22a2-113">Você pode encontrá-lo aqui: </span><span class="sxs-lookup"><span data-stu-id="a22a2-113">You can find it here:</span></span>  
<span data-ttu-id="a22a2-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="a22a2-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="a22a2-115">Vamos usar arquivo hello chamado **german.data**.</span><span class="sxs-lookup"><span data-stu-id="a22a2-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="a22a2-116">Baixe este arquivo tooyour de disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="a22a2-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="a22a2-117">Olá **german.data** conjunto de dados contém linhas de 20 variáveis para 1000 candidatos anteriores de crédito.</span><span class="sxs-lookup"><span data-stu-id="a22a2-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="a22a2-118">Essas 20 variáveis representam o conjunto de saudação do conjunto de recursos (Olá *vetor de recurso*), que fornece as características de identifica para cada candidato de crédito.</span><span class="sxs-lookup"><span data-stu-id="a22a2-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="a22a2-119">Uma coluna adicional em cada linha representa um risco de crédito calculado do candidato Olá, com 700 candidatos identificados como um risco de crédito baixa e 300 como um alto risco.</span><span class="sxs-lookup"><span data-stu-id="a22a2-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="a22a2-120">site UCI Olá fornece uma descrição dos atributos de saudação do vetor de recurso Olá para esses dados.</span><span class="sxs-lookup"><span data-stu-id="a22a2-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="a22a2-121">Isso inclui informações financeiras, histórico de crédito, status de emprego e informações pessoais.</span><span class="sxs-lookup"><span data-stu-id="a22a2-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="a22a2-122">Para cada candidato, foi dada uma classificação binária indicando se são um risco baixo ou alto de crédito.</span><span class="sxs-lookup"><span data-stu-id="a22a2-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="a22a2-123">Vamos usar essa tootrain dados um modelo de análise de previsão.</span><span class="sxs-lookup"><span data-stu-id="a22a2-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="a22a2-124">Quando terminamos, nosso modelo deve ser capaz de tooaccept um vetor de recurso para um novo indivíduo e prever se ele é um risco de crédito baixa ou alta.</span><span class="sxs-lookup"><span data-stu-id="a22a2-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="a22a2-125">Aqui está uma mudança interessante.</span><span class="sxs-lookup"><span data-stu-id="a22a2-125">Here's an interesting twist.</span></span> <span data-ttu-id="a22a2-126">Olá descrição do conjunto de dados de saudação em Olá UCI site menciona o custo se nós misclassify o risco de crédito de uma pessoa.</span><span class="sxs-lookup"><span data-stu-id="a22a2-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="a22a2-127">Se o modelo de saudação prevê um risco de crédito alta para alguém que é realmente um risco de crédito baixa, modelo Olá fez uma misclassification.</span><span class="sxs-lookup"><span data-stu-id="a22a2-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="a22a2-128">Mas misclassification inversa Olá é cinco vezes mais cara instituição financeira de toohello: se o modelo de saudação prevê um risco de crédito baixa para alguém que é realmente um risco de crédito alta.</span><span class="sxs-lookup"><span data-stu-id="a22a2-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="a22a2-129">Assim, desejamos tootrain nosso modelo para que o custo de saudação este último tipo de misclassification é cinco vezes maior do que classifique Olá outra maneira.</span><span class="sxs-lookup"><span data-stu-id="a22a2-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="a22a2-130">Toodo de uma maneira simples isso ao modelo Olá em nossa experiência de treinamento é duplicando (cinco vezes) dessas entradas que representam uma pessoa com um risco de crédito alta.</span><span class="sxs-lookup"><span data-stu-id="a22a2-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="a22a2-131">Em seguida, se o modelo de saudação classificar incorretamente alguém como um risco de crédito baixa quando eles são, na verdade, um alto risco, Olá modelo faz esse mesmo misclassification cinco vezes, uma vez para cada linha duplicada.</span><span class="sxs-lookup"><span data-stu-id="a22a2-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="a22a2-132">Isso aumentará o custo de saudação do erro nos resultados de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="a22a2-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="a22a2-133">Converter o formato de conjunto de dados Olá</span><span class="sxs-lookup"><span data-stu-id="a22a2-133">Convert hello dataset format</span></span>
<span data-ttu-id="a22a2-134">saudação de conjunto de dados original usa um formato de separadas por espaço em branco.</span><span class="sxs-lookup"><span data-stu-id="a22a2-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="a22a2-135">Estúdio de aprendizado de máquina funciona melhor com um arquivo de valores separados por vírgulas (CSV), portanto converteremos Olá conjunto de dados, substituindo espaços por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="a22a2-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="a22a2-136">Há muitos tooconvert de maneiras esses dados.</span><span class="sxs-lookup"><span data-stu-id="a22a2-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="a22a2-137">É uma maneira usando Olá comando do Windows PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="a22a2-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="a22a2-138">Outra maneira é usando o comando de sed Olá Unix:</span><span class="sxs-lookup"><span data-stu-id="a22a2-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="a22a2-139">Em ambos os casos, criamos uma versão separada por vírgulas dos dados de saudação em um arquivo chamado **german.csv** que podemos usar nossa experiência.</span><span class="sxs-lookup"><span data-stu-id="a22a2-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="a22a2-140">Carregar Olá dataset tooMachine estúdio de aprendizado</span><span class="sxs-lookup"><span data-stu-id="a22a2-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="a22a2-141">Depois que dados saudação tem sido convertido tooCSV formato, precisamos tooupload no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a22a2-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="a22a2-142">Home page do hello abrir estúdio de aprendizado de máquina ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="a22a2-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="a22a2-143">Clique em menu Olá ![Menu][1] no canto superior esquerdo de saudação da janela de saudação, clique em **aprendizado de máquina do Azure**, selecione **Studio**e entre.</span><span class="sxs-lookup"><span data-stu-id="a22a2-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="a22a2-144">Clique em **+ novo** na parte inferior da saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a22a2-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="a22a2-145">Selecione **CONJUNTO DE DADOS**.</span><span class="sxs-lookup"><span data-stu-id="a22a2-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="a22a2-146">Selecione **DO ARQUIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="a22a2-146">Select **FROM LOCAL FILE**.</span></span>

    ![Adicionar um conjunto de dados de um arquivo local][2]

6. <span data-ttu-id="a22a2-148">Em Olá **carregar um novo conjunto de dados** caixa de diálogo, clique em **procurar** e localize Olá **german.csv** arquivo que você criou.</span><span class="sxs-lookup"><span data-stu-id="a22a2-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="a22a2-149">Insira um nome para o conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a22a2-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="a22a2-150">Para este passo a passo, vamos chamá-lo de "Dados do cartão de crédito alemão UCI".</span><span class="sxs-lookup"><span data-stu-id="a22a2-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="a22a2-151">Para tipo de dados, selecione **Arquivo CSV genérico sem cabeçalho (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="a22a2-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="a22a2-152">Inclua uma descrição se desejar.</span><span class="sxs-lookup"><span data-stu-id="a22a2-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="a22a2-153">Clique em Olá **Okey** marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="a22a2-153">Click hello **OK** check mark.</span></span>  

    ![Carregar o conjunto de dados Olá][3]

<span data-ttu-id="a22a2-155">Isso carrega dados saudação em um módulo de conjunto de dados que podemos usar em um experimento.</span><span class="sxs-lookup"><span data-stu-id="a22a2-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="a22a2-156">Você pode gerenciar conjuntos de dados que você carregou tooStudio clicando Olá **conjuntos de dados** toohello guia à esquerda da janela do Studio hello.</span><span class="sxs-lookup"><span data-stu-id="a22a2-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Gerenciar conjuntos de dados][4]

<span data-ttu-id="a22a2-158">Para obter mais informações sobre como importar outros tipos de dados para um teste, consulte [Importar dados de treinamento para o Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="a22a2-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="a22a2-159">**A seguir: [criar um novo experimento](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="a22a2-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
