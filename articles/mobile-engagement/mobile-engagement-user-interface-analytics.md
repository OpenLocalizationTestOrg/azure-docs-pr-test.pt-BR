---
title: "aaaAzure Interface de usuário do Mobile Engagement - análise"
description: "Saiba como tooanalyze os dados históricos sobre seu aplicativo usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Como os dados históricos sobre o seu aplicativo tooanalyze
Este artigo descreve Olá **análise** guia da saudação **Mobile Engagement** portal. Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis. Observe que toostart usando o portal de saudação toocreate primeiro é necessário um **do Azure Mobile Engagement** conta.

Olá seção de análise de saudação da interface do usuário fornece informações agregadas sobre seu aplicativo com base em dados históricos que são atualizados a cada 24 horas. Olá informações são exibidas em painéis diferentes compostos de mapas, grades e gráficos de barra/linha/pizza. dados de saudação também podem ser baixados como arquivos. csv. A maioria das mesmas informações está disponível em tempo real em Olá seção de Monitor de saudação da interface do usuário, e também podem ser acessado de saudação API de análise.

> [!NOTE]
> Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão. Pressione este botão tooget mais informações contextuais sobre uma seção.

## <a name="standard-and-custom-analytics"></a>Análise padrão e personalizada
O Azure Mobile Engagement fornece um conjunto de informações analíticas basic, standard sobre os aplicativos que podem ser mostrados como integrar seu aplicativo hello SDK. O Azure Mobile Engagement também fornece Olá capacidade toogather personalizados de análise adicional informações que você deseja sobre o comportamento de seus usuários finais. Você pode fazer isso criando um plano de marca das “Marcas (informações do aplicativo)” personalizadas, criado em **Configurações** para que o Azure Mobile Engagement possa coletar esses dados adicionais para você.

## <a name="analytics"></a>Análise
* Painel: Mostra informações gerais sobre os usuários novos e ativos e suas tendências.
* Usuários: Os usuários são identificados por seu identificador de dispositivo: esse identificador é exclusivo para cada dispositivo (um novo usuário é, na verdade, um novo dispositivo). Um usuário é considerado como novo em um intervalo de tempo se ele realizou sua primeira sessão durante este intervalo de tempo. Um usuário é considerado como retido se ele tiver executado pelo menos uma sessão durante a saudação últimos 7 dias. Usuários ativos são usuários que fizeram pelo menos uma sessão durante um determinado período. Você pode classificar por mensal, semanal, diária ou períodos de tempo por hora. Todos os gráficos de saudação semelhante mas permitem que você toofilter por diferentes recursos, como a versão de saudação do seu aplicativo e, em seguida, toosort por um período de tempo. Olá, padrão informações coletadas, integrando Olá SDK incluem seguinte Olá: usuários ativos, o novo usuário, o número de sessões, o comprimento de cada sessão, as informações técnicas sobre o país hello, locais, local, operadora de idioma, dispositivos, firmware, rede (Wi-Fi), versões do aplicativo hello e o SDK, usado por clientes. Essas informações podem ser exibidas em tempo real da seção de monitor de saudação.

> [!NOTE]
> Olá período de tempo é baseado nas Olá data dos usuários Olá configurações de dispositivo, para que um usuário cujo telefone tiver date de hello definida incorretamente pode aparecer em Olá errado período de tempo.

* Retenção: Um usuário é considerado como retido em um determinado intervalo de tempo se ele realizou sua primeira sessão durante este intervalo de tempo. Você pode alterar os intervalos de tempo de saudação durante os quais usuários retidos (e novos) são contados toohours, dias, semanas ou meses. análise de retenção de usuário Olá é criada sobre colaboradores. Um cohort é o conjunto de saudação de todos os usuários novos Olá detectado por um determinado período (ou seja, o conjunto de saudação de usuários executar sua primeira sessão durante esse período). Usamos coortes de 1 dia, 2 dias, 4 dias, 7 dias ou 1 mês. Especificado um cohort, cada 1 dia, 2 dias, 4 dias, 7 dias, 1 mês, Azure Mobile Engagement calcula Olá conjunto de ou todos os usuários que pertencem toohello cohort e são ainda está ativa (ou seja, o conjunto de Olá de usuários que executaram pelo menos uma sessão durante o período de saudação). Este conjunto de usuários é chamado uma versão coorte. (O azure Mobile Engagement pode mostrar a quantos de seus usuários ainda estão usando o seu aplicativo, mas somente loja específica de plataforma de saudação pode determinar a quantos de seus usuários desinstalado o iTunes app - por exemplo, GooglePlay, Windows Store, etc.).
* Sessões: Um uso de aplicativo hello por um usuário. Sessões são geradas de sequência de saudação de atividades executadas pelos usuários (uma atividade é geralmente associado toohello uso de uma tela do aplicativo hello, mas isso pode variar dependendo Olá Olá de maneira SDK foi integrado no aplicativo hello). Um usuário só pode executar uma atividade em um momento: uma sessão é iniciada assim que o usuário de saudação inicia sua primeira atividade e é interrompido quando ele termina sua última atividade. Se um usuário permanecer mais de alguns segundos sem executar qualquer atividade, sua sequência de atividades é dividida em duas sessões distintas.
* Atividades: nomes de saudação de cada tela no seu aplicativo e o comprimento de saudação de tempo que os usuários gastam em cada tela. Atividades são uma opção personalizada analítica que corresponderá marcas de "app info" toohello que você configurou para seu próprio aplicativo:
* Caminho do usuário: Mostra como os usuários navegam por meio de atividades do aplicativo (telas). Você pode mover o nível de saudação do hello controle deslizante tooadjust de detalhes. Nós azuis representam as atividades do seu aplicativo. Seu tamanho é proporcional toohello vez que os usuários gastam nele. Nós brancos representam o início e o final da sessão. Nós vermelhos representam falhas. Os links representam as transições entre as atividades do aplicativo (ou entre atividades e falhas). Clique em um nó ou um link toodisplay uma dica de ferramenta com mais informações sobre seus dados: tempo de saudação gasto em determinada tela, Olá contagem de transições e Olá percentual de transições da atividade de destino do hello origem atividade toohello. (Um---60%---> B significa que os usuários na atividade for tooactivity B 60% de tempo de saudação.) Você pode reorganizar o gráfico de saudação como você deseja tooclarify; sua posição é salva toda vez que fizer uma alteração. Você pode mostrar ou ocultar Olá falhas toolighten Olá gráfico.
* Eventos: Ações específicas executadas por um usuário no aplicativo hello. distribuição de saudação de eventos é mostrada como contagem de saudação de eventos por usuário por sessão. Um evento representa uma ação instantânea, por exemplo, um clique no recebimento de um botão ou saudação de notificação. (significado Olá de eventos depende de como Olá SDK foi integrado no aplicativo hello.) Um evento pode ocorrer durante uma sessão ou um trabalho ou pode ser autônomo.
* Trabalhos: Tooevents semelhantes exceto que eles se concentrar no comprimento de saudação da ação de saudação. Por exemplo, trabalhos poderiam determinar informações técnicas sobre o tempo de conteúdo tooload ou um serviço de chamada de tooweb. Ele também pode mostrar quanto tempo um toofill de usuário um formulário, criar uma conta ou fazer uma compra. Um trabalho representa Olá duração de uma tarefa, por exemplo, a duração de saudação de uma tarefa de download ou Olá uma faixa de tempo é exibido na tela hello. (significado saudação de trabalhos depende de como Olá SDK foi integrado no aplicativo hello.) Trabalhos são geralmente associados a tarefas em segundo plano que são executadas fora do escopo de saudação de uma sessão (ou seja, sem qualquer atividade de usuário).
* Technicals: Obter informações técnicas sobre dispositivos de saudação de usuários de saudação do aplicativo que você pode controlar, como Olá tamanho de localidade, transporte, rede, dispositivo, Firmware e tela de dispositivos dos usuários hello e Olá versão do aplicativo e Olá versão do SDK usado em seu aplicativo.
* Erros de: Informações sobre erros no aplicativo hello técnicas que fazem com que Olá toocrash de aplicativo. Um erro representa um problema instantâneo, por exemplo, uma falha de rede ou uma manipulação incorreta. (significado Olá de eventos depende de como Olá SDK foi integrado no aplicativo hello.) Um erro pode ocorrer durante uma sessão ou um trabalho ou pode ser autônomo.
* Falhas: Informações sobre os erros que causam toocrash seu aplicativo. Uma falha é uma condição inesperada em que o aplicativo hello para executar suas funções esperadas e deve ser interrompido. Uma falha é geralmente devido tooa bug no aplicativo hello.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Acessando Olá visão geral de retenção
![Analytics3][12]

Visão geral de retenção de saudação é dividida em meio Olá em várias placas, cada visão de geral mostrando Olá por um determinado período de retenção. período de retenção de 2 dias Olá é visto no exemplo hello. Olá outros cartões Mostrar Olá 4-dia e os períodos de retenção de 7 dias.

## <a name="understanding-hello-retention-overview-cards"></a>Noções básicas sobre cartões de visão geral de retenção de saudação
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Cada cartão é composto de 3 partes principais:
1. 1: cohort hello e período de saudação considerados
2. 2-4: Olá retenção para Olá período atual
3. 5: um minigráfico de histórico de saudação

### <a name="here-is-detailed-information-about-each-element"></a>Aqui há informações detalhadas sobre cada elemento:
1. Cohort e período: esse título fornece o tipo de saudação de cohort. Aqui "período de 2 dias" significa que, veremos comportamento Olá de usuários em dois dias, os usuários que chegaram durante um período de 2 dias e se eles se conectam em Olá blocos de 2 dias a seguir. exemplo Hello acima considera a atividade de saudação de usuários entre hello 21 e 22 de novembro.
2. Isso retorna a taxa de retenção de Olá sobre Olá 21 e 22 de novembro para usuários de saudação que chegam em 19 e 20 de novembro. Aqui que tivemos 1 usuário ativo entre Olá 21 e 22, sobre Olá 3 que eram novos usuários entre Olá dia 19 e 20.
3. Saudação de fornece esse indicador visual informações mesmo que acima representadas graficamente. (Olá terceiro de saudação círculo é de número de 33% hello.) cor de saudação fornece informações adicionais: verde indica que esse número está aumentando de cálculo de saudação anterior. Amarelo significa estável e vermelho significa redução.
4. Isso indica valores hello usados para cálculo de saudação.
5. Este é um minigráfico de histórico de saudação de valores de retenção de saudação. Ele permite valores de saudação toosee em Olá após toohave uma visão geral de como surgiu.

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
