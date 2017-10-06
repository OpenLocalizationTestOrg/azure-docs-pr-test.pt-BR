---
title: alertas em tempo real de CDN aaaAzure | Microsoft Docs
description: "Alertas em tempo real na CDN do Microsoft Azure. Os alertas em tempo real fornecem notificações sobre o desempenho de saudação de pontos de extremidade de saudação em seu perfil CDN."
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="79817-104">Alertas em tempo real na CDN do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="79817-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="79817-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="79817-105">Overview</span></span>
<span data-ttu-id="79817-106">Este documento explica os alertas em tempo real na CDN do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="79817-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="79817-107">Essa funcionalidade fornece notificações em tempo real sobre o desempenho de saudação de pontos de extremidade de saudação em seu perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="79817-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="79817-108">Você pode configurar alertas por email ou HTTP com base em:</span><span class="sxs-lookup"><span data-stu-id="79817-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="79817-109">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="79817-109">Bandwidth</span></span>
* <span data-ttu-id="79817-110">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="79817-110">Status Codes</span></span>
* <span data-ttu-id="79817-111">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="79817-111">Cache Statuses</span></span>
* <span data-ttu-id="79817-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="79817-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="79817-113">Criar um alerta em tempo real</span><span class="sxs-lookup"><span data-stu-id="79817-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="79817-114">Em Olá [Portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="79817-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Folha Perfil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="79817-116">Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="79817-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="79817-118">portal de gerenciamento de CDN Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="79817-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="79817-119">Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **estatísticas em tempo real** flutuante.</span><span class="sxs-lookup"><span data-stu-id="79817-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="79817-120">Clique em **Alertas em Tempo Real**.</span><span class="sxs-lookup"><span data-stu-id="79817-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="79817-122">saudação de lista de configurações de alerta existentes (se houver) é exibida.</span><span class="sxs-lookup"><span data-stu-id="79817-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="79817-123">Clique em Olá **adicionar alerta** botão.</span><span class="sxs-lookup"><span data-stu-id="79817-123">Click hello **Add Alert** button.</span></span>
   
    ![Botão Adicionar Alerta](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="79817-125">Um formulário para criar um novo alerta é exibido.</span><span class="sxs-lookup"><span data-stu-id="79817-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulário Novo Alerta](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="79817-127">Se você quiser que esse alerta toobe ativa quando você clica em **salvar**, verificar Olá **alerta habilitado** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="79817-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="79817-128">Insira um nome descritivo para o alerta no hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="79817-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="79817-129">Em Olá **o tipo de mídia** lista suspensa, selecione **objeto grande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="79817-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo de Mídia com Objeto Grande HTTP selecionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="79817-131">Você deve selecionar **objeto grande HTTP** como Olá **o tipo de mídia**.</span><span class="sxs-lookup"><span data-stu-id="79817-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="79817-132">Olá outras opções não são usadas pelo **CDN do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="79817-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="79817-133">Falha tooselect **objeto grande HTTP** fará com que o alerta toonever ser disparado.</span><span class="sxs-lookup"><span data-stu-id="79817-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="79817-134">Criar um **expressão** toomonitor selecionando um **métrica**, **operador**, e **disparar valor**.</span><span class="sxs-lookup"><span data-stu-id="79817-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="79817-135">Para **métrica**, selecione o tipo de saudação da condição que deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="79817-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="79817-136">**Mbps de largura de banda** é a quantidade de saudação do uso de largura de banda em megabits por segundo.</span><span class="sxs-lookup"><span data-stu-id="79817-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="79817-137">**Total de conexões** é o número de saudação do tooour de conexões de HTTP simultânea servidores de borda.</span><span class="sxs-lookup"><span data-stu-id="79817-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="79817-138">Para obter definições de saudação vários status do cache e códigos de status, consulte [códigos de Status de Cache do Azure CDN](https://msdn.microsoft.com/library/mt759237.aspx) e [códigos de Status de HTTP de CDN do Azure](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="79817-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="79817-139">**Operador** é Olá operador matemático que estabelece a relação Olá entre métrica hello e valor de saudação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="79817-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="79817-140">**Disparar valor** é o valor de limite de saudação que deve ser atendido antes que uma notificação será enviada.</span><span class="sxs-lookup"><span data-stu-id="79817-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="79817-141">Olá exemplo abaixo, expressão Olá criei indica que gostaria de toobe notificado quando o número de saudação de códigos de status 404 é maior que 25.</span><span class="sxs-lookup"><span data-stu-id="79817-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Expressão de exemplo de alerta em tempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="79817-143">Para **intervalo**, insira a frequência com a qual você deseja que expressão Olá avaliada.</span><span class="sxs-lookup"><span data-stu-id="79817-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="79817-144">Em Olá **notificar em** lista suspensa, selecione quando você deseja toobe notificado quando hello expressão for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="79817-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="79817-145">**Início da condição** indica que uma notificação será enviada quando Olá especificado condição é detectada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="79817-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="79817-146">**Condição final** indica que uma notificação será enviada quando Olá especificado não é detectado.</span><span class="sxs-lookup"><span data-stu-id="79817-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="79817-147">Essa notificação só pode ser acionada após a detecção de nosso sistema de monitoramento de rede que Olá especificado condição ocorreu.</span><span class="sxs-lookup"><span data-stu-id="79817-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="79817-148">**Contínua** indica que uma notificação será enviada sempre que Olá sistema de monitoramento de rede detecta Olá especificado condição.</span><span class="sxs-lookup"><span data-stu-id="79817-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="79817-149">Tenha em mente rede Olá monitoramento será de sistema somente a verificação de uma vez por intervalo de saudação a condição especificada.</span><span class="sxs-lookup"><span data-stu-id="79817-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="79817-150">**Condição de início e término** indica que uma notificação será enviada Olá Olá condição especificada pela primeira vez é detectado e novamente quando a condição de saudação não for detectada.</span><span class="sxs-lookup"><span data-stu-id="79817-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="79817-151">Se você quiser tooreceive notificações por email, verifique Olá **notificação por Email** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="79817-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Formulário Notificar por Email](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="79817-153">Em Olá **para** , digite o endereço de email de saudação é onde você deseja que as notificações enviadas.</span><span class="sxs-lookup"><span data-stu-id="79817-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="79817-154">Para **assunto** e **corpo**, você pode deixar o padrão de saudação ou você pode personalizar a mensagem de saudação usando Olá **palavras-chave disponíveis** toodynamically lista Inserir dados de alerta quando mensagem de saudação é enviada.</span><span class="sxs-lookup"><span data-stu-id="79817-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="79817-155">Você pode testar a notificação por email Olá clicando Olá **notificação de teste** botão, mas somente após a configuração de alerta de saudação foi salvo.</span><span class="sxs-lookup"><span data-stu-id="79817-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="79817-156">Notificações toobe postada tooa servidor de web, marque Olá **notificar por HTTP Post** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="79817-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulário Notificar por HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="79817-158">Em Olá **Url** , digite o URL Olá onde deseja que a mensagem de saudação HTTP postada.</span><span class="sxs-lookup"><span data-stu-id="79817-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="79817-159">Em Olá **cabeçalhos** caixa de texto, digite Olá HTTP cabeçalhos toobe enviado na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="79817-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="79817-160">Para **corpo** você pode personalizar a mensagem de saudação usando Olá **palavras-chave disponíveis** toodynamically lista Inserir dados de alerta quando a mensagem é enviada.</span><span class="sxs-lookup"><span data-stu-id="79817-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="79817-161">**Cabeçalhos** e **corpo** padrão tooan XML carga semelhante toohello exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="79817-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="79817-162">Você pode testar Olá notificação HTTP Post clicando Olá **notificação de teste** botão, mas somente após a configuração de alerta de saudação foi salvo.</span><span class="sxs-lookup"><span data-stu-id="79817-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="79817-163">Clique em Olá **salvar** botão toosave sua configuração de alerta.</span><span class="sxs-lookup"><span data-stu-id="79817-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="79817-164">Se você tiver selecionado **Alerta Habilitado** na etapa 5, o alerta estará ativo agora.</span><span class="sxs-lookup"><span data-stu-id="79817-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79817-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79817-165">Next Steps</span></span>
* <span data-ttu-id="79817-166">Analisar [estatísticas em tempo real na CDN do Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="79817-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="79817-167">Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="79817-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="79817-168">Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="79817-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

