---
title: "aaaAzure Interface de usuário do Mobile Engagement - campanha de alcance"
description: "Laern como toocreate e gerenciar campanhas de notificação por push usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Como toocreate e gerenciar campanhas de notificação por push
Você pode usar o hello seção alcance de saudação da interface do usuário toocreate uma nova campanha de Push com uma fórmula complexa, fornecendo todas as informações de saudação necessário toosend uma notificação por push. Olá opções de uma campanha de Push variam ligeiramente, dependendo tipos de campanha Olá quatro: anúncios, votações, envia dados e lado a lado (somente no Windows Phone).

### <a name="option-applies-to"></a>As Opções se Aplicam a:
* Idiomas: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)
* Campanha: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)
* Notificação: anúncios, pesquisas
* Conteúdo: exclusivo para cada tipo de campanha
* Público-alvo: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)
* Período: anúncios, pesquisas, blocos
* Teste: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)

![Reach-Campaign1][20]

## <a name="languages"></a>Linguagens
Você pode usar o hello idiomas lista suspensa menu toosend uma versão diferente do seu toodevices Push definidas toouse diferentes idiomas. Por padrão, todos os dispositivos receberá Olá mesmo Push, independentemente da linguagem em que elas são definidas toouse. Os usuários com idioma diferente do conjunto tooa seu dispositivo receberá a versão de idioma padrão de saudação do hello por Push. Muitas das opções de campanha de push Olá permitem conteúdo alternativo toospecify para cada um dos idiomas adicionais hello, que você selecionar. 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>As diferenças de idioma se aplicam a:
* Idiomas: Idiomas exclusivos podem ser selecionados de linguagem adição toohello padrão
* Campanha: a mesma para todos os idiomas
* Notificação: Exclusivo para cada idioma além toohello idioma padrão
* Conteúdo: Exclusivo para cada idioma além toohello idioma padrão
* Público-alvo: pode ser filtrado por um critério de idioma separado
* Período: o mesmo para todos os idiomas
* Teste: Podem ser enviados a linguagem tooeach por vez

### <a name="supported-languages"></a>Idiomas com suporte:
* Árabe (ar) 
* Búlgaro (bg) 
* Catalão (ca) 
* Chinês (zh) 
* Croata (h) 
* Tcheco (cs) 
* Dinamarquês (da) 
* Holandês (nl) 
* Inglês (en) 
* Finlandês (fi) 
* Francês (fr) 
* Alemão (de) 
* Grego (el) 
* Hebraico (he) 
* Híndi (Olá) 
* Húngaro (hu) 
* Indonésio (id) 
* Italiano (it) 
* Japonês (ja) 
* Coreano (ko) 
* Letão (lv) 
* Lituano (lt) 
* Malaio (macroidioma) (ms) 
* Norueguês Bokmål (nb) 
* Polonês (pl) 
* Português (Portugal) 
* Romeno (ro) 
* Russo (ru) 
* Sérvio (sr) 
* Eslovaco (discos) 
* Esloveno (sl) 
* Espanhol (es) 
* Sueco (sv) 
* Tagalo (NFA) 
* Tailandês (th) 
* Turco (tr) 
* Ucraniano (uk) 
* Vietnamita (vi) 

## <a name="campaign"></a>Campanha
Você pode usar Olá campanha seção tooset Olá nome e a categoria da campanha, bem como se você planejar tooignore seção de público-alvo de saudação de uma campanha de Push e envia essa campanha via API de alcance da saudação (e alguns elementos de nível baixo de saudação API por Push) em vez disso. Categorias podem ser usadas com uma notificação personalizada modelo toocontrol no aplicativo as notificações com base em configurações predefinidas. Você pode obter uma lista existente "categorias" via Olá API de alcance.

> [!WARNING]
> Se você usar a opção de "Ignorar público, push será enviado toousers via API de hello" Olá, na seção de "Da campanha" hello de uma campanha de alcance, campanha de saudação não enviará automaticamente, você precisará toosend-los manualmente por meio de saudação API de alcance.

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>As Opções se Aplicam a:
* Nome: todos
* Categoria: anúncios, pesquisas
* Ignorar o público-alvo, push será enviado toousers via Olá API: todos os

## <a name="notification"></a>Notificação
Você pode usar o hello notificação seção tooset as configurações básicas para seu envio, incluindo: Olá título da saudação Push, mensagem de saudação, uma imagem no aplicativo, ou se ele for dispensáveis. Muitas configurações de notificação são toohello específicas à plataforma do dispositivo. Você pode selecionar se o envio por push será feito “no aplicativo” ou “fora do aplicativo” ou ambos. (Lembre-se de que os usuários podem "aceitar" ou "recusar" de "fora do aplicativo" envia no sistema operacional de saudação nível em seus dispositivos e do Azure Mobile Engagement não poderá ser capaz de toooverride essa configuração. Também Lembre-se de que trata de API de alcance hello "no aplicativo" e "fora do aplicativo" envia. Olá Push API pode ser usado toohandle "fora do aplicativo" leva muito). Envios por push podem ser personalizados com imagens ou conteúdo HTML, incluindo links profundos para vinculação fora de seu local de aplicativo ou tooanother em seu aplicativo (SDK do Android 2.1.0 ou posteriores categorias intenção necessárias). Você pode alterar a notificação de ícone ou iOS hello e enviar o conteúdo da web ou de texto (um pop-up com html, URL link tooanother local de conteúdo dentro ou fora do aplicativo hello). Você também pode fazer o anel de dispositivos com Android ou Vibrar com hello por Push. (Lembre-se de que você será necessário Olá correto permissões SDK em seu Android tooring do arquivo de manifesto ou Vibrar um dispositivo.) Atualmente, não há nenhum padrão no setor para tamanhos de “Foto Grande" do Android, haja visto que os tamanhos das telas são diferentes em cada dispositivo, porém imagens de 400 x 100 funciona bem em quase todos os tamanhos de tela.

### <a name="delivery-types"></a>Tipos de entrega:
* Somente fora do aplicativo: Olá notificação será enviada ao usuário Olá não usa o aplicativo hello.
* Olá sem notificação somente de aplicativo requer um certificado da Apple ou do Google (certificado APNS ou GCM).
* No aplicativo somente: notificação de saudação aparece apenas quando o aplicativo hello está sendo executado.
* notificação de saudação usa Olá Capptain entrega tooreach Olá de usuário do sistema. Totalmente, você pode personalizar layout/exibição Olá visual de seu envio.
* A qualquer momento: Essa opção garante que você enviar uma notificação que o aplicativo hello está em execução ou não.

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>As Opções se Aplicam a:
* Notificação: anúncios, pesquisas

## <a name="content"></a>Conteúdo
Você pode usar o conteúdo de saudação de toomodify Olá seção de conteúdo de anúncios, votações, envia dados e blocos (somente no Windows Phone). configuração de conteúdo de saudação de campanhas de Push é toohello específico de tipo de campanha. 

### <a name="see-also"></a>Consulte também
* [Documentação da Interface do Usuário ‑ Alcance ‑ Enviar conteúdo por push][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>Público-alvo
Você pode usar o hello público seção toodefine uma lista padrão de itens toolimit sua campanha ou limites de sua campanha com base em critérios personalizados. conjunto padrão de saudação de opções tooLimit seu público-alvo permite toopush tooeither novo ou antigo usuários ou somente usuários de envio por push nativo. Você também pode definir um número de saudação toolimit cota de usuários que recebem o envio de saudação. Você pode editar manualmente a expressão hello como sua campanha é filtrado tooinclude um ou mais usuários tootarget de critério. Você pode digitar manualmente uma expressão de público-alvo. Essa expressão deve definir explicitamente uma relação entre a critérios Olá. Um critério é descrito por um identificador que deve começar com uma letra maiúscula e não pode conter espaços. uma relação entre a critérios Olá Olá pode ser descrita usando 'e', 'ou', 'not' operadores, bem como '(',')'. Exemplo: "Critérion1 ou (Critérion1 e não Critérion2)".

> [!NOTE]
> Com um grande público incluído em campanhas, Olá servidor direcionamento do lado do verificação pode ser lento, especialmente se você tentar toostart várias campanhas em Olá mesmo tempo.

* Se possível, só inicie uma campanha por vez.
* No máximo, Olá apenas iniciar quatro campanhas de cada vez.
* Enviar por push apenas usuários ativos tooyour (caixa de seleção "envolver somente usuários que podem ser alcançados usando Push nativo" e "Envolver apenas usuários ativos") para que somente os usuários que ainda têm o aplicativo hello instalado e usá-lo precisará toobe verificado.
  Quando seu público-alvo é definido, você pode usar o hello simular toofind botão out quantos usuários receberão esse envio. Isso será calcula o número de saudação de usuários conhecidos potencialmente direcionados por esse público-alvo (essa é uma estimativa com base em uma amostra aleatória de usuários). Lembre-se de que os usuários que tenham desinstalado o aplicativo hello também fazem parte desse público, mas não podem ser alcançados.

### <a name="see-also"></a>Consulte também
* [Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>Editar expressão
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>A opção para limitar seu público-alvo se aplica a:
* Envolver somente um subconjunto de usuários: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)
* Envolver apenas usuários antigos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)
* Envolver apenas usuários novos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)
* Envolver apenas usuários inativos: anúncios, pesquisas, blocos
* Envolver apenas usuários ativos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)
* Envolver apenas os usuários que podem ser alcançados usando Push Nativo: anúncios, pesquisas

## <a name="time-frame"></a>Período
Você pode usar o hello período seção tooset quando Olá push será enviado ou você pode deixar a campanha de Olá Olá período de tempo em branco toostart imediatamente. Lembre-se de que usar o fuso horário de usuários finais da saudação pode iniciar campanha Olá um dia antes do que esperar para seus usuários finais na Ásia e enviem lotes pequenos de avanços cada vez até que todos os fusos horários no período de tempo de saudação do hello world correspondência definida para sua campanha. Usar o fuso horário Olá dos usuários finais também pode causar atrasos em campanhas porque ele tem tempo de saudação toorequest de telefone de saudação antes de iniciar o envio de saudação.

> [!NOTE]
> Campanhas sem uma data de término podem armazenar localmente em cachês de envios e ainda exibi-los após as suas campanhas completas manualmente. tooavoid esse comportamento, específica de uma hora de término para campanhas.

### <a name="see-also"></a>Consulte também
* [Alcance ‑ Instruções – Agendamento][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>As configurações se aplicam a:
* Período: anúncios, pesquisas, blocos

## <a name="test"></a>Teste
Você pode usar o hello teste seção toosend este dispositivo do push tooyour próprio teste antes de salvar campanha hello. Se você tiver configurado qualquer idiomas personalizados para essa campanha, você pode testar o envio de saudação em cada idioma. Você pode configurar um dispositivo de teste para "Minha Conta".

> [!NOTE]
> Nenhum lado servidor dados são registrados quando você usar o botão de saudação muito "testar" envia, somente os dados serão registrados para campanhas de push real.

### <a name="see-also"></a>Consulte também
* [Documentação da Interface do Usuário ‑ Minha Conta][Link 14]

![Reach-Campaign9][28]

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

