---
title: "aaaAzure modelo de dados de telemetria do Application Insights - telemetria de solicitação | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de solicitações"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Telemetria de solicitações: modelo de dados do Application Insights

Um item de telemetria de solicitação (em [Application Insights](app-insights-overview.md)) representa Olá sequência lógica de execução disparada por um aplicativo de tooyour solicitação externa. Cada execução da solicitação é identificada pelo exclusivo `ID` e `url` que contém todos os parâmetros de execução de saudação. Você pode agrupar solicitações por lógica `name` e definir Olá `source` desta solicitação. A execução de código pode resultar em `success` ou `fail` e tem um determinado `duration`. Execuções com êxito e falha podem ser agrupadas ainda mais pelo `resultCode`. Hora de início para telemetria de solicitação Olá definida no nível de envelope hello.

Solicitação de telemetria dá suporte ao modelo de extensibilidade padrão hello usando personalizado `properties` e `measurements`.

## <a name="name"></a>Nome

Nome da solicitação de saudação representa a solicitação de código de caminho tomado tooprocess Olá. Valor de baixa cardinalidade tooallow melhor agrupamento de solicitações. Para solicitações HTTP, ele representa Olá método HTTP e o modelo de caminho de URL como `GET /values/{id}` sem Olá real `id` valor.

Web do Application Insights SDK envia o nome da solicitação "como está" com relação tooletter caso. Agrupamento na interface do usuário diferencia maiusculas de minúsculas para `GET /Home/Index` é contadas separadamente das `GET /home/INDEX` , embora geralmente eles resultam em Olá que mesmo controlador e ação de execução. Hello motivo disso é que as urls são em geral [diferencia maiusculas de minúsculas](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). Convém toosee se todas as `404` aconteceu para urls de saudação digitadas em letras maiusculas. Você pode ler mais em nome coleção request pelo SDK de Web do ASP.Net em Olá [postagem de blog](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Comprimento máximo: 1.024 caracteres

## <a name="id"></a>ID

Identificador de uma instância de chamada de solicitação. Usada para a correlação entre a solicitação e outros itens de telemetria. A ID deve ser globalmente exclusiva. Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).

Comprimento máximo: 128 caracteres

## <a name="url"></a>Url

URL de solicitação com todos os parâmetros de cadeia de consulta.

Comprimento máximo: 2.048 caracteres

## <a name="source"></a>Fonte

Origem da solicitação de saudação. Exemplos são a chave de instrumentação de saudação do chamador hello ou endereço de ip de saudação do chamador hello. Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).

Comprimento máximo: 1.024 caracteres

## <a name="duration"></a>Duração

Duração da solicitação no formato: `DD.HH:MM:SS.MMMMMM`. Deve ser positivo e menor que `1000` dias. Este campo é necessário, pois a telemetria de solicitação representa a operação de saudação com início hello e de término de saudação.

## <a name="response-code"></a>Código de resposta

Resultado de uma execução de solicitação. Código de status HTTP para solicitações HTTP. Pode ser um valor `HRESULT` ou um tipo de exceção para outros tipos de solicitação.

Comprimento máximo: 1.024 caracteres

## <a name="success"></a>Sucesso

Indicação de chamada bem-sucedida ou malsucedida. Esse campo é obrigatório. Quando não definir explicitamente muito`false` -solicitação considerado toobe bem-sucedido. Defina esse valor muito`false` se a operação foi interrompida pela exceção ou retornou o código de resultado do erro.

Para aplicativos da web de hello, Application Insights definir solicitações com falha quando o código de resposta de saudação é menos hello `400` ou igual muito`401`. No entanto há casos em que esse mapeamento padrão não corresponde a saudação semântica do aplicativo hello. O código de resposta `404` não pode indicar "nenhum registro", o que pode ser parte do fluxo regular. Ele também pode indicar um link desfeito. Para Olá links quebrados, você ainda pode implementar lógica mais avançada. Você pode marcar links quebrados como falhas somente quando esses links estão localizados no mesmo site analisando referenciador de url de saudação. Ou marcá-los como falhas quando acessado a partir do aplicativo móvel da empresa hello. Da mesma forma `301` e `302` indica falha quando acessado a partir do cliente de saudação que não dá suporte ao redirecionamento.

Conteúdo `206` parcialmente aceito pode indicar uma falha de uma solicitação geral. Por exemplo, o ponto de extremidade do Application Insights recebe um lote de itens de telemetria como uma única solicitação. Ele retorna `206` quando alguns itens no lote de saudação não foram processados com êxito. Taxa de aumento de `206` indica um problema que precisa toobe investigado. Lógica semelhante aplica-se muito`207` Status Múltiplo onde sucesso Olá pode ser Olá pior de códigos de resposta separados.

Você pode ler mais resultados de solicitação no código e o código de status no hello [postagem de blog](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Próximas etapas

- [Escrever uma telemetria de solicitação personalizada](app-insights-api-custom-events-metrics.md#trackrequest)
- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- Saiba como muito[configurar ASP.NET Core](app-insights-asp-net.md) aplicativo com o Application Insights.
- Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.
