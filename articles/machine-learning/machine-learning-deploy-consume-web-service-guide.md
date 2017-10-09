---
title: "Serviços Web do Azure Machine Learning: implantação e consumo | Microsoft Docs"
description: "Recursos para implantar e consumir serviços Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="6c08c-103">Serviços Web do Azure Machine Learning: implantação e consumo</span><span class="sxs-lookup"><span data-stu-id="6c08c-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="6c08c-104">Você pode usar modelos e fluxos de trabalho de aprendizado de máquina toodeploy aprendizado de máquina do Azure como serviços da web.</span><span class="sxs-lookup"><span data-stu-id="6c08c-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="6c08c-105">Esses serviços da web, em seguida, podem ser usado toocall Olá aprendizado de máquina modelos de aplicativos em previsões de toodo de Internet Olá em tempo real ou em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="6c08c-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="6c08c-106">Porque Olá web serviços RESTful, você pode chamá-los de várias linguagens de programação e plataformas, como o .NET e Java e de aplicativos, como o Excel.</span><span class="sxs-lookup"><span data-stu-id="6c08c-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="6c08c-107">seções a seguir Olá fornecem links toowalkthroughs, código e documentação toohelp começar.</span><span class="sxs-lookup"><span data-stu-id="6c08c-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="6c08c-108">Implantar um serviço Web</span><span class="sxs-lookup"><span data-stu-id="6c08c-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="6c08c-109">Com o Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="6c08c-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="6c08c-110">Estúdio de aprendizado de máquina e o portal de serviços Web de aprendizado de máquina do Microsoft Azure Olá ajudarão-lo a implantar e gerenciar um serviço web sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="6c08c-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="6c08c-111">Olá, links a seguir fornecem informações gerais sobre como toodeploy um novo serviço web:</span><span class="sxs-lookup"><span data-stu-id="6c08c-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="6c08c-112">Para obter uma visão geral sobre como toodeploy um novo serviço da web com base no Gerenciador de recursos do Azure, consulte [implantar um novo serviço da web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6c08c-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="6c08c-113">Para obter instruções sobre como toodeploy um serviço web, consulte [implantar um serviço web de aprendizado de máquina do Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6c08c-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="6c08c-114">Para obter uma explicação completa sobre como toocreate e implantar um serviço web, consulte [passo a passo etapa 1: criar um espaço de trabalho do aprendizado de máquina](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6c08c-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="6c08c-115">Para obter exemplos específicos que implantam um serviço Web, consulte:</span><span class="sxs-lookup"><span data-stu-id="6c08c-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="6c08c-116">Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="6c08c-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="6c08c-117">Como toodeploy um web serviço toomultiple regiões</span><span class="sxs-lookup"><span data-stu-id="6c08c-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="6c08c-118">Com as APIs do provedor de recursos dos serviços Web (APIs do Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6c08c-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="6c08c-119">provedor de recursos de aprendizado de máquina do Azure Olá para serviços da web permite que a implantação e gerenciamento de serviços da web usando chamadas da API REST.</span><span class="sxs-lookup"><span data-stu-id="6c08c-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="6c08c-120">Para obter mais detalhes, veja a referência [Serviço Web do Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="6c08c-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="6c08c-121">Com os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c08c-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="6c08c-122">O provedor de recursos do Azure Machine Learning para serviços Web permite a implantação e o gerenciamento dos serviços Web usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c08c-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="6c08c-123">toouse Olá cmdlets, você deve primeiro entrar tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c08c-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="6c08c-124">Se você estiver familiarizado com como toocall PowerShell os comandos que se baseiam no Gerenciador de recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="6c08c-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="6c08c-125">tooexport testar sua previsão, use [esse código de exemplo](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="6c08c-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="6c08c-126">Depois de criar o arquivo de .exe de saudação do código hello, você pode digitar:</span><span class="sxs-lookup"><span data-stu-id="6c08c-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="6c08c-127">Executar o aplicativo hello cria um modelo JSON de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="6c08c-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="6c08c-128">toouse Olá modelo toodeploy um serviço web, você deve adicionar Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c08c-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="6c08c-129">Nome e chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="6c08c-129">Storage account name and key</span></span>

    <span data-ttu-id="6c08c-130">Você pode obter Olá nome de conta de armazenamento e chave de qualquer Olá [portal do Azure](https://portal.azure.com/) ou hello [portal clássico do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6c08c-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="6c08c-131">ID do plano de compromisso</span><span class="sxs-lookup"><span data-stu-id="6c08c-131">Commitment plan ID</span></span>

    <span data-ttu-id="6c08c-132">Você pode obter o ID do plano de saudação do hello [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal entrar e clicando em um nome de plano.</span><span class="sxs-lookup"><span data-stu-id="6c08c-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="6c08c-133">Adicioná-los toohello modelo JSON como filhos do hello *propriedades* nó na saudação de mesmo nível como Olá *MachineLearningWorkspace* nó.</span><span class="sxs-lookup"><span data-stu-id="6c08c-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="6c08c-134">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c08c-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="6c08c-135">Consulte Olá artigos a seguir e exemplo de código para obter detalhes adicionais:</span><span class="sxs-lookup"><span data-stu-id="6c08c-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="6c08c-136">
            [cmdlets do Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) no MSDN</span><span class="sxs-lookup"><span data-stu-id="6c08c-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="6c08c-137">[Passo a passo](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) de exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="6c08c-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="6c08c-138">Consumir serviços web de saudação</span><span class="sxs-lookup"><span data-stu-id="6c08c-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="6c08c-139">De saudação serviços da Web de aprendizado do Azure máquina UI (teste)</span><span class="sxs-lookup"><span data-stu-id="6c08c-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="6c08c-140">Você pode testar o serviço web do portal de serviços de Web de aprendizado de máquina do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6c08c-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="6c08c-141">Isso inclui o serviço de solicitação-resposta hello (RR) de teste e interfaces de serviço de execução de lote (BES).</span><span class="sxs-lookup"><span data-stu-id="6c08c-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="6c08c-142">Implantar um novo serviço Web</span><span class="sxs-lookup"><span data-stu-id="6c08c-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* <span data-ttu-id="6c08c-143">
            [Implantar um serviço Web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="6c08c-143">[Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* [<span data-ttu-id="6c08c-144">Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="6c08c-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="6c08c-145">No Excel</span><span class="sxs-lookup"><span data-stu-id="6c08c-145">From Excel</span></span>
<span data-ttu-id="6c08c-146">Você pode baixar um modelo do Excel que consome Olá web serviço:</span><span class="sxs-lookup"><span data-stu-id="6c08c-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="6c08c-147">Consumindo um Serviço Web do Azure Machine Learning por meio do Excel</span><span class="sxs-lookup"><span data-stu-id="6c08c-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="6c08c-148">Suplemento do Excel para Serviços Web do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6c08c-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="6c08c-149">Em um cliente baseado em REST</span><span class="sxs-lookup"><span data-stu-id="6c08c-149">From a REST-based client</span></span>
<span data-ttu-id="6c08c-150">Os Serviços Web do Azure Machine Learning são APIs RESTful.</span><span class="sxs-lookup"><span data-stu-id="6c08c-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="6c08c-151">Você pode usar essas APIs de várias plataformas, como .NET, Python, R, Java, Olá etc. **consumir** página para seu serviço da web em Olá [portal de serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net) tem exemplo código que pode ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="6c08c-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="6c08c-152">Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="6c08c-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
