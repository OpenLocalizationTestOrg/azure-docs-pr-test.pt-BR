---
title: "aaaAzure Interface de usuário do Mobile Engagement - Monitor"
description: Saiba como toomonitor de dados em tempo real sobre o seu aplicativo usando o Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a>Como toomonitor de dados em tempo real sobre o seu aplicativo
Este artigo descreve Olá **MONITOR** guia da saudação **Mobile Engagement** portal. Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis. Observe que toostart usando o portal de saudação toocreate primeiro é necessário um **do Azure Mobile Engagement** conta. 

Olá seção de Monitor de saudação da interface do usuário fornece informações de análise em tempo real e permite que você tooset alertas quando os limites são atingidos para a maioria dos Olá mesmo informações disponíveis historicamente em Olá [análise](mobile-engagement-user-interface-analytics.md) seção Saudação da interface do usuário. Consulte Olá **glossário** seção Olá [conceitos](http://go.microsoft.com/fwlink/?LinkId=525555) tópico para definições de termos e abreviações na análise e monitoramento (como a seguir Olá: usuário ativo, o novo usuário, usuário retido, sessão, Gráfico de caminho do usuário, os usuários mapa, URLs de acompanhamento, tendências, atividade, evento, trabalho, erro, informações adicionais, falhas e App-info).

> [!NOTE]
> Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão. Pressione este botão tooget mais informações contextuais sobre uma seção.
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a>Monitorar - sessões, trabalhos, eventos, erros e falhas
Você pode ver quantos usuários estão atualmente na sessão e em telas específicas ou executando ações específicas. Você pode exibir atividades de usuário divididas em sessões, trabalhos, eventos, erros e falhas. Você pode ver informações atuais de saudação e exiba informações de saudação do hello última hora, dia ou semana. Você pode ver todas as informações de saudação em cada categoria ou classificar por Olá específico de sessão, trabalho, evento, erro e falha.  Monitoramento em tempo real é útil toouse durante eventos como um toosee da campanha de Push se houver um aumento na ação à direita depois que você enviar a notificação por Push.

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a>Solucionando problemas com o Monitor - Eventos - Detalhes
Gerar um evento em seu aplicativo do seu dispositivo de teste e localizá-lo no Monitor - eventos - detalhes são um dos hello mais fácil maneiras toofind ID de seu dispositivo para seu dispositivo de teste e tooconfirm que integração do Azure Mobile Engagement de análise, monitoramento, e Segmentos estiver trabalhando em seu aplicativo. Quando você tiver Olá ID do dispositivo do seu dispositivo de teste, você pode adicionar dispositivos de teste tooyour em "Meus dispositivos de conta –". Se você não pode gerar um evento, certifique-se de que o Azure Mobile Engagement corretamente é integrado em seu aplicativo do Android/iOS/Web/Windows/Windows Phone com hello SDK.

Para obter mais informações, veja: [Documentação do SDK][Link 5]

![Monitor2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a>Solucionando problemas com Monitor - Falhas - Detalhes
Você pode examinar informações de falha sobre seu aplicativo de detalhes do Monitor - falhas - toohelp determinar por que o aplicativo está falhando. Você também deve procurar problemas conhecidos com cada versão do SDK de saudação nas notas de versão de saudação para cada versão do SDK para Android/iOS/Web/Windows/Windows Phone de saudação.

Para obter mais informações, veja: [Documentação do SDK – Notas de versão][Link 5]

![Monitor3][16]

## <a name="monitor---alerts"></a>Monitor - Alertas
Você também pode especificar condições para alertas que serão automaticamente enviados tooyou via email ou mensagem instantânea. (Quaisquer serviços compatíveis com XMPP, como GTalk do Google ou iChat da Apple, têm suporte). Os alertas são baseados em um limite de detecção predefinido maior que (>) ou menor que (<) um número específico de sessões, trabalhos, eventos, erros ou falhas por hora, minuto ou segundo. Alertas podem monitorar todas as atividades de um determinado tipo, ou apenas para monitorar uma atividade de um trabalho, evento ou erro específico. 

Você também pode especificar uma taxa mínima de detecção, que é a quantidade mínima de saudação de minutos que separará duas notificações do hello mesmo alerta toomake-se de que quando o alerta for disparado, você nunca receberá mais de 1 notificação por intervalo especificado.

![Monitor4][17]

## <a name="see-also"></a>Consulte também
* [Conceitos][Link 6]
* [Serviço do Guia de Solução de Problemas][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
