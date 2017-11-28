---
title: "Padrões e limites de aaaScheduler"
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
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="97845-103">Limites e padrões do Agendador</span><span class="sxs-lookup"><span data-stu-id="97845-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="97845-104">Aceleradores, limites, padrões e cotas do Agendador</span><span class="sxs-lookup"><span data-stu-id="97845-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="97845-105">Olá x-ms-request-id cabeçalho</span><span class="sxs-lookup"><span data-stu-id="97845-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="97845-106">Cada solicitação feita no hello serviço Agendador retorna um cabeçalho de resposta chamado**x-ms-request-id**. Esse cabeçalho contém um valor opaco que identifica exclusivamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="97845-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="97845-107">Se uma solicitação é consistente com falha e você tiver verificado que solicitação Olá formulada corretamente, você pode usar este tooMicrosoft de erro do valor tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="97845-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="97845-108">Em seu relatório, inclua o valor de saudação de tempo aproximado de saudação do x-ms-request-id, essa solicitação Olá foi feita, Olá identificador de assinatura hello, coleção de trabalhos e/ou trabalho e Olá o tipo de operação que Olá tentativa de solicitação.</span><span class="sxs-lookup"><span data-stu-id="97845-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="97845-109">Consulte também</span><span class="sxs-lookup"><span data-stu-id="97845-109">See Also</span></span>
 [<span data-ttu-id="97845-110">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="97845-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="97845-111">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="97845-112">Começar a usar o Agendador no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="97845-113">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="97845-114">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="97845-115">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="97845-116">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="97845-117">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="97845-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

