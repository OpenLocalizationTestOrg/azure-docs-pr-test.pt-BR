---
title: "aaaAutomate Azure Application Insights processa usando lógica de aplicativos."
description: "Saiba como você pode rapidamente automatizar processos repetíveis adicionando Olá Application Insights conector tooyour lógica aplicativo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="6f21a-103">Automatize os processos do Application Insights usando os Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="6f21a-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="6f21a-104">Você encontra-se repetidamente Olá mesmo consultas executadas em seu toocheck de dados de telemetria se o serviço está funcionando corretamente?</span><span class="sxs-lookup"><span data-stu-id="6f21a-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="6f21a-105">É buscam tooautomate essas consultas para descobrir tendências e anomalias e, em seguida, criar seus próprios fluxos de trabalho contorná-las? Hello Azure aplicativo Insights connector (visualização) para aplicativos lógicos é a ferramenta certa Olá para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="6f21a-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="6f21a-106">Com essa integração, você pode automatizar diversos processos sem a necessidade de escrever nenhuma linha de código.</span><span class="sxs-lookup"><span data-stu-id="6f21a-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="6f21a-107">Você pode criar um aplicativo lógico com hello Application Insights conector tooquickly automatizar qualquer processo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6f21a-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="6f21a-108">Adicione também outras ações.</span><span class="sxs-lookup"><span data-stu-id="6f21a-108">You can add additional actions as well.</span></span> <span data-ttu-id="6f21a-109">recurso de aplicativos lógicos de saudação do serviço de aplicativo do Azure torna centenas de ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6f21a-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="6f21a-110">Por exemplo, usando um aplicativo lógico, você pode enviar automaticamente uma notificação por email ou criar um bug no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6f21a-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="6f21a-111">Você também pode usar uma saudação muitas disponível [modelos](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar o processo de saudação de criação de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6f21a-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="6f21a-112">Criar um aplicativo lógico para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="6f21a-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="6f21a-113">Neste tutorial, você aprenderá como toocreate um aplicativo de lógica que usa Olá análise autocluster algoritmo toogroup atributos nos dados Olá para um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="6f21a-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="6f21a-114">fluxo de saudação envia automaticamente resultados Olá por email, apenas um exemplo de como você pode usar análise de informações do aplicativo e os aplicativos lógicos juntos.</span><span class="sxs-lookup"><span data-stu-id="6f21a-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="6f21a-115">Etapa 1: criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="6f21a-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="6f21a-116">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f21a-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6f21a-117">Em Olá **novo** painel, selecione **Web + móvel**e, em seguida, selecione **aplicativo lógico**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Janela Novo aplicativo lógico](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="6f21a-119">Etapa 2: criar um gatilho para seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="6f21a-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="6f21a-120">Em Olá **lógica de aplicativo Designer** janela, em **começar com um gatilho comuns**, selecione **recorrência**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Janela Designer de Aplicativo Lógico](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="6f21a-122">Em Olá **frequência** selecione **dia** e, em seguida, em Olá **intervalo** , digite **1**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Janela "Recorrência" do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="6f21a-124">Etapa 3: adicionar uma ação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6f21a-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="6f21a-125">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="6f21a-126">Em Olá **escolher uma ação** caixa de pesquisa, digite **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="6f21a-127">Em **Ações**, clique em **Versão Prévia do Azure Application Insights – Visualizar consulta do Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Janela "Escolha uma ação" do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="6f21a-129">Etapa 4: Conectar-se o recurso do Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="6f21a-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="6f21a-130">toocomplete nesta etapa, você precisa de uma ID de aplicativo e uma chave de API para o recurso.</span><span class="sxs-lookup"><span data-stu-id="6f21a-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="6f21a-131">Você pode recuperá-las de saudação portal do Azure, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="6f21a-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID do aplicativo no portal do Azure de saudação](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="6f21a-133">Forneça um nome para a conexão, a ID do aplicativo hello e a chave de API do hello.</span><span class="sxs-lookup"><span data-stu-id="6f21a-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Janela Conexão de fluxo do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="6f21a-135">Etapa 5: Especificar hello consulta de análise e o tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="6f21a-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="6f21a-136">Em Olá exemplo a seguir, consulta Olá seleciona solicitações Olá falhado no último dia do hello e correlaciona-los com exceções que ocorreram como parte da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f21a-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="6f21a-137">Análise de correlaciona solicitações Olá falhou, com base no identificador de operation_Id hello.</span><span class="sxs-lookup"><span data-stu-id="6f21a-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="6f21a-138">consulta de saudação segmentos, em seguida, resultados hello usando algoritmo de autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="6f21a-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="6f21a-139">Quando você cria suas próprias consultas, verifique se estão funcionando corretamente na análise antes de adicioná-lo tooyour fluxo.</span><span class="sxs-lookup"><span data-stu-id="6f21a-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="6f21a-140">Em Olá **consulta** caixa, adicione Olá consulta de análise a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f21a-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="6f21a-141">Em Olá **tipo de gráfico** selecione **tabela Html**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Janela de configuração de consulta do Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="6f21a-143">Etapa 6: Configurar o email de toosend de aplicativo hello lógica</span><span class="sxs-lookup"><span data-stu-id="6f21a-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="6f21a-144">Clique em **Nova etapa** e, depois, selecione **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="6f21a-145">Na caixa de pesquisa hello, digite **Outlook do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="6f21a-146">Clique em **Office 365 Outlook – Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Seleção do Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="6f21a-148">Em Olá **enviar um email** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f21a-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="6f21a-149">a.</span><span class="sxs-lookup"><span data-stu-id="6f21a-149">a.</span></span> <span data-ttu-id="6f21a-150">Digite o endereço de email de saudação do destinatário hello.</span><span class="sxs-lookup"><span data-stu-id="6f21a-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="6f21a-151">b.</span><span class="sxs-lookup"><span data-stu-id="6f21a-151">b.</span></span> <span data-ttu-id="6f21a-152">Digite o assunto do email de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f21a-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="6f21a-153">c.</span><span class="sxs-lookup"><span data-stu-id="6f21a-153">c.</span></span> <span data-ttu-id="6f21a-154">Clique em qualquer lugar Olá **corpo** caixa e, em seguida, em Olá conteúdo menu dinâmico que é aberto no hello direito, selecione **corpo**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="6f21a-155">d.</span><span class="sxs-lookup"><span data-stu-id="6f21a-155">d.</span></span> <span data-ttu-id="6f21a-156">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-156">Click **Show advanced options**.</span></span>

      ![Configuração do Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="6f21a-158">No menu de conteúdo dinâmico Olá, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f21a-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="6f21a-159">a.</span><span class="sxs-lookup"><span data-stu-id="6f21a-159">a.</span></span> <span data-ttu-id="6f21a-160">Selecione o **Nome do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="6f21a-161">b.</span><span class="sxs-lookup"><span data-stu-id="6f21a-161">b.</span></span> <span data-ttu-id="6f21a-162">Selecione o **Conteúdo do Anexo**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="6f21a-163">c.</span><span class="sxs-lookup"><span data-stu-id="6f21a-163">c.</span></span> <span data-ttu-id="6f21a-164">Em Olá **é HTML** selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Tela de configuração de email do Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="6f21a-166">Etapa 7: salvar e testar o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="6f21a-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="6f21a-167">Clique em **salvar** toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="6f21a-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="6f21a-168">Você pode aguardar Olá gatilho toorun Olá lógica aplicativo ou você pode executar o aplicativo de lógica de saudação imediatamente selecionando **executar**.</span><span class="sxs-lookup"><span data-stu-id="6f21a-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Tela de criação do aplicativo lógico](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="6f21a-170">Quando sua lógica de aplicativo é executado, destinatários Olá especificado na lista de email Olá receberá um email que se parece com o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6f21a-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Mensagem de email do aplicativo lógico](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="6f21a-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f21a-172">Next steps</span></span>

- <span data-ttu-id="6f21a-173">Saiba mais sobre a criação de [Consultas do Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="6f21a-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="6f21a-174">Saiba mais sobre o [Aplicativos Lógicos](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="6f21a-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





