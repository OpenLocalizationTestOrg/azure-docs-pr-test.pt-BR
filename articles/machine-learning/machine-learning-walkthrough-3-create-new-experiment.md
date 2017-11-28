---
title: 'Etapa 3: Criar um novo teste de Machine Learning | Microsoft Docs'
description: "Etapa 3 do hello desenvolver um passo a passo de solução de previsão: criar uma nova experiência de treinamento no estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="0ae35-103">Passo a passo Etapa 3: Criar um novo teste de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ae35-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="0ae35-104">Isso é a terceira etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="0ae35-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="0ae35-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="0ae35-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="0ae35-106">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="0ae35-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="0ae35-107">**Criar um novo teste**</span><span class="sxs-lookup"><span data-stu-id="0ae35-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="0ae35-108">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="0ae35-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="0ae35-109">Implantar o serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="0ae35-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="0ae35-110">Acessar o serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="0ae35-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="0ae35-111">Olá próxima etapa neste passo a passo é toocreate um experimento no estúdio de aprendizado de máquina que usa o conjunto de dados de saudação que são carregados.</span><span class="sxs-lookup"><span data-stu-id="0ae35-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="0ae35-112">No Studio, clique em **+ novo** na parte inferior da saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ae35-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="0ae35-113">Selecione **TESTE**e, em seguida, selecione "Teste em branco".</span><span class="sxs-lookup"><span data-stu-id="0ae35-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Criar um novo experimento][0]

2. <span data-ttu-id="0ae35-115">Padrão de Select Olá experimentar nome hello superior da tela hello e renomeie-a como toosomething significativo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Renomear o teste][5]
   
   > [!TIP]
   > <span data-ttu-id="0ae35-117">É uma boa prática toofill **resumo** e **descrição** para teste de saudação em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="0ae35-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="0ae35-118">Esses fornecem propriedades Olá experimento de saudação toodocument oportunidade para que qualquer pessoa que analisa-lo mais tarde compreendam suas metas e metodologia.</span><span class="sxs-lookup"><span data-stu-id="0ae35-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Propriedades de teste][6]
   > 
3. <span data-ttu-id="0ae35-120">Olá módulo paleta toohello à esquerda da tela de experimento hello, expanda **conjuntos de dados salvos**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="0ae35-121">Localizar Olá conjunto de dados criado em **Meus conjuntos de dados** e arraste-o para a tela hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="0ae35-122">Você também pode encontrar o conjunto de dados de saudação inserindo nome Olá Olá **pesquisa** caixa acima paleta hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Adicionar teste de toohello do conjunto de dados Olá][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="0ae35-124">Preparar dados Olá</span><span class="sxs-lookup"><span data-stu-id="0ae35-124">Prepare hello data</span></span>
<span data-ttu-id="0ae35-125">Você pode exibir hello as primeiras 100 linhas de dados hello e algumas informações estatísticas para Olá todo o conjunto de dados: clique Olá a porta de saída do conjunto de dados hello (Olá pequeno círculo na parte inferior da saudação) e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="0ae35-126">Porque o arquivo de dados de saudação não foi fornecido com cabeçalhos de coluna, Studio forneceu títulos genéricos (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="0ae35-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="0ae35-127">BOM títulos não são essencial toocreating um modelo, mas eles tornam mais fácil toowork com dados de saudação experimento hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="0ae35-128">Além disso, quando publicamos eventualmente esse modelo em um serviço web, cabeçalhos de saudação ajuda identificar Olá colunas toohello usuário do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ae35-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="0ae35-129">Podemos adicionar cabeçalhos de coluna usando Olá [editar metadados] [ edit-metadata] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="0ae35-130">Use Olá [editar metadados] [ edit-metadata] módulo toochange metadados associados a um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0ae35-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="0ae35-131">Nesse caso, vamos usá-lo tooprovide nomes mais amigáveis para títulos de coluna.</span><span class="sxs-lookup"><span data-stu-id="0ae35-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="0ae35-132">toouse [editar metadados][edit-metadata], você deve determinar quais toomodify colunas (nesse caso, todos eles.) Em seguida, você pode especificar Olá ação toobe executada nessas colunas (nesse caso, a alteração de cabeçalhos de coluna.)</span><span class="sxs-lookup"><span data-stu-id="0ae35-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="0ae35-133">Na paleta de módulo hello, digite "metadados" hello **pesquisa** caixa.</span><span class="sxs-lookup"><span data-stu-id="0ae35-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="0ae35-134">Olá [editar metadados] [ edit-metadata] aparece na lista de módulos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ae35-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="0ae35-135">Clique e arraste Olá [editar metadados] [ edit-metadata] módulo no hello tela e solte-o abaixo Olá de conjunto de dados são adicionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ae35-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="0ae35-136">Conectar Olá dataset toohello [editar metadados][edit-metadata]: clique Olá porta de saída do conjunto de dados hello (Olá pequeno círculo na parte inferior de saudação do conjunto de dados de saudação), arraste toohello porta de entrada de [editar metadados ] [ edit-metadata] (Olá pequeno círculo na parte superior de saudação do módulo de saudação), em seguida, solte o botão do mouse hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="0ae35-137">módulo e o conjunto de dados Olá permanecerem conectados, mesmo se você move o na tela hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="0ae35-138">experiência de saudação agora deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="0ae35-138">hello experiment should now look something like this:</span></span>  
   
   ![Adicionar Editar Metadados][1]
   
   <span data-ttu-id="0ae35-140">Olá vermelho ponto de exclamação indica que estamos ainda não definidas propriedades Olá para este módulo ainda.</span><span class="sxs-lookup"><span data-stu-id="0ae35-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="0ae35-141">Faremos isso em seguida.</span><span class="sxs-lookup"><span data-stu-id="0ae35-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0ae35-142">Você pode adicionar um módulo de tooa comentário clicando duas vezes em módulo de saudação e a inserção de texto.</span><span class="sxs-lookup"><span data-stu-id="0ae35-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="0ae35-143">Isso pode ajudá-lo a ver rapidamente quais módulo hello está fazendo sua experiência.</span><span class="sxs-lookup"><span data-stu-id="0ae35-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="0ae35-144">Nesse caso, clique duas vezes em Olá [editar metadados] [ edit-metadata] módulo e tipo hello comentário "adicionar cabeçalhos de coluna".</span><span class="sxs-lookup"><span data-stu-id="0ae35-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="0ae35-145">Clique em qualquer lugar na caixa de texto de saudação do hello tela tooclose.</span><span class="sxs-lookup"><span data-stu-id="0ae35-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="0ae35-146">toodisplay Olá comentário, clique em Olá seta para baixo no módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ae35-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Módulo Editar Metadados com comentário adicionado][8]
   > 
4. <span data-ttu-id="0ae35-148">Selecione [editar metadados][edit-metadata]e em Olá **propriedades** toohello painel à direita da tela hello, clique em **seletor de coluna iniciar**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="0ae35-149">Em Olá **selecionar colunas** caixa de diálogo, selecione todos os Olá linhas em **colunas disponíveis** e clique em > toomove-los muito**colunas selecionadas**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="0ae35-150">caixa de diálogo Olá deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0ae35-150">hello dialog should look like this:</span></span>

   ![Seletor de coluna com todas as colunas selecionadas][2]

6. <span data-ttu-id="0ae35-152">Clique em Olá **Okey** marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="0ae35-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="0ae35-153">Em Olá **propriedades** painel, procure Olá **novos nomes de coluna** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0ae35-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="0ae35-154">Neste campo, digite uma lista de nomes de colunas de 21 Olá no conjunto de dados hello, separados por vírgulas e na ordem de coluna.</span><span class="sxs-lookup"><span data-stu-id="0ae35-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="0ae35-155">É possível obter nomes de colunas de saudação na documentação do conjunto de dados Olá no site UCI hello, ou para sua conveniência você pode copiar e colar Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ae35-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="0ae35-156">Painel de propriedades de saudação tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0ae35-156">hello Properties pane looks like this:</span></span>
   
   ![Propriedades de Editar Metadados][3]

> [!TIP]
> <span data-ttu-id="0ae35-158">Se você quiser títulos de coluna tooverify hello, execute o teste de saudação (clique **executar** abaixo de tela de experimento Olá).</span><span class="sxs-lookup"><span data-stu-id="0ae35-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="0ae35-159">Quando ela terminar a execução (uma marca de seleção verde é exibida em [editar metadados][edit-metadata]), clique em Olá porta de saída de hello [editar metadados] [ edit-metadata] módulo e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="0ae35-160">Você pode exibir a saída de saudação de qualquer módulo no hello progresso da mesmo maneira tooview Olá de dados de saudação por meio de experiência de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ae35-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="0ae35-161">Criar conjuntos de dados de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="0ae35-161">Create training and test datasets</span></span>
<span data-ttu-id="0ae35-162">Precisamos de alguns tootrain Olá modelo dados e alguns tootest-lo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="0ae35-163">Na próxima etapa do experimento Olá Olá, dividiremos Olá conjunto de dados em dois conjuntos de dados separados: um para treinar nosso modelo e o outro para testá-lo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="0ae35-164">toodo isso, usamos Olá [dividir dados] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="0ae35-165">Localize Olá [dividir dados] [ split] módulo, arraste-o para a tela hello e conectá-lo toohello [editar metadados] [ edit-metadata] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="0ae35-166">Por padrão, a taxa de divisão de saudação é 0,5 e hello **divisão aleatória** parâmetro está definido.</span><span class="sxs-lookup"><span data-stu-id="0ae35-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="0ae35-167">Isso significa que meia aleatória de dados Olá saída através de uma porta de saudação [dividir dados] [ split] módulo e meia a saudação outros.</span><span class="sxs-lookup"><span data-stu-id="0ae35-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="0ae35-168">Você pode ajustar esses parâmetros, bem como Olá **semente aleatória** parâmetro, Olá toochange divididos entre dados de teste e treinamento.</span><span class="sxs-lookup"><span data-stu-id="0ae35-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="0ae35-169">Neste exemplo, deixaremos como está.</span><span class="sxs-lookup"><span data-stu-id="0ae35-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0ae35-170">Olá propriedade **fração de linhas na Olá primeiro conjunto de dados de saída** determina a quantidade de dados de saudação é de saída por meio de saudação *esquerdo* porta de saída.</span><span class="sxs-lookup"><span data-stu-id="0ae35-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="0ae35-171">Por exemplo, se você definir Olá taxa too0.7, 70% dos dados de saudação é saída por meio de saudação esquerda da porta e 30% por meio de porta de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="0ae35-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="0ae35-172">Clique duas vezes em Olá [dividir dados] [ split] módulo e Inserir comentário hello, "50% de divisão de dados de treinamento/teste".</span><span class="sxs-lookup"><span data-stu-id="0ae35-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="0ae35-173">Podemos usar saídas de saudação do hello [dividir dados] [ split] dados de testes de saída do módulo no entanto, como, mas vamos escolher toouse Olá esquerda saída como dados de treinamento e Olá à direita.</span><span class="sxs-lookup"><span data-stu-id="0ae35-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="0ae35-174">Conforme mencionado em Olá [etapa anterior](machine-learning-walkthrough-2-upload-data.md), classifique um risco de crédito alta como baixo custo Olá é cinco vezes maior do que o custo de saudação do classifique um risco de crédito baixa como alto.</span><span class="sxs-lookup"><span data-stu-id="0ae35-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="0ae35-175">tooaccount para isso, podemos gerar um novo conjunto de dados que reflete essa função de custo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="0ae35-176">Olá novo conjunto de dados, cada exemplo de alto risco é replicado cinco vezes, enquanto cada exemplo de baixo risco não é replicado.</span><span class="sxs-lookup"><span data-stu-id="0ae35-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="0ae35-177">Podemos fazer essa replicação usando o código R:</span><span class="sxs-lookup"><span data-stu-id="0ae35-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="0ae35-178">Localizar e arraste Olá [Executar Script R] [ execute-r-script] módulo na tela de experimento hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="0ae35-179">Conectar-se a saudação à esquerda a porta de saída de hello [dividir dados] [ split] toohello módulo primeiro porta de entrada ("Dataset1") da saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="0ae35-180">Clique duas vezes em Olá [Executar Script R] [ execute-r-script] módulo e Inserir comentário hello, "Conjunto de ajuste de custo".</span><span class="sxs-lookup"><span data-stu-id="0ae35-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="0ae35-181">Em Olá **propriedades** painel, excluir saudação padrão texto de saudação **Script R** parâmetro e digite este script:</span><span class="sxs-lookup"><span data-stu-id="0ae35-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script de R no módulo Executar Script R de saudação][9]

<span data-ttu-id="0ae35-183">Precisamos toodo essa mesma operação de replicação para cada saída de saudação [dividir dados] [ split] módulo de forma que Olá dados de teste e treinamento ter Olá mesmo custo de ajuste.</span><span class="sxs-lookup"><span data-stu-id="0ae35-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="0ae35-184">Olá toodo de maneira mais fácil trata duplicando Olá [Executar Script R] [ execute-r-script] módulo acabou de criar e conectá-lo toohello de saída de outra porta de saudação [dividir dados] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="0ae35-185">Saudação de atalho [Executar Script R] [ execute-r-script] módulo e selecione **cópia**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="0ae35-186">Tela de experimento hello e selecione **colar**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="0ae35-187">Arraste o novo módulo de saudação para a posição e conecte Olá porta de saída à direita de saudação [dividir dados] [ split] toohello módulo primeiro porta de entrada desse novo [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="0ae35-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="0ae35-188">Na parte inferior de saudação da tela hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="0ae35-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="0ae35-189">cópia de saudação do módulo Executar Script R de saudação contém Olá mesmo script como módulo original hello.</span><span class="sxs-lookup"><span data-stu-id="0ae35-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="0ae35-190">Quando você copiar e colar um módulo na tela hello, cópia Olá retém todas as propriedades de saudação do hello original.</span><span class="sxs-lookup"><span data-stu-id="0ae35-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="0ae35-191">Nosso teste agora se parece com esse:</span><span class="sxs-lookup"><span data-stu-id="0ae35-191">Our experiment now looks something like this:</span></span>

![Adicionando módulo Divisão e Scripts R][4]

<span data-ttu-id="0ae35-193">Para obter mais informações sobre como usar scripts R em seus testes, consulte [Estender seu teste com R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="0ae35-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="0ae35-194">**Em seguida: [treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="0ae35-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
