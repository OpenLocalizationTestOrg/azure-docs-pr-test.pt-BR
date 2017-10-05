---
title: "Solução de Problemas de readaptação de um serviço Web clássico do Azure Machine Learning | Microsoft Docs"
description: "Identifique e corrija os problemas comuns encontrados quando você está readaptando o modelo para um serviço Web do Azure Machine Learning."
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
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="6ca2f-103">Solução de problemas de readaptação de um serviço Web clássico do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6ca2f-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="6ca2f-104">Visão geral da readaptação</span><span class="sxs-lookup"><span data-stu-id="6ca2f-104">Retraining overview</span></span>
<span data-ttu-id="6ca2f-105">Quando você implanta um experimento de previsão como um serviço Web de pontuação, ele é um modelo estático.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="6ca2f-106">Conforme novos dados ficam disponíveis ou quando o consumidor da API tem seus próprios dados, o modelo precisa ser readaptado.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="6ca2f-107">Para obter uma explicação completa sobre o processo de readaptação de um serviço Web clássico, consulte [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="6ca2f-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="6ca2f-108">Processo de readaptação</span><span class="sxs-lookup"><span data-stu-id="6ca2f-108">Retraining process</span></span>
<span data-ttu-id="6ca2f-109">Quando precisar readaptar o serviço Web, você deverá adicionar algumas partes extras:</span><span class="sxs-lookup"><span data-stu-id="6ca2f-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="6ca2f-110">Um serviço Web implantado a partir do Teste de treinamento.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="6ca2f-111">O teste deve ter um módulo de **Saída do serviço Web** anexado à saída do módulo do **Modelo de treinamento**.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Anexe a saída do serviço Web ao modelo de treinamento.][image1]
* <span data-ttu-id="6ca2f-113">Um novo ponto de extremidade adicionado ao seu serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="6ca2f-114">Você pode adicionar o ponto de extremidade por meio da programação usando o código de exemplo referenciado no tópico Readaptar os modelos de Machine Learning de forma programática ou por meio do portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="6ca2f-115">Em seguida, pode usar o código C# de exemplo na página de ajuda da API do Serviço Web de Treinamento para readaptar o modelo.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="6ca2f-116">Depois de ter avaliado os resultados e ficar satisfeito com eles, você atualizará o serviço Web de pontuação do modelo treinado usando o novo ponto de extremidade adicionado.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="6ca2f-117">Com todas as peças no lugar, as principais etapas necessárias para readaptar o modelo são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="6ca2f-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="6ca2f-118">Chame o serviço Web de treinamento: a chamada é para o BES (Serviço de Execução em Lote), não o RRS (Serviço de Resposta a Solicitação).</span><span class="sxs-lookup"><span data-stu-id="6ca2f-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="6ca2f-119">Você pode usar o Código c# de exemplo na página de ajuda da API para fazer a chamada.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="6ca2f-120">Encontre os valores para *BaseLocation*, *RelativeLocation* e *SasBlobToken*: esses valores são retornados na saída de sua chamada para o Serviço Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="6ca2f-121">![exibindo a saída do exemplo de readaptação e os valores BaseLocation, RelativeLocation e SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="6ca2f-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="6ca2f-122">Atualize o ponto de extremidade adicionado do serviço Web de pontuação com o novo modelo treinado: usando o código de exemplo fornecido em Readaptar os modelos de Machine Learning de forma programática, atualize o novo ponto de extremidade adicionado ao modelo de pontuação com o modelo treinado recentemente do Serviço Web de Treinamento.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="6ca2f-123">Obstáculos comuns</span><span class="sxs-lookup"><span data-stu-id="6ca2f-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="6ca2f-124">Verifique se você tem a URL correta do PATCH</span><span class="sxs-lookup"><span data-stu-id="6ca2f-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="6ca2f-125">A URL do PATCH que você está usando deve ser a associada ao novo ponto de extremidade de pontuação adicionado ao serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="6ca2f-126">Há várias maneiras de obter a URL do PATCH:</span><span class="sxs-lookup"><span data-stu-id="6ca2f-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="6ca2f-127">**Opção 1: use um programa**</span><span class="sxs-lookup"><span data-stu-id="6ca2f-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="6ca2f-128">Para obter a URL correta do PATCH:</span><span class="sxs-lookup"><span data-stu-id="6ca2f-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="6ca2f-129">Execute o código de exemplo [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="6ca2f-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="6ca2f-130">Na saída do AddEndpoint, encontre o valor *HelpLocation* e copie a URL.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation na saída do exemplo addEndpoint.][image2]
3. <span data-ttu-id="6ca2f-132">Cole a URL em um navegador para navegar até uma página que fornece links de ajuda para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="6ca2f-133">Clique no link **Atualizar Recurso** para abrir a página de ajuda do patch.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="6ca2f-134">**Opção 2: use o portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="6ca2f-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="6ca2f-135">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6ca2f-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6ca2f-136">Abra a guia Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="6ca2f-137">![Guia Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="6ca2f-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="6ca2f-138">Clique no nome do espaço de trabalho e depois em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="6ca2f-139">Clique no serviço Web de pontuação com o qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="6ca2f-140">(Se você não modificou o nome padrão do serviço Web, ele terminará com [Scoring Exp.].)</span><span class="sxs-lookup"><span data-stu-id="6ca2f-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="6ca2f-141">Clicar em **Adicionar Ponto de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="6ca2f-142">Depois do ponto de extremidade ser adicionado, clique no nome dele.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="6ca2f-143">Em seguida, clique em **Atualizar Recurso** para abrir a página de ajuda do patch.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="6ca2f-144">Caso tenha adicionado o ponto de extremidade para o Serviço Web de treinamento em vez do Serviço Web de previsão, você receberá o seguinte erro quando clicar no link **Atualizar Recurso**: Desculpe, mas esse recurso não tem suporte nem está disponível neste contexto.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="6ca2f-145">Este serviço Web não tem recursos atualizáveis.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="6ca2f-146">Pedimos desculpas pela inconveniência e estamos trabalhando para melhorar esse fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Painel Novo ponto de extremidade.][image3]

<span data-ttu-id="6ca2f-148">A página de ajuda do PATCH contém a URL do PATCH que você deve usar e fornece o código de exemplo que você pode usar para chamar.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![URL de patch.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="6ca2f-150">Verifique se você está atualizando o ponto de extremidade correto de pontuação</span><span class="sxs-lookup"><span data-stu-id="6ca2f-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="6ca2f-151">Não corrija o Serviço Web de treinamento: a operação do patch deve ser executada no serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="6ca2f-152">Não corrija o ponto de extremidade padrão no serviço Web: a operação do patch deve ser executada no novo ponto de extremidade do serviço Web de pontuação que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="6ca2f-153">Você pode verificar em qual serviço Web está o ponto de extremidade visitando o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ca2f-154">Certifique-se de que você está adicionando o ponto de extremidade ao serviço Web de previsão e não ao serviço da Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="6ca2f-155">Se você tiver implantado corretamente um serviço Web de previsão e um serviço da Web de treinamento, você verá dois serviços Web separados listados.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="6ca2f-156">O serviço Web de previsão deve terminar com "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="6ca2f-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="6ca2f-157">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6ca2f-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6ca2f-158">Abra a guia Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="6ca2f-159">![IU do espaço de trabalho do Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="6ca2f-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="6ca2f-160">Selecione o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-160">Select your workspace.</span></span>
4. <span data-ttu-id="6ca2f-161">Clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="6ca2f-162">Selecione o Serviço Web de previsão.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="6ca2f-163">Verifique se o novo ponto de extremidade foi adicionado ao serviço Web.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="6ca2f-164">Verifique o espaço de trabalho no qual o serviço Web está para garantir que esteja na região correta</span><span class="sxs-lookup"><span data-stu-id="6ca2f-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="6ca2f-165">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6ca2f-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6ca2f-166">Selecione Machine Learning no menu.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="6ca2f-167">![IU da região do Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="6ca2f-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="6ca2f-168">Verifique o local do seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6ca2f-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
