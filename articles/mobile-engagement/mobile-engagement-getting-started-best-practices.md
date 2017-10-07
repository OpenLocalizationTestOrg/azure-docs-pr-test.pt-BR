---
title: "aaaAzure Mobile Engagement guia de Introdução com as práticas recomendadas"
description: "Guia de introdução ao Azure Mobile Engagement e práticas recomendadas para a integração"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - Guia de introdução com práticas recomendadas
## <a name="overview"></a>Visão geral
**tela de Hello móvel é um espaço muito cheio:** em 2013, um estudo encontrado dispositivo móvel médio de saudação tinha 27 aplicativos instalados. Os usuários normalmente passam 30 horas por mês em seus aplicativos. A maior parte desse tempo foi passado em redes sociais e em jogos (cerca de 20 horas). Até 2014, Olá mercado Android tinha cerca de 1,5 milhão aplicativos para usuários toochoose de. da loja Apple Olá contidos em torno de 1,2 milhões de aplicativos. O uso de aplicativos móveis não para de aumentar à medida que os desenvolvedores competem nesse mercado em expansão. 

Média do usuário móvel Olá irá instalar e desinstalar aplicativos com alta frequência dependendo da alteração interesses e experiências no aplicativo. No caso de sucesso de saudação toodetermine de ordem de um aplicativo é vital tooknow mais do que apenas quantos usuários instalarem seu aplicativo. É importante tooknow como útil está de seu aplicativo e se essa tendência de uso está alterando. Olá perguntas a seguir tornam-se importantes:

* Os usuários começam toofind seu aplicativo como não interessantes ou obsoleto? 
* Quantos usuários deixaram de usar seu aplicativo? 
* A tendência de compras no aplicativo está aumentando ou diminuindo?
* Os usuários estão toocomplete fluxos de trabalho devido a problemas com o aplicativo hello ou falta de interesse? 
* Foi você manterá o aplicativo relevantes e úteis por push tooyour conteúdo novo usuário base? 
* Esse novo conteúdo seria Olá mesmo para todos os usuários ou se concentrem em segmentos de usuário com base no comportamento em seu aplicativo? 

As respostas tooquestions semelhante toothese pode ajudar a estender a vida hello e receita do seu aplicativo. Elas também podem ajudar você a definir e a manter sua base de usuários. 

Mídia relacionados a aplicativos tendem toohave alguns de retenção mais alta de saudação entre usuários. Uma razão para isso é constantemente estiverem fornecendo toousers conteúdo atualizado. Adoção antecipada de notificações por push útil direcionado tende a segmento de usuário tooa toohave um grande impacto sobre a retenção de aplicativo. 

programa do Azure Mobile Engagement Olá é projetado toohelp estender a vida hello e retenção de seu aplicativo, fornecendo um método toogather e analisar informações detalhadas sobre o uso de saudação do seu aplicativo. Ele ajudará a classificar sua base de usuários de acordo com o toobehavior e criar campanhas de determinados para entregar notificações por push e no aplicativo mensagens tooidentified segmentos de usuário. Os indicadores chave de desempenho (KPIs) medem o nível de atividade dos usuários em diferentes aspectos de seu aplicativo. O Azure Mobile Engagement fornece métodos de saudação precisar toodetermine esses KPIs. Ele ajuda a aumentar Olá retorno sobre o investimento (ROI) fornecendo Olá infra-estrutura, você precisa tooincrease contrato com seu aplicativo móvel. 

Olá tooget de ordem mais fora do Azure Mobile Engagement, é necessário toostart com um plano de compromisso bem projetada. Seu plano ajudará você a identificar dados granulares Olá, será necessário toosegment capaz de toobe seu usuário base. Isso pode ter base no comportamento e em experiências no aplicativo. Para sua toobe de plano com êxito, é um tooclearly de prática recomendada definir Olá KPI que mede os objetivos de saudação do seu aplicativo. Com indicadores de desempenho definidos, você pode inserir facilmente lógica necessária Olá em seu aplicativo toocollect bem refinada dados que você irá usar tooanalyze e avaliar os KPIs. Este tópico é um guia de práticas recomendadas para definir KPIs Olá que você usará com seu plano de projeto. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Etapa 1: Definir o modelo de opção KPIs toofit Olá
Definir corretamente os KPIs pode ser toocomplete uma tarefa difícil. Os aplicativos projetados para diversos setores têm suas próprias especificações e objetivos. Isso pode tendem a tooconfuse sua abordagem. toohelp evitar isso, KPIs e objetivos devem ser classificados em três categorias principais: **Business**, **contrato**, e **técnico**. Este é o que chamamos de saudação **modelo opção**.

Um bom plano geralmente terá objetivos Olá KPIs que medem sucessos de saudação em cada Olá categorias de modelo de opção Olá a seguir.

#### <a name="business-kpis"></a>KPIs de Negócios
KPIs da empresa devem ser hello mais fácil parte toobuild. Provavelmente você já os definiu de alguma forma quando planejou seu aplicativo móvel. Esses KPIs normalmente ajudam a medir a receita e o ROI do aplicativo. Olá lista a seguir fornece alguns exemplos de KPIs de negócios que podem ajudá-lo ao definir as indicadores de desempenho:

* KPIs de Negócios de Mídia
  * Número de anúncios clicados
  * Número de visitas à página por usuário
  * Número de assinaturas atuais
* KPIs de Negócios em Jogos
  * Número de compras no aplicativo
  * Receita média por usuário (ARPU)
  * Tempo gasto por sessão
  * Dias jogados e atuais no nível do jogo
* KPIs da Negócios em Comércio Eletrônico
  * Dias de utilização do aplicativo
  * Receita média por usuário (ARPU)
  * Valor médio no carrinho durante o check-out
  * Categoria do produto com mais visualizações e compras
* KPIs de Negócios em Banco e Seguros
  * Número de contas
  * Recursos ativados
  * Páginas de ofertas visitadas
  * Alertas clicados ou ativados       

#### <a name="engagement-kpis"></a>KPIs de Envolvimento
Um KPI de contrato é um contrato de saudação do desempenho indicador toomeasure dos usuários. Tendências nesta área ajudam a determinar a retenção de saudação do seu aplicativo. Aqui estão alguns exemplos de indicadores de desempenho para esse tipo de KPI:

* Usuários ativos no hello últimos 7 dias
* Contagem de usuários inativos do hello últimos 7 dias
* Contagem de usuários que não tenham usado o aplicativo hello em 30 dias  

Alguns fatores externos óbvios podem influenciar os indicadores nessa área. Por exemplo, você pode considerar toobe um dispositivo móvel com um usuário em todos os momentos. Isso pode ou não ser verdadeiro. Um aplicativo de jogos talvez tenha tendência toohave maior uso em torno de feriados quando um jogador pode desempenhar mais ao trabalho ou escola.   

Bem definidas KPIs nessa categoria devem ajudar a medir o relacionamento de saudação entre seu aplicativo e seus clientes.

#### <a name="technical-kpis"></a>KPIs Técnicos
Os indicadores de desempenho nessa categoria ajudarão você a determinar se o seu aplicativo está se comportando corretamente, se está travando ou falhando. Esses indicadores podem medir a integridade de saudação do seu aplicativo e identificar problemas de usabilidade que podem impedir que os usuários usando o aplicativo hello. As informações coletadas para esta categoria também podem conter informações de desempenho que seriam relevantes toomarketing equipes. dados de saudação também podem ser útil para solução de problemas, IT e suporte a equipes toohelp identificar erros não relatados. 

Veja alguns exemplos de KPIs Técnicos:

* Contagem e informações sobre exceções manipuladas ou não manipuladas 
* Carimbo de data e hora do último travamento
* Último botão clicado ou última página visitada
* Uso de memória de aplicativo hello
* Taxa de quadros do aplicativo
* Versão do sistema operacional que Olá aplicativo está em execução no
* Versão do aplicativo

Definir o desempenho do aplicativo esses KPIs toohelp medidas e identificar possíveis bugs. Este indicadores devem ajudar a reduzir o tempo de saudação que precisar toodeliver uma correção para seus clientes. Eles também podem ajudar a definir um segmento de usuários que enfrentou um problema específico. Você pode usar a segmentação toocreate campanhas toodeliver as notificações ao usuário sobre correções disponíveis e potencial toohelp de promoções recuperem satisfação do cliente. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Exercício 1 do guia estratégico: Criar seu painel de KPIs
Depois de definir sua estratégia de marketing, os KPIs deverão apresentar uma visão de cada um dos seus principais objetivos. Eles devem ser os pontos de dados claramente definida que permitirá que você toocollect informações vitais toomonitor o comportamento do seu aplicativo e saudação do usuário final de saudação.

Criar um painel KPI que contém Olá informações abaixo

1. Quais são Olá KPIs para o aplicativo hello?
2. Pontos de dados que será uso toorepresent cada KPI?
3. Onde esses dados estarão localizados para meu aplicativo (ou seja, tela, configurações, sistema...)?
4. Posso executar uma sequência de Envolvimento para este KPI?

Você pode usar o hello **KPI construtor** planilha em nossa [mídia guia estratégico de modelo] [ Media Playbook link] para obter exemplos e orientação.

## <a name="step-2-your-engagement-program"></a>Etapa 2: seu programa de envolvimento
Um ótimo programa de envolvimento móvel deve ser considerado um componente fundamental de seu aplicativo. Isso absolutamente deve incluir um programa de boas-vindo grande que é executado para um usuário durante a saudação primeiros dias de uso do aplicativo. Isso tende a toohave um efeito muito positivo no contrato e retenção de seu aplicativo. Estudos mostram que maioria Olá de parada de usuários usando uma saudação aplicativo primeiros dias após a instalação. Você deseja toostrive toomeet ou excede interesse principal de expectativa de cliente no início, enquanto o usuário Olá ainda se concentra em seu aplicativo. Verifique se que você apresentar o valor da chave hello e benefícios do seu aplicativo tooyour clientes. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Notificações por push são Olá melhor abordagem tooearly os contratos com usuários de dispositivos móveis. No entanto, tome bastante cuidado ao segmentar os usuários para o envio de notificações por push. Isso porque se o usuário sentir que está recebendo spam ou notificações desinteressantes, o impacto poderá ser grave. Em alguns cliques, um usuário pode excluir seu aplicativo nunca tooreturn. usuário Olá deve receber altamente personalizado valor no aplicativo em vez de spam genérico.

Depois que os usuários ativamente envolvidos, o programa do contrato pode ajudar unidade outros aspectos do aplicativo hello.

Por exemplo, você pode configurar uma campanha que solicita a seu usuários ativos toorate seu aplicativo. Como este segmento de usuário é hello mais ativo e tem hello mais experiência com o aplicativo, você esperaria-los toogive Olá classificação mais precisa. Depois que você tiver uma classificação alta de aplicativo, pode ajudar a aumentar download orgânicos de saudação do seu aplicativo também reduz os custos de aquisição novo cliente.

#### <a name="engagement-sequence"></a>Sequência de envolvimento
Um programa de envolvimento global inclui sequências de envolvimento diferentes. Cada sequência visa tooreach vários objetivos.

###### <a name="life-push-sequence"></a>Sequência de envio por push durante a vida útil
objetivos Olá para uma sequência de envio de vida são diferentes dependendo do ciclo de vida de saudação de envolvimento do usuário Olá com aplicativo hello. Um usuário específico pode ser novo, inativo ou muito ativo. Em diferentes estágios do ciclo de vida de um contrato, usuários podem aproveitar o conteúdo atualizado na forma de saudação de toodocumentation dicas ou links. 

Por exemplo um novo usuário pode precisar ajuda obtendo tooan orientado por aplicativo ou se beneficiar de um novo usuário incentivos semelhantes toohello após Olá a primeira vez que iniciar aplicativo hello...

*"Toohave feliz sua integração! Lembre-se de toologin tooget seu mês 1º livre! "*

###### <a name="behavioral-push-sequence"></a>Sequência de envio por push comportamental
sequência de push comportamentais Olá visa uso tooincrease com base no comportamento do usuário coletado para o aplicativo hello.  

Por exemplo, um usuário muito ativo de um aplicativo de futebol fantasia pode se beneficiar de sendo envolvido com hello notificação por push a seguir...

*"Julio, você é um verdadeiro fã de futebol! Faça logon na seção de NFL tooour e ganhar acesso livre toohello SuperBowl!"*

###### <a name="alerting-push-sequence"></a>Sequência de envio por push de alerta
Os usuários apreciarão notícias relevantes focadas em seus interesses. Uma sequência de envio por push de alerta melhora o envolvimento enviando alertas baseados nos interesses claramente demonstrados de um usuário. Isso pode ser explícito quando um usuário seleciona seus próprios interesses no aplicativo hello. Ele também foi possível determinar implicitamente com base nos dados coletados durante a interação do usuário com o aplicativo hello.

Por exemplo, o usuário Olá de um aplicativo de comércio eletrônico regularmente pode comprar uma marca específica de café que você capturou um KPI de negócios. Olá alerta a seguir pode melhorar o envolvimento do usuário com o aplicativo hello.

*"Oi Wes, um dos seus favoritas marcas de café será em 25% de venda off Olá primeira semana de setembro de 2015. Agradecemos como um cliente e quisesse toomake-se de que você estava ciente."*

###### <a name="rentention-push-sequence"></a>Sequência de envio por push de retenção
Essa sequência tem como objetivo tooretain usuários que usando um toohelp de campanhas de notificação por push repetitivas unidade o hábito regular de interação com o aplicativo hello. Isso pode ajudar a aumentar a retenção de aplicativo se o usuário Olá gosta de interações de saudação. 

Por exemplo, o usuário de saudação de um aplicativo de esportes relacionados pode receber Olá notificação por push semanal com base em equipes de favoritos do usuário Olá a seguir:

*"Para uma chance toowin 200 pontos, vá voto se Olá Yankees de Nova York win seu jogo nesta semana contra Toronto azul Jays!"*

#### <a name="hello-3w-approach"></a>abordagem de 3W Olá
Dominar sequências de envio por push diferentes Olá ajudará você a se comunicar com os usuários finais. No entanto, você ainda precisa de toouse Olá 3W abordagem para personalizar as notificações. Olá abordagem 3W devem ser abordados quem, o que e quando cada notificação. Se você responder claramente essas perguntas, suas notificações estarão apropriadamente focadas no envolvimento.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Quem: Olá segmento do usuário que receberá as mensagens
Os usuários tooyour de notificações de envio por push deve ser considerado um canal de comunicação muito sensíveis. Certifique-se de notificações de saudação que visar o segmento de usuário tooa toosend são interesses toohello bem no escopo do segmento do usuário. Uma notificação de roteados incorretamente é muito provável que toohave um efeito negativo em um usuário. Ele podem ser spam à esquerda tooyour aplicativo que está sendo desinstalado. 

Use uma combinação de critérios técnicos e comportamentais específicos ao definir os segmentos de usuários que receberão as notificações. Um exemplo simples de definir um segmento de usuário pode ser semelhante toohello instrução a seguir:

"Todos os usuários que iniciou Olá um aplicativo móvel para hello a primeira vez que 3 dias atrás e visitaram a página de logon Olá duas vezes sem realmente concluí-um logon".

Essa instrução ajuda a identificar dados Olá você precisaria toocollect toosupport um cenário específico.

###### <a name="what-hello-message-that-you-will-send"></a>O que: mensagem de saudação do envio
**Tom**

Use, em seus envolvimentos, um tom apropriado para seus usuários segmentados. Isso é definitivamente tooconnect uma boa maneira com que os usuários finais e promover o interesse de um usuário em seu aplicativo. 

**Redirecionamento**

Uma notificação por push pode ser usada para abrir mais de aplicativo hello. Se hello mensagem de notificação fornece um contexto como notícias difusão ou uma promoção de produto, esse link profundo de maio de notificação diretamente toohello direita conteúdo em um aplicativo hello. toosupport isso, você deve criar uma URL de aplicativo do esquema toolet hello gerenciar o redirecionamento de saudação. Ao trabalhar em suas sequências de envolvimento, essa é uma etapa importante que não deve ser negligenciada.

O redirecionamento também pode ser gerenciado para outros sistemas. Por exemplo, com uma URL de ação é possível tooredirect os usuários finais toomany outros sistemas incluindo Olá seguinte:

* Um site
* Uma caixa de correio com um email já configurado
* Uma caixa de SMS
* Um serviço de discagem
* Diretamente toohello loja de aplicativos para o aplicativo hello de classificação. 

Isso fornece muitas oportunidades tooengage os usuários finais e criar regras automáticas tooimprove desempenhos.

**Formato/conteúdo**

Tipos e formatos diferentes de notificação por push:

1. **Anúncios** : permite que você toosend publicidade mensagens toousers em momentos diferentes (fora do aplicativo, no aplicativo ou a qualquer momento).
2. **Pesquisas** : habilitado toogather informações dos usuários finais, fazendo perguntas eles. As respostas estão disponíveis, em seguida, ao criar critérios tootarget os usuários finais.
3. **Envios de dados** : permite que você toosend um binário ou base64 dados arquivo tooupdate Olá aplicativo. informações de saudação contidas em um envio de dados são enviadas tooyour aplicativo toopersonalize Olá experiência dos usuários em seu aplicativo. Seu aplicativo precisa de dados de saudação toosupport toobe projetado em um envio de dados.
4. **Lado a lado (somente no Windows Phone)** : permitia toouse Olá serviço de notificação por Push da Microsoft (MPNS) toosend notificação por Push nativa que contém dados XML (com suporte desde a versão 0.9.0 do SDK. a carga final Olá para blocos não pode exceder 32 quilobytes.). mensagem de saudação aparece diretamente no bloco do quadro.
5. **Modo de exibição da Web** : um modo de exibição da Web é um pop-up com conteúdo da Web. Essa janela pop-up aparece quando o usuário final de saudação clicou na notificação de push hello. Uma exibição da web permite que você toohave mais interação com o usuário final de saudação.

> [!NOTE]
> Certifique-se de que conteúdo Olá que estiver enviando como notificações por push está em conformidade com plataforma respectivo da saudação (iOS, Android, Windows) diretrizes de desenvolvimento de aplicativos e enviar notificações por push.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Quando: tempo de sua campanha de hello
Quando é Olá melhor tempo tooactivate uma campanha disparando notificações por push? Isso deve ser manual ou automático? Deve ser recorrente? Determinando momento certo hello ou a frequência é essencial tooengage aos usuários obter os melhores resultados hello. Para cada sequência de contrato e o cenário, você deve especificar quando será Olá melhor tempo toosend notificações por push. Aqui estão alguns exemplos possíveis:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Se você estiver enviando muitas notificações por dia, pense seriamente se os usuários estão considerando suas comunicações como spam. 

O Azure Mobile Engagement fornece duas maneiras toohelp evitar suas comunicações sendo consideradas como spam. Primeiro, use refinadas segmentação tooensure fazer Olá de destino não mesmos usuários. Além disso, o Azure Mobile Engagement fornece um recurso de "cota". Esse recurso pode limitar as notificações enviadas para uma campanha. Por exemplo, definir um too5 de cota padrão por semana garantirá que um usuário incluído como parte do segmento de usuário de campanha Olá recebe notificações não mais de 5 nessa semana.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Exercício 2 do guia estratégico: Criar o seu programa de envolvimento
Dedique algum tempo para resumir seus objetivos e definindo campanhas Olá esperado tooplay usando sequências específicas. Certifique-se de que aplicar as notificações do hello 3W abordagem toohello em suas campanhas. 

Saudação de uso **programa do contrato** planilha Olá [mídia guia estratégico modelo] [ Media Playbook link] para obter exemplos e orientações.

## <a name="step-3-app-integration"></a>Etapa 3: integração do aplicativo
#### <a name="create-a-tag-plan"></a>Criar um plano de marca
toointegrate do Azure Mobile Engagement em seu aplicativo, você precisará toocreate um plano de marca. plano de marca de saudação é a base de saudação do projeto de saudação. Ele define a relação de saudação entre Especificações de marketing, fluxo de trabalho de saudação do aplicativo hello e dados de marca real Olá coletados no hello aplicativo toomeasure KPIs. Indica qual analytics será capaz de toosee no portal de saudação. Ele também ajuda a definir segmentos de usuários e enviar tooengage de notificações por push focada seus usuários finais. Uma vez que o plano de marca Olá definido, adicionando Olá toointegrate de código em seu aplicativo é simple usando Olá SDK do Azure Mobile Engagement.

Um plano de marca não deve marcar tudo em um aplicativo. Ele deve incluir apenas os dados de marca que fazem parte de sua estratégia de envolvimento móvel. Provavelmente haverá diferenças entre os aplicativos. Olá [mídia guia estratégico modelo] [ Media Playbook link] fornecido com a Ajuda do Azure Mobile Engagement a você criar um plano de marca com um determinado método. Saudação de uso **marca plano** planilha como um guia toobuilding sua marca de plano.

Ao definir uma seção de marca na planilha hello, ser muito específicas. Isso é muito importante tooavoid confusão. Detalhe cada cenário esperado no qual cada marca será enviada. Inclua nome de saudação de atividade Olá onde cada marca é inserida. Isso deve todas ser incluído na Olá **Informative** parte da planilha de saudação. planilha de planejamento de marca Olá deve ser a referência principal Olá para verificação de teste. 

Em Olá **toocollect dados** seção, sua equipe de desenvolvimento deve localizar tipos de hello, nomes, valores e pares de chave/valor de informações extras necessárias para cada marca que será inserido no aplicativo hello.

É recomendável analisar o plano de marca Olá com todas as equipes associadas ao projeto de saudação. Faça as correções necessárias e confirme se tudo está claro para as equipes de marketing e desenvolvimento.

Olá **declaração de trabalho** planilha pode ser usado toohelp guia todas as pessoas envolvidas no projeto de saudação.

#### <a name="data-types"></a>Tipos de dados
Estes são os tipos comuns de dados com suporte no Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Dispositivos e usuários
O Azure Mobile Engagement identifica os usuários gerando um identificador exclusivo para cada dispositivo. Esse identificador é chamado de identificador de dispositivo hello (ou deviceid). Ele é gerado de forma que todos os aplicativos em execução no mesmo compartilhamento dispositivo Olá mesmo identificador de dispositivo.

###### <a name="sessions-and-activities"></a>Sessões e atividades
Uma sessão é uma instância do aplicativo hello está sendo executado por um usuário. sessão Olá abrange de tempo de saudação usuário Olá inicia o aplicativo hello, até que ela pare.

Uma atividade é um agrupamento lógico de um conjunto de coisas Olá aplicativo pode fazer durante uma sessão. É normalmente uma determinada tela no aplicativo hello, mas pode ser que qualquer coisa definidas pela lógica de saudação do aplicativo hello. No mínimo, você deve marcar cada tela ou atividade para seu aplicativo. Isso permitirá que você toounderstand Olá-caminho de usuário.

###### <a name="events"></a>Eventos
Os eventos são usados tooreport interação do usuário com o aplicativo hello. Podem ser ações instantâneas, como o compartilhamento de conteúdo ou reprodução de um vídeo. Marcação de eventos fornece conjuntos de dados que mostram como os usuários interagem com o aplicativo hello. 

###### <a name="jobs"></a>Trabalhos
Os trabalhos são ações tooreport usado com uma duração. Alguns exemplos incluem:

* Execução de chamadas à API
* Tempo de exibição de anúncios
* Execução de tarefas em segundo plano 
* Duração do processo de compra
* Reprodução de um vídeo

###### <a name="errors"></a>Errors
Os erros são usados tooreport problemas detectados pelo aplicativo hello. Por exemplo, ações incorretas do usuário ou falhas na chamada da API.

###### <a name="application-information"></a>Informações do aplicativo
Informações de aplicativo (App-Info) são usadas tootag dados relacionam a experiência do usuário tooa com um aplicativo. Ela é gerada pela interação do usuário com o aplicativo hello. 

Para uma chave de determinado aplicativo-info, Azure Mobile Engagement só mantém o controle de valor mais recente da saudação (nenhum histórico). Informações do aplicativo revela o status de saudação do seu aplicativo ou seus usuários finais. Por exemplo hello status de logon ou grupo de produto Favoritos do usuário.

###### <a name="crash-data"></a>Dados de falha
Dados coletados automaticamente por falhas de aplicativo hello SDK do Mobile Engagement relatórios não são manipuladas pelo aplicativo hello de falhas. Por exemplo, uma exceção não tratada que ocorrer.

###### <a name="extra-data"></a>Dados extras
Eventos, erros, atividades e eventos podem ser aprimorados com parâmetros. Este é um desenvolvedor pode fornecer como dados específicos de aplicativo hello obter informações adicionais. Isso é importante para a definição de uma segmentação mais refinada. 

Por exemplo, valor de saudação de uma marca de "artigo" permitirá que você toosegment os usuários finais com base em quem exibidos artigo específico. No entanto, talvez isso não seja suficiente. Talvez fosse melhor se essa mesma marca "article" também incluísse informações adicionais, como "news_category" em uma atividade. Isso pode ser útil toodetermine dinamicamente Olá categorias favoritas para o usuário hello. 

Informação extras são reportadas como um par de chave/valor. No exemplo hello para este aplicativo de mídia, Olá extra-info para "news_category" seria valor Olá para aquela categoria. Por exemplo, “sports", "economy" ou "politics".

#### <a name="tag-and-sdk-integration"></a>Marcas e integração do SDK
Para instruções passo a passo para integrar hello SDK do Azure Mobile Engagement em seu aplicativo, siga Olá [contrato SDK integração](mobile-engagement-windows-store-integrate-engagement.md) documentação no site do Azure. Escolha sua plataforma de destino de links de saudação na parte superior de saudação da página.

Recomendamos a criação de projetos para dois aplicativos criados com base no Azure Mobile Engagement. Um para o desenvolvimento e teste de preparação e Olá para preparação de produção. Sua equipe de TI pode promover de teste, preparo tooproduction quando os testes de aceitação do usuário de saudação for bem-sucedida.

#### <a name="user-acceptance-testing-uat"></a>Teste de aceitação do usuário
O Teste de aceitação do usuário envolve a certeza de que tudo está funcionando corretamente. É possível usar fluxos de trabalho para coletar todos os dados necessários com base em seu plano de marca:

* Informações de marcação deve estar em vigor, de acordo com toodocumented conceitos AZME
* Todas as informações necessárias foram coletadas (incluindo os valores Extra info e App info)
* A nomenclatura corresponde tooyout acordo marca de plano
* Nenhuma marca duplicada foi enviada

Teste completamente todos os tipos de saudação do comportamento de notificação que você tenha incorporado em seu aplicativo

* Envios por push de anúncios, pesquisas e dados para fora do aplicativo e dentro do aplicativo
* Modos de exibição de texto/Web
* Atualização de notificação, categorias

#### <a name="setup"></a>Configuração
A configuração do Azure Mobile Engagement é muito simples. Toda a documentação Olá relacionadas a interface do usuário toohello está disponível no site do Azure Mobile Engagement Olá, [como toonavigate Olá a interface do usuário](mobile-engagement-user-interface-home.md).

É recomendável que você comece Configurando funções de saudação à direita e associações de função para usuários de saudação do seu projeto. Isso ajuda você a gerenciar a plataforma de toohello de acesso apropriados para todos os usuários. As funções podem incluir:

* Administradores
* Desenvolvedores
* Visualizadores 

Em seguida:

* Registre seu tootest deviceID em seu próprio dispositivo.
* Ir toohello configurações da sua conta e configure a gráficos de toohave Olá fuso horário e a hora de entrega de notificação definido para seu fuso horário.
* Vá toohello configurações de seu aplicativo e registrar hello "App-info" é necessário tootarget do usuário final ao alcance.

Para obter mais informações sobre como toorun seu primeiro envio campanha de notificação, examine [como tooget iniciado usando e gerenciando envia tooreach os usuários finais de tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusão
Os programas de envolvimento são iterativos, e você deve melhorar os seus continuamente à medida que experimenta o que funciona melhor para seu aplicativo. 

Inicialmente, durante a experiência de desenvolvimento com contrato estratégias não tente toobuild uma estratégia de contrato global inteiro. Adotar uma abordagem passo a passo identificando os KPIs e como tooleverage-los. A estratégia de envolvimento será exclusiva para cada aplicativo.

Depois que você desenvolveu alguma experiência, que você pode considerar adicionar Olá tooyour contrato programas a seguir:

* Acompanhamento: você vai adquirir usuários e provavelmente definirá fontes de coleta de dados. Do Azure mobile Engagement pode ser fontes de coleção de toodata vinculado. Ele permite que você toomonitor o desempenho de cada fonte. Essas informações serão toomaximize interessante seu investimento de aquisição. 
* Teste A/B: essa é uma parte essencial do programa de envolvimento. Cada aplicativo tem suas própria especificações. Com o teste A/B, você pode melhorar seu programa de envolvimento.
* Localização geográfica: essa é uma grande oportunidade para as marcas. Recurso de toothis Obrigado, você pode entrar em lugar certo hello e hora. É recomendável verificar que você coletou dados suficientes comportamento do usuário final antes de iniciar a localização geográfica toouse.
* Envio de dados por push: o envio de dados por push é um envio invisível. O envio de dados por push permite a personalização de seu aplicativo com base no comportamento do usuário final. Por exemplo, se um segmento de usuário geralmente consulta produtos de alta tecnologia, o proprietário do aplicativo hello pode enviar um envio de dados que vai personalizar sua página inicial com o conteúdo de alta tecnologia.

## <a name="next-steps"></a>Próximas etapas
* [Criar uma conta no Azure Mobile Engagement](mobile-engagement-create.md).
* Visite [definir sua estratégia do Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn mais sobre como definir sua estratégia do Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
