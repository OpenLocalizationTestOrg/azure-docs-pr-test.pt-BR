---
title: "aaaManage serviços de nuvem do Azure usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage serviços em nuvem do Azure em grande escala."
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="a42b6-103">Gerenciamento de Serviços de Nuvem do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="a42b6-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="a42b6-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento dos serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="a42b6-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="a42b6-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="a42b6-105">What is Azure Automation?</span></span>
<span data-ttu-id="a42b6-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="a42b6-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="a42b6-107">Tarefas de longa execução, manuais, propensas a erros e repetidas com frequência usando a automação do Azure, podem ser automatizado tooincrease confiabilidade, a eficiência e toovalue de tempo para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="a42b6-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="a42b6-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades que sua organização cresce.</span><span class="sxs-lookup"><span data-stu-id="a42b6-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="a42b6-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="a42b6-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="a42b6-110">Reduzir a sobrecarga operacional e liberar IT / DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a42b6-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="a42b6-111">Como a Automação do Azure ajuda a gerenciar os serviços de nuvem do Azure?</span><span class="sxs-lookup"><span data-stu-id="a42b6-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="a42b6-112">Serviços de nuvem do Azure podem ser gerenciados na automação do Azure usando cmdlets do PowerShell Olá que estão disponíveis no hello [ferramentas do Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="a42b6-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="a42b6-113">Automação do Azure tem esses cmdlets de PowerShell de serviço de nuvem disponíveis fora da caixa hello, para que você possa executar todas as tarefas de gerenciamento de serviço de nuvem no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a42b6-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="a42b6-114">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="a42b6-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="a42b6-115">Alguns exemplos de usos de toomanage de automação do Azure, que serviços de nuvem do Azure incluem:</span><span class="sxs-lookup"><span data-stu-id="a42b6-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="a42b6-116">Implantação contínua de um Serviço de Nuvem sempre que cscfg ou cspkg é atualizado no Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a42b6-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="a42b6-117">Reinicialização das instâncias do Serviço de Nuvem em paralelo, com um domínio de atualização por vez</span><span class="sxs-lookup"><span data-stu-id="a42b6-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="a42b6-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a42b6-118">Next Steps</span></span>
<span data-ttu-id="a42b6-119">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage serviços em nuvem do Azure, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a42b6-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="a42b6-120">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="a42b6-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="a42b6-121">Meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="a42b6-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="a42b6-122">Mapa de aprendizagem de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="a42b6-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
