---
title: "Desvincular conta de Automação do Azure do Log Analytics | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como desvincular sua conta de Automação do Azure de um espaço de trabalho do OMS."
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="18742-103">Como desvincular sua conta de Automação de um espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="18742-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="18742-104">A Automação do Azure integra-se ao Log Analytics não só para dar suporte ao monitoramento proativo do seus trabalhos de runbook em todas as suas contas de Automação, mas ela também é necessária quando você importa as seguintes soluções que dependem do Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="18742-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="18742-105">Gerenciamento de atualizações</span><span class="sxs-lookup"><span data-stu-id="18742-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="18742-106">Controle de alterações</span><span class="sxs-lookup"><span data-stu-id="18742-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="18742-107">Iniciar/parar VMs durante os horários fora de pico</span><span class="sxs-lookup"><span data-stu-id="18742-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="18742-108">Caso decida que não quer mais integrar sua conta de Automação ao Log Analytics, você poderá desvincular a conta diretamente no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18742-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="18742-109">Antes de prosseguir, você precisa remover as soluções mencionadas anteriormente primeiro, caso contrário, esse processo será impedido de continuar.</span><span class="sxs-lookup"><span data-stu-id="18742-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="18742-110">Examine o tópico sobre a solução específica que você importou para entender as etapas necessárias para removê-la.</span><span class="sxs-lookup"><span data-stu-id="18742-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="18742-111">Depois de remover essas soluções, você poderá executar as etapas a seguir para desvincular sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="18742-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="18742-112">Desvincular o espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="18742-112">Unlink workspace</span></span>

1. <span data-ttu-id="18742-113">No Portal do Azure, abra a conta de Automação e, na folha da conta de Automação, na folha da conta, escolha **Desvincular espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="18742-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="18742-114">![Opção Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="18742-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="18742-115">Na folha Desvincular espaço de trabalho, clique em **Desvincular espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="18742-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="18742-116">![Folha Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="18742-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="18742-117">Você receberá uma solicitação perguntando se deseja prosseguir.</span><span class="sxs-lookup"><span data-stu-id="18742-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="18742-118">Enquanto a Automação do Azure tenta desvincular a conta do seu espaço de trabalho do Log Analytics, você pode acompanhar o progresso no menu **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="18742-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="18742-119">Se você tiver usado a solução Gerenciamento de Atualizações, como opção, convém remover os itens a seguir que não serão mais necessários após a remoção da solução.</span><span class="sxs-lookup"><span data-stu-id="18742-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="18742-120">Agendas de atualizações.</span><span class="sxs-lookup"><span data-stu-id="18742-120">Update schedules.</span></span>  <span data-ttu-id="18742-121">Cada uma terá nomes que correspondam às implantações de atualizações que você criou)</span><span class="sxs-lookup"><span data-stu-id="18742-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="18742-122">Grupos de trabalho híbridos criados para a solução.</span><span class="sxs-lookup"><span data-stu-id="18742-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="18742-123">Cada um receberá um nome semelhante a machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="18742-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="18742-124">Se você tiver usado a solução Iniciar/parar VMs durante os horários fora de pico, como opção, convém remover os itens a seguir que não serão mais necessários após a remoção da solução.</span><span class="sxs-lookup"><span data-stu-id="18742-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="18742-125">Iniciar e parar agendas de runbook da VM</span><span class="sxs-lookup"><span data-stu-id="18742-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="18742-126">Iniciar e parar runbooks da VM</span><span class="sxs-lookup"><span data-stu-id="18742-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="18742-127">variáveis</span><span class="sxs-lookup"><span data-stu-id="18742-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="18742-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18742-128">Next steps</span></span>

<span data-ttu-id="18742-129">Para reconfigurar sua conta de Automação para se integrar ao Log Analytics do OMS, confira [Encaminhar status do trabalho e fluxos de trabalho de Automação para Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="18742-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 