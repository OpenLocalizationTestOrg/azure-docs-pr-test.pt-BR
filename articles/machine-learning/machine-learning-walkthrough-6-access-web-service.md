---
title: "Etapa 6: Acessar o serviço da Web de aprendizado de máquina de saudação | Microsoft Docs"
description: "Etapa 6 do hello desenvolver um passo a passo de solução de previsão: acessar um serviço Web de aprendizado de máquina do Azure ativo."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="8f796-103">Etapa 6 do passo a passo: Saudação de acesso serviço web de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="8f796-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="8f796-104">Esta é a última etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="8f796-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. <span data-ttu-id="8f796-105">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="8f796-105">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="8f796-106">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="8f796-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="8f796-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="8f796-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="8f796-108">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="8f796-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="8f796-109">Implantar o serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="8f796-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="8f796-110">**Acessar o serviço Web Olá**</span><span class="sxs-lookup"><span data-stu-id="8f796-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="8f796-111">Na etapa anterior de saudação neste passo a passo é implantado um serviço web que usa o nosso modelo de previsão de risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="8f796-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="8f796-112">Agora os usuários são capazes de toosend dados tooit e recebem resultados.</span><span class="sxs-lookup"><span data-stu-id="8f796-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="8f796-113">Olá serviço Web é um serviço web do Azure que pode receber e retornar dados usando APIs REST de uma das duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="8f796-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="8f796-114">**Solicitação/resposta** - usuário Olá envia uma ou mais linhas de crédito toohello de dados de serviço usando um protocolo HTTP e Olá serviço responde com um ou mais conjuntos de resultados.</span><span class="sxs-lookup"><span data-stu-id="8f796-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="8f796-115">**Execução em lote** - usuário Olá armazena uma ou mais linhas de dados de crédito em um Azure blob e, em seguida, envia o serviço de toohello Olá blob local.</span><span class="sxs-lookup"><span data-stu-id="8f796-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="8f796-116">Olá de pontuações de serviço Olá que todos Olá linhas de dados no blob de entrada, repositórios hello resulta em outro blob e retorna Olá URL do contêiner.</span><span class="sxs-lookup"><span data-stu-id="8f796-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="8f796-117">Olá tooaccess de maneira mais rápida e fácil um serviço da web clássico é por meio de saudação [aplicativo Web de serviço de solicitação-resposta do Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) ou [modelo de aplicativo do Azure ML lote execução do serviço Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="8f796-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="8f796-118">Esses modelos de aplicativo Web podem compilar um aplicativo Web personalizado que conhece os dados de entrada do seu serviço Web e o que ele retornará.</span><span class="sxs-lookup"><span data-stu-id="8f796-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="8f796-119">Você só precisa toodo é fornecer acesso tooyour web serviço e os dados e modelo Olá Olá rest.</span><span class="sxs-lookup"><span data-stu-id="8f796-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="8f796-120">Para obter mais informações sobre como usar modelos de aplicativo web hello, consulte [consumir um serviço Web de aprendizado de máquina do Azure com um modelo de aplicativo da web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="8f796-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="8f796-121">Você também pode desenvolver um aplicativo personalizado tooaccess Olá web service usando código inicial fornecido em R, c# e linguagens de programação Python.</span><span class="sxs-lookup"><span data-stu-id="8f796-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="8f796-122">Você pode encontrar detalhes completos em [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="8f796-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

