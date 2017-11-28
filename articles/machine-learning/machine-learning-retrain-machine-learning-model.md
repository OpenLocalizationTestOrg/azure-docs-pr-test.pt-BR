---
title: "um modelo de aprendizado de máquina do aaaRetrain | Microsoft Docs"
description: "Saiba como tooretrain um modelo e atualização Olá Web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="fb358-103">Readaptar um modelo do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fb358-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="fb358-104">Como parte do processo de saudação do operacionalização de modelos de aprendizado de máquina no aprendizado de máquina do Azure, o modelo é treinado e salvo.</span><span class="sxs-lookup"><span data-stu-id="fb358-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="fb358-105">Em seguida, use-toocreate um serviço Web predicative.</span><span class="sxs-lookup"><span data-stu-id="fb358-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="fb358-106">saudação de serviço da Web pode ser consumida em sites da web, painéis e aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="fb358-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="fb358-107">Os modelos que você cria usando o Machine Learning geralmente não são estáticos.</span><span class="sxs-lookup"><span data-stu-id="fb358-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="fb358-108">À medida que novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seu próprio modelo de saudação de dados precisa toobe treinados novamente.</span><span class="sxs-lookup"><span data-stu-id="fb358-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="fb358-109">A readaptação pode ocorrer com frequência.</span><span class="sxs-lookup"><span data-stu-id="fb358-109">Retraining may occur frequently.</span></span> <span data-ttu-id="fb358-110">Com recurso de programação API treinamento hello, programaticamente você pode treinar novamente modelo hello usando o serviço de Web de saudação de APIs de treinamento e de atualização de Olá Olá recentemente treinado.</span><span class="sxs-lookup"><span data-stu-id="fb358-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="fb358-111">Este documento descreve Olá processo de treinamento e mostra como toouse Olá APIs de treinamento.</span><span class="sxs-lookup"><span data-stu-id="fb358-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="fb358-112">Por que treinar novamente: definindo Olá problema</span><span class="sxs-lookup"><span data-stu-id="fb358-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="fb358-113">Como parte do processo de treinamento de aprendizado de máquina hello, um modelo é treinado usando um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="fb358-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="fb358-114">Os modelos que você cria usando o Machine Learning geralmente não são estáticos.</span><span class="sxs-lookup"><span data-stu-id="fb358-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="fb358-115">À medida que novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seu próprio modelo de saudação de dados precisa toobe treinados novamente.</span><span class="sxs-lookup"><span data-stu-id="fb358-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="fb358-116">Nesses cenários, uma API de programação fornece uma maneira conveniente de tooallow você ou hello consumidor de seu toocreate APIs um cliente que pode, em uma base única ou regular, treinar novamente modelo hello usando seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="fb358-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="fb358-117">Em seguida, podem avaliar os resultados de saudação do treinamento e atualizar Olá Web serviço API toouse Olá recentemente treinado.</span><span class="sxs-lookup"><span data-stu-id="fb358-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="fb358-118">Se você tiver uma experiência de treinamento existentes e o serviço Web de novo, convém toocheck out treinar novamente uma previsão Web serviço em vez de seguir Olá passo a passo mencionada na Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="fb358-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="fb358-119">Fluxos de trabalho completos</span><span class="sxs-lookup"><span data-stu-id="fb358-119">End-to-end workflow</span></span>
<span data-ttu-id="fb358-120">Olá, processo envolve Olá componentes a seguir: uma experiência de treinamento e teste uma previsão publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="fb358-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="fb358-121">tooenable treinamento de um modelo treinado, Olá experiência de treinamento deve ser publicado como um serviço Web com saída de saudação de um modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="fb358-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="fb358-122">Isso permite que o modelo de toohello de acesso de API para treinamento.</span><span class="sxs-lookup"><span data-stu-id="fb358-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="fb358-123">Olá, as etapas a seguir se aplicam a tooboth novo e clássico serviços da Web:</span><span class="sxs-lookup"><span data-stu-id="fb358-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="fb358-124">Crie serviço Web de previsão inicial de saudação:</span><span class="sxs-lookup"><span data-stu-id="fb358-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="fb358-125">Criar um teste de treinamento</span><span class="sxs-lookup"><span data-stu-id="fb358-125">Create a training experiment</span></span>
* <span data-ttu-id="fb358-126">Criar um teste da Web preditivo</span><span class="sxs-lookup"><span data-stu-id="fb358-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="fb358-127">Implantar um serviço Web preditivo</span><span class="sxs-lookup"><span data-stu-id="fb358-127">Deploy a predictive web service</span></span>

<span data-ttu-id="fb358-128">Treinar novamente o serviço Web de saudação:</span><span class="sxs-lookup"><span data-stu-id="fb358-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="fb358-129">Atualizar tooallow de experiência de treinamento para treinamento</span><span class="sxs-lookup"><span data-stu-id="fb358-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="fb358-130">Implantar Olá treinamento serviço web</span><span class="sxs-lookup"><span data-stu-id="fb358-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="fb358-131">Usar o modelo de saudação do hello serviço de execução de lote código tooretrain</span><span class="sxs-lookup"><span data-stu-id="fb358-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="fb358-132">Para obter uma explicação da saudação etapas anteriores, consulte [aprendizado de máquina treinar novamente modelos programaticamente](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="fb358-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="fb358-133">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb358-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="fb358-134">Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="fb358-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="fb358-135">Se você implantou um Serviço Web Clássico:</span><span class="sxs-lookup"><span data-stu-id="fb358-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="fb358-136">Criar um novo ponto de extremidade no serviço Web de previsão de saudação</span><span class="sxs-lookup"><span data-stu-id="fb358-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="fb358-137">Obter URL de PATCH hello e código</span><span class="sxs-lookup"><span data-stu-id="fb358-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="fb358-138">Use Olá URL PATCH toopoint Olá novo ponto de extremidade no hello treinados novamente o modelo</span><span class="sxs-lookup"><span data-stu-id="fb358-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="fb358-139">Para obter uma explicação da saudação etapas anteriores, consulte [treinar novamente um serviço Web clássico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="fb358-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="fb358-140">Se você tiver dificuldade para treinamento de um serviço Web clássico, consulte [Olá treinamento de um serviço Web clássico do Azure Machine Learning de solução de problemas](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="fb358-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="fb358-141">Se você tiver implantado um Novo serviço Web:</span><span class="sxs-lookup"><span data-stu-id="fb358-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="fb358-142">Entrar tooyour conta de Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="fb358-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="fb358-143">Obter definição de serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="fb358-143">Get hello Web service definition</span></span>
* <span data-ttu-id="fb358-144">Saudação de exportação de definição de serviço Web como JSON</span><span class="sxs-lookup"><span data-stu-id="fb358-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="fb358-145">Atualizar Olá referência toohello `ilearner` blob em Olá JSON</span><span class="sxs-lookup"><span data-stu-id="fb358-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="fb358-146">Importar Olá JSON em uma definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="fb358-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="fb358-147">Olá Web serviço de atualização com a nova definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="fb358-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="fb358-148">Para obter uma explicação da saudação etapas anteriores, consulte [treinar novamente um serviço Web de novo usando cmdlets do PowerShell de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fb358-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="fb358-149">processo de saudação para configurar o treinamento de um serviço Web clássico envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb358-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Visão geral do processo readaptação][1]

<span data-ttu-id="fb358-151">processo de saudação para configurar o treinamento de um serviço Web de novo envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb358-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Visão geral do processo readaptação][7]

## <a name="other-resources"></a><span data-ttu-id="fb358-153">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="fb358-153">Other Resources</span></span>
* <span data-ttu-id="fb358-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Readaptando e atualizando modelos do Machine Learning com o Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="fb358-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)</span></span>
* [<span data-ttu-id="fb358-155">Criar vários modelos do Machine Learning e pontos de extremidade de serviço Web com base em um teste usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb358-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="fb358-156">Olá [AML treinar novamente modelos usando APIs](https://www.youtube.com/watch?v=wwjglA8xllg) vídeo mostra como modelos de aprendizado de máquina tooretrain criados no aprendizado de máquina do Azure usando Olá PowerShell e APIs de treinamento.</span><span class="sxs-lookup"><span data-stu-id="fb358-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

