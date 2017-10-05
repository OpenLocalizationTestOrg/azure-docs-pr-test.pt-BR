---
title: "Gerenciar aplicativo Web do Azure usando a Automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar o Aplicativo Web do Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="332a0-103">Gerenciando o Aplicativo Web do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="332a0-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="332a0-104">Este guia apresentará o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento do Aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="332a0-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="332a0-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="332a0-105">What is Azure Automation?</span></span>
<span data-ttu-id="332a0-106">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="332a0-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="332a0-107">Com o uso da Automação do Azure, as tarefas manuais, repetidas, de execução longa e propensas a erros podem ser automatizadas para aumentar a confiabilidade, a eficiência e o tempo de retorno para sua organização.</span><span class="sxs-lookup"><span data-stu-id="332a0-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="332a0-108">A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que é dimensionado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="332a0-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="332a0-109">Na Automação do Azure, processos podem ser inicializados manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecem exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="332a0-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="332a0-110">Reduza o custo operacional e libere a equipe de TI e DevOps para se concentrar no trabalho que agrega valor de negócios, transferindo as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="332a0-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="332a0-111">Como a Automação do Azure ajuda a gerenciar o Aplicativo Web do Azure?</span><span class="sxs-lookup"><span data-stu-id="332a0-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="332a0-112">O aplicativo Web pode ser gerenciado na Automação do Azure usando os cmdlets do PowerShell que estão disponíveis em [Módulos do Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="332a0-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="332a0-113">Você pode [instalar esses cmdlets do PowerShell do aplicativo Web na Automação do Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), de modo que você pode executar todas as tarefas de gerenciamento de aplicativo Web no serviço.</span><span class="sxs-lookup"><span data-stu-id="332a0-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="332a0-114">Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets de outros serviços do Azure para automatizar tarefas complexas em serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="332a0-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="332a0-115">Aqui estão alguns exemplos de Serviços de Aplicativos com a automação de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="332a0-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="332a0-116">Scripts para gerenciar os Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="332a0-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="332a0-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="332a0-117">Next steps</span></span>
<span data-ttu-id="332a0-118">Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para gerenciar o Aplicativo Web do Azure, siga estes links para obter mais informações sobre a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="332a0-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="332a0-119">Confira o [Guia de introdução](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="332a0-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

