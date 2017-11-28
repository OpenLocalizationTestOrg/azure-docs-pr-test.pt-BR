---
title: "Visão geral de DSC de automação de aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="d70b8-104">Visão geral do DSC da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d70b8-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="d70b8-105">DSC de automação do Azure é um serviço do Azure que permite que você toowrite, gerenciar e compilar a configuração de estado desejado (DSC) da PowerShell [configurações](https://msdn.microsoft.com/powershell/dsc/configurations), importar [recursos DSC](https://msdn.microsoft.com/powershell/dsc/resources)e atribuir nós de tootarget de configurações, todos na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d70b8-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="d70b8-106">Por que usar o DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d70b8-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="d70b8-107">O DSC de automação do Azure oferece várias vantagens a usar o DSC fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="d70b8-108">Servidor de pull interno</span><span class="sxs-lookup"><span data-stu-id="d70b8-108">Built-in pull server</span></span>

<span data-ttu-id="d70b8-109">Automação do Azure fornece um [servidor de pull de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que nós de destino recebem automaticamente as configurações, está de acordo com o estado de toohello desejado e relatar sobre sua conformidade.</span><span class="sxs-lookup"><span data-stu-id="d70b8-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="d70b8-110">servidor de pull internos de saudação na automação do Azure elimina Olá necessidade tooset backup e manter seu próprio servidor de pull.</span><span class="sxs-lookup"><span data-stu-id="d70b8-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="d70b8-111">Automação do Azure pode máquinas de Windows ou Linux físicas ou virtuais, na nuvem de saudação ou no local de destino.</span><span class="sxs-lookup"><span data-stu-id="d70b8-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="d70b8-112">Gerenciamento de todos os seus artefatos de DSC</span><span class="sxs-lookup"><span data-stu-id="d70b8-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="d70b8-113">DSC de automação do Azure coloca Olá a mesma camada de gerenciamento muito[configuração de estado desejado do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) como a automação do Azure oferece para o script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d70b8-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="d70b8-114">De saudação portal do Azure, ou do PowerShell, você pode gerenciar todos os seus DSC configurações, recursos e nós de destino.</span><span class="sxs-lookup"><span data-stu-id="d70b8-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Captura de tela da folha de automação do Azure Olá](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="d70b8-116">Importar dados de relatórios para o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d70b8-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="d70b8-117">Nós que são gerenciados com DSC de automação do Azure envio detalhada status dados toohello pull internos servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="d70b8-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="d70b8-118">Você pode configurar o DSC de automação do Azure toosend este espaço de trabalho de análise de logs do Microsoft Operations Management Suite (OMS) de tooyour de dados.</span><span class="sxs-lookup"><span data-stu-id="d70b8-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="d70b8-119">toolearn como toosend DSC status dados tooyour espaço de trabalho de análise de Log, consulte [Forward Azure DSC de automação reporting dados tooOMS análise de Log](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d70b8-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="d70b8-120">Vídeo de introdução</span><span class="sxs-lookup"><span data-stu-id="d70b8-120">Introduction video</span></span>

<span data-ttu-id="d70b8-121">Preferir assistir tooreading?</span><span class="sxs-lookup"><span data-stu-id="d70b8-121">Prefer watching tooreading?</span></span> <span data-ttu-id="d70b8-122">Dê uma olhada nos Olá seguindo o vídeo de maio de 2015, quando DSC de automação do Azure foi anunciada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="d70b8-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="d70b8-123">Enquanto Olá conceitos e ciclo de vida discutidos neste vídeo são corretos, DSC de automação do Azure avançou muito desde que este vídeo foi gravado.</span><span class="sxs-lookup"><span data-stu-id="d70b8-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="d70b8-124">Ele agora está disponível, tem uma interface de usuário muito mais amplo em Olá portal do Azure e oferece suporte a vários recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="d70b8-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="d70b8-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d70b8-125">Next steps</span></span>

* <span data-ttu-id="d70b8-126">toolearn como tooonboard toobe de nós gerenciados com DSC de automação do Azure, consulte [máquinas de integração para o gerenciamento de DSC de automação do Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="d70b8-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="d70b8-127">tooget iniciado usando a DSC de automação do Azure, consulte [guia de Introdução ao DSC de automação do Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="d70b8-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="d70b8-128">toolearn sobre configurações de DSC de compilação para que você possa atribuir tootarget nós, consulte [compilando configurações no DSC de automação do Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="d70b8-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="d70b8-129">Para referência de cmdlet do PowerShell para a DSC de Automação do Azure, consulte [cmdlets da DSC de Automação do Azure](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="d70b8-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="d70b8-130">Para obter informações sobre preços, consulte [Preços da DSC de Automação do Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="d70b8-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="d70b8-131">toosee um exemplo de como usar o DSC de automação do Azure em um pipeline de implantação contínua, consulte [tooIaaS implantação contínua DSC de automação do Azure VMs usando e Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="d70b8-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
