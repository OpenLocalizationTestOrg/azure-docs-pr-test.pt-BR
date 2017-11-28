---
title: "aaaDeploying um novo serviço da web no aprendizado de máquina do Azure | Microsoft Docs"
description: "serviço web baseado em fluxo de trabalho de saudação de implantação de um BRAÇO"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="5b0ee-103">Implantar um novo serviço Web</span><span class="sxs-lookup"><span data-stu-id="5b0ee-103">Deploy a new web service</span></span>
<span data-ttu-id="5b0ee-104">Agora de aprendizado de máquina do Microsoft Azure fornece serviços web baseados em [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permitindo novas opções de plano de cobrança e implantar as regiões de toomultiple do serviço web.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="5b0ee-105">Olá fluxo de trabalho geral toodeploy um serviço web usando serviços Web de aprendizado de máquina do Microsoft Azure é:</span><span class="sxs-lookup"><span data-stu-id="5b0ee-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="5b0ee-106">Criar um teste preditivo</span><span class="sxs-lookup"><span data-stu-id="5b0ee-106">Create a predictive experiment</span></span>
* <span data-ttu-id="5b0ee-107">implantá-lo</span><span class="sxs-lookup"><span data-stu-id="5b0ee-107">deploy it</span></span>
* <span data-ttu-id="5b0ee-108">configurar seu nome</span><span class="sxs-lookup"><span data-stu-id="5b0ee-108">configure its name</span></span>
* <span data-ttu-id="5b0ee-109">Plano de Faturamento</span><span class="sxs-lookup"><span data-stu-id="5b0ee-109">billing plan</span></span>
* <span data-ttu-id="5b0ee-110">testá-lo</span><span class="sxs-lookup"><span data-stu-id="5b0ee-110">test it</span></span>
* <span data-ttu-id="5b0ee-111">consumi-lo.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-111">consume it.</span></span>

<span data-ttu-id="5b0ee-112">Olá gráfico a seguir ilustra o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-112">hello following graphic illustrates hello workflow.</span></span>

![Fluxo de trabalho de implantação de serviço Web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="5b0ee-114">Implantar serviço Web do Studio</span><span class="sxs-lookup"><span data-stu-id="5b0ee-114">Deploy web service from Studio</span></span>
<span data-ttu-id="5b0ee-115">toodeploy uma experiência como um novo serviço web.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="5b0ee-116">Entrar no estúdio de aprendizado de máquina do hello e criar um novo serviço web de previsão.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="5b0ee-117">**Observação**: se você já implantou um teste como um serviço Web clássico, não poderá implantá-lo como um novo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="5b0ee-118">Clique em **executar** final Olá Olá experimentar tela e, em seguida, clique em **implantar o serviço da Web** e **implantar o serviço de Web [novo]**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="5b0ee-119">página de implantação de saudação do Gerenciador de serviço de Web de aprendizado de máquina Olá será aberto.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="5b0ee-120">Página de teste de implantação do Gerente de Serviços Web de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b0ee-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="5b0ee-121">Na página de teste implantar hello, insira um nome para o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="5b0ee-122">Selecione um plano de preços.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-122">Select a pricing plan.</span></span> <span data-ttu-id="5b0ee-123">Se você tiver um plano de preços existente, que você poderá selecioná-lo, caso contrário, você deve criar um novo plano de preço para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="5b0ee-124">Em Olá **plano de preço** lista suspensa, selecione um plano existente ou selecione Olá **selecione novo plano** opção.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="5b0ee-125">Em **nome do plano de**, digite um nome que identifique Olá plano na sua conta.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="5b0ee-126">Selecione uma saudação **níveis mensal planejar**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="5b0ee-127">Observe que as camadas de plano de saudação padrão toohello planos para a sua região padrão e o serviço web é implantado toothat região.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="5b0ee-128">Clique em **implantar** e Olá página de início rápido para o serviço web é aberta.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="5b0ee-129">Página Início Rápido</span><span class="sxs-lookup"><span data-stu-id="5b0ee-129">Quickstart page</span></span>
<span data-ttu-id="5b0ee-130">página de início rápido de serviço Olá web fornece acesso e orientação em tarefas mais comuns hello, que você irá executar depois de criar um novo serviço web.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="5b0ee-131">A partir daqui, você pode acessar facilmente os dois Olá **teste** página e **consumir** página.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="5b0ee-132">Testando seu serviço Web</span><span class="sxs-lookup"><span data-stu-id="5b0ee-132">Testing your web service</span></span>
<span data-ttu-id="5b0ee-133">Na página de início rápido de saudação, clique em Testar serviço web em tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="5b0ee-134">serviço web tootest hello como um serviço de solicitação-resposta (RR):</span><span class="sxs-lookup"><span data-stu-id="5b0ee-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="5b0ee-135">Clique em **teste** na barra de menus do hello.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="5b0ee-136">Clique em **Solicitação-Resposta**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="5b0ee-137">Insira os valores apropriados para colunas de entrada hello de sua experiência.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="5b0ee-138">Clique em **Solicitação-Resposta**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="5b0ee-139">Resultados serão exibido no lado direito Olá da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="5b0ee-140">tootest um serviço de web do serviço de execução de lote (BES), você usará um arquivo CSV:</span><span class="sxs-lookup"><span data-stu-id="5b0ee-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="5b0ee-141">Clique em **teste** na barra de menus do hello.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="5b0ee-142">Clique em **Lote**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-142">Click **Batch**.</span></span>
* <span data-ttu-id="5b0ee-143">Em sua entrada, clique em Procurar e navegue tooyour arquivo de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="5b0ee-144">Clique em **Testar**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-144">Click **Test**.</span></span>

<span data-ttu-id="5b0ee-145">status de saudação do teste é exibido em **testar trabalhos de lote**.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="5b0ee-146">Consumindo seu serviço Web</span><span class="sxs-lookup"><span data-stu-id="5b0ee-146">Consuming your Web Service</span></span>
<span data-ttu-id="5b0ee-147">Quando implantado como um serviço Web, os testes de Azure Machine Learning fornecem uma API REST que pode ser consumida por uma ampla variedade de dispositivos e plataformas.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="5b0ee-148">Isso ocorre porque as mensagens formatadas em Olá API REST simples aceita e responde com JSON.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="5b0ee-149">Olá, portal de aprendizado de máquina do Azure fornece código que pode ser usado toocall Olá web Services em R, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="5b0ee-150">Na página de consomem hello, você encontrará:</span><span class="sxs-lookup"><span data-stu-id="5b0ee-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="5b0ee-151">Olá API de chave e URI para o consumo de serviço da web em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="5b0ee-152">Tookick de modelos de aplicativo web e Excel iniciar o processo de consumo.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="5b0ee-153">Código de exemplo em c#, python e R tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="5b0ee-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="5b0ee-154">Para obter mais informações sobre o consumo de serviços web, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="5b0ee-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b0ee-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b0ee-155">Next Steps</span></span>
<span data-ttu-id="5b0ee-156">Para obter mais informações sobre o consumo dos serviços Web, consulte:</span><span class="sxs-lookup"><span data-stu-id="5b0ee-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="5b0ee-157">Como tooconsume um serviço Web de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="5b0ee-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="5b0ee-158">Serviços Web do Azure Machine Learning: implantação e consumo</span><span class="sxs-lookup"><span data-stu-id="5b0ee-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
