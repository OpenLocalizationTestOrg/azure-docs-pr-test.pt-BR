---
title: aaaAzure perguntas frequentes sobre o Application Insights | Microsoft Docs
description: Perguntas frequentes sobre o Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: Perguntas Frequentes

## <a name="configuration-problems"></a>Problemas de configuração
*Estou tendo problemas para configurar:*

* [Aplicativo .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [Monitorar um aplicativo já em execução](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Diagnóstico do Azure](app-insights-azure-diagnostics.md)
* [Aplicativo Web Java](app-insights-java-troubleshoot.md)

*Não recebo qualquer valor de meu servidor*

* [Definir exceções de firewall](app-insights-ip-addresses.md)
* [Configurar um servidor ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Configurar um servidor Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>É possível usar o Application Insights com...?

* [Aplicativos Web em um servidor IIS : em uma VM ou local](app-insights-asp-net.md)
* [Aplicativos Web Java](app-insights-java-get-started.md)
* [Aplicativos do Node.js](app-insights-nodejs.md)
* [Aplicativos Web no Azure](app-insights-azure-web-apps.md)
* [Serviços de Nuvem no Azure](app-insights-cloudservices.md)
* [Servidores de aplicativo executando em Docker](app-insights-docker.md)
* [Aplicativos Web de página única](app-insights-javascript.md)
* [Sharepoint](app-insights-sharepoint.md)
* [Aplicativo da área de trabalho do Windows](app-insights-windows-desktop.md)
* [Outras plataformas](app-insights-platforms.md)

## <a name="is-it-free"></a>É gratuito?

Sim, para uso experimental. No hello básica de preços do plano, seu aplicativo pode enviar uma determinada extra de dados por mês sem custo adicional. permissão de livre de Olá seja grande o suficiente toocover desenvolvimento e publicação de um aplicativo para um número pequeno de usuários. Você pode definir um cap tooprevent mais de uma quantidade especificada de dados que está sendo processada.

Volumes maiores de telemetria são cobrados por Olá Gb. Fornecemos algumas dicas sobre como muito[limitar os encargos](app-insights-pricing.md).

plano de empresa Olá incorre em um custo para cada dia em que cada nó do servidor da web envia a telemetria. Ele é adequado se você quiser toouse exportação contínua em grande escala.

[Olá leitura preços plano](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Quanto isso custa?

* Olá abrir **recursos + preços** página em um recurso do Application Insights. Há um gráfico de uso recente. Você pode definir um limite de volume de dados, se desejar.
* Olá abrir [folha de cobrança do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee suas contas em todos os recursos.

## <a name="q14"></a>O que o Application Insights modifica no meu projeto?
detalhes de saudação dependem do tipo de saudação do projeto. Para um aplicativo Web:

* Adiciona o projeto de tooyour esses arquivos:

  * ApplicationInsights.config.
  * ai.js
* Instala estes pacotes NuGet:

  * *API do Application Insights* - Olá core API
  * *API do Application Insights para aplicativos Web* -usado toosend telemetria do servidor de saudação
  * *API do Application Insights para aplicativos JavaScript* -usado toosend telemetria do cliente Olá

    os pacotes de saudação incluem esses assemblies:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Insere itens em:

  * Web.config
  * packages.config
* (Novos projetos somente - se você [Adicionar projeto existente do Application Insights tooan][start], você tem toodo isso manualmente.) Insere trechos Olá tooinitialize de código de cliente e servidor com ID de recurso Olá Application Insights. Por exemplo, em um aplicativo MVC, código é inserido na página principal do hello Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Como atualizar de versões anteriores do SDK?
Consulte Olá [notas de versão](app-insights-release-notes.md) para Olá SDK apropriados tooyour tipo de aplicativo.

## <a name="update"></a>Como alterar o recurso do Azure ao qual meu projeto envia dados?
No Gerenciador de Soluções, clique com o botão direito do mouse em `ApplicationInsights.config` e escolha **Atualizar o Application Insights**. Você pode enviar Olá dados tooan existente ou novo recurso no Azure. Assistente de atualização altera o Olá Olá chave de instrumentação no applicationinsights. config, que determina onde o servidor de saudação SDK envia seus dados. A menos que você desmarque a opção "Atualizar tudo", chave Olá onde ela aparecerá em páginas da web também será alterado.

## <a name="what-is-status-monitor"></a>O que é o Status Monitor?

Um aplicativo de área de trabalho que você pode usar em sua toohelp de servidor web IIS configurar o Application Insights em aplicativos da web. Ele não coleta telemetria: você pode interrompê-lo quando não estiver configurando um aplicativo. 

[Saiba mais](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Qual a telemetria coletada pelo Application Insights?

A partir dos aplicativos Web do servidor:

* Solicitações HTTP
* [Dependências](app-insights-asp-net-dependencies.md). Chamadas para: bancos de dados SQL; HTTP chama tooexternal serviços; Azure Cosmos banco de dados, tabela, o armazenamento de blob e fila. 
* [Exceções](app-insights-asp-net-exceptions.md) e rastreamentos de pilha.
* [Contadores de desempenho](app-insights-performance-counters.md) - se você usar [Status Monitor](app-insights-monitor-performance-live-website-now.md), monitoring(app-insights-azure-web-apps.md) do Azure ou hello [gravador do Application Insights collectd](app-insights-java-collectd.md).
* [Eventos e métricas personalizados](app-insights-api-custom-events-metrics.md) que você codifica.
* [Logs de rastreamento](app-insights-asp-net-trace-logs.md) se você configurar o coletor apropriado hello.

A partir das [páginas da Web do cliente](app-insights-javascript.md):

* [Contagens de exibição de página](app-insights-web-track-usage.md)
* [Chamadas AJAX](app-insights-asp-net-dependencies.md) Solicitações feitas a partir de um script em execução.
* Dados de carregamento de exibição de página
* Contagens de sessão e usuários
* [IDs de Usuário Autenticado](app-insights-api-custom-events-metrics.md#authenticated-users)

A partir de outras fontes, se você configurá-las:

* [Diagnóstico do Azure](app-insights-azure-diagnostics.md)
* [Contêineres de Docker](app-insights-docker.md)
* [Importar tabelas tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>Eu posso filtrar ou modificar alguma telemetria?

Sim, no servidor de saudação é possível escrever:

* Telemetria processador toofilter ou adicionar propriedades de itens de telemetria tooselected antes que sejam enviados do seu aplicativo.
* Telemetria itens inicializadores de tooadd propriedades tooall de telemetria.

Saiba mais sobre [ASP.NET](app-insights-api-filtering-sampling.md) ou [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Como dados de Cidade, País e outros dados de área geográfica são calculados?

Podemos pesquisar Olá endereço IP (IPv4 ou IPv6) saudação do cliente de web usando [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Telemetria do navegador: coletamos o endereço IP do remetente hello.
* Telemetria de servidor: endereço IP do cliente de saudação de coleta de módulo do Application Insights hello. Ele não será coletado se `X-Forwarded-For` estiver configurado.

Você pode configurar Olá `ClientIpHeaderTelemetryInitializer` tootake endereço IP de saudação de um cabeçalho diferente. Em alguns sistemas, por exemplo, ele é movido por um proxy, carregar balanceador ou CDN muito`X-Originating-IP`. [Saiba mais](http://apmtips.com/blog/2016/07/05/client-ip-address/).

Você pode [usar o Power BI](app-insights-export-power-bi.md) toodisplay sua telemetria de solicitação em um mapa.


## <a name="data"></a>Quanto tempo os dados são retidos no portal de Olá? É seguro?
Veja [Privacidade e Retenção de Dados][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Podem pessoal informações de identificação pessoais (PII) ser enviadas na telemetria Olá?

Isso é possível se o seu código envia tais dados. Isso também pode acontecer se as variáveis nos rastreamentos de pilha incluírem PII. Sua equipe de desenvolvimento deve realizar tooensure de avaliações de risco PII são tratada corretamente. [Saiba mais sobre privacidade e retenção de dados ](app-insights-data-retention-privacy.md).

último octeto saudação do endereço de web do cliente Olá é sempre definido too0 após a inclusão pelo portal de saudação.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Meu iKey está visível na minha fonte da página da Web. 

* Essa é uma prática comum em soluções de monitoramento.
* Ele não pode ser usado toosteal seus dados.
* Ele pode ser usado tooskew seus alertas de dados ou gatilho.
* Não temos conhecimento se algum cliente teve tais problemas.

Você pode:

* Usar dois iKeys separados (recursos do Application Insights separados) para dados do servidor e cliente. Ou
* Escrever um proxy que é executado em seu servidor e ter o cliente da web de saudação enviar dados por meio do proxy.

## <a name="post"></a>Como eu vejo dados de POST na pesquisa de Diagnóstico?
Nós não registrar dados de POSTAGEM automaticamente, mas você pode usar uma chamada de TrackTrace: colocar dados saudação no parâmetro de mensagem de saudação. Isso tem um limite de tamanho maior que os limites de saudação nas propriedades de cadeia de caracteres, embora ele não é possível filtrar.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Devo usar recursos do Application Insights simples ou múltiplos?

Use um recurso único para todos os componentes de saudação ou funções em um sistema de negócios único. Use recursos separados para desenvolvimento, teste e versões de lançamento e para aplicativos independentes.

* [Consulte a discussão Olá aqui](app-insights-separate-resources.md)
* [Exemplo : serviço de nuvem com funções Web e funções de trabalho](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Como alterar dinamicamente o chave de instrumentação Olá?

* [Discussão aqui](app-insights-separate-resources.md)
* [Exemplo : serviço de nuvem com funções Web e funções de trabalho](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Quais são hello usuário e sessão conta?

* Olá SDK de JavaScript define um cookie de usuário no cliente de web hello, usuários retornando tooidentify e uma atividades de toogroup de cookie de sessão.
* Se não houver nenhum script de cliente, você pode [definir cookies no servidor de saudação](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Se um usuário real usar seu site em diferentes navegadores, usar navegação em modo privado/incógnito ou usar diferentes computadores, então, eles serão contados mais de uma vez.
* tooidentify um usuário que fez logon em computadores e navegadores, adicione uma chamada muito[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a> Eu habilitei tudo no Application Insights?
| O que você deverá ver | Como tooget-lo | Por que você deseja isso |
| --- | --- | --- |
| Gráficos de disponibilidade |[Testes da Web](app-insights-monitor-web-app-availability.md) |Tenha certeza que o aplicativo Web está ativo |
| Desempenho do aplicativo para servidores: tempos de resposta... |[Adicionar projeto do Application Insights tooyour](app-insights-asp-net.md) ou [instalar AI Status Monitor no servidor](app-insights-monitor-performance-live-website-now.md) (ou escrever seu próprio código muito[rastrear dependências](app-insights-api-custom-events-metrics.md#trackdependency)) |Detectar problemas de desempenho |
| Telemetria de dependência |[Instalar o AI Status Monitor no servidor](app-insights-monitor-performance-live-website-now.md) |Diagnosticar problemas com bancos de dados ou outros componentes externos |
| Obter rastreamentos de pilha por meio de exceções |[Inserir chamadas TrackException em seu código](app-insights-asp-net-exceptions.md) (mas alguns são informados automaticamente) |Detectar e diagnosticar exceções |
| Pesquisar rastreamentos de log |[Adicionar um adaptador de registro em log](app-insights-asp-net-trace-logs.md) |Diagnosticar exceções, problemas de desempenho |
| Noções básicas de uso do cliente: modos de exibição de página, sessões,... |[Inicializador de JavaScript em páginas da Web](app-insights-javascript.md) |Análise de uso |
| Métricas de cliente personalizadas |[Rastreando chamadas em páginas da Web](app-insights-api-custom-events-metrics.md) |Aprimorar a experiência do usuário |
| Métricas de servidor personalizadas |[Rastreando chamadas no servidor](app-insights-api-custom-events-metrics.md) |Business intelligence |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Por que são Olá contagens em gráficos de métricas e de pesquisa diferente?

[Amostragem](app-insights-sampling.md) reduz o número de saudação de itens de telemetria (solicitações, eventos personalizados e assim por diante) que, na verdade, são enviadas de seu portal de toohello do aplicativo. Na pesquisa, você ver o número de saudação de itens, na verdade, recebidos. Em gráficos de métricas que exibem uma contagem de eventos, você ver o número de saudação do originais eventos que ocorreram. 

Cada item que é transmitido carrega uma propriedade `itemCount` que mostra quantos eventos originais esse item representa. tooobserve amostragem na operação, você pode executar essa consulta em análise:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automação

### <a name="configuring-application-insights"></a>Configurando o Application Insights

Você pode [gravar scripts do PowerShell](app-insights-powershell.md) usando o Azure Resource Monitor para:

* Criar e atualizar recursos do Application Insights.
* Saudação de conjunto de preços do plano.
* Obter chave de instrumentação hello.
* Adicionar um alerta de métrica.
* Adicionar um teste de disponibilidade.

Não é possível configurar um relatório do Metric Explorer ou configurar a exportação contínua.

### <a name="querying-hello-telemetry"></a>Consultando telemetria Olá

Saudação de uso [API REST](https://dev.applicationinsights.io/) toorun [análise](app-insights-analytics.md) consultas.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Como configurar um alerta em um evento?

Os alertas do Azure são somente em métricas. Crie uma métrica personalizada que cruze um limite de valor sempre que o evento ocorrer. Em seguida, defina um alerta na métrica hello. Observe que: você receberá uma notificação sempre que a métrica de saudação exceder o limite de saudação em qualquer direção; Você não obterá uma notificação até Olá primeiro cruzamento, independentemente se o valor inicial da saudação está alto ou baixo; sempre há uma latência de alguns minutos.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Há encargos de transferência de dados entre um aplicativo Web e o Application Insights?

* Se seu aplicativo Web do Azure estiver hospedado em um data center, onde há um ponto de extremidade de coleta do Application Insights, não haverá cobrança. 
* Se não houver um ponto de extremidade de coleta no data center do host, então, a telemetria do seu aplicativo incorrerá em [Encargos de saída do Azure](https://azure.microsoft.com/pricing/details/bandwidth/).

Isso não depende de onde seu recurso Application Insights está hospedado. Apenas depende de distribuição de saudação do nosso pontos de extremidade.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Portal do Application Insights toohello telemetria pode enviar?

Recomendamos que você usar nossos SDKs e Olá API do SDK (app-insights-api-custom-events-metrics.md). Há variantes de saudação SDK para várias [plataformas](app-insights-platforms.md). Esses SDKs tratam buffer, compressão, limitação, repetições e, assim por diante. No entanto, Olá [esquema de inclusão](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) e [protocolo de ponto de extremidade](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) são públicos.

## <a name="can-i-monitor-an-intranet-web-server"></a>É possível monitorar um servidor Web de intranet?

Aqui estão dois métodos:

### <a name="firewall-door"></a>Porta de firewall

Permitir que o web server toosend telemetria tooour pontos de extremidade https://dc.services.visualstudio.com:443 e https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Proxy

Rotear o tráfego do seu servidor de gateway tooa em sua intranet, definindo isso no applicationinsights. config:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

O gateway deve encaminhar toohttps://dc.services.visualstudio.com:443 v2/controle de tráfego de saudação

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>É possível executar testes na Web de Disponibilidade em um servidor de intranet?

Nosso [testes na web](app-insights-monitor-web-app-availability.md) executados em pontos que são distribuídos em todo o mundo de saudação de presença. Existem duas soluções:

* Porta de firewall - permitir solicitações de servidor tooyour de [hello longo e lista mutável de web agentes de teste](app-insights-ip-addresses.md).
* Escreva seu próprio código toosend solicitações periódicas tooyour servidor de dentro de sua intranet. Você pode executar testes na Web do Visual Studio para essa finalidade. Testador de saudação pode enviar resultados Olá Insights tooApplication usando Olá TrackAvailability() API.

## <a name="more-answers"></a>Mais respostas
* [Fórum do Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
