---
title: "aaaAzure Interface de usuário do Mobile Engagement - acessar conteúdo"
description: "Saiba como o conteúdo de exclusivo Olá toomanage de tipos diferentes de saudação de notificação por push campanhas no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>Como toomanage Olá conteúdo exclusivo de tipos diferentes de saudação de campanhas de notificação por push
Você pode usar a seção de conteúdo de saudação de um novo contato campanha toomodify Olá conteúdo de anúncios, votações, envia dados e blocos (somente no Windows Phone). configuração de conteúdo de saudação de campanhas de Push é toohello específico de tipo de campanha. 

### <a name="content-types"></a>Tipos de conteúdo:
* Anúncios
* Pesquisas
* Envios de dados por push
* Blocos (apenas no Windows Phone)

## <a name="content-of-announcements"></a>Conteúdo de anúncios
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>Escolha o tipo de saudação da notificação:
* Somente notificação: é uma notificação simples padrão. Isso significa que se um usuário clica nela, nenhuma exibição adicional será exibida, mas somente a ação de saudação associados tooit ocorrerá.
* Anúncio de texto: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição de texto.
* Anúncio da Web: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição da web.

### <a name="see-also"></a>Consulte também
* [Alcance ‑ Instruções ‑ Anúncios][Link 3] 

### <a name="about-web-view-announcements"></a>Sobre os anúncios de exibição na Web:
Ocorrências do padrão de hello "{deviceid}" no código HTML da saudação ou código JavaScript fornecidos aqui serão automaticamente substituídas pelo identificador de saudação do dispositivo Olá exibindo comunicado hello. Este é um identificadores de dispositivo do modo fácil tooretrieve do Azure Mobile Engagement em externo web serviço hospedado em seu back office.
Se você quiser toocreate uma completa da tela (sem saudação padrão botões ação e sair fornecemos) no modo de exibição web você pode usar o hello funções a seguir do código de JavaScript do anúncio de exibição da web: 

* executar ação da notificação Olá: ReachContent.actionContent()
* sair do anúncio de saudação: ReachContent.exitContent()

### <a name="choose-your-action"></a>Escolha a ação:
### <a name="about-action-urls"></a>Sobre as URLs de ação:
Qualquer URL que possa ser interpretada pelo sistema operacional de destino do dispositivo pode ser usada como uma URL de ação.
Qualquer URL dedicada que seu aplicativo pode suporte (por exemplo, os usuários toomake saltar tooa determinada tela) também pode ser usado como uma URL de ação.
Cada ocorrência do padrão de Olá {deviceid} é substituída automaticamente pelo identificador de saudação do dispositivo Olá executar ação hello. Isso pode ser usado tooeasily recuperar identificadores de dispositivo do Azure Mobile Engagement por meio de um serviço web externo hospedado em seu back office.

* **Ações do Android + iOS**
  * Abrir uma página Web
  * http://\[web-site-domain\] 
  * Exemplo:http://www.azure.com
  * Enviar um email
  * mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * Enviar um SMS
  * sms:\[número-de-telefone\] 
  * Exemplo:sms:2125551212
  * Discar um número de telefone
  * tel:\[número-de-telefone\] 
  * Exemplo:tel:2125551212
* **Somente ações do Android**
  * Baixar um aplicativo hello Play Store
  * market://details?id=\[app package\] 
  * Exemplo:market://details?id=com.microsoft.office.word
  * Iniciar uma pesquisa localizada geograficamente
  * geo:0,0?q=\[search query\] 
  * Exemplo:geo:0,0?q=starbucks,paris
* **Somente ações do iOS**
  * Baixar um aplicativo hello App Store
  * http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8 
  * Exemplo:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Ações do Windows
  * Abrir uma página Web
  * http://\[web-site-domain\] 
  * Exemplo:http://www.azure.com
  * Enviar um email
  * mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * Enviar um SMS (necessário o aplicativo da Skype Store)
  * sms:\[número-de-telefone\] 
  * Exemplo:sms:2125551212
  * Discar um número de telefone (necessário o aplicativo da Skype Store)
  * tel:\[número-de-telefone\] 
  * Exemplo:tel:2125551212
  * Baixar um aplicativo hello Play Store
  * ms-windows-store:PDP?PFN=\[app package ID\] 
  * Exemplo: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * Iniciar uma pesquisa do Bing Mapas
  * bingmaps:?q=\[consulta de pesquisa\] 
  * Exemplo:bingmaps:? q=starbucks,paris
  * Usar um esquema personalizado
  * \[esquema personalizado\]://\[parâmetros do esquema personalizado\] 
  * Exemplo:myCustomProtocol://myCustomParams
  * Usar um pacote de dados (necessário o aplicativo da Store para leitura de extensão)
  * \[pasta\]\[dados\].\[extensão\] 
  * Example:myfolderdata.txt

### <a name="build-a-tracking-url"></a>Criar uma URL de rastreamento:
* Consulte Olá a seção "Configurações" hello <UI Documentation> para obter instruções sobre como criar uma URL de acompanhamento que permitirá toodownload usuários um de seus outros aplicativos.

### <a name="define-hello-texts-of-your-announcement"></a>Definir Olá textos da notificação
Preencha Olá título, conteúdo e textos de botão da notificação. Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha. Público-alvo pode ser com base nos comentários de saudação do se essa campanha foi apenas enviada, respondidas, acionadas ou encerradas.

### <a name="see-also"></a>Consulte também
* [Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]

## <a name="content-of-polls"></a>Conteúdo das pesquisas
![Reach-Content2][31] 

Preencha Olá título, descrição e textos de botão da notificação. Em seguida, adicione perguntas e opções para Olá respostas tooyour perguntas.
Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha. O público-alvo direcionado pode ser baseado no fato desta campanha ter sido apenas enviada por push, respondida, acionada ou encerrada. Público-alvo também pode ser baseado nos comentários de resposta de sondagem, em que escolha de pergunta e resposta hello são usadas como critérios.

### <a name="see-also"></a>Consulte também
* [Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]

## <a name="content-of-data-pushes"></a>Conteúdo de envio de dados por push
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a>Escolha o tipo de saudação de seus dados:
* Texto
* Dados binários
* Dados Base64

### <a name="define-hello-content-of-your-data"></a>Definir o conteúdo de saudação de seus dados
* Se você selecionou toopush dados de texto, copie e cole o texto de saudação na caixa "conteúdo" hello.
* Se você selecionou toopush dados binários ou base64, use tooupload de botão "carregar o arquivo" hello seu arquivo.
* Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha. O público-alvo direcionado pode ser baseado no fato desta campanha ter sido apenas enviada por push, respondida, acionada ou encerrada.

### <a name="see-also"></a>Consulte também
* [Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Conteúdo de blocos (somente para o Windows Phone)
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a>Definir o conteúdo de saudação do bloco
carga de bloco de saudação é toobe de texto de saudação exibida no bloco de saudação do seu aplicativo em dispositivos Windows Phone.
Um envio por push de bloco é Olá Microsoft Push Notification Service (MPNS) versão um envio por push nativo para Windows Phone. tipo de envio por push de bloco Olá é Olá único push tipo que não tem uma resposta e então público Olá futuras campanhas não pode ser criado em resultados de saudação de uma campanha de push de bloco. 

### <a name="see-also"></a>Consulte também
* [Documentação da API – API de Alcance – Envio por Push Nativo][Link 4]

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

