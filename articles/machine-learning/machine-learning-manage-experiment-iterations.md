---
title: "Gerenciar iterações de teste no Machine Learning Studio | Microsoft Docs"
description: "Como gerenciar iterações de teste no Machine Learning Studio do Microsoft Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="2b796-103">Gerenciar iterações de teste no Machine Learning Studio do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2b796-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="2b796-104">Desenvolver um modelo de análise de previsão é um processo iterativo - como modificar as várias funções e parâmetros de seu teste, seus resultados convergem até você ficar satisfeito com um modelo treinado e eficiente.</span><span class="sxs-lookup"><span data-stu-id="2b796-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="2b796-105">A chave para esse processo está em acompanhar várias iterações dos parâmetros e configurações do seu teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2b796-106">Você pode examinar as execuções anteriores dos seus testes a qualquer momento para desafiar, revisitar e, por fim, confirmar ou refinar suposições anteriores.</span><span class="sxs-lookup"><span data-stu-id="2b796-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="2b796-107">Quando você executa um teste, o Machine Learning Studio mantém um histórico de execução, incluindo o conjunto de dados, o módulo e as conexões de porta e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="2b796-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="2b796-108">Esse histórico também captura resultados, informações de tempo de execução, como tempos de início e parada, mensagens de log e status de execução.</span><span class="sxs-lookup"><span data-stu-id="2b796-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="2b796-109">Você pode observar qualquer uma dessas execuções a qualquer momento para examinar o cronograma de seu teste e os resultados intermediários.</span><span class="sxs-lookup"><span data-stu-id="2b796-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="2b796-110">Você pode até usar uma execução anterior de seu teste para fazer a inicialização em uma nova fase de consulta e descoberta em seu caminho para criar soluções simples, complexas ou até mesmo de modelagem conjunta.</span><span class="sxs-lookup"><span data-stu-id="2b796-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="2b796-111">Quando você exibe uma execução anterior de um teste, essa versão do teste está bloqueada e não pode ser editada.</span><span class="sxs-lookup"><span data-stu-id="2b796-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="2b796-112">No entanto, você pode salvar uma cópia dele clicando em **SALVAR COMO** e fornecendo um novo nome para a cópia.</span><span class="sxs-lookup"><span data-stu-id="2b796-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="2b796-113">O Machine Learning Studio abre a nova cópia, que você pode editar e executar.</span><span class="sxs-lookup"><span data-stu-id="2b796-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="2b796-114">Esta cópia do seu teste está disponível na lista **TESTES** junto com todos os seus testes.</span><span class="sxs-lookup"><span data-stu-id="2b796-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="2b796-115">Exibindo a execução anterior</span><span class="sxs-lookup"><span data-stu-id="2b796-115">Viewing the Prior Run</span></span>
<span data-ttu-id="2b796-116">Quando tiver um teste aberto que você tenha executado pelo menos uma vez, você pode exibir a execução anterior do teste clicando em **Execução anterior** no painel Propriedades.</span><span class="sxs-lookup"><span data-stu-id="2b796-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="2b796-117">Por exemplo, suponha que você crie um teste e execute versões dele às 11h23 11h42 e 11h55.</span><span class="sxs-lookup"><span data-stu-id="2b796-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="2b796-118">Se você abrir a última execução do teste (11h55) e clicar em **Execução anterior**, a versão que você executou às 11h42 será aberta.</span><span class="sxs-lookup"><span data-stu-id="2b796-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="2b796-119">Exibindo o Histórico de execução</span><span class="sxs-lookup"><span data-stu-id="2b796-119">Viewing the Run History</span></span>
<span data-ttu-id="2b796-120">Você pode exibir todas as execuções anteriores de um teste clicando em **Exibir Histórico de execução** em um teste aberto.</span><span class="sxs-lookup"><span data-stu-id="2b796-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="2b796-121">Por exemplo, suponha que você crie um teste com o módulo [Regressão Linear][linear-regression] e queira observar o efeito da alteração no valor da **Taxa de aprendizado** em seus resultados do teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="2b796-122">Você executa o teste várias vezes com valores diferentes para esse parâmetro, conforme segue:</span><span class="sxs-lookup"><span data-stu-id="2b796-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="2b796-123">Valor da Taxa de aprendizado</span><span class="sxs-lookup"><span data-stu-id="2b796-123">Learning Rate value</span></span> | <span data-ttu-id="2b796-124">Hora de início da execução</span><span class="sxs-lookup"><span data-stu-id="2b796-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="2b796-125">0,1</span><span class="sxs-lookup"><span data-stu-id="2b796-125">0.1</span></span> |<span data-ttu-id="2b796-126">11/09/2014 16h18min58s</span><span class="sxs-lookup"><span data-stu-id="2b796-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="2b796-127">0,2</span><span class="sxs-lookup"><span data-stu-id="2b796-127">0.2</span></span> |<span data-ttu-id="2b796-128">11/09/2014 16h24min33s</span><span class="sxs-lookup"><span data-stu-id="2b796-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="2b796-129">0,4</span><span class="sxs-lookup"><span data-stu-id="2b796-129">0.4</span></span> |<span data-ttu-id="2b796-130">11/09/2014 16h28min36s</span><span class="sxs-lookup"><span data-stu-id="2b796-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="2b796-131">0,5</span><span class="sxs-lookup"><span data-stu-id="2b796-131">0.5</span></span> |<span data-ttu-id="2b796-132">11/09/2014 16h33min31s</span><span class="sxs-lookup"><span data-stu-id="2b796-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="2b796-133">Se clicar em **EXIBIR O HISTÓRICO DE EXECUÇÃO**, você verá uma lista de todas essas execuções:</span><span class="sxs-lookup"><span data-stu-id="2b796-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Exemplo de histórico de execução][runhistory]

<span data-ttu-id="2b796-135">Clique em qualquer uma dessas execuções para exibir um instantâneo do teste no momento em que você o executou.</span><span class="sxs-lookup"><span data-stu-id="2b796-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="2b796-136">A configuração, os valores de parâmetro, comentários e resultados são preservados para que você tenha um registro completo da execução do seu teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="2b796-137">Para documentar suas iterações do teste, você pode modificar o título cada vez que executá-lo, pode atualizar o **Resumo** do teste no painel de propriedades e pode adicionar ou atualizar os comentários em módulos individuais para registrar as alterações.</span><span class="sxs-lookup"><span data-stu-id="2b796-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="2b796-138">Os comentários do título, do resumo e do módulo são salvos com cada execução do teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="2b796-139">A lista de testes na guia **TESTES** no Machine Learning Studio sempre exibe a versão mais recente de um teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="2b796-140">Se abrir uma execução anterior do teste (usando **Execução anterior** ou **EXIBIR O HISTÓRICO DE EXECUÇÃO**), você pode retornar para a versão de rascunho, clicando em **EXIBIR O HISTÓRICO DE EXECUÇÃO** e selecionando a iteração que tem um **ESTADO** **Editável**.</span><span class="sxs-lookup"><span data-stu-id="2b796-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="2b796-141">Iterando sobre uma Execução anterior</span><span class="sxs-lookup"><span data-stu-id="2b796-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="2b796-142">Quando clicar em **Execução anterior** ou em **EXIBIR O HISTÓRICO DE EXECUÇÃO** e abrir uma execução anterior, você poderá exibir um teste concluído no modo somente leitura.</span><span class="sxs-lookup"><span data-stu-id="2b796-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="2b796-143">Se quiser iniciar uma iteração de seu teste começando com o modo como você o configurou para uma execução anterior, você pode fazer isso abrindo a execução e clicando em **SALVAR COMO**.</span><span class="sxs-lookup"><span data-stu-id="2b796-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="2b796-144">Isso cria um novo teste, com um novo título, um histórico de execução vazio e todos os componentes e os valores de parâmetro de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="2b796-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="2b796-145">Esse novo teste é listado na guia **TESTES** na home page do Machine Learning Studio e você pode modificá-lo e executá-lo, iniciando um novo histórico de execução para essa iteração do seu teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="2b796-146">Por exemplo, suponha que você tenha o teste executando o histórico mostrado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="2b796-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="2b796-147">Você deseja observar o que acontece quando define o parâmetro **Taxa de aprendizagem** para 0,4 e testa valores diferentes para o parâmetro **Número de épocas de treinamento**.</span><span class="sxs-lookup"><span data-stu-id="2b796-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="2b796-148">Clique em **EXIBIR O HISTÓRICO DE EXECUÇÃO** e abra a iteração do teste que você executou às 16h28min36s (no qual você definiu o valor do parâmetro para 0,4).</span><span class="sxs-lookup"><span data-stu-id="2b796-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="2b796-149">Clique em **SALVAR COMO**.</span><span class="sxs-lookup"><span data-stu-id="2b796-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="2b796-150">Digite um novo título e clique na marca de seleção **OK** .</span><span class="sxs-lookup"><span data-stu-id="2b796-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="2b796-151">É criada uma nova cópia do teste.</span><span class="sxs-lookup"><span data-stu-id="2b796-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="2b796-152">Modifique o parâmetro **Número de épocas de treinamento** .</span><span class="sxs-lookup"><span data-stu-id="2b796-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="2b796-153">Clique em **EXECUTAR**.</span><span class="sxs-lookup"><span data-stu-id="2b796-153">Click **RUN**.</span></span>

<span data-ttu-id="2b796-154">Agora você pode continuar a modificar e executar esta versão do seu teste, criando um novo histórico de execução para registrar o seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b796-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
