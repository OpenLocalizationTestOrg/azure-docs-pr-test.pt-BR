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
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Alertas em tempo real na CDN do Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Visão geral
Este documento explica os alertas em tempo real na CDN do Microsoft Azure. Essa funcionalidade fornece notificações em tempo real sobre o desempenho de saudação de pontos de extremidade de saudação em seu perfil CDN.  Você pode configurar alertas por email ou HTTP com base em:

* Largura de banda
* Códigos de status
* Status do Cache
* Conexões

## <a name="creating-a-real-time-alert"></a>Criar um alerta em tempo real
1. Em Olá [Portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.
   
    ![Folha Perfil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
3. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **estatísticas em tempo real** flutuante.  Clique em **Alertas em Tempo Real**.
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    saudação de lista de configurações de alerta existentes (se houver) é exibida.
4. Clique em Olá **adicionar alerta** botão.
   
    ![Botão Adicionar Alerta](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Um formulário para criar um novo alerta é exibido.
   
    ![Formulário Novo Alerta](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Se você quiser que esse alerta toobe ativa quando você clica em **salvar**, verificar Olá **alerta habilitado** caixa de seleção.
6. Insira um nome descritivo para o alerta no hello **nome** campo.
7. Em Olá **o tipo de mídia** lista suspensa, selecione **objeto grande HTTP**.
   
    ![Tipo de Mídia com Objeto Grande HTTP selecionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > Você deve selecionar **objeto grande HTTP** como Olá **o tipo de mídia**.  Olá outras opções não são usadas pelo **CDN do Azure da Verizon**.  Falha tooselect **objeto grande HTTP** fará com que o alerta toonever ser disparado.
   > 
   > 
8. Criar um **expressão** toomonitor selecionando um **métrica**, **operador**, e **disparar valor**.
   
   * Para **métrica**, selecione o tipo de saudação da condição que deseja monitorar.  **Mbps de largura de banda** é a quantidade de saudação do uso de largura de banda em megabits por segundo.  **Total de conexões** é o número de saudação do tooour de conexões de HTTP simultânea servidores de borda.  Para obter definições de saudação vários status do cache e códigos de status, consulte [códigos de Status de Cache do Azure CDN](https://msdn.microsoft.com/library/mt759237.aspx) e [códigos de Status de HTTP de CDN do Azure](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Operador** é Olá operador matemático que estabelece a relação Olá entre métrica hello e valor de saudação do gatilho.
   * **Disparar valor** é o valor de limite de saudação que deve ser atendido antes que uma notificação será enviada.
     
     Olá exemplo abaixo, expressão Olá criei indica que gostaria de toobe notificado quando o número de saudação de códigos de status 404 é maior que 25.
     
     ![Expressão de exemplo de alerta em tempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. Para **intervalo**, insira a frequência com a qual você deseja que expressão Olá avaliada.
10. Em Olá **notificar em** lista suspensa, selecione quando você deseja toobe notificado quando hello expressão for verdadeira.
    
    * **Início da condição** indica que uma notificação será enviada quando Olá especificado condição é detectada pela primeira vez.
    * **Condição final** indica que uma notificação será enviada quando Olá especificado não é detectado. Essa notificação só pode ser acionada após a detecção de nosso sistema de monitoramento de rede que Olá especificado condição ocorreu.
    * **Contínua** indica que uma notificação será enviada sempre que Olá sistema de monitoramento de rede detecta Olá especificado condição. Tenha em mente rede Olá monitoramento será de sistema somente a verificação de uma vez por intervalo de saudação a condição especificada.
    * **Condição de início e término** indica que uma notificação será enviada Olá Olá condição especificada pela primeira vez é detectado e novamente quando a condição de saudação não for detectada.
11. Se você quiser tooreceive notificações por email, verifique Olá **notificação por Email** caixa de seleção.  
    
    ![Formulário Notificar por Email](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    Em Olá **para** , digite o endereço de email de saudação é onde você deseja que as notificações enviadas. Para **assunto** e **corpo**, você pode deixar o padrão de saudação ou você pode personalizar a mensagem de saudação usando Olá **palavras-chave disponíveis** toodynamically lista Inserir dados de alerta quando mensagem de saudação é enviada.
    
    > [!NOTE]
    > Você pode testar a notificação por email Olá clicando Olá **notificação de teste** botão, mas somente após a configuração de alerta de saudação foi salvo.
    > 
    > 
12. Notificações toobe postada tooa servidor de web, marque Olá **notificar por HTTP Post** caixa de seleção.
    
    ![Formulário Notificar por HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    Em Olá **Url** , digite o URL Olá onde deseja que a mensagem de saudação HTTP postada. Em Olá **cabeçalhos** caixa de texto, digite Olá HTTP cabeçalhos toobe enviado na solicitação de saudação.  Para **corpo** você pode personalizar a mensagem de saudação usando Olá **palavras-chave disponíveis** toodynamically lista Inserir dados de alerta quando a mensagem é enviada.  **Cabeçalhos** e **corpo** padrão tooan XML carga semelhante toohello exemplo abaixo.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Você pode testar Olá notificação HTTP Post clicando Olá **notificação de teste** botão, mas somente após a configuração de alerta de saudação foi salvo.
    > 
    > 
13. Clique em Olá **salvar** botão toosave sua configuração de alerta.  Se você tiver selecionado **Alerta Habilitado** na etapa 5, o alerta estará ativo agora.

## <a name="next-steps"></a>Próximas etapas
* Analisar [estatísticas em tempo real na CDN do Azure](cdn-real-time-stats.md)
* Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)
* Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)

