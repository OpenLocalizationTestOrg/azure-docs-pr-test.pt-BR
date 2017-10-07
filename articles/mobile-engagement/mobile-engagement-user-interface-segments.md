---
title: "aaaAzure Interface de usuário do Mobile Engagement - segmentos"
description: "Saiba como toocreate e gerenciam segmentos de padrões de uso de tooidentify usuários usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Como toocreate e gerenciam segmentos de padrões de uso de tooidentify de usuários
Este artigo descreve Olá **segmentos** guia da saudação **Mobile Engagement** portal. Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis.

seção de segmentos de saudação do hello da interface do usuário permite que você toowork em segmentando os usuários com base em um comportamento diferente hello e análise que você pode obter de um aplicativo hello e também pode acessar por meio de saudação segmentos de API. Segmentos são computados primeiro 24 horas depois que são criados, e eles são recalculados com base nas informações de análise mais recentes da saudação a cada 24 horas. Quando um segmento é calculado, ele exibe um gráfico de "Histórico de tooday do dia" por dia.

> [!NOTE]
> Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão. Pressione este botão tooget mais informações contextuais sobre uma seção.
> 
> 

## <a name="create-segments"></a>Criação segmentos
Você pode criar um segmento com base em critérios de too10 em um período específico se too60 dias Olá passado da seção de análise de saudação. Por exemplo, você pode criar um segmento com base em pessoas Olá tiveram exibido certas páginas ou pesquisada em busca de conteúdo específico dentro de seu aplicativo em Olá últimos 10 dias. Essas informações estão disponíveis na seção de análise de saudação. Assim, usá-lo em um segmento de toocreate e em seguida, configure um tootarget de notificação por push esse subconjunto dos usuários tooget-los toocome toohello back aplicativo. 

> [!NOTE]
> Após um segmento ter sido calculado, ele não pode ser editado; ele só pode ser clonado (copiado) ou destruído (excluído). Um segmento pode ser clonado em Olá mesmo aplicativo (com hello AppID mesmo), e também podem ser clonado em outros aplicativos (com um AppID diferente). 

 ![segments1][35] 

## <a name="examples-segments"></a>Exemplos de segmentos
 ![segments2][36]

Segmentos permitem que você toosegment os usuários finais de saudação do seu aplicativo.
Segmentar os usuários é uma importante estratégia de marketing. O Azure Mobile Engagement permite que os dados históricos tooget e criar segmentos personalizados. Essa ferramenta avançada permite que você toolearn sobre a experiência de seus clientes em seu aplicativo. Você pode facilmente analisar os segmentos e usá-los como destinos de envio.
Um caso de uso comum é que você deseja toosend um tooencourage uma notificação de envio por push seu usuários finais toorate seu aplicativo no repositório de saudação. Em vez de enviar uma notificação tooall seus usuários finais, você pode criar um segmento que deve especificar apenas os usuários que usaram seu aplicativo diariamente para Olá no último mês e tiveram um usuário ótimo experiência. Quando você envia notificações por push menos extremamente específicas, você pode obter um melhor ROI.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Segmentos, que você pode criar com base nas principais elementos do Azure Mobile Engagement hello:
* Evento: Crie um segmento de evento específico que destinos um aplicativo hello que ocorreram mais de duas vezes por semana. 
* Sessão: Crie um segmento de usuários que usaram o aplicativo hello mais de 5 vezes na semana passada.
* Atividade: crie um segmento de usuários que usaram uma página ou conteúdo mais ou menos 10 vezes no mês passado.
* Trabalho: crie um segmento de usuários que concluíram um trabalho mais de duas vezes ao dia.
* Falha: Crie um segmento de todos os usuários de saudação que tiveram uma falha de mais de 10 vezes na semana passada. (Você poderia enviar este segmento com uma desculpa ou até mesmo um cupom!)
* Erro: Crie um segmento de todos os usuários de saudação que tiveram um erro mais do que o 100 vezes da últimos 3 dias.
* Informações do aplicativo: Crie um segmento que tem como alvo um informações de aplicativo personalizado que ocorreram durante a saudação últimos 25 dias.
  
  ![segments4][38]

toouse segmento de maneira ideal, você deve ter feito uma integração personalizada do hello SDK em seu aplicativo com um plano de marcação de marcas "Informações de aplicativo".
Em seguida, vá toohello home page da interface Olá, selecione aplicativo hello desejado e clique na seção de "Segmentos" hello.

1. Selecione a seção de "Segmentos" hello.
2. Clique em hello "Novo segmento" botão toocreate um novo segmento.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Crie um segmento simples com base nas informações de "Sessão".
Crie um segmento de todos os usuários finais Olá que usou seu aplicativo pelo menos 50 vezes Olá última semana. A partir daí, localize somente Olá os usuários finais que passaram pelo menos 30 segundos no seu aplicativo por sessão. Isso mostrará todos os usuários finais Olá tem uma experiência positiva em seu aplicativo. Em seguida, segmento Olá criado pode ser usado toopush um tooask de usuários finais notificação toothese-los toorate seu aplicativo hello armazenar.

 ![segments5][39]

1. Nomeie o segmento em ordem toofind rapidamente na lista de "Segmento" hello.
2. Clique em Olá botão "Criar".
   
   ![segments6][40]

Selecione a sessão.

 ![segments7][41]

1. Selecione o período de saudação da "Última semana".
2. Clique em Avançar.
   
   ![segments8][42]
3. Selecione Olá operador relevantes lista Olá: =; ≥, ≤.
4. Digite hello contagem desejada.
5. Selecione Olá ocorrência desejado. 
6. Clique em Avançar.
   Este exemplo é definido para que mais Olá última semana, correspondência de usuários que fizeram pelo menos 50 sessões.
   
   ![segments9][43]

Para Olá segmentação de sessão, você pode escolher comprimento Olá por sessão como um critério.

1. Selecione Olá operador na lista de saudação.
2. Fornece Olá comprimento por sessão.
3. Clique em Avançar.
   Neste exemplo, ela diz que sobre todas hello sessões que foram segmentadas na seção de ocorrência hello, selecione apenas Olá usuários que passaram mais de 30 segundos por sessão.
   
   ![segments10][44]

Nomeie seu critério em ordem tooretrieve concluí-lo em Olá funil e clique em Concluir.

 ![segments11][45]

Quando você terminar a configuração ao seu critério, ele será exibido no funil de segmento de saudação.
Como um segmento é baseado em dados de análise, os segmentos são calculados uma vez por dia.
Neste exemplo, 47,7% dos usuários finais de total Olá correspondentes ao critério de saudação. Eles devem ser usuários Olá que tiveram uma boa experiência e será ser tooprovide provavelmente uma classificação mais alta, se você enviar uma notificação solicitando toorate Olá aplicativo no repositório de saudação.

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

