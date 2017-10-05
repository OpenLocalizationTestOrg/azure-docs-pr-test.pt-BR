---
title: Automatizar os processos do Azure Application Insights com o Microsoft Flow
description: "Saiba como você pode usar o Microsoft Flow para automatizar rapidamente os processos repetidos usando o conector do Application Insights."
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="c1981-103">Automatizar os processos do Azure Application Insights com o conector para o Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="c1981-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="c1981-104">Você está executando repetidamente as mesmas consultas nos dados telemétricos para verificar se o serviço está funcionando corretamente?</span><span class="sxs-lookup"><span data-stu-id="c1981-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="c1981-105">Deseja automatizar essas consultas para descobrir tendências e anomalias e então criar seus próprios fluxos de trabalho para elas?</span><span class="sxs-lookup"><span data-stu-id="c1981-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="c1981-106">O conector do Azure Application Insights (versão prévia) para o Microsoft Flow é a ferramenta certa para esses fins.</span><span class="sxs-lookup"><span data-stu-id="c1981-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="c1981-107">Com essa integração, você agora pode automatizar diversos processos sem a necessidade de escrever nenhuma linha de código.</span><span class="sxs-lookup"><span data-stu-id="c1981-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="c1981-108">Depois de você criar um fluxo usando uma ação do Application Insights, o fluxo executa automaticamente a consulta do Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="c1981-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="c1981-109">Adicione também outras ações.</span><span class="sxs-lookup"><span data-stu-id="c1981-109">You can add additional actions as well.</span></span> <span data-ttu-id="c1981-110">O Microsoft Flow disponibiliza centenas de ações.</span><span class="sxs-lookup"><span data-stu-id="c1981-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="c1981-111">Por exemplo, você pode usar o Microsoft Flow para enviar uma notificação por email automaticamente ou criar um bug no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c1981-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="c1981-112">Use também um dos vários [modelos](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) disponíveis para o conector para o Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="c1981-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="c1981-113">Esses modelos aceleram o processo de criação de um fluxo.</span><span class="sxs-lookup"><span data-stu-id="c1981-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="c1981-114">Criar um fluxo para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="c1981-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="c1981-115">Neste tutorial, você aprenderá a criar um fluxo que usa o algoritmo de cluster automático do Analytics para agrupar atributos nos dados de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c1981-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="c1981-116">O fluxo envia automaticamente os resultados por email, apenas um exemplo de como você pode usar o Microsoft Flow e o Application Insights Analytics juntos.</span><span class="sxs-lookup"><span data-stu-id="c1981-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="c1981-117">Etapa 1: Criar um fluxo</span><span class="sxs-lookup"><span data-stu-id="c1981-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="c1981-118">Entre no [Microsoft Flow](http://flow.microsoft.com) e, em seguida, selecione **Meus Fluxos**.</span><span class="sxs-lookup"><span data-stu-id="c1981-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="c1981-119">Clique em **Criar um fluxo em branco**.</span><span class="sxs-lookup"><span data-stu-id="c1981-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="c1981-120">Etapa 2: Criar um gatilho para o fluxo</span><span class="sxs-lookup"><span data-stu-id="c1981-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="c1981-121">Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.</span><span class="sxs-lookup"><span data-stu-id="c1981-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="c1981-122">Na caixa **frequência**, selecione **Dia** e, na caixa **Intervalo**, digite **1**.</span><span class="sxs-lookup"><span data-stu-id="c1981-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Caixa de diálogo de gatilho do Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="c1981-124">Etapa 3: adicionar uma ação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c1981-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="c1981-125">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="c1981-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c1981-126">Pesquise por **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="c1981-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="c1981-127">Clique em **Versão Prévia do Azure Application Insights – Visualizar a versão prévia da consulta do Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c1981-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Janela Executar consulta do Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="c1981-129">Etapa 4: conectar-se a um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c1981-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="c1981-130">Para concluir esta etapa, você precisa de uma ID do Aplicativo e uma Chave de API do recurso.</span><span class="sxs-lookup"><span data-stu-id="c1981-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="c1981-131">Você pode recuperá-las no Portal do Azure, conforme mostrado no seguinte diagrama:</span><span class="sxs-lookup"><span data-stu-id="c1981-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![ID do Aplicativo no portal do Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="c1981-133">Forneça um nome para a conexão, junto com a ID do aplicativo e a Chave de API.</span><span class="sxs-lookup"><span data-stu-id="c1981-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Janela de conexão do Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="c1981-135">Etapa 5: especificar o tipo de consulta do Analytics e o tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="c1981-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="c1981-136">Esta consulta de exemplo seleciona as solicitações com falha no último dia e correlaciona-as com as exceções que ocorreram como parte da operação.</span><span class="sxs-lookup"><span data-stu-id="c1981-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="c1981-137">O Analytics correlaciona-os com base no identificador operation_Id.</span><span class="sxs-lookup"><span data-stu-id="c1981-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="c1981-138">Em seguida, a consulta segmenta os resultados usando o algoritmo de cluster automático.</span><span class="sxs-lookup"><span data-stu-id="c1981-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="c1981-139">Quando criar suas próprias consultas, verifique se elas estão funcionando corretamente no Analytics antes de adicioná-las ao fluxo.</span><span class="sxs-lookup"><span data-stu-id="c1981-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="c1981-140">Adicione a consulta do Analytics a seguir e selecione o tipo de gráfico de tabela HTML.</span><span class="sxs-lookup"><span data-stu-id="c1981-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="c1981-142">Etapa 6: Configurar o fluxo para enviar email</span><span class="sxs-lookup"><span data-stu-id="c1981-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="c1981-143">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="c1981-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c1981-144">Pesquise por **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="c1981-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="c1981-145">Clique em **Office 365 Outlook – Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="c1981-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Janela de seleção do Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="c1981-147">Na janela **Enviar um email**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c1981-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="c1981-148">a.</span><span class="sxs-lookup"><span data-stu-id="c1981-148">a.</span></span> <span data-ttu-id="c1981-149">Digite o endereço de email do destinatário.</span><span class="sxs-lookup"><span data-stu-id="c1981-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="c1981-150">b.</span><span class="sxs-lookup"><span data-stu-id="c1981-150">b.</span></span> <span data-ttu-id="c1981-151">Digite um assunto para o email.</span><span class="sxs-lookup"><span data-stu-id="c1981-151">Type a subject for the email.</span></span>

   <span data-ttu-id="c1981-152">c.</span><span class="sxs-lookup"><span data-stu-id="c1981-152">c.</span></span> <span data-ttu-id="c1981-153">Clique em qualquer lugar na caixa **Corpo** e, no menu de conteúdo dinâmico que se abre à direita, selecione **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="c1981-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="c1981-154">d.</span><span class="sxs-lookup"><span data-stu-id="c1981-154">d.</span></span> <span data-ttu-id="c1981-155">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="c1981-155">Click **Show advanced options**.</span></span>

    ![Configuração do Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="c1981-157">No menu de conteúdo dinâmico, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c1981-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="c1981-158">a.</span><span class="sxs-lookup"><span data-stu-id="c1981-158">a.</span></span> <span data-ttu-id="c1981-159">Selecione o **Nome do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="c1981-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="c1981-160">b.</span><span class="sxs-lookup"><span data-stu-id="c1981-160">b.</span></span> <span data-ttu-id="c1981-161">Selecione o **Conteúdo do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="c1981-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="c1981-162">c.</span><span class="sxs-lookup"><span data-stu-id="c1981-162">c.</span></span> <span data-ttu-id="c1981-163">Na caixa **É HTML**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c1981-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Janela de configuração de email do Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="c1981-165">Etapa 7: Salvar e testar o fluxo</span><span class="sxs-lookup"><span data-stu-id="c1981-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="c1981-166">Na caixa **Nome do fluxo**, adicione um nome para o fluxo e, em seguida, clique em **Criar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="c1981-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Janela de criação de fluxo](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="c1981-168">Você Pode aguardar até que o gatilho execute essa ação ou executar o fluxo imediatamente [executando o gatilho sob demanda](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="c1981-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="c1981-169">Quando o fluxo é executado, os destinatários que você especificou na lista de emails recebem uma mensagem de email com a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="c1981-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Email de exemplo](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="c1981-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1981-171">Next steps</span></span>

- <span data-ttu-id="c1981-172">Saiba mais sobre como criar [consultas do Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="c1981-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="c1981-173">Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c1981-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





