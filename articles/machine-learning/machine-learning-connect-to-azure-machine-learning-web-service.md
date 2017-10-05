---
title: "Conectar a um Serviço Web do Machine Learning | Microsoft Docs"
description: "Com C# ou Python, conecte a um serviço Web do Azure Machine Learning usando uma chave de autorização."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="60e4b-103">Conectar a um Serviço Web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60e4b-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="60e4b-104">A experiência do desenvolvedor do Azure Machine Learning é uma API de serviço Web para fazer previsões de dados de entrada em tempo real ou em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="60e4b-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="60e4b-105">Você pode usar o Azure Machine Learning Studio para criar previsões e implantar um serviço Web do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60e4b-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="60e4b-106">Para saber como criar e implantar um serviço Web do Azure Machine Learning usando o Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="60e4b-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="60e4b-107">Para obter um tutorial sobre como criar um teste no Machine Learning Studio, confira a seção [Crie seu primeiro experimento](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="60e4b-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="60e4b-108">Para obter detalhes sobre como implantar um serviço Web, confira [Implantar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="60e4b-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="60e4b-109">Para obter mais informações sobre o Machine Learning em geral, visite o [Centro de Documentação do Machine Learning do Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="60e4b-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="60e4b-110">Serviço Web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60e4b-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="60e4b-111">Com o serviço Web do Azure Machine Learning, um aplicativo externo se comunica com um modelo de pontuação do fluxo de trabalho do Machine Learning em tempo real.</span><span class="sxs-lookup"><span data-stu-id="60e4b-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="60e4b-112">Uma chamada do serviço Web do Machine Learning retorna resultados de previsão para um aplicativo externo.</span><span class="sxs-lookup"><span data-stu-id="60e4b-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="60e4b-113">Para fazer uma chamada de serviço Web do Machine Learning, transmita uma chave de API que é criada quando você implanta uma previsão.</span><span class="sxs-lookup"><span data-stu-id="60e4b-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="60e4b-114">O serviço Web do Machine Learning baseia-se em REST, uma opção popular de arquitetura para projetos de programação da Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="60e4b-115">O Azure Machine Learning tem dois tipos de serviços:</span><span class="sxs-lookup"><span data-stu-id="60e4b-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="60e4b-116">Serviço de Solicitação-Resposta (RRS) – Um serviço de baixa latência e altamente escalonável que fornece uma interface para os modelos sem monitoração de estado criados e implantados no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="60e4b-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="60e4b-117">Serviço de Execução de Lote (BES) – Um serviço assíncrono que pontua um lote de registros de dados.</span><span class="sxs-lookup"><span data-stu-id="60e4b-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="60e4b-118">Para obter mais informações sobre os serviços Web do Machine Learning, confira [Implantar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="60e4b-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="60e4b-119">Obtenha uma chave de autorização de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60e4b-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="60e4b-120">Quando você implanta seu experimento, as chaves de API são geradas para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="60e4b-121">Você pode recuperar as chaves de vários locais.</span><span class="sxs-lookup"><span data-stu-id="60e4b-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="60e4b-122">Por meio do portal de serviços Web do Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60e4b-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="60e4b-123">Entre no portal [Serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="60e4b-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="60e4b-124">Para recuperar a chave de API para um novo serviço Web do Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="60e4b-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="60e4b-125">No portal de serviços Web do Azure Machine Learning, clique em **Serviços Web** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="60e4b-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="60e4b-126">Clique no serviço Web para o qual deseja recuperar a chave.</span><span class="sxs-lookup"><span data-stu-id="60e4b-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="60e4b-127">No menu superior, clique em **Consumir**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="60e4b-128">Copie e salve a **Chave Primária**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="60e4b-129">Para recuperar a chave de API para um serviço Web clássico do Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="60e4b-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="60e4b-130">No portal de serviços Web do Azure Machine Learning, clique em **Serviços Web Clássicos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="60e4b-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="60e4b-131">Clique no serviço Web com o qual está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="60e4b-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="60e4b-132">Clique no ponto de extremidade para o qual deseja recuperar a chave.</span><span class="sxs-lookup"><span data-stu-id="60e4b-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="60e4b-133">No menu superior, clique em **Consumir**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="60e4b-134">Copie e salve a **Chave Primária**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="60e4b-135">Serviço Web Clássico</span><span class="sxs-lookup"><span data-stu-id="60e4b-135">Classic Web service</span></span>
 <span data-ttu-id="60e4b-136">Você também pode recuperar uma chave para um serviço Web Clássico por meio do Machine Learning Studio ou do Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="60e4b-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="60e4b-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="60e4b-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="60e4b-138">No Machine Learning Studio, clique em **SERVIÇOS WEB** à esquerda.</span><span class="sxs-lookup"><span data-stu-id="60e4b-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="60e4b-139">Clique em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-139">Click a Web service.</span></span> <span data-ttu-id="60e4b-140">A **Chave de API** está na guia **PAINEL**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="60e4b-141">portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="60e4b-141">Azure classic portal</span></span>
1. <span data-ttu-id="60e4b-142">Clique em **APRENDIZADO DE MÁQUINA** à esquerda.</span><span class="sxs-lookup"><span data-stu-id="60e4b-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="60e4b-143">Clique no espaço de trabalho no qual o serviço Web está localizado.</span><span class="sxs-lookup"><span data-stu-id="60e4b-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="60e4b-144">Clique em **SERVIÇOS WEB**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="60e4b-145">Clique em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-145">Click a Web service.</span></span>
5. <span data-ttu-id="60e4b-146">Clique em um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="60e4b-146">Click an endpoint.</span></span> <span data-ttu-id="60e4b-147">A “CHAVE DE API” está mais abaixo na parte inferior direita.</span><span class="sxs-lookup"><span data-stu-id="60e4b-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="60e4b-148"><a id="connect"></a>Conectar-se a um serviço Web do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60e4b-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="60e4b-149">Você pode se conectar a um serviço Web do Machine Learning usando qualquer linguagem de programação que dá suporte à resposta e à solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="60e4b-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="60e4b-150">Você pode exibir exemplos em C#, Python e R de uma página de ajuda do serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60e4b-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="60e4b-151">**Ajuda da API do Machine Learning** Uma ajuda de API do Machine Learning é criada quando você implanta um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="60e4b-152">Confira [Passo a passo do Azure Machine Learning – Implantar serviço Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="60e4b-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="60e4b-153">A ajuda da API do Machine Learning contém detalhes sobre um serviço Web de previsão.</span><span class="sxs-lookup"><span data-stu-id="60e4b-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="60e4b-154">Clique no serviço Web com o qual está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="60e4b-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="60e4b-155">Clique no ponto de extremidade para o qual deseja exibir uma página de ajuda da API.</span><span class="sxs-lookup"><span data-stu-id="60e4b-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="60e4b-156">No menu superior, clique em **Consumir**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="60e4b-157">Clique na **página de ajuda da API** nos pontos de extremidade Solicitação de Resposta ou Execução em Lote.</span><span class="sxs-lookup"><span data-stu-id="60e4b-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="60e4b-158">**Como exibir a ajuda da API do Machine Learning para um novo serviço Web**</span><span class="sxs-lookup"><span data-stu-id="60e4b-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="60e4b-159">No portal de serviços Web do Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="60e4b-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="60e4b-160">Clique em **SERVIÇOS WEB** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="60e4b-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="60e4b-161">Clique no serviço Web para o qual deseja recuperar a chave.</span><span class="sxs-lookup"><span data-stu-id="60e4b-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="60e4b-162">Clique em **Consumir** para obter os URIs dos serviços de Solicitação-Resposta e Execução em Lotes, bem como o código de exemplo em C#, R e Python.</span><span class="sxs-lookup"><span data-stu-id="60e4b-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="60e4b-163">Clique em **API do Swagger** para obter a documentação baseada no Swagger para as APIs chamadas dos URIs fornecidos.</span><span class="sxs-lookup"><span data-stu-id="60e4b-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="60e4b-164">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="60e4b-164">C# Sample</span></span>
<span data-ttu-id="60e4b-165">Para se conectar a um serviço Web do Machine Learning, use um **HttpClient** passando ScoreData.</span><span class="sxs-lookup"><span data-stu-id="60e4b-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="60e4b-166">ScoreData contém um FeatureVector, um vetor com n dimensões de recursos numéricos que representa o ScoreData.</span><span class="sxs-lookup"><span data-stu-id="60e4b-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="60e4b-167">Autentique no serviço de Machine Learning com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="60e4b-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="60e4b-168">Para se conectar a um serviço Web do Machine Learning, o pacote Nuget **Microsoft.AspNet.WebApi.Client** deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="60e4b-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="60e4b-169">**Instalar o Nuget Microsoft.AspNet.WebApi.Client no Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="60e4b-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="60e4b-170">Publique “Baixe o conjunto de dados de Download de UCI: Serviço Web do conjunto de dados da classe Adulto 2”.</span><span class="sxs-lookup"><span data-stu-id="60e4b-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="60e4b-171">Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="60e4b-172">Escolha **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="60e4b-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="60e4b-173">**Para executar o exemplo de código**</span><span class="sxs-lookup"><span data-stu-id="60e4b-173">**To run the code sample**</span></span>

1. <span data-ttu-id="60e4b-174">Publique o experimento “Exemplo 1: Baixe o conjunto de dados de UCI: conjunto de dados da classe Adulto 2”, parte da coleção de exemplos de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60e4b-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="60e4b-175">Atribua apiKey com a chave de um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="60e4b-176">Confira a seção acima **Obter uma chave de autorização de Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="60e4b-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="60e4b-177">Atribua serviceUri com o URI de solicitação.</span><span class="sxs-lookup"><span data-stu-id="60e4b-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="60e4b-178">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="60e4b-178">Python Sample</span></span>
<span data-ttu-id="60e4b-179">Para se conectar a um serviço Web do Machine Learning, use a biblioteca **urllib2** passando ScoreData.</span><span class="sxs-lookup"><span data-stu-id="60e4b-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="60e4b-180">ScoreData contém um FeatureVector, um vetor com n dimensões de recursos numéricos que representa o ScoreData.</span><span class="sxs-lookup"><span data-stu-id="60e4b-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="60e4b-181">Autentique no serviço de Machine Learning com uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="60e4b-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="60e4b-182">**Para executar o exemplo de código**</span><span class="sxs-lookup"><span data-stu-id="60e4b-182">**To run the code sample**</span></span>

1. <span data-ttu-id="60e4b-183">Implante o experimento "Exemplo 1: Baixe o conjunto de dados de UCI: conjunto de dados da classe Adulto 2", parte da coleção de exemplos de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60e4b-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="60e4b-184">Atribua apiKey com a chave de um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="60e4b-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="60e4b-185">Consulte a seção **Obter uma chave de autorização do Azure Machine Learning** perto do início deste artigo.</span><span class="sxs-lookup"><span data-stu-id="60e4b-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="60e4b-186">Atribua serviceUri com o URI de solicitação.</span><span class="sxs-lookup"><span data-stu-id="60e4b-186">Assign serviceUri with the Request URI.</span></span>

