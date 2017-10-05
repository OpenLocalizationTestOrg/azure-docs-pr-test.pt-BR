---
title: "Visão Geral do DSC de Automação do Azure | Microsoft Docs"
description: "Uma visão geral da DSC (Configuração do Estado Desejado) da Automação do Azure, seus termos e problemas conhecidos"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, configuração de estado desejada, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="5b7b5-104">Visão geral do DSC da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7b5-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="5b7b5-105">O DSC de Automação do Azure é um serviço do Azure que permite gravar, gerenciar e compilar [configurações](https://msdn.microsoft.com/powershell/dsc/configurations) de DSC (Desired State Configuration) do PowerShell, importar [recursos de DSC](https://msdn.microsoft.com/powershell/dsc/resources) e atribuir configurações a nós de destino, tudo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="5b7b5-106">Por que usar o DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7b5-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="5b7b5-107">O DSC de automação do Azure oferece várias vantagens a usar o DSC fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="5b7b5-108">Servidor de pull interno</span><span class="sxs-lookup"><span data-stu-id="5b7b5-108">Built-in pull server</span></span>

<span data-ttu-id="5b7b5-109">A Automação do Azure oferece um [servidor de pull DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que os nós de destino recebam configurações automaticamente, estejam em conformidade com o estado desejado e relatem a respectiva conformidade.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="5b7b5-110">O servidor de pull interno na Automação do Azure elimina a necessidade de configurar e manter seu próprio servidor de pull.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="5b7b5-111">A Automação do Azure pode destinar computadores Windows ou Linux físicos ou virtuais, na nuvem ou localmente.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="5b7b5-112">Gerenciamento de todos os seus artefatos de DSC</span><span class="sxs-lookup"><span data-stu-id="5b7b5-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="5b7b5-113">O DSC de Automação do Azure oferece a mesma camada de gerenciamento para a [Desired State Configuration do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) que a Automação do Azure oferece para scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="5b7b5-114">No portal do Azure ou do PowerShell, você pode gerenciar todas as suas configurações, recursos e nós de destino da DSC.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Captura de tela da folha de Automação do Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="5b7b5-116">Importar dados de relatórios para o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5b7b5-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="5b7b5-117">Nós gerenciados com DSC de Automação do Azure enviam dados de status de relatórios detalhados para o servidor de pull interno.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="5b7b5-118">Você pode configurar a DSC de Automação do Azure para enviar esses dados para seu espaço de trabalho do Log Analytics do OMS (Microsoft Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="5b7b5-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="5b7b5-119">Para saber como enviar dados de status da DSC para seu espaço de trabalho de Log Analytics, consulte [Encaminhar dados de relatório de DSC de Automação do Azure para o Log Analytics do OMS](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5b7b5-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="5b7b5-120">Vídeo de introdução</span><span class="sxs-lookup"><span data-stu-id="5b7b5-120">Introduction video</span></span>

<span data-ttu-id="5b7b5-121">Prefere assistir do que ler?</span><span class="sxs-lookup"><span data-stu-id="5b7b5-121">Prefer watching to reading?</span></span> <span data-ttu-id="5b7b5-122">Assista ao vídeo abaixo, de maio de 2015, quando a DSC de Automação do Azure foi anunciada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="5b7b5-123">Embora os conceitos e o ciclo de vida abordados neste vídeo estejam corretos, a DSC de Automação do Azure avançou muito desde que este vídeo foi gravado.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="5b7b5-124">Agora ele está disponível totalmente, tem uma interface do usuário mais ampla no Portal do Azure e dá suporte a vários recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="5b7b5-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="5b7b5-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b7b5-125">Next steps</span></span>

* <span data-ttu-id="5b7b5-126">Para saber como integrar nós a serem gerenciados com DSC de Automação do Azure, consulte [Integração de computadores para gerenciamento de DSC de Automação do Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="5b7b5-127">Para começar a usar a DSC de Automação do Azure, consulte [Introdução à DSC de Automação do Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="5b7b5-128">Para saber mais sobre configurações da DSC de compilação para que você possa atribuí-las a nós de destino, consulte [Como compilar configurações na DSC de Automação do Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="5b7b5-129">Para referência de cmdlet do PowerShell para a DSC de Automação do Azure, consulte [cmdlets da DSC de Automação do Azure](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="5b7b5-130">Para obter informações sobre preços, consulte [Preços da DSC de Automação do Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="5b7b5-131">Para ver um exemplo de como usar o DSC de automação do Azure em um pipeline de implantação contínua, consulte [implantação contínua para DSC de automação do IaaS VMs usando o Azure e Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="5b7b5-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>