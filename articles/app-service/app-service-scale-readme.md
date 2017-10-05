---
title: "Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo"
description: "Saiba as vantagens e desvantagens do dimensionamento do aplicativo no Serviço de Aplicativo."
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
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="3cf58-104">Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="3cf58-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="3cf58-105">Aplicativos hospedados no Serviço de Aplicativo do Azure podem [chegar a uma escala enorme](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="3cf58-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="3cf58-106">No entanto, o dimensionamento de um aplicativo é um problema complexo que não tem uma solução que se aplique a todas as situações.</span><span class="sxs-lookup"><span data-stu-id="3cf58-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="3cf58-107">Para dimensionar corretamente o aplicativo, há três áreas principais que contribuirão para o sucesso do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="3cf58-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="3cf58-108">Entender a arquitetura do aplicativo e seus pontos fracos.</span><span class="sxs-lookup"><span data-stu-id="3cf58-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="3cf58-109">Seu aplicativo é com estado?</span><span class="sxs-lookup"><span data-stu-id="3cf58-109">Is your Application Stateful?</span></span> <span data-ttu-id="3cf58-110">Sem estado?</span><span class="sxs-lookup"><span data-stu-id="3cf58-110">Stateless?</span></span>
   * <span data-ttu-id="3cf58-111">O que são todos os componentes do seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="3cf58-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="3cf58-112">Onde estão os gargalos no aplicativo?</span><span class="sxs-lookup"><span data-stu-id="3cf58-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="3cf58-113">Quando a carga é aplicada ao seu aplicativo, o que será interrompido primeiro?</span><span class="sxs-lookup"><span data-stu-id="3cf58-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="3cf58-114">Entender os requisitos de desempenho e carga esperados.</span><span class="sxs-lookup"><span data-stu-id="3cf58-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="3cf58-115">O aplicativo precisa atender mil usuários? Ou um milhão?</span><span class="sxs-lookup"><span data-stu-id="3cf58-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="3cf58-116">O tráfego virá de um único local geográfico ou é global?</span><span class="sxs-lookup"><span data-stu-id="3cf58-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="3cf58-117">Há variações sazonais? Picos de tráfego?</span><span class="sxs-lookup"><span data-stu-id="3cf58-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="3cf58-118">Com que rapidez o aplicativo deve responder?</span><span class="sxs-lookup"><span data-stu-id="3cf58-118">How fast should the app respond?</span></span> <span data-ttu-id="3cf58-119">1 segundo?</span><span class="sxs-lookup"><span data-stu-id="3cf58-119">1 second?</span></span> <span data-ttu-id="3cf58-120">1 milissegundo?</span><span class="sxs-lookup"><span data-stu-id="3cf58-120">1 millisecond?</span></span>
3. <span data-ttu-id="3cf58-121">Entender e aproveitar corretamente a plataforma de hospedagem de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3cf58-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="3cf58-122">Quais recursos devo aproveitar para alcançar meus objetivos de escala?</span><span class="sxs-lookup"><span data-stu-id="3cf58-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="3cf58-123">Esta seção o ajudará a entender todos os fatores e ajudá-lo a conceber uma estratégia que aproveita os recursos do Serviço de Aplicativo necessários para atingir suas metas de escalabilidade do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3cf58-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

