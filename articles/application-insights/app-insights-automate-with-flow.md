---
title: processa a Azure Application Insights aaaAutomate Microsoft Flow
description: "Saiba como você pode usar o Microsoft Flow tooquickly automatizar processos repetíveis usando o conector do Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="cc1d0-103">Automatizar processos de informações de aplicativo do Azure com conector Olá para o Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="cc1d0-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="cc1d0-104">Você encontra-se repetidamente Olá mesmo consultas executadas em seu toocheck de dados de telemetria que o serviço está funcionando corretamente?</span><span class="sxs-lookup"><span data-stu-id="cc1d0-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="cc1d0-105">É buscam tooautomate essas consultas para descobrir tendências e anomalias e, em seguida, criar seus próprios fluxos de trabalho contorná-las? Hello Azure Application Insights connector (visualização) para Microsoft Flow é a ferramenta certa Olá para esses fins.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="cc1d0-106">Com essa integração, você agora pode automatizar diversos processos sem a necessidade de escrever nenhuma linha de código.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="cc1d0-107">Depois de criar um fluxo usando uma ação do Application Insights, o fluxo de saudação executa automaticamente a consulta de análise de informações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="cc1d0-108">Adicione também outras ações.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-108">You can add additional actions as well.</span></span> <span data-ttu-id="cc1d0-109">O Microsoft Flow disponibiliza centenas de ações.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="cc1d0-110">Por exemplo, você pode usar Microsoft Flow tooautomatically enviar uma notificação por email ou criar um bug no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="cc1d0-111">Você também pode usar uma saudação muitas [modelos](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) que estão disponíveis para o conector Olá para o Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="cc1d0-112">Esses modelos acelerar o processo de saudação de criação de um fluxo.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="cc1d0-113">Criar um fluxo para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc1d0-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="cc1d0-114">Neste tutorial, você aprenderá como toocreate um fluxo que usa Olá análise automática cluster algoritmo toogroup atributos nos dados Olá para um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="cc1d0-115">fluxo de saudação envia automaticamente resultados Olá por email, apenas um exemplo de como você pode usar Microsoft Flow e análises do aplicativo Insights juntos.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="cc1d0-116">Etapa 1: Criar um fluxo</span><span class="sxs-lookup"><span data-stu-id="cc1d0-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="cc1d0-117">Entrar muito[Microsoft Flow](http://flow.microsoft.com)e, em seguida, selecione **flui meu**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="cc1d0-118">Clique em **Criar um fluxo em branco**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="cc1d0-119">Etapa 2: Criar um gatilho para o fluxo</span><span class="sxs-lookup"><span data-stu-id="cc1d0-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="cc1d0-120">Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="cc1d0-121">Em hello **frequência** selecione **dia**e em Olá **intervalo** , digite **1**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Caixa de diálogo de gatilho do Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="cc1d0-123">Etapa 3: adicionar uma ação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc1d0-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="cc1d0-124">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="cc1d0-125">Pesquise por **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="cc1d0-126">Clique em **Versão Prévia do Azure Application Insights – Visualizar a versão prévia da consulta do Analytics**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Janela Executar consulta do Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="cc1d0-128">Etapa 4: Conectar-se o recurso do Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="cc1d0-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="cc1d0-129">toocomplete nesta etapa, você precisa de uma ID de aplicativo e uma chave de API para o recurso.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="cc1d0-130">Você pode recuperá-las de saudação portal do Azure, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="cc1d0-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID do aplicativo no portal do Azure de saudação](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="cc1d0-132">Forneça um nome para a conexão, juntamente com a chave de API e a ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Janela de conexão do Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="cc1d0-134">Etapa 5: Especificar hello consulta de análise e o tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="cc1d0-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="cc1d0-135">Este exemplo de consulta seleciona solicitações Olá falhado no último dia do hello e correlaciona-los com exceções que ocorreram como parte da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="cc1d0-136">Análise de correlaciona-las com base no identificador de operation_Id hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="cc1d0-137">consulta de saudação segmentos, em seguida, resultados hello usando algoritmo de autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="cc1d0-138">Quando você cria suas próprias consultas, verifique se estão funcionando corretamente na análise antes de adicioná-lo tooyour fluxo.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="cc1d0-139">Adicionar Olá após a consulta de análise e, em seguida, selecione o tipo de gráfico de tabela HTML de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Janela de configuração de consulta do Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="cc1d0-141">Etapa 6: Configurar o email de toosend fluxo Olá</span><span class="sxs-lookup"><span data-stu-id="cc1d0-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="cc1d0-142">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="cc1d0-143">Pesquise por **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="cc1d0-144">Clique em **Office 365 Outlook – Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Janela de seleção do Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="cc1d0-146">Em Olá **enviar um email** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc1d0-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="cc1d0-147">a.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-147">a.</span></span> <span data-ttu-id="cc1d0-148">Digite o endereço de email de saudação do destinatário hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="cc1d0-149">b.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-149">b.</span></span> <span data-ttu-id="cc1d0-150">Digite o assunto do email de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="cc1d0-151">c.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-151">c.</span></span> <span data-ttu-id="cc1d0-152">Clique em qualquer lugar Olá **corpo** caixa e, em seguida, em Olá conteúdo menu dinâmico que é aberto no hello direito, selecione **corpo**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="cc1d0-153">d.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-153">d.</span></span> <span data-ttu-id="cc1d0-154">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-154">Click **Show advanced options**.</span></span>

    ![Configuração do Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="cc1d0-156">No menu de conteúdo dinâmico Olá, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc1d0-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="cc1d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-157">a.</span></span> <span data-ttu-id="cc1d0-158">Selecione o **Nome do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="cc1d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-159">b.</span></span> <span data-ttu-id="cc1d0-160">Selecione o **Conteúdo do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="cc1d0-161">c.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-161">c.</span></span> <span data-ttu-id="cc1d0-162">Em Olá **é HTML** selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Janela de configuração de email do Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="cc1d0-164">Etapa 7: Salvar e testar o fluxo</span><span class="sxs-lookup"><span data-stu-id="cc1d0-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="cc1d0-165">Em Olá **nome do fluxo de** caixa, adicione um nome para o fluxo e, em seguida, clique em **criar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="cc1d0-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Janela de criação de fluxo](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="cc1d0-167">Você pode aguardar Olá gatilho toorun essa ação ou você pode executar o fluxo de saudação imediatamente por [execução do gatilho Olá sob demanda](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="cc1d0-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="cc1d0-168">Quando o fluxo de saudação é executado, destinatários de saudação especificado na lista de email Olá receber uma mensagem de email que se parece com o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="cc1d0-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Email de exemplo](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="cc1d0-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc1d0-170">Next steps</span></span>

- <span data-ttu-id="cc1d0-171">Saiba mais sobre como criar [consultas do Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="cc1d0-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="cc1d0-172">Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cc1d0-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





