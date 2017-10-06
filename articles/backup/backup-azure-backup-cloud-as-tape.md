---
title: aaaUse Backup do Azure tooreplace sua infraestrutura de fita | Microsoft Docs
description: "Saiba como o Backup do Azure fornece a semântica semelhantes a fita que permite que você toobackup e restaurar dados no Azure"
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
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="890ea-103">Mover o armazenamento de longo prazo de fita toohello nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="890ea-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="890ea-104">Os clientes do Backup do Azure e do System Center Data Protection Manager podem:</span><span class="sxs-lookup"><span data-stu-id="890ea-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="890ea-105">Fazer backup de dados em agendas que melhor atenda às necessidades organizacionais hello.</span><span class="sxs-lookup"><span data-stu-id="890ea-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="890ea-106">Manter os dados de backup Olá por períodos mais longos</span><span class="sxs-lookup"><span data-stu-id="890ea-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="890ea-107">Tornar o Azure parte das necessidades de retenção de longo prazo (em vez de fita).</span><span class="sxs-lookup"><span data-stu-id="890ea-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="890ea-108">Este artigo explica como os clientes podem habilitar políticas de backup e retenção.</span><span class="sxs-lookup"><span data-stu-id="890ea-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="890ea-109">Os clientes que usam fitas tooaddress seu longo-prazo-suas necessidades de retenção agora tem uma alternativa viável e poderosa com disponibilidade Olá desse recurso.</span><span class="sxs-lookup"><span data-stu-id="890ea-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="890ea-110">Olá recurso está habilitado na versão mais recente de saudação do hello Azure Backup (que está disponível [aqui](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="890ea-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="890ea-111">Os clientes do System Center DPM devem atualizar para, pelo menos, o DPM 2012 R2 UR5 antes de usar o DPM com hello serviço Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="890ea-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="890ea-112">O que é Olá agendamento de Backup?</span><span class="sxs-lookup"><span data-stu-id="890ea-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="890ea-113">agendamento de backup Olá indica a frequência de Olá Olá da operação de backup.</span><span class="sxs-lookup"><span data-stu-id="890ea-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="890ea-114">Por exemplo, configurações Olá Olá tela a seguir indicam que os backups são realizados diariamente às 18: 00 e à meia-noite.</span><span class="sxs-lookup"><span data-stu-id="890ea-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Agendamento diário](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="890ea-116">Os clientes também podem agendar um backup semanal.</span><span class="sxs-lookup"><span data-stu-id="890ea-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="890ea-117">Por exemplo, hello configurações em Olá tela a seguir indicam que os backups são realizados a cada alternativa domingo & quarta-feira em 9:30 da manhã e 1:00 AM.</span><span class="sxs-lookup"><span data-stu-id="890ea-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Agendamento semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="890ea-119">O que é Olá política de retenção?</span><span class="sxs-lookup"><span data-stu-id="890ea-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="890ea-120">política de retenção de saudação especifica a duração de saudação para o qual o backup Olá deve ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="890ea-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="890ea-121">Em vez de especificar apenas uma "política simples" para todos os pontos de backup, os clientes podem especificar políticas de retenção diferentes com base em quando é feito backup hello.</span><span class="sxs-lookup"><span data-stu-id="890ea-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="890ea-122">Por exemplo, a saudação ponto de backup feito diariamente, que serve como um ponto de recuperação operacional, é preservado por 90 dias.</span><span class="sxs-lookup"><span data-stu-id="890ea-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="890ea-123">ponto de backup Olá colocado no final de saudação de cada trimestre para fins de auditoria é preservado por mais tempo.</span><span class="sxs-lookup"><span data-stu-id="890ea-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Política de retenção](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="890ea-125">Olá número total de pontos de retenção"" especificados nesta política é 90 (pontos de diários) + 40 (um para cada trimestre para 10 anos) = 130.</span><span class="sxs-lookup"><span data-stu-id="890ea-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="890ea-126">Exemplo – Juntando ambos</span><span class="sxs-lookup"><span data-stu-id="890ea-126">Example – Putting both together</span></span>
![Tela de exemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="890ea-128">**Política de retenção diária**: os backups diários são armazenados por sete dias.</span><span class="sxs-lookup"><span data-stu-id="890ea-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="890ea-129">**Política de retenção semanal**: os backups feitos aos sábados, à meia-noite e às 18h, serão preservados por quatro semanas</span><span class="sxs-lookup"><span data-stu-id="890ea-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="890ea-130">**Política de retenção mensal**: Backups feitos em meia-noite e 18h00 de saudação Último sábado de cada mês são preservados por 12 meses</span><span class="sxs-lookup"><span data-stu-id="890ea-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="890ea-131">**Política de retenção anual**: Backups feitos à meia-noite Olá Último sábado de março, cada são preservados para 10 anos</span><span class="sxs-lookup"><span data-stu-id="890ea-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="890ea-132">Olá número total de pontos de retenção"" (do qual um cliente pode restaurar dados de pontos) em Olá diagrama anterior é calculado da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="890ea-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="890ea-133">dois pontos por dia por sete dias = 14 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="890ea-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="890ea-134">dois pontos por semana por quatro semanas = oito pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="890ea-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="890ea-135">dois pontos por mês por 12 meses = 24 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="890ea-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="890ea-136">um ponto por ano por 10 anos = 10 pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="890ea-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="890ea-137">Olá o número total de pontos de recuperação é 56.</span><span class="sxs-lookup"><span data-stu-id="890ea-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="890ea-138">O backup do Azure não tem uma restrição para o número de pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="890ea-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="890ea-139">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="890ea-139">Advanced configuration</span></span>
<span data-ttu-id="890ea-140">Clicando em **modificar** em Olá antes da tela, os clientes têm mais flexibilidade para especificar agendamentos de retenção.</span><span class="sxs-lookup"><span data-stu-id="890ea-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="890ea-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="890ea-142">Next Steps</span></span>
<span data-ttu-id="890ea-143">Para saber mais sobre o Backup do Azure, veja:</span><span class="sxs-lookup"><span data-stu-id="890ea-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="890ea-144">Introdução tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="890ea-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="890ea-145">Teste o Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="890ea-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
