---
title: "exemplo de ação de alerta de aaaWebhook na análise de Log do OMS | Microsoft Docs"
description: "Uma das ações de saudação, você pode executar em resposta tooa alerta de análise de Log é um * webhook *, que permite que você tooinvoke um processo externo por meio de uma única solicitação HTTP. Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack."
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
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="b9e8e-104">Criar uma ação de alerta do webhook na análise de logs do OMS toosend mensagem tooSlack</span><span class="sxs-lookup"><span data-stu-id="b9e8e-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="b9e8e-105">Uma das ações de saudação, você pode executar em resposta tooa [alerta de análise de Log](log-analytics-alerts.md) é um *webhook*, que permite a você tooinvoke um processo externo por meio de uma única solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="b9e8e-106">Você pode ler sobre os detalhes de alertas e webhooks em [Alertas no Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="b9e8e-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="b9e8e-107">Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack, que é um serviço de mensagens.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e8e-108">Você deve ter uma conta do Slack toocomplete Este exemplo.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="b9e8e-109">Inscreva-se para uma conta gratuita em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="b9e8e-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="b9e8e-110">Etapa 1: Habilitar webhooks no Slack</span><span class="sxs-lookup"><span data-stu-id="b9e8e-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="b9e8e-111">Entrar tooSlack em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="b9e8e-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="b9e8e-112">Selecione um canal em Olá **canais** seção no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="b9e8e-113">Este é o canal de saudação essa mensagem de saudação será enviada para.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="b9e8e-114">Você pode selecionar um dos canais de padrão de saudação como **geral** ou **aleatório**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="b9e8e-115">Em um cenário de produção, você provavelmente criaria um canal especial como **alertasdeserviçocríticos**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="b9e8e-117">Clique em **adicionar um aplicativo ou a integração personalizados** tooopen Olá diretório de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="b9e8e-118">Tipo *webhooks* na caixa de pesquisa de saudação e, em seguida, selecione **WebHooks entrada**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="b9e8e-120">Clique em **instalar** nome da equipe tooyour Avançar.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="b9e8e-121">Clique em **Adicionar Configuração**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="b9e8e-122">Canal de Olá Olá selecione que você vai toouse para este exemplo e, em seguida, clique em **Adicionar entrada WebHooks integração**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="b9e8e-123">Saudação de cópia **URL do Webhook**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="b9e8e-124">Você estará colando isso na configuração de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="b9e8e-126">Etapa 2: Criar a regra de alerta no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b9e8e-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="b9e8e-127">[Criar uma regra de alerta](log-analytics-alerts.md) com hello configurações a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="b9e8e-128">Consulta: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="b9e8e-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="b9e8e-129">Verificar esse alerta a cada: 5 minutos</span><span class="sxs-lookup"><span data-stu-id="b9e8e-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="b9e8e-130">saudação de número de resultados é: maior que 10</span><span class="sxs-lookup"><span data-stu-id="b9e8e-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="b9e8e-131">Durante o período de: 60 minutos</span><span class="sxs-lookup"><span data-stu-id="b9e8e-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="b9e8e-132">Selecione **Sim** para **Webhook** e **não** para Olá outras ações.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="b9e8e-133">Olá colar a URL de margem de atraso em Olá **URL do Webhook** campo.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="b9e8e-134">Selecione a opção de saudação muito**incluem uma carga JSON personalizada**.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="b9e8e-135">O Slack espera uma carga formatada em JSON com um parâmetro chamado *text*.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="b9e8e-136">Esse é o texto de saudação que ela será exibida na mensagem de saudação, que ele cria.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="b9e8e-137">Você pode usar um ou mais dos parâmetros de alerta hello usando Olá  *#*  símbolo, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![carga JSON de exemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="b9e8e-139">Clique em **salvar** toosave regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="b9e8e-140">Aguarde tempo suficiente para um alerta toobe criado e verifique se a margem de atraso para uma mensagem que será a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![webhook de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="b9e8e-142">Carga de webhook avançada para o Slack</span><span class="sxs-lookup"><span data-stu-id="b9e8e-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="b9e8e-143">É possível personalizar amplamente as mensagens de entrada com o Slack.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="b9e8e-144">Para obter mais informações, consulte [Webhooks entrada](https://api.slack.com/incoming-webhooks) no site de margem de atraso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="b9e8e-145">A seguir está uma toocreate de carga uma mensagem rich com formatação mais complexo:</span><span class="sxs-lookup"><span data-stu-id="b9e8e-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
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


<span data-ttu-id="b9e8e-146">Isso poderia gerar uma mensagem de atraso seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-146">This would generate a message in Slack similar toohello following.</span></span>

![mensagem de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="b9e8e-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="b9e8e-148">Summary</span></span>
<span data-ttu-id="b9e8e-149">Com esta regra de alerta em vigor, você teria tooSlack uma mensagem enviada sempre Olá critérios forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="b9e8e-150">Isso é apenas um exemplo de uma ação que você pode criar no alerta de tooan de resposta.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="b9e8e-151">Você pode criar uma ação de webhook que chama outro serviço externo, um toostart de ação de runbook um runbook na automação do Azure ou um toosend de ação de email tooyourself um email ou outros destinatários.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="b9e8e-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9e8e-152">Next Steps</span></span>
* <span data-ttu-id="b9e8e-153">Saiba mais sobre outras [ações de alerta no Log Analytics](log-analytics-alerts-actions.md), incluindo outras ações.</span><span class="sxs-lookup"><span data-stu-id="b9e8e-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


