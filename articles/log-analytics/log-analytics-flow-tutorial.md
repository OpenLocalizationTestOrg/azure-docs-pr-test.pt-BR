---
title: Automatizar os processos do Azure Log Analytics com o Microsoft Flow
description: "Saiba como você pode usar o Microsoft Flow para automatizar rapidamente os processos repetidos usando o conector do Azure Log Analytics."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="2fe5c-103">Automatizar os processos do Log Analytics com o conector para o Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="2fe5c-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="2fe5c-104">O [Microsoft Flow](https://ms.flow.microsoft.com) permite que você crie fluxos de trabalho automatizados usando centenas de ações para vários serviços.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="2fe5c-105">A saída de uma ação pode ser usada como entrada para outra, permitindo que você crie a integração entre serviços diferentes.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="2fe5c-106">O conector do Azure Log Analytics para Microsoft Flow permite que você crie fluxos de trabalho que incluem dados recuperados pelas pesquisas de log no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="2fe5c-107">Por exemplo, você pode usar o Microsoft Flow para usar dados do Log Analytics em uma notificação por email do Office 365, criar um bug no Visual Studio Team Services ou postar uma mensagem no Slack.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="2fe5c-108">Você pode disparar um fluxo de trabalho com um agendamento simples ou a partir de alguma ação em um serviço conectado, por exemplo, quando um email ou tweet é recebido.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="2fe5c-109">O conector do Azure Log Analytics para Microsoft Flow exige a atualização de seu espaço de trabalho para a nova linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="2fe5c-110">Você pode saber mais sobre a nova linguagem e obter o procedimento para fazer upgrade do espaço de trabalho em [Fazer upgrade do espaço de trabalho do Azure Log Analytics para uma nova pesquisa de logs](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="2fe5c-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="2fe5c-111">O tutorial neste artigo mostra como criar um fluxo que envia automaticamente os resultados de uma pesquisa de log do Log Analytics por email, apenas um exemplo de como você pode usar a o Log Analytics no Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="2fe5c-112">Etapa 1: Criar um fluxo</span><span class="sxs-lookup"><span data-stu-id="2fe5c-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="2fe5c-113">Entre no [Microsoft Flow](http://flow.microsoft.com) e selecione **Meus Fluxos**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="2fe5c-114">Clique em **+ Criar em branco**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="2fe5c-115">Etapa 2: Criar um gatilho para o fluxo</span><span class="sxs-lookup"><span data-stu-id="2fe5c-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="2fe5c-116">Clique em **Pesquisar centenas de conectores e gatilhos**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="2fe5c-117">Digite **Agenda** na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="2fe5c-118">Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="2fe5c-119">Na caixa **frequência**, selecione **Dia** e, na caixa **Intervalo**, digite **1**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="2fe5c-120">![Caixa de diálogo de gatilho do Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="2fe5c-121">Etapa 3: Adicionar uma ação do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fe5c-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="2fe5c-122">Clique em **+ Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="2fe5c-123">Pesquise por **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="2fe5c-124">Clique em **Azure Log Analytics – Executar a consulta e visualizar os resultados**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="2fe5c-125">![Janela Executar consulta do Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="2fe5c-126">Etapa 4: Configurar a ação do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2fe5c-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="2fe5c-127">Especifique os detalhes de seu espaço de trabalho incluindo a ID da Assinatura, o Grupo de Recursos e o Nome do Espaço de Trabalho.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="2fe5c-128">Adicione a seguinte consulta do Log Analytics à janela **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="2fe5c-129">Isso é apenas um exemplo de consulta, e você pode substituir por qualquer outra que retorne dados.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="2fe5c-130">Selecione **Tabela HTML** para o **Tipo de Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="2fe5c-131">![Ação do Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="2fe5c-132">Etapa 5: Configurar o fluxo para enviar email</span><span class="sxs-lookup"><span data-stu-id="2fe5c-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="2fe5c-133">Clique em **Nova etapa** e depois clique em **+ Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="2fe5c-134">Pesquise por **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="2fe5c-135">Clique em **Office 365 Outlook – Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="2fe5c-136">![Janela de seleção do Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="2fe5c-137">Especifique o endereço de email de um destinatário na janela **Para** e um assunto para o email em **Assunto**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="2fe5c-138">Clique em qualquer lugar da caixa **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="2fe5c-139">Uma janela de **Conteúdo dinâmico** é aberta com valores de ações anteriores.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="2fe5c-140">Selecione **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-140">Select **Body**.</span></span>  <span data-ttu-id="2fe5c-141">Esses são os resultados da consulta na ação do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="2fe5c-142">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="2fe5c-143">Na caixa **É HTML**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="2fe5c-144">![Janela de configuração de email do Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="2fe5c-145">Etapa 6: Salvar e testar o fluxo</span><span class="sxs-lookup"><span data-stu-id="2fe5c-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="2fe5c-146">Na caixa **Nome do fluxo**, adicione um nome para o fluxo e, em seguida, clique em **Criar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="2fe5c-147">![Salvar o fluxo](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="2fe5c-148">Agora, o fluxo é criado e será executado após um dia, que é a agenda especificada.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="2fe5c-149">Para testar o fluxo imediatamente, clique em **Executar Agora** e **Executar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="2fe5c-150">![Executar fluxo](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="2fe5c-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="2fe5c-151">Após a conclusão do fluxo, verifique o email do destinatário que você especificou.</span><span class="sxs-lookup"><span data-stu-id="2fe5c-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="2fe5c-152">Você deve ter recebido um email com um corpo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="2fe5c-152">You should have received a mail with a body similar to the following:</span></span><br><br>![Email de exemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="2fe5c-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fe5c-154">Next steps</span></span>

- <span data-ttu-id="2fe5c-155">Saiba mais sobre o [Pesquisas de log no Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="2fe5c-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="2fe5c-156">Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2fe5c-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



