---
title: "aaaWhat é o Agendador do Azure? | Microsoft Docs"
description: "O Agendador do Azure permite que você toodeclaratively descrevem ações toorun na nuvem hello. Em seguida, ele agenda e executa essas ações automaticamente."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="3dcfa-105">O que é o Agendador do Azure?</span><span class="sxs-lookup"><span data-stu-id="3dcfa-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="3dcfa-106">O Agendador do Azure permite que você toodeclaratively descrevem ações toorun na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="3dcfa-107">Em seguida, ele agenda e executa essas ações automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="3dcfa-108">Faz isso usando [Olá portal do Azure](scheduler-get-started-portal.md), código, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="3dcfa-109">O Agendador cria, mantém e invoca o trabalho agendado.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="3dcfa-110">O Agendador não hospeda qualquer carga de trabalho ou executar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="3dcfa-111">Ele apenas *invoca* código hospedado em outro lugar—no Azure, no local ou em outro provedor.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="3dcfa-112">Ele invoca via HTTP, HTTPS, uma fila de armazenamento, uma fila do barramento de serviço ou um tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="3dcfa-113">Agendas de Agendador [trabalhos](scheduler-concepts-terms.md), mantém um histórico dos resultados da execução de trabalho que um pode examinar e forma determinista e confiável executar agendas toobe de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="3dcfa-114">WebJobs do Azure (parte do recurso de aplicativos Web Olá no serviço de aplicativo do Azure) e outros recursos de agendamento do Azure usam o Agendador no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="3dcfa-115">Olá [API REST do Agendador](https://msdn.microsoft.com/library/mt629143.aspx) ajuda a gerenciar a comunicação Olá para essas ações.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="3dcfa-116">Dessa forma, o Agendador oferece suporte para [agendas complexas e recorrência avançadas](scheduler-advanced-complexity.md) facilmente.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="3dcfa-117">Há vários cenários que se prestam toohello uso do Agendador.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="3dcfa-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3dcfa-118">For example:</span></span>

* <span data-ttu-id="3dcfa-119">*Ações do aplicativo recorrente* : coleta periódica de dados do Twitter no feed.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="3dcfa-120">*Manutenção diária:* redução diária de logs, realização de backups e outras tarefas de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="3dcfa-121">Por exemplo, um administrador pode escolher tooback o banco de dados de saudação à 1:00 A.M.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="3dcfa-122">todos os dias para Olá próximos nove meses.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-122">every day for hello next nine months.</span></span>

<span data-ttu-id="3dcfa-123">Agendador permite toocreate, atualizar, excluir, exibir e gerenciar trabalhos e [coleções de trabalhos](scheduler-concepts-terms.md) programaticamente, usando scripts e no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dcfa-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="3dcfa-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3dcfa-124">See also</span></span>
 [<span data-ttu-id="3dcfa-125">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="3dcfa-126">Começar a usar o Agendador no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="3dcfa-127">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="3dcfa-128">Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="3dcfa-129">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="3dcfa-130">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="3dcfa-131">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="3dcfa-132">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="3dcfa-133">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="3dcfa-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

