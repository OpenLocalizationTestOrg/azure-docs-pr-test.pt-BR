---
title: "aaaManage gerenciamento de API do Azure usando a automação do Azure"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage gerenciamento de API do Azure."
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
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="eae58-103">Gerenciando o Gerenciamento de API do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="eae58-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="eae58-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento do gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae58-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="eae58-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="eae58-105">What is Azure Automation?</span></span>
<span data-ttu-id="eae58-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="eae58-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="eae58-107">Usando a automação do Azure, as tarefas manuais repetidas, demoradas e propensas a erros podem ser toovalue de tempo para a sua organização, eficiência e confiabilidade de tooincrease automatizada.</span><span class="sxs-lookup"><span data-stu-id="eae58-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="eae58-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="eae58-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="eae58-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="eae58-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="eae58-110">Reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae58-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="eae58-111">Como a Automação do Azure ajudar a gerenciar o Gerenciamento de API?</span><span class="sxs-lookup"><span data-stu-id="eae58-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="eae58-112">Gerenciamento de API podem ser gerenciado na automação do Azure usando Olá [cmdlets do Windows PowerShell para a API de gerenciamento de API do Azure](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="eae58-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="eae58-113">Na automação do Azure você pode escrever tooperform de scripts de fluxo de trabalho do PowerShell, muitas das tarefas de gerenciamento de API usando cmdlets de saudação.</span><span class="sxs-lookup"><span data-stu-id="eae58-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="eae58-114">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="eae58-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="eae58-115">Aqui estão alguns exemplos de uso do Gerenciamento de API com Automação:</span><span class="sxs-lookup"><span data-stu-id="eae58-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="eae58-116">Gerenciamento de API do Azure – Usando o PowerShell para backup e restauração</span><span class="sxs-lookup"><span data-stu-id="eae58-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="eae58-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eae58-117">Next Steps</span></span>
<span data-ttu-id="eae58-118">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage gerenciamento de API do Azure, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="eae58-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="eae58-119">Consulte Olá automação do Azure [tutorial de Introdução](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="eae58-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

