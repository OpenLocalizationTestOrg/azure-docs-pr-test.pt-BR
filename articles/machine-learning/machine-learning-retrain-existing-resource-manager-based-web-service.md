---
title: "serviço web de aaaRetrain uma previsão existente | Microsoft Docs"
description: "Saiba como tooretrain um modelo e atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="e99e0-103">Readaptar um serviço Web de previsão existente</span><span class="sxs-lookup"><span data-stu-id="e99e0-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="e99e0-104">Este documento descreve Olá treinamento processo para Olá cenário a seguir:</span><span class="sxs-lookup"><span data-stu-id="e99e0-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="e99e0-105">Você tem um experimento de treinamento e um experimento de previsão implantado como um serviço Web operacionalizado.</span><span class="sxs-lookup"><span data-stu-id="e99e0-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="e99e0-106">Você tem novos dados que você deseja que seu tooperform de toouse de serviço web de previsão sua pontuação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="e99e0-107">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="e99e0-108">Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e99e0-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e99e0-109">Começando com o serviço da web existente e experiências, você precisa toofollow estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e99e0-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="e99e0-110">Atualize o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-110">Update hello model.</span></span>
   1. <span data-ttu-id="e99e0-111">Modifique seu tooallow de experiência de treinamento para as entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="e99e0-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="e99e0-112">Implante a experiência de treinamento hello como um serviço web novos treinamentos.</span><span class="sxs-lookup"><span data-stu-id="e99e0-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="e99e0-113">Use modelo de saudação do teste de treinamento Olá serviço de execução de lote (BES) tooretrain.</span><span class="sxs-lookup"><span data-stu-id="e99e0-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="e99e0-114">Use o teste da previsão de Olá Olá aprendizado de máquina do Azure PowerShell cmdlets tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e99e0-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="e99e0-115">Entrar tooyour conta do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e99e0-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="e99e0-116">Obter definição de serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="e99e0-117">Exporte a definição de serviço web hello como JSON.</span><span class="sxs-lookup"><span data-stu-id="e99e0-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="e99e0-118">Atualização Olá toohello ilearner blob de referência no hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e99e0-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="e99e0-119">Importe Olá JSON em uma definição de serviço web.</span><span class="sxs-lookup"><span data-stu-id="e99e0-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="e99e0-120">Atualize o serviço web de saudação com uma nova definição de serviço web.</span><span class="sxs-lookup"><span data-stu-id="e99e0-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="e99e0-121">Implantar a experiência de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="e99e0-121">Deploy hello training experiment</span></span>
<span data-ttu-id="e99e0-122">experiência de treinamento toodeploy hello como um serviço web novos treinamentos, você deve adicionar o modelo toohello do web service entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="e99e0-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="e99e0-123">Conectando-se um *saída do serviço Web* da experiência do módulo toohello  *[treinar modelo] [ train-model]*  módulo, habilitar Olá experiência de treinamento tooproduce um novo modelo treinado que você pode usar em sua experiência de previsão.</span><span class="sxs-lookup"><span data-stu-id="e99e0-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="e99e0-124">Se você tiver um *avaliar modelo* módulo, você também pode anexar resultados da avaliação do web service saída tooget hello como saída.</span><span class="sxs-lookup"><span data-stu-id="e99e0-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="e99e0-125">tooupdate sua experiência de treinamento:</span><span class="sxs-lookup"><span data-stu-id="e99e0-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="e99e0-126">Conecte-se um *entrada de serviço da Web* dados tooyour do módulo de entrada (por exemplo, um *limpar dados ausentes* módulo).</span><span class="sxs-lookup"><span data-stu-id="e99e0-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="e99e0-127">Geralmente, você deseja tooensure seus dados de entrada são processados em Olá mesma forma que os dados de treinamento original.</span><span class="sxs-lookup"><span data-stu-id="e99e0-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="e99e0-128">Conecte-se um *saída do serviço Web* saída do módulo toohello do seu *treinar modelo* módulo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="e99e0-129">Se você tiver um *avaliar modelo* módulo e você deseja que os resultados de avaliação do toooutput hello, conecte-se um *saída do serviço Web* saída do módulo toohello do seu *avaliar modelo* módulo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="e99e0-130">Execute seu experimento.</span><span class="sxs-lookup"><span data-stu-id="e99e0-130">Run your experiment.</span></span>

<span data-ttu-id="e99e0-131">Em seguida, você deve implantar Olá experiência de treinamento como um serviço web que produz um modelo treinado e resultados de avaliação do modelo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="e99e0-132">Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web**e, em seguida, selecione **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="e99e0-133">portal de serviços de Web de aprendizado de máquina do Azure Olá abre toohello **implantar o serviço da Web** página.</span><span class="sxs-lookup"><span data-stu-id="e99e0-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="e99e0-134">Digite um nome para o serviço Web, escolha um plano de pagamento e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="e99e0-135">Somente você pode usar o método de execução de lote hello para a criação de modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="e99e0-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="e99e0-136">Treinar novamente o modelo de saudação com novos dados usando BES</span><span class="sxs-lookup"><span data-stu-id="e99e0-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="e99e0-137">Neste exemplo, estamos usando c# toocreate Olá treinamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="e99e0-138">Você também pode usar essa tarefa Python ou R tooaccomplish de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="e99e0-139">Olá toocall treinamento APIs:</span><span class="sxs-lookup"><span data-stu-id="e99e0-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="e99e0-140">Crie um aplicativo de console C# no Visual Studio: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="e99e0-141">Entrar toohello portal de serviços de Web do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="e99e0-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="e99e0-142">Clique em Olá web service que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="e99e0-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="e99e0-143">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-143">Click **Consume**.</span></span>
5. <span data-ttu-id="e99e0-144">Na parte inferior de saudação do hello **consumir** página Olá **código de exemplo** seção, clique em **lote**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="e99e0-145">Copie Olá c# código de exemplo para execução em lotes e cole-o no arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="e99e0-146">Certifique-se de que o namespace Olá permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="e99e0-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="e99e0-147">Adicione o pacote de NuGet Olá Microsoft.AspNet.WebApi.Client, conforme especificado nos comentários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="e99e0-148">tooadd Olá referência tooMicrosoft.WindowsAzure.Storage.dll, talvez seja necessário primeiro Olá tooinstall [biblioteca de cliente para serviços de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="e99e0-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="e99e0-149">Olá, seguinte captura de tela mostra Olá **consumir** página no portal de serviços de Web de aprendizado de máquina do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Página Consumir][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="e99e0-151">Atualizar a declaração de apikey Olá</span><span class="sxs-lookup"><span data-stu-id="e99e0-151">Update hello apikey declaration</span></span>
<span data-ttu-id="e99e0-152">Localizar Olá **apikey** declaração:</span><span class="sxs-lookup"><span data-stu-id="e99e0-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="e99e0-153">Em Olá **informações básicas de consumo** seção Olá **consumir** página, localize a chave primária hello e copiá-lo toohello **apikey** declaração.</span><span class="sxs-lookup"><span data-stu-id="e99e0-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="e99e0-154">Atualizar informações de armazenamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="e99e0-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="e99e0-155">Olá, código de exemplo do BES carrega um arquivo de um armazenamento de tooAzure de disco local (por exemplo, "C:\temp\CensusIpnput.csv"), processa e grava tooAzure armazenamento do retorno de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="e99e0-156">informações de armazenamento do Azure do tooupdate hello, você deve recuperar informações de nome, a chave e o contêiner para sua conta de armazenamento de saudação portal clássico do Azure e, em seguida, atualização Olá correspondi após a execução de sua experiência, Olá resultante de conta de armazenamento Olá fluxo de trabalho deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="e99e0-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Fluxo de trabalho resultante após a execução][4]<span data-ttu-id="e99e0-158">valores NG código hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-158">ng values in hello code.</span></span>

1. <span data-ttu-id="e99e0-159">Entrar toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e99e0-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="e99e0-160">Na coluna de navegação à esquerda hello, clique em **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="e99e0-161">Na lista de saudação de contas de armazenamento, selecione uma toostore saudação retreinados modelo.</span><span class="sxs-lookup"><span data-stu-id="e99e0-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="e99e0-162">Final Olá Olá página, clique em **gerenciar chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="e99e0-163">Copie e salve Olá **chave de acesso primária** e caixa de diálogo fechar hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="e99e0-164">Na parte superior de saudação da página de saudação, clique em **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="e99e0-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="e99e0-165">Selecione um contêiner existente, ou crie um novo e salve o nome hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="e99e0-166">Localizar Olá *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* declarações e atualizar valores de saudação que você salvou no portal clássico Olá .</span><span class="sxs-lookup"><span data-stu-id="e99e0-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="e99e0-167">Você também deve garantir que arquivos de entrada hello está disponível no local de Olá especificado por você no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="e99e0-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="e99e0-168">Especifique o local de saída Olá</span><span class="sxs-lookup"><span data-stu-id="e99e0-168">Specify hello output location</span></span>
<span data-ttu-id="e99e0-169">Quando você especifica o local de saída de saudação em Olá carga de solicitação, Olá a extensão do arquivo hello especificado em *RelativeLocation* devem ser especificados como `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="e99e0-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="e99e0-170">Consulte Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e99e0-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="e99e0-171">Olá, a seguir é um exemplo de saída de treinamento: ![treinamento de saída][6]</span><span class="sxs-lookup"><span data-stu-id="e99e0-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="e99e0-172">Avaliar Olá treinamento resultados</span><span class="sxs-lookup"><span data-stu-id="e99e0-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="e99e0-173">Quando você executa o aplicativo hello, saída de hello inclui Olá URL e token de assinaturas de acesso compartilhado que são os resultados da avaliação Olá tooaccess necessário.</span><span class="sxs-lookup"><span data-stu-id="e99e0-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="e99e0-174">Você pode ver os resultados de desempenho de saudação do modelo Olá treinados novamente combinando Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída para *output2* (conforme mostrado no hello anterior de treinamento a imagem de saída) e colando URL completa Olá na barra de endereços do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="e99e0-175">Examine Olá resultados toodetermine se Olá recentemente treinado executa também suficiente Olá tooreplace existente a um.</span><span class="sxs-lookup"><span data-stu-id="e99e0-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="e99e0-176">Saudação de cópia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída.</span><span class="sxs-lookup"><span data-stu-id="e99e0-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="e99e0-177">Treinar novamente o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="e99e0-177">Retrain hello web service</span></span>
<span data-ttu-id="e99e0-178">Quando você treinar novamente um novo serviço da web, atualiza Olá web de previsão serviço definição tooreference Olá novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="e99e0-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="e99e0-179">definição de serviço web Hello é uma representação interna do modelo treinado de saudação do serviço web de saudação e não pode ser modificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="e99e0-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="e99e0-180">Certifique-se de que você está recuperando a definição de serviço web Olá para sua experiência de previsão e não sua experiência de treinamento.</span><span class="sxs-lookup"><span data-stu-id="e99e0-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="e99e0-181">Entrar no Gerenciador de recursos de tooAzure</span><span class="sxs-lookup"><span data-stu-id="e99e0-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="e99e0-182">Você deve primeiro entrar em tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e99e0-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="e99e0-183">Obter o objeto de definição de serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="e99e0-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="e99e0-184">Em seguida, obter objeto de definição de serviço Web Olá Olá chamada [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e99e0-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="e99e0-185">nome do grupo toodetermine Olá recursos de um serviço da web existente, execute o cmdlet de Get-AzureRmMlWebService de saudação sem serviços parâmetros toodisplay Olá web em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e99e0-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="e99e0-186">Localize o serviço web de saudação e, em seguida, examine a sua ID de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="e99e0-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="e99e0-187">nome de Olá Olá do grupo de recursos é quarto elemento Olá Olá ID, logo após Olá *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="e99e0-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="e99e0-188">Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.</span><span class="sxs-lookup"><span data-stu-id="e99e0-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="e99e0-189">Como alternativa, toodetermine Olá recurso nome de grupo de um objeto existente serviço web, entre no portal de serviços de Web de aprendizado de máquina do Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e99e0-190">Selecione Olá web service.</span><span class="sxs-lookup"><span data-stu-id="e99e0-190">Select hello web service.</span></span> <span data-ttu-id="e99e0-191">nome do grupo de recursos de saudação é elemento quinto Olá Olá URL do serviço da web de hello, logo após Olá *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="e99e0-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="e99e0-192">Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.</span><span class="sxs-lookup"><span data-stu-id="e99e0-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="e99e0-193">Exportar o objeto de definição de serviço Web hello como JSON</span><span class="sxs-lookup"><span data-stu-id="e99e0-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="e99e0-194">definição de saudação toomodify de saudação do hello treinado toouse modelo treinado recentemente, primeiro você deve usar o hello [AzureRmMlWebService de exportação](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport-arquivo tooa formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e99e0-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="e99e0-195">Atualizar Olá referência toohello ilearner blob</span><span class="sxs-lookup"><span data-stu-id="e99e0-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="e99e0-196">Em ativos hello, localize Olá [treinado], atualização Olá *uri* valor Olá *locationInfo* nó com hello URI do blob de ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="e99e0-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="e99e0-197">Olá URI é gerado pela combinação Olá *BaseLocation* e hello *RelativeLocation* da saída de saudação de saudação chamada novos treinamentos BES.</span><span class="sxs-lookup"><span data-stu-id="e99e0-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="e99e0-198">Importar Olá JSON para um objeto de definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="e99e0-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="e99e0-199">Você deve usar o hello [AzureRmMlWebService importação](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Olá modificado arquivo JSON de volta para um objeto de definição de serviço Web que você pode usar o experimento predicative do tooupdate Olá.</span><span class="sxs-lookup"><span data-stu-id="e99e0-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="e99e0-200">Olá web serviço de atualização</span><span class="sxs-lookup"><span data-stu-id="e99e0-200">Update hello web service</span></span>
<span data-ttu-id="e99e0-201">Por fim, use Olá [AzureRmMlWebService atualização](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate cmdlet Olá experiência previsível.</span><span class="sxs-lookup"><span data-stu-id="e99e0-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
