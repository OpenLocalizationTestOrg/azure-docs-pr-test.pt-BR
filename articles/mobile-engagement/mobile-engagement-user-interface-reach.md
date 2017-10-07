---
title: "aaaAzure Interface de usuário do Mobile Engagement - alcance"
description: "Saiba como tooreach toohello usuários de seu aplicativo com notificações por push usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Como tooreach toohello usuários de seu aplicativo com notificações por push
Este artigo descreve Olá **alcançar** guia da saudação **Mobile Engagement** portal. Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis. Observe que toostart usando o portal de saudação toocreate primeiro é necessário um **do Azure Mobile Engagement** conta. Para obter mais informações, veja [Criar uma conta do Azure Mobile Engagement](mobile-engagement-create.md).

Olá atingir seção Olá interface do usuário é ferramenta de gerenciamento de campanha Olá Push onde você pode criar/editar/ativar/término/monitor e obter estatísticas sobre os recursos que também podem ser acessados por meio de hello API de alcance (e alguns elementos da saudação baixa e campanhas de notificação por Push nível de API do Push). Lembre-se de que, se você estiver usando APIs de saudação ou saudação da interface do usuário, você precisará toointegrate do Azure Mobile Engagement e alcance em seu aplicativo para cada plataforma com hello SDK antes de usar alcançar campanhas.

> [!NOTE]
> Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão. Pressione este botão tooget mais informações contextuais sobre uma seção.
> 
> 

## <a name="four-types-of-push-notifications"></a>Quatro tipos de notificações por Push
1. Anúncios - permitir toosend toousers de mensagens de anúncio que redirecioná-los tooanother local dentro de seu aplicativo ou toosend-los tooa página da Web ou armazenar fora de seu aplicativo. 
2. Pesquisas - permitir toogather informações de usuários finais por fazer perguntas a eles.
3. Envios de dados - permitir toosend um arquivo de dados binário ou base64. Olá informações contidas em um envio de dados são enviados tooyour aplicativo toomodify experiência atual dos usuários em seu aplicativo. Seu aplicativo precisa de dados de saudação toobe tooprocess capaz em um envio de dados.

## <a name="campaign-details"></a>Detalhes da campanha
Você pode editar, clonar, excluir ou ativar campanhas que não foram ativadas ainda focalizando seus nomes ou você pode clicar em tooopen-los. Você pode clonar campanhas que já foi ativadas focalizando seus nomes ou você pode clicar em tooopen-los. No entanto, você não pode alterar uma campanha depois que ela tiver sido ativada.

![Reach1][18]

## <a name="reach-feedback"></a>Comentários do Reach
Clique em **estatísticas** toosee detalhes de saudação de uma campanha de alcance. Olá **simples** exibição fornece uma representação visual na forma de saudação de um gráfico de barras de coluna sobre o que aconteceu, depois de uma campanha foi ativada. Olá **avançado** exibição fornece mais detalhes sobre a campanha de push hello. Esses detalhes não estará disponíveis se você estiver enviando uma campanha de teste ou seja, um dispositivo de teste tooa enviados por push. Veja como você deve interpretar esses detalhes:

1. **Enviado por push** -Isso especifica o número de saudação de mensagens enviadas por push toohello dispositivos. Esse número dependerá de público-alvo Olá especificado ao criar a campanha de push hello. Se você não especificar qualquer público-alvo, em seguida, esse push será enviado tooall Olá registrado dispositivos. Como todos os outros serviços de envio, nós não Olá enviar notificações por push diretamente toohello dispositivos, mas em vez disso, push toohello respectivas plataformas específicas Push Notification Services (PNS - GCM/APNS/WNS) para que eles podem oferecer notificações Olá toohello dispositivos. 
2. **Entregue** -Isso especifica o número de saudação de mensagens que são entregues pelo dispositivo de toohello PNS hello e confirmada com êxito como recebida pelo SDK do Mobile Engagement. 
   
   *Motivos para a contagem Entregues ser menor do que a contagem de Enviada por push:*
   
   1. Se usuário Olá tiver desinstalado o aplicativo hello de dispositivo Olá mas Olá PNS não sabe sobre ele em tempo de saudação que podemos enviar por push de saudação toohello PNS a mensagem de saudação será removida.
   2. Se dispositivo Olá Olá aplicativo mas próprios dispositivos Olá estavam offline por longos períodos de tempo, em seguida, hello PNS falhará toodeliver dispositivo de toohello de mensagem de saudação. 
   3. Se mensagem entregue toohello dispositivo mas Olá SDK do Mobile Engagement no aplicativo hello não reconhece o conteúdo de saudação da mensagem de saudação, descarta essa mensagem. Isso pode acontecer se a personalização de saudação da notificação de saudação no aplicativo hello gera uma exceção que captura de nós na mensagem de saudação SDK e drop Olá. Isso também pode ocorrer se Olá aplicativo no dispositivo hello está usando uma versão do SDK do Mobile Engagement que não é capaz de toounderstand hello mais recente versão da mensagem de saudação do envio de saudação enviadas de plataforma hello, mas isso é somente quando o aplicativo hello foi atualizado após a notificação de saudação foi distribuída de plataforma de saudação do serviço. Olá **avançado** guia informará quantas mensagens foram descartadas. 
   4. Em dispositivos iOS, mensagens, às vezes, não obter entregue se qualquer dispositivo hello está funcionando com bateria baixa ou se o aplicativo hello está consumindo uma quantidade significativa de energia durante o processamento de notificações remotas. Essa é uma limitação de dispositivos iOS de saudação.   
3. **Exibido** -Isso especifica o número de saudação de mensagens com êxito mostrados toohello usuário de aplicativo no dispositivo de saudação na forma de saudação de uma notificação de push/fora-de-aplicativo de sistema no Centro de notificação de saudação ou uma notificação no aplicativo em hello móvel aplicativo.  Olá **avançado** guia lhe indicará quantos foram notificações do sistema e quantos foram notificações no aplicativo. 
   
   *Motivos para exibidas contagem seja menor que a contagem de entregues (espera toobe exibido)*
   
   1. Se a campanha de notificação Olá tinha uma data de término nele e em seguida, é possível que Olá notificação foi entregue, mas quando o tempo de saudação veio tooopen e exiba-o usuário do aplicativo toohello, ele já expirou para que ele nunca foi exibido.   
   2. Se a notificação de saudação é uma notificação no aplicativo notificação Olá é exibida apenas quando o usuário do aplicativo hello abre o aplicativo hello. Em casos onde o usuário de aplicativo hello ainda não abriu o aplicativo hello, Olá SDK relatará que notificação Olá foi entregue, mas ainda não exibida até que o aplicativo hello é aberto. 
   3. Se notificação Olá é uma notificação no aplicativo e configurado toobe mostrado em uma determinada atividade/tela também notificação Olá será relatada como fornecidos, mas ainda não foram entregues até que o usuário de Olá abre aplicativo hello em uma tela específica. 
4. **Interações do usuário** -Especifica Olá número de mensagens de usuário do aplicativo que Olá interagiu com e incluirá mensagens de saudação que são acionadas ou encerradas. 
   
   * *usuário do aplicativo Hello pode tomar uma ação em uma notificação em uma saudação maneiras a seguir:*
     
     1. Se hello notificação é uma notificação de sistema/fora-de-app ou uma notificação no aplicativo enviado como apenas de notificação e usuário do aplicativo hello clica na notificação de saudação.
     2. Se notificação Olá é uma notificação no aplicativo com um texto ou modo de exibição web ou pesquisas hello, em seguida, o usuário do aplicativo clica no hello botão de ação de notificação de saudação.
     3. Se a notificação de saudação é uma notificação no aplicativo com uma exibição da web, em seguida, Olá cliques do usuário do aplicativo em uma URL Olá web somente na exibição [Android]
   * *usuário do aplicativo Hello pode sair de uma notificação em uma saudação maneiras a seguir:*
     
     1. Botão de saudação Fechar na notificação de saudação diretamente. 
     2. Passar o dedo ausente ou excluindo Olá notificação. 
     3. Notificações no aplicativo com o conteúdo de texto/web e pesquisas são exibidos normalmente toohello usuário de aplicativo em um processo de duas etapas. Eles veem uma notificação pela primeira vez e quando clicar nele, consulte o conteúdo de texto/web/sondagem subsequentes hello. usuário do aplicativo Hello pode sair de uma notificação em qualquer uma dessas etapas e detalhes de saudação na exibição avançada Olá captura isso. 
5. **Acionadas** -Isso especifica o número de saudação de mensagens que foram acionadas explicitamente pelo usuário do aplicativo hello. Este é o número de mais interessante de saudação como isso informa quantos usuários de aplicativo foram interessados por mensagem de saudação enviado na notificação de saudação. 

> [!NOTE]
> No iOS e plataformas do Windows, se usuário Olá Olá aplicativo abrir e campanha Olá foi uma campanha "A qualquer momento", em seguida, é possível que as notificações do aplicativo e no aplicativo são exibidas em hello simultaneamente. Isso pode causar uma contagem de exibidas maior Olá entregues. Se usuário Olá interage ou notificação de saudação de ações, Olá, em seguida, até mesmo as interações do usuário/Actioned contagem pode ser maior que entregues. 
> 
> 

![Reach2][19]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

