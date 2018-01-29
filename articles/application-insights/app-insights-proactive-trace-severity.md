---
title: "Detecção Inteligente - Degradação na taxa de gravidade de rastreamento, no Azure Application Insights | Microsoft Docs"
description: "Monitore os rastreamentos de aplicativo com o Azure Application Insights para padrões incomuns na telemetria de rastreamento."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: mbullwin
ms.openlocfilehash: 29ed195dadb7230df425d6d981a0a482e09ee79f
ms.sourcegitcommit: 42ee5ea09d9684ed7a71e7974ceb141d525361c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/09/2017
---
# <a name="degradation-in-trace-severity-ratio-preview"></a>Degradação na taxa de gravidade de rastreamento (visualização)

Os rastreamentos são amplamente usados em aplicativos, porque ajudam a contar a história do que acontece nos bastidores. Quando as coisas não dão certo, os rastreamentos fornecem visibilidade crucial da sequência de eventos que acarretam o estado indesejado. Embora os rastreamentos sejam geralmente não estruturados, há algo que pode ser aprendido concretamente com eles – o nível de gravidade. No estado estável de um aplicativo, esperaríamos que a taxa entre rastreamentos “bons” (*Informações* e *Detalhado*) e “ruins” (*Aviso*, *Erro* e *Crítico*) permanecesse estável. A suposição é de que os rastreamentos “ruins” possam ocorrer regularmente até determinado ponto por causa de vários motivos (problemas de rede transitórios, por exemplo). Mas, quando começa a crescer, um problema real geralmente se manifesta como um aumento na proporção relativa de rastreamentos “bons” X “ruins”. O Application Insights Smart Detection analisa automaticamente os rastreamentos registrados pelo aplicativo e pode avisar você sobre padrões incomuns na gravidade da telemetria de rastreamento.

Este recurso não exige configuração especial, além de configurar o registro em log de rastreamento para o aplicativo (veja como configurar um ouvinte de log de rastreamento para [.NET](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-trace-logs) ou [Java](https://docs.microsoft.com/azure/application-insights/app-insights-java-trace-logs)). Ele permanece ativo quando o aplicativo gera telemetria de exceção suficiente.

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a>Quando eu receberia este tipo de notificação de detecção inteligente?
Você poderá receber esse tipo de notificação se a taxa entre rastreamentos “bons” (rastreamentos registrados com um nível de *informações* ou *detalhado*) e “ruins” (rastreamentos registrados com um nível de *aviso*, *erro ou *fatal*) estiver caindo em um dia específico, em comparação com uma linha de base calculada nos sete dias anteriores.

## <a name="does-my-app-definitely-have-a-problem"></a>Meu aplicativo definitivamente tem um problema?
Não, uma notificação não significa que seu aplicativo definitivamente tem um problema. Embora uma degradação na taxa entre rastreamentos “bons” e “ruins” possa indicar um problema no aplicativo, essa alteração na taxa pode ser benigna. Por exemplo, o aumento pode ser devido a um fluxo de novo no aplicativo emitindo mais rastreamentos “ruins” do que fluxos existentes).

## <a name="how-do-i-fix-it"></a>Como corrigi-la?
As notificações incluem informações de diagnóstico para oferecer suporte no processo de diagnóstico:
1. **Triagem.** A notificação mostra quantas operações foram afetadas. Isso pode ajudá-lo a atribuir uma prioridade ao problema.
2. **Escopo.** O problema está afetando todo o tráfego ou apenas algumas operações? Essas informações podem ser obtidas na notificação.
3. **Diagnosticar.** Você pode usar os itens e os relatórios relacionados às informações de suporte para ajudar a diagnosticar o problema.


