---
title: aaaAzure modelo de dados de telemetria do Application Insights - contexto de telemetria | Microsoft Docs
description: Modelo de dados de contexto do Application Insights Telemetry
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Contexto de telemetria: modelo de dados do Application Insights

Cada item de telemetria pode ter campos de contexto fortemente tipados. Cada campo habilita um cenário de monitoramento específico. Use Olá propriedades personalizadas coleção toostore personalizados ou específicos ao aplicativo informações contextuais.


##<a name="application-version"></a>Versão do aplicativo

As informações nos campos de contexto de aplicativo hello estão sempre sobre o aplicativo hello que está enviando a telemetria de saudação. Versão do aplicativo é usado tooanalyze tendência alterações no comportamento do aplicativo hello e suas implantações de toohello de correlação.

Comprimento máximo: 1024


##<a name="client-ip-address"></a>Endereço IP do cliente

endereço IP Olá Olá de dispositivo de cliente. Há suporte para IPv4 e IPv6. Quando a telemetria é enviada de um serviço, o contexto de local de Olá é sobre o usuário Olá que iniciou a operação Olá no serviço de saudação. Extrair informações de localização geográfica de saudação do IP do cliente de saudação do Application Insights e, em seguida, Trunque-o. Portanto, o IP do cliente por si só não pode ser usado como informações de identificação do usuário final. 

Comprimento máximo: 46


##<a name="device-type"></a>Tipo de dispositivo

Esse campo foi usado originalmente tooindicate Olá tipo de usuário do hello dispositivo Olá final do aplicativo hello está sendo usado. Hoje usado principalmente telemetria de JavaScript toodistinguish com hello dispositivo tipo 'Browser' de telemetria do lado do servidor com o tipo de dispositivo de saudação 'Computador'.

Comprimento máximo: 64


##<a name="operation-id"></a>ID da operação

Um identificador exclusivo da operação de raiz de saudação. Esse identificador permite toogroup telemetria entre vários componentes. Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes. id da operação Olá é criado por uma solicitação ou um modo de exibição de página. Todos os outros telemetria define o valor deste campo toohello para Olá que contém a exibição de página ou solicitação. 

Comprimento máximo: 128


##<a name="parent-operation-id"></a>ID de operação pai

Olá identificador exclusivo do pai imediato do item de telemetria hello. Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes.

Comprimento máximo: 128


##<a name="operation-name"></a>Nome da operação

nome da saudação (grupo) da operação de saudação. nome da operação Olá é criado por uma solicitação ou um modo de exibição de página. Todos os outros itens de telemetria definir esse valor de toohello de campo para Olá que contém o modo de solicitação ou de página. Nome da operação é usado para localizar todos os itens de telemetria Olá para um grupo de operações (por exemplo ' inicial de GET/Index'). Essa propriedade de contexto é usado tooanswer perguntas como "quais são exceções típico de saudação geradas nesta página."

Comprimento máximo: 1024


##<a name="synthetic-source-of-hello-operation"></a>Sintética fonte da operação de saudação

Nome da origem sintética. Alguns telemetria do aplicativo hello pode representar o tráfego sintético. Pode ser o site da web hello, indexação rastreador, testes de disponibilidade do site ou rastreamentos de diagnósticos bibliotecas como o SDK do Application Insights em si.

Comprimento máximo: 1024


##<a name="session-id"></a>Id da sessão

ID de sessão - instância Olá Olá de interação do usuário com o aplicativo hello. As informações nos campos de contexto de sessão Olá estão sempre sobre o usuário final de saudação. Quando a telemetria é enviada de um serviço, contexto de sessão Olá é sobre o usuário Olá que iniciou a operação Olá no serviço de saudação.

Comprimento máximo: 64


##<a name="anonymous-user-id"></a>Id de usuário anônimo

Id de usuário anônimo. Representa o usuário final de saudação do aplicativo hello. Quando a telemetria é enviada de um serviço, o contexto de usuário de saudação está sobre o usuário Olá que iniciou a operação Olá no serviço de saudação.

[Amostragem](app-insights-sampling.md) é um valor de saudação do hello técnicas toominimize de telemetria coletada. Exemplo in ou out Olá todos os tooeither de tentativas de algoritmo de amostragem correlacionados telemetria. A id de usuário anônimo é usado para a geração de pontuação de amostragem. A id de usuário anônimo deve ser um valor suficientemente aleatório. 

Usar o nome de usuário de toostore de id de usuário anônimo é um uso indevido do campo hello. Usar id de usuário Autenticado.

Comprimento máximo: 128


##<a name="authenticated-user-id"></a>Id de usuário autenticado

Id de usuário autenticado. Olá oposta da id de usuário anônimo, este campo representa o usuário Olá com um nome amigável. As informações de PII não são coletadas por padrão pela maioria dos SDKs.

Comprimento máximo: 1024


##<a name="account-id"></a>Id de conta

Em aplicativos de multilocação é Olá ID da conta ou nome de usuário hello está agindo com. Exemplos podem ser a ID da assinatura do Portal do Azure ou a plataforma de blogs de nome de blog.

Comprimento máximo: 1024


##<a name="cloud-role"></a>Função de nuvem

Nome do aplicativo de saudação do hello função é uma parte do. Mapeia diretamente toohello nome da função no azure. Também é possível toodistinguish usado micro serviços, que fazem parte de um único aplicativo.

Comprimento máximo: 256


##<a name="cloud-role-instance"></a>Instância de função de nuvem

Nome da instância de saudação onde o aplicativo hello está sendo executado. Nome do computador para o nome de instância local do Azure.

Comprimento máximo: 256


##<a name="internal-sdk-version"></a>Interno: versão de SDK

Versão do SDK. Veja https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para saber mais.

Comprimento máximo: 64


##<a name="internal-node-name"></a>Interno: nome do nó

Este campo representa o nome do nó Olá usado para fins de cobrança. Use-toooverride saudação padrão a detecção de nós.

Comprimento máximo: 256


## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[estender e filtrar telemetria](app-insights-api-filtering-sampling.md).
- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- Confira a coleção de propriedades de contexto padrão [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).
