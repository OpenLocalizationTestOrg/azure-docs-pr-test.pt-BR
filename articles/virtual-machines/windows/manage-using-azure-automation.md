---
title: "aaaManage VMs usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage máquinas virtuais do Azure em grande escala."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="fb982-103">Gerenciamento de Máquinas Virtuais do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="fb982-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="fb982-104">Este guia apresenta toohello serviço de automação do Azure e como ele pode ser usado toosimplify gerenciar suas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb982-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="fb982-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="fb982-105">What is Azure Automation?</span></span>
<span data-ttu-id="fb982-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="fb982-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="fb982-107">Usando a automação do Azure, as tarefas de longa execução, manuais, propensas a erros e repetidas com frequência podem ser automatizada tooincrease confiabilidade, a eficiência e o tempo de implantação para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="fb982-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="fb982-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades que sua organização cresce.</span><span class="sxs-lookup"><span data-stu-id="fb982-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="fb982-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="fb982-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="fb982-110">Você pode reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, executando sua nuvem de tarefas de gerenciamento automaticamente com a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb982-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="fb982-111">Como a Automação do Azure pode ajudar a gerenciar máquinas virtuais do Azure?</span><span class="sxs-lookup"><span data-stu-id="fb982-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="fb982-112">As máquinas virtuais podem ser gerenciadas na Automação do Azure usando [PowerShell do Azure](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb982-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="fb982-113">Automação do Azure inclui cmdlets do PowerShell do Azure hello, para que você pode executar todas as suas tarefas de gerenciamento de máquina virtual no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb982-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="fb982-114">Cmdlets de saudação na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados com os serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="fb982-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb982-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb982-115">Next steps</span></span>
<span data-ttu-id="fb982-116">Agora que você aprendeu os fundamentos de saudação de automação do Azure e como ela pode ser usado toomanage máquinas virtuais do Azure, saiba mais:</span><span class="sxs-lookup"><span data-stu-id="fb982-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="fb982-117">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="fb982-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="fb982-118">Meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="fb982-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="fb982-119">Mapa de aprendizagem de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="fb982-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

