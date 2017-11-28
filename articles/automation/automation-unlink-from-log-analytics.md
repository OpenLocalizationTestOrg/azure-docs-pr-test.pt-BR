---
title: "aaaUnlink conta de automação do Azure da análise de Log | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como toounlink à automação do Azure a conta de um espaço de trabalho do OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="3dc7c-103">Como toounlink a automação da conta de um espaço de trabalho de análise de Log</span><span class="sxs-lookup"><span data-stu-id="3dc7c-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="3dc7c-104">Automação do Azure integra-se com a análise de Log toonot somente suporte o monitoramento proativo de seus trabalhos de runbook em todas as suas contas de automação, mas também é necessária quando você importar Olá soluções que são dependentes de análise de Log a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dc7c-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="3dc7c-105">Gerenciamento de atualizações</span><span class="sxs-lookup"><span data-stu-id="3dc7c-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="3dc7c-106">Controle de alterações</span><span class="sxs-lookup"><span data-stu-id="3dc7c-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="3dc7c-107">Iniciar/parar VMs durante os horários fora de pico</span><span class="sxs-lookup"><span data-stu-id="3dc7c-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="3dc7c-108">Se você decidir que não deseja mais toointegrate sua conta de automação com análise de Log, você pode desvincular sua conta diretamente da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="3dc7c-109">Antes de prosseguir, você precisará primeiro tooremove soluções de saudação mencionadas anteriormente, caso contrário, esse processo será impedido de continuar.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="3dc7c-110">Tópico de saudação de revisão para solução em particular Olá importou etapas de saudação toounderstand necessárias tooremove-lo.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="3dc7c-111">Após a remoção dessas soluções pode executar Olá toounlink as etapas a seguir sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="3dc7c-112">Desvincular o espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="3dc7c-112">Unlink workspace</span></span>

1. <span data-ttu-id="3dc7c-113">Em Olá portal do Azure, abra sua conta de automação e, na folha de conta de automação hello, na folha de conta hello, selecione **desvincular o espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="3dc7c-114">![Opção Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="3dc7c-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="3dc7c-115">Na folha de espaço de trabalho de desvinculação hello, clique em **desvincular o espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="3dc7c-116">![Folha Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="3dc7c-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="3dc7c-117">Você receberá um aviso verificando que desejar tooproceed.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="3dc7c-118">Enquanto a automação do Azure tenta conta de saudação toounlink seu espaço de trabalho de análise de Log, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="3dc7c-119">Se você usou a solução de gerenciamento de atualizações de Olá, opcionalmente, convém Olá tooremove itens que não são mais necessárias após remover solução Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="3dc7c-120">Agendas de atualizações.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-120">Update schedules.</span></span>  <span data-ttu-id="3dc7c-121">Cada uma terá nomes que correspondam às implantações de atualização de saudação criado)</span><span class="sxs-lookup"><span data-stu-id="3dc7c-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="3dc7c-122">Grupos de trabalho híbrida criados para solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="3dc7c-123">Cada uma será nomeada da mesma forma muito machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="3dc7c-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="3dc7c-124">Se você usou Olá iniciar/parar VMs durante a solução de fora do horário comercial, opcionalmente, convém Olá tooremove itens que não são mais necessárias após remover solução Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3dc7c-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="3dc7c-125">Iniciar e parar agendas de runbook da VM</span><span class="sxs-lookup"><span data-stu-id="3dc7c-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="3dc7c-126">Iniciar e parar runbooks da VM</span><span class="sxs-lookup"><span data-stu-id="3dc7c-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="3dc7c-127">variáveis</span><span class="sxs-lookup"><span data-stu-id="3dc7c-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="3dc7c-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3dc7c-128">Next steps</span></span>

<span data-ttu-id="3dc7c-129">tooreconfigure seu toointegrate de conta de automação com análise de logs do OMS, consulte [encaminhar o status do trabalho e fluxos de trabalho de automação tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="3dc7c-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
