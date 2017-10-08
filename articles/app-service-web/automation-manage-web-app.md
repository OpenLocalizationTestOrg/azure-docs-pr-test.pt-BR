---
title: "aaaManage aplicativo Web do Azure usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage aplicativo Web do Azure."
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
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="f2f3f-103">Gerenciando o Aplicativo Web do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="f2f3f-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="f2f3f-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento de aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f2f3f-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="f2f3f-105">What is Azure Automation?</span></span>
<span data-ttu-id="f2f3f-106">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="f2f3f-107">Usando a automação do Azure, as tarefas manuais repetidas, demoradas e propensas a erros podem ser toovalue de tempo para a sua organização, eficiência e confiabilidade de tooincrease automatizada.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="f2f3f-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="f2f3f-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f2f3f-110">Reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="f2f3f-111">Como a Automação do Azure ajuda a gerenciar o Aplicativo Web do Azure?</span><span class="sxs-lookup"><span data-stu-id="f2f3f-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="f2f3f-112">Aplicativo Web pode ser gerenciado na automação do Azure usando cmdlets do PowerShell Olá que estão disponíveis no hello [módulos do PowerShell do Azure](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f2f3f-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f2f3f-113">Você pode [instalar esses cmdlets do PowerShell do aplicativo Web na automação do Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), de modo que você pode executar todas as tarefas de gerenciamento de aplicativo Web no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="f2f3f-114">Esses cmdlets na automação do Azure com os cmdlets do hello tarefas complexas, tooautomate outros serviços do Azure também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="f2f3f-115">Aqui estão alguns exemplos de Serviços de Aplicativos com a automação de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="f2f3f-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="f2f3f-116">Scripts para gerenciar os Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="f2f3f-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="f2f3f-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2f3f-117">Next steps</span></span>
<span data-ttu-id="f2f3f-118">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage aplicativo Web do Azure, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f3f-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="f2f3f-119">Consulte Olá automação do Azure [Tutorial de Introdução](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="f2f3f-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

