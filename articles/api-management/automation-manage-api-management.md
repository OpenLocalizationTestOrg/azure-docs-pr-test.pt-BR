---
title: "Gerenciar o Gerenciamento de API do Azure usando a Automação do Azure"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar o Gerenciamento de API do Azure."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="fd05b-103">Gerenciando o Gerenciamento de API do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="fd05b-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="fd05b-104">Este guia apresentará o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fd05b-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="fd05b-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="fd05b-105">What is Azure Automation?</span></span>
<span data-ttu-id="fd05b-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="fd05b-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="fd05b-107">Com o uso da Automação do Azure, as tarefas manuais, repetidas, de execução longa e propensas a erros podem ser automatizadas para aumentar a confiabilidade, a eficiência e o tempo de retorno para sua organização.</span><span class="sxs-lookup"><span data-stu-id="fd05b-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="fd05b-108">A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que é dimensionado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="fd05b-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="fd05b-109">Na Automação do Azure, processos podem ser inicializados manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecem exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="fd05b-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="fd05b-110">Reduza o custo operacional e libere a equipe de TI e DevOps para se concentrar no trabalho que agrega valor de negócios, transferindo as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd05b-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="fd05b-111">Como a Automação do Azure ajudar a gerenciar o Gerenciamento de API?</span><span class="sxs-lookup"><span data-stu-id="fd05b-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="fd05b-112">O Gerenciamento de API pode ser gerenciado na Automação do Azure usando a [cmdlets do Windows PowerShell para a API de Gerenciamento de API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="fd05b-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="fd05b-113">Dentro de Automação do Azure, você pode escrever scripts de fluxo de trabalho do PowerShell para executar muitas de suas tarefas de Gerenciamento de API usando os cmdlets.</span><span class="sxs-lookup"><span data-stu-id="fd05b-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="fd05b-114">Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets para outros serviços do Azure, para automatizar tarefas complexas nos serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="fd05b-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="fd05b-115">Aqui estão alguns exemplos de uso do Gerenciamento de API com Automação:</span><span class="sxs-lookup"><span data-stu-id="fd05b-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="fd05b-116">Gerenciamento de API do Azure – Usando o PowerShell para backup e restauração</span><span class="sxs-lookup"><span data-stu-id="fd05b-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="fd05b-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd05b-117">Next Steps</span></span>
<span data-ttu-id="fd05b-118">Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para gerenciar o Gerenciamento de API do Azure, siga estes links para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fd05b-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="fd05b-119">Veja o [tutorial de introdução](../automation/automation-first-runbook-graphical.md)da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd05b-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

