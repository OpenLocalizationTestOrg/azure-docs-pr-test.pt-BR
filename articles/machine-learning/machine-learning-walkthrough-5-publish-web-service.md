---
title: "Etapa 5: Implantar o serviço de web de aprendizado de máquina Olá | Microsoft Docs"
description: "Etapa 5 da saudação desenvolver um passo a passo de solução de previsão: implantar um experimento de previsão no estúdio de aprendizado de máquina como um serviço web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="30256-103">Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="30256-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="30256-104">Isso é a quinta etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="30256-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="30256-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="30256-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="30256-106">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="30256-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="30256-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="30256-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="30256-108">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="30256-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="30256-109">**Implantar o serviço web de saudação**</span><span class="sxs-lookup"><span data-stu-id="30256-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="30256-110">Serviço de acesso a saudação da web</span><span class="sxs-lookup"><span data-stu-id="30256-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="30256-111">toogive outros toouse uma chance Olá desenvolvemos neste passo a passo do modelo de previsão, é possível implantá-lo como um serviço web no Azure.</span><span class="sxs-lookup"><span data-stu-id="30256-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="30256-112">Ponto toothis vamos Estive testando com nosso modelo de treinamento.</span><span class="sxs-lookup"><span data-stu-id="30256-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="30256-113">Mas serviço Olá implantado não vai toodo treinamento - será toogenerate novas previsões pela entrada do usuário Olá com base em nosso modelo de pontuação.</span><span class="sxs-lookup"><span data-stu-id="30256-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="30256-114">Por isso vamos toodo tooconvert alguma preparação isso experiências de um ***treinamento*** experimentar tooa ***previsão*** experiências.</span><span class="sxs-lookup"><span data-stu-id="30256-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="30256-115">Esse é um processo de três etapas:</span><span class="sxs-lookup"><span data-stu-id="30256-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="30256-116">Remova um dos modelos de saudação</span><span class="sxs-lookup"><span data-stu-id="30256-116">Remove one of hello models</span></span>
2. <span data-ttu-id="30256-117">Converter Olá *experiência de treinamento* criamos em um *experimento preditivo*</span><span class="sxs-lookup"><span data-stu-id="30256-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="30256-118">Implantar a experiência de previsão hello como um serviço web</span><span class="sxs-lookup"><span data-stu-id="30256-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="30256-119">Remova um dos modelos de saudação</span><span class="sxs-lookup"><span data-stu-id="30256-119">Remove one of hello models</span></span>

<span data-ttu-id="30256-120">Primeiro, precisamos tootrim esse teste para baixo um pouco.</span><span class="sxs-lookup"><span data-stu-id="30256-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="30256-121">No momento, temos dois modelos diferentes no experimento hello, mas só queremos toouse um modelo quando for implantada isso como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="30256-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="30256-122">Digamos que decidimos esse modelo de árvore Olá ampliada melhor do que o modelo SVM Olá executada.</span><span class="sxs-lookup"><span data-stu-id="30256-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="30256-123">Olá primeira coisa toodo é remover Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo e Olá módulos que foram usados para treinar a ele.</span><span class="sxs-lookup"><span data-stu-id="30256-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="30256-124">Convém toomake uma cópia do experimento Olá primeiro clicando **Salvar como** final Olá Olá experimentar tela.</span><span class="sxs-lookup"><span data-stu-id="30256-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="30256-125">Precisamos Olá toodelete seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="30256-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="30256-126">[Computador de Vetor de Suporte de Duas Classes][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="30256-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="30256-127">[Treinar modelo] [ train-model] e [modelo de pontuação] [ score-model] módulos que estavam conectado tooit</span><span class="sxs-lookup"><span data-stu-id="30256-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="30256-128">[Normalizar Dados][normalize-data] (ambos)</span><span class="sxs-lookup"><span data-stu-id="30256-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="30256-129">[Avaliar modelo] [ evaluate-model] (porque terminamos avaliar modelos Olá)</span><span class="sxs-lookup"><span data-stu-id="30256-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="30256-130">Selecione cada módulo e pressione a tecla Delete de saudação ou módulo de saudação do botão direito do mouse e selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="30256-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Remover modelo SVM de saudação][3a]

<span data-ttu-id="30256-132">Nosso modelo agora deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="30256-132">Our model should now look something like this:</span></span>

![Remover modelo SVM de saudação][3]

<span data-ttu-id="30256-134">Agora estamos pronto toodeploy modelo usando Olá [árvore de decisão ampliada de duas classes][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="30256-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="30256-135">Converter a experiência de previsão do hello treinamento experimento tooa</span><span class="sxs-lookup"><span data-stu-id="30256-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="30256-136">tooget esse modelo pronto para implantação, precisamos tooconvert essa experiência tooa previsão experiência de treinamento.</span><span class="sxs-lookup"><span data-stu-id="30256-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="30256-137">Isso envolve três etapas:</span><span class="sxs-lookup"><span data-stu-id="30256-137">This involves three steps:</span></span>

1. <span data-ttu-id="30256-138">Salvar modelo Olá podemos tiver treinado e, em seguida, substituir os módulos de treinamento</span><span class="sxs-lookup"><span data-stu-id="30256-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="30256-139">Trim Olá experimento tooremove os módulos que foram necessário apenas para treinamento</span><span class="sxs-lookup"><span data-stu-id="30256-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="30256-140">Definir onde o serviço web de saudação aceitará entrada e onde ele gera a saída de hello</span><span class="sxs-lookup"><span data-stu-id="30256-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="30256-141">Podemos fazer isso manualmente, mas felizmente todas as três etapas podem ser realizadas clicando **configurar o serviço Web** na parte inferior da saudação da tela de experimento hello (e selecionando Olá **previsão Web Service** opção).</span><span class="sxs-lookup"><span data-stu-id="30256-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="30256-142">Se você quiser obter mais detalhes sobre o que acontece quando você converte um tooa de experiência de treinamento previsão experimentar, consulte [como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="30256-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="30256-143">Quando você clica em **Configurar Serviço Web**, várias coisas acontecem:</span><span class="sxs-lookup"><span data-stu-id="30256-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="30256-144">modelo treinado Hello é convertido tooa único **treinado** módulo e armazenados em Olá módulo paleta toohello esquerda da saudação experimentar tela (você pode encontrar em **modelos treinados**)</span><span class="sxs-lookup"><span data-stu-id="30256-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="30256-145">Os módulos que foram usados para o treinamento são removidos; especificamente:</span><span class="sxs-lookup"><span data-stu-id="30256-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="30256-146">[Árvore de Decisão Aumentada em Duas Classes][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="30256-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="30256-147">[Modelo de Treinamento][train-model]</span><span class="sxs-lookup"><span data-stu-id="30256-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="30256-148">[Dados Divididos][split]</span><span class="sxs-lookup"><span data-stu-id="30256-148">[Split Data][split]</span></span>
  * <span data-ttu-id="30256-149">Olá segundo [Executar Script R] [ execute-r-script] módulo que foi usado para dados de teste</span><span class="sxs-lookup"><span data-stu-id="30256-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="30256-150">treinado Olá salvada é adicionado no experimento Olá</span><span class="sxs-lookup"><span data-stu-id="30256-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="30256-151">**Entrada de serviço de Web** e **Web de saída do serviço** módulos são adicionados (eles identificam onde os dados do usuário Olá entrará modelo hello e quais dados são retornados, quando o serviço web de saudação é acessado)</span><span class="sxs-lookup"><span data-stu-id="30256-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="30256-152">Você pode ver que experimento Olá é salvo em duas partes em guias que foram adicionados na parte superior de saudação da tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="30256-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="30256-153">Olá experiência de treinamento original é na guia Olá **experiência de treinamento**, e Olá recém-criado experimento previsão está sob **experimento previsão**.</span><span class="sxs-lookup"><span data-stu-id="30256-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="30256-154">experiência de previsão Olá é hello um que nós implantará como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="30256-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="30256-155">Precisamos de uma etapa adicional tootake com esse teste específico.</span><span class="sxs-lookup"><span data-stu-id="30256-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="30256-156">Adicionamos dois [Executar Script R] [ execute-r-script] tooprovide módulos uma ponderação função toohello dados.</span><span class="sxs-lookup"><span data-stu-id="30256-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="30256-157">Que estavam apenas uma rodada que é necessário para treinamento e teste, vamos esses módulos no modelo final hello.</span><span class="sxs-lookup"><span data-stu-id="30256-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="30256-158">O estúdio de aprendizado de máquina removido um [Executar Script R] [ execute-r-script] módulo quando ele removido Olá [divisão] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="30256-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="30256-159">Agora podemos remover Olá outros e conecte-se [Editor de metadados] [ metadata-editor] diretamente muito[modelo de pontuação][score-model].</span><span class="sxs-lookup"><span data-stu-id="30256-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="30256-160">Agora o teste deve se parecer como isto:</span><span class="sxs-lookup"><span data-stu-id="30256-160">Our experiment should now look like this:</span></span>  

![Pontuação treinado Olá][4]  

> [!NOTE]
> <span data-ttu-id="30256-162">Você deve estar se perguntando por que foi deixado dataset de dados de cartão de crédito alemão UCI Olá experimento previsão hello.</span><span class="sxs-lookup"><span data-stu-id="30256-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="30256-163">serviço de saudação será tooscore Olá dados usuário, não Olá conjunto de dados original, então por que deixam Olá conjunto de dados original no modelo de saudação?</span><span class="sxs-lookup"><span data-stu-id="30256-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="30256-164">É verdade que serviço Olá não precisa Olá dados originais de cartão de crédito.</span><span class="sxs-lookup"><span data-stu-id="30256-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="30256-165">Mas é necessário esquema Olá para os dados, que inclui informações como o número de colunas há e quais colunas são numéricas.</span><span class="sxs-lookup"><span data-stu-id="30256-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="30256-166">Essas informações de esquema são necessário toointerpret Olá dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="30256-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="30256-167">Vamos deixar esses componentes conectados de modo que hello pontuação módulo tem esquema de conjunto de dados hello quando Olá serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="30256-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="30256-168">dados de saudação não for usados, apenas o esquema hello.</span><span class="sxs-lookup"><span data-stu-id="30256-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="30256-169">Executar teste Olá pela última vez (clique **executar**.) Tooverify que Olá modelo ainda está funcionando, clique em saída Olá Olá [modelo de pontuação] [ score-model] módulo e selecione **exibir resultados**.</span><span class="sxs-lookup"><span data-stu-id="30256-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="30256-170">Você pode ver dados originais Olá são exibidos, juntamente com o valor de risco de crédito hello ("rótulos de pontuação") e hello pontuação valor de probabilidade ("classificado probabilidades".)</span><span class="sxs-lookup"><span data-stu-id="30256-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="30256-171">Implantar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="30256-171">Deploy hello web service</span></span>
<span data-ttu-id="30256-172">Você pode implantar Olá experiência como um serviço de web clássico ou como um novo serviço da web com base no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="30256-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="30256-173">Implantar como serviço Web clássico</span><span class="sxs-lookup"><span data-stu-id="30256-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="30256-174">toodeploy um clássico web serviço derivado de nossa experiência, clique em **implantar o serviço da Web** abaixo Olá tela e selecione **implantar o serviço Web [clássico]**.</span><span class="sxs-lookup"><span data-stu-id="30256-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="30256-175">Estúdio de aprendizado de máquina implanta Olá experiência como um serviço web e vai toohello painel para o serviço web.</span><span class="sxs-lookup"><span data-stu-id="30256-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="30256-176">Nessa página, você pode retornar toohello experimento (**exibir instantâneo** ou **exibir mais recente**) e executar um teste simple de serviço da web de saudação (consulte **testar Olá web serviço** abaixo).</span><span class="sxs-lookup"><span data-stu-id="30256-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="30256-177">Há também informações para a criação de aplicativos que podem acessar o serviço web da saudação (mais detalhes na próxima etapa Olá deste passo a passo).</span><span class="sxs-lookup"><span data-stu-id="30256-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Painel de serviço Web][6]

<span data-ttu-id="30256-179">Você pode configurar o serviço de saudação clicando Olá **configuração** guia. Aqui você pode modificar o nome do serviço hello (é Olá determinado nome de teste por padrão) e dê a ele uma descrição.</span><span class="sxs-lookup"><span data-stu-id="30256-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="30256-180">Você também pode fornecer mais rótulos amigáveis para Olá dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="30256-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Configurar o serviço web de saudação][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="30256-182">Implantar como um novo serviço Web</span><span class="sxs-lookup"><span data-stu-id="30256-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="30256-183">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você está implantando Olá serviço da web.</span><span class="sxs-lookup"><span data-stu-id="30256-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="30256-184">Para obter mais informações, consulte [gerenciar um serviço web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="30256-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="30256-185">toodeploy um novo serviço web derivado da nossa experiência:</span><span class="sxs-lookup"><span data-stu-id="30256-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="30256-186">Clique em **implantar o serviço da Web** abaixo Olá tela e selecione **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="30256-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="30256-187">O estúdio de aprendizado de máquina transfere dos serviços web de aprendizado de máquina do Azure toohello **implantar experimento** página.</span><span class="sxs-lookup"><span data-stu-id="30256-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="30256-188">Insira um nome para o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="30256-189">Para **plano de preço**, você pode selecionar um plano de preços existente ou selecione "Criar novo" e dê Olá novo plano de um nome e uma opção de plano mensal Olá select.</span><span class="sxs-lookup"><span data-stu-id="30256-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="30256-190">plano de saudação camadas padrão toohello planos para sua região padrão e o serviço web é implantado toothat região.</span><span class="sxs-lookup"><span data-stu-id="30256-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="30256-191">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="30256-191">Click **Deploy**.</span></span>

<span data-ttu-id="30256-192">Depois de alguns minutos, Olá **Quickstart** página para seu serviço da web é aberta.</span><span class="sxs-lookup"><span data-stu-id="30256-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="30256-193">Você pode configurar o serviço de saudação clicando Olá **configurar** guia. Aqui você pode modificar o serviço Olá title e dê a ele uma descrição.</span><span class="sxs-lookup"><span data-stu-id="30256-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="30256-194">Olá tootest serviço da web, clique em Olá **teste** guia (consulte **testar Olá web serviço** abaixo).</span><span class="sxs-lookup"><span data-stu-id="30256-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="30256-195">Para obter informações sobre como criar aplicativos que podem acessar o serviço web de saudação, clique em Olá **consumir** guia (a próxima etapa Olá neste passo a passo entrará em mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="30256-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="30256-196">Você pode atualizar o serviço web de saudação depois que você implantou.</span><span class="sxs-lookup"><span data-stu-id="30256-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="30256-197">Por exemplo, se você quiser toochange seu modelo, você pode editar experiência de treinamento hello, ajustar os parâmetros de modelo Olá e clique em **implantar o serviço da Web**, selecionando **implantar o serviço Web [clássico]** ou  **Implantar o serviço da Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="30256-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="30256-198">Quando você implanta o experimento Olá novamente, ele substitui o serviço da web hello, usando o modelo atualizado.</span><span class="sxs-lookup"><span data-stu-id="30256-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="30256-199">Testar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="30256-199">Test hello web service</span></span>

<span data-ttu-id="30256-200">Quando o serviço web de saudação é acessado, dados do usuário Olá entram por Olá **Web serviço entrada** módulo onde ele passou toohello [modelo de pontuação] [ score-model] módulo e classificados.</span><span class="sxs-lookup"><span data-stu-id="30256-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="30256-201">forma Olá que configuramos o experimento previsão Olá, o modelo Olá espera dados no hello mesmo formato que o dataset de risco de crédito original hello.</span><span class="sxs-lookup"><span data-stu-id="30256-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="30256-202">resultados de saudação são retornados toohello usuário do serviço web de saudação por meio de saudação **Web de saída do serviço** módulo.</span><span class="sxs-lookup"><span data-stu-id="30256-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="30256-203">forma Olá Olá previsão experimento configurado, Olá inteira, temos os resultados de saudação [modelo de pontuação] [ score-model] módulo são retornados.</span><span class="sxs-lookup"><span data-stu-id="30256-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="30256-204">Isso inclui todos os dados de entrada hello mais valor de risco de crédito hello e hello pontuação de probabilidade.</span><span class="sxs-lookup"><span data-stu-id="30256-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="30256-205">Mas você pode retornar algo diferente se você quiser - por exemplo, você poderia retornar apenas Olá valor de risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="30256-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="30256-206">toodo, inserir um [colunas do projeto] [ project-columns] módulo entre [modelo de pontuação] [ score-model] e hello **Webdesaídadeserviço** tooeliminate colunas indesejadas Olá tooreturn de serviço web.</span><span class="sxs-lookup"><span data-stu-id="30256-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="30256-207">Você pode testar uma web clássico de serviço em **estúdio de aprendizado de máquina** ou em Olá **serviços de Web de aprendizado de máquina do Azure** portal.</span><span class="sxs-lookup"><span data-stu-id="30256-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="30256-208">Você pode testar um novo serviço da web apenas no hello **serviços de Web do aprendizado de máquina** portal.</span><span class="sxs-lookup"><span data-stu-id="30256-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="30256-209">Durante o teste no portal de serviços de Web de aprendizado de máquina do Azure Olá, você pode fazer com que o portal Olá criar dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta.</span><span class="sxs-lookup"><span data-stu-id="30256-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="30256-210">Em Olá **configurar** , selecione "Sim" para **habilitado de dados de exemplo?**.</span><span class="sxs-lookup"><span data-stu-id="30256-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="30256-211">Quando você abre a guia Olá Olá solicitação-resposta **teste** página, portal Olá preenche os dados de exemplo obtidos Olá original dataset de risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="30256-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="30256-212">Testar um serviço Web Clássico</span><span class="sxs-lookup"><span data-stu-id="30256-212">Test a Classic web service</span></span>

<span data-ttu-id="30256-213">Você pode testar um serviço da web clássico no estúdio de aprendizado de máquina ou no portal de serviços de Web do aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="30256-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="30256-214">Testar no Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="30256-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="30256-215">Em Olá **painel** para serviço web de saudação, clique em Olá **teste** botão em **ponto de extremidade padrão**.</span><span class="sxs-lookup"><span data-stu-id="30256-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="30256-216">Uma caixa de diálogo será exibida e solicita dados de entrada hello para serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="30256-217">Esses é Olá mesmas colunas que eram exibidos no dataset de risco de crédito original hello.</span><span class="sxs-lookup"><span data-stu-id="30256-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="30256-218">Insira um conjunto de dados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="30256-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="30256-219">Teste no portal de serviços de Web do aprendizado de máquina Olá</span><span class="sxs-lookup"><span data-stu-id="30256-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="30256-220">Em Olá **painel** para serviço web de saudação, clique em Olá **visualização de teste** link em **ponto de extremidade padrão**.</span><span class="sxs-lookup"><span data-stu-id="30256-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="30256-221">página de teste de saudação no portal de serviços de Web de aprendizado de máquina do Azure Olá para o ponto de extremidade de serviço de web hello abre e solicita dados de entrada hello para serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="30256-222">Esses é Olá mesmas colunas que eram exibidos no dataset de risco de crédito original hello.</span><span class="sxs-lookup"><span data-stu-id="30256-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="30256-223">Clique em **Solicitação-Resposta**.</span><span class="sxs-lookup"><span data-stu-id="30256-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="30256-224">Testar um novo serviço Web</span><span class="sxs-lookup"><span data-stu-id="30256-224">Test a New web service</span></span>

<span data-ttu-id="30256-225">Você pode testar um novo serviço da web apenas no portal de serviços de Web do aprendizado de máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="30256-226">Em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net/quickstart) portal, clique **teste** na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="30256-227">Olá **teste** página abre e você pode inserir dados para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="30256-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="30256-228">campos de entrada Hello exibidos correspondem toohello colunas que eram exibidos no dataset de risco de crédito original hello.</span><span class="sxs-lookup"><span data-stu-id="30256-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="30256-229">Insira um conjunto de dados e clique em **Testar solicitação-resposta**.</span><span class="sxs-lookup"><span data-stu-id="30256-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="30256-230">Olá resultados de teste de saudação são exibidos no lado direito de saudação da página Olá na coluna de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="30256-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="30256-231">Gerenciar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="30256-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="30256-232">Gerenciar um serviço da web clássico no hello portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="30256-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="30256-233">Depois de implantar seu serviço da web clássico, você pode gerenciá-lo de saudação [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="30256-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="30256-234">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="30256-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="30256-235">No painel de serviços do Microsoft Azure hello, clique em **APRENDIZADO de máquina**</span><span class="sxs-lookup"><span data-stu-id="30256-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="30256-236">Clique no espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="30256-236">Click your workspace</span></span>
4. <span data-ttu-id="30256-237">Clique em Olá **serviços Web** guia</span><span class="sxs-lookup"><span data-stu-id="30256-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="30256-238">Clique em Olá web service criamos</span><span class="sxs-lookup"><span data-stu-id="30256-238">Click hello web service we created</span></span>
6. <span data-ttu-id="30256-239">Clique em ponto de extremidade do hello "padrão"</span><span class="sxs-lookup"><span data-stu-id="30256-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="30256-240">A partir daqui, você pode fazer coisas como monitorar como o serviço web de saudação está fazendo e fazer ajustes de desempenho, alterando o serviço de saudação quantas chamadas simultâneas pode manipular.</span><span class="sxs-lookup"><span data-stu-id="30256-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="30256-241">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="30256-241">For more details, see:</span></span>

* [<span data-ttu-id="30256-242">Criando pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="30256-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="30256-243">Dimensionando serviço Web</span><span class="sxs-lookup"><span data-stu-id="30256-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="30256-244">Gerenciar um clássico ou um novo serviço da web no portal de serviços de Web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="30256-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="30256-245">Assim que tiver implantado o serviço web, se clássico ou novo, você pode gerenciá-lo de saudação [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="30256-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="30256-246">desempenho de saudação toomonitor do serviço web:</span><span class="sxs-lookup"><span data-stu-id="30256-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="30256-247">Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) portal</span><span class="sxs-lookup"><span data-stu-id="30256-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="30256-248">Clique em **Serviços Web**</span><span class="sxs-lookup"><span data-stu-id="30256-248">Click **Web services**</span></span>
3. <span data-ttu-id="30256-249">Clique no seu serviço Web</span><span class="sxs-lookup"><span data-stu-id="30256-249">Click your web service</span></span>
4. <span data-ttu-id="30256-250">Clique em Olá **painel**</span><span class="sxs-lookup"><span data-stu-id="30256-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="30256-251">**Em seguida: [acessar o serviço web Olá](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="30256-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
