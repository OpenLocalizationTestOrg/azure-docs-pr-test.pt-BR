---
title: "serviço da web aaaTroubleshoot treinamento um clássico de aprendizado de máquina do Azure | Microsoft Docs"
description: "Identifique e corrija encontrado comum de problemas quando você estiver treinamento modelo Olá para um serviço de Web do aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="17489-103">Olá treinamento de um serviço Web clássico do Azure Machine Learning de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="17489-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="17489-104">Visão geral da readaptação</span><span class="sxs-lookup"><span data-stu-id="17489-104">Retraining overview</span></span>
<span data-ttu-id="17489-105">Quando você implanta um experimento de previsão como um serviço Web de pontuação, ele é um modelo estático.</span><span class="sxs-lookup"><span data-stu-id="17489-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="17489-106">Conforme novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seus próprios dados, o modelo Olá precisa toobe treinados novamente.</span><span class="sxs-lookup"><span data-stu-id="17489-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="17489-107">Para obter uma explicação completa de saudação treinar novamente o processo de um serviço Web clássico, consulte [treinar novamente Machine Learning modelos por meio de programação](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="17489-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="17489-108">Processo de readaptação</span><span class="sxs-lookup"><span data-stu-id="17489-108">Retraining process</span></span>
<span data-ttu-id="17489-109">Quando você precisar tooretrain Olá serviço da Web, você deve adicionar algumas informações adicionais:</span><span class="sxs-lookup"><span data-stu-id="17489-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="17489-110">Um serviço da Web implantado por meio de saudação experiência de treinamento.</span><span class="sxs-lookup"><span data-stu-id="17489-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="17489-111">experiência de saudação deve ter uma **saída do serviço Web** módulo anexado toohello saída de hello **treinar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="17489-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Anexe o modelo de treinamento de toohello Olá web serviço saída.][image1]
* <span data-ttu-id="17489-113">Um novo ponto de extremidade adicionados tooyour serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="17489-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="17489-114">Você pode adicionar o ponto de extremidade Olá programaticamente usando código de exemplo hello referenciado em Olá aprendizado de máquina treinar novamente modelos programaticamente tópico ou por meio de saudação portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="17489-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="17489-115">Você pode usar código c# exemplo de saudação do modelo de tooretrain do serviço de Web do treinamento Olá API ajuda página.</span><span class="sxs-lookup"><span data-stu-id="17489-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="17489-116">Depois de ter avaliado resultados Olá e está satisfeito com eles, você atualizar o modelo treinado hello, serviço web usando Olá novo ponto de extremidade que você adicionou a pontuação.</span><span class="sxs-lookup"><span data-stu-id="17489-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="17489-117">Com todas as partes da saudação em vigor, etapas principais hello, você deve executar o modelo de saudação tooretrain são:</span><span class="sxs-lookup"><span data-stu-id="17489-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="17489-118">Chamar hello serviço da Web de treinamento: chamada hello toohello serviço de execução de lote (BES), não Olá serviço de resposta de solicitação (RR).</span><span class="sxs-lookup"><span data-stu-id="17489-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="17489-119">Você pode usar o código c# exemplo hello na chamada de Olá Olá API ajuda página toomake.</span><span class="sxs-lookup"><span data-stu-id="17489-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="17489-120">Localizar valores de saudação para Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: esses valores são retornados na saída de saudação do toohello sua chamada de treinamento Serviço.</span><span class="sxs-lookup"><span data-stu-id="17489-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="17489-121">![Mostrar saída Olá Olá treinamento valores BaseLocation, RelativeLocation e SasBlobToken de exemplo e hello.][image6]</span><span class="sxs-lookup"><span data-stu-id="17489-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="17489-122">Atualização Olá adicionado modelo treinado do ponto de extremidade do hello novo serviço web com hello de pontuação: usando o código de exemplo hello fornecido Olá aprendizado de máquina treinar novamente modelos programaticamente, atualizar novo ponto de extremidade de saudação adicionado toohello pontuação modelos com hello recentemente modelo treinado de saudação serviço da Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="17489-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="17489-123">Obstáculos comuns</span><span class="sxs-lookup"><span data-stu-id="17489-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="17489-124">Verificar toosee se você tiver Olá corrigir PATCH URL</span><span class="sxs-lookup"><span data-stu-id="17489-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="17489-125">Olá PATCH URL que está usando deve ser Olá associado Olá novo ponto de extremidade de pontuação adicionado toohello serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="17489-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="17489-126">Há uma série de maneiras tooobtain Olá PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="17489-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="17489-127">**Opção 1: use um programa**</span><span class="sxs-lookup"><span data-stu-id="17489-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="17489-128">Olá tooget corrigir PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="17489-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="17489-129">Executar Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="17489-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="17489-130">Da saída de saudação de AddEndpoint, localize Olá *HelpLocation* valor e copie a URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="17489-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation na saída de saudação do exemplo de addEndpoint hello.][image2]
3. <span data-ttu-id="17489-132">Cole a URL de saudação em uma página de tooa toonavigate de navegador que fornece links de ajuda para Olá serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="17489-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="17489-133">Clique em Olá **recurso de atualização** página de Ajuda do link tooopen Olá patch.</span><span class="sxs-lookup"><span data-stu-id="17489-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="17489-134">**Opção 2: Usar Olá portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="17489-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="17489-135">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17489-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17489-136">Guia de aprendizado de máquina Olá aberto. ![Guia Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="17489-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="17489-137">Clique no nome do espaço de trabalho e depois em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="17489-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="17489-138">Clique em Olá serviço Web que você está trabalhando com a pontuação.</span><span class="sxs-lookup"><span data-stu-id="17489-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="17489-139">(Se você não modificou o nome padrão de saudação do serviço web de saudação, ela terminará em [pontuação Exp]..)</span><span class="sxs-lookup"><span data-stu-id="17489-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="17489-140">Clicar em **Adicionar Ponto de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="17489-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="17489-141">Depois que o ponto de extremidade de saudação é adicionado, clique em nome do ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="17489-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="17489-142">Em seguida, clique em **recurso de atualização** tooopen Olá a página de ajuda de aplicação de patch.</span><span class="sxs-lookup"><span data-stu-id="17489-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="17489-143">Se você tiver adicionado toohello serviço da Web de treinamento do ponto de extremidade Olá em vez da saudação serviço Web de previsão, você receberá Olá erro a seguir quando você clica em Olá **recurso de atualização** link: Desculpe, mas não há suporte para esse recurso ou disponível neste contexto.</span><span class="sxs-lookup"><span data-stu-id="17489-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="17489-144">Este serviço Web não tem recursos atualizáveis.</span><span class="sxs-lookup"><span data-stu-id="17489-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="17489-145">Lamentamos o inconveniente hello e está trabalhando em melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="17489-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Painel Novo ponto de extremidade.][image3]

<span data-ttu-id="17489-147">página de ajuda de PATCH Olá contém Olá URL PATCH, você deve usar e fornece código de exemplo, você pode usar toocall-lo.</span><span class="sxs-lookup"><span data-stu-id="17489-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="17489-149">Toosee de seleção que você está atualizando Olá pontuação ponto de extremidade correto</span><span class="sxs-lookup"><span data-stu-id="17489-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="17489-150">Patch não Olá serviço da Web de treinamento: operação de patch Olá deve ser executada em Olá pontuação serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="17489-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="17489-151">Não corrigir o ponto de extremidade saudação padrão no serviço Web: operação de patch Olá deve ser executada em Olá pontuação novo ponto de extremidade de serviço de Web que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="17489-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="17489-152">Você pode verificar qual ponto de extremidade de saudação do Web service é ativado por Olá visitando portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="17489-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="17489-153">Certifique-se de que você está adicionando toohello de ponto de extremidade Olá serviço Web de previsão, Olá serviço da Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="17489-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="17489-154">Se você tiver implantado corretamente um serviço Web de previsão e um serviço da Web de treinamento, você verá dois serviços Web separados listados.</span><span class="sxs-lookup"><span data-stu-id="17489-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="17489-155">Olá serviço Web de previsão deve terminar com "[previsão exp]"..</span><span class="sxs-lookup"><span data-stu-id="17489-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="17489-156">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17489-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17489-157">Guia de aprendizado de máquina Olá aberto. ![IU do espaço de trabalho do Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="17489-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="17489-158">Selecione o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="17489-158">Select your workspace.</span></span>
4. <span data-ttu-id="17489-159">Clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="17489-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="17489-160">Selecione o Serviço Web de previsão.</span><span class="sxs-lookup"><span data-stu-id="17489-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="17489-161">Verifique se o novo ponto de extremidade foi adicionado toohello Web service.</span><span class="sxs-lookup"><span data-stu-id="17489-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="17489-162">Verificar espaço de trabalho de saudação que seu serviço web está em tooensure é na região correta Olá</span><span class="sxs-lookup"><span data-stu-id="17489-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="17489-163">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17489-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17489-164">Selecione o aprendizado de máquina no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="17489-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="17489-165">![IU da região do Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="17489-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="17489-166">Verifique se o local de saudação do seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="17489-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
