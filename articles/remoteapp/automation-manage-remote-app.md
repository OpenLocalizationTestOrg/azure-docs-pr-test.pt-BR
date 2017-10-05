---
title: "Gerenciar Azure RemoteApp usando a Automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar o Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="cb7d5-103">Gerenciando o Azure RemoteApp usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d5-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cb7d5-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cb7d5-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cb7d5-106">Este guia apresentará o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="cb7d5-107">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="cb7d5-107">What is Azure Automation?</span></span>
<span data-ttu-id="cb7d5-108">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="cb7d5-109">Com o uso da Automação do Azure, as tarefas manuais, repetidas com frequência, de execução longa e propensas a erros podem ser automatizadas para aumentar a confiabilidade, a eficiência e o tempo de retorno para sua organização.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="cb7d5-110">A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que é dimensionado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="cb7d5-111">Na Automação do Azure, processos podem ser inicializados manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecem exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="cb7d5-112">Reduza o custo operacional e libere a equipe de TI e DevOps para se concentrar no trabalho que agrega valor de negócios, transferindo as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="cb7d5-113">Como a Automação do Azure ajuda a gerenciar o Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="cb7d5-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="cb7d5-114">O RemoteApp pode ser gerenciado na Automação do Azure usando os cmdlets do PowerShell disponíveis em [Ferramentas PowerShell do Azure](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb7d5-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="cb7d5-115">A Automação do Azure tem esses cmdlets do PowerShell do RemoteApp disponíveis imediatamente para que você possa executar todas as tarefas de gerenciamento do RemoteApp dentro do serviço.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="cb7d5-116">Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets para outros serviços do Azure, para automatizar tarefas complexas nos serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb7d5-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb7d5-117">Next steps</span></span>
<span data-ttu-id="cb7d5-118">Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para gerenciar o Azure RemoteApp, siga estes links para obter mais informações sobre a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d5-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="cb7d5-119">Confira o [Guia de introdução](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="cb7d5-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

