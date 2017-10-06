---
title: aaaLearn como toomanage AzureML web services usando o gerenciamento de API | Microsoft Docs
description: Um guia mostrando como toomanage AzureML web services usando o gerenciamento de API.
keywords: "aprendizado de máquina, gerenciamento de api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="e80ed-104">Saiba como toomanage AzureML web services usando o gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="e80ed-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="e80ed-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e80ed-105">Overview</span></span>
<span data-ttu-id="e80ed-106">Este guia mostra como tooquickly começar a usar o gerenciamento de API toomanage serviços da web do AzureML.</span><span class="sxs-lookup"><span data-stu-id="e80ed-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="e80ed-107">O que é o Gerenciamento de API do Azure?</span><span class="sxs-lookup"><span data-stu-id="e80ed-107">What is Azure API Management?</span></span>
<span data-ttu-id="e80ed-108">O Gerenciamento de API do Azure é um serviço do Azure que permite que você gerencie seus pontos de extremidade da API REST, definindo o acesso do usuário, a limitação de uso e o monitoramento por painel.</span><span class="sxs-lookup"><span data-stu-id="e80ed-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="e80ed-109">Clique em [aqui](https://azure.microsoft.com/services/api-management/) para obter detalhes sobre o Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ed-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="e80ed-110">Clique em [aqui](../api-management/api-management-get-started.md) para um guia como tooget Introdução ao gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ed-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="e80ed-111">Essa outra guia, na qual este guia se baseia, aborda mais tópicos, incluindo configurações de notificação, faixa de preços, manipulação de resposta, autenticação do usuário, criação de produtos, assinaturas de desenvolvedor e dashboarding de uso.</span><span class="sxs-lookup"><span data-stu-id="e80ed-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="e80ed-112">O que é o AzureML?</span><span class="sxs-lookup"><span data-stu-id="e80ed-112">What is AzureML?</span></span>
<span data-ttu-id="e80ed-113">AzureML é um serviço do Azure para o aprendizado de máquina que permite construir tooeasily, implantar e compartilhar soluções de análise avançada.</span><span class="sxs-lookup"><span data-stu-id="e80ed-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="e80ed-114">Clique em [aqui](https://azure.microsoft.com/services/machine-learning/) para obter detalhes sobre AzureML.</span><span class="sxs-lookup"><span data-stu-id="e80ed-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e80ed-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e80ed-115">Prerequisites</span></span>
<span data-ttu-id="e80ed-116">toocomplete neste guia, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e80ed-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="e80ed-117">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ed-117">An Azure account.</span></span> <span data-ttu-id="e80ed-118">Se você não tiver uma conta do Azure, clique em [aqui](https://azure.microsoft.com/pricing/free-trial/) para obter detalhes sobre como toocreate uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="e80ed-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="e80ed-119">Uma conta do AzureML.</span><span class="sxs-lookup"><span data-stu-id="e80ed-119">An AzureML account.</span></span> <span data-ttu-id="e80ed-120">Se você não tiver uma conta do AzureML, clique em [aqui](https://studio.azureml.net/) para obter detalhes sobre como toocreate uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="e80ed-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="e80ed-121">espaço de trabalho Hello, serviço e api_key de um experimento AzureML implantado como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="e80ed-122">Clique em [aqui](machine-learning-create-experiment.md) para obter detalhes sobre como toocreate uma AzureML experiências.</span><span class="sxs-lookup"><span data-stu-id="e80ed-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="e80ed-123">Clique em [aqui](machine-learning-publish-a-machine-learning-web-service.md) para obter detalhes sobre como toodeploy uma AzureML experimentar como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="e80ed-124">Como alternativa, o Apêndice A tem instruções sobre como toocreate e teste uma simple AzureML experimentar e implantação-lo como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="e80ed-125">Criar uma instância de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="e80ed-125">Create an API Management instance</span></span>
<span data-ttu-id="e80ed-126">Abaixo estão as etapas de Olá para usar o gerenciamento de API toomanage seu serviço de web do AzureML.</span><span class="sxs-lookup"><span data-stu-id="e80ed-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="e80ed-127">Primeiro, crie uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e80ed-127">First create a service instance.</span></span> <span data-ttu-id="e80ed-128">Faça logon no toohello [Portal clássico](https://manage.windowsazure.com/) e clique em **novo** > **serviços de aplicativos** > **gerenciamento de API**  >  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="e80ed-130">Especifique uma **URL**exclusiva.</span><span class="sxs-lookup"><span data-stu-id="e80ed-130">Specify a unique **URL**.</span></span> <span data-ttu-id="e80ed-131">Este guia usa **demoazureml** – você precisará toochoose algo diferente.</span><span class="sxs-lookup"><span data-stu-id="e80ed-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="e80ed-132">Escolha a saudação desejada **assinatura** e **região** para sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e80ed-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="e80ed-133">Depois de fazer suas seleções, clique no botão Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="e80ed-135">Especifique um valor para Olá **nome da organização**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="e80ed-136">Este guia usa **demoazureml** – você precisará toochoose algo diferente.</span><span class="sxs-lookup"><span data-stu-id="e80ed-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="e80ed-137">Insira seu endereço de email no hello **email do administrador** campo.</span><span class="sxs-lookup"><span data-stu-id="e80ed-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="e80ed-138">Este endereço de email é usado para notificações do sistema de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="e80ed-140">Clique em toocreate de caixa de seleção Olá sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e80ed-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="e80ed-141">*Ocupe toothirty minutos para um novo toobe de serviço criada*.</span><span class="sxs-lookup"><span data-stu-id="e80ed-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="e80ed-142">Criar hello API</span><span class="sxs-lookup"><span data-stu-id="e80ed-142">Create hello API</span></span>
<span data-ttu-id="e80ed-143">Depois de criar a instância do serviço hello, Olá próxima etapa é toocreate Olá API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="e80ed-144">Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="e80ed-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="e80ed-145">Operações de API são serviços da web de tooexisting por proxy.</span><span class="sxs-lookup"><span data-stu-id="e80ed-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="e80ed-146">Este guia cria APIs que toohello proxy existente AzureML RRS e BES serviços da web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="e80ed-147">APIs são criados e configurados da saudação API portal do publicador, que pode é acessada por meio de saudação Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ed-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="e80ed-148">tooreach Olá selecione portal do publicador a sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e80ed-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="e80ed-150">Clique em **gerenciar** em hello Portal clássico do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="e80ed-152">Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="e80ed-154">Tipo **API de demonstração do AzureML** como Olá **nome de API da Web**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="e80ed-155">Tipo **https://ussouthcentral.services.azureml.net** como Olá **URL do serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="e80ed-156">Tipo **azureml demonstração** como Olá **sufixo de URL da API da Web**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="e80ed-157">Verificar **HTTPS** como Olá **URL da API da Web** esquema.</span><span class="sxs-lookup"><span data-stu-id="e80ed-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="e80ed-158">Selecione **Iniciador** como **Produtos**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="e80ed-159">Quando terminar, clique em **salvar** toocreate Olá API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="e80ed-161">Adicionar operações Olá</span><span class="sxs-lookup"><span data-stu-id="e80ed-161">Add hello operations</span></span>
<span data-ttu-id="e80ed-162">Clique em **Adicionar operação** tooadd operações toothis API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="e80ed-164">Olá **nova operação** janela será exibida e Olá **assinatura** guia será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="e80ed-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="e80ed-165">Adicionar operação RRS</span><span class="sxs-lookup"><span data-stu-id="e80ed-165">Add RRS Operation</span></span>
<span data-ttu-id="e80ed-166">Primeiro, crie uma operação para Olá serviço AzureML RRS.</span><span class="sxs-lookup"><span data-stu-id="e80ed-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="e80ed-167">Selecione **POST** como Olá **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="e80ed-168">Tipo **/services/ /workspaces/ {espaço de trabalho} {serviço} / executar? api-version = {apiversion} & detalhes = {detalhes}** como Olá **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="e80ed-169">Tipo **RRS executar** como Olá **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="e80ed-171">Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="e80ed-172">Clique em **salvar** toosave esta operação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="e80ed-174">Adicionar operações BES</span><span class="sxs-lookup"><span data-stu-id="e80ed-174">Add BES Operations</span></span>
<span data-ttu-id="e80ed-175">Capturas de tela não estão incluídas para Olá operações BES conforme forem toothose muito semelhante para a adição de operação de RRS hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="e80ed-176">Enviar (mas não iniciar) um trabalho de execução em lotes</span><span class="sxs-lookup"><span data-stu-id="e80ed-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="e80ed-177">Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="e80ed-178">Selecione **POST** para Olá **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="e80ed-179">Tipo **/services/ /workspaces/ {espaço de trabalho} {serviço} / trabalhos? api-version = {apiversion}** para Olá **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="e80ed-180">Tipo **BES enviar** para Olá **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="e80ed-181">Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="e80ed-182">Clique em **salvar** toosave esta operação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="e80ed-183">Iniciar um trabalho de execução em lotes</span><span class="sxs-lookup"><span data-stu-id="e80ed-183">Start a Batch Execution job</span></span>
<span data-ttu-id="e80ed-184">Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="e80ed-185">Selecione **POST** para Olá **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="e80ed-186">Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid} / iniciar? api-version = {apiversion}** para Olá **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="e80ed-187">Tipo **BES iniciar** para Olá **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="e80ed-188">Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="e80ed-189">Clique em **salvar** toosave esta operação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="e80ed-190">Obter status de saudação ou resultado de um trabalho de execução de lote</span><span class="sxs-lookup"><span data-stu-id="e80ed-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="e80ed-191">Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="e80ed-192">Selecione **obter** para Olá **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="e80ed-193">Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid}? api-version = {apiversion}** para Olá **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="e80ed-194">Tipo **BES Status** para Olá **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="e80ed-195">Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="e80ed-196">Clique em **salvar** toosave esta operação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="e80ed-197">Excluir um trabalho de execução em lote</span><span class="sxs-lookup"><span data-stu-id="e80ed-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="e80ed-198">Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="e80ed-199">Selecione **excluir** para Olá **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="e80ed-200">Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid}? api-version = {apiversion}** para Olá **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="e80ed-201">Tipo **BES excluir** para Olá **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="e80ed-202">Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="e80ed-203">Clique em **salvar** toosave esta operação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="e80ed-204">Chamar uma operação de saudação Portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="e80ed-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="e80ed-205">Operações podem ser chamadas diretamente no portal do desenvolvedor hello, que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API.</span><span class="sxs-lookup"><span data-stu-id="e80ed-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="e80ed-206">Nesta etapa guia você chamará Olá **RRS executar** método foi adicionado toohello **AzureML demonstração API**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="e80ed-207">Clique em **portal do desenvolvedor** do menu de saudação à saudação parte superior direita da saudação Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="e80ed-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="e80ed-209">Clique em **APIs** no menu superior hello e clique **AzureML demonstração API** toosee operações de saudação disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e80ed-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="e80ed-211">Selecione **RRS executar** para operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="e80ed-212">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-212">Click **Try It**.</span></span>

![avaliar](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="e80ed-214">Para parâmetros de solicitação, digite sua **espaço de trabalho**, **service**, **2.0** para Olá **apiversion**, e **true**para Olá **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="e80ed-215">Você pode encontrar o **espaço de trabalho** e **service** no painel de serviço web do hello AzureML (consulte **testar Olá web serviço** no Apêndice A).</span><span class="sxs-lookup"><span data-stu-id="e80ed-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="e80ed-216">Para cabeçalhos Request, clique em **Adicionar cabeçalho** e digite **Content-Type** e **application/json**; em seguida, clique em **Adicionar cabeçalho** e digite **Authorization** e **Bearer<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="e80ed-217">Você pode encontrar o **chave api** no painel de serviço web do hello AzureML (consulte **testar Olá web serviço** no Apêndice A).</span><span class="sxs-lookup"><span data-stu-id="e80ed-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="e80ed-218">Tipo **{"Entradas": {"Entrada1": {"ColumnNames": ["Col2"], "valores": [["Este é um bom dia"]]}}, "GlobalParameters": {}}** para o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="e80ed-220">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-220">Click **Send**.</span></span>

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="e80ed-222">Depois que uma operação é invocada, portal do desenvolvedor Olá exibe Olá **URL solicitada** do serviço de back-end hello, Olá **status da resposta**, Olá **cabeçalhos de resposta**, e qualquer **conteúdo de resposta**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="e80ed-224">Apêndice A - criando e testando um serviço Web do AzureML simples</span><span class="sxs-lookup"><span data-stu-id="e80ed-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="e80ed-225">Criando experimento Olá</span><span class="sxs-lookup"><span data-stu-id="e80ed-225">Creating hello experiment</span></span>
<span data-ttu-id="e80ed-226">Abaixo estão as etapas de saudação para criar uma experiência simples do AzureML e implantá-lo como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="e80ed-227">Olá leva de serviço da web como uma coluna de texto arbitrário de entrada e retorna um conjunto de recursos representado como números inteiros.</span><span class="sxs-lookup"><span data-stu-id="e80ed-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="e80ed-228">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e80ed-228">For example:</span></span>

| <span data-ttu-id="e80ed-229">Texto</span><span class="sxs-lookup"><span data-stu-id="e80ed-229">Text</span></span> | <span data-ttu-id="e80ed-230">Texto marcado com sustenido</span><span class="sxs-lookup"><span data-stu-id="e80ed-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="e80ed-231">Este é um bom dia</span><span class="sxs-lookup"><span data-stu-id="e80ed-231">This is a good day</span></span> |<span data-ttu-id="e80ed-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="e80ed-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="e80ed-233">Primeiro, usando um navegador de sua escolha, navegue até: [https://studio.azureml.net/](https://studio.azureml.net/) e insira sua toolog de credenciais no.</span><span class="sxs-lookup"><span data-stu-id="e80ed-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="e80ed-234">Em seguida, crie um novo teste em branco.</span><span class="sxs-lookup"><span data-stu-id="e80ed-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="e80ed-236">Renomeie-muito**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="e80ed-237">Expanda **Conjuntos de dados salvos** e arraste **Resenhas de livros da Amazon** para o teste.</span><span class="sxs-lookup"><span data-stu-id="e80ed-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="e80ed-239">Expanda **Transformação de Dados** e **Manipulação** e arraste **Selecionar Colunas do Conjunto de Dados** para o teste.</span><span class="sxs-lookup"><span data-stu-id="e80ed-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="e80ed-240">Conecte-se **revisões de livros da Amazon** muito**selecionar colunas no conjunto de dados**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="e80ed-242">Clique em **Selecionar Colunas do Conjunto de Dados** e em **Iniciar seletor de colunas** e selecione **Col2**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="e80ed-243">Clique em tooapply de marca de seleção Olá essas alterações.</span><span class="sxs-lookup"><span data-stu-id="e80ed-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="e80ed-245">Expanda **análises de texto** e arraste **hash de recurso** no experimento hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="e80ed-246">Conecte-se **selecionar colunas no conjunto de dados** muito**hash de recurso**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="e80ed-248">Tipo **3** para Olá **bitsize de hash**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="e80ed-249">Isso criará 8 (23) colunas.</span><span class="sxs-lookup"><span data-stu-id="e80ed-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="e80ed-251">Neste ponto, convém tooclick **executar** tootest experimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Executar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="e80ed-253">Criar um serviço Web</span><span class="sxs-lookup"><span data-stu-id="e80ed-253">Create a web service</span></span>
<span data-ttu-id="e80ed-254">Agora crie um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="e80ed-254">Now create a web service.</span></span> <span data-ttu-id="e80ed-255">Expanda **Serviço Web** e arraste **Entrada** para o teste.</span><span class="sxs-lookup"><span data-stu-id="e80ed-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="e80ed-256">Conecte-se **entrada** muito**hash de recurso**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="e80ed-257">Também arraste **saída** para seu teste.</span><span class="sxs-lookup"><span data-stu-id="e80ed-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="e80ed-258">Conecte-se **saída** muito**hash de recurso**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="e80ed-260">Clique em **Publicar serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="e80ed-262">Clique em **Sim** toopublish experimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="e80ed-264">Testar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="e80ed-264">Test hello web service</span></span>
<span data-ttu-id="e80ed-265">Um serviço Web AzureML consiste em RSS (serviço de solicitação/resposta) e pontos de extremidade BES (serviço de execução em lotes).</span><span class="sxs-lookup"><span data-stu-id="e80ed-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="e80ed-266">RSS é para execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="e80ed-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="e80ed-267">BES é para execução do trabalho assíncrono.</span><span class="sxs-lookup"><span data-stu-id="e80ed-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="e80ed-268">tootest de serviço web com fonte de Python de exemplo hello abaixo, você pode precisar toodownload e instalar hello Azure SDK para Python (consulte: [como tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="e80ed-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="e80ed-269">Você também precisará Olá **espaço de trabalho**, **service**, e **api_key** de sua experiência de fonte de exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="e80ed-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="e80ed-270">Você pode encontrar o espaço de trabalho de saudação e serviço clicando em **solicitação/resposta** ou **Batch Execution** para sua experiência no painel de serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="e80ed-272">Você pode encontrar hello **api_key** clicando em sua experiência no painel de serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="e80ed-274">Testar ponto de extremidade RRS</span><span class="sxs-lookup"><span data-stu-id="e80ed-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="e80ed-275">Botão de teste</span><span class="sxs-lookup"><span data-stu-id="e80ed-275">Test button</span></span>
<span data-ttu-id="e80ed-276">Um ponto de extremidade maneira fácil tootest Olá RRS é tooclick **teste** no painel de serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="e80ed-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="e80ed-278">Digite **Este é um bom dia** para **col2**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="e80ed-279">Clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e80ed-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="e80ed-281">Você verá algo semelhante a</span><span class="sxs-lookup"><span data-stu-id="e80ed-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="e80ed-283">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="e80ed-283">Sample Code</span></span>
<span data-ttu-id="e80ed-284">Outro tootest de maneira seus RRS é de código do cliente.</span><span class="sxs-lookup"><span data-stu-id="e80ed-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="e80ed-285">Se você clicar em **solicitação/resposta** Olá painel e rolagem toohello inferior, você verá o código de exemplo para c#, Python e R. Você também verá sintaxe Olá Olá RRS solicitação, incluindo o URI de solicitação hello, cabeçalhos e corpo.</span><span class="sxs-lookup"><span data-stu-id="e80ed-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="e80ed-286">Este guia mostra um exemplo de trabalho do Python.</span><span class="sxs-lookup"><span data-stu-id="e80ed-286">This guide shows a working Python example.</span></span> <span data-ttu-id="e80ed-287">Você precisará toomodify com hello **espaço de trabalho**, **service**, e **api_key** de sua experiência.</span><span class="sxs-lookup"><span data-stu-id="e80ed-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="e80ed-288">Testar ponto de extremidade BES</span><span class="sxs-lookup"><span data-stu-id="e80ed-288">Test BES endpoint</span></span>
<span data-ttu-id="e80ed-289">Clique em **execução em lote** em Olá painel e rolagem toohello inferior.</span><span class="sxs-lookup"><span data-stu-id="e80ed-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="e80ed-290">Você verá o código de exemplo para c#, Python e R. Você também verá sintaxe Olá Olá BES solicitações toosubmit um trabalho, iniciar um trabalho, obter status de saudação ou os resultados de um trabalho e excluir um trabalho.</span><span class="sxs-lookup"><span data-stu-id="e80ed-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="e80ed-291">Este guia mostra um exemplo de trabalho do Python.</span><span class="sxs-lookup"><span data-stu-id="e80ed-291">This guide shows a working Python example.</span></span> <span data-ttu-id="e80ed-292">Você precisa toomodify com hello **espaço de trabalho**, **service**, e **api_key** de sua experiência.</span><span class="sxs-lookup"><span data-stu-id="e80ed-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="e80ed-293">Além disso, você precisa Olá toomodify **nome da conta de armazenamento**, **chave da conta de armazenamento**, e **nome do contêiner de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="e80ed-294">Por fim, você precisará de local de saudação toomodify de saudação **arquivo de entrada** e o local de saudação do hello **arquivo de saída**.</span><span class="sxs-lookup"><span data-stu-id="e80ed-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
