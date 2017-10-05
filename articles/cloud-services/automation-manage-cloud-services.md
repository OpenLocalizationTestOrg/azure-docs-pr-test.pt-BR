---
title: "Gerenciar os Serviços de Nuvem do Azure usando a Automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar serviços de nuvem do Azure em grande escala."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="a5071-103">Gerenciamento de Serviços de Nuvem do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="a5071-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="a5071-104">Este guia apresentará o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento de seus serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5071-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="a5071-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="a5071-105">What is Azure Automation?</span></span>
<span data-ttu-id="a5071-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="a5071-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="a5071-107">Com a Automação do Azure, tarefas de execução longa, manuais, propensas a erros e repetidas com frequência podem ser automatizadas para melhorar a confiabilidade, a eficiência e o tempo de implantação para sua organização.</span><span class="sxs-lookup"><span data-stu-id="a5071-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="a5071-108">A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que pode ser dimensionado para atender às suas necessidades à medida que sua organização cresce.</span><span class="sxs-lookup"><span data-stu-id="a5071-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="a5071-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="a5071-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="a5071-110">Reduza o custo operacional e libere a equipe de TI/ DevOps para se concentrar no trabalho que adiciona valor comercial ao transferir as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5071-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="a5071-111">Como a Automação do Azure ajuda a gerenciar os serviços de nuvem do Azure?</span><span class="sxs-lookup"><span data-stu-id="a5071-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="a5071-112">Os serviços de nuvem do Azure podem ser gerenciados na Automação do Azure usando os cmdlets do PowerShell disponíveis em [Ferramentas PowerShell do Azure](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5071-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="a5071-113">A Automação do Azure tem esses cmdlets do PowerShell do serviço de nuvem disponíveis imediatamente para que você possa executar todas as tarefas de gerenciamento do serviço de nuvem no serviço.</span><span class="sxs-lookup"><span data-stu-id="a5071-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="a5071-114">Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets para outros serviços do Azure, para automatizar tarefas complexas nos serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="a5071-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="a5071-115">Entre alguns usos de exemplo da Automação do Azure para gerenciar os Serviços de Nuvem do Azure estão:</span><span class="sxs-lookup"><span data-stu-id="a5071-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="a5071-116">Implantação contínua de um Serviço de Nuvem sempre que cscfg ou cspkg é atualizado no Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a5071-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="a5071-117">Reinicialização das instâncias do Serviço de Nuvem em paralelo, com um domínio de atualização por vez</span><span class="sxs-lookup"><span data-stu-id="a5071-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="a5071-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5071-118">Next Steps</span></span>
<span data-ttu-id="a5071-119">Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para serviços de nuvem do Azure, siga estes links para obter mais informações sobre a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5071-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="a5071-120">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="a5071-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="a5071-121">Meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="a5071-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="a5071-122">Mapa de aprendizagem de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="a5071-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
