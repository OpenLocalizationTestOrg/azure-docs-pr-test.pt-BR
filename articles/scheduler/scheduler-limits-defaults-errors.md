---
title: "Limites e padrões do Agendador"
description: "Limites e padrões do Agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="a10d2-103">Limites e padrões do Agendador</span><span class="sxs-lookup"><span data-stu-id="a10d2-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="a10d2-104">Aceleradores, limites, padrões e cotas do Agendador</span><span class="sxs-lookup"><span data-stu-id="a10d2-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="a10d2-105">O cabeçalho x-ms-request-id</span><span class="sxs-lookup"><span data-stu-id="a10d2-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="a10d2-106">Cada solicitação feita no serviço de Agendador retorna um cabeçalho de resposta chamado**x-ms-request-id**.</span><span class="sxs-lookup"><span data-stu-id="a10d2-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="a10d2-107">Esse cabeçalho contém um valor opaco que identifica exclusivamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="a10d2-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="a10d2-108">Se uma solicitação estiver falhando consistentemente e você tiver verificado que a solicitação foi formulada corretamente, você poderá usar esse valor para relatar o erro à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a10d2-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="a10d2-109">Em seu relatório, inclua o valor de x-ms-request-id, a hora aproximada na qual a solicitação foi feita, o identificador da assinatura, a coleção de trabalhos e/ou o trabalho e o tipo de operação para o qual a solicitação realizou uma tentativa.</span><span class="sxs-lookup"><span data-stu-id="a10d2-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="a10d2-110">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a10d2-110">See Also</span></span>
 [<span data-ttu-id="a10d2-111">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="a10d2-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="a10d2-112">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="a10d2-113">Introdução à utilização do Agendador no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a10d2-114">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a10d2-115">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a10d2-116">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a10d2-117">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a10d2-118">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a10d2-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

