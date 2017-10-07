---
title: aaaOverview do Azure Application Insights para DevOps | Microsoft Docs
description: Saiba como toouse Application Insights em um ambiente de desenvolvimento Ops.
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Visão geral do Application Insights para DevOps

Ajuda do [Application Insights ](app-insights-overview.md), você pode encontrar rapidamente qual é o desempenho do seu aplicativo e como está sendo usado quando ele estiver ativo. Se houver um problema, ele permite que você sobre ele, ajuda a avaliar o impacto de saudação e ajuda a determinar a causa de saudação.

Aqui está uma conta de uma equipe que desenvolve aplicativos da Web:

* *"Alguns dias atrás, implantamos um hotfix “secundário”. Não foi executada uma passagem de teste amplo, mas infelizmente alguma alteração inesperada foi mesclada com carga Olá, causando a incompatibilidade entre o início hello e back-end. Imediatamente, exceções de servidor surged, nosso alerta acionado, e foram feitas atento a situação de saudação. Alguns cliques no portal do Application Insights hello, nós temos informações suficientes de exceção pilhas toonarrow problema hello. É revertida imediatamente e Olá danos limitados. Application Insights fez essa parte da saudação devops ciclo muito fácil e acionáveis."*

Neste artigo, execute um agrupamento do banco da Fabrikam que desenvolve Olá bancários toosee do sistema (OBS) como usam online Application Insights tooquickly responder toocustomers e faça as atualizações.  

equipe de saudação funciona em um ciclo de DevOps descrito nos Olá ilustração a seguir:

![Ciclo do DevOps](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Requisitos de feed em sua lista de pendências de desenvolvimento (lista de tarefas). Em resumo, eles funcionam sprints, que geralmente oferecem software trabalho - geralmente na forma de saudação de aprimoramentos e extensões toohello de aplicativo existente. aplicativo Hello em tempo real é frequentemente atualizado com novos recursos. Enquanto ele está ativo, equipe Olá monitora-lo para uso com a Ajuda de saudação do Application Insights e desempenho. Esses dados do APM voltam para sua lista de pendências de desenvolvimento.

equipe de saudação usa o aplicativo web em tempo real do Application Insights toomonitor hello atentamente para:

* Desempenho. Quiserem toounderstand como os tempos de resposta variam de acordo com a contagem de solicitação; quanto CPU, rede, disco e outros recursos estão sendo usados; e onde estão os gargalos de saudação.
* Falhas. Se houver exceções solicitações com falha ou se um contador de desempenho ficar fora de seu intervalo confortável, Olá equipe necessidades tooknow rapidamente para que eles podem levar a ação.
* Uso. Sempre que um novo recurso for liberado, equipe Olá deseja tooknow toowhat extensão é usado, e se os usuários têm dificuldade com ele.

Vamos nos concentrar em parte de comentários de saudação do ciclo de saudação:

![Detectar-Realizar a triagem-Diagnosticar](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Detectar baixa disponibilidade
Marcela Markova é um desenvolvedor sênior da equipe OBS hello e leva lead Olá sobre o monitoramento de desempenho on-line. Ela define vários [testes de disponibilidade](app-insights-monitor-web-app-availability.md):

* Um teste de URL única para a página principal de saudação para o aplicativo hello, http://fabrikambank.com/onlinebanking/. Ela define os critérios de código HTTP 200 e o texto “Bem-vindo!”. Se esse teste falhar, há algo errado seriamente com rede hello ou servidores de hello ou pode ser um problema de implantação. (Ou alguém alterou Olá bem-vindo! mensagem na página de saudação sem deixar seu sabe).
* Um teste de várias etapas mais aprofundado, que faz logon e obtém uma listagem atual das contas, verificando alguns detalhes principais em cada página. Esse teste verifica que esse banco de dados de contas do hello link toohello está funcionando. Ela usa uma ID do cliente fictícia: algumas delas são mantidas para fins de teste.

Com esses testes, configuradas, Marcela é seguro que essa equipe Olá saibam rapidamente sobre qualquer interrupção.  

Falhas aparecem como vermelhos pontos no gráfico de teste da web hello:

![Exibição de testes da web que foram executados pela Olá que precedem o período](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Mas é mais importante, um alerta sobre qualquer falha é enviado por email toohello equipe de desenvolvimento. Dessa forma, eles sabem sobre ele para que quase todos os clientes de hello.

## <a name="monitor-performance"></a>Monitorar o desempenho
Página de visão geral de saudação do Application Insights, há um gráfico que mostra uma variedade de [chave métricas](app-insights-web-monitor-performance.md).

![Métricas diversas](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

O tempo de carregamento de página do navegador é derivado da telemetria enviada diretamente a partir de páginas da Web. Tempo de resposta do servidor, contagem de solicitação do servidor e contagem de solicitação com falha são todos medidos no servidor de web hello e enviados tooApplication Insights de lá.

Marcela é um pouco preocupado com gráfico de resposta do servidor de saudação. Este gráfico mostra o tempo médio de saudação entre quando o servidor de saudação recebe uma solicitação HTTP de navegador do usuário, e quando ele retorna a resposta de saudação. Não é incomum toosee uma variação neste gráfico, como a carga no sistema Olá varia. Mas, nesse caso, há uma correlação entre pequeno sobe Olá contagem de solicitações e grande de toobe aumenta no tempo de resposta de saudação. Que pode indicar que o sistema de saudação estiver funcionando em seus limites.

Ela abre os gráficos de servidores hello:

![Métricas diversas](./media/app-insights-detect-triage-diagnose/06.png)

Parece toobe sem sinal de limitação de recursos, portanto, talvez Olá impactos em gráficos de resposta do servidor de saudação são apenas uma coincidência.

## <a name="set-alerts-toomeet-goals"></a>Definir alertas toomeet metas
No entanto, ela gostaria tookeep olho nos tempos de resposta de saudação. Se eles forem muito altos, ela deseja tooknow sobre ele imediatamente.

Portanto, ela define um [alerta](app-insights-metrics-explorer.md) para tempos de resposta maiores do que um limite típico. Isso lhe dá a certeza de que será informada sobre isso caso os tempos de resposta sejam lentos.

![Folha Adicionar alerta](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Alertas podem ser definidos em uma grande variedade de outras métricas. Por exemplo, você pode receber emails se a contagem de exceção Olá torna-se alta, ou a memória disponível Olá fica baixa, ou se houver um pico em solicitações de cliente.

## <a name="stay-informed-with-smart-detection-alerts"></a>Mantenha-se informado com Alertas de detecção inteligente
No dia seguinte, chega um email de alerta do Application Insights. Mas quando ela abri-la, ela localiza não é alerta de tempo de resposta de saudação que ela está definida. Em vez disso, ele informa que houve um aumento repentino de solicitações com falha – ou seja, solicitações que retornaram códigos de falha de 500 ou mais.

Solicitações com falha são onde os usuários viu o erro - geral após uma exceção gerada no código de saudação. Talvez eles recebam uma mensagem informando “Desculpe, não foi possível atualizar os detalhes no momento”. Ou, no pior inconveniente absoluto, um despejo da pilha aparece na tela do usuário hello, pela agência de servidor de web hello.

Este alerta é uma surpresa, porque a última vez em que ela visto, hello hello falhou solicitação contagem foi Felizmente baixa. Um pequeno número de falhas é toobe esperado em um servidor ocupado.

Ele também foi um pouco de surpresa para ela porque ela não tinha tooconfigure este alerta. Application Insights inclui Detecção Inteligente. Ajusta automaticamente o padrão comum de falha do aplicativo tooyour e falhas "é usado para" em uma página específica ou sob alta carga ou métricas tooother vinculado. Ele gera o alarme Olá somente se houver um aumento acima que vem tooexpect.

![email de diagnóstico proativo](./media/app-insights-detect-triage-diagnose/21.png)

Este é um email muito útil. Ele não apenas aciona um alarme. Ele faz muita triagem hello e trabalho de diagnóstico, muito.

Mostra quantos clientes foram afetados e em quais páginas da Web ou operações. Marcela pode decidir se precisa tooget Olá toda a equipe trabalhando nisso como um incêndio, ou se ele pode ser ignorado até a próxima semana.

email Olá também mostra que ocorreu uma exceção específica e - ainda mais interessante - essa falha hello está associada ao banco de dados específico do tooa chamadas com falha. Isso explica por que falhas de saudação apareceram, de repente, mesmo que a equipe do Marcela recentemente não implantou as atualizações.

Líder de saudação Marcella pings de Olá equipe de banco de dados com base neste email. Ela descobre que eles liberado um hot fix Olá última meia hora; e Opa, talvez tenha sido uma alteração de esquema secundário...

Assim o problema de saudação está no toobeing de maneira Olá corrigido, mesmo antes de analisar logs e dentro de 15 minutos depois de ele decorrentes. No entanto, Marcela clica Olá link tooopen Application Insights. Ele é aberto para uma solicitação com falha e ele pode ver o banco de dados com falha chamar na lista de associados de saudação de chamadas de dependência.

![solicitação com falha](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Detectar exceções
Com um pouco de instalação, [exceções](app-insights-asp-net-exceptions.md) são relatado tooApplication Insights automaticamente. Eles podem também ser capturados explicitamente inserindo chamadas muito[trackexception ()](app-insights-api-custom-events-metrics.md#trackexception) em código hello:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


equipe do banco da Fabrikam Olá evoluiu prática Olá sempre enviar telemetria em uma exceção, a menos que haja uma recuperação óbvia.  

Na verdade, é ainda mais ampla do que a sua estratégia: enviam telemetria em cada caso em que o cliente Olá é frustrado o que quisessem toodo, se ele corresponde tooan exceção no código hello, ou não. Por exemplo, se sistema de transferência entre banco externa Olá retornará uma mensagem "não é possível concluir esta transação" por algum motivo operacional (nenhuma falha do cliente de saudação), em seguida, controlam se o evento.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException é exceções tooreport usado porque ele envia uma cópia da pilha de saudação. TrackEvent é tooreport usado outros eventos. Você pode anexar as propriedades que podem ser úteis no diagnóstico.

Exceções e eventos aparecem no hello [pesquisa diagnóstico](app-insights-diagnostic-search.md) folha. É possível analisá-los propriedades adicionais do toosee hello e rastreamento de pilha.

![Na pesquisa de diagnóstico, use filtros tooshow determinados tipos de dados](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Monitorar proativamente
Marcela não fica apenas sentada esperando por alertas. Logo após cada nova implantação, ela usa uma olhada em [tempos de resposta](app-insights-web-monitor-performance.md) - ambos Olá Figura geral e contagens de tabela de saudação de solicitações mais lentas, bem como a exceção.  

![Gráfico de tempo de resposta e uma grade dos tempos de resposta do servidor.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Ela pode avaliar o efeito de desempenho de saudação de cada implantação, normalmente comparando cada semana com hello última. Se houver uma queda repentina worsening, ela gera que com desenvolvedores de saudação relevantes.

## <a name="triage-issues"></a>Problemas de triagem
Triagem - avaliar severidade hello e a extensão de um problema - é Olá primeira etapa após a detecção. Deve chamamos out equipe saudação à meia-noite? Ou pode ser deixado até que o intervalo de conveniente Avançar Olá na lista de pendências Olá? Há algumas perguntas cruciais na triagem.

Frequência está acontecendo? gráficos de saudação na folha de visão geral de saudação dar algum problema de tooa de perspectiva. Por exemplo, Olá Fabrikam aplicativo gerado alertas de teste da web quatro uma noite. Observando o gráfico de saudação manhã Olá, equipe Olá pode ver que foram realmente alguns pontos vermelhos, embora ainda grande parte dos testes de saudação verde. O detalhamento de gráfico de disponibilidade hello, ficou claro que todos esses problemas intermitentes foram de local de um teste. Isso, obviamente, foi um problema de rede que afetou somente uma rota e provavelmente se resolveria sozinho.  

Por outro lado, um aumento significativo e estável no gráfico de saudação de contagens de exceção ou tempos de resposta é obviamente algo toopanic sobre.

Uma tática de triagem útil é “Experimente você mesmo”. Se você tiver Olá mesmo problema, você sabe que é real.

Que fração de usuários são afetados? tooobtain uma resposta aproximada, divida a taxa de falha de Olá por contagem de sessões de saudação.

![Gráficos de sessões e solicitações com falha](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Quando há respostas lentas, compare tabela Olá de solicitações mais lentas responder com frequência de uso de saudação de cada página.

Qual é a importância cenário Olá bloqueada? Se esse for um problema funcional bloqueando uma história de usuário específica, isso importa muito? Se os clientes não podem pagar suas contas, isso é sério; se eles não podem alterar suas preferências de cor da tela, talvez isso possa esperar. Olá detalhes do evento hello ou exceção, ou a identidade de saudação do página lento Olá, informa onde os clientes estão tendo problemas.

## <a name="diagnose-issues"></a>Diagnosticar problemas
Diagnóstico não está bem Olá igual a depuração. Antes de iniciar o rastreamento através do código hello, você deve ter uma ideia do motivo, onde e quando o problema de saudação está ocorrendo.

**Quando isso acontece?**  exibição histórica do hello fornecida pelo gráficos de evento e métrica Olá torna efeitos toocorrelate fácil com as possíveis causas. Se houver picos intermitentes em taxas de exceção ou tempo de resposta, examinar a contagem de solicitações de saudação: se ele culmina no hello mesmo tempo, em seguida, ele se parece com um problema de recurso. Você precisa tooassign mais CPU ou memória? Ou é uma dependência que não é possível gerenciar a carga Olá?

**O problema é conosco?**  Se você tiver uma queda repentina no desempenho de um tipo específico de solicitação - por exemplo quando Olá cliente desejar um extrato - é possível pode ser um subsistema externo em vez de seu aplicativo web. No Metrics Explorer, selecione a taxa de falha de dependência hello e taxas de duração de dependência e comparar seus históricos sobre Olá após algumas horas ou dias com problema Olá detectadas. Se há são correlacionar as alterações, um subsistema externo pode ser tooblame.  

![Gráficos de falha de dependência e a duração de chamadas toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Alguns problemas de dependência de lentidão são problemas de localização geográfica. O Fabrikam Bank usa máquinas virtuais do Azure, e descobriu que eles tinham inadvertidamente localizado seu servidor Web e servidor de conta em diferentes países. Obtiveram uma melhoria expressiva migrando um deles.

**O que fizemos?** Se o problema de saudação não aparece toobe em uma dependência, e se sempre não, provavelmente é causado por uma alteração recente. Olá perspectiva histórica fornecida pelo gráficos de métricas e eventos de saudação torna fácil toocorrelate alterações repentinas com implantações. Que restringe a pesquisa Olá para problema de saudação.

**O que está acontecendo?** Alguns problemas ocorrem raramente e podem ser difícil tootrack para baixo testando offline. Tudo o que podemos fazer é bug de saudação do tootry toocapture quando ela ocorre ao vivo. Você pode inspecionar Olá despejos de pilha em relatórios de exceção. Além disso, é possível escrever chamadas de rastreamento, com sua estrutura de registros favorita ou com TrackTrace() ou TrackEvent().  

A Fabrikam tinha um problema intermitente com transferências entre contas, mas apenas com determinados tipos de conta. toounderstand melhor o que estava acontecendo, eles inseridos tracktrace () chama nos pontos-chave no código hello, anexando Olá o tipo de conta como uma chamada de tooeach de propriedade. Que tornou fácil toofilter out apenas os rastreamentos em busca de diagnóstico. Eles também anexados valores de parâmetro como chamadas de rastreamento toohello propriedades e medidas.

## <a name="respond-toodiscovered-issues"></a>Responder a problemas de toodiscovered
Depois que você tenha diagnosticado problema hello, você pode fazer um plano toofix-lo. Talvez você precisa tooroll fazer uma alteração recente, ou talvez você pode prosseguir e corrigi-lo. Depois de corrigir Olá, o Application Insights informa se você teve êxito.  

Equipe de desenvolvimento do banco da Fabrikam tomar uma medida tooperformance abordagem mais estruturada costumavam toobefore usavam Application Insights.

* Eles definir metas de desempenho em termos de medidas específicas na página de visão geral do Application Insights hello.
* Projetar medidas de desempenho no aplicativo hello a partir do início do hello, como as métricas de saudação medir o progresso de usuário por meio de 'funis'.  


## <a name="monitor-user-activity"></a>Monitorar as atividades do usuário
Quando o tempo de resposta é bom e há algumas exceções, equipe de desenvolvimento Olá pode passar toousability. Eles podem pensar em como tooimprove Olá experiência dos usuários e como tooencourage hello mais de tooachieve usuários desejado metas.

Informações do aplicativo também podem ser usado toolearn fazem o que os usuários com um aplicativo. Depois que ele é executado sem problemas, equipe Olá que tooknow quais recursos estão hello mais popular, o que os usuários como ou tem dificuldades com e a frequência na qual elas retornam. Isso os ajudará a definir as prioridades para seus futuros trabalhos. E possa planejar de sucesso de saudação toomeasure de cada recurso como parte do ciclo de desenvolvimento de saudação. 

Por exemplo, uma viagem típica do usuário por meio do site da web hello tem um "funil" claro. Muitos clientes examinar as taxas de saudação de diferentes tipos de empréstimo. Um número menor vá toofill no formulário de cotação hello. Aqueles que recebem uma cotação, alguns vá em frente e retire empréstimo hello.

![Contagens de exibição de página](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Considerando onde diminuir Olá números de maiores de clientes, negócios Olá podem descobrir como tooget mais usuários por meio da parte inferior do toohello da saudação funil. Em alguns casos, pode haver uma falha do usuário (UX) de experiência - por exemplo, botão 'Próximo' hello é toofind rígido ou instruções de saudação não óbvias. Provavelmente, há mais significativos motivos dos negócios para transferências de soltar: talvez forem muito altas taxas de empréstimo hello.

Qualquer motivos Olá, Olá dados ajudam a equipe de saudação descobrir o que os usuários estão fazendo. Mais controle de chamadas podem ser inserido toowork mais detalhes. Trackevent pode ser usado toocount quaisquer ações do usuário, de muitos detalhes Olá de cliques de botão individual, conquistas toosignificant como pagar um empréstimo.

equipe de saudação está ficando usado toohaving informações sobre a atividade de usuário. Hoje em dia, sempre que criam um novo recurso, eles pensam como irão receber comentários sobre seu uso. Eles chama o controle de recurso de saudação do início da saudação de design. Eles usam o recurso de Olá Olá comentários tooimprove em cada ciclo de desenvolvimento.

[Leia mais sobre o uso de controle](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Aplicar o ciclo de DevOps Olá
Isso é como um uso de equipe do Application Insights individuais não apenas toofix problemas, mas tooimprove seu ciclo de vida de desenvolvimento. Espero que isso tenha dado a você algumas ideias sobre como o Application Insights pode lhe ajudar com o gerenciamento do desempenho dos seus próprios aplicativos.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas
Você pode começar de diversas maneiras, dependendo das características de saudação do seu aplicativo. Escolha o que lhe convém:

* [Aplicativo web do ASP.NET](app-insights-asp-net.md)
* [Aplicativo web Java](app-insights-java-get-started.md)
* [Aplicativo web do Node.js](app-insights-nodejs.md)
* Aplicativos já implantados, hospedados em [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md) ou [Azure](app-insights-azure.md).
* [Páginas da Web](app-insights-javascript.md) -aplicativo de página única ou página da web comum - use isso em seu próprio ou em tooany de adição de opções de saudação do servidor.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) tootest Olá de seu aplicativo de internet pública.
