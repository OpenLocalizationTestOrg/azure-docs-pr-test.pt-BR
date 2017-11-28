---
title: "aaaCreate uma função no Azure acionado por um webhook genérico | Microsoft Docs"
description: "Use as funções do Azure toocreate uma função sem servidor que é invocada por um webhook no Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="801ea-103">Criar uma função disparada por um webhook genérico</span><span class="sxs-lookup"><span data-stu-id="801ea-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="801ea-104">As funções do Azure permite que você execute seu código em um ambiente sem servidor sem ter que toofirst criar uma VM ou publicar um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="801ea-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="801ea-105">Por exemplo, você pode configurar um toobe função disparado por um alerta gerado pelo Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="801ea-105">For example, you can configure a function toobe triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="801ea-106">Este tópico mostra como o código c# tooexecute quando um grupo de recursos é adicionado tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="801ea-106">This topic shows you how tooexecute C# code when a resource group is added tooyour subscription.</span></span>   

![Webhook genérico disparado função hello portal do Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="801ea-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="801ea-108">Prerequisites</span></span> 

<span data-ttu-id="801ea-109">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="801ea-109">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="801ea-110">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="801ea-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="801ea-111">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="801ea-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="801ea-112">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="801ea-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="801ea-113"><a name="create-function"></a>Criar uma função disparada por um webhook genérico</span><span class="sxs-lookup"><span data-stu-id="801ea-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="801ea-114">Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="801ea-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="801ea-115">Se essa função é hello um primeiro em seu aplicativo de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="801ea-115">If this function is hello first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="801ea-116">Isso exibe o conjunto completo de saudação de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="801ea-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="801ea-118">Selecione Olá **WebHook genérico - C#** modelo.</span><span class="sxs-lookup"><span data-stu-id="801ea-118">Select hello **Generic WebHook - C#** template.</span></span> <span data-ttu-id="801ea-119">Digite um nome para sua função C# e selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="801ea-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Crie uma função genérica webhook disparado no hello portal do Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="801ea-121">Em sua nova função, clique em **<> / Get função URL**, copie e salve o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-121">In your new function, click **</> Get function URL**, then copy and save hello value.</span></span> <span data-ttu-id="801ea-122">Você usa esse webhook de saudação do valor tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="801ea-122">You use this value tooconfigure hello webhook.</span></span> 

    ![Examine o código de função hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="801ea-124">Em seguida, crie um ponto de extremidade de webhook em um alerta do log de atividades no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="801ea-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="801ea-125">Criar um alerta do log de atividades</span><span class="sxs-lookup"><span data-stu-id="801ea-125">Create an activity log alert</span></span>

1. <span data-ttu-id="801ea-126">Olá portal do Azure no, navegue toohello **Monitor** serviço, selecione **alertas**e clique em **adicionar alerta do log de atividade**.</span><span class="sxs-lookup"><span data-stu-id="801ea-126">In hello Azure portal, navigate toohello **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Monitoramento](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="801ea-128">Usar configurações de saudação conforme especificado na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="801ea-128">Use hello settings as specified in hello table:</span></span>

    ![Criar um alerta do log de atividades](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="801ea-130">Configuração</span><span class="sxs-lookup"><span data-stu-id="801ea-130">Setting</span></span>      |  <span data-ttu-id="801ea-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="801ea-131">Suggested value</span></span>   | <span data-ttu-id="801ea-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="801ea-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="801ea-133">**Nome do alerta do log de atividades**</span><span class="sxs-lookup"><span data-stu-id="801ea-133">**Activity log alert name**</span></span> | <span data-ttu-id="801ea-134">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="801ea-134">resource-group-create-alert</span></span> | <span data-ttu-id="801ea-135">Nome do alerta de log de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-135">Name of hello activity log alert.</span></span> |
    | <span data-ttu-id="801ea-136">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="801ea-136">**Subscription**</span></span> | <span data-ttu-id="801ea-137">Sua assinatura</span><span class="sxs-lookup"><span data-stu-id="801ea-137">Your subscription</span></span> | <span data-ttu-id="801ea-138">assinatura de saudação que você está usando para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="801ea-138">hello subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="801ea-139">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="801ea-139">**Resource Group**</span></span> | <span data-ttu-id="801ea-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="801ea-140">myResourceGroup</span></span> | <span data-ttu-id="801ea-141">grupo de recursos de Olá recursos de alerta de saudação são implantados.</span><span class="sxs-lookup"><span data-stu-id="801ea-141">hello resource group that hello alert resources are deployed to.</span></span> <span data-ttu-id="801ea-142">Usando Olá o mesmo grupo de recursos, como seu aplicativo de função torna mais fácil tooclean depois de concluir o tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-142">Using hello same resource group as your function app makes it easier tooclean up after you complete hello tutorial.</span></span> |
    | <span data-ttu-id="801ea-143">**Categoria de eventos**</span><span class="sxs-lookup"><span data-stu-id="801ea-143">**Event category**</span></span> | <span data-ttu-id="801ea-144">Administrativo</span><span class="sxs-lookup"><span data-stu-id="801ea-144">Administrative</span></span> | <span data-ttu-id="801ea-145">Essa categoria inclui as alterações feitas tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="801ea-145">This category includes changes made tooAzure resources.</span></span>  |
    | <span data-ttu-id="801ea-146">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="801ea-146">**Resource type**</span></span> | <span data-ttu-id="801ea-147">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="801ea-147">Resource groups</span></span> | <span data-ttu-id="801ea-148">Filtros de atividades em grupo tooresource alertas.</span><span class="sxs-lookup"><span data-stu-id="801ea-148">Filters alerts tooresource group activities.</span></span> |
    | <span data-ttu-id="801ea-149">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="801ea-149">**Resource Group**</span></span><br/><span data-ttu-id="801ea-150">e **Recurso**</span><span class="sxs-lookup"><span data-stu-id="801ea-150">and **Resource**</span></span> | <span data-ttu-id="801ea-151">Todos</span><span class="sxs-lookup"><span data-stu-id="801ea-151">All</span></span> | <span data-ttu-id="801ea-152">Monitore todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="801ea-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="801ea-153">**Nome da operação**</span><span class="sxs-lookup"><span data-stu-id="801ea-153">**Operation name**</span></span> | <span data-ttu-id="801ea-154">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="801ea-154">Create Resource Group</span></span> | <span data-ttu-id="801ea-155">Filtra as operações toocreate de alertas.</span><span class="sxs-lookup"><span data-stu-id="801ea-155">Filters alerts toocreate operations.</span></span> |
    | <span data-ttu-id="801ea-156">**Level**</span><span class="sxs-lookup"><span data-stu-id="801ea-156">**Level**</span></span> | <span data-ttu-id="801ea-157">Informativo</span><span class="sxs-lookup"><span data-stu-id="801ea-157">Informational</span></span> | <span data-ttu-id="801ea-158">Inclua os alertas de nível informativo.</span><span class="sxs-lookup"><span data-stu-id="801ea-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="801ea-159">**Status**</span><span class="sxs-lookup"><span data-stu-id="801ea-159">**Status**</span></span> | <span data-ttu-id="801ea-160">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="801ea-160">Succeeded</span></span> | <span data-ttu-id="801ea-161">Filtra tooactions alertas que foram concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="801ea-161">Filters alerts tooactions that have completed successfully.</span></span> |
    | <span data-ttu-id="801ea-162">**Grupo de ações**</span><span class="sxs-lookup"><span data-stu-id="801ea-162">**Action group**</span></span> | <span data-ttu-id="801ea-163">Novo</span><span class="sxs-lookup"><span data-stu-id="801ea-163">New</span></span> | <span data-ttu-id="801ea-164">Crie um novo grupo de ação, que define Olá ação toma quando um alerta é gerado.</span><span class="sxs-lookup"><span data-stu-id="801ea-164">Create a new action group, which defines hello action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="801ea-165">**Nome do grupo de ações**</span><span class="sxs-lookup"><span data-stu-id="801ea-165">**Action group name**</span></span> | <span data-ttu-id="801ea-166">function-webhook</span><span class="sxs-lookup"><span data-stu-id="801ea-166">function-webhook</span></span> | <span data-ttu-id="801ea-167">Um grupo de ação do nome tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="801ea-167">A name tooidentify hello action group.</span></span>  | 
    | <span data-ttu-id="801ea-168">**Nome curto**</span><span class="sxs-lookup"><span data-stu-id="801ea-168">**Short name**</span></span> | <span data-ttu-id="801ea-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="801ea-169">funcwebhook</span></span> | <span data-ttu-id="801ea-170">Um nome curto para o grupo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-170">A short name for hello action group.</span></span> |  

3. <span data-ttu-id="801ea-171">Em **ações**, adicione uma ação usando configurações de saudação conforme especificado na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="801ea-171">In **Actions**, add an action using hello settings as specified in hello table:</span></span> 

    ![Adicionar um grupo de ações](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="801ea-173">Configuração</span><span class="sxs-lookup"><span data-stu-id="801ea-173">Setting</span></span>      |  <span data-ttu-id="801ea-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="801ea-174">Suggested value</span></span>   | <span data-ttu-id="801ea-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="801ea-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="801ea-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="801ea-176">**Name**</span></span> | <span data-ttu-id="801ea-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="801ea-177">CallFunctionWebhook</span></span> | <span data-ttu-id="801ea-178">Um nome para a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-178">A name for hello action.</span></span> |
    | <span data-ttu-id="801ea-179">**Tipo de ação**</span><span class="sxs-lookup"><span data-stu-id="801ea-179">**Action type**</span></span> | <span data-ttu-id="801ea-180">webhook</span><span class="sxs-lookup"><span data-stu-id="801ea-180">Webhook</span></span> | <span data-ttu-id="801ea-181">alerta de toohello Olá resposta é que uma URL de Webhook é chamada.</span><span class="sxs-lookup"><span data-stu-id="801ea-181">hello response toohello alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="801ea-182">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="801ea-182">**Details**</span></span> | <span data-ttu-id="801ea-183">URL da função</span><span class="sxs-lookup"><span data-stu-id="801ea-183">Function URL</span></span> | <span data-ttu-id="801ea-184">Cole a URL do webhook Olá da função de saudação que você copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="801ea-184">Paste in hello webhook URL of hello function that you copied earlier.</span></span> |<span data-ttu-id="801ea-185">v</span><span class="sxs-lookup"><span data-stu-id="801ea-185">v</span></span>

4. <span data-ttu-id="801ea-186">Clique em **Okey** toocreate Olá alerta e ação de grupo.</span><span class="sxs-lookup"><span data-stu-id="801ea-186">Click **OK** toocreate hello alert and action group.</span></span>  

<span data-ttu-id="801ea-187">Olá webhook agora é chamado quando um grupo de recursos é criado na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="801ea-187">hello webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="801ea-188">Em seguida, você atualizar o código de saudação na saudação de toohandle sua função dados de log JSON no corpo de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="801ea-188">Next, you update hello code in your function toohandle hello JSON log data in hello body of hello request.</span></span>   

## <a name="update-hello-function-code"></a><span data-ttu-id="801ea-189">Atualizar o código de função hello</span><span class="sxs-lookup"><span data-stu-id="801ea-189">Update hello function code</span></span>

1. <span data-ttu-id="801ea-190">Navegue de aplicativo de função tooyour Voltar no portal de saudação e, em seguida, expanda sua função.</span><span class="sxs-lookup"><span data-stu-id="801ea-190">Navigate back tooyour function app in hello portal, and expand your function.</span></span> 

2. <span data-ttu-id="801ea-191">Substitua o código de script de saudação c# em função hello no portal de saudação com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="801ea-191">Replace hello C# script code in hello function in hello portal with hello following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="801ea-192">Agora você pode testar a função hello, criando um novo grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="801ea-192">Now you can test hello function by creating a new resource group in your subscription.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="801ea-193">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="801ea-193">Test hello function</span></span>

1. <span data-ttu-id="801ea-194">Clique no ícone do grupo de recursos de saudação à esquerda de saudação do hello portal do Azure, selecione **+ adicionar**, digite um **nome do grupo de recursos**e selecione **criar** toocreate um grupo de recurso vazio.</span><span class="sxs-lookup"><span data-stu-id="801ea-194">Click hello resource group icon in hello left of hello Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** toocreate an empty resource group.</span></span>
    
    ![Crie um grupos de recursos.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="801ea-196">Voltar a função tooyour e expanda Olá **Logs** janela.</span><span class="sxs-lookup"><span data-stu-id="801ea-196">Go back tooyour function and expand hello **Logs** window.</span></span> <span data-ttu-id="801ea-197">Após a criação do grupo de recursos de saudação, gatilhos de alerta de log de atividade Olá Olá webhook e Olá função é executada.</span><span class="sxs-lookup"><span data-stu-id="801ea-197">After hello resource group is created, hello activity log alert triggers hello webhook and hello function executes.</span></span> <span data-ttu-id="801ea-198">Você verá o nome de saudação do grupo de recursos novos Olá gravado toohello logs.</span><span class="sxs-lookup"><span data-stu-id="801ea-198">You see hello name of hello new resource group written toohello logs.</span></span>  

    ![Adicione uma configuração de aplicativo de teste.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="801ea-200">(Opcional) Voltar e exclua o grupo de recursos de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="801ea-200">(Optional) Go back and delete hello resource group that you created.</span></span> <span data-ttu-id="801ea-201">Observe que essa atividade não aciona a função hello.</span><span class="sxs-lookup"><span data-stu-id="801ea-201">Note that this activity doesn't trigger hello function.</span></span> <span data-ttu-id="801ea-202">Isso ocorre porque excluir operações são filtradas pelo alerta hello.</span><span class="sxs-lookup"><span data-stu-id="801ea-202">This is because delete operations are filtered out by hello alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="801ea-203">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="801ea-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="801ea-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="801ea-204">Next steps</span></span>

<span data-ttu-id="801ea-205">Você criou uma função que é executada quando uma solicitação é recebida de um webhook genérico.</span><span class="sxs-lookup"><span data-stu-id="801ea-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="801ea-206">Para saber mais sobre gatilhos do webhook, veja [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="801ea-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="801ea-207">toolearn mais sobre o desenvolvimento de funções em c#, consulte [referência do desenvolvedor do Azure funções C# script](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="801ea-207">toolearn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

