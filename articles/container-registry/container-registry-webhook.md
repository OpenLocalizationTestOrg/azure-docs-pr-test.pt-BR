---
title: "aaaAzure contêiner do registro webhooks | Microsoft Docs"
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
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="ae9ef-104">Usar webhooks de registro de contêiner do Azure – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="ae9ef-105">Um registro de contêiner do Azure armazena e gerencia imagens de contêiner do Docker privadas, modo toohello semelhante Hub do Docker armazena imagens públicas do Docker.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="ae9ef-106">Use o webhooks tootrigger eventos quando certas ações ocorrem em um dos repositórios do registro.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="ae9ef-107">Webhooks pode responder tooevents no nível de registro de saudação ou eles podem ser definidos para baixo da marca do repositório específico tooa.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="ae9ef-108">Para obter mais informações e conceitos, consulte Olá [visão geral](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ef-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae9ef-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae9ef-109">Prerequisites</span></span> 

- <span data-ttu-id="ae9ef-110">Registro gerenciado de contêiner do Azure – crie um registro de contêiner gerenciado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="ae9ef-111">Por exemplo, usar Olá portal do Azure ou Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="ae9ef-112">Docker CLI - tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instale o mecanismo do Docker.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="ae9ef-113">Criar webhook no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="ae9ef-114">Faça logon no portal do Azure de toohello e navegue toohello registro no qual você deseja toocreate webhooks.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="ae9ef-115">Na folha de contêiner Olá, selecione a guia de "Webhooks" hello.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="ae9ef-116">Selecione "Adicionar" hello webhook folha da barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="ae9ef-117">Olá completa *Webhook criar* formulário com hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae9ef-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="ae9ef-118">Valor</span><span class="sxs-lookup"><span data-stu-id="ae9ef-118">Value</span></span> | <span data-ttu-id="ae9ef-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae9ef-119">Description</span></span> |
|---|---|
| <span data-ttu-id="ae9ef-120">Nome</span><span class="sxs-lookup"><span data-stu-id="ae9ef-120">Name</span></span> | <span data-ttu-id="ae9ef-121">Olá nome toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="ae9ef-122">Ele pode conter apenas letras minúsculas e números e entre 5 e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="ae9ef-123">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="ae9ef-123">Service URI</span></span> | <span data-ttu-id="ae9ef-124">Olá URI onde Olá webhook enviar notificações de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="ae9ef-125">Cabeçalhos personalizados</span><span class="sxs-lookup"><span data-stu-id="ae9ef-125">Custom headers</span></span> | <span data-ttu-id="ae9ef-126">Cabeçalhos de que deseja toopass junto com a solicitação POST hello.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="ae9ef-127">Eles devem estar no formato "chave: valor".</span><span class="sxs-lookup"><span data-stu-id="ae9ef-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="ae9ef-128">Ações de gatilho</span><span class="sxs-lookup"><span data-stu-id="ae9ef-128">Trigger actions</span></span> | <span data-ttu-id="ae9ef-129">Ações que disparam Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="ae9ef-130">No momento webhooks podem ser acionados por push e/ou excluir ações tooan imagem.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="ae9ef-131">Status</span><span class="sxs-lookup"><span data-stu-id="ae9ef-131">Status</span></span> | <span data-ttu-id="ae9ef-132">status de saudação do webhook Olá depois que ele é criado.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="ae9ef-133">Ele é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-133">It's enabled by default.</span></span> |
| <span data-ttu-id="ae9ef-134">Escopo</span><span class="sxs-lookup"><span data-stu-id="ae9ef-134">Scope</span></span> | <span data-ttu-id="ae9ef-135">escopo de saudação no que funciona de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="ae9ef-136">Por padrão o escopo de saudação é para todos os eventos no registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="ae9ef-137">Pode ser especificado para um repositório ou uma marca usando o formato de saudação "repositório: marca".</span><span class="sxs-lookup"><span data-stu-id="ae9ef-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="ae9ef-138">Formulário de webhook de exemplo:</span><span class="sxs-lookup"><span data-stu-id="ae9ef-138">Example webhook form:</span></span>

![INTERFACE DO USUÁRIO DE DC/SO](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="ae9ef-140">Criar webhook na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="ae9ef-141">toocreate usando um webhook Olá CLI do Azure, use Olá [criar az acr webhook](/cli/azure/acr/webhook#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="ae9ef-142">Testar webhook</span><span class="sxs-lookup"><span data-stu-id="ae9ef-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ae9ef-143">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-143">Azure portal</span></span>

<span data-ttu-id="ae9ef-144">Toousing anterior Olá webhook no contêiner imagem push e ações de exclusão, pode ser testado usando Olá **Ping** botão.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="ae9ef-145">Quando usado, Olá Ping envia que um toohello de solicitação post genérico especificado logs e o ponto de extremidade Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="ae9ef-146">Isso é útil tooverify que Olá webhook foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="ae9ef-147">Selecione webhook Olá deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="ae9ef-148">Na barra de ferramentas superior Olá, selecione a ação de "Ping" hello.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="ae9ef-149">Seleção Olá solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="ae9ef-150">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-150">Azure CLI</span></span>

<span data-ttu-id="ae9ef-151">tootest um webhook ACR com hello CLI do Azure, use Olá [ping de webhook acr az](/cli/azure/acr/webhook#ping) comando.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="ae9ef-152">resultados de saudação toosee, use Olá [az acr lista webhook eventos](/cli/azure/acr/webhook#list-events) comando.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="ae9ef-153">Excluir webhook</span><span class="sxs-lookup"><span data-stu-id="ae9ef-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ae9ef-154">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-154">Azure portal</span></span>

<span data-ttu-id="ae9ef-155">Cada webhook pode ser excluído selecionando webhook hello e botão de exclusão de Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ef-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="ae9ef-156">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ae9ef-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```