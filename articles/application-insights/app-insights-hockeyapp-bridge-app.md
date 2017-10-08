---
title: aaaExploring HockeyApp dados no Azure Application Insights | Microsoft Docs
description: Analise o uso e o desempenho de seu aplicativo do Azure com o Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Exploração de dados do HockeyApp no Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) Olá recomenda plataforma para monitoramento de aplicativos móveis e desktop ao vivo. Do HockeyApp, você pode enviar personalizado e uso de toomonitor de telemetria de rastreamento e auxiliar no diagnóstico (em adição toogetting falha de dados). Este fluxo de telemetria pode ser consultado usando Olá poderoso [análise](app-insights-analytics.md) recurso de [Azure Application Insights](app-insights-overview.md). Além disso, você pode [exportar hello personalizado e telemetria de rastreamento](app-insights-export-telemetry.md). tooenable esses recursos, você configurar uma ponte que retransmite HockeyApp dados personalizados tooApplication Insights.

## <a name="hello-hockeyapp-bridge-app"></a>aplicativo de ponte HockeyApp Olá
Olá HockeyApp ponte aplicativo é Olá dos principais recursos que permite que você tooaccess o HockeyApp personalizado e telemetria de rastreamento no Application Insights por meio de saudação análise e os recursos de exportação contínua. Eventos de rastreamento e personalizados coletados por HockeyApp após a criação de saudação do hello HockeyApp ponte aplicativo poderá ser acessados desses recursos. Vamos ver como tooset um desses aplicativos de ponte.

No HockeyApp, abra Configurações de Conta, [Tokens de API](https://rink.hockeyapp.net/manage/auth_tokens). Crie um novo token ou reutilize um existente. direitos mínimos Olá necessárias são "somente leitura". Faça uma cópia da saudação API token.

![Obter um token da API do HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Portal do Microsoft Azure Olá aberto e [criar um recurso do Application Insights](app-insights-create-new-resource.md). Defina o tipo de aplicativo muito "Aplicativo de ponte HockeyApp":

![Novo recurso do Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Não é necessário tooset um nome - isso será definido automaticamente do nome do HockeyApp hello.

Olá HockeyApp ponte campos são exibidos. 

![Inserir campos de ponte](./media/app-insights-hockeyapp-bridge-app/03.png)

Insira o token do HockeyApp Olá que você anotou anteriormente. Essa ação preenche o menu de lista suspensa "HockeyApp aplicativo" hello com todos os seus aplicativos de HockeyApp. Selecione Olá um deseja toouse e restante Olá completa dos campos de saudação. 

Abra o novo recurso de saudação. 

Observe que os dados de saudação leva um tempo toostart fluindo.

![Recurso do Application Insights aguardando os dados](./media/app-insights-hockeyapp-bridge-app/04.png)

É isso! Dados de rastreamento e personalizados coletados em seu aplicativo instrumentado HockeyApp daqui em diante agora também estão tooyou disponível no hello análise e recursos de exportação contínua do Application Insights.

Vamos examinar rapidamente cada um desses tooyou de recursos agora disponíveis.

## <a name="analytics"></a>Análise
Análise é uma ferramenta poderosa para ad-hoc consultar seus dados, permitindo que você toodiagnose e analisar a telemetria e rapidamente descobre padrões e causas raiz.

![Análise](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Saiba mais sobre o Analytics](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Exportação contínua
A exportação contínua permite tooexport seus dados em um contêiner de armazenamento de BLOBs do Azure. Isso é muito útil se você precisar tookeep seus dados por mais de um período de retenção Olá oferecido atualmente pelo Application Insights. Você pode manter dados saudação no armazenamento de blob, processá-lo em um banco de dados SQL ou seu preferencial solução do data warehouse.

[Saiba mais sobre a Exportação Contínua](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Próximas etapas
* [Aplique a análise de dados de tooyour](app-insights-analytics-tour.md)

