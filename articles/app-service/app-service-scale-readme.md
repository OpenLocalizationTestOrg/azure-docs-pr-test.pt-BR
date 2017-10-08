---
title: "Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo"
description: "Saiba Olá vantagens e desvantagens de dimensionamento do aplicativo no serviço de aplicativo."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, escala, escalonável, plano de serviço de aplicativo, custo de serviço de aplicativo"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="8e453-104">Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e453-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="8e453-105">Aplicativos hospedados no Serviço de Aplicativo do Azure podem [chegar a uma escala enorme](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="8e453-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="8e453-106">No entanto, o dimensionamento de um aplicativo é um problema complexo que não tem uma solução que se aplique a todas as situações.</span><span class="sxs-lookup"><span data-stu-id="8e453-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="8e453-107">toocorrectly dimensionar seu aplicativo há 3 áreas principais que contribuirão com êxito de aplicativos tooyour:</span><span class="sxs-lookup"><span data-stu-id="8e453-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="8e453-108">Entender a arquitetura do aplicativo e seus pontos fracos.</span><span class="sxs-lookup"><span data-stu-id="8e453-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="8e453-109">Seu aplicativo é com estado?</span><span class="sxs-lookup"><span data-stu-id="8e453-109">Is your Application Stateful?</span></span> <span data-ttu-id="8e453-110">Sem estado?</span><span class="sxs-lookup"><span data-stu-id="8e453-110">Stateless?</span></span>
   * <span data-ttu-id="8e453-111">O que são todos os componentes de saudação do seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="8e453-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="8e453-112">Onde estão os gargalos de saudação no aplicativo hello?</span><span class="sxs-lookup"><span data-stu-id="8e453-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="8e453-113">Quando a carga for aplicado tooyour aplicativo, o que interromperá primeiro?</span><span class="sxs-lookup"><span data-stu-id="8e453-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="8e453-114">Saudação de Noções básicas sobre esperado requisitos de carga e desempenho.</span><span class="sxs-lookup"><span data-stu-id="8e453-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="8e453-115">Aplicativo hello precisa tooserve mil usuários? ou um milhão?</span><span class="sxs-lookup"><span data-stu-id="8e453-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="8e453-116">O tráfego virá de um único local geográfico ou é global?</span><span class="sxs-lookup"><span data-stu-id="8e453-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="8e453-117">Há variações sazonais? Picos de tráfego?</span><span class="sxs-lookup"><span data-stu-id="8e453-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="8e453-118">Rapidez o aplicativo hello deve responder?</span><span class="sxs-lookup"><span data-stu-id="8e453-118">How fast should hello app respond?</span></span> <span data-ttu-id="8e453-119">1 segundo?</span><span class="sxs-lookup"><span data-stu-id="8e453-119">1 second?</span></span> <span data-ttu-id="8e453-120">1 milissegundo?</span><span class="sxs-lookup"><span data-stu-id="8e453-120">1 millisecond?</span></span>
3. <span data-ttu-id="8e453-121">Noções básicas sobre corretamente aproveite Olá plataforma e hospedagem de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e453-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="8e453-122">O que devem recursos utilizam tooachieve Minhas metas de escala?</span><span class="sxs-lookup"><span data-stu-id="8e453-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="8e453-123">Esta seção ajudará você a entender todos os fatores de saudação e ajuda a planejar uma estratégia que tira proveito dos tooachieve de recursos de serviço de aplicativo necessário Olá suas metas de escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="8e453-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

