---
title: "Saiba como gerenciar os serviços Web do AzureML usando o Gerenciamento de API | Microsoft Docs"
description: "Um guia mostrando como gerenciar os serviços Web do AzureML usando o Gerenciamento de API."
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="d15d9-104">Saiba como gerenciar os serviços Web do AzureML usando o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d15d9-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="d15d9-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d15d9-105">Overview</span></span>
<span data-ttu-id="d15d9-106">Este guia mostra como começar a usar rapidamente o Gerenciamento de API para gerenciar seus serviços Web do AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="d15d9-107">O que é o Gerenciamento de API do Azure?</span><span class="sxs-lookup"><span data-stu-id="d15d9-107">What is Azure API Management?</span></span>
<span data-ttu-id="d15d9-108">O Gerenciamento de API do Azure é um serviço do Azure que permite que você gerencie seus pontos de extremidade da API REST, definindo o acesso do usuário, a limitação de uso e o monitoramento por painel.</span><span class="sxs-lookup"><span data-stu-id="d15d9-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="d15d9-109">Clique em [aqui](https://azure.microsoft.com/services/api-management/) para obter detalhes sobre o Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d9-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="d15d9-110">Clique em [aqui](../api-management/api-management-get-started.md) para obter um guia sobre como começar a usar o Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d9-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="d15d9-111">Essa outra guia, na qual este guia se baseia, aborda mais tópicos, incluindo configurações de notificação, faixa de preços, manipulação de resposta, autenticação do usuário, criação de produtos, assinaturas de desenvolvedor e dashboarding de uso.</span><span class="sxs-lookup"><span data-stu-id="d15d9-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="d15d9-112">O que é o AzureML?</span><span class="sxs-lookup"><span data-stu-id="d15d9-112">What is AzureML?</span></span>
<span data-ttu-id="d15d9-113">O AzureML é um serviço do Azure para aprendizado de máquina que permite facilmente criar, implantar e compartilhar soluções de análise avançadas.</span><span class="sxs-lookup"><span data-stu-id="d15d9-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="d15d9-114">Clique em [aqui](https://azure.microsoft.com/services/machine-learning/) para obter detalhes sobre AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d15d9-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d15d9-115">Prerequisites</span></span>
<span data-ttu-id="d15d9-116">Para concluir este guia, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d15d9-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="d15d9-117">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d9-117">An Azure account.</span></span> <span data-ttu-id="d15d9-118">Se você não tiver uma conta do Azure, clique [aqui](https://azure.microsoft.com/pricing/free-trial/) para obter detalhes sobre como criar uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="d15d9-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="d15d9-119">Uma conta do AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-119">An AzureML account.</span></span> <span data-ttu-id="d15d9-120">Se você não tiver uma conta do AzureML, clique [aqui](https://studio.azureml.net/) para obter detalhes sobre como criar uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="d15d9-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="d15d9-121">O espaço de trabalho, o serviço e a api_key para um teste do AzureML implantado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="d15d9-122">Clique [aqui](machine-learning-create-experiment.md) para obter detalhes sobre como criar um teste do AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="d15d9-123">Clique [aqui](machine-learning-publish-a-machine-learning-web-service.md) para obter detalhes sobre como implantar um teste do AzureML como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="d15d9-124">Como alternativa, o Apêndice A traz instruções sobre como criar e testar um teste simples do AzureML e implantá-lo como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="d15d9-125">Criar uma instância de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d15d9-125">Create an API Management instance</span></span>
<span data-ttu-id="d15d9-126">A seguir estão as etapas para usar o Gerenciamento de API para gerenciar seu serviço Web do AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="d15d9-127">Primeiro, crie uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d15d9-127">First create a service instance.</span></span> <span data-ttu-id="d15d9-128">Faça logon no [Portal Clássico](https://manage.windowsazure.com/) e clique em **Novo** > **Serviços de Aplicativos** > **Gerenciamento de API** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="d15d9-130">Especifique uma **URL**exclusiva.</span><span class="sxs-lookup"><span data-stu-id="d15d9-130">Specify a unique **URL**.</span></span> <span data-ttu-id="d15d9-131">Este guia usa **demoazureml** – você precisará escolher algo diferente.</span><span class="sxs-lookup"><span data-stu-id="d15d9-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="d15d9-132">Selecione a **Assinatura** e a **Região** da sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d15d9-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="d15d9-133">Após fazer suas seleções, clique no botão Avançar.</span><span class="sxs-lookup"><span data-stu-id="d15d9-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="d15d9-135">Especifique um valor para o **Nome da Organização**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="d15d9-136">Este guia usa **demoazureml** – você precisará escolher algo diferente.</span><span class="sxs-lookup"><span data-stu-id="d15d9-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="d15d9-137">Insira seu endereço de email no campo **email do administrador** .</span><span class="sxs-lookup"><span data-stu-id="d15d9-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="d15d9-138">Esse endereço de email é usado para notificações do sistema de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="d15d9-140">Clique na caixa de seleção para criar sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d15d9-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="d15d9-141">*Demora até 30 minutos para um novo serviço ser criado*.</span><span class="sxs-lookup"><span data-stu-id="d15d9-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="d15d9-142">Criar a API</span><span class="sxs-lookup"><span data-stu-id="d15d9-142">Create the API</span></span>
<span data-ttu-id="d15d9-143">Após criar a instância de serviço, a próxima etapa é criar a API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="d15d9-144">Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d15d9-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="d15d9-145">Todas as operações de API são colocadas em proxies de serviços Web existentes.</span><span class="sxs-lookup"><span data-stu-id="d15d9-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="d15d9-146">Este guia cria APIs que atua como proxy para os serviços Web RRS e BES do AzureML existentes.</span><span class="sxs-lookup"><span data-stu-id="d15d9-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="d15d9-147">As APIs são criadas e configuradas no portal do editor de API, que pode ser acessado por meio do Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d9-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="d15d9-148">Para acessar o portal do editor, selecione a instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d15d9-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="d15d9-150">Clique em **Gerenciar** no Portal Clássico do Azure do seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="d15d9-152">Clique em **APIs** no menu **Gerenciamento de API** à esquerda e depois clique em **Adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="d15d9-154">Digite **AzureML demonstração API** como o **Nome da API Web**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="d15d9-155">Digite **https://ussouthcentral.services.azureml.net** como a **URL do serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="d15d9-156">Digite **azureml-demo** como o **sufixo da URL da API Web**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="d15d9-157">Marque **HTTPS** como o esquema de **URL da API Web**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="d15d9-158">Selecione **Iniciador** como **Produtos**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="d15d9-159">Quando terminar, clique em **Salvar** para criar a API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="d15d9-161">Adicionar as operações</span><span class="sxs-lookup"><span data-stu-id="d15d9-161">Add the operations</span></span>
<span data-ttu-id="d15d9-162">Clique em **Adicionar operação** para adicionar operações a esta API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="d15d9-164">A janela **Nova operação** será exibida e a guia **Assinatura** será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="d15d9-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="d15d9-165">Adicionar operação RRS</span><span class="sxs-lookup"><span data-stu-id="d15d9-165">Add RRS Operation</span></span>
<span data-ttu-id="d15d9-166">Primeiro, crie uma operação para o serviço RRS do AzureML.</span><span class="sxs-lookup"><span data-stu-id="d15d9-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="d15d9-167">Selecione **POST** como o **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="d15d9-168">Digite **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** como o **Modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="d15d9-169">Digite **RRS Execute** como o **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="d15d9-171">Clique em **Respostas** > **ADICIONAR** à esquerda e selecione **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="d15d9-172">Clique em **Salvar** para salvar esta operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="d15d9-174">Adicionar operações BES</span><span class="sxs-lookup"><span data-stu-id="d15d9-174">Add BES Operations</span></span>
<span data-ttu-id="d15d9-175">Capturas de tela não estão incluídas para as operações BES pois são muito semelhantes àquelas para adicionar a operação RRS.</span><span class="sxs-lookup"><span data-stu-id="d15d9-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="d15d9-176">Enviar (mas não iniciar) um trabalho de execução em lotes</span><span class="sxs-lookup"><span data-stu-id="d15d9-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="d15d9-177">Clique em **Adicionar operação** para adicionar a operação BES do AzureML à API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="d15d9-178">Selecione **POST** para o **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="d15d9-179">Digite **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** para o **Modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="d15d9-180">Digite **BES Submit** para o **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="d15d9-181">Clique em **Respostas** > **ADICIONAR** à esquerda e selecione **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="d15d9-182">Clique em **Salvar** para salvar esta operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="d15d9-183">Iniciar um trabalho de execução em lotes</span><span class="sxs-lookup"><span data-stu-id="d15d9-183">Start a Batch Execution job</span></span>
<span data-ttu-id="d15d9-184">Clique em **Adicionar operação** para adicionar a operação BES do AzureML à API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="d15d9-185">Selecione **POST** para o **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="d15d9-186">Digite **/workspaces/ {espaço} {serviço} /services/ /jobs/ {jobid} / iniciar? api-version = {apiversion}** para o **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="d15d9-187">Digite **BES Start** para o **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="d15d9-188">Clique em **Respostas** > **ADICIONAR** à esquerda e selecione **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="d15d9-189">Clique em **Salvar** para salvar esta operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="d15d9-190">Obter o status ou o resultado de um trabalho de execução em lotes</span><span class="sxs-lookup"><span data-stu-id="d15d9-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="d15d9-191">Clique em **Adicionar operação** para adicionar a operação BES do AzureML à API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="d15d9-192">Selecione **GET** para o **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="d15d9-193">Digite **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** para o **Modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="d15d9-194">Digite **BES Status** para o **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="d15d9-195">Clique em **Respostas** > **ADICIONAR** à esquerda e selecione **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="d15d9-196">Clique em **Salvar** para salvar esta operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="d15d9-197">Excluir um trabalho de execução em lote</span><span class="sxs-lookup"><span data-stu-id="d15d9-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="d15d9-198">Clique em **Adicionar operação** para adicionar a operação BES do AzureML à API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="d15d9-199">Selecione **DELETE** para o **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="d15d9-200">Digite **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** para o **Modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="d15d9-201">Digite **BES Delete** para o **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="d15d9-202">Clique em **Respostas** > **ADICIONAR** à esquerda e selecione **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="d15d9-203">Clique em **Salvar** para salvar esta operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="d15d9-204">Chamar uma operação no Portal do Desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="d15d9-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="d15d9-205">As operações podem ser chamadas diretamente do Portal do Desenvolvedor, que fornece uma forma conveniente de exibir e testar as operações de uma API.</span><span class="sxs-lookup"><span data-stu-id="d15d9-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="d15d9-206">Nesta etapa do guia, você chamará o método **RRS Execute** que foi adicionado à **API de demonstração do AzureML**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="d15d9-207">Clique em **Portal do desenvolvedor** no menu da parte superior direita do Portal Clássico.</span><span class="sxs-lookup"><span data-stu-id="d15d9-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="d15d9-209">Clique em **APIs** no menu superior e depois clique em **API de demonstração do AzureML** para ver as operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d15d9-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="d15d9-211">Selecione **RRS Execute** para a operação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="d15d9-212">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-212">Click **Try It**.</span></span>

![avaliar](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="d15d9-214">Para os parâmetros Request, digite seu **espaço de trabalho**, **serviço**, **2.0** para **apiversion** e **true** para **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="d15d9-215">Você pode encontrar o **espaço de trabalho** e o **serviço** no painel de serviço Web do AzureML (confira **Testar o serviço Web** no Apêndice A).</span><span class="sxs-lookup"><span data-stu-id="d15d9-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="d15d9-216">Para cabeçalhos Request, clique em **Adicionar cabeçalho** e digite **Content-Type** e **application/json**; em seguida, clique em **Adicionar cabeçalho** e digite **Authorization** e **Bearer<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="d15d9-217">Você pode encontrar a **chave de api** no painel de serviço Web do AzureML (confira **Testar o serviço Web** no Apêndice A).</span><span class="sxs-lookup"><span data-stu-id="d15d9-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="d15d9-218">Digite **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["Este é um bom dia"]]}}, "GlobalParameters": {}}** para o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="d15d9-220">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-220">Click **Send**.</span></span>

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="d15d9-222">Após invocar uma operação, o portal do desenvolvedor exibe a **URL solicitada** do serviço back-end, o **Status de resposta**, os **Cabeçalhos de resposta** e qualquer **Conteúdo de resposta**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="d15d9-224">Apêndice A - criando e testando um serviço Web do AzureML simples</span><span class="sxs-lookup"><span data-stu-id="d15d9-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="d15d9-225">Criando o teste</span><span class="sxs-lookup"><span data-stu-id="d15d9-225">Creating the experiment</span></span>
<span data-ttu-id="d15d9-226">Veja abaixo as etapas para criar um teste simples do AzureML e implantá-lo como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="d15d9-227">O serviço Web assume como entrada uma coluna de texto arbitrário e retorna um conjunto de recursos representados como números inteiros.</span><span class="sxs-lookup"><span data-stu-id="d15d9-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="d15d9-228">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d15d9-228">For example:</span></span>

| <span data-ttu-id="d15d9-229">Texto</span><span class="sxs-lookup"><span data-stu-id="d15d9-229">Text</span></span> | <span data-ttu-id="d15d9-230">Texto marcado com sustenido</span><span class="sxs-lookup"><span data-stu-id="d15d9-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="d15d9-231">Este é um bom dia</span><span class="sxs-lookup"><span data-stu-id="d15d9-231">This is a good day</span></span> |<span data-ttu-id="d15d9-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="d15d9-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="d15d9-233">Primeiro, usando um navegador de sua escolha, navegue até: [https://studio.azureml.net/](https://studio.azureml.net/) e insira suas credenciais para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="d15d9-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="d15d9-234">Em seguida, crie um novo teste em branco.</span><span class="sxs-lookup"><span data-stu-id="d15d9-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="d15d9-236">Renomeie-o para **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="d15d9-237">Expanda **Conjuntos de dados salvos** e arraste **Resenhas de livros da Amazon** para o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="d15d9-239">Expanda **Transformação de Dados** e **Manipulação** e arraste **Selecionar Colunas do Conjunto de Dados** para o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="d15d9-240">Conecte **Resenhas de livros da Amazon** a **Selecionar Colunas do Conjunto de Dados**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="d15d9-242">Clique em **Selecionar Colunas do Conjunto de Dados** e em **Iniciar seletor de colunas** e selecione **Col2**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="d15d9-243">Clique na marca de seleção para aplicar essas alterações.</span><span class="sxs-lookup"><span data-stu-id="d15d9-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="d15d9-245">Expanda **Análise de texto** e arraste **Hash de recurso** para o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="d15d9-246">Conecte **Selecionar Colunas no Conjunto de Dados** para **Hash de Funcionalidade**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="d15d9-248">Digite **3** para **Tamanho de Bit de Hash**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="d15d9-249">Isso criará 8 (23) colunas.</span><span class="sxs-lookup"><span data-stu-id="d15d9-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="d15d9-251">Neste ponto, talvez você queira clicar em **Executar** para verificar o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Executar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="d15d9-253">Criar um serviço Web</span><span class="sxs-lookup"><span data-stu-id="d15d9-253">Create a web service</span></span>
<span data-ttu-id="d15d9-254">Agora crie um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-254">Now create a web service.</span></span> <span data-ttu-id="d15d9-255">Expanda **Serviço Web** e arraste **Entrada** para o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="d15d9-256">Conecte **Entrada** a **Hash de Funcionalidade**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="d15d9-257">Também arraste **saída** para seu teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="d15d9-258">Conecte **Saída** a **Hash de Funcionalidade**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="d15d9-260">Clique em **Publicar serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="d15d9-262">Clique em **Sim** para publicar o teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="d15d9-264">Testar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="d15d9-264">Test the web service</span></span>
<span data-ttu-id="d15d9-265">Um serviço Web AzureML consiste em RSS (serviço de solicitação/resposta) e pontos de extremidade BES (serviço de execução em lotes).</span><span class="sxs-lookup"><span data-stu-id="d15d9-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="d15d9-266">RSS é para execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="d15d9-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="d15d9-267">BES é para execução do trabalho assíncrono.</span><span class="sxs-lookup"><span data-stu-id="d15d9-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="d15d9-268">Para testar o serviço Web com a fonte Python de exemplo a seguir, talvez seja necessário baixar e instalar o SDK do Azure para Python (consulte: [Como instalar Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="d15d9-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="d15d9-269">Você também precisará do **espaço de trabalho**, do **serviço** e da **api_key** do teste para a fonte de exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="d15d9-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="d15d9-270">Você pode encontrar o espaço de trabalho e o serviço clicando em **Solicitação/resposta** ou **Execução em lote** para o teste no painel de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="d15d9-272">Você pode encontrar a **api_key** clicando no teste no painel de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="d15d9-274">Testar ponto de extremidade RRS</span><span class="sxs-lookup"><span data-stu-id="d15d9-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="d15d9-275">Botão de teste</span><span class="sxs-lookup"><span data-stu-id="d15d9-275">Test button</span></span>
<span data-ttu-id="d15d9-276">Uma maneira fácil de testar o ponto de extremidade RRS é clicar em **Testar** no painel de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="d15d9-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="d15d9-278">Digite **Este é um bom dia** para **col2**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="d15d9-279">Clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="d15d9-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="d15d9-281">Você verá algo semelhante a</span><span class="sxs-lookup"><span data-stu-id="d15d9-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="d15d9-283">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="d15d9-283">Sample Code</span></span>
<span data-ttu-id="d15d9-284">Outra maneira de testar seu RRS é do código cliente.</span><span class="sxs-lookup"><span data-stu-id="d15d9-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="d15d9-285">Se você clicar em **Solicitação/resposta** no painel e rolar até o final, verá o código de exemplo para C#, Python e R. Também verá a sintaxe da solicitação RRS, incluindo o URI, os cabeçalhos e o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d15d9-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="d15d9-286">Este guia mostra um exemplo de trabalho do Python.</span><span class="sxs-lookup"><span data-stu-id="d15d9-286">This guide shows a working Python example.</span></span> <span data-ttu-id="d15d9-287">Você precisará modificar com o **espaço de trabalho**, o **serviço** e a **api_key** do teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="d15d9-288">Testar ponto de extremidade BES</span><span class="sxs-lookup"><span data-stu-id="d15d9-288">Test BES endpoint</span></span>
<span data-ttu-id="d15d9-289">Clique em **Execução em lote** no painel e role até o final.</span><span class="sxs-lookup"><span data-stu-id="d15d9-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="d15d9-290">Você verá o código de exemplo para C#, Python e R. Também verá a sintaxe das solicitações BES para enviar um trabalho, iniciar um trabalho, obter o status ou os resultados de um trabalho e excluir um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d15d9-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="d15d9-291">Este guia mostra um exemplo de trabalho do Python.</span><span class="sxs-lookup"><span data-stu-id="d15d9-291">This guide shows a working Python example.</span></span> <span data-ttu-id="d15d9-292">Você precisa modificar com o **espaço de trabalho**, o **serviço** e a **api_key** do teste.</span><span class="sxs-lookup"><span data-stu-id="d15d9-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="d15d9-293">Além disso, você precisa modificar o **nome da conta de armazenamento**, a **chave da conta de armazenamento** e o **nome do contêiner de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="d15d9-294">Por fim, você precisará modificar o local do **arquivo de entrada** e o local do **arquivo de saída**.</span><span class="sxs-lookup"><span data-stu-id="d15d9-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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
