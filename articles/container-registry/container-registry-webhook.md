---
title: "Webhooks de registro de contêiner do Azure | Microsoft Docs"
description: "Webhooks de registro de contêiner do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, Contêineres, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="3dcad-104">Usar webhooks de registro de contêiner do Azure – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="3dcad-105">Um registro de contêiner do Azure armazena e gerencia imagens de contêiner privadas do Docker, de forma semelhante a como o Docker Hub armazena imagens públicas do Docker.</span><span class="sxs-lookup"><span data-stu-id="3dcad-105">An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="3dcad-106">Você usar webhooks para disparar eventos quando certas ações ocorrem em um dos repositórios do registro.</span><span class="sxs-lookup"><span data-stu-id="3dcad-106">You use webhooks to trigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="3dcad-107">Webhooks podem responder a eventos em nível de registro ou eles podem ter o escopo reduzido para a marca de um repositório específico.</span><span class="sxs-lookup"><span data-stu-id="3dcad-107">Webhooks can respond to events at the registry level or they can be scoped down to a specific repository tag.</span></span> 

<span data-ttu-id="3dcad-108">Para obter mais informações e conceitos, consulte a [visão geral](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3dcad-108">For more background and concepts, see the [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dcad-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3dcad-109">Prerequisites</span></span> 

- <span data-ttu-id="3dcad-110">Registro gerenciado de contêiner do Azure – crie um registro de contêiner gerenciado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcad-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="3dcad-111">Por exemplo, use o Portal do Azure ou a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="3dcad-111">For example, use the Azure portal or the Azure CLI 2.0.</span></span> 
- <span data-ttu-id="3dcad-112">CLI do Docker – para configurar o computador local como um host do Docker e acessar os comandos da CLI do Docker, instale o Mecanismo do Docker.</span><span class="sxs-lookup"><span data-stu-id="3dcad-112">Docker CLI - To set up your local computer as a Docker host and access the Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="3dcad-113">Criar webhook no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="3dcad-114">Faça logon no portal do Azure e navegue até o registro no qual você deseja criar webhooks.</span><span class="sxs-lookup"><span data-stu-id="3dcad-114">Log in to the Azure portal and navigate to the registry in which you want to create webhooks.</span></span> 

2. <span data-ttu-id="3dcad-115">Na folha do contêiner, selecione a guia "Webhooks".</span><span class="sxs-lookup"><span data-stu-id="3dcad-115">In the container blade, select the "Webhooks" tab.</span></span> 

3. <span data-ttu-id="3dcad-116">Selecione "Adicionar" na barra de ferramentas da folha do webhook.</span><span class="sxs-lookup"><span data-stu-id="3dcad-116">Select "Add" from the webhook blade toolbar.</span></span> 

4. <span data-ttu-id="3dcad-117">Complete o formulário *Criar Webhook* com as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3dcad-117">Complete the *Create Webhook* form with the following information:</span></span>

| <span data-ttu-id="3dcad-118">Valor</span><span class="sxs-lookup"><span data-stu-id="3dcad-118">Value</span></span> | <span data-ttu-id="3dcad-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="3dcad-119">Description</span></span> |
|---|---|
| <span data-ttu-id="3dcad-120">Nome</span><span class="sxs-lookup"><span data-stu-id="3dcad-120">Name</span></span> | <span data-ttu-id="3dcad-121">O nome que você deseja dar ao webhook.</span><span class="sxs-lookup"><span data-stu-id="3dcad-121">The name you want to give to the webhook.</span></span> <span data-ttu-id="3dcad-122">Ele pode conter apenas letras minúsculas e números e entre 5 e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3dcad-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="3dcad-123">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="3dcad-123">Service URI</span></span> | <span data-ttu-id="3dcad-124">O URI para que o webhook deveria enviar notificações POST.</span><span class="sxs-lookup"><span data-stu-id="3dcad-124">The URI where the webhook should send POST notifications.</span></span> |
| <span data-ttu-id="3dcad-125">Cabeçalhos personalizados</span><span class="sxs-lookup"><span data-stu-id="3dcad-125">Custom headers</span></span> | <span data-ttu-id="3dcad-126">Cabeçalhos que você deseja passar junto com a solicitação POST.</span><span class="sxs-lookup"><span data-stu-id="3dcad-126">Headers you want to pass along with the POST request.</span></span> <span data-ttu-id="3dcad-127">Eles devem estar no formato "chave: valor".</span><span class="sxs-lookup"><span data-stu-id="3dcad-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="3dcad-128">Ações de gatilho</span><span class="sxs-lookup"><span data-stu-id="3dcad-128">Trigger actions</span></span> | <span data-ttu-id="3dcad-129">Ações que disparam o webhook.</span><span class="sxs-lookup"><span data-stu-id="3dcad-129">Actions that trigger the webhook.</span></span> <span data-ttu-id="3dcad-130">Atualmente, webhooks podem ser acionados por ações de exclusão e/ou de push para uma imagem.</span><span class="sxs-lookup"><span data-stu-id="3dcad-130">Currently webhooks can be triggered by push and/or delete actions to an image.</span></span> |
| <span data-ttu-id="3dcad-131">Status</span><span class="sxs-lookup"><span data-stu-id="3dcad-131">Status</span></span> | <span data-ttu-id="3dcad-132">O status do webhook depois que ele é criado.</span><span class="sxs-lookup"><span data-stu-id="3dcad-132">The status for the webhook after it's created.</span></span> <span data-ttu-id="3dcad-133">Ele é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3dcad-133">It's enabled by default.</span></span> |
| <span data-ttu-id="3dcad-134">Escopo</span><span class="sxs-lookup"><span data-stu-id="3dcad-134">Scope</span></span> | <span data-ttu-id="3dcad-135">O escopo no qual o webhook funciona.</span><span class="sxs-lookup"><span data-stu-id="3dcad-135">The scope at which the webhook works.</span></span> <span data-ttu-id="3dcad-136">Por padrão, o escopo é para todos os eventos no registro.</span><span class="sxs-lookup"><span data-stu-id="3dcad-136">By default the scope is for all events in the registry.</span></span> <span data-ttu-id="3dcad-137">Pode ser especificado para um repositório ou uma marca usando o formato "repositório: marca".</span><span class="sxs-lookup"><span data-stu-id="3dcad-137">It can be specified for a repository or a tag by using the format "repository: tag".</span></span> |

<span data-ttu-id="3dcad-138">Formulário de webhook de exemplo:</span><span class="sxs-lookup"><span data-stu-id="3dcad-138">Example webhook form:</span></span>

![INTERFACE DO USUÁRIO DE DC/SO](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="3dcad-140">Criar webhook na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="3dcad-141">Para criar um webhook usando a CLI do Azure, use o comando [az acr webhook create](/cli/azure/acr/webhook#create).</span><span class="sxs-lookup"><span data-stu-id="3dcad-141">To create a webhook using the Azure CLI, use the [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="3dcad-142">Testar webhook</span><span class="sxs-lookup"><span data-stu-id="3dcad-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3dcad-143">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-143">Azure portal</span></span>

<span data-ttu-id="3dcad-144">Antes de usar o webhook em ações de exclusão e de push na imagem de contêiner, ele pode ser testado usando o botão **Executar ping**.</span><span class="sxs-lookup"><span data-stu-id="3dcad-144">Prior to using the webhook on container image push and delete actions, it can be tested using the **Ping** button.</span></span> <span data-ttu-id="3dcad-145">Quando usado, o Executar ping envia uma solicitação POST genérica para o ponto de extremidade especificado e registra a resposta.</span><span class="sxs-lookup"><span data-stu-id="3dcad-145">When used, the Ping sends a generic post request to the specified endpoint and logs the response.</span></span> <span data-ttu-id="3dcad-146">Isso é útil para verificar se o webhook foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="3dcad-146">This is helpful to verify that the webhook has been set up correctly.</span></span>

1. <span data-ttu-id="3dcad-147">Selecione o webhook que você deseja testar.</span><span class="sxs-lookup"><span data-stu-id="3dcad-147">Select the webhook you want to test.</span></span> 
2. <span data-ttu-id="3dcad-148">Na barra de ferramentas superior, selecione a ação "Executar ping".</span><span class="sxs-lookup"><span data-stu-id="3dcad-148">In the top toolbar, select the "Ping" action.</span></span> 
3. <span data-ttu-id="3dcad-149">Verifique a solicitação e a resposta.</span><span class="sxs-lookup"><span data-stu-id="3dcad-149">Check the request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="3dcad-150">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-150">Azure CLI</span></span>

<span data-ttu-id="3dcad-151">Para testar um webhook ACR com a CLI do Azure, use o comando [az acr webhook ping](/cli/azure/acr/webhook#ping).</span><span class="sxs-lookup"><span data-stu-id="3dcad-151">To test an ACR webhook with the Azure CLI, use the [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="3dcad-152">Para ver os resultados, use o comando [az acr webhook list-events](/cli/azure/acr/webhook#list-events).</span><span class="sxs-lookup"><span data-stu-id="3dcad-152">To see the results, use the [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="3dcad-153">Excluir webhook</span><span class="sxs-lookup"><span data-stu-id="3dcad-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3dcad-154">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-154">Azure portal</span></span>

<span data-ttu-id="3dcad-155">Cada webhook pode ser excluído selecionando-se o webhook e, em seguida, o botão Excluir no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcad-155">Each webhook can be deleted by selecting the webhook and then the delete button on the Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="3dcad-156">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcad-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```