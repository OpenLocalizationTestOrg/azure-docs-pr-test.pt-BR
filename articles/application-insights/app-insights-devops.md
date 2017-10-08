---
title: "monitoramento de desempenho do aplicativo de aaaWeb - informações de aplicativo do Azure | Microsoft Docs"
description: "Como o Application Insights se encaixa no ciclo de devOps Olá"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Diagnósticos detalhados para aplicativos Web e serviços com o Application Insights
## <a name="why-do-i-need-application-insights"></a>Por que eu preciso do Application Insights?
O Application Insights monitora seu aplicativo Web em execução. Ele informa sobre problemas de desempenho e falhas e ajuda você a analisar como os clientes usam seu aplicativo. Ele funciona para aplicativos executados em várias plataformas (ASP.NET, J2EE, Node. js,...) e é hospedado em Olá nuvem ou local. 

![Aspectos de complexidade de saudação do fornecimento de aplicativos web](./media/app-insights-devops/010.png)

É essencial toomonitor um aplicativo moderno enquanto ele está em execução. Mais importante, você deseja toodetect falhas antes da maioria dos clientes. Você também deseja toodiscover e corrige problemas de desempenho que, enquanto não catastrófico, talvez desaceleram ou fazer com que alguns inconveniente tooyour usuários. E quando o sistema de saudação está executando tooyour satisfação, você deseja tooknow quais usuários Olá estão fazendo com que ele: eles estão usando o recurso mais recente Olá? Eles estão tendo êxito com ele?

Aplicativos web modernos são desenvolvidos em um ciclo de fornecimento contínuo: versão de um novo recurso ou melhoria; Observe como ele funciona para usuários de saudação; Planeje o próximo incremento de saudação do desenvolvimento com base em que dados de Conhecimento. Uma parte importante desse ciclo é a fase de observação de saudação. Application Insights fornece Olá ferramentas toomonitor um aplicativo web para uso e desempenho.

aspecto mais importante do Hello desse processo é o diagnóstico e diagnóstico. Se o aplicativo hello falhar, em seguida, negócios é perdido. a função principal saudação de uma estrutura de monitoramento, portanto, é toodetect falhas confiável, notificar você imediatamente e toopresent que Olá informações necessárias toodiagnose problema de saudação. Isso é exatamente o que o Application Insights faz.

### <a name="where-do-bugs-come-from"></a>De onde vêm os bugs?
Falhas em sistemas da web geralmente surgem de problemas de configuração ou interações ruins entre seus vários componentes. Olá primeira tarefa ao lidar com um incidente de site dinâmico, portanto, é tooidentify locus de saudação do problema Olá: qual componente ou a relação é causa Olá?

Alguns de nós, aqueles com cabelos grisalhos, podem se lembrar de uma era mais simples na qual um programa de computador era executado em um computador. os desenvolvedores de saudação seriam testá-lo completamente antes de enviá-los. e ter enviado, seria raramente consulte ou pensar novamente. Olá os usuários teriam tooput com bugs residual Olá por muitos anos. 

Hoje em dia tudo é diferente. Seu aplicativo tem uma grande quantidade de diferentes dispositivos toorun no, e pode ser difícil tooguarantee Olá mesmo comportamento exato em cada um deles. Hospedar aplicativos em nuvem Olá significa que bugs podem ser corrigidos rápido, mas também significa contínua competição e hello expectativa dos novos recursos em intervalos frequentes. 

Nas seguintes condições, hello apenas tookeep de maneira que um controle sólido na contagem de bug de saudação é automatizada de teste de unidade. É impossível ser toomanually novamente teste tudo em cada entrega. Teste de unidade é agora parte comum de saudação do processo de compilação. Ferramentas como Olá Xamarin Test Cloud ajudar fornecendo automatizada de interface do usuário de teste em várias versões de navegador. Esses testes regimes permitem toohope essa taxa de saudação de bugs encontrados dentro de um aplicativo pode ser mantida tooa mínimo.

Os aplicativos Web típicos têm muitos componentes em tempo real. Adição toohello cliente (um aplicativo de navegador ou dispositivo) e o servidor de web hello, há processamento de back-end substancial provavelmente toobe. Talvez Olá back-end é um pipeline de componentes, ou uma coleção menos rígida de partes de colaboração. E muitos deles não estarão sob seu controle, são serviços externos dos quais você depende.

Em configurações como essas, pode ser difícil e uneconomical tootest, ou prevê, cada modo de falha possíveis, diferente de em Olá vive próprio sistema. 

### <a name="questions-"></a>Perguntas...
Algumas perguntas que fazemos quando estamos desenvolvendo um sistema Web:

* Meu aplicativo está falhando? 
* O que aconteceu exatamente? -Se ele uma solicitação com falha, quero tooknow como ele obteve existe. Precisamos de um rastreamento de eventos...
* Meu aplicativo é rápido o suficiente? Quanto tempo leva toorespond tootypical solicitações?
* Saudação de identificador do servidor de saudação pode carregar? Quando a taxa de saudação de solicitações aumentar, o tempo de resposta Olá mantém constante?
* O nível de resposta são meu dependências - Olá APIs REST, bancos de dados e outros componentes que chama meu aplicativo. Em particular, se o sistema Olá estiver lento, é o componente ou estou recebendo respostas lentas de outra pessoa?
* Meu aplicativo está ativo ou inativo? Ele pode ser visto no mundo Olá? Avise-me se ele parar...
* O que é a causa raiz de Olá? Foi falha Olá no meu componente ou uma dependência? É um problema de comunicação?
* Quantos usuários foram afetados? Se tiver mais de um tootackle do problema, que é mais importante do Olá?

## <a name="what-is-application-insights"></a>O que é o Application Insights?
![Fluxo de trabalho básico do Application Insights](./media/app-insights-devops/020.png)

1. Application Insights instrumenta o seu aplicativo e envia telemetria sobre ele enquanto o aplicativo hello está sendo executado. Você pode criar hello SDK do Application Insights em aplicativo hello, ou você pode aplicar instrumentação em tempo de execução. método antigo Hello é mais flexível, como você pode adicionar seus próprios módulos regular de toohello de telemetria.
2. Telemetria de saudação é enviada toohello portal do Application Insights, onde são armazenado e processado. (Embora o Application Insights esteja hospedado no Microsoft Azure, ele pode monitorar quaisquer aplicativos Web, não apenas os do Azure.)
3. Telemetria de saudação é apresentada tooyou na forma de saudação de gráficos e tabelas de eventos.

Há dois tipos principais de telemetria: instâncias agregadas e brutas. 

* Os dados de instância incluem, por exemplo, um relatório de uma solicitação que foi recebida pelo seu aplicativo Web. Você pode encontrar para e inspecione os detalhes de saudação de uma solicitação usando a ferramenta de pesquisa Olá no portal do Application Insights hello. instância Olá poderia incluir dados como quanto tempo seu aplicativo levou toorespond toohello solicitação, bem como Olá URL solicitada, a localização aproximada do cliente hello e outros dados.
* Dados agregados incluem o número de eventos por unidade de tempo, para que você possa comparar taxa de saudação de solicitações com tempos de resposta de saudação. Ele também inclui as médias de métricas, como tempos de resposta de solicitação.

categorias principais de saudação de dados são:

* Solicitações tooyour aplicativo (normalmente solicitações HTTP), com dados na URL, o tempo de resposta e o êxito ou falha.
* Dependências, chamadas REST e SQL feitas pelo seu aplicativo, também com o URI, tempos de resposta e êxito
* Exceções, incluindo os rastreamentos de pilha.
* Dados de exibição de página, que vêm de navegadores Olá dos usuários.
* As métricas, como contadores de desempenho, bem como as métricas que você escreve. 
* Eventos personalizados que você pode usar eventos de negócios tootrack
* Rastreamentos de log usados para depuração.

## <a name="case-study-real-madrid-fc"></a>Estudo de caso: Real Madrid F.C.
Olá serviço web de [sociedade Real de futebol Madri](http://www.realmadrid.com/) serve ventiladores de cerca de 450 milhões em torno de Olá, mundo. Ventiladores acesse-os dois por meio de navegadores da web e Olá aplicativos móveis do sociedade. Os fãs podem não apenas podem reservar ingressos, mas também acessar informações e videoclipes sobre os resultados, jogadores e próximos jogos. Eles podem pesquisar com filtros como os números de gols marcados. Também há mídia de toosocial links. experiência do usuário Olá altamente personalizada e foi projetada como ventiladores de tooengage uma comunicação bidirecional.

Olá solução [é um sistema de serviços e aplicativos no Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). A escalabilidade é um requisito fundamental: o tráfego é variável e pode atingir volumes muito grandes durante e próximo das partidas.

Para o Real Madri, é vital toomonitor Olá desempenho de sistema. Informações de aplicativo do Azure fornece uma visão abrangente todo sistema hello, garantir um nível mais alto e mais confiável do serviço. 

Olá sociedade também obtém uma compreensão detalhada dos ventiladores: onde eles estão (apenas 3% são Espanha), que interesse possuem em players, resultados históricos e futuros jogos e como eles respondem toomatch resultados.

A maioria desses dados de telemetria são coletadas automaticamente sem nenhum código adicionado, que simplificado solução hello e redução da complexidade operacional.  Para o Real Madrid, o Application Insights lida com 3,8 bilhões de pontos de telemetria por mês.

Madri real usa Olá Power BI módulo tooview sua telemetria.

![Exibição do Power BI de telemetria do Application Insights](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Detecção inteligente
O [diagnóstico proativo](app-insights-proactive-diagnostics.md) é um recurso recente. Sem qualquer configuração especial determinada por você, o Application Insights detecta e o alerta automaticamente sobre aumentos incomuns nas taxas de falhas do aplicativo. É inteligente o bastante tooignore um plano de fundo de falhas ocasionais e também aumenta é simplesmente proporcional tooa aumento nas solicitações. Por exemplo, se houver uma falha em um dos serviços de saudação que depende de você, ou se Olá nova compilação que você acabou de ser implantado não está funcionando tão bem, em seguida, você saberá sobre ele, assim que você examine seu email. (E há webhooks para que você possa disparar outros aplicativos.)

Outro aspecto desse recurso executa uma análise detalhada diária da sua telemetria, procurando padrões incomuns de desempenho que são toodiscover de disco rígido. Por exemplo, ela pode localizar lentidão no desempenho associada a uma determinada área geográfica ou com a versão de navegador específico.

Em ambos os casos, Olá alerta não apenas informa Olá sintomas for detectado, mas também permite que seus dados, você precisa toohelp diagnosticar Olá problema, como relatórios de exceção relevantes.

![Email do diagnóstico proativo](./media/app-insights-devops/030.png)

O cliente Samtec disse: "Durante uma migração de recurso recente, encontramos um banco de dados subdimensionado que estava atingindo seus limites de recursos e causando tempos limite. Alertas de detecção proativa fornecida por meio de literalmente nós foram separação problema hello, muito quase em tempo real conforme anunciado. Esse alerta juntamente com alertas de plataforma do Azure Olá nos ajudou a quase instantaneamente corrigir o problema de saudação. O tempo de inatividade total foi menor que 10 minutos."

## <a name="live-metrics-stream"></a>Live Metrics Stream
Implantar a compilação mais recente Olá pode ser uma experiência ansiosas. Se houver algum problema, você deseja tooknow sobre eles imediatamente, para que você pode fazer a se necessário. O Live Metrics Stream fornece métricas importantes com uma latência de aproximadamente um segundo.

![Métricas em tempo real](./media/app-insights-devops/040.png)

E permite que você inspecione imediatamente uma amostra de quaisquer falhas ou exceções.

![Eventos de falha em tempo real](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Mapa de aplicativo
Mapa de aplicativos detecta automaticamente a topologia de aplicativo, layout de informações de desempenho de saudação sobre ele, toolet facilmente identificar afunilamentos de desempenho e fluxos de um problema em seu ambiente distribuído. Ele permite que você toodiscover dependências de aplicativo nos serviços do Azure. Você pode triagem problema Olá entender se ele está relacionado ao código ou dependência relacionada e de uma simulação local único no diagnóstico relacionado experiência. Por exemplo, seu aplicativo pode estar falhando devido a degradação de tooperformance na camada SQL. Com o mapa de aplicativo, você pode vê-lo imediatamente e Detalhar a experiência do Supervisor de índice do SQL ou consulta Insights hello.

![Mapa de aplicativo](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Análise do Application Insights
Com a [Análise](app-insights-analytics.md), você pode escrever consultas arbitrárias em uma poderosa linguagem semelhante a SQL.  Diagnosticando na pilha do aplicativo inteiro Olá se torna fácil, como conectar várias perspectivas e solicite Olá perguntas certas toocorrelate o desempenho do serviço com métricas de negócios e experiência do cliente. 

Você pode consultar todos os seus dados brutos da métrica armazenados no portal de saudação e instância de telemetria. linguagem de saudação inclui filtros, junção, agregação e outras operações. Você pode calcular campos e realizar a análise estatística. Há visualizações de tabela e gráficas.

![Gráfico de consulta e os resultados da análise](./media/app-insights-devops/025.png)

Por exemplo, é fácil:

* Solicitação do aplicativo toounderstand de camadas de dados de desempenho por cliente sua experiência de segmento.
* Pesquisar códigos de erro específicos ou nomes de evento personalizados durante investigações do site ativo.
* Fazer drill down em uso do aplicativo hello de clientes específicos toounderstand como os recursos são adquiridos e adotados.
* Controlar sessões e tempos de resposta para operações equipes tooprovide instantânea atendimento e suporte de tooenable de usuários específicos.
* Determine os aplicativos usados com frequência recursos tooanswer recurso priorização perguntas.

Cliente DNN disse: "Application Insights forneceu Olá parte da equação de saudação para ser capaz de toocombine, classificação, consulta e filtrar os dados conforme necessário ausente. Permitindo que nossa equipe toouse seu próprios toofind criatividade e experiência de dados com uma linguagem de consulta avançada tem permitido toofind insights e que ainda não sabíamos que tivemos problemas. Muito interessantes respostas vêm de perguntas Olá começando com *' é por isso if... '.*"

## <a name="development-tools-integration"></a>Integração de ferramentas de desenvolvimento
### <a name="configuring-application-insights"></a>Configurando o Application Insights
Visual Studio e Eclipse tem ferramentas tooconfigure Olá correto SDK pacotes para projeto Olá que você está desenvolvendo. Há um comando de menu tooadd Application Insights.

Se você se deparar toobe usando uma estrutura de log de rastreamento como trace, NLog ou Log4N, em seguida, você obter Olá opção toosend Olá logs tooApplication Insights junto com hello outros telemetria, para que você pode facilmente correlacionar rastreamentos Olá com solicitações , chamadas de dependência e exceções.

### <a name="search-telemetry-in-visual-studio"></a>Pesquisar telemetria no Visual Studio
Ao desenvolver e depurar um recurso, você pode exibir e procurar Olá telemetria diretamente no Visual Studio, usando Olá mesmo pesquisar recursos como no portal da web de saudação.

E, ao Application Insights registra uma exceção, você pode exibir hello ponto de dados no Visual Studio e ir código relevante toohello retas.

![Pesquisa do Visual Studio](./media/app-insights-devops/060.png)

Durante a depuração, você tem telemetria de Olá Olá opção tookeep em sua máquina de desenvolvimento, exibindo-o no Visual Studio, mas sem enviá-la toohello portal. Essa opção local evita a mistura da telemetria de produção com a de depuração.

### <a name="build-annotations"></a>Anotações do build
Se você usar o Visual Studio Team Services toobuild e implanta seu aplicativo, anotações de implantação aparecem nos gráficos no portal de saudação. Se a versão mais recente tiver qualquer efeito nas métricas Olá, é óbvio.

![Anotações do build](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Itens de trabalho
Quando um alerta é gerado, o Application Insights pode criar automaticamente um item de trabalho no seu sistema de controle de trabalho.

## <a name="but-what-about"></a>Mas e...?
* [Privacidade e armazenamento](app-insights-data-retention-privacy.md) : sua telemetria é mantida em servidores seguros do Azure.
* Desempenho - impacto Olá é muito baixo. A telemetria é feita em lotes.
* [Preço](app-insights-pricing.md) - você pode começar a usar gratuitamente e isso continua enquanto estiver no volume baixo.


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas
É fácil começar a usar o Application Insights. Opções de saudação principais são:

* Instrumentar um aplicativo Web já em execução. Isso fornece toda a telemetria Olá desempenho internas. Isso está disponível para [Java](app-insights-java-live.md) e [servidores IIS](app-insights-monitor-performance-live-website-now.md) e também para [aplicativos Web do Azure](app-insights-azure.md).
* Instrumentar seu projeto durante o desenvolvimento. Você pode fazer isso para aplicativos [ASP.NET](app-insights-asp-net.md) ou [Java](app-insights-java-get-started.md), bem como [Node.js](app-insights-nodejs.md) e um host de [outros tipos](app-insights-platforms.md). 
* Instrumentar [qualquer página da Web](app-insights-javascript.md) adicionando um trecho de código curto.

