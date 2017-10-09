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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="aa396-103">Uso de tooenable de contexto de usuário envio experiências no Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa396-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="aa396-104">Acompanhamento de usuários</span><span class="sxs-lookup"><span data-stu-id="aa396-104">Tracking users</span></span>

<span data-ttu-id="aa396-105">Permite que você toomonitor do Application Insights e controlar seus usuários por meio de um conjunto de ferramentas de uso do produto:</span><span class="sxs-lookup"><span data-stu-id="aa396-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="aa396-106">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="aa396-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="aa396-107">Funis</span><span class="sxs-lookup"><span data-stu-id="aa396-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="aa396-108">Retenção</span><span class="sxs-lookup"><span data-stu-id="aa396-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="aa396-109">Coortes</span><span class="sxs-lookup"><span data-stu-id="aa396-109">Cohorts</span></span>
* [<span data-ttu-id="aa396-110">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="aa396-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="aa396-111">Em ordem tootrack de que um usuário faz ao longo do tempo, Application Insights precisa de uma ID para cada usuário ou sessão.</span><span class="sxs-lookup"><span data-stu-id="aa396-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="aa396-112">Inclua essas IDs em cada exibição de página ou evento personalizado.</span><span class="sxs-lookup"><span data-stu-id="aa396-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="aa396-113">Usuários, Funis, Retenção e Coortes: inclua a ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="aa396-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="aa396-114">Sessões: inclua a ID da sessão.</span><span class="sxs-lookup"><span data-stu-id="aa396-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="aa396-115">Se seu aplicativo estiver integrado com hello [SDK de JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), usuário ID é rastreado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa396-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="aa396-116">Escolher as IDs de usuário</span><span class="sxs-lookup"><span data-stu-id="aa396-116">Choosing user IDs</span></span>

<span data-ttu-id="aa396-117">As IDs de usuário devem persistir em tootrack de sessões de usuário, como os usuários se comportam ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="aa396-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="aa396-118">Há várias abordagens para a ID de saudação persistentes.</span><span class="sxs-lookup"><span data-stu-id="aa396-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="aa396-119">Uma definição de um usuário que você já tem em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="aa396-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="aa396-120">Se o serviço de saudação tem acesso tooa navegador, ele pode passar o navegador Olá um cookie com uma ID nele.</span><span class="sxs-lookup"><span data-stu-id="aa396-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="aa396-121">Olá ID será mantido para como cookie Olá permanece no navegador do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="aa396-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="aa396-122">Se necessário, você pode usar uma nova ID de cada sessão, mas os resultados Olá sobre usuários será limitados.</span><span class="sxs-lookup"><span data-stu-id="aa396-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="aa396-123">Por exemplo, você não será capaz de toosee como o comportamento do usuário é alterado ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="aa396-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="aa396-124">Olá ID deve ser um Guid ou outra cadeia de caracteres complexa o bastante tooidentify cada usuário exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="aa396-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="aa396-125">Por exemplo, poderia ser um número aleatório comprido.</span><span class="sxs-lookup"><span data-stu-id="aa396-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="aa396-126">Se Olá ID contém informações de identificação pessoal sobre o usuário hello, não é tooApplication de toosend um valor apropriado Insights como um ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="aa396-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="aa396-127">Você pode enviar tal ID como um [autenticado a ID de usuário](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), mas não preenche o requisito de ID de usuário Olá para cenários de uso.</span><span class="sxs-lookup"><span data-stu-id="aa396-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="aa396-128">Aplicativos ASP .NET: definir o contexto de usuário em um ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="aa396-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="aa396-129">Criar um inicializador de telemetria, conforme descrito em detalhes [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)e defina Olá Context.User.Id e Olá Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="aa396-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="aa396-130">Este exemplo define o identificador tooan de ID de usuário de saudação que expira após Olá sessão.</span><span class="sxs-lookup"><span data-stu-id="aa396-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="aa396-131">Se possível, use uma ID de usuário que persiste entre as sessões.</span><span class="sxs-lookup"><span data-stu-id="aa396-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="aa396-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="aa396-132">*C#*</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="aa396-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa396-133">Next steps</span></span>
- <span data-ttu-id="aa396-134">uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="aa396-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="aa396-135">Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="aa396-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="aa396-136">Visão geral do uso</span><span class="sxs-lookup"><span data-stu-id="aa396-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="aa396-137">Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="aa396-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="aa396-138">Funis</span><span class="sxs-lookup"><span data-stu-id="aa396-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="aa396-139">Retenção</span><span class="sxs-lookup"><span data-stu-id="aa396-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="aa396-140">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="aa396-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
