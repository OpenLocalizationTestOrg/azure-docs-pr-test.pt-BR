---
title: "aaaData retenção e armazenamento no Azure Application Insights | Microsoft Docs"
description: "Declaração de política de privacidade e retenção"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Coleta, retenção e armazenamento de dados no Application Insights


Quando você instala o [Azure Application Insights] [ start] SDK em seu aplicativo, ele enviará telemetria sobre sua nuvem de toohello do aplicativo. Naturalmente, os desenvolvedores responsáveis desejam tooknow exatamente quais dados são enviados, o que acontece toohello dados e como eles podem manter controle sobre ele. Em particular, poderiam ser enviados dados confidenciais, onde são armazenados e qual é o nível de segurança? 

Primeiro, Olá realidade:

* os módulos de telemetria padrão Hello "sem caixa hello" serão improvável que toosend dados confidenciais toohello. Telemetria Hello está preocupada com carga, métricas de desempenho e uso, relatórios de exceção e outros dados de diagnóstico. dados de usuário principal de saudação visíveis nos relatórios de diagnóstico Olá são URLs. mas seu aplicativo em qualquer caso não deve colocar dados confidenciais em texto sem formatação em uma URL.
* Você pode escrever código que envia toohelp adicionais telemetria personalizada com o uso de monitoramento e diagnóstico. (Essa extensibilidade é um ótimo recurso do Application Insights.) Seria possível, por engano, toowrite esse código para que ela inclua pessoais e outros dados confidenciais. Se seu aplicativo funcione com esses dados, você deve aplicar um código de saudação rigorosa processos tooall que você escrever.
* Ao desenvolver e testar seu aplicativo, é fácil tooinspect o que está sendo enviado por Olá SDK. dados saudação aparecem no hello depuração janelas de saída de hello IDE e navegador. 
* dados de saudação são mantidos em [Microsoft Azure](http://azure.com) servidores no hello EUA ou na Europa. (Mas seu aplicativo pode ser executado em qualquer lugar). O Azure tem [fortes processos de segurança e cumpre uma ampla gama de padrões de conformidade](https://azure.microsoft.com/support/trust-center/). Somente você e sua equipe designada que têm acesso tooyour dados. Equipe da Microsoft pode ter restringido o acesso tooit apenas em circunstâncias limitadas específicas com o seu conhecimento. Ele é criptografado em trânsito, embora não estiverem em servidores de saudação.

restante deste artigo Hello mais totalmente aborda essas respostas. Ele foi projetado toobe independente, para que você pode mostrar toocolleagues que não fazem parte da sua equipe.

## <a name="what-is-application-insights"></a>O que é o Application Insights?
[Informações de aplicativo do Azure] [ start] é um serviço fornecido pela Microsoft que ajuda a melhorar o desempenho de saudação e usabilidade do seu aplicativo ao vivo. Ele monitora o seu aplicativo todo o tempo de saudação executando, durante o teste e depois de publicado ou implantá-lo. Application Insights cria gráficos e tabelas que mostram a você, por exemplo, que horas do dia para obter a maioria dos usuários, como aplicativo hello responsivo está, e também que ser fornecido por qualquer externos de serviços que ele depende. Se houver falhas, falhas ou problemas de desempenho, você pode procurar dados de telemetria Olá causa de saudação toodiagnose detalhes. E serviço Olá enviará emails se houver alterações na disponibilidade de saudação e o desempenho do seu aplicativo.

Ordem tooget essa funcionalidade, você instala um SDK do Application Insights no seu aplicativo, que se torna parte do seu código. Quando seu aplicativo estiver em execução, Olá SDK monitora sua operação e envia o serviço de aplicativo Insights toohello telemetria. Este é um serviço de nuvem hospedado pelo [Microsoft Azure](http://azure.com). (Mas o Application Insights funciona para qualquer aplicativo, não apenas aqueles hospedados no Azure.)

![Olá SDK em seu aplicativo enviará telemetria toohello serviço Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

Olá serviço Application Insights armazena e analisa a telemetria de saudação. análise de saudação toosee ou pesquise Olá armazenados telemetria, entrar no tooyour conta do Azure e o recurso do Application Insights Olá aberto para seu aplicativo. Você também pode compartilhar acesso toohello dados com outros membros da equipe, ou com assinantes do Azure especificados.

Você pode ter dados exportados da saudação serviço Application Insights, por exemplo tooa banco de dados ou tooexternal ferramentas. Você fornece uma chave especial que você obtém do serviço de saudação cada ferramenta. chave de saudação pode ser revogado, se necessário. 

SDKs do Application Insights estão disponíveis para uma variedade de tipos de aplicativos: web serviços hospedados em seus próprios servidores J2EE ou ASP.NET ou no Azure. clientes da Web - ou seja, código de saudação em execução em uma página da web. aplicativos de área de trabalho e serviços; aplicativos de dispositivo, como o Windows Phone, iOS e Android. Todos eles enviarem telemetria toohello mesmo serviço.

## <a name="what-data-does-it-collect"></a>Quais dados são coletados?
### <a name="how-is-hello-data-is-collected"></a>Como é dados saudação é coletado?
Há três fontes de dados:

* Olá SDK, que se integram com o seu aplicativo ou [em desenvolvimento](app-insights-asp-net.md) ou [em tempo de execução](app-insights-monitor-performance-live-website-now.md). Há diferentes SDKs para diferentes tipos de aplicativos. Também há um [SDK para páginas da web](app-insights-javascript.md), que carrega no navegador de saudação do usuário final junto com a página de saudação.
  
  * Cada SDK tem um número de [módulos](app-insights-configuration-with-applicationinsights-config.md), que usam técnicas diferentes toocollect diferentes tipos de telemetria.
  * Se você instalar Olá SDK em desenvolvimento, você pode usar sua API toosend sua telemetria em módulos padrão de toohello de adição. Essa telemetria personalizada pode incluir quaisquer dados que você deseja toosend.
* Em alguns servidores de web, também há agentes que executam juntamente com o aplicativo hello e enviar telemetria sobre CPU, memória e ocupação da rede. Por exemplo, as VMs do Azure, hosts de Docker e [servidores J2EE](app-insights-java-agent.md) podem ter esses agentes.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) são processos executados pela Microsoft que enviam solicitações tooyour web app em intervalos regulares. serviço do Application Insights toohello os resultados de saudação são enviados.

### <a name="what-kinds-of-data-are-collected"></a>Quais tipos de dados são coletados?
categorias de saudação principais são:

* [Telemetria do servidor Web](app-insights-asp-net.md) - solicitações HTTP.  URI, solicitação de saudação do tempo gasto tooprocess, código de resposta, o endereço IP do cliente. ID da sessão
* [Páginas da Web](app-insights-javascript.md) - contagens de página, usuário e sessão. Tempos de carregamento de página. Exceções. Chamadas Ajax.
* Contadores de desempenho - memória, CPU, E/S, ocupação de rede.
* Contexto de cliente e servidor - sistema operacional, localidade, tipo de dispositivo, navegador, resolução da tela.
* [Exceções](app-insights-asp-net-exceptions.md) e falhas - **despejos de pilha**, id da compilação, tipo de CPU. 
* [Dependências](app-insights-asp-net-dependencies.md) -chama tooexternal serviços como REST, SQL, AJAX. Cadeia de conexão ou URI, duração, sucesso, comando.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) - duração do teste e etapas, respostas.
* [Logs de rastreamento](app-insights-asp-net-trace-logs.md) e [telemetria personalizada](app-insights-api-custom-events-metrics.md) - **qualquer elemento que você codifique nos seus logs ou telemetria**.

[Mais detalhes](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Como verificar o que está sendo coletado?
Se você estiver desenvolvendo um aplicativo hello usando o Visual Studio, execute o aplicativo hello no modo de depuração (F5). Telemetria Olá aparece na janela de saída de hello. A partir dali, é possível copiá-la e formatá-la como JSON para fácil inspeção. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Há também uma exibição mais legível na janela de diagnóstico de saudação.

Para páginas da Web, abra a janela de depuração do navegador.

![Pressione F12 e abra a guia de rede hello.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>É possível gravar o telemetria do código toofilter Olá antes de serem enviado?
Isso seria possível escrevendo um [plug-in de processador de telemetria](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Quanto tempo são mantidos os dados Olá?
Pontos de dados brutos (ou seja, itens que você pode consultar na análise e inspecionar na pesquisa) são mantidos por backup too90 dias. Se você precisar tookeep dados mais que isso, você poderá usar [a exportação contínua](app-insights-export-telemetry.md) toocopy-tooa conta de armazenamento.

Os dados agregados (ou seja, contagens, médias e outros dados estatísticos que você vê no Gerenciador de Métricas) são mantidos em um detalhamento de um minuto por 90 dias.

## <a name="who-can-access-hello-data"></a>Quem pode acessar dados Olá?
dados de saudação são tooyou visível e, se você tiver uma conta de organização, os membros da equipe. 

Ele pode ser exportado por você e os membros da equipe e pode ser copiado tooother locais e repassadas tooother pessoas.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>O que faz a Microsoft fazer com informações de saudação meu aplicativo envia tooApplication Insights?
A Microsoft usa os dados de saudação apenas em ordem tooprovide Olá serviço tooyou.

## <a name="where-is-hello-data-held"></a>Onde os dados saudação são mantidos?
* Olá EUA ou Europa. Você pode selecionar o local de hello quando você cria um novo recurso do Application Insights. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Isso significa que o aplicativo tem toobe hospedado no hello EUA ou Europa?
* Não. Seu aplicativo pode ser executado em qualquer lugar, em seus próprios hosts locais ou na nuvem de saudação.

## <a name="how-secure-is-my-data"></a>Quão seguros meus dados estão?
O Application Insights é um serviço do Azure. Políticas de segurança são descritas no hello [white paper de segurança do Azure, privacidade e conformidade](http://go.microsoft.com/fwlink/?linkid=392408).

Olá dados são armazenados em servidores do Microsoft Azure. Para contas Olá Portal do Azure, restrições de conta são descritas no hello [documento Azure segurança, privacidade e conformidade](http://go.microsoft.com/fwlink/?linkid=392408).

Acessar dados de tooyour pelos funcionários da Microsoft são restritos. Podemos acessar seus dados com a sua permissão e se é necessário toosupport o uso do Application Insights. 

Dados de agregação em aplicativos de todos os nossos clientes (por exemplo, taxas de dados e tamanho médio dos rastreamentos) são usado tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>A telemetria de outra pessoa poderia interferir meus dados do Application Insights?
Ele podem enviar conta tooyour de telemetria adicionais usando a chave de instrumentação hello, que pode ser encontrado no código Olá das páginas da web. Com dados suficientes adicionais, suas métricas não representariam corretamente o uso e o desempenho do seu aplicativo.

Se você compartilhar código com outros projetos, lembre-se de tooremove sua chave de instrumentação.

## <a name="is-hello-data-encrypted"></a>Dados de saudação são criptografados?
Não dentro de servidores de saudação no momento.

Todos os dados são criptografados conforme se movem entre datacenters.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Dados de saudação são criptografados em trânsito de servidores de Insights de tooApplication meu aplicativo?
Sim, podemos usar https toosend dados toohello portal de quase todos os SDKs, incluindo servidores web, dispositivos e páginas da web HTTPS. Olá única exceção é dados enviados de páginas de web HTTP simples. 

## <a name="personally-identifiable-information"></a>Informações pessoalmente identificáveis
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Informações pessoalmente identificáveis (PII) foi possível enviar o tooApplication Insights?
Sim, é possível. 

Como orientação geral:

* A telemetria mais padrão (ou seja, telemetria enviada sem que você escreva nenhum código) não inclui PII explícitas. No entanto, talvez seja possível tooidentify indivíduos por inferência de uma coleção de eventos.
* Mensagens de exceção e rastreamento podem conter informações de identificação pessoal
* Telemetria personalizada - ou seja, chamadas como TrackEvent escritos em código usando os rastreamentos de log ou API Olá - pode conter qualquer dado que você escolher.

tabela de saudação no final deste documento hello contém descrições mais detalhadas de saudação dados coletados.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Estou responsável por respeitar as leis e regulamentos na relação tooPII?
Sim. É o tooensure de responsabilidade coleção hello e uso de dados de saudação está em conformidade com as leis e regulamentos e com os termos do hello Microsoft Online Services.

Você deve informar os clientes adequadamente dados Olá que coleta de seu aplicativo e como dados de saudação são usados.

#### <a name="can-my-users-turn-off-application-insights"></a>Meus usuários podem desativar o Application Insights?
Não diretamente. Não fornecemos um comutador que os usuários podem operar tooturn fora do Application Insights.

No entanto, você pode implementar tal recurso em seu aplicativo. Olá todos os SDKs incluem uma definição de API que desativa a coleção de telemetria. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Meu aplicativo está coletando informações confidenciais acidentalmente. O Application Insights pode eliminar esses dados para que eles não sejam retidos?
O Application Insights não filtra nem exclui seus dados. Você deve gerenciar dados saudação adequadamente e evitar o envio de tal tooApplication dados Insights.

## <a name="data-sent-by-application-insights"></a>Dados enviados pelo Application Insights
Olá SDKs variam entre plataformas e existem tem vários componentes que você pode instalar. (Consulte muito[Application Insights - visão geral de][start].) Cada componente envia dados diferentes.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Classes de dados enviados em cenários diferentes
| Sua ação | Classes de dados coletados (consulte a tabela a seguir) |
| --- | --- |
| [Adicionar projeto da web do SDK do Application Insights tooa .NET][greenbrown] |ServerContext<br/>Inferido<br/>Contadores de desempenho<br/>Solicitações<br/>**Exceções**<br/>Session<br/>users |
| [Instalar o Monitor de Status no IIS][redfield] |Dependências<br/>ServerContext<br/>Inferido<br/>Contadores de desempenho |
| [Adicionar o aplicativo web do SDK do Application Insights tooa Java][java] |ServerContext<br/>Inferido<br/>Solicitação<br/>Session<br/>users |
| [Adicionar página de tooweb do SDK de JavaScript][client] |ClientContext  <br/>Inferido<br/>Página<br/>ClientPerf<br/>Ajax |
| [Definir propriedades padrão][apiproperties] |**Propriedades** em todos os eventos padrão e personalizados |
| [Chamar TrackMetric][api] |Valores numéricos<br/>**Propriedades** |
| [Chamar Track*][api] |Nome do evento<br/>**Propriedades** |
| [Chamar TrackException][api] |**Exceções**<br/>Despejo da pilha<br/>**Propriedades** |
| O SDK não é capaz de coletar dados. Por exemplo: <br/> - não é possível acessar os contadores de desempenho<br/> - exceção no inicializador de telemetria |Diagnóstico do SDK |

Para [SDKs para outras plataformas][platforms], consulte seus respectivos documentos.

#### <a name="hello-classes-of-collected-data"></a>classes de saudação de dados coletados
| Classe de dados coletados | Inclui (não é uma lista completa) |
| --- | --- |
| **Propriedades** |**Quaisquer dados - determinados pelo seu código** |
| DeviceContext |ID, IP, localidade, modelo de dispositivo, rede, tipo de rede, nome OEM, resolução de tela, instância de função, nome da função, tipo de dispositivo |
| ClientContext  |Sistema operacional, localidade, linguagem, rede, resolução da janela |
| Session |ID da sessão |
| ServerContext |Nome do computador, localidade, sistema operacional, dispositivo, sessão de usuário, contexto de usuário, operação |
| Inferido |localização geográfica do endereço IP, carimbo de data/hora, sistema operacional, navegador |
| Métricas |Valor e nome da métrica |
| Eventos |Valor e nome do evento |
| PageViews |URL e nome da página ou o nome de tela |
| Desempenho do cliente |URL/nome de página, tempo de carregamento do navegador |
| Ajax |Chamadas HTTP a partir da página da web tooserver |
| Solicitações |URL, duração, código de resposta |
| Dependências |Tipo (SQL, HTTP,...), cadeia de conexão ou URI, síncrono/assíncrono, duração, sucesso, instrução SQL (com Monitor de Status) |
| **Exceções** |Tipo, **mensagem**, pilhas de chamadas, arquivo-fonte e número de linha, ID do thread |
| Falhas |ID do processo, ID do processo-pai, ID de thread de falha; patch do aplicativo, ID de compilação; tipo de exceção, endereço, motivo; símbolos e registros ofuscados, endereços binários de início e término, nome e caminho binários, tipo de CPU |
| Rastreamento |**Mensagem** e nível de severidade |
| Contadores de desempenho |Tempo do processador, memória disponível, taxa de solicitação, taxa de exceções, bytes particulares do processo, taxa de E/S, duração da solicitação, comprimento da fila de solicitações |
| Disponibilidade |Código de resposta de teste da Web, duração de cada etapa de teste, nome do teste, carimbo de data/hora, sucesso, tempo de resposta, local de teste |
| Diagnóstico do SDK |Mensagem de rastreamento ou exceção |

Você pode [desativar alguns dados Olá editando applicationinsights. config][config]

## <a name="credits"></a>Credits
Este produto inclui dados GeoLite2 criados pelo MaxMind, disponíveis em [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

