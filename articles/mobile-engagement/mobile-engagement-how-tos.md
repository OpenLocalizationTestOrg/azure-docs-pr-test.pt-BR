---
title: "aaaAzure Interface de usuário do Mobile Engagement - alcançar How To"
description: "Visão geral da Interface de usuário para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Como tooget iniciado usando e gerenciando envia tooreach os usuários finais de tooyour
Depois de hello SDK está totalmente integrado ao seu aplicativo, você pode começar usando Olá Olá alcance seção de saudação da interface do usuário tooPush notificações toohello usuários em seu aplicativo.  

## <a name="do-your-first-push-notification-campaign"></a>Faça sua primeira campanha de notificação por push
* Confirme que o seu alcance é integrado ao seu aplicativo com hello SDK. 
* Selecione seu aplicativo

![First1][1]

* Vá toohello seção "Alcance" e clique em "novo comunicado"

![First2][2]

* Criar uma nova campanha e nomeie-a
  
![First3][3]

* Selecione como a notificação de saudação deve ser entregue, como no aplicativo somente

![First4][4]

* Criar mensagem de saudação desejado toopush

![First5][5]

* Você pode escrever um título na notificação de saudação (opcional).
* Gravar o conteúdo da mensagem por push.
* Você pode carregar uma imagem. Lembre-se de que o tamanho de saudação do arquivo hello não pode exceder 32.768 bytes.
* Você também tem Olá capacidade tooselect mais opções, mas para foco Olá deste tutorial, veremos que mais tarde.
* Selecione o tipo de conteúdo hello como notificação apenas

![First6][6]

* Crie sua campanha de envio e ele aparecerá na lista de campanha.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Testar sua campanha de notificação por push
![Test1][8]

* Registre seu dispositivo.
* Clique na caixa de seleção de saudação do dispositivo Olá você deseja toopush.
* Clique em hello "Testar" botão toosend Olá push toohello dispositivo.

![Test2][9]

* Ativar Olá campanha

![Test3][10]

* Agora que você criou sua campanha, basta tooactivate-o para hello toobe de notificação enviada por push usuários tooyour.

## <a name="send-personalized-pushes"></a>Enviar pressionamentos personalizados
* Este exemplo cria um envio por push em que um código de desconto personalizado é inserido na notificação de envio de saudação.

![Personalize1][11]

Personalização funciona substituindo um marcador, de uma marca de informações do aplicativo, assim, você terá toomake se usuário Olá tem Olá adequada app-info definido primeiro. Olá Este exemplo usuários de destino terão uma marca de informações de aplicativo chamada rebate_code definido.
Como você vê acima conteúdo da notificação por push Olá inclui Olá marcador ${rebate_code} que indicará que ele toobe substituído pelo conteúdo real de saudação da marca de informações do aplicativo hello.

> [!WARNING]
> Se a marca de informações do aplicativo hello não está definida para o usuário hello, usuário Olá não receberá push hello.

* Result

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Você pode personalizar ainda mais o texto de saudação a notificação
![Personalize3][13]

* Incluindo Olá título de notificação de saudação
* E Olá conteúdo de mensagem de saudação.
* Escolha o tipo de saudação do anúncio (exibição de texto ou da Web)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>corpo de saudação de um comunicado também pode ser personalizado com:
* Olá a URL da ação, você deve toocustomize Olá página inicial
* título de saudação
* corpo de saudação da mensagem de saudação.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Diferenciar a sua notificação por push (estando ou não no aplicativo)
* Escolha o tipo de saudação de notificação será push, selecione seu aplicativo, vá toohello "Alcance" seção, selecionar ou criar uma campanha de push e vá toohello seção de "Notificação".
* Clique em hello "modo de entrega" desejado.
* Clique em hello "Restringir atividades" caixa de seleção quando desejar notificação Olá ocorre em atividades específicas (telas).

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>Modo de entrega "Somente fora do aplicativo"
![Differentiate2][16]

"Somente fora do aplicativo" modo de entrega fornece notificação por push ao aplicativo hello está fechado. Esta é a notificação de push padrão de saudação.
Quando você seleciona "fora do aplicativo", você deve já ter fornecido certificados Olá de plataforma Olá que seu aplicativo está aproveitando (APNS ou GCM).

### <a name="see-also"></a>Consulte também
* [Apple Push Notification Service – Certificados](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificado](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>Modo de entrega "Apenas no aplicativo"
![Differentiate3][17]

Modo de entrega "No aplicativo somente" fornece notificação por push ao aplicativo hello está em execução.
Para essa notificação, não é necessário toogo por meio de saudação APNS e do sistema do GCM.
Você pode usar tooreach de sistema de entrega no aplicativo hello seus usuários finais.
Totalmente, você pode personalizar a notificação de saudação e decidir em qual atividade (tela) notificação Olá será exibida.

### <a name="anytime-delivery-mode"></a>Modo de entrega a "Qualquer hora"
Você pode escolher um modo de entrega "A qualquer momento", o que garante a você tooreach seu usuário final se Olá aplicativo está sendo executado ou não.
Quando você selecionar "A qualquer momento", você deve já ter fornecido certificados Olá de plataforma Olá que seu aplicativo baseando (APNS ou GCM). 

## <a name="schedule-a-push-campaign"></a>Agendar uma campanha de envio por push
### <a name="plan-toostart-a-campaign"></a>Planejar uma campanha de tooStart
![Shedule1][18]

Ele é hello 21 de março e toomake um anúncio e planejado para Olá 22 de março de à meia-noite. Você não tem toostay na frente Olá interface toodo um envio por push! Você pode planejar com antecedência Olá exato minuto notificações serão enviadas.

* Desmarque a opção hello "None" caixa de seleção e selecione uma hora de início 
* Escolha date de hello e a hora de saudação desejado campanha de push toostart hello.

### <a name="plan-tooend-a-campaign"></a>Planejar uma campanha de tooend
![Shedule2][19]

Você deseja toostop sua campanha em Olá 25 de março 3.00 pm mas você sabe que não será existe toodo-lo.
Você não tem toostay na frente Olá interface toopush! Você pode planejar com antecedência Olá exato minuto que sua campanha será interrompida.

* Clique em hello "None" caixa de seleção ou selecione uma hora de término
* Escolha date de hello e a hora de saudação desejado campanha de push toofinish hello.

### <a name="end-a-campaign-manually"></a>Terminar uma campanha manualmente
![Shedule3][20]

Por padrão, Olá "None" caixas de seleção estão marcadas.
Isto significa que a campanha Olá será iniciada assim que você ativá-la no hello alcançar seção e final quando interromperá em Olá alcançará seção.

> [!NOTE]
> Campanhas criadas sem uma data de término armazenam Olá push localmente no dispositivo hello e mostrá-lo Olá próxima vez aplicativo hello for aberto, mesmo que a campanha Olá é encerrada manualmente.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Aprimorar uma notificação por Push com uma Exibição de texto
### <a name="what-is-a-text-view"></a>O que é uma Exibição de texto?
![TextView1][21]

Uma exibição de texto é um pop-up com conteúdo de texto. Essa janela pop-up aparece depois dos usuários finais de saudação clicou na notificação de push hello.
Uma exibição de texto permite que você toopresent mais conteúdo tooyour pelos usuários finais. Isso também é Olá oportunidade toopresent tooaction uma chamada como saltando tooa página do seu aplicativo, redirecionando tooa repositório, abrir uma página da web, enviar um email, iniciando uma pesquisa cercas geográficas, etc...

### <a name="example-text-view"></a>Exemplo: Exibição de texto
* Criar sua campanha de notificação por Push na seção de "Acessar" hello e dê um nome de sua campanha

![TextView2][22]

* Grave a mensagem de saudação que será exibido na notificação de saudação.
* Selecione Olá anúncio de tipo de conteúdo "texto"

![TextView3][23]

> [!NOTE]
> Quando você envia por push uma exibição de texto, ela sempre vem com uma notificação pela primeira vez. 

* Definir o texto de saudação (após a seleção de conteúdo de anúncio de texto de saudação, sub-seção Olá será exibida, permitindo que você toodefine Olá texto toobe exibido.)

![TextView4][24]

* Escreva Olá título que será exibido na parte superior de saudação da mensagem de saudação.
* Grave o conteúdo principal de saudação do modo de exibição de texto de saudação.
* Grave o conteúdo de saudação que será exibido no botão de ação hello (Olá aplicativo toomake uma ação específica, como abrir uma página de aplicativo hello, redirecionando tooan App store ou qualquer tipo de fontes que você pode fornecer permite que um botão de ação).
* Conteúdo de saudação de gravação que será exibido no botão de sair da saudação (clicando no botão de saída de hello, exibição de texto de saudação desaparecerá.)
* Crie sua campanha de notificação por push e ele será exibido na lista de saudação da campanha.

![TextView5][25]

* Ative seu envio notificação campanha toosend Olá texto exibição tooyour usuários.

![TextView6][26]

* Result

![TextView7][27]

* Olá usuário recebe a notificação de saudação e clique nele.
* exibição de texto de saudação aparece como um toointeract pop-up de permissão do usuário Olá com ele.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Aprimorar uma notificação por push com uma exibição da web
### <a name="what-is-a-web-view"></a>O que é uma exibição da Web?
![WebView1][28]

Uma exibição da web é um pop-up com conteúdo da web. Essa janela pop-up aparece quando o usuário final de saudação clicou na notificação de push hello.
Uma exibição da web permite que você toohave mais interação com o usuário final de saudação.
Isso também é Olá oportunidade toopresent tooaction uma chamada como redirecionamento tooApp repositório, abrir uma página da web, enviar um email, iniciando uma pesquisa cercas geográficas, etc...

### <a name="example-web-view"></a>Exemplo: Exibição da Web
* Crie sua campanha de Push na seção de "Acessar" hello e dê um nome de sua campanha.

![WebView2][29]

* Grave a mensagem de saudação que será exibido na notificação de saudação.
* Selecione Olá anúncio de tipo de conteúdo como "web"

![WebView3][30]

### <a name="about-announcement-types"></a>Sobre os tipos de comunicado:
* Somente notificação: é uma notificação simples padrão. Isso significa que se um usuário clica nela, nenhuma exibição adicional será exibida, mas somente a ação de saudação associados tooit ocorrerá.
* Anúncio de texto: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição de texto.
* Anúncio da Web: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição da web.
  Selecione Olá conteúdo "Anúncio da Web".

> [!NOTE]
> quando você envia por push uma exibição da web, ela sempre vem com uma notificação pela primeira vez.

* Definir o conteúdo da web de saudação (após ter Olá web comunicado conteúdo selecionado, subseção Olá será exibida, permitindo que você toodefine Olá web exibir conteúdo que você deseja toobe exibido.)

![WebView4][31]

* Escreva Olá título que será exibido na parte superior de saudação da mensagem de saudação (opcional).
* Escreva o código HTML aqui.
* Clique na fonte de saudação edição de tooswitch do botão de modo de edição e ver como ele se parece com.
* Grave o conteúdo de saudação que será exibido no botão de ação hello (Olá aplicativo toomake uma ação específica, como abrir uma página de aplicativo hello, redirecionando tooa repositório ou qualquer tipo de fontes que você pode fornecer permite que um botão de ação).
* Conteúdo de saudação de gravação que será exibido no botão de sair da saudação (clicando no botão de saída de hello, modo de exibição de web hello desaparecerá).
* Result

![WebView5][32]

* usuário Olá receber notificação hello e clique nele.
* exibição de texto de saudação aparece como um toointeract pop-up de permissão do usuário Olá com ele.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

