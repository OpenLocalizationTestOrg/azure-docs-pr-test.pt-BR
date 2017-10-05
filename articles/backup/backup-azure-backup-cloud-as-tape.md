---
title: Usar o Backup do Azure para substituir a infraestrutura de fita | Microsoft Docs
description: "Saiba como o Backup do Azure fornece semântica semelhante à fita que permite fazer backup e restaurar dados no Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="6fabb-103">Mover o armazenamento de longo prazo da fita para a nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="6fabb-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="6fabb-104">Os clientes do Backup do Azure e do System Center Data Protection Manager podem:</span><span class="sxs-lookup"><span data-stu-id="6fabb-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="6fabb-105">Fazer backup de dados em agendas mais adequadas às necessidades da organização.</span><span class="sxs-lookup"><span data-stu-id="6fabb-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="6fabb-106">Manter os dados de backup por períodos mais longos</span><span class="sxs-lookup"><span data-stu-id="6fabb-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="6fabb-107">Tornar o Azure parte das necessidades de retenção de longo prazo (em vez de fita).</span><span class="sxs-lookup"><span data-stu-id="6fabb-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="6fabb-108">Este artigo explica como os clientes podem habilitar políticas de backup e retenção.</span><span class="sxs-lookup"><span data-stu-id="6fabb-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="6fabb-109">Os clientes que usam fitas para tratar suas necessidades de retenção de longo prazo agora têm uma alternativa viável e eficiente com a disponibilidade desse recurso.</span><span class="sxs-lookup"><span data-stu-id="6fabb-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="6fabb-110">O recurso está habilitado na versão mais recente do Backup do Azure (que está disponível [aqui](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="6fabb-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="6fabb-111">Os clientes do System Center DPM devem atualizar para, pelo menos, o DPM 2012 R2 UR5 antes de usar o DPM com o serviço de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fabb-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="6fabb-112">Qual é o agendamento de backup?</span><span class="sxs-lookup"><span data-stu-id="6fabb-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="6fabb-113">O agendamento de backup indica a frequência da operação de backup.</span><span class="sxs-lookup"><span data-stu-id="6fabb-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="6fabb-114">Por exemplo, as configurações na tela a seguir indicam que os backups são feitos diariamente às 18h e à meia-noite.</span><span class="sxs-lookup"><span data-stu-id="6fabb-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Agendamento diário](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="6fabb-116">Os clientes também podem agendar um backup semanal.</span><span class="sxs-lookup"><span data-stu-id="6fabb-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="6fabb-117">Por exemplo, as configurações na tela a seguir indicam que os backups são feitos a cada dois domingos e a cada duas quartas-feiras às 9h30 e à 1h.</span><span class="sxs-lookup"><span data-stu-id="6fabb-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Agendamento semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="6fabb-119">O que é a política de retenção?</span><span class="sxs-lookup"><span data-stu-id="6fabb-119">What is the Retention Policy?</span></span>
<span data-ttu-id="6fabb-120">A política de retenção especifica durante quanto tempo o backup deve ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="6fabb-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="6fabb-121">Em vez de especificar apenas uma “política simples” para todos os pontos de backup, os clientes podem especificar diferentes políticas de retenção com base em quando o backup é feito.</span><span class="sxs-lookup"><span data-stu-id="6fabb-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="6fabb-122">Por exemplo, o ponto de backup feito diariamente (que funciona como um ponto de recuperação operacional) é preservado por 90 dias.</span><span class="sxs-lookup"><span data-stu-id="6fabb-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="6fabb-123">O ponto de backup feito no final de cada trimestre para fins de auditoria é preservado por mais tempo.</span><span class="sxs-lookup"><span data-stu-id="6fabb-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Política de retenção](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="6fabb-125">O número total de “pontos de retenção” especificado nessa política é de 90 (pontos diários) + 40 (um a cada trimestre por 10 anos) = 130.</span><span class="sxs-lookup"><span data-stu-id="6fabb-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="6fabb-126">Exemplo – Juntando ambos</span><span class="sxs-lookup"><span data-stu-id="6fabb-126">Example – Putting both together</span></span>
![Tela de exemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="6fabb-128">**Política de retenção diária**: os backups diários são armazenados por sete dias.</span><span class="sxs-lookup"><span data-stu-id="6fabb-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="6fabb-129">**Política de retenção semanal**: os backups feitos aos sábados, à meia-noite e às 18h, serão preservados por quatro semanas</span><span class="sxs-lookup"><span data-stu-id="6fabb-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="6fabb-130">**Política de retenção mensal**: os backups feitos à meia-noite e às 18h no último sábado de cada mês são preservados por 12 meses</span><span class="sxs-lookup"><span data-stu-id="6fabb-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="6fabb-131">**Política anual de retenção**: os backups feitos à meia-noite no último sábado de cada mês de março são preservados por 10 anos</span><span class="sxs-lookup"><span data-stu-id="6fabb-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="6fabb-132">O número total de “pontos de retenção” (dos quais um cliente pode restaurar dados) no diagrama anterior é calculado da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6fabb-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="6fabb-133">dois pontos por dia por sete dias = 14 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="6fabb-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="6fabb-134">dois pontos por semana por quatro semanas = oito pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="6fabb-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="6fabb-135">dois pontos por mês por 12 meses = 24 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="6fabb-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="6fabb-136">um ponto por ano por 10 anos = 10 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="6fabb-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="6fabb-137">O número total de pontos de recuperação é 56.</span><span class="sxs-lookup"><span data-stu-id="6fabb-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="6fabb-138">O backup do Azure não tem uma restrição para o número de pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6fabb-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="6fabb-139">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="6fabb-139">Advanced configuration</span></span>
<span data-ttu-id="6fabb-140">Clicando em **Modificar** na tela anterior, os clientes têm mais flexibilidade para especificar agendamentos de retenção.</span><span class="sxs-lookup"><span data-stu-id="6fabb-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="6fabb-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fabb-142">Next Steps</span></span>
<span data-ttu-id="6fabb-143">Para saber mais sobre o Backup do Azure, veja:</span><span class="sxs-lookup"><span data-stu-id="6fabb-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="6fabb-144">Introdução ao Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="6fabb-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="6fabb-145">Teste o Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="6fabb-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
