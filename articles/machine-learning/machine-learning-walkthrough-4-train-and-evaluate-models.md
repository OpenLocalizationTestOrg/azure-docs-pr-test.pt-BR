---
title: "Etapa 4: Treinar e avaliar modelos de análise preditiva Olá | Microsoft Docs"
description: "Etapa 4 do hello desenvolver um passo a passo de solução de previsão: trem, classificar e avaliar vários modelos no estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="7e979-103">Etapa 4 do passo a passo: Treinar e avaliar modelos de análise preditiva Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="7e979-104">Este tópico contém a quarta etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="7e979-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="7e979-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="7e979-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="7e979-106">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="7e979-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="7e979-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="7e979-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="7e979-108">**Treinar e avaliar modelos Olá**</span><span class="sxs-lookup"><span data-stu-id="7e979-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="7e979-109">Implantar o serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="7e979-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="7e979-110">Acessar o serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="7e979-111">Um dos benefícios de saudação do estúdio de aprendizado de máquina do Azure para criar modelos de aprendizado de máquina é Olá capacidade tootry mais de um tipo de modelo de cada vez em uma única experiência e comparar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="7e979-112">Esse tipo de experimentação ajuda você a encontrar a melhor solução de saudação para o seu problema.</span><span class="sxs-lookup"><span data-stu-id="7e979-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="7e979-113">Experiência de saudação que desenvolve neste passo a passo, vamos criar dois tipos diferentes de modelos e, em seguida, compare seu toodecide resultados pontuação qual algoritmo queremos toouse em nossa experiência final.</span><span class="sxs-lookup"><span data-stu-id="7e979-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="7e979-114">Existem diversos modelos dentre os quais podemos escolher.</span><span class="sxs-lookup"><span data-stu-id="7e979-114">There are various models we could choose from.</span></span> <span data-ttu-id="7e979-115">modelos de saudação toosee disponíveis, expanda Olá **aprendizado de máquina** nó na paleta de módulo Olá e, em seguida, expanda **inicializar modelo** e Olá nós abaixo dela.</span><span class="sxs-lookup"><span data-stu-id="7e979-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="7e979-116">Para fins de saudação desse teste, estamos selecionará Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] (SVM) e hello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulos.</span><span class="sxs-lookup"><span data-stu-id="7e979-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="7e979-117">Ajuda tooget decidir qual algoritmo de aprendizado de máquina melhor atende às problema específico de saudação estiver tentando toosolve, consulte [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="7e979-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="7e979-118">Treinar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-118">Train hello models</span></span>

<span data-ttu-id="7e979-119">Vamos adicionar os dois Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo e [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo neste experiência.</span><span class="sxs-lookup"><span data-stu-id="7e979-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="7e979-120">Árvore de decisão aumentada em duas classes</span><span class="sxs-lookup"><span data-stu-id="7e979-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="7e979-121">Primeiro, vamos configurar o modelo de árvore de decisão ampliada de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="7e979-122">Localize Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo na paleta de módulo hello e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="7e979-123">Localize Olá [treinar modelo] [ train-model] módulo, arraste-o para a tela hello e, em seguida, conecte a saída de saudação do hello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree]porta de entrada de saudação à esquerda do módulo toohello [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="7e979-124">Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico de Olá, e [treinar modelo] [ train-model] usa dados de treinamento modelo de saudação tootrain.</span><span class="sxs-lookup"><span data-stu-id="7e979-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="7e979-125">Conecte a saída à esquerda Olá da esquerda Olá [Executar Script R] [ execute-r-script] porta de saudação de entrada do módulo toohello direito [treinar modelo] [ train-model] módulo (nós decidir em [etapa 3](machine-learning-walkthrough-3-create-new-experiment.md) desses dados passo a passo toouse hello proveniente Olá lado esquerdo de módulo de dividir dados Olá para treinamento).</span><span class="sxs-lookup"><span data-stu-id="7e979-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7e979-126">Não é necessário duas entradas hello e uma das saídas de saudação do hello [Executar Script R] [ execute-r-script] módulo para esse teste, portanto, pode deixá-los desanexada.</span><span class="sxs-lookup"><span data-stu-id="7e979-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="7e979-127">Esta parte da experiência de saudação agora tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="7e979-127">This portion of hello experiment now looks something like this:</span></span>  

![Treinando um modelo][1]

<span data-ttu-id="7e979-129">Agora precisamos Olá tootell [treinar modelo] [ train-model] que desejamos que o valor de risco de crédito Olá modelo toopredict saudação do módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="7e979-130">Selecione Olá [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="7e979-131">Em Olá **propriedades** painel, clique em **seletor de coluna iniciar**.</span><span class="sxs-lookup"><span data-stu-id="7e979-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="7e979-132">Em Olá **selecionar uma única coluna** caixa de diálogo, digite "risco de crédito" no campo de pesquisa de saudação em **colunas disponíveis**, selecione "Risco de crédito" abaixo e clique botão de seta para a direita da saudação ( **>** ) toomove muito "crédito risco"**colunas selecionadas**.</span><span class="sxs-lookup"><span data-stu-id="7e979-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Selecionar coluna de risco de crédito Olá para o módulo treinar modelo de saudação][0]

3. <span data-ttu-id="7e979-134">Clique em Olá **Okey** marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="7e979-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="7e979-135">Computador de vetor de suporte de duas classes</span><span class="sxs-lookup"><span data-stu-id="7e979-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="7e979-136">Em seguida, configuramos o modelo SVM hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="7e979-137">Primeiro, uma pequena explicação sobre o SVM.</span><span class="sxs-lookup"><span data-stu-id="7e979-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="7e979-138">Árvores de decisão aumentadas funcionam bem com recursos de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="7e979-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="7e979-139">No entanto, desde que o módulo SVM hello gera um classificador linear, o modelo de saudação que ele gera tem erro de teste melhor hello quando todos os recursos numéricos tem Olá mesma escala.</span><span class="sxs-lookup"><span data-stu-id="7e979-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="7e979-140">tooconvert numérico todos os recursos toohello mesmo dimensionar, usamos uma transformação de "Tanh" (com hello [normalizar dados] [ normalize-data] módulo).</span><span class="sxs-lookup"><span data-stu-id="7e979-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="7e979-141">Isso transforma os números em intervalo Olá [0,1].</span><span class="sxs-lookup"><span data-stu-id="7e979-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="7e979-142">módulo SVM Olá converte os recursos de toocategorical de recursos de cadeia de caracteres e, em seguida, de toobinary 0/1, portanto, não precisa toomanually transformar os recursos de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7e979-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="7e979-143">Além disso, nós não desejamos tootransform Olá risco de crédito coluna (21) - ele for numérico, mas é valor Olá nós estiver treinamento Olá toopredict de modelo, por isso, precisamos tooleave-lo sozinho.</span><span class="sxs-lookup"><span data-stu-id="7e979-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="7e979-144">tooset o modelo de SVM hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e979-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="7e979-145">Localize Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo na paleta de módulo hello e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="7e979-146">Saudação de atalho [treinar modelo] [ train-model] módulo, selecione **cópia**e, em seguida, clique com botão direito tela hello e selecione **colar**.</span><span class="sxs-lookup"><span data-stu-id="7e979-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="7e979-147">Olá cópia da saudação [treinar modelo] [ train-model] módulo tem Olá mesmo seleção de coluna como Olá original.</span><span class="sxs-lookup"><span data-stu-id="7e979-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="7e979-148">Conecte a saída de saudação do hello [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] toohello do módulo à esquerda a porta de entrada de saudação segundo [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="7e979-149">Localize Olá [normalizar dados] [ normalize-data] módulo e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="7e979-150">Conecte a saída à esquerda Olá da esquerda Olá [Executar Script R] [ execute-r-script] entrada do módulo toohello deste módulo (Observe que Olá a porta de saída de um módulo pode ser conectado toomore que um outro módulo).</span><span class="sxs-lookup"><span data-stu-id="7e979-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="7e979-151">Conectar-se a saudação à esquerda a porta de saída de hello [normalizar dados] [ normalize-data] toohello do módulo à direita de entrada porta Olá segundo [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="7e979-152">Esta parte de nosso teste deve se parecer um pouco com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7e979-152">This portion of our experiment should now look something like this:</span></span>  

![Modelo de segundo de saudação do treinamento][2]  

<span data-ttu-id="7e979-154">Configurar Olá [normalizar dados] [ normalize-data] módulo:</span><span class="sxs-lookup"><span data-stu-id="7e979-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="7e979-155">Clique em Olá tooselect [normalizar dados] [ normalize-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="7e979-156">Em Olá **propriedades** painel, selecione **Tanh** para Olá **método de transformação** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7e979-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="7e979-157">Clique em **seletor de coluna iniciar**, não selecione "Nenhum colunas" para **começa com**, selecione **incluir** no hello primeiro menu suspenso, selecione **tipo de coluna**Olá segundo menu suspenso e selecione **numérico** na lista suspensa de terceiro hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="7e979-158">Especifica que todos os hello colunas numéricas (e somente numérico) são transformadas.</span><span class="sxs-lookup"><span data-stu-id="7e979-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="7e979-159">Clique em Olá toohello de sinal de adição (+) à direita dessa linha - isso cria uma linha de listas suspensas.</span><span class="sxs-lookup"><span data-stu-id="7e979-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="7e979-160">Selecione **excluir** no hello primeiro menu suspenso, selecione **nomes de coluna** Olá segundo menu suspenso e digite "Risco de crédito" no campo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="7e979-161">Isso especifica a coluna Olá risco de crédito deve ser ignorada (precisamos toodo isso porque essa coluna é numérica e assim seria transformado se podemos não excluí-la).</span><span class="sxs-lookup"><span data-stu-id="7e979-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="7e979-162">Clique em Olá **Okey** marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="7e979-162">Click hello **OK** check mark.</span></span>  

    ![Selecione as colunas para o módulo de normalizar dados Olá][5]

<span data-ttu-id="7e979-164">Olá [normalizar dados] [ normalize-data] módulo agora é conjunto tooperform uma transformação Tanh em todas as colunas numéricas, exceto a coluna de risco de crédito hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="7e979-165">Classificar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-165">Score and evaluate hello models</span></span>

<span data-ttu-id="7e979-166">Usamos Olá dados de teste que foi separados por Olá [dividir dados] [ split] tooscore módulo nossos modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="7e979-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="7e979-167">Podemos pode comparar resultados Olá Olá dois modelos toosee que gerou resultados melhores.</span><span class="sxs-lookup"><span data-stu-id="7e979-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="7e979-168">Adicionar módulos do modelo de pontuação Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="7e979-169">Localize Olá [modelo de pontuação] [ score-model] módulo e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="7e979-170">Conecte-se a saudação [treinar modelo] [ train-model] módulo que está conectado toohello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] entrada do módulo toohello esquerda porta de saudação [modelo de pontuação] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="7e979-171">Conecte-se o direito de saudação [Executar Script R] [ execute-r-script] toohello de módulo (nossos dados de teste) à direita de entrada porta Olá [modelo de pontuação] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Módulo Modelo de Pontuação conectado][6]
   
   <span data-ttu-id="7e979-173">Olá [modelo de pontuação] [ score-model] módulo agora pode ter informações de crédito de saudação do hello dados, executados-lo por meio do modelo de saudação de teste e comparar previsões de saudação modelo hello gera com hello real risco de crédito coluna Olá dados de teste.</span><span class="sxs-lookup"><span data-stu-id="7e979-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="7e979-174">Copie e cole Olá [modelo de pontuação] [ score-model] toocreate módulo uma segunda cópia.</span><span class="sxs-lookup"><span data-stu-id="7e979-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="7e979-175">Conecte a saída de saudação do modelo SVM hello (ou seja, porta de saudação de saída de hello [treinar modelo] [ train-model] módulo que está conectado toohello [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo) toohello entrada porta Olá segundo [modelo de pontuação] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="7e979-176">Para o modelo SVM hello, temos toodo Olá mesmo dados de teste de toohello de transformação como fizemos toohello dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="7e979-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="7e979-177">Para copiar e colar Olá [normalizar dados] [ normalize-data] toocreate módulo uma segunda cópia e conecte-o direito de toohello [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="7e979-178">Conecte-se a saída à esquerda Olá Olá segundo [normalizar dados] [ normalize-data] toohello do módulo à direita de entrada porta Olá segundo [modelo de pontuação] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Os dois módulos Modelo de Pontuação estão conectados][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="7e979-180">Adicionar módulo de avaliar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="7e979-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="7e979-181">tooevaluate Olá dois resultados de pontuação e compará-los, usamos um [avaliar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="7e979-182">Localize Olá [avaliar modelo] [ evaluate-model] módulo e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="7e979-183">Conecte-se a porta de saída de saudação do hello [modelo de pontuação] [ score-model] módulo associado Olá ampliada decisão toohello de modelo de árvore à esquerda de porta de saudação entrada [avaliar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="7e979-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="7e979-184">Conectar-se a saudação outros [modelo de pontuação] [ score-model] toohello do módulo à direita de porta de entrada.</span><span class="sxs-lookup"><span data-stu-id="7e979-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Módulo Modelo de Avaliação conectado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="7e979-186">Executar teste hello e Olá resultados da verificação</span><span class="sxs-lookup"><span data-stu-id="7e979-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="7e979-187">toorun Olá experimento, clique em Olá **executar** botão abaixo tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="7e979-188">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7e979-188">It may take a few minutes.</span></span> <span data-ttu-id="7e979-189">Um indicador de rotação em cada módulo mostra que ele está em execução e, em seguida, uma marca de seleção verde mostra quando o módulo de saudação for concluído.</span><span class="sxs-lookup"><span data-stu-id="7e979-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="7e979-190">Quando todos os módulos de saudação tem uma marca de seleção, experimento Olá concluiu a execução.</span><span class="sxs-lookup"><span data-stu-id="7e979-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="7e979-191">experiência de saudação agora deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="7e979-191">hello experiment should now look something like this:</span></span>  

![Avaliando os dois modelos][3]

<span data-ttu-id="7e979-193">resultados de saudação toocheck, clique em Olá a porta de saída de hello [avaliar modelo] [ evaluate-model] módulo e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="7e979-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="7e979-194">Olá [avaliar modelo] [ evaluate-model] módulo gera um par de curvas e métricas que permitem a você resultados de saudação toocompare dois modelos de classificado Olá.</span><span class="sxs-lookup"><span data-stu-id="7e979-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="7e979-195">Você pode exibir os resultados da saudação como curvas característica de operador do receptor (ROC), precisão/recuperação curvas ou curvas de comparação de precisão.</span><span class="sxs-lookup"><span data-stu-id="7e979-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="7e979-196">Dados adicionais exibidos incluem uma matriz de confusão, cumulativos valores para a área de saudação sob a curva de saudação (AUC) e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="7e979-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="7e979-197">Você pode alterar o valor de limite de saudação pela movimentação controle deslizante à esquerda ou direita do hello e ver como ele afeta o conjunto de saudação de métricas.</span><span class="sxs-lookup"><span data-stu-id="7e979-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="7e979-198">toohello à direita do gráfico de saudação, clique em **conjunto de dados classificado** ou **classificado toocompare de conjunto de dados** toohighlight Olá associado curva e toodisplay Olá associados métricas abaixo.</span><span class="sxs-lookup"><span data-stu-id="7e979-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="7e979-199">Na legenda Olá para curvas hello, "Conjunto de dados classificado" corresponde toohello à esquerda de porta de entrada de saudação [avaliar modelo] [ evaluate-model] módulo - em nosso caso, isso é o modelo de árvore de decisão ampliada de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="7e979-200">"Toocompare de conjunto de dados de pontuação" corresponde a porta de entrada à direita do toohello - modelo SVM Olá em nosso caso.</span><span class="sxs-lookup"><span data-stu-id="7e979-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="7e979-201">Quando você clicar em uma dessas etiquetas, curva Olá para o modelo é realçada e métricas de saudação correspondentes são exibidas, conforme mostrado no gráfico a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![Curvas ROC dos modelos][4]

<span data-ttu-id="7e979-203">Ao examinar esses valores, você pode decidir qual modelo é o mais próximo toogiving que Olá resultados que você está procurando.</span><span class="sxs-lookup"><span data-stu-id="7e979-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="7e979-204">Você pode voltar e iterar em sua experiência alterando os valores de parâmetro em modelos diferentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="7e979-205">ciência Hello e arte de interpretar esses resultados e ajuste de desempenho do modelo hello está fora do escopo Olá este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7e979-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="7e979-206">Para obter ajuda adicional, você pode ler Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e979-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="7e979-207">Como tooevaluate modelo desempenho no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="7e979-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="7e979-208">Escolher parâmetros toooptimize seus algoritmos de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="7e979-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="7e979-209">Interpretar os resultados do modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7e979-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="7e979-210">Cada vez que executar o teste de saudação um registro de iteração é mantido no histórico de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e979-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="7e979-211">Você pode exibir essas iterações e retornar tooany, clicando em **exibir o histórico de execução** abaixo tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="7e979-212">Você também pode clicar em **anteriores executar** em Olá **propriedades** iteração de toohello tooreturn painel imediatamente anterior Olá um aberto.</span><span class="sxs-lookup"><span data-stu-id="7e979-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="7e979-213">Você pode fazer uma cópia de qualquer iteração de sua experiência clicando **salvar AS** abaixo tela hello.</span><span class="sxs-lookup"><span data-stu-id="7e979-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="7e979-214">Use a experiência de saudação **resumo** e **descrição** propriedades tookeep um registro de que você tentou seu iterações de teste.</span><span class="sxs-lookup"><span data-stu-id="7e979-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="7e979-215">Consulte [Gerenciar iterações do experimento no Machine Learning Studio do Azure](machine-learning-manage-experiment-iterations.md)para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="7e979-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="7e979-216">**Em seguida: [implantar Olá web service](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="7e979-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
