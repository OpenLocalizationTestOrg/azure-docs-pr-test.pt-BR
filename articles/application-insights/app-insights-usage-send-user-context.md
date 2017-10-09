---
title: "uso de tooenable de contexto de usuário aaaSending experiências no Azure Application Insights | Microsoft Docs"
description: "Controle como os usuários navegam pelo serviço depois de atribuir a cada um de uma cadeia de identificação exclusiva e persistente no Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Uso de tooenable de contexto de usuário envio experiências no Azure Application Insights

## <a name="tracking-users"></a>Acompanhamento de usuários

Permite que você toomonitor do Application Insights e controlar seus usuários por meio de um conjunto de ferramentas de uso do produto: 
* [Usuários, Sessões, Eventos](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Funis](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Retenção](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Coortes
* [Pastas de trabalho](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

Em ordem tootrack de que um usuário faz ao longo do tempo, Application Insights precisa de uma ID para cada usuário ou sessão. Inclua essas IDs em cada exibição de página ou evento personalizado.
- Usuários, Funis, Retenção e Coortes: inclua a ID de usuário.
- Sessões: inclua a ID da sessão.

Se seu aplicativo estiver integrado com hello [SDK de JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), usuário ID é rastreado automaticamente.

## <a name="choosing-user-ids"></a>Escolher as IDs de usuário

As IDs de usuário devem persistir em tootrack de sessões de usuário, como os usuários se comportam ao longo do tempo. Há várias abordagens para a ID de saudação persistentes.
- Uma definição de um usuário que você já tem em seu serviço.
- Se o serviço de saudação tem acesso tooa navegador, ele pode passar o navegador Olá um cookie com uma ID nele. Olá ID será mantido para como cookie Olá permanece no navegador do usuário hello.
- Se necessário, você pode usar uma nova ID de cada sessão, mas os resultados Olá sobre usuários será limitados. Por exemplo, você não será capaz de toosee como o comportamento do usuário é alterado ao longo do tempo.

Olá ID deve ser um Guid ou outra cadeia de caracteres complexa o bastante tooidentify cada usuário exclusivamente. Por exemplo, poderia ser um número aleatório comprido.

Se Olá ID contém informações de identificação pessoal sobre o usuário hello, não é tooApplication de toosend um valor apropriado Insights como um ID de usuário. Você pode enviar tal ID como um [autenticado a ID de usuário](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), mas não preenche o requisito de ID de usuário Olá para cenários de uso.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>Aplicativos ASP .NET: definir o contexto de usuário em um ITelemetryInitializer

Criar um inicializador de telemetria, conforme descrito em detalhes [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)e defina Olá Context.User.Id e Olá Context.Session.Id.

Este exemplo define o identificador tooan de ID de usuário de saudação que expira após Olá sessão. Se possível, use uma ID de usuário que persiste entre as sessões.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Próximas etapas
- uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.
    * [Visão geral do uso](app-insights-usage-overview.md)
    * [Usuários, Sessões e Eventos](app-insights-usage-segmentation.md)
    * [Funis](usage-funnels.md)
    * [Retenção](app-insights-usage-retention.md)
    * [Pastas de trabalho](app-insights-usage-workbooks.md)
