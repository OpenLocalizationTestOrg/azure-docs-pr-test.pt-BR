---
title: "aaaCreate vários modelos de um experimento | Microsoft Docs"
description: "Usar o PowerShell toocreate vários modelos de aprendizado de máquina e web pontos de extremidade de serviço com hello mesmo algoritmo, mas conjuntos de dados de treinamento diferentes."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="ba55b-103">Criar vários modelos do Machine Learning e pontos de extremidade de serviço Web com base em um teste usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba55b-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="ba55b-104">Este é um problema comum de aprendizado de máquina: deseja toocreate muitos modelos que têm Olá mesmo fluxo de trabalho de treinamento e use Olá mesmo algoritmo, mas têm conjuntos de dados de treinamento diferentes como entrada.</span><span class="sxs-lookup"><span data-stu-id="ba55b-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="ba55b-105">Este artigo mostra como toodo isso em grande escala no estúdio de aprendizado de máquina do Azure usando apenas uma única experiência.</span><span class="sxs-lookup"><span data-stu-id="ba55b-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="ba55b-106">Por exemplo, digamos que você tenha um negócio de franquia mundial de aluguel de bicicletas.</span><span class="sxs-lookup"><span data-stu-id="ba55b-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="ba55b-107">Você deseja toobuild uma demanda de aluguel regressão modelo toopredict Olá com base em dados históricos.</span><span class="sxs-lookup"><span data-stu-id="ba55b-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="ba55b-108">Você tem 1.000 locais de aluguel em Olá, mundo e coletados um conjunto de dados para cada local que inclui recursos importantes, como data, hora, clima e tráfego local tooeach específico.</span><span class="sxs-lookup"><span data-stu-id="ba55b-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="ba55b-109">Você pode treinar seu modelo uma vez usando uma versão mesclada de todos os conjuntos de dados de saudação em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="ba55b-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="ba55b-110">Mas como cada um dos seus locais tem um ambiente exclusivo, uma abordagem melhor seria ser tootrain seu modelo de regressão separadamente usando o conjunto de dados Olá para cada local.</span><span class="sxs-lookup"><span data-stu-id="ba55b-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="ba55b-111">Dessa forma, cada modelo treinado pode levar em tamanhos de armazenamento diferente do conta hello, volume, geografia, população, ambiente de tráfego de bicicleta amigável, *etc.*.</span><span class="sxs-lookup"><span data-stu-id="ba55b-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="ba55b-112">Que pode ser uma abordagem melhor hello, mas não desejar toocreate 1.000 experiências de treinamento no aprendizado de máquina do Azure com cada um representando um local exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ba55b-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="ba55b-113">Além de ser uma tarefa difícil, também é parece muito ineficiente, pois cada teste teria que todos os Olá mesmos componentes, exceto o conjunto de dados de treinamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba55b-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="ba55b-114">Felizmente, é possível fazer isso usando Olá [treinamento API de aprendizado de máquina do Azure](machine-learning-retrain-models-programmatically.md) e automatizar tarefas de saudação com [PowerShell de aprendizado de máquina do Azure](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="ba55b-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba55b-115">toomake nossa amostra executado mais rapidamente, podemos será reduzir o número de Olá dos locais de too10 1.000.</span><span class="sxs-lookup"><span data-stu-id="ba55b-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="ba55b-116">Mas hello mesmos princípios e procedimentos se aplicam too1, 000 locais.</span><span class="sxs-lookup"><span data-stu-id="ba55b-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="ba55b-117">Olá única diferença é que se você quiser tootrain de 1.000 conjuntos de dados provavelmente deseja toothink da execução Olá scripts do PowerShell em paralelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba55b-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="ba55b-118">Como toodo está além do escopo de saudação neste artigo, mas você pode encontrar exemplos do PowerShell multi-thread na saudação da Internet.</span><span class="sxs-lookup"><span data-stu-id="ba55b-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="ba55b-119">Configurar a experiência de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="ba55b-119">Set up hello training experiment</span></span>
<span data-ttu-id="ba55b-120">Vamos toouse um exemplo [experiência de treinamento](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que já criamos em Olá [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="ba55b-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ba55b-121">Abra esse teste em seu espaço de trabalho do [Azure Machine Learning Studio](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="ba55b-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="ba55b-122">Ordem toofollow junto com este exemplo, convém toouse um espaço de trabalho padrão em vez de um espaço de trabalho grátis.</span><span class="sxs-lookup"><span data-stu-id="ba55b-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="ba55b-123">Podemos criará um ponto de extremidade para cada cliente - para um total de 10 pontos de extremidade - e isso, é necessário um espaço de trabalho padrão como um espaço de trabalho gratuito é limitada too3 pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ba55b-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="ba55b-124">Se você tiver apenas um espaço de trabalho grátis, modifique os scripts de saudação abaixo tooallow para apenas 3 locais apenas.</span><span class="sxs-lookup"><span data-stu-id="ba55b-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="ba55b-125">experiência de saudação usa um **importar dados** conjunto de dados de treinamento do módulo tooimport Olá *customer001.csv* de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba55b-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="ba55b-126">Vamos supor que temos coletados conjuntos de dados de treinamento de todos os locais de aluguel de bicicleta e armazenou em Olá mesmo local de armazenamento de blob com nomes de arquivo que variam de *rentalloc001.csv* muito*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="ba55b-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="ba55b-128">Observe que uma **saída do serviço Web** módulo foi adicionado toohello **treinar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="ba55b-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="ba55b-129">Quando esse teste é implantado como um serviço web, o ponto de extremidade de saudação associado a essa saída retornará treinado Olá no formato de saudação de um arquivo de .ilearner.</span><span class="sxs-lookup"><span data-stu-id="ba55b-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="ba55b-130">Observe também que configuramos um parâmetro de serviço da web para a URL de saudação que Olá **importar dados** módulo usa.</span><span class="sxs-lookup"><span data-stu-id="ba55b-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="ba55b-131">Isso nos permite toouse Olá parâmetro toospecify individuais conjuntos de dados tootrain Olá modelo de treinamento para cada local.</span><span class="sxs-lookup"><span data-stu-id="ba55b-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="ba55b-132">Existem outras maneiras poderíamos ter feito isso, como usando uma consulta SQL com um web serviço parâmetro tooget os dados de um banco de dados do SQL Azure, ou simplesmente um **entrada de serviço Web** toopass de módulo em um conjunto de dados toohello de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="ba55b-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="ba55b-134">Agora, vamos executar esse teste de treinamento usando o valor padrão de saudação *rental001.csv* como Olá conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="ba55b-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="ba55b-135">Se você exibir saída Olá Olá **avaliar** módulo (clique em saída hello e selecione **visualizar**), você pode ver, obtemos um desempenho razoável de *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="ba55b-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="ba55b-136">Neste ponto, estamos pronto toodeploy um serviço web sem esse teste de treinamento.</span><span class="sxs-lookup"><span data-stu-id="ba55b-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="ba55b-137">Implantar serviços web de classificação e treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="ba55b-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="ba55b-138">Olá toodeploy treinamento de serviço da web, clique em Olá **configurar o serviço Web** abaixo da tela de experimento hello e selecione **implantar o serviço da Web**.</span><span class="sxs-lookup"><span data-stu-id="ba55b-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="ba55b-139">Chame esse serviço Web de “Treinamento do Aluguel de Bicicletas”.</span><span class="sxs-lookup"><span data-stu-id="ba55b-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="ba55b-140">Agora precisamos de serviço de web toodeploy Olá pontuação.</span><span class="sxs-lookup"><span data-stu-id="ba55b-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="ba55b-141">toodo, clicamos **configurar o serviço Web** abaixo Olá tela e selecione **previsão Web Service**.</span><span class="sxs-lookup"><span data-stu-id="ba55b-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="ba55b-142">Isso criará um teste de pontuação.</span><span class="sxs-lookup"><span data-stu-id="ba55b-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="ba55b-143">Vamos precisar toomake alguns toomake pequenos ajustes ele funciona como um serviço web, tais como dados de entrada a remoção de coluna de rótulo hello "cnt" hello e limitar Olá correspondente e o id da instância Olá Olá saída tooonly previu o valor.</span><span class="sxs-lookup"><span data-stu-id="ba55b-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="ba55b-144">toosave que trabalhar, basta abrir Olá [experimento previsão](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) em Olá Galeria já foi preparado.</span><span class="sxs-lookup"><span data-stu-id="ba55b-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="ba55b-145">serviço de web hello toodeploy, executar teste de previsão hello, clique em Olá **implantar o serviço da Web** botão abaixo tela hello.</span><span class="sxs-lookup"><span data-stu-id="ba55b-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="ba55b-146">Saudação de nome serviço web "Bicicleta aluguel de pontuação" de pontuação ".</span><span class="sxs-lookup"><span data-stu-id="ba55b-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="ba55b-147">Criar 10 pontos de extremidade de serviço Web idênticos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba55b-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="ba55b-148">Este serviço Web é fornecido com um ponto de extremidade padrão.</span><span class="sxs-lookup"><span data-stu-id="ba55b-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="ba55b-149">Mas não estamos tão interessados no ponto de extremidade saudação padrão porque ele não pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="ba55b-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="ba55b-150">O que devemos toodo é toocreate 10 pontos de extremidade adicionais, uma para cada local.</span><span class="sxs-lookup"><span data-stu-id="ba55b-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="ba55b-151">Faremos isso com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba55b-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="ba55b-152">Primeiro, configuramos nosso ambiente do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ba55b-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="ba55b-153">Em seguida, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="ba55b-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="ba55b-154">Agora, criamos 10 pontos de extremidade e contiverem Olá mesmo modelo treinado treinado em *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="ba55b-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="ba55b-155">Você pode exibi-los no Portal de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba55b-155">You can view them in hello Azure Management Portal.</span></span>

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="ba55b-157">Atualizar Olá pontos de extremidade toouse treinamento separado conjuntos de dados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba55b-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="ba55b-158">Olá próxima etapa é tooupdate pontos de extremidade de saudação com modelos treinados exclusivamente nos dados de cada cliente individual.</span><span class="sxs-lookup"><span data-stu-id="ba55b-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="ba55b-159">Mas primeiro é preciso tooproduce esses modelos de saudação **treinamento de aluguel de bicicleta** serviço web.</span><span class="sxs-lookup"><span data-stu-id="ba55b-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="ba55b-160">Vamos voltar toohello **treinamento de aluguel de bicicleta** serviço web.</span><span class="sxs-lookup"><span data-stu-id="ba55b-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="ba55b-161">Precisamos toocall seu ponto de extremidade do BES 10 vezes com 10 conjuntos de dados de treinamento diferentes em modelos diferentes de tooproduce 10 de ordem.</span><span class="sxs-lookup"><span data-stu-id="ba55b-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="ba55b-162">Vamos usar Olá **InovkeAmlWebServiceBESEndpoint** toodo de cmdlet do PowerShell isso.</span><span class="sxs-lookup"><span data-stu-id="ba55b-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="ba55b-163">Você também precisará de credenciais tooprovide para sua conta de armazenamento de blob em `$configContent`, ou seja, os campos de saudação `AccountName`, `AccountKey` e `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="ba55b-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="ba55b-164">Olá `AccountName` pode ser um dos seus nomes de conta, como visto no hello **Portal de gerenciamento clássico do Azure** (*armazenamento* guia).</span><span class="sxs-lookup"><span data-stu-id="ba55b-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="ba55b-165">Depois que você clicar em uma conta de armazenamento, seu `AccountKey` podem ser encontrados ao pressionar Olá **gerenciar chaves de acesso** botão inferior hello e copiando Olá *chave de acesso primário*.</span><span class="sxs-lookup"><span data-stu-id="ba55b-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="ba55b-166">Olá `RelativeLocation` é Olá caminho relativo tooyour armazenamento onde um novo modelo será armazenado.</span><span class="sxs-lookup"><span data-stu-id="ba55b-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="ba55b-167">Por exemplo, o caminho Olá `hai/retrain/bike_rental/` no script hello abaixo pontos tooa contêiner nomeado `hai`, e `/retrain/bike_rental/` são subpastas.</span><span class="sxs-lookup"><span data-stu-id="ba55b-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="ba55b-168">Atualmente, não é possível criar subpastas por meio da interface do usuário do portal hello, mas há [vários gerenciadores de armazenamento do Azure](../storage/common/storage-explorers.md) que permitem que você toodo assim.</span><span class="sxs-lookup"><span data-stu-id="ba55b-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="ba55b-169">É recomendável que você crie um novo contêiner no seu Olá toostore de armazenamento novos modelos treinados (arquivos .ilearner) da seguinte maneira: sua página de armazenamento, clique em Olá **adicionar** botão na parte inferior do hello e nomeie-o `retrain`.</span><span class="sxs-lookup"><span data-stu-id="ba55b-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="ba55b-170">Em resumo, o script do toohello alterações necessárias Olá abaixo pertencem muito`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="ba55b-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="ba55b-171">Olá ponto de extremidade do BES é Olá só tem suporte modo para esta operação.</span><span class="sxs-lookup"><span data-stu-id="ba55b-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="ba55b-172">O RRS não pode ser usado para a produção de modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="ba55b-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="ba55b-173">Como você pode ver acima, em vez de criar 10 diferentes BES trabalho json arquivos de configuração, criamos dinamicamente cadeia de caracteres de configuração de saudação em vez disso e inseri-la toohello *jobConfigString* parâmetro hello  **InvokeAmlWebServceBESEndpoint** cmdlet, porque não há realmente nenhum tookeep da necessidade de uma cópia em disco.</span><span class="sxs-lookup"><span data-stu-id="ba55b-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="ba55b-174">Se tudo correr bem, após alguns instantes verá 10 arquivos .ilearner, de *model001.ilearner* muito*model010.ilearner*, em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba55b-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="ba55b-175">Agora estamos pronto tooupdate nosso 10 da web de pontuação pontos de extremidade de serviço com esses modelos usando Olá **AmlWebServiceEndpoint Patch** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba55b-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="ba55b-176">Lembre-se novamente de que podemos pode patch apenas pontos de extremidade não padrão Olá que programaticamente criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ba55b-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="ba55b-177">Isso deverá ser executado rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ba55b-177">This should run fairly quickly.</span></span> <span data-ttu-id="ba55b-178">Ao término da execução de hello, podemos será criou com êxito pontos de extremidade de serviço de web de previsão 10, cada uma contendo um modelo treinado exclusivamente treinado em Olá conjunto de dados específico tooa aluguel local, tudo a partir de uma experiência de treinamento único.</span><span class="sxs-lookup"><span data-stu-id="ba55b-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="ba55b-179">tooverify isso, você pode tentar chamar esses pontos de extremidade usando Olá **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornecendo a eles com hello mesmo dados de entrada e você deve esperar resultados de previsão diferentes toosee como modelos de saudação são treinado com conjuntos de treinamento diferentes.</span><span class="sxs-lookup"><span data-stu-id="ba55b-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="ba55b-180">Script completo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba55b-180">Full PowerShell script</span></span>
<span data-ttu-id="ba55b-181">Aqui está uma listagem de saudação do código-fonte completo hello:</span><span class="sxs-lookup"><span data-stu-id="ba55b-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
