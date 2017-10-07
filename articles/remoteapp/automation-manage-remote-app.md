---
title: "aaaManage RemoteApp do Azure usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage Azure RemoteApp."
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
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="f932e-103">Gerenciando o Azure RemoteApp usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="f932e-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f932e-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f932e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f932e-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f932e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f932e-106">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f932e-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f932e-107">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="f932e-107">What is Azure Automation?</span></span>
<span data-ttu-id="f932e-108">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="f932e-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="f932e-109">Usando a automação do Azure, as tarefas manuais repetidas com frequência, demoradas e propensas a erros podem ser toovalue de tempo para a sua organização, eficiência e confiabilidade de tooincrease automatizada.</span><span class="sxs-lookup"><span data-stu-id="f932e-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="f932e-110">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f932e-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="f932e-111">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="f932e-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f932e-112">Reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f932e-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="f932e-113">Como a Automação do Azure ajuda a gerenciar o Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="f932e-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="f932e-114">RemoteApp pode ser gerenciado na automação do Azure usando cmdlets do PowerShell Olá que estão disponíveis no hello [ferramentas do Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="f932e-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="f932e-115">Automação do Azure tem esses cmdlets do PowerShell do RemoteApp disponíveis fora da caixa hello, para que você possa executar todas as suas tarefas de gerenciamento do RemoteApp no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f932e-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="f932e-116">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="f932e-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f932e-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f932e-117">Next steps</span></span>
<span data-ttu-id="f932e-118">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage RemoteApp do Azure, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f932e-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="f932e-119">Consulte Olá automação do Azure [Tutorial de Introdução](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="f932e-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

