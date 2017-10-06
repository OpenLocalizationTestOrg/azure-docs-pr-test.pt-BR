---
title: "modelos de aprendizado de máquina do aaaRetrain programaticamente | Microsoft Docs"
description: "Saiba como tooprogrammatically treinar novamente um modelo e a atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="f0271-103">Readaptar os modelos de Machine Learning de forma programática</span><span class="sxs-lookup"><span data-stu-id="f0271-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="f0271-104">Este passo a passo, você aprenderá como tooprogrammatically treinar novamente um serviço Web do Azure Machine Learning usando c# e hello serviço de execução de lote de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="f0271-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="f0271-105">Depois de você ter retreinados modelo hello, Olá explicações passo a passo a seguir mostra como tooupdate Olá modelo em seu serviço web de previsão:</span><span class="sxs-lookup"><span data-stu-id="f0271-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="f0271-106">Se você implantou um serviço da web clássico no portal de serviços de Web do aprendizado de máquina hello, consulte [treinar novamente um serviço da web clássico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="f0271-107">Se você implantou um novo serviço da web, consulte [treinar novamente um novo serviço da web usando cmdlets de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="f0271-108">Para obter uma visão geral de Olá processo de treinamento, consulte [treinar novamente um modelo de aprendizado de máquina](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="f0271-109">Se você quiser toostart com seu novo Gerenciador de recursos do Azure baseada em serviço web, consulte [treinar novamente um serviço web de previsão existente](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="f0271-110">Criar um teste de treinamento</span><span class="sxs-lookup"><span data-stu-id="f0271-110">Create a training experiment</span></span>
<span data-ttu-id="f0271-111">Neste exemplo, você usará "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" exemplos de aprendizado de máquina do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f0271-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="f0271-112">experiência de saudação toocreate:</span><span class="sxs-lookup"><span data-stu-id="f0271-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="f0271-113">Entrar no tooMicrosoft estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0271-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="f0271-114">No hello canto inferior direito do painel de saudação, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="f0271-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="f0271-115">Selecione Olá Microsoft Samples, 5 de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f0271-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="f0271-116">experiência de saudação toorename, na parte superior de saudação da tela de experimento Olá, selecione o nome de teste de hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados somente para adultos".</span><span class="sxs-lookup"><span data-stu-id="f0271-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="f0271-117">Tipo de modelo de censo.</span><span class="sxs-lookup"><span data-stu-id="f0271-117">Type Census Model.</span></span>
6. <span data-ttu-id="f0271-118">Na parte inferior de saudação da tela de experimento hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="f0271-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="f0271-119">Clique em **Configurar o Serviço Web** e selecione **Readaptação do Serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="f0271-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="f0271-120">Veja a seguir de Olá experiência inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-120">hello following shows hello initial experiment.</span></span>
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="f0271-122">Criar um Teste de Preditivo e publicar como um serviço Web</span><span class="sxs-lookup"><span data-stu-id="f0271-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="f0271-123">Em seguida, crie um Experimento Predicativo.</span><span class="sxs-lookup"><span data-stu-id="f0271-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="f0271-124">Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **previsão Web Service**.</span><span class="sxs-lookup"><span data-stu-id="f0271-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="f0271-125">Isso economiza modelo hello como um modelo treinado e adiciona módulos do serviço web de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="f0271-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="f0271-126">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="f0271-126">Click **Run**.</span></span> 
3. <span data-ttu-id="f0271-127">Depois de experiência de saudação concluiu a execução, clique em **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="f0271-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="f0271-128">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="f0271-129">Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="f0271-130">Implantar a experiência de treinamento hello como um serviço da web de treinamento</span><span class="sxs-lookup"><span data-stu-id="f0271-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="f0271-131">tooretrain Olá treinado, você deve implantar a experiência de treinamento Olá criado como um serviço da web Retraining.</span><span class="sxs-lookup"><span data-stu-id="f0271-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="f0271-132">Esse serviço da web precisa um *saída do serviço Web* módulo conectado toohello  *[treinar modelo] [ train-model]*  tooproduce capaz de toobe novo, de módulo modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="f0271-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="f0271-133">experiência de treinamento de toohello tooreturn, ícone de experiências de saudação no painel esquerdo do hello clique experimento Olá chamado modelo de censo.</span><span class="sxs-lookup"><span data-stu-id="f0271-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="f0271-134">Na caixa de pesquisa de itens de experiência de pesquisa hello, tipo de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="f0271-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="f0271-135">Arraste um *entrada de serviço Web* módulo no hello experiências de tela e conecte-se sua saída toohello *limpar dados ausentes* módulo.</span><span class="sxs-lookup"><span data-stu-id="f0271-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="f0271-136">Isso garante que os dados novos treinamentos seja processados Olá mesma maneira como os dados de treinamento original.</span><span class="sxs-lookup"><span data-stu-id="f0271-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="f0271-137">Arraste dois *saída do serviço web* módulos para Olá experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="f0271-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="f0271-138">Conecte a saída de saudação do hello *treinar modelo* tooone e Olá saída de hello módulo *avaliar modelo* módulo toohello outros.</span><span class="sxs-lookup"><span data-stu-id="f0271-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="f0271-139">Olá saída do serviço web para **treinar modelo** nos dá novo modelo treinado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="f0271-140">Olá saída anexada muito**avaliar modelo** retorna a saída desse módulo, que é resultados de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="f0271-141">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="f0271-141">Click **Run**.</span></span> 

<span data-ttu-id="f0271-142">Em seguida, você deve implantar Olá experiência de treinamento como um serviço web que produz um modelo treinado e resultados de avaliação do modelo.</span><span class="sxs-lookup"><span data-stu-id="f0271-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="f0271-143">tooaccomplish isso, o próximo conjunto de ações dependem se você estiver trabalhando com um serviço da web clássico ou um novo serviço web.</span><span class="sxs-lookup"><span data-stu-id="f0271-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="f0271-144">**Serviço Web Clássico**</span><span class="sxs-lookup"><span data-stu-id="f0271-144">**Classic web service**</span></span>

<span data-ttu-id="f0271-145">Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **implantar o serviço Web [clássico]**.</span><span class="sxs-lookup"><span data-stu-id="f0271-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="f0271-146">Olá Web Service **painel** é exibido com a página de ajuda Olá chave de API e hello API para execução em lotes.</span><span class="sxs-lookup"><span data-stu-id="f0271-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="f0271-147">Olá método de execução em lote pode ser usado para criar modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="f0271-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="f0271-148">**Novo Serviço Web**</span><span class="sxs-lookup"><span data-stu-id="f0271-148">**New web service**</span></span>

<span data-ttu-id="f0271-149">Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="f0271-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="f0271-150">portal de serviços da Web de aprendizado de máquina do Web Service Azure Olá abre toohello página de serviço de web de implantação.</span><span class="sxs-lookup"><span data-stu-id="f0271-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="f0271-151">Digite um nome para o serviço Web, escolha um plano de pagamento clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="f0271-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="f0271-152">Olá método de execução de lote pode ser usado para criar modelos treinados</span><span class="sxs-lookup"><span data-stu-id="f0271-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="f0271-153">Em ambos os casos, após o teste foi concluído em execução, fluxo de trabalho resultante Olá se assemelhar ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0271-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Fluxo de trabalho resultante após a execução.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="f0271-155">Treinar novamente o modelo de saudação com novos dados usando BES</span><span class="sxs-lookup"><span data-stu-id="f0271-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="f0271-156">Neste exemplo, você está usando o c# toocreate Olá treinamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0271-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="f0271-157">Você também pode usar Olá Python ou tooaccomplish de código de exemplo R Esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="f0271-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="f0271-158">toocall Olá APIs de treinamento:</span><span class="sxs-lookup"><span data-stu-id="f0271-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="f0271-159">Crie um aplicativo de console C# no Visual Studio: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f0271-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="f0271-160">Entrar toohello portal do serviço de Web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="f0271-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="f0271-161">Se você estiver trabalhando com um serviço Web Clássico, clique em **Serviços Web Clássicos**.</span><span class="sxs-lookup"><span data-stu-id="f0271-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="f0271-162">Clique em Olá web service que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="f0271-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="f0271-163">Clique em ponto de extremidade saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="f0271-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="f0271-164">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="f0271-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="f0271-165">Na parte inferior de saudação do hello **consumir** página Olá **código de exemplo** seção, clique em **lote**.</span><span class="sxs-lookup"><span data-stu-id="f0271-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="f0271-166">Continue toostep 5 deste procedimento.</span><span class="sxs-lookup"><span data-stu-id="f0271-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="f0271-167">Se você estiver trabalhando com um Novo serviço Web, clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="f0271-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="f0271-168">Clique em Olá web service que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="f0271-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="f0271-169">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="f0271-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="f0271-170">Na parte inferior da saudação de Olá consumir da página Olá **código de exemplo** seção, clique em **lote**.</span><span class="sxs-lookup"><span data-stu-id="f0271-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="f0271-171">Copie Olá c# código de exemplo para execução em lotes e cole-o no arquivo Program.cs de hello, certificando-se de namespace Olá permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="f0271-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="f0271-172">Adicione o pacote de Nuget Olá Microsoft.AspNet.WebApi.Client conforme especificado nos comentários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="f0271-173">tooadd Olá referência tooMicrosoft.WindowsAzure.Storage.dll, talvez seja necessário primeiro biblioteca de cliente tooinstall Olá para serviços de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f0271-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="f0271-174">Para obter mais informações, consulte [Serviços de Armazenamento do Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="f0271-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="f0271-175">Atualizar a declaração de apikey Olá</span><span class="sxs-lookup"><span data-stu-id="f0271-175">Update hello apikey declaration</span></span>
<span data-ttu-id="f0271-176">Localizar Olá **apikey** declaração.</span><span class="sxs-lookup"><span data-stu-id="f0271-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="f0271-177">Em Olá **informações básicas de consumo** seção Olá **consumir** página, localize a chave primária hello e copiá-lo toohello **apikey** declaração.</span><span class="sxs-lookup"><span data-stu-id="f0271-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="f0271-178">Atualizar informações de armazenamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="f0271-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="f0271-179">Olá, código de exemplo do BES carrega um arquivo de um armazenamento de tooAzure de disco local (por exemplo "C:\temp\CensusIpnput.csv"), processa e grava tooAzure armazenamento do retorno de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="f0271-180">tooaccomplish nesta tarefa, você deve recuperar informações de contêiner, chave e nome de conta de armazenamento do Olá para sua conta de armazenamento do portal do Azure clássico de saudação e atualização Olá correspondente valores no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="f0271-181">Faça logon no portal do Azure clássico de toohello.</span><span class="sxs-lookup"><span data-stu-id="f0271-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="f0271-182">Na coluna de navegação à esquerda hello, clique em **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="f0271-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="f0271-183">Na lista de saudação de contas de armazenamento, selecione uma toostore saudação retreinados modelo.</span><span class="sxs-lookup"><span data-stu-id="f0271-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="f0271-184">Final Olá Olá página, clique em **gerenciar chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="f0271-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="f0271-185">Copie e salve Olá **chave de acesso primária** e caixa de diálogo fechar hello.</span><span class="sxs-lookup"><span data-stu-id="f0271-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="f0271-186">Na parte superior de saudação da página de saudação, clique em **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="f0271-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="f0271-187">Selecione um contêiner existente ou crie um novo e salve o nome hello.</span><span class="sxs-lookup"><span data-stu-id="f0271-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="f0271-188">Localizar Olá *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* declarações e atualizar valores de saudação salvo do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0271-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="f0271-189">Você também deve garantir o arquivo de entrada hello está disponível no local Olá especificado no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0271-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="f0271-190">Especifique o local de saída Olá</span><span class="sxs-lookup"><span data-stu-id="f0271-190">Specify hello output location</span></span>
<span data-ttu-id="f0271-191">Ao especificar local de saída Olá Olá carga de solicitação, Olá a extensão do arquivo hello especificado na *RelativeLocation* devem ser especificados como ilearner.</span><span class="sxs-lookup"><span data-stu-id="f0271-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="f0271-192">Consulte Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0271-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="f0271-193">nomes de saudação de seus locais de saída podem ser diferentes da saudação aqueles neste passo a passo com base na ordem de saudação em que você adicionou Olá módulos de saída de serviço de web.</span><span class="sxs-lookup"><span data-stu-id="f0271-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="f0271-194">Como configurar esse teste de treinamento com duas saídas, resultados da saudação incluem informações de local de armazenamento para ambos.</span><span class="sxs-lookup"><span data-stu-id="f0271-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Saída da readaptação][6]

<span data-ttu-id="f0271-196">Diagrama 4:Saída da readaptação.</span><span class="sxs-lookup"><span data-stu-id="f0271-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="f0271-197">Avaliar os resultados de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="f0271-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="f0271-198">Quando você executa o aplicativo hello, saída de hello inclui a URL de saudação e tooaccess necessário do token SAS Olá resultados da avaliação.</span><span class="sxs-lookup"><span data-stu-id="f0271-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="f0271-199">Você pode ver os resultados de desempenho de saudação do modelo Olá treinados novamente combinando Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída para *output2* (conforme mostrado no hello anterior de treinamento a imagem de saída) e colando URL completa Olá na barra de endereços do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="f0271-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="f0271-200">Examine Olá resultados toodetermine se Olá recentemente treinado executa também suficiente Olá tooreplace existente a um.</span><span class="sxs-lookup"><span data-stu-id="f0271-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="f0271-201">Saudação de cópia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída, você usará-los durante a saudação processo de treinamento.</span><span class="sxs-lookup"><span data-stu-id="f0271-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0271-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0271-202">Next steps</span></span>
<span data-ttu-id="f0271-203">Se você implantou o serviço web de previsão de saudação clicando **implantar o serviço Web [clássico]**, consulte [treinar novamente um serviço da web clássico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="f0271-204">Se você implantou o serviço web de previsão de saudação clicando **implantar o serviço de Web [novo]**, consulte [treinar novamente um novo serviço da web usando cmdlets de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f0271-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
