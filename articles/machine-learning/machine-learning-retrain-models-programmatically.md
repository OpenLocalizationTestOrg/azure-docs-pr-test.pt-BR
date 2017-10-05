---
title: "Readaptar os modelos de Machine Learning de forma programática | Microsoft Docs"
description: "Aprenda como readaptar um modelo de forma programática e atualizar o serviço Web para usar o modelo treinado recentemente no Azure Machine Learning."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="47b21-103">Readaptar os modelos do Machine Learning de forma programática</span><span class="sxs-lookup"><span data-stu-id="47b21-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="47b21-104">Neste passo a passo, você aprenderá como programaticamente readaptar um serviço Web do Machine Learning do Azure usando C# e o serviço de Execução de Lote do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47b21-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="47b21-105">Depois de você ter readaptado o modelo, as instruções a seguir mostram como atualizar o modelo no seu serviço Web preditivo:</span><span class="sxs-lookup"><span data-stu-id="47b21-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="47b21-106">Se você implantou um serviço Web Clássico no portal de serviços Web do Machine Learning, confira [Readaptar um serviço Web Clássico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="47b21-107">Se você implantou um Novo serviço Web, confira [Readaptar um Novo serviço Web usando os cmdlets de Gerenciamento do Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="47b21-108">Para obter uma visão geral do processo de readaptação, confira [Readaptar um Modelo do Machine Learning](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="47b21-109">Se você quiser começar a usar o seu novo serviço Web baseado no Azure Resource Manager existente, confira [Readaptar um serviço Web preditivo existente](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="47b21-110">Criar um teste de treinamento</span><span class="sxs-lookup"><span data-stu-id="47b21-110">Create a training experiment</span></span>
<span data-ttu-id="47b21-111">Para este exemplo, você usará "Amostra 5: Treinar, testar, avaliar para classificação binária: conjunto de dados adulto" das amostras do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47b21-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="47b21-112">Para criar o experimento:</span><span class="sxs-lookup"><span data-stu-id="47b21-112">To create the experiment:</span></span>

1. <span data-ttu-id="47b21-113">Entre no Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="47b21-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="47b21-114">No canto inferior direito do painel, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="47b21-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="47b21-115">Nas Amostras da Microsoft, selecione a Amostra 5.</span><span class="sxs-lookup"><span data-stu-id="47b21-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="47b21-116">Para renomear o teste, na parte superior da tela do experimento, selecione o nome do teste "Amostra 5: Treinar, testar, avaliar para classificação binária: conjunto de dados adulto".</span><span class="sxs-lookup"><span data-stu-id="47b21-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="47b21-117">Tipo de modelo de censo.</span><span class="sxs-lookup"><span data-stu-id="47b21-117">Type Census Model.</span></span>
6. <span data-ttu-id="47b21-118">Na parte inferior da tela do experimento, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="47b21-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="47b21-119">Clique em **Configurar o Serviço Web** e selecione **Readaptação do Serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="47b21-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="47b21-120">A seguir, o teste inicial.</span><span class="sxs-lookup"><span data-stu-id="47b21-120">The following shows the initial experiment.</span></span>
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="47b21-122">Criar um Teste de Preditivo e publicar como um serviço Web</span><span class="sxs-lookup"><span data-stu-id="47b21-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="47b21-123">Em seguida, crie um Experimento Predicativo.</span><span class="sxs-lookup"><span data-stu-id="47b21-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="47b21-124">Na parte inferior da tela do experimento, clique em **Configurar o Serviço Web** e selecione **Serviço Web Preditivo**.</span><span class="sxs-lookup"><span data-stu-id="47b21-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="47b21-125">Isso salva o modelo como um Modelo Treinado e adiciona os módulos de Entrada e Saída do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="47b21-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="47b21-126">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="47b21-126">Click **Run**.</span></span> 
3. <span data-ttu-id="47b21-127">Após o teste em execução ter terminado, clique em **Implantar Serviço Web [Clássico]** ou **Implantar Serviço Web [Novo]**.</span><span class="sxs-lookup"><span data-stu-id="47b21-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="47b21-128">Para implantar um novo serviço Web, você precisa ter permissões suficientes na assinatura na qual o serviço Web está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="47b21-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="47b21-129">Para obter mais informações, consulte [Gerenciar um serviço Web usando o portal de Serviços Web do Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="47b21-130">Implantar o Teste de Treinamento como um serviço Web de Treinamento</span><span class="sxs-lookup"><span data-stu-id="47b21-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="47b21-131">Para readaptar o modelo treinado, você deve implantar o Teste de Treinamento criado como um Serviço Web de Readaptação.</span><span class="sxs-lookup"><span data-stu-id="47b21-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="47b21-132">Este serviço Web precisa um módulo *Saída do Serviço Web* conectado ao módulo *[Modelo de Treino][train-model]* para poder produzir novos modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="47b21-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="47b21-133">Para voltar para o teste de treinamento, clique no ícone de Experimentos no painel esquerdo, em seguida, clique no experimento chamado Modelo de Censo.</span><span class="sxs-lookup"><span data-stu-id="47b21-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="47b21-134">Na caixa de pesquisa Pesquisar Itens do Experimento, digite o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="47b21-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="47b21-135">Arraste um módulo *Entrada do Serviço Web* para a tela do experimento e conecte sua saída ao módulo *Limpar Dados Ausentes*.</span><span class="sxs-lookup"><span data-stu-id="47b21-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="47b21-136">Isso garante que os dados de readaptação são processados da mesma forma que os dados de treinamento original.</span><span class="sxs-lookup"><span data-stu-id="47b21-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="47b21-137">Arraste os dois módulos *Saída do Serviço Web* para as telas do experimento.</span><span class="sxs-lookup"><span data-stu-id="47b21-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="47b21-138">Conecte a saída do módulo *Modelo de Treinamento* a um e a saída do módulo *Modelo de Avaliação* ao outro.</span><span class="sxs-lookup"><span data-stu-id="47b21-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="47b21-139">A saída do serviço Web para o **Modelo de Treino** fornecerá o novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="47b21-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="47b21-140">A saída anexada ao **Modelo de Avaliação** retorna a saída do módulo, que são os resultados de desempenho.</span><span class="sxs-lookup"><span data-stu-id="47b21-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="47b21-141">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="47b21-141">Click **Run**.</span></span> 

<span data-ttu-id="47b21-142">Em seguida, você deve implantar o Teste de Treinamento como um serviço Web que produz um modelo treinado e os resultados de avaliação do modelo.</span><span class="sxs-lookup"><span data-stu-id="47b21-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="47b21-143">Para fazer isso, o próximo conjunto de ações dependem de você estar trabalhando com um serviço Web Clássico ou um Novo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="47b21-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="47b21-144">**Serviço Web Clássico**</span><span class="sxs-lookup"><span data-stu-id="47b21-144">**Classic web service**</span></span>

<span data-ttu-id="47b21-145">Na parte inferior da tela do experimento, clique em **Configurar o Serviço Web** e selecione **Implantar Serviço Web [Clássico]**.</span><span class="sxs-lookup"><span data-stu-id="47b21-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="47b21-146">O **Painel** do Serviço Web é exibido com a Chave de API e a página de ajuda da API para a Execução em Lotes.</span><span class="sxs-lookup"><span data-stu-id="47b21-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="47b21-147">Apenas o método de Execução em Lotes pode ser usado para criar Modelos Treinados.</span><span class="sxs-lookup"><span data-stu-id="47b21-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="47b21-148">**Novo Serviço Web**</span><span class="sxs-lookup"><span data-stu-id="47b21-148">**New web service**</span></span>

<span data-ttu-id="47b21-149">Na parte inferior da tela do experimento, clique em **Configurar o Serviço Web** e selecione **Implantar Serviço Web [Novo]**.</span><span class="sxs-lookup"><span data-stu-id="47b21-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="47b21-150">O portal dos Serviços Web de Machine Learning do Azure abre a página Implantar Serviço Web.</span><span class="sxs-lookup"><span data-stu-id="47b21-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="47b21-151">Digite um nome para o serviço Web, escolha um plano de pagamento clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="47b21-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="47b21-152">Apenas o método Execução em Lotes pode ser usado para criar os Modelos Treinados</span><span class="sxs-lookup"><span data-stu-id="47b21-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="47b21-153">Em ambos os casos, após o teste terminar a execução, o fluxo de trabalho resultante fica como a seguir:</span><span class="sxs-lookup"><span data-stu-id="47b21-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Fluxo de trabalho resultante após a execução.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="47b21-155">Você quer readaptar o modelo com novos dados</span><span class="sxs-lookup"><span data-stu-id="47b21-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="47b21-156">Para este exemplo, você está usando C# para criar o aplicativo de readaptação.</span><span class="sxs-lookup"><span data-stu-id="47b21-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="47b21-157">Você também pode usar o código de exemplo do Python ou R para realizar essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="47b21-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="47b21-158">Para chamar as APIs de Readaptação:</span><span class="sxs-lookup"><span data-stu-id="47b21-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="47b21-159">Crie um aplicativo de console C# no Visual Studio: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="47b21-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="47b21-160">Entre no portal do Serviço Web de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47b21-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="47b21-161">Se você estiver trabalhando com um serviço Web Clássico, clique em **Serviços Web Clássicos**.</span><span class="sxs-lookup"><span data-stu-id="47b21-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="47b21-162">Clique no serviço Web com o qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="47b21-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="47b21-163">Clique no ponto de extremidade padrão.</span><span class="sxs-lookup"><span data-stu-id="47b21-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="47b21-164">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="47b21-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="47b21-165">Na parte inferior da página **Consumir**, na seção **Código de Exemplo**, clique em **Lote**.</span><span class="sxs-lookup"><span data-stu-id="47b21-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="47b21-166">Continue na etapa 5 deste procedimento.</span><span class="sxs-lookup"><span data-stu-id="47b21-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="47b21-167">Se você estiver trabalhando com um Novo serviço Web, clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="47b21-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="47b21-168">Clique no serviço Web com o qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="47b21-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="47b21-169">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="47b21-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="47b21-170">Na parte inferior da página Consumir, na seção **Código de Exemplo**, clique em **Lote**.</span><span class="sxs-lookup"><span data-stu-id="47b21-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="47b21-171">Copie o código C# de exemplo da execução em lotes e cole-o no arquivo Program.cs, verificando se o namespace permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="47b21-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="47b21-172">Adicione o pacote do Nuget Microsoft.AspNet.WebApi.Client como especificado nos comentários.</span><span class="sxs-lookup"><span data-stu-id="47b21-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="47b21-173">Para adicionar a referência a Microsoft.WindowsAzure.Storage.dll, você precisará primeiro instalar a biblioteca de cliente para os serviços de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47b21-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="47b21-174">Para obter mais informações, consulte [Serviços de Armazenamento do Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="47b21-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="47b21-175">Atualizar a declaração da apikey</span><span class="sxs-lookup"><span data-stu-id="47b21-175">Update the apikey declaration</span></span>
<span data-ttu-id="47b21-176">Localize a declaração da **apikey** .</span><span class="sxs-lookup"><span data-stu-id="47b21-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="47b21-177">Na seção **Informações básicas de consumo** da página **Consumir**, localize a chave primária e copie-a para a declaração da **apikey**.</span><span class="sxs-lookup"><span data-stu-id="47b21-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="47b21-178">Atualize as informações do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="47b21-178">Update the Azure Storage information</span></span>
<span data-ttu-id="47b21-179">O código de exemplo de BES carrega um arquivo de uma unidade local (por exemplo "C:\temp\CensusIpnput.csv") para o armazenamento do Azure, processa e grava os resultados de volta para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47b21-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="47b21-180">Para realizar essa tarefa, você deve recuperar as informações de nome da Conta de armazenamento, da chave e do contêiner para sua Conta de armazenamento no portal clássico do Azure e os valores correspondentes de atualização no código.</span><span class="sxs-lookup"><span data-stu-id="47b21-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="47b21-181">Entre no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="47b21-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="47b21-182">Na coluna de navegação à esquerda, clique em **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="47b21-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="47b21-183">Na lista de contas de armazenamento, selecione uma para armazenar o modelo recuperado.</span><span class="sxs-lookup"><span data-stu-id="47b21-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="47b21-184">Na parte inferior da página, clique em **Gerenciar Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="47b21-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="47b21-185">Copie e salve a **Chave de Acesso Primária** e feche a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47b21-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="47b21-186">Na parte superior da página, clique em **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="47b21-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="47b21-187">Selecione um contêiner existente ou crie um novo e salve o nome.</span><span class="sxs-lookup"><span data-stu-id="47b21-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="47b21-188">Localize as declarações *StorageAccountName*, *StorageAccountKey* e *StorageContainerName*, e atualize os valores salvos no portal no Azure.</span><span class="sxs-lookup"><span data-stu-id="47b21-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="47b21-189">Você também deve garantir que o arquivo de entrada está disponível no local especificado no código.</span><span class="sxs-lookup"><span data-stu-id="47b21-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="47b21-190">Especificar o local de saída</span><span class="sxs-lookup"><span data-stu-id="47b21-190">Specify the output location</span></span>
<span data-ttu-id="47b21-191">Ao especificar o local de saída no Conteúdo de Solicitação, a extensão do arquivo especificado em *RelativeLocation* deve ser definido como ilearner.</span><span class="sxs-lookup"><span data-stu-id="47b21-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="47b21-192">Veja os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="47b21-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="47b21-193">Os nomes de seus locais de saída podem ser diferentes neste passo a passo com base na ordem em que você adicionou os módulos de saída do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="47b21-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="47b21-194">Como você configura esse Teste de Treinamento com duas saídas, os resultados incluem informações de local de armazenamento para ambos.</span><span class="sxs-lookup"><span data-stu-id="47b21-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Saída da readaptação][6]

<span data-ttu-id="47b21-196">Diagrama 4:Saída da readaptação.</span><span class="sxs-lookup"><span data-stu-id="47b21-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="47b21-197">Avaliar os resultados da readaptação</span><span class="sxs-lookup"><span data-stu-id="47b21-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="47b21-198">Quando você executa o aplicativo, a saída inclui o token SAS e a URL necessários para acessar os resultados da avaliação.</span><span class="sxs-lookup"><span data-stu-id="47b21-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="47b21-199">Você pode ver os resultados do desempenho do modelo readaptado ao combinar *BaseLocation*, *RelativeLocation* e *SasBlobToken* dos resultados de saída para *output2* (como mostrado na imagem de readaptação anterior) e colando a URL completa na barra de endereço do navegador.</span><span class="sxs-lookup"><span data-stu-id="47b21-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="47b21-200">Examine os resultados para determinar se o modelo treinado recentemente executa bem o suficiente para substituir o existente.</span><span class="sxs-lookup"><span data-stu-id="47b21-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="47b21-201">Copie *BaseLocation*, *RelativeLocation* e *SasBlobToken* dos resultados de saída e use-os durante o processo de readaptação.</span><span class="sxs-lookup"><span data-stu-id="47b21-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47b21-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47b21-202">Next steps</span></span>
<span data-ttu-id="47b21-203">Se você tiver implantado o serviço Web de previsão clicando em **implantar o serviço Web [clássico]**, consulte [treinar novamente um serviço web clássico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="47b21-204">Se você tiver implantado um Novo serviço Web clicando em **Implantar o Serviço Web [Novo]**, consulte [treinar novamente um serviço web novo usando os cmdlets de gerenciamento do Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47b21-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
