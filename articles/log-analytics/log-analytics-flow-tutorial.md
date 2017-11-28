---
title: "aaaAutomate processos de análise de logs do Azure com Microsoft Flow"
description: "Saiba como você pode usar o Microsoft Flow tooquickly automatizar processos repetíveis usando o conector do Azure Log Analytics hello."
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
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="5bc80-103">Automatizar processos de análise de Log com conector Olá para o Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="5bc80-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="5bc80-104">[Microsoft Flow](https://ms.flow.microsoft.com) permite que os fluxos de trabalho toocreate automatizada usando centenas de ações para uma variedade de serviços.</span><span class="sxs-lookup"><span data-stu-id="5bc80-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="5bc80-105">Saída de uma ação pode ser usada como entrada tooanother, permitindo que você toocreate integração entre serviços diferentes.</span><span class="sxs-lookup"><span data-stu-id="5bc80-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="5bc80-106">conector do Azure Log Analytics Olá para o Microsoft Flow permitir toobuild fluxos de trabalho que incluem dados recuperados pelas pesquisas de log na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="5bc80-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="5bc80-107">Por exemplo, você pode usar dados de análise de logs do Microsoft Flow toouse em uma notificação por email do Office 365, criar um bug no Visual Studio Team Services ou postar uma mensagem de margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="5bc80-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="5bc80-108">Você pode disparar um fluxo de trabalho com um agendamento simples ou a partir de alguma ação em um serviço conectado, por exemplo, quando um email ou tweet é recebido.</span><span class="sxs-lookup"><span data-stu-id="5bc80-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="5bc80-109">conector do Azure Log Analytics Olá para o Microsoft Flow requer seu espaço de trabalho toobe atualizado toohello nova análise de Log linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="5bc80-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="5bc80-110">Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="5bc80-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="5bc80-111">tutorial de saudação neste artigo mostra como toocreate um fluxo que envia automaticamente Olá resultados de uma pesquisa de log de análise de Log por email, apenas um exemplo de como você pode usar a análise de Log no Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="5bc80-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="5bc80-112">Etapa 1: Criar um fluxo</span><span class="sxs-lookup"><span data-stu-id="5bc80-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="5bc80-113">Entrar muito[Microsoft Flow](http://flow.microsoft.com)e selecione **flui meu**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="5bc80-114">Clique em **+ Criar em branco**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="5bc80-115">Etapa 2: Criar um gatilho para o fluxo</span><span class="sxs-lookup"><span data-stu-id="5bc80-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="5bc80-116">Clique em **Pesquisar centenas de conectores e gatilhos**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="5bc80-117">Tipo **agenda** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bc80-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="5bc80-118">Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="5bc80-119">Em Olá **frequência** marque **dia** e em Olá **intervalo** , digite **1**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="5bc80-120">![Caixa de diálogo de gatilho do Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="5bc80-121">Etapa 3: Adicionar uma ação do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5bc80-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="5bc80-122">Clique em **+ Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="5bc80-123">Pesquise por **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="5bc80-124">Clique em **Azure Log Analytics – Executar a consulta e visualizar os resultados**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="5bc80-125">![Janela Executar consulta do Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="5bc80-126">Etapa 4: Configurar a ação de análise de Log Olá</span><span class="sxs-lookup"><span data-stu-id="5bc80-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="5bc80-127">Especifique os detalhes de saudação de seu espaço de trabalho incluindo Olá assinatura ID, grupo de recursos e o nome do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5bc80-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="5bc80-128">Adicionar Olá toohello de consulta de análise de Log a seguir **consulta** janela.</span><span class="sxs-lookup"><span data-stu-id="5bc80-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="5bc80-129">Isso é apenas um exemplo de consulta, e você pode substituir por qualquer outra que retorne dados.</span><span class="sxs-lookup"><span data-stu-id="5bc80-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="5bc80-130">Selecione **tabela HTML** para Olá **tipo de gráfico**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="5bc80-131">![Ação do Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="5bc80-132">Etapa 5: Configurar o email de toosend fluxo Olá</span><span class="sxs-lookup"><span data-stu-id="5bc80-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="5bc80-133">Clique em **Nova etapa** e depois clique em **+ Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="5bc80-134">Pesquise por **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="5bc80-135">Clique em **Office 365 Outlook – Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="5bc80-136">![Janela de seleção do Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="5bc80-137">Especifique o endereço de email de saudação de um destinatário no hello **para** janela e o assunto do email de saudação em **assunto**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="5bc80-138">Clique em qualquer lugar Olá **corpo** caixa.</span><span class="sxs-lookup"><span data-stu-id="5bc80-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="5bc80-139">Uma janela de **Conteúdo dinâmico** é aberta com valores de ações anteriores.</span><span class="sxs-lookup"><span data-stu-id="5bc80-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="5bc80-140">Selecione **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-140">Select **Body**.</span></span>  <span data-ttu-id="5bc80-141">Isso é resultados de saudação da consulta Olá Olá ação de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="5bc80-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="5bc80-142">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="5bc80-143">Em Olá **é HTML** selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="5bc80-144">![Janela de configuração de email do Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="5bc80-145">Etapa 6: Salvar e testar o fluxo</span><span class="sxs-lookup"><span data-stu-id="5bc80-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="5bc80-146">Em Olá **nome do fluxo de** caixa, adicione um nome para o fluxo e, em seguida, clique em **criar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="5bc80-147">![Salvar o fluxo](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="5bc80-148">fluxo de saudação é criado e será executado após um dia que é Olá agendamento especificado.</span><span class="sxs-lookup"><span data-stu-id="5bc80-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="5bc80-149">tooimmediately teste Olá fluxo, clique em **executar agora** e **executar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="5bc80-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="5bc80-150">![Executar fluxo](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="5bc80-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="5bc80-151">Quando o fluxo de saudação for concluída, verifique mensagens de saudação do destinatário Olá que você especificou.</span><span class="sxs-lookup"><span data-stu-id="5bc80-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="5bc80-152">Você deve ter recebido um email com um corpo semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bc80-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Email de exemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="5bc80-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bc80-154">Next steps</span></span>

- <span data-ttu-id="5bc80-155">Saiba mais sobre o [Pesquisas de log no Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="5bc80-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="5bc80-156">Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5bc80-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



