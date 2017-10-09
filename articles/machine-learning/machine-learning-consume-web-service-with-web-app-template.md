---
title: "aaaConsume um serviço web de aprendizado de máquina com um modelo de aplicativo da web | Microsoft Docs"
description: "Use um modelo de aplicativo da web no Azure Marketplace tooconsume um serviço web de previsão no aprendizado de máquina do Azure."
keywords: "serviço Web, operacionalização, API REST, aprendizado de máquina"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="cedd2-104">Consumir um serviço Web de Azure Machine Learning com um modelo de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cedd2-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="cedd2-105">Uma vez você tiver desenvolvido seu modelo de previsão e implantá-lo como um serviço web do Azure usando o estúdio de aprendizado de máquina, ou usando ferramentas como o R ou Python, você pode acessar o modelo operacionalizados hello, usando uma API REST.</span><span class="sxs-lookup"><span data-stu-id="cedd2-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="cedd2-106">Há várias maneiras de tooconsume Olá API REST do serviço e acesso Olá web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="cedd2-107">Por exemplo, você pode escrever um aplicativo em c#, R, ou Python usando Olá exemplo de código gerado para você quando você implantou o serviço web de saudação (disponível no hello [Portal de serviços de Web de aprendizado de máquina](https://services.azureml.net/quickstart) ou no painel de serviço web Olá no Estúdio de aprendizado de máquina).</span><span class="sxs-lookup"><span data-stu-id="cedd2-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="cedd2-108">Ou você pode usar o livro do Microsoft Excel de exemplo hello criado para você no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="cedd2-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="cedd2-109">Mas Olá tooaccess de maneira mais rápida e mais fácil é seu serviço web por meio de modelos do aplicativo da Web hello disponíveis no hello [Azure Marketplace de aplicativo Web](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="cedd2-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="cedd2-110">Olá modelos de aplicativo do Azure máquina aprendizado da Web</span><span class="sxs-lookup"><span data-stu-id="cedd2-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="cedd2-111">modelos do aplicativo da web Hello disponíveis no hello Azure Marketplace podem criar um aplicativo da web personalizado que lide com os dados de entrada e resultados esperados do serviço web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="cedd2-112">Você só precisa toodo é dar Olá web access tooyour da web do serviço de aplicativo e de dados e modelo Olá Olá rest.</span><span class="sxs-lookup"><span data-stu-id="cedd2-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="cedd2-113">Dois modelos estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="cedd2-113">Two templates are available:</span></span>

* [<span data-ttu-id="cedd2-114">Modelo do Aplicativo Web do Serviço de Solicitação-Resposta do Azure ML</span><span class="sxs-lookup"><span data-stu-id="cedd2-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="cedd2-115">Modelo do aplicativo Web do Serviço de Execução em Lote do Azure ML</span><span class="sxs-lookup"><span data-stu-id="cedd2-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="cedd2-116">Cada modelo cria um aplicativo ASP.NET de exemplo, usando Olá URI da API e a chave para o serviço web e o implanta como tooAzure um site da web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="cedd2-117">modelo de serviço de solicitação-resposta (RR) Olá cria um aplicativo web que permite que você toosend uma única linha de dados toohello web serviço tooget um único resultado.</span><span class="sxs-lookup"><span data-stu-id="cedd2-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="cedd2-118">modelo de serviço de execução de lote (BES) Olá cria um aplicativo web que permite que você toosend muitas linhas de dados tooget vários resultados.</span><span class="sxs-lookup"><span data-stu-id="cedd2-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="cedd2-119">Codificação não é necessário toouse esses modelos.</span><span class="sxs-lookup"><span data-stu-id="cedd2-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="cedd2-120">Basta fornecer Olá chave de API e o URI e modelo Olá cria o aplicativo hello para você.</span><span class="sxs-lookup"><span data-stu-id="cedd2-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="cedd2-121">chave de API de saudação tooget e URI de solicitação para um serviço web:</span><span class="sxs-lookup"><span data-stu-id="cedd2-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="cedd2-122">Em Olá [Portal de serviços da Web](https://services.azureml.net/quickstart), para um novo serviço da web, clique em **serviços Web** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="cedd2-123">Ou para gerenciar um serviço Web Clássico, clique em **Serviços Web Clássicos**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="cedd2-124">Clique em Olá web serviço você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cedd2-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="cedd2-125">Para um serviço web clássico, clique em ponto de extremidade de saudação deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cedd2-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="cedd2-126">Clique em **consumir** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="cedd2-127">Saudação de cópia **primário** ou **chave secundária** e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="cedd2-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="cedd2-128">Se você estiver criando um modelo de serviço de solicitação-resposta (RR), copie Olá **solicitação-resposta** URI e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="cedd2-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="cedd2-129">Se você estiver criando um modelo de serviço de execução de lote (BES), copie Olá **solicitações em lote** URI e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="cedd2-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="cedd2-130">Como toouse Olá modelo de serviço de solicitação-resposta (RR)</span><span class="sxs-lookup"><span data-stu-id="cedd2-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="cedd2-131">Siga estas etapas toouse Olá RRS web modelo de aplicativo, conforme mostrado no diagrama a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Modelo do processo toouse RRS da web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="cedd2-133">Vá toohello [portal do Azure](https://portal.azure.com), **logon**, clique em **novo**, procure e selecione **aplicativo Web de serviço de solicitação-resposta do Azure ML**, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="cedd2-134">Dê um nome exclusivo ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-134">Give your web app a unique name.</span></span> <span data-ttu-id="cedd2-135">URL de saudação do aplicativo web de saudação será esse nome seguido por `.azurewebsites.net.` por exemplo,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="cedd2-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="cedd2-136">Selecione hello assinatura do Azure e serviços sob a qual o serviço web está em execução.</span><span class="sxs-lookup"><span data-stu-id="cedd2-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="cedd2-137">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-137">Click **Create**.</span></span>
     
     ![Criar um aplicativo Web][image5]

4. <span data-ttu-id="cedd2-139">Quando o Azure concluiu a implantação de aplicativo da web de Olá, clique em Olá **URL** na Olá a página de configurações de aplicativo web no Azure, ou insira Olá URL em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="cedd2-140">Por exemplo, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="cedd2-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="cedd2-141">Olá quando executa primeiro do aplicativo web solicitará que você para hello **API Post URL** e **chave API**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="cedd2-142">Insira valores hello salvos anteriormente (**URI da solicitação** e **chave API**, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="cedd2-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="cedd2-143">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-143">Click **Submit**.</span></span>
     
     ![Insira o URI de Postagem e a Chave de API][image6]

6. <span data-ttu-id="cedd2-145">Olá web app exibe seu **configuração de aplicativo da Web** página de configurações de serviço da web atual hello.</span><span class="sxs-lookup"><span data-stu-id="cedd2-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="cedd2-146">Aqui você pode fazer alterações toohello configurações usadas pelo aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cedd2-147">Alterar as configurações de saudação aqui altera apenas-los para este aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="cedd2-148">Ele não altera as configurações padrão de saudação do serviço web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="cedd2-149">Por exemplo, se você alterar Olá **descrição** aqui ele não altera a descrição de saudação mostrada no painel de serviço web Olá no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="cedd2-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="cedd2-150">Quando terminar, clique em **salvar alterações**e, em seguida, clique em **vá tooHome página**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="cedd2-151">Página inicial que você pode inserir valores de toosend tooyour web Services da saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="cedd2-152">Clique em **enviar** quando tiver terminado e Olá resultado será retornado.</span><span class="sxs-lookup"><span data-stu-id="cedd2-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="cedd2-153">Se você quiser tooreturn toohello **configuração** página, ir toohello `setting.aspx` página do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="cedd2-154">Por exemplo: `http://carprediction.azurewebsites.net/setting.aspx.` será chave de saudação API tooenter solicitadas novamente - você precisa que tooaccess Olá página e atualizar as configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="cedd2-155">Você pode parar, reiniciar ou excluir o aplicativo web de Olá Olá portal do Azure como qualquer outro aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cedd2-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="cedd2-156">Enquanto ele está em execução, você pode procurar o endereço inicial toohello e insira novos valores.</span><span class="sxs-lookup"><span data-stu-id="cedd2-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="cedd2-157">Como toouse Olá modelo de serviço de execução de lote (BES)</span><span class="sxs-lookup"><span data-stu-id="cedd2-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="cedd2-158">Você pode usar o hello BES do modelo de aplicativo da web em Olá mesma maneira como modelo RRS Olá, exceto esse aplicativo web de saudação que é criado permitirá toosubmit várias linhas de dados e receber vários resultados.</span><span class="sxs-lookup"><span data-stu-id="cedd2-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="cedd2-159">valores de entrada Hello para um serviço de web de execução de lote podem vir de armazenamento do Azure ou um arquivo local. Olá resultados são armazenados em um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cedd2-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="cedd2-160">Assim, será necessário um toohold de contêiner de armazenamento do Azure Olá resultados retornados pelo aplicativo de web hello, e você precisará tooget seus dados de entrada pronto.</span><span class="sxs-lookup"><span data-stu-id="cedd2-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Processar toouse BES modelo da web][image2]

1. <span data-ttu-id="cedd2-162">Siga Olá mesmo saudação do procedimento toocreate BES do aplicativo da web para o modelo RRS hello, exceto go muito[modelo de aplicativo do Azure ML lote execução do serviço Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Olá modelo BES no Azure Marketplace e clique em **criar aplicativo de Web** .</span><span class="sxs-lookup"><span data-stu-id="cedd2-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="cedd2-163">toospecify onde você deseja que os resultados de saudação armazenados, insira informações de contêiner de destino Olá na home page do aplicativo de web de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedd2-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="cedd2-164">Especifique também onde Olá web aplicativo pode obter valores de entrada de hello, em um arquivo local ou um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cedd2-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="cedd2-165">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="cedd2-165">Click **Submit**.</span></span>
   
    ![Informações de armazenamento][image7]

<span data-ttu-id="cedd2-167">Olá web app exibirá uma página de status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="cedd2-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="cedd2-168">Quando tiver concluído o trabalho de saudação você terá local Olá dos resultados de saudação no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cedd2-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="cedd2-169">Você também tem a opção de saudação de download de arquivo local da saudação resultados tooa.</span><span class="sxs-lookup"><span data-stu-id="cedd2-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="cedd2-170">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="cedd2-170">For more information</span></span>
<span data-ttu-id="cedd2-171">toolearn mais sobre...</span><span class="sxs-lookup"><span data-stu-id="cedd2-171">toolearn more about...</span></span>

* <span data-ttu-id="cedd2-172">como criar uma experiência de aprendizado de máquina com o Machine Learning Studio, veja [Criar seu primeiro teste no Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="cedd2-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="cedd2-173">como toodeploy o aprendizado de máquina de teste como um serviço web, consulte [implantar um serviço web de aprendizado de máquina do Azure](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="cedd2-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="cedd2-174">outras maneiras tooaccess seu serviço web, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="cedd2-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
