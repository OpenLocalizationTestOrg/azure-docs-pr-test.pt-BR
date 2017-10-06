---
title: "aaaManage preço e volume de dados para o Azure Application Insights | Microsoft Docs"
description: Gerencie volumes de telemetria e monitore custos no Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Gerenciar preços e volume de dados no Application Insights


Os preços do [Azure Application Insights][start] baseiam-se no volume de dados por aplicativo. Baixa utilização durante o desenvolvimento ou para um aplicativo pequeno é provavelmente toobe livre, porque não há uma provisão mensal de 1 GB de dados de telemetria.

Cada recurso do Application Insights é cobrado como um serviço separado e contribui toohello fatura para tooAzure sua assinatura.

Há dois planos de preço. plano de padrão de saudação é chamado de Basic. Você pode optar por plano de empresa hello, que tem um custo diário, mas permite que determinados recursos adicionais, como [a exportação contínua](app-insights-export-telemetry.md).

Se você tiver dúvidas sobre como funciona o preço para o Application Insights, sinta-se livre toopost uma pergunta em nosso [fórum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>planos de preços Olá

Consulte Olá [página de preços do Application Insights] [ pricing] de preços atuais na sua moeda.

### <a name="basic-plan"></a>Plano Básico

plano básico Olá é o padrão de saudação quando um novo recurso do Application Insights é criado e será suficiente para a maioria dos clientes.

* No plano básico do hello, você será cobrado por volume de dados: número de bytes de telemetria recebida pelo Application Insights. Volume de dados é medido como tamanho de saudação de pacote de dados JSON Olá descompactado recebido pelo Application Insights do seu aplicativo.
Para [dados tabulares importados para análise](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), volume de dados de saudação é medido como Olá tamanho descompactado de arquivos enviados tooApplication Insights.  
* O primeiro 1 GB para cada aplicativo é gratuito, então se você estiver apenas testando ou desenvolver, você está toopay toohave improvável.
* Os dados de [Live Metrics Stream](app-insights-live-stream.md) não são contatos para fins de preços.
* [A exportação contínua](app-insights-export-telemetry.md) está disponível para um encargo extra por GB no plano básico hello.

### <a name="enterprise-plan"></a>Plano Enterprise

* No plano de empresa hello, seu aplicativo pode usar todos os recursos de saudação do Application Insights. [Exportação Contínua](app-insights-export-telemetry.md) e 

[Conector de análise de log](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) estão disponíveis sem nenhum custo extra no plano de empresa hello.
* Você paga por nó que está enviando a telemetria para todos os aplicativos no plano de empresa hello. 
 * Um *nó* é um computador de servidor físico ou virtual ou então uma instância de função de Plataforma como Serviço que hospeda seu aplicativo.
 * Computadores de desenvolvimento, navegadores do cliente e dispositivos móveis não são contados como nós.
 * Se seu aplicativo tem vários componentes que enviam telemetria, assim como um serviço Web e um trabalho de back-end, eles são contadas separadamente.
 * Os dados de [Live Metrics Stream](app-insights-live-stream.md) não são contados para fins de preço.* Em uma assinatura, as cobranças são por nó, não por aplicativo. Se você tiver cinco nós enviar telemetria para aplicativos 12 e Olá cobra é de cinco nós.
* Embora as cobrança sejam cotadas por mês, você é cobrado apenas por aquelas horas em que um nó envia telemetria de um aplicativo. Olá taxa por hora é Olá entre aspas mensalidade / 744 (Olá o número de horas em um mês dia 31).
* Uma alocação de volume de dados de 200 MB por dia é fornecida para cada nó detectado (com granularidade por hora). Alocação de dados não utilizados não é transferida de um dia toohello lado.
 * Se você escolher Olá opção preços do Enterprise, cada assinatura é um limite diário de dados com base no número de saudação de nós enviar telemetria de recursos do Application Insights toohello nessa assinatura. Portanto, se você tiver 5 nós enviar dados de todos os dias, você terá uma pool extra de 1 GB aplicado tooall Olá Application Insights recursos nessa assinatura. Não importa se alguns nós estão enviando que dados mais do que outros nós porque Olá incluía dados são compartilhados entre todos os nós. Se, em um determinado dia, recursos do Application Insights Olá recebem mais dados do que está incluído na alocação de dados diário Olá para essa assinatura, aplicam encargos de dados excedentes Olá por GB. 
 * o limite de dados diário Olá é calculado como número de saudação de horas por dia hello (usando o UTC) que cada nó está enviando telemetria dividida por 24 horas 200 MB. Portanto, se você tiver 4 nós enviar telemetria durante 15 da saudação 24 horas por dia hello, Olá incluídos dados para esse dia seria ((4 x 15) / 24) x 200 MB = 500 MB. Preço de saudação do 2.30 USD por GB para média de dados, gratuitamente Olá seria USD 1.15 se nós Olá enviam 1 GB de dados naquele dia.
 * Note que o limite diário do plano de empresa Olá não é compartilhado com aplicativos para que você escolheu opção básica hello e extra não utilizada não é herdada do dia a dia. 
* Aqui estão alguns exemplos de determinar a contagem de nós distintos:
| Cenário                               | Contagem de nós diária total |
|:---------------------------------------|:----------------:|
| Um aplicativo está usando três instâncias do Serviço de Aplicativo do Azure e um servidor virtual | 4 |
| 3 aplicativos em execução em 2 VMs e recursos do Application Insights Olá para esses aplicativos são em Olá a mesma assinatura e planeje Olá Enterprise | 2 | 
| 4 aplicativos cujos recursos de informações de aplicativos estão em Olá a mesma assinatura. Cada aplicativo executa duas instâncias durante 16 horas fora do horário de pico e quatro instâncias durante oito horas no horário de pico. | 13.33 | 
| Serviços de nuvem com uma função de trabalho e uma função web, cada uma executando duas instâncias | 4 | 
| Cluster do Service Fabric de cinco nós executando 50 microsserviços, cada microsserviço executando três instâncias | 5|

* comportamento de contagem de nó preciso Olá depende em que o SDK do Application Insights seu aplicativo está usando. 
  * Nas versões do SDK 2.2 e em diante, ambos Olá Application Insights [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) ou [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) será cada host de aplicativo como um nó de relatório, por exemplo hello nome do computador para o servidor físico e hosts de VM ou Olá nome da instância no caso de saudação de serviços de nuvem.  Olá a única exceção é aplicativos usando apenas [.NET Core](https://dotnet.github.io/) e hello SDK do Application Insights Core, nesse caso somente um nó será relatado para todos os hosts porque o nome de host de saudação não está disponível. 
  * Para versões anteriores do SDK do hello, Olá [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) irão se comportar como hello versões mais recentes do SDK, porém Olá [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) relatará um único nó, independentemente do número de saudação de hosts de aplicativo real. 
  * Observe que se seu aplicativo estiver usando Olá SDK tooset roleInstance tooa valor de personalizado, por padrão mesmo valor será usado toodetermine Olá contagem de nós. 
  * Se você estiver usando uma nova versão do SDK com um aplicativo que é executado em dispositivos móveis ou computadores cliente, é possível que a contagem de saudação de nós pode retornar um número que é muito grande (de grande número de dispositivos móveis ou computadores cliente Olá). 

### <a name="multi-step-web-tests"></a>Testes na Web com diversas etapas

Há uma cobrança adicional para [testes na Web de várias etapas](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Isso se refere a tooweb testes que executam uma sequência de ações. 

Não há nenhuma cobrança separada para 'testes de ping' de uma única página. A telemetria de testes de ping e de testes de várias etapas é cobrada juntamente com outras telemetrias do seu aplicativo.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Qualificação de assinatura do Operations Management Suite

Como [recentemente anunciado](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), os clientes que compram Microsoft Operations Management Suite E1 e E2 estão tooget capaz de aplicativo Insights Enterprise como um componente adicional sem custo adicional. Especificamente, cada unidade do Operations Management Suite E1 e E2 inclui um nó de too1 de qualificação do plano de empresa de saudação do Application Insights. Conforme observado acima, cada nó do Application Insights inclui too200 MB de dados incluídos por dia (separado de ingestão de dados de análise de Log), com a retenção de dados de 90 dias sem nenhum custo adicional. 

> [!NOTE]
> tooensure que você obtenha este direito, você deve ter os recursos do Application Insights Olá empresa preços do plano. Esse direito se aplica apenas como nós, portanto recursos do Application Insights no plano básico Olá não terão nenhum benefício. Observe que esse direito não estarão visível no hello estimado custos mostrados em recursos Olá + folha de preços. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Examine os planos de preços e estime os custos

Applicaition Insights torna fácil toounderstand Olá preços planos disponíveis e quais Olá custos são provavelmente ser com base nos padrões de uso recentes. Comece abrindo Olá **recursos + preços** folha em Olá recurso do Application Insights no hello portal do Azure:

![Escolha Preço.](./media/app-insights-pricing/01-pricing.png)

**a.** Examine o volume de dados para o mês de saudação. Isso inclui todos os dados de saudação recebidas e mantidas (após qualquer [amostragem](app-insights-sampling.md) de seus aplicativos de cliente e servidor e de testes de disponibilidade.

**b.** Uma cobrança separada é feita pelos [testes na Web de várias etapas](app-insights-monitor-web-app-availability.md#multi-step-web-tests). (Isso não inclui os testes de disponibilidade simples, que são incluídos no hello custos de volume de dados).

**c.** Habilite o plano de empresa hello.

**d.** Clique no volume de dados de tooview toodata gerenciamento opções para Olá no mês passado, defina uma capacidade diária ou amostragem de inclusão.

Encargos de informações do aplicativo são adicionados tooyour fatura do Azure. Você pode ver detalhes do seu Azure cobrar em Olá seção de cobrança do hello portal do Azure ou em Olá [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![No menu do lado de saudação, escolha a cobrança.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Taxa de dados
Há três maneiras na qual Olá volume enviar dados é limitado:

* **Amostragem:** esse mecanismo pode ser usado reduza Olá telemetria enviada de seus aplicativos de servidor e cliente, com mínima distorção de métricas. Essa é Olá ferramenta primária tem tootune Olá quantidade de dados. Saiba mais sobre [recursos de amostragem](app-insights-sampling.md). 
* **Capacidade diária:** quando criar um recurso do Application Insights de saudação do portal Azure isso está definido too500 GB/dia. Olá padrão ao criar um recurso do Application Insights do Visual Studio, é pequeno (somente 32,3 MB/dia) que é destinado somente toofaciliate de teste. Nesse caso, ele é destinado a que usuário Olá gerará capacidade diária de saudação antes de implantar o aplicativo hello em produção. limite máximo de saudação é 500 GB/dia, a menos que você solicitou um máximo maior para um aplicativo de alto tráfego. Tome cuidado ao definir a capacidade diária de hello, como sua intenção deve ser **nunca toohit Olá capacidade diária**, porque você, em seguida, perda de dados para o restante de saudação do dia hello e ser toomonitor não é possível que seu aplicativo. toochange-lo, use Olá diário volume cap folha vinculados na folha de gerenciamento de volumes de dados de saudação (veja abaixo). Observe que alguns tipos de assinatura têm crédito que não pode ser usado no Application Insights. Se a assinatura Olá apresenta um gastos limitar, Olá diariamente folha cap terá instruções como tooremove-lo e habilitar Olá diário toobe cap gerado mais 32,3 MB/dia.  
* **Limitação:** essa limites Olá dados taxa too32 k eventos por segundo, calculada pela média em 1 minuto. 


*O que acontece se meu aplicativo exceder a limitação de taxa de saudação?*

* volume de saudação de dados que envia seu aplicativo é avaliada a cada minuto. Se ele exceder Olá taxa média de minuto hello, o servidor de saudação recusa algumas solicitações. Olá SDK armazena em buffer Olá dados e, em seguida, tenta tooresend, distribuindo um surto em vários minutos. Se seu aplicativo consistentemente envia dados em acima Olá limitação de taxa, alguns dados serão removidos. (Olá ASP.NET, Java e JavaScript SDKs tente tooresend dessa maneira; outros SDKs podem simplesmente soltar limitada dados). Caso ocorra uma limitação, será exibido um aviso de notificação que isso aconteceu.

*Como posso saber quantos dados meu aplicativo está enviando?*

* Olá abrir **gerenciamento do volume de dados** gráfico de volume do folha toosee Olá diário dados. 
* Ou, no Metrics Explorer, adicione um novo gráfico e selecione **Volume de pontos de dados** como a métrica. Ative o Agrupamento e agrupe por **Tipo de dados**.

## <a name="tooreduce-your-data-rate"></a>tooreduce a taxa de dados
Aqui estão algumas coisas que você pode fazer tooreduce o volume de dados:

* Use a [Amostragem](app-insights-sampling.md). Essa tecnologia reduz a taxa de dados sem prejudicar suas métricas e sem interromper Olá capacidade toonavigate entre itens relacionados em pesquisa. Em aplicativos de servidor, ela funciona automaticamente.
* [Limitar o número de saudação de chamadas Ajax que podem ser relatadas](app-insights-javascript.md#detailed-configuration) em cada modo de exibição de página ou comutador relatório de Ajax.
* Desative os módulos de coleção que você não precisa [editando o ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Por exemplo, você pode decidir que os contadores de desempenho ou dados de dependência não são essenciais.
* Divida as chaves de instrumentação tooseparate telemetria. 
* Métricas de pré-agregação. Se você tiver colocado chamadas tooTrackMetric em seu aplicativo, você pode reduzir o tráfego usando a sobrecarga de saudação que aceita o cálculo da média de saudação e desvio padrão de um lote de medidas. Ou então, você pode usar um [pacote de pré-agregação](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Gerenciando o volume de dados máximo diária para o hello

Você pode usar o hello diário volume cap toolimit Olá dados coletados, mas se cap Olá for atendida, resultará em perda de todos os telemetery enviadas do seu aplicativo para o restante de saudação do dia de saudação. É **não é aconselhável** toohave capacidade diária de saudação do toohit seu aplicativo desde que você está integridade de saudação do tootrack não é possível e o desempenho do seu aplicativo depois que for atingido. 

Em vez disso, use [amostragem](app-insights-sampling.md) tootune Olá volume toohello nível de dados você deseja e usar capacidade diária Olá apenas como um "último recurso" caso o aplicativo começa a enviar muito mais altos volumes de telemetery inesperadamente. 

capacidade diária do toochange hello, em Olá seção de configuração do recurso Insihgts do aplicativo, clique em **gerenciamento do volume de dados** , em seguida, **capacidade diária**.

![Ajustando a capacidade de volume de telemetria diária Olá](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>amostragem
[Amostragem](app-insights-sampling.md) é um método de reduzir a taxa de saudação à qual telemetria é enviada tooyour aplicativo, enquanto ainda retém Olá capacidade toofind eventos relacionados durante as pesquisas de diagnósticas e a conta ainda retendo evento correto. 

A amostragem é uma maneira eficiente tooreduce cobra e permanecer dentro da sua cota mensal. Olá algoritmo de amostragem retém itens relacionados de telemetria, para que, por exemplo, quando você usa a pesquisa, você pode encontrar solicitação Olá relacionadas tooa exceção em particular. algoritmo de saudação também retém contagens corretas, para que você veja os valores corretos Olá no Explorer de métrica de taxas de solicitação, taxas de exceção e outras contagens.

Há várias formas de amostragem.

* [Amostragem adaptável](app-insights-sampling.md) é padrão Olá Olá ASP.NET SDK, que ajusta automaticamente o volume de toohello de telemetria que envia seu aplicativo. Ela funciona automaticamente no hello SDK em seu aplicativo web, para que o tráfego de telemetria Olá na rede de saudação seja reduzido. 
* *Amostragem de inclusão* é uma alternativa que opera no ponto de saudação onde telemetria do seu aplicativo insere o serviço do Application Insights hello. Ela não afeta o volume de saudação de telemetria enviada do seu aplicativo, mas reduz volume Olá retido pelo serviço de saudação. Você pode usá-lo cota de saudação tooreduce usada pela telemetria dos navegadores e outros SDKs.

tooset inclusão de amostragem, definir o controle de saudação na folha de preços hello:

![De saudação cotas e preços folha, clique em bloco de exemplos de saudação e selecione uma fração de amostragem.](./media/app-insights-pricing/04.png)

> [!WARNING]
> folha de amostragem de dados Olá controla apenas o valor Olá de amostragem de inclusão. Ele não reflete a taxa de amostragem de Olá Olá SDK do Application Insights no seu aplicativo está sendo aplicada. Se a telemetria de entrada hello já tem foram amostrada a saudação SDK, amostragem de inclusão não será aplicada.
> 

toodiscover Olá real amostragem taxa, independentemente de onde ela foi aplicada, use um [consulta analítica](app-insights-analytics.md) como este:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Em cada retidos registro, `itemCount` indica número Olá de originais registros que ele representa, igual too1 + número de saudação de registros descartados anteriores. 


## <a name="automation"></a>Automação

Você pode escrever um plano de preço do script tooset hello, usando o gerenciamento de recursos do Azure. [Saiba como](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Resumo de limites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Próximas etapas

* [Amostragem](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

