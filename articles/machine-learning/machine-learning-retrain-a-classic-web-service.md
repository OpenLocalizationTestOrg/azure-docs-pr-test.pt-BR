---
title: "aaaRetrain um serviço da web clássico | Microsoft Docs"
description: "Saiba como tooprogrammatically treinar novamente um modelo e a atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="fd0b3-103">Treinar novamente um serviço Web Clássico</span><span class="sxs-lookup"><span data-stu-id="fd0b3-103">Retrain a Classic web service</span></span>
<span data-ttu-id="fd0b3-104">Olá previsão serviço Web é implantado é o padrão de saudação ponto de extremidade de pontuação.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="fd0b3-105">Pontos de extremidade padrão são mantidos em sincronia com hello originais de treinamento e pontuação experiências e, portanto, hello treinado para o ponto de extremidade do saudação padrão não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="fd0b3-106">serviço de web hello tooretrain, adicione um novo serviço da web de toohello ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd0b3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fd0b3-107">Prerequisites</span></span>
<span data-ttu-id="fd0b3-108">Você deve ter configurado um Teste de Treinamento e um Experimento de Previsão, como mostrado em [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fd0b3-109">experiência de previsão Olá deve ser implantada como uma serviço web de aprendizado de máquina clássico.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="fd0b3-110">Para obter mais informações sobre como implantar os serviços Web, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="fd0b3-111">Adicionar um novo ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="fd0b3-111">Add a new Endpoint</span></span>
<span data-ttu-id="fd0b3-112">Olá previsão serviço Web que você implantou contém um ponto de extremidade que é mantido em sincronizado com o treinamento original hello e pontuação treinado experiências de pontuação padrão.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="fd0b3-113">tooupdate toowith seu serviço web um novo modelo treinado, você deve criar um novo ponto de extremidade de pontuação.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="fd0b3-114">toocreate um novo pontuação ponto de extremidade em Olá previsão serviço Web que pode ser atualizada com o modelo treinado hello:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="fd0b3-115">Certifique-se de que você está adicionando toohello de ponto de extremidade Olá serviço Web de previsão, Olá serviço da Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="fd0b3-116">Se você tiver implantado corretamente um serviço Web de previsão e um serviço da Web de treinamento, você verá dois serviços Web separados listados.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="fd0b3-117">Olá serviço Web de previsão deve terminar com "[previsão exp]"..</span><span class="sxs-lookup"><span data-stu-id="fd0b3-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="fd0b3-118">Há três maneiras em que você pode adicionar um novo serviço da web de tooa ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="fd0b3-119">Programaticamente</span><span class="sxs-lookup"><span data-stu-id="fd0b3-119">Programmatically</span></span>
2. <span data-ttu-id="fd0b3-120">Usar o portal de serviços Web do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="fd0b3-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="fd0b3-121">Use Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="fd0b3-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="fd0b3-122">Adicionar um ponto de extremidade programaticamente</span><span class="sxs-lookup"><span data-stu-id="fd0b3-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="fd0b3-123">Você pode adicionar pontos de extremidade de pontuação usando o código de exemplo hello fornecido neste [repositório github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="fd0b3-124">Use tooadd um ponto de extremidade do portal de serviços Web do Microsoft Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="fd0b3-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="fd0b3-125">No estúdio de aprendizado de máquina, na coluna de navegação à esquerda do hello, clique em serviços da Web.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="fd0b3-126">Na parte inferior de saudação do painel de serviço web hello, clique em **visualização de pontos de extremidade de gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="fd0b3-127">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-127">Click **Add**.</span></span>
4. <span data-ttu-id="fd0b3-128">Digite um nome e uma descrição para o novo ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="fd0b3-129">Selecione o nível de log hello e se os dados de exemplo estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="fd0b3-130">Para obter mais informações sobre registro em log, consulte [Habilitar o log de serviços Web de Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="fd0b3-131">Use Olá tooadd portal clássico do Azure um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="fd0b3-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="fd0b3-132">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd0b3-133">No menu à esquerda do hello, clique em **aprendizado de máquina**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="fd0b3-134">Em Nome, clique em seu espaço de Em Nome, clique em seu espaço de trabalho e, em seguida, clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="fd0b3-135">Em Nome, clique em **Modelo de Censo [exp. preditivo]**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="fd0b3-136">Final Olá Olá página, clique em **Adicionar ponto de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="fd0b3-137">Para saber mais sobre a adição de pontos de extremidade, veja [Criação de pontos de extremidade](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="fd0b3-138">Saudação de atualização adicionado treinado do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="fd0b3-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="fd0b3-139">processo novos treinamentos do toocomplete hello, você deve atualizar treinado Olá de saudação novo ponto de extremidade que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="fd0b3-140">Se você adicionou Olá novo ponto de extremidade usando o portal do Azure clássico de saudação, clique no nome hello novo ponto de extremidade no portal de saudação e Olá **UpdateResource** link tooget Olá URL seria necessário modelo tooupdate saudação do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="fd0b3-141">Se você adicionou o ponto de extremidade de saudação usando o código de exemplo hello, isso inclui o local da URL de ajuda Olá identificado pelo Olá *HelpLocationURL* valor na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="fd0b3-142">tooretrieve Olá caminho URL:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="fd0b3-143">Copie e cole a URL de saudação no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="fd0b3-144">Clique o link de recurso de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="fd0b3-145">Copie Olá postar na URL de solicitação de PATCH hello.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="fd0b3-146">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-146">For example:</span></span>
   
     <span data-ttu-id="fd0b3-147">URL DO PATCH: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="fd0b3-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="fd0b3-148">Agora você pode usar Olá Olá de tooupdate treinado pontuação de ponto de extremidade que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="fd0b3-149">Olá, código de exemplo a seguir mostra como Olá toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*e o ponto de extremidade do URL de PATCH tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="fd0b3-150">Olá *apiKey* e hello *endpointUrl* para chamada hello pode ser obtida no painel de controle do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="fd0b3-151">Olá valor Olá *nome* parâmetro em *recursos* deve saudação de correspondência de nome do recurso de saudação salvo treinado no experimento previsão hello.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="fd0b3-152">Olá tooget nome do recurso:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="fd0b3-153">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd0b3-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd0b3-154">No menu à esquerda do hello, clique em **aprendizado de máquina**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="fd0b3-155">Em Nome, clique em seu espaço de Em Nome, clique em seu espaço de trabalho e, em seguida, clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="fd0b3-156">Em Nome, clique em **Modelo de Censo [exp. preditivo]**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="fd0b3-157">Clique em Olá novo ponto de extremidade que é adicionado.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="fd0b3-158">No painel de controle de ponto de extremidade hello, clique em **recurso de atualização**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="fd0b3-159">Na página de documentação de API do recurso de atualização de saudação para serviço web de saudação, você pode encontrar hello **nome do recurso** em **recursos atualizáveis**.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="fd0b3-160">Se seu token SAS expirar antes de você terminar de atualizar o ponto de extremidade hello, você deve executar um GET com a Id do trabalho de saudação tooobtain um novo token.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="fd0b3-161">Quando o código de saudação foi executado com êxito, novo ponto de extremidade de saudação deve começar a usar o modelo Olá treinados novamente em aproximadamente 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="fd0b3-162">Resumo</span><span class="sxs-lookup"><span data-stu-id="fd0b3-162">Summary</span></span>
<span data-ttu-id="fd0b3-163">Usando Olá APIs de treinamento, você pode atualizar o modelo treinado de saudação de um serviço Web previsão habilitar cenários, como:</span><span class="sxs-lookup"><span data-stu-id="fd0b3-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="fd0b3-164">Readaptação de modelo periódico com novos dados.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="fd0b3-165">Distribuição de um modelo toocustomers com objetivo de saudação de permitir que eles treinar novamente o modelo de saudação usando seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="fd0b3-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd0b3-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd0b3-166">Next steps</span></span>
[<span data-ttu-id="fd0b3-167">Solução de problemas Olá treinamento de um serviço da web clássico de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="fd0b3-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

