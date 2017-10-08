---
title: "análise de aaaUsage para aplicativos web com o Azure Application Insights | Documentos da Microsoft"
description: "Compreenda seus usuários e o que eles fazem com seu aplicativo Web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Análise de uso para aplicativos Web com o Application Insights

Quais recursos de seu aplicativo Web são mais populares? Os usuários atingem as metas deles com seu aplicativo? Eles deixam o aplicativo em determinados pontos? E retornam posteriormente?  O [Application Insights do Azure](app-insights-overview.md) ajuda você a ter insights profundos sobre como as pessoas usam seu aplicativo Web. Sempre que atualiza seu aplicativo, você pode avaliar como ele funciona para os usuários. Com esse conhecimento, você pode tomar decisões baseadas em dados sobre os próximos ciclos de desenvolvimento.

## <a name="send-telemetry-from-your-app"></a>Enviar telemetria de seu aplicativo

melhor experiência de saudação é obtida com a instalação do Application Insights no código do servidor de aplicativo e nas páginas da web. componentes de cliente e servidor de saudação do seu aplicativo enviam telemetria back toohello portal do Azure para análise.

1. **Código do servidor:** instalar módulo apropriado do Olá para sua [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [outros](app-insights-platforms.md) aplicativo.

    * *Não quer que o código de servidor tooinstall? Apenas [crie um recurso do Azure Application Insights](app-insights-create-new-resource.md).*

2. **Código de página da Web:** abrir Olá [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para seu aplicativo e, em seguida, abra **Introdução > monitorar e diagnosticar cliente**. 

    ![Copie o script hello para head Olá mestre da página da web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Obtenha telemetria:** executar seu projeto no modo de depuração por alguns minutos e, em seguida, procure os resultados na folha de visão geral de saudação no Application Insights.

    Publicar seu aplicativo toomonitor desempenho do aplicativo e descobrir o que seus usuários estão fazendo com que seu aplicativo.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Incluir a ID de usuário e de sessão em sua telemetria
tootrack usuários ao longo do tempo, Application Insights requer uma maneira tooidentify-los. Eventos de Olá, ferramenta é Olá única ferramenta de uso que não requer uma ID de usuário ou uma ID de sessão.

Comece a enviar essas IDs [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Explore as estatísticas e dados demográficos de uso
Descubra quando as pessoas usam seu aplicativo, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam. 

relatórios de usuários e sessões Olá filtrar seus dados por páginas ou eventos personalizados e segmento-los por propriedades, como local, ambiente e página. Você também pode adicionar seus próprios filtros.

![Usuários](./media/app-insights-usage-overview/users.png)  

Ideias sobre Olá direita destacar padrões interessantes no conjunto de saudação de dados.  

* Olá **usuários** relatório conta os números de saudação de usuários exclusivos que acessam as páginas em seu períodos de tempo escolhido. (Os usuários são contados usando cookies. Se alguém acessar seu site usando computadores cliente ou navegadores diferentes ou limpar os cookies, essa pessoa será contada mais de uma vez.)
* Olá **sessões** relatório conta o número de saudação de sessões de usuário que acessar seu site. Uma sessão é um período de atividade de um usuário, encerrada por um período de inatividade de mais de meia hora.

[Mais sobre as ferramentas de usuários, sessões e eventos Olá](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Visualizações de página

Na folha de uso de saudação, clique nas Olá modos de exibição de página bloco tooget uma análise das páginas mais populares:

![Na folha de visão geral de saudação, clique em Olá gráfico de modos de exibição de página](./media/app-insights-usage-overview/05-games.png)

exemplo Hello acima é de um site de jogos. Gráficos de hello, podemos instantaneamente ver:

* Uso não melhorou em Olá semana passada. Talvez devamos pensar em otimização do mecanismo de pesquisa?
* Tênis é Olá página de jogo mais popular. Vamos nos concentrar na página de toothis melhorias adicionais.
* Em média, os usuários visitam Olá Tênis página cerca de três vezes por semana. (Há cerca de três vezes mais sessões do que usuários.)
* A maioria dos usuários visite o site de saudação durante a semana de trabalho Olá dos Estados Unidos e no horário de trabalho. Talvez, deve fornecer um botão "Ocultar rápida" na página da web de saudação.
* Olá [anotações](app-insights-annotations.md) em gráfico Olá Mostrar quando novas versões do site Olá foram implantadas. Nenhuma das implantações recentes Olá tinha um efeito significativo no uso.

Se quiser que o site de tooyour de tráfego tooinvestigate hello mais detalhadamente, como divisão por uma propriedade personalizada que envia seu site em sua telemetria de exibição de página?

1. Olá abrir **eventos** ferramenta no menu de recurso do Application Insights hello. Essa ferramenta permite analisar quantas exibições de página e eventos personalizados foram enviados de seu aplicativo, com base em uma variedade de opções de filtragem, divisão em coortes e segmentação.
2. No hello "Que usado" suspensa, selecione "Qualquer exibição da página".
3. No menu suspenso de "Divisão por" Olá, selecione uma propriedade pela qual toosplit sua página Exibir telemetria.

## <a name="retention---how-many-users-come-back"></a>Retenção – quantos usuários voltam?

Retenção ajuda a entender a frequência na qual os usuários retornarem toouse seu aplicativo, com base em colaboradores de usuários que executou alguma ação de negócios durante um bucket de tempo determinado. 

- Entender quais recursos específicos com que os usuários toocome back mais do que outras pessoas 
- Forme hipóteses com base em dados de usuários reais 
- Determine se a retenção é um problema para seu produto 

![Retenção](./media/app-insights-usage-overview/retention.png) 

controles de retenção de saudação na parte superior permitem que você toodefine eventos específicos e retenção de toocalculate de intervalo de tempo. gráfico no meio Olá Olá fornece uma representação visual de saudação porcentagem total de retenção por Olá intervalo de tempo especificado. gráfico de saudação inferior Olá representa retenção individual em um determinado período de tempo. Esse nível de detalhe permite que você toounderstand que seus usuários estão fazendo e o que pode afetar usuários retorno em uma granularidade mais detalhada.  

[Mais informações sobre a ferramenta de retenção Olá](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Eventos de negócios personalizados

uma compreensão clara de que os usuários de tooget fazer com o seu aplicativo web, é útil tooinsert linhas de eventos personalizados do código toolog. Esses eventos podem controlar qualquer coisa detalhadas de ações de usuário, como clicar nos botões específicos, eventos de negócios significativa toomore como efetuar uma compra ou vencer um jogo. 

Embora em alguns casos as exibições de página possam representar eventos úteis, de modo geral não é esse o caso. Um usuário pode abrir uma página de produto sem adquirir o produto hello. 

Com eventos de negócios específicos, você pode traçar um gráfico do progresso do dos usuários em seu site. Você pode descobrir as preferências deles com relação a diferentes opções e quando eles desistem ou têm dificuldades. Com esse conhecimento, você pode tomar decisões informadas sobre prioridades Olá na sua lista de pendências de desenvolvimento.

Eventos podem ser registrados na página da web de saudação:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Ou, no lado do servidor de saudação do aplicativo web de saudação:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Você pode anexar eventos de toothese de valores de propriedade, para que você pode filtrar ou dividir eventos hello quando inspecioná-los no portal de saudação. Além disso, um conjunto padrão de propriedades é o evento tooeach anexado, como ID de usuário anônimo, que permite que você tootrace sequência de saudação de atividades de um usuário individual.

Saiba mais sobre [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) e [propriedades](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Fatiar e dividir eventos

Em ferramentas de usuários, sessões e eventos hello, você pode fatiar e nos dados de eventos personalizados pelo usuário, nome do evento e propriedades.
![Usuários](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Telemetria de saudação do design com o aplicativo hello

Quando você estiver criando cada recurso do aplicativo, considere como você vai toomeasure seu sucesso com os usuários. Decida quais eventos de negócios precisa toorecord e código Olá chamadas para esses eventos de rastreamento em seu aplicativo de saudação iniciar.

## <a name="a--b-testing"></a>Testando A | B
Se você não souber qual variante de um recurso será mais bem-sucedida, libere ambas, tornando cada usuários toodifferent acessível. Medir o sucesso de saudação de cada e, em seguida, mova o versão unificada tooa.

Para essa técnica, você deve anexar propriedade distintos valores tooall Olá da telemetria enviada por cada versão do seu aplicativo. Você pode fazer isso definindo propriedades no hello TelemetryContext ativo. Essas propriedades padrão são adicionadas a mensagem de telemetria tooevery Olá aplicativo envia - não apenas a mensagens personalizadas, mas também a telemetria de padrão de saudação.

No portal do Application Insights hello, filtrar e dividir os dados em valores de propriedade hello, assim como versões diferentes do toocompare hello.

toodo, [configurar um inicializador de telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

Inicializador de aplicativo da web de hello como asax:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

TelemetryClients novo todos os adiciona automaticamente o valor da propriedade Olá que você especificar. Eventos de telemetria individual podem substituir valores padrão de saudação.

## <a name="next-steps"></a>Próximas etapas
   - [Usuários, Sessões, Eventos](app-insights-usage-segmentation.md)
   - [Funis](usage-funnels.md)
   - [Retenção](app-insights-usage-retention.md)
   - [Fluxos de Usuário](app-insights-usage-flows.md)
   - [Pastas de trabalho](app-insights-usage-workbooks.md)
   - [Adicionar contexto de usuário](app-insights-usage-send-user-context.md)
