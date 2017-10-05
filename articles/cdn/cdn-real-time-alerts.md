---
title: Alertas em tempo real do Azure CDN | Microsoft Docs
description: "Alertas em tempo real na CDN do Microsoft Azure. Alertas em tempo real fornecem notificações sobre o desempenho dos pontos de extremidade em seu perfil da CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="26482-104">Alertas em tempo real na CDN do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="26482-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="26482-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="26482-105">Overview</span></span>
<span data-ttu-id="26482-106">Este documento explica os alertas em tempo real na CDN do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="26482-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="26482-107">Essa funcionalidade fornece notificações em tempo real sobre o desempenho dos pontos de extremidade em seu perfil da CDN.</span><span class="sxs-lookup"><span data-stu-id="26482-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="26482-108">Você pode configurar alertas por email ou HTTP com base em:</span><span class="sxs-lookup"><span data-stu-id="26482-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="26482-109">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="26482-109">Bandwidth</span></span>
* <span data-ttu-id="26482-110">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="26482-110">Status Codes</span></span>
* <span data-ttu-id="26482-111">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="26482-111">Cache Statuses</span></span>
* <span data-ttu-id="26482-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="26482-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="26482-113">Criar um alerta em tempo real</span><span class="sxs-lookup"><span data-stu-id="26482-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="26482-114">No [Portal do Azure](https://portal.azure.com), navegue para seu perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="26482-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Folha Perfil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="26482-116">Na folha do perfil CDN, clique no botão **Gerenciar** .</span><span class="sxs-lookup"><span data-stu-id="26482-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="26482-118">O portal de gerenciamento da CDN é aberto.</span><span class="sxs-lookup"><span data-stu-id="26482-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="26482-119">Focalize a guia **Análise** e, em seguida, o submenu **Estatísticas em Tempo Real**.</span><span class="sxs-lookup"><span data-stu-id="26482-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="26482-120">Clique em **Alertas em Tempo Real**.</span><span class="sxs-lookup"><span data-stu-id="26482-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="26482-122">A lista de configurações de alerta existentes (se houver) é exibida.</span><span class="sxs-lookup"><span data-stu-id="26482-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="26482-123">Clique no botão **Adicionar Alerta** .</span><span class="sxs-lookup"><span data-stu-id="26482-123">Click the **Add Alert** button.</span></span>
   
    ![Botão Adicionar Alerta](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="26482-125">Um formulário para criar um novo alerta é exibido.</span><span class="sxs-lookup"><span data-stu-id="26482-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulário Novo Alerta](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="26482-127">Se você quiser que esse alerta esteja ativo quando clicar em **Salvar**, marque a caixa de seleção **Alerta Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="26482-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="26482-128">Insira um nome descritivo para o alerta no campo **Nome** .</span><span class="sxs-lookup"><span data-stu-id="26482-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="26482-129">Na lista suspensa **Tipo de Mídia**, selecione **Objeto Grande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="26482-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo de Mídia com Objeto Grande HTTP selecionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="26482-131">Você deve selecionar o **Objeto Grande HTTP** como o **Tipo de Mídia**.</span><span class="sxs-lookup"><span data-stu-id="26482-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="26482-132">As outras opções não são usadas pela **CDN do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="26482-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="26482-133">Se **Objeto Grande HTTP** não for selecionado, isso fará com que o alerta nunca seja disparado.</span><span class="sxs-lookup"><span data-stu-id="26482-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="26482-134">Crie uma **Expressão** para monitorar, selecionando uma **Métrica**, um **Operador** e um **Valor de gatilho**.</span><span class="sxs-lookup"><span data-stu-id="26482-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="26482-135">Para **Métrica**, selecione o tipo de condição que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="26482-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="26482-136">**Mbps de largura de banda** é a quantidade de uso de largura de banda em megabits por segundo.</span><span class="sxs-lookup"><span data-stu-id="26482-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="26482-137">**Total de Conexões** é o número de conexões HTTP simultâneas para os servidores de borda.</span><span class="sxs-lookup"><span data-stu-id="26482-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="26482-138">Para obter definições dos vários códigos de status e dos status de cache, confira [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Códigos de Status de Cache da CDN do Azure) e [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Códigos de Status de HTTP da CDN do Azure)</span><span class="sxs-lookup"><span data-stu-id="26482-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="26482-139">**Operador** é o operador matemático que estabelece a relação entre a métrica e o valor do gatilho.</span><span class="sxs-lookup"><span data-stu-id="26482-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="26482-140">**Valor de Disparador** é o valor de limite que deve ser atingido antes que uma notificação seja enviada.</span><span class="sxs-lookup"><span data-stu-id="26482-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="26482-141">No exemplo abaixo, a expressão que criei indica que desejo ser notificado quando o número de códigos de status 404 for maior que 25.</span><span class="sxs-lookup"><span data-stu-id="26482-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Expressão de exemplo de alerta em tempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="26482-143">Para **Intervalo**, digite a frequência com que você quer que a expressão seja avaliada.</span><span class="sxs-lookup"><span data-stu-id="26482-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="26482-144">Na lista suspensa **Notificar sobre** , selecione quando deseja ser notificado quando a expressão for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="26482-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="26482-145">**Início da Condição** indica que uma notificação será enviada quando a condição especificada for detectada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="26482-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="26482-146">**Condição Final** indica que uma notificação será enviada quando a condição especificada não for mais detectada.</span><span class="sxs-lookup"><span data-stu-id="26482-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="26482-147">Essa notificação só pode ser disparada após nosso sistema de monitoramento de rede detectar que ocorreu a condição especificada.</span><span class="sxs-lookup"><span data-stu-id="26482-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="26482-148">**Contínuo** indica que uma notificação será enviada sempre que o sistema de monitoramento de rede detectar a condição especificada.</span><span class="sxs-lookup"><span data-stu-id="26482-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="26482-149">Lembre-se de que o sistema de monitoramento de rede verifica a condição especificada somente uma vez por intervalo .</span><span class="sxs-lookup"><span data-stu-id="26482-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="26482-150">**Início e Fim de Condição** indica que uma notificação será enviada na primeira vez em que a condição especificada for detectada e novamente quando a condição não for mais detectada.</span><span class="sxs-lookup"><span data-stu-id="26482-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="26482-151">Se você desejar receber notificações por email, marque a caixa de seleção **Notificar por Email** .</span><span class="sxs-lookup"><span data-stu-id="26482-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Formulário Notificar por Email](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="26482-153">No campo **Para** , insira o endereço de email para o qual deseja que as notificações sejam enviadas.</span><span class="sxs-lookup"><span data-stu-id="26482-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="26482-154">Para **Assunto** e **Corpo**, você pode manter o padrão ou personalizar a mensagem usando a lista **Palavras-chave disponíveis** para inserir dados de alerta dinamicamente quando a mensagem for enviada.</span><span class="sxs-lookup"><span data-stu-id="26482-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="26482-155">Você pode testar a notificação por email clicando no botão **Notificação de Teste** , mas somente depois que a configuração de alertas for salva.</span><span class="sxs-lookup"><span data-stu-id="26482-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="26482-156">Se você quiser que as notificações sejam postadas em um servidor Web, marque a caixa de seleção **Notificar por HTTP Post** .</span><span class="sxs-lookup"><span data-stu-id="26482-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulário Notificar por HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="26482-158">No campo **Url** , digite a URL em que você deseja que a mensagem HTTP seja postada.</span><span class="sxs-lookup"><span data-stu-id="26482-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="26482-159">Na caixa de texto **Cabeçalhos** , insira os cabeçalhos HTTP a serem enviados na solicitação.</span><span class="sxs-lookup"><span data-stu-id="26482-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="26482-160">Para **Corpo**, você pode personalizar a mensagem usando a lista de **Palavras-chave disponíveis** para inserir dados de alerta dinamicamente quando a mensagem for enviada.</span><span class="sxs-lookup"><span data-stu-id="26482-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="26482-161">**Cabeçalhos** e **Corpo** usam como padrão um conteúdo de XML semelhante ao exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="26482-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="26482-162">Você pode testar a notificação de HTTP Post clicando no botão **Notificação de Teste** , mas somente depois que a configuração de alertas for salva.</span><span class="sxs-lookup"><span data-stu-id="26482-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="26482-163">Clique no botão **Salvar** para salvar sua configuração de alerta.</span><span class="sxs-lookup"><span data-stu-id="26482-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="26482-164">Se você tiver selecionado **Alerta Habilitado** na etapa 5, o alerta estará ativo agora.</span><span class="sxs-lookup"><span data-stu-id="26482-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26482-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26482-165">Next Steps</span></span>
* <span data-ttu-id="26482-166">Analisar [estatísticas em tempo real na CDN do Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="26482-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="26482-167">Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="26482-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="26482-168">Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="26482-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

