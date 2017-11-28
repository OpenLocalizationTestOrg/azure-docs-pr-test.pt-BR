---
title: "aaaHow tooconsume um serviço Web de aprendizado de máquina do Azure | Microsoft Docs"
description: "Depois que um serviço de aprendizado de máquina é implantado, Olá serviço Web RESTFul que se tornam disponível pode ser consumido como serviço de solicitação-resposta em tempo real ou como um serviço de execução de lote."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a><span data-ttu-id="7676e-103">Como tooconsume um serviço Web de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="7676e-103">How tooconsume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="7676e-104">Depois de implantar um modelo de previsão de aprendizado de máquina do Azure como um serviço Web, você pode usar uma API REST toosend ele dados e obter previsões.</span><span class="sxs-lookup"><span data-stu-id="7676e-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API toosend it data and get predictions.</span></span> <span data-ttu-id="7676e-105">Você pode enviar dados saudação em tempo real ou em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="7676e-105">You can send hello data in real-time or in batch mode.</span></span>

<span data-ttu-id="7676e-106">Você pode encontrar mais informações sobre como toocreate e implantar um serviço Web de aprendizado de máquina usando o estúdio de aprendizado de máquina aqui:</span><span class="sxs-lookup"><span data-stu-id="7676e-106">You can find more information about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="7676e-107">Para obter um tutorial sobre como toocreate um experimento no estúdio de aprendizado de máquina, consulte [criar sua primeira experiência](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="7676e-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="7676e-108">Para obter detalhes sobre como toodeploy um serviço Web, consulte [implantar um serviço Web de aprendizado de máquina](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7676e-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="7676e-109">Para obter mais informações sobre o aprendizado de máquina em geral, visite Olá [Centro de documentação de aprendizado de máquina](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="7676e-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="7676e-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7676e-110">Overview</span></span>
<span data-ttu-id="7676e-111">Com hello serviço da Web de aprendizado de máquina do Azure, um aplicativo externo se comunica com um modelo de pontuação de fluxo de trabalho do aprendizado de máquina em tempo real.</span><span class="sxs-lookup"><span data-stu-id="7676e-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="7676e-112">Uma chamada de serviço Web de aprendizado de máquina retorna resultados da previsão aplicativo externo tooan.</span><span class="sxs-lookup"><span data-stu-id="7676e-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="7676e-113">toomake uma chamada de serviço Web de aprendizado de máquina, você passar uma chave de API que é criada quando você implanta uma previsão.</span><span class="sxs-lookup"><span data-stu-id="7676e-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="7676e-114">Olá serviço Web de aprendizado de máquina é baseado em REST, uma opção de populares de arquitetura para projetos de programação da web.</span><span class="sxs-lookup"><span data-stu-id="7676e-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="7676e-115">O Azure Machine Learning tem dois tipos de serviços:</span><span class="sxs-lookup"><span data-stu-id="7676e-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="7676e-116">Serviço de solicitação-resposta (RR) – uma baixa latência, um serviço altamente escalonável que fornece uma interface modelos sem monitoração de estado de toohello criado e implantado a partir de saudação estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="7676e-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="7676e-117">Serviço de Execução de Lote (BES) – Um serviço assíncrono que pontua um lote de registros de dados.</span><span class="sxs-lookup"><span data-stu-id="7676e-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="7676e-118">Para obter mais informações sobre os serviços Web do Machine Learning, confira [Implantar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7676e-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="7676e-119">Obtenha uma chave de autorização de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7676e-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="7676e-120">Quando você implanta sua experiência, chaves de API são geradas para Olá serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="7676e-121">Você pode recuperar chaves de saudação em vários locais.</span><span class="sxs-lookup"><span data-stu-id="7676e-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="7676e-122">No portal de serviços Web de aprendizado de máquina do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="7676e-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="7676e-123">Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="7676e-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="7676e-124">chave de API de saudação tooretrieve para um serviço Web de aprendizado de máquina novo:</span><span class="sxs-lookup"><span data-stu-id="7676e-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="7676e-125">No portal de serviços de Web de aprendizado de máquina do Azure hello, clique em **serviços Web** menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="7676e-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="7676e-126">Clique em Olá Web service para o qual deseja que o tooretrieve Olá da chave.</span><span class="sxs-lookup"><span data-stu-id="7676e-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="7676e-127">Clique no menu superior Olá **consumir**.</span><span class="sxs-lookup"><span data-stu-id="7676e-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="7676e-128">Copie e salve Olá **chave primária**.</span><span class="sxs-lookup"><span data-stu-id="7676e-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="7676e-129">chave de API de saudação tooretrieve para um serviço Web de aprendizado de máquina clássico:</span><span class="sxs-lookup"><span data-stu-id="7676e-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="7676e-130">No portal de serviços de Web de aprendizado de máquina do Azure hello, clique em **Web Services clássico** menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="7676e-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="7676e-131">Clique em Olá Web service com a qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="7676e-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="7676e-132">Clique em ponto de extremidade de saudação do qual você deseja tooretrieve chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="7676e-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="7676e-133">Clique no menu superior Olá **consumir**.</span><span class="sxs-lookup"><span data-stu-id="7676e-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="7676e-134">Copie e salve Olá **chave primária**.</span><span class="sxs-lookup"><span data-stu-id="7676e-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="7676e-135">Serviço Web Clássico</span><span class="sxs-lookup"><span data-stu-id="7676e-135">Classic Web service</span></span>
 <span data-ttu-id="7676e-136">Você também pode recuperar uma chave para um serviço Web clássico do estúdio de aprendizado de máquina ou hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="7676e-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="7676e-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="7676e-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="7676e-138">No estúdio de aprendizado de máquina, clique em **serviços WEB** Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="7676e-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="7676e-139">Clique em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-139">Click a Web service.</span></span> <span data-ttu-id="7676e-140">Olá **chave API** está em Olá **painel** guia.</span><span class="sxs-lookup"><span data-stu-id="7676e-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="7676e-141">portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7676e-141">Azure classic portal</span></span>
1. <span data-ttu-id="7676e-142">Clique em **APRENDIZADO de máquina** Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="7676e-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="7676e-143">Clique em espaço de trabalho de saudação em que o serviço da Web está localizado.</span><span class="sxs-lookup"><span data-stu-id="7676e-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="7676e-144">Clique em **SERVIÇOS WEB**.</span><span class="sxs-lookup"><span data-stu-id="7676e-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="7676e-145">Clique em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-145">Click a Web service.</span></span>
5. <span data-ttu-id="7676e-146">Clique em um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7676e-146">Click an endpoint.</span></span> <span data-ttu-id="7676e-147">Olá "Chave de API" está inativo no hello inferior direito.</span><span class="sxs-lookup"><span data-stu-id="7676e-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="7676e-148"><a id="connect"></a>Conecte-se o serviço da Web de aprendizado de máquina de tooa</span><span class="sxs-lookup"><span data-stu-id="7676e-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="7676e-149">Você pode conectar tooa serviço Web de aprendizado de máquina usando qualquer linguagem de programação que dá suporte à resposta e solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="7676e-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="7676e-150">Você pode exibir exemplos em C#, Python e R de uma página de ajuda do serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7676e-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="7676e-151">**Ajuda da API do Machine Learning** Uma ajuda de API do Machine Learning é criada quando você implanta um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="7676e-152">Confira [Passo a passo do Azure Machine Learning – Implantar serviço Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7676e-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="7676e-153">Olá ajuda da API de aprendizado de máquina contém detalhes sobre um serviço Web de previsão.</span><span class="sxs-lookup"><span data-stu-id="7676e-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="7676e-154">Clique em Olá Web service com a qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="7676e-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="7676e-155">Clique em ponto de extremidade de saudação do qual você deseja tooview Olá a página de ajuda de API.</span><span class="sxs-lookup"><span data-stu-id="7676e-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="7676e-156">Clique no menu superior Olá **consumir**.</span><span class="sxs-lookup"><span data-stu-id="7676e-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="7676e-157">Clique em **página de Ajuda da API** em Olá solicitação-resposta ou pontos de extremidade de execução de lote.</span><span class="sxs-lookup"><span data-stu-id="7676e-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="7676e-158">**ajudar a API de aprendizado de máquina tooview para um serviço Web de novo**</span><span class="sxs-lookup"><span data-stu-id="7676e-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="7676e-159">Em hello Azure Machine Learning Web Services Portal:</span><span class="sxs-lookup"><span data-stu-id="7676e-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="7676e-160">Clique em **serviços WEB** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="7676e-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="7676e-161">Clique em Olá Web service para o qual deseja que o tooretrieve Olá da chave.</span><span class="sxs-lookup"><span data-stu-id="7676e-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="7676e-162">Clique em **consumir** tooget hello URIs para hello Reposonse de solicitação e serviços de execução de lote e código de exemplo em c#, R e Python.</span><span class="sxs-lookup"><span data-stu-id="7676e-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="7676e-163">Clique em **Swagger API** tooget Swagger documentação com base para Olá APIs chamada de hello fornecido URIs.</span><span class="sxs-lookup"><span data-stu-id="7676e-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="7676e-164">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="7676e-164">C# Sample</span></span>
<span data-ttu-id="7676e-165">tooconnect tooa serviço Web de aprendizado de máquina, use uma **HttpClient** passando ScoreData.</span><span class="sxs-lookup"><span data-stu-id="7676e-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="7676e-166">ScoreData contém um FeatureVector, um vetor de n-dimensional de recursos numéricos que representa Olá ScoreData.</span><span class="sxs-lookup"><span data-stu-id="7676e-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="7676e-167">Autenticar o serviço de aprendizado de máquina toohello com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="7676e-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="7676e-168">Olá tooconnect tooa serviço Web de aprendizado de máquina, **Microsoft.AspNet.WebApi.Client** pacote NuGet deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="7676e-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="7676e-169">**Instalar o Nuget Microsoft.AspNet.WebApi.Client no Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="7676e-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="7676e-170">Publicar o conjunto de dados de Download de saudação do UCI: 2 adulto classe dataset serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="7676e-171">Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="7676e-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="7676e-172">Escolha **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="7676e-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="7676e-173">**exemplo de código toorun Olá**</span><span class="sxs-lookup"><span data-stu-id="7676e-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="7676e-174">Publicar "exemplo 1: baixar o conjunto de dados do UCI: conjunto de dados de classe adulto 2" experimento, parte da saudação coleção de aprendizado de máquina de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7676e-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="7676e-175">Atribua apiKey com chave de saudação de um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="7676e-176">Confira a seção acima **Obter uma chave de autorização de Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="7676e-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="7676e-177">Atribua serviceUri com hello URI da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7676e-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="7676e-178">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="7676e-178">Python Sample</span></span>
<span data-ttu-id="7676e-179">tooconnect tooa serviço Web de aprendizado de máquina, use Olá **urllib2** passando ScoreData de biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7676e-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="7676e-180">ScoreData contém um FeatureVector, um vetor de n-dimensional de recursos numéricos que representa Olá ScoreData.</span><span class="sxs-lookup"><span data-stu-id="7676e-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="7676e-181">Autenticar o serviço de aprendizado de máquina toohello com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="7676e-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="7676e-182">**exemplo de código toorun Olá**</span><span class="sxs-lookup"><span data-stu-id="7676e-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="7676e-183">Implantar "exemplo 1: baixar o conjunto de dados do UCI: conjunto de dados de classe adulto 2" experimento, parte da saudação coleção de aprendizado de máquina de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7676e-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="7676e-184">Atribua apiKey com chave de saudação de um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7676e-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="7676e-185">Consulte Olá **obter uma chave de autorização de aprendizado de máquina do Azure** seção próximo início Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7676e-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="7676e-186">Atribua serviceUri com hello URI da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7676e-186">Assign serviceUri with hello Request URI.</span></span>

