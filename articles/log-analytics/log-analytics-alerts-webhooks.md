---
title: "Exemplo de ação de alerta de Webhook no Log Analytics do OMS | Microsoft Docs"
description: "Uma das ações que você pode executar em resposta a um alerta do Log Analytics é um *webhook*, que permite invocar um processo externo por meio de uma única solicitação HTTP. Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="776ca-104">Criar uma ação de webhook de alerta no OMS Log Analytics para enviar mensagens ao Slack</span><span class="sxs-lookup"><span data-stu-id="776ca-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="776ca-105">Uma das ações que você pode executar em resposta a um [alerta do Log Analytics](log-analytics-alerts.md) é um *webhook*, que permite invocar um processo externo por meio de uma única solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="776ca-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="776ca-106">Você pode ler sobre os detalhes de alertas e webhooks em [Alertas no Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="776ca-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="776ca-107">Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack, que é um serviço de mensagens.</span><span class="sxs-lookup"><span data-stu-id="776ca-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="776ca-108">Você deve ter uma conta do Slack para concluir este exemplo.</span><span class="sxs-lookup"><span data-stu-id="776ca-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="776ca-109">Inscreva-se para uma conta gratuita em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="776ca-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="776ca-110">Etapa 1: Habilitar webhooks no Slack</span><span class="sxs-lookup"><span data-stu-id="776ca-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="776ca-111">Entre no Slack em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="776ca-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="776ca-112">Selecione um canal na seção **Canais** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="776ca-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="776ca-113">Esse é o canal para o qual a mensagem será enviada.</span><span class="sxs-lookup"><span data-stu-id="776ca-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="776ca-114">Você pode selecionar um dos canais padrão como **geral** ou **aleatório**.</span><span class="sxs-lookup"><span data-stu-id="776ca-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="776ca-115">Em um cenário de produção, você provavelmente criaria um canal especial como **alertasdeserviçocríticos**.</span><span class="sxs-lookup"><span data-stu-id="776ca-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="776ca-117">Clique em **Adicionar um aplicativo ou uma integração personalizada** para abrir o Diretório de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="776ca-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="776ca-118">Digite *webhooks* na caixa de pesquisa e selecione **WebHooks de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="776ca-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="776ca-120">Clique em **Instalar** ao lado do nome da sua equipe.</span><span class="sxs-lookup"><span data-stu-id="776ca-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="776ca-121">Clique em **Adicionar Configuração**.</span><span class="sxs-lookup"><span data-stu-id="776ca-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="776ca-122">Selecione o canal que você vai usar para este exemplo e clique em **Adicionar integração de WebHooks de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="776ca-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="776ca-123">Copie a **URL do Webhook**.</span><span class="sxs-lookup"><span data-stu-id="776ca-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="776ca-124">Você colará isso na configuração do Alerta.</span><span class="sxs-lookup"><span data-stu-id="776ca-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="776ca-126">Etapa 2: Criar a regra de alerta no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="776ca-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="776ca-127">[Crie uma regra de alerta](log-analytics-alerts.md) com as seguintes configurações.</span><span class="sxs-lookup"><span data-stu-id="776ca-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="776ca-128">Consulta: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="776ca-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="776ca-129">Verificar esse alerta a cada: 5 minutos</span><span class="sxs-lookup"><span data-stu-id="776ca-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="776ca-130">O número de resultados é: maior que 10</span><span class="sxs-lookup"><span data-stu-id="776ca-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="776ca-131">Durante o período de: 60 minutos</span><span class="sxs-lookup"><span data-stu-id="776ca-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="776ca-132">Selecione **Sim** para **Webhook** e **Não** para as outras ações.</span><span class="sxs-lookup"><span data-stu-id="776ca-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="776ca-133">Cole a URL do Slack no campo **URL do Webhook** .</span><span class="sxs-lookup"><span data-stu-id="776ca-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="776ca-134">Selecione a opção para **incluir uma carga JSON personalizada**.</span><span class="sxs-lookup"><span data-stu-id="776ca-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="776ca-135">O Slack espera uma carga formatada em JSON com um parâmetro chamado *text*.</span><span class="sxs-lookup"><span data-stu-id="776ca-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="776ca-136">Este é o texto que será exibido na mensagem que ele cria.</span><span class="sxs-lookup"><span data-stu-id="776ca-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="776ca-137">Você pode usar um ou mais dos parâmetros de alerta usando o símbolo *#* , como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="776ca-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![carga JSON de exemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="776ca-139">Clique em **Salvar** para salvar a regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="776ca-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="776ca-140">Aguarde o tempo suficiente para que um alerta seja criado e verifique se há uma mensagem no Slack semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="776ca-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![webhook de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="776ca-142">Carga de webhook avançada para o Slack</span><span class="sxs-lookup"><span data-stu-id="776ca-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="776ca-143">É possível personalizar amplamente as mensagens de entrada com o Slack.</span><span class="sxs-lookup"><span data-stu-id="776ca-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="776ca-144">Para obter mais informações, consulte [Webhooks de Entrada](https://api.slack.com/incoming-webhooks) no site do Slack.</span><span class="sxs-lookup"><span data-stu-id="776ca-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="776ca-145">A seguir está uma carga mais complexa para criar uma mensagem avançada com formatação:</span><span class="sxs-lookup"><span data-stu-id="776ca-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="776ca-146">O script gerará uma mensagem no Slack semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="776ca-146">This would generate a message in Slack similar to the following.</span></span>

![mensagem de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="776ca-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="776ca-148">Summary</span></span>
<span data-ttu-id="776ca-149">Com essa regra de alerta em vigor, uma mensagem será enviada para o Slack sempre que os critérios forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="776ca-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="776ca-150">Esse é apenas um exemplo de uma ação que você pode criar em resposta a um alerta.</span><span class="sxs-lookup"><span data-stu-id="776ca-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="776ca-151">Você pode criar uma ação de webhook que chama outro serviço externo, uma ação de runbook para iniciar um runbook na Automação do Azure ou uma ação de email para enviar um email para si mesmo ou para outros destinatários.</span><span class="sxs-lookup"><span data-stu-id="776ca-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="776ca-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="776ca-152">Next Steps</span></span>
* <span data-ttu-id="776ca-153">Saiba mais sobre outras [ações de alerta no Log Analytics](log-analytics-alerts-actions.md), incluindo outras ações.</span><span class="sxs-lookup"><span data-stu-id="776ca-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


