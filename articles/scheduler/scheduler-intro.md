---
title: "O que é o Agendador do Azure? | Microsoft Docs"
description: "O Agendador do Azure permite que você descreva declarativamente ações a serem executadas na nuvem. Em seguida, ele agenda e executa essas ações automaticamente."
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
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="a1183-105">O que é o Agendador do Azure?</span><span class="sxs-lookup"><span data-stu-id="a1183-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="a1183-106">O Agendador do Azure permite que você descreva declarativamente ações a serem executadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a1183-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="a1183-107">Em seguida, ele agenda e executa essas ações automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a1183-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="a1183-108">O Agendador do Azure faz isso usando o [portal do Azure](scheduler-get-started-portal.md), código, a [API REST](https://msdn.microsoft.com/library/mt629143.aspx) ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1183-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="a1183-109">O Agendador cria, mantém e invoca o trabalho agendado.</span><span class="sxs-lookup"><span data-stu-id="a1183-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="a1183-110">O Agendador não hospeda qualquer carga de trabalho ou executar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="a1183-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="a1183-111">Ele apenas *invoca* código hospedado em outro lugar—no Azure, no local ou em outro provedor.</span><span class="sxs-lookup"><span data-stu-id="a1183-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="a1183-112">Ele invoca via HTTP, HTTPS, uma fila de armazenamento, uma fila do barramento de serviço ou um tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="a1183-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="a1183-113">O Agendador agenda [trabalhos](scheduler-concepts-terms.md), mantém um histórico do trabalho de resultados de execução que alguém pode revisar, e agenda de forma determinista e confiável agenda cargas de trabalho a serem executadas.</span><span class="sxs-lookup"><span data-stu-id="a1183-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="a1183-114">Trabalhos Web do Azure (parte do recurso de aplicativos Web no serviço de aplicativo do Azure) e outro recursos de agendamento do Azure usam o Agendador em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a1183-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="a1183-115">A [API REST do Agendador](https://msdn.microsoft.com/library/mt629143.aspx) ajuda a gerenciar a comunicação para essas ações.</span><span class="sxs-lookup"><span data-stu-id="a1183-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="a1183-116">Dessa forma, o Agendador oferece suporte para [agendas complexas e recorrência avançadas](scheduler-advanced-complexity.md) facilmente.</span><span class="sxs-lookup"><span data-stu-id="a1183-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="a1183-117">Há vários cenários em que o Agendador pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="a1183-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="a1183-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1183-118">For example:</span></span>

* <span data-ttu-id="a1183-119">*Ações do aplicativo recorrente* : coleta periódica de dados do Twitter no feed.</span><span class="sxs-lookup"><span data-stu-id="a1183-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="a1183-120">*Manutenção diária:* redução diária de logs, realização de backups e outras tarefas de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a1183-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="a1183-121">Por exemplo, um administrador pode escolher realizar o backup de seu banco de dados à 1h da manhã, todos os dias, pelos próximos nove meses.</span><span class="sxs-lookup"><span data-stu-id="a1183-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="a1183-122">todos os dias nos próximos nove meses.</span><span class="sxs-lookup"><span data-stu-id="a1183-122">every day for the next nine months.</span></span>

<span data-ttu-id="a1183-123">O Agendador permite criar, atualizar, excluir, exibir e gerenciar trabalhos e [coleções de trabalhos](scheduler-concepts-terms.md) programaticamente, usando scripts e no portal.</span><span class="sxs-lookup"><span data-stu-id="a1183-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="a1183-124">Confira também</span><span class="sxs-lookup"><span data-stu-id="a1183-124">See also</span></span>
 [<span data-ttu-id="a1183-125">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="a1183-126">Introdução à utilização do Agendador no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a1183-127">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a1183-128">Como criar agendas complexas e recorrência avançada com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="a1183-129">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a1183-130">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a1183-131">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a1183-132">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="a1183-133">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="a1183-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

