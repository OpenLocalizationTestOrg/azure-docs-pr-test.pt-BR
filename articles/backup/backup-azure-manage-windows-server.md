---
title: "servidores e cofres de serviços aaaManage recuperação do Azure | Microsoft Docs"
description: "Use este tutorial toolearn como os serviços de recuperação do Azure toomanage cofres e servidores."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="fc67b-103">Monitore e gerencie os cofres dos serviços de recuperação do Azure e os servidores para os computadores que usam o Windows</span><span class="sxs-lookup"><span data-stu-id="fc67b-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc67b-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="fc67b-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="fc67b-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="fc67b-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="fc67b-106">Neste artigo você encontrará uma visão geral da saudação monitor e gerenciamento de tarefas de backup disponíveis por meio de saudação agente de Backup do Microsoft Azure hello e portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="fc67b-107">Este artigo pressupõe que você já tem uma assinatura do Azure e já criou pelo menos um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="fc67b-108">Abrir um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="fc67b-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="fc67b-109">painel do Cofre de serviços de recuperação de saudação mostra detalhes de saudação ou atributos de um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="fc67b-110">Entrar toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="fc67b-111">No menu de Hub hello, clique em **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-111">On hello Hub menu, click **More Services**.</span></span>

    ![Abrir a lista de cofres dos Serviços de Recuperação, etapa 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="fc67b-113">Você deseja tooopen um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="fc67b-114">Na caixa de diálogo hello, comece a digitar **dos serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="fc67b-115">Como começar a digitar, lista Olá filtra com base em sua entrada.</span><span class="sxs-lookup"><span data-stu-id="fc67b-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="fc67b-116">Clique em **os cofres de serviços de recuperação** cofres de lista de saudação toodisplay dos serviços de recuperação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="fc67b-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="fc67b-118">saudação de lista de cofres de serviços de recuperação é aberta.</span><span class="sxs-lookup"><span data-stu-id="fc67b-118">hello list of Recovery Services vaults opens.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="fc67b-120">Na lista de saudação de cofres, selecione o nome de saudação do hello Cofre de serviços de recuperação você deseja tooopen.</span><span class="sxs-lookup"><span data-stu-id="fc67b-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="fc67b-121">Abre a folha de painel de Cofre de serviços de recuperação Hello.</span><span class="sxs-lookup"><span data-stu-id="fc67b-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![painel do cofre dos serviços de recuperação](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="fc67b-123">Agora que você abriu o Cofre de serviços de recuperação hello, tente qualquer uma das tarefas de monitoramento ou gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="fc67b-124">Monitorar trabalhos e alertas de backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="fc67b-125">Monitorar trabalhos e alertas de saudação dos serviços de recuperação cofre dashboard, onde você pode ver:</span><span class="sxs-lookup"><span data-stu-id="fc67b-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="fc67b-126">Detalhes dos alertas de backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-126">Backup alerts details</span></span>
* <span data-ttu-id="fc67b-127">Arquivos e pastas, bem como máquinas virtuais do Azure protegidas na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="fc67b-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="fc67b-128">Armazenamento total consumido no Azure</span><span class="sxs-lookup"><span data-stu-id="fc67b-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="fc67b-129">Status do trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-129">Backup job status</span></span>

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="fc67b-131">Informações de saudação em cada um desses blocos abre Olá folha associado onde você gerencia as tarefas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="fc67b-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="fc67b-132">Da parte superior de saudação do hello painel:</span><span class="sxs-lookup"><span data-stu-id="fc67b-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="fc67b-133">As configurações fornecem acesso às tarefas de backup disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fc67b-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="fc67b-134">Cofre de backup - backup novos arquivos e pastas (ou máquinas virtuais do Azure) dos serviços de recuperação de toohello de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="fc67b-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="fc67b-135">Excluir - se uma recuperação o Cofre de serviços não está sendo usado, você poderá excluí-la toofree o espaço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc67b-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="fc67b-136">Delete só estará habilitada após a exclusão de todos os servidores protegidos do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="fc67b-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="fc67b-138">Alertas de backups usando o agente de backup do Azure:</span><span class="sxs-lookup"><span data-stu-id="fc67b-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="fc67b-139">Nível de alerta</span><span class="sxs-lookup"><span data-stu-id="fc67b-139">Alert Level</span></span> | <span data-ttu-id="fc67b-140">Alertas enviados</span><span class="sxs-lookup"><span data-stu-id="fc67b-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="fc67b-141">Crítico</span><span class="sxs-lookup"><span data-stu-id="fc67b-141">Critical</span></span> |<span data-ttu-id="fc67b-142">Falha de backup, falha na recuperação</span><span class="sxs-lookup"><span data-stu-id="fc67b-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="fc67b-143">Aviso</span><span class="sxs-lookup"><span data-stu-id="fc67b-143">Warning</span></span> |<span data-ttu-id="fc67b-144">Backup foi concluído com avisos (quando menos de 100 arquivos sem backup devido a problemas de toocorruption e mais de um milhão de arquivos é feito com êxito)</span><span class="sxs-lookup"><span data-stu-id="fc67b-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="fc67b-145">Informativo</span><span class="sxs-lookup"><span data-stu-id="fc67b-145">Informational</span></span> |<span data-ttu-id="fc67b-146">Nenhum</span><span class="sxs-lookup"><span data-stu-id="fc67b-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="fc67b-147">Gerenciar alertas de Backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-147">Manage Backup alerts</span></span>
<span data-ttu-id="fc67b-148">Clique em Olá **alertas de Backup** bloco tooopen Olá **alertas de Backup** folha e gerenciar alertas.</span><span class="sxs-lookup"><span data-stu-id="fc67b-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Alertas de Backup](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="fc67b-150">Alertas de Backup Olá bloco mostra Olá número de:</span><span class="sxs-lookup"><span data-stu-id="fc67b-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="fc67b-151">alertas críticos não resolvidos nas últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="fc67b-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="fc67b-152">alertas de aviso não resolvidos nas últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="fc67b-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="fc67b-153">Clicando em cada um desses links leva toohello **alertas de Backup** folha com uma exibição filtrada desses alertas (crítico ou de aviso).</span><span class="sxs-lookup"><span data-stu-id="fc67b-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="fc67b-154">Na folha de alertas de Backup hello, você:</span><span class="sxs-lookup"><span data-stu-id="fc67b-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="fc67b-155">Escolha Olá informações apropriadas tooinclude com seus alertas.</span><span class="sxs-lookup"><span data-stu-id="fc67b-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Escolher colunas](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="fc67b-157">Filtra os alertas quanto à gravidade, status e horários de início/término.</span><span class="sxs-lookup"><span data-stu-id="fc67b-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="fc67b-159">Configura as notificações quanto à gravidade, frequência e destinatários, bem como ativa ou desativa os alertas.</span><span class="sxs-lookup"><span data-stu-id="fc67b-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="fc67b-161">Se **por alerta** é selecionado como Olá **notificar** frequência nenhum agrupamento ou redução nos emails ocorre.</span><span class="sxs-lookup"><span data-stu-id="fc67b-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="fc67b-162">Cada alerta resulta em uma notificação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="fc67b-163">Essa é a configuração de padrão de saudação e email de resolução Olá também é enviada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="fc67b-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="fc67b-164">Se **Digest por hora** é selecionado como Olá **notificar** frequência um email é enviado toohello usuário informando que há não resolvido novos alertas gerados no hello última hora.</span><span class="sxs-lookup"><span data-stu-id="fc67b-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="fc67b-165">Um email de resolução é enviado no final de saudação de hora hello.</span><span class="sxs-lookup"><span data-stu-id="fc67b-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="fc67b-166">Alertas podem ser enviados para Olá níveis de severidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc67b-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="fc67b-167">Crítico</span><span class="sxs-lookup"><span data-stu-id="fc67b-167">critical</span></span>
* <span data-ttu-id="fc67b-168">Aviso</span><span class="sxs-lookup"><span data-stu-id="fc67b-168">warning</span></span>
* <span data-ttu-id="fc67b-169">informações</span><span class="sxs-lookup"><span data-stu-id="fc67b-169">information</span></span>

<span data-ttu-id="fc67b-170">Desativar alerta Olá Olá **desativar** botão na folha de detalhes do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="fc67b-171">Quando você clica em desativar, pode fornecer observações de resolução.</span><span class="sxs-lookup"><span data-stu-id="fc67b-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="fc67b-172">Escolher colunas Olá deseja tooappear como parte do alerta Olá Olá **escolher colunas** botão.</span><span class="sxs-lookup"><span data-stu-id="fc67b-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="fc67b-173">De saudação **configurações** folha, gerenciar alertas de backup selecionando **monitoramento e relatórios > alertas e eventos > alertas de Backup** e, em seguida, clicando em **filtro** ou  **Configurar notificações**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="fc67b-174">Gerenciar itens de Backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-174">Manage Backup items</span></span>
<span data-ttu-id="fc67b-175">Gerenciar backups locais agora está disponível no portal de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="fc67b-176">Na seção de Backup de saudação do painel hello, Olá **itens de Backup** bloco mostra o número de saudação de itens de backup protegidos toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="fc67b-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="fc67b-177">Clique em **pastas de arquivos** em Olá Backup itens lado a lado.</span><span class="sxs-lookup"><span data-stu-id="fc67b-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Bloco Itens de backup](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="fc67b-179">Itens de Backup Olá folha abre com hello filtrar conjunto tooFile-pasta onde você pode ver cada backup específico item listado.</span><span class="sxs-lookup"><span data-stu-id="fc67b-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Itens de Backup](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="fc67b-181">Se você selecionar um item de backup específico na lista de hello, você verá detalhes essenciais de Olá para aquele item.</span><span class="sxs-lookup"><span data-stu-id="fc67b-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="fc67b-182">De saudação **configurações** folha, gerenciar arquivos e pastas selecionando **itens protegidos > itens de Backup** e, em seguida, selecionando **pastas de arquivos** de saudação menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="fc67b-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Itens de backup das configurações](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="fc67b-184">Gerenciar trabalhos de Backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-184">Manage Backup jobs</span></span>
<span data-ttu-id="fc67b-185">Trabalhos de backup para local (quando o servidor de local de saudação do backup de tooAzure) e backups do Azure são visíveis no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="fc67b-186">Olá seção de Backup Olá painel, bloco de trabalho de Backup Olá mostra número saudação de trabalhos:</span><span class="sxs-lookup"><span data-stu-id="fc67b-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="fc67b-187">em andamento</span><span class="sxs-lookup"><span data-stu-id="fc67b-187">in progress</span></span>
* <span data-ttu-id="fc67b-188">Falha no hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="fc67b-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="fc67b-189">toomanage os trabalhos de backup, clique em Olá **trabalhos de Backup** lado a lado, que abre a folha de trabalhos de Backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Itens de backup das configurações](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="fc67b-191">Modificar Olá informações disponíveis na folha de trabalhos de Backup Olá com hello **escolher colunas** botão na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="fc67b-192">Saudação de uso **filtro** tooselect botão entre arquivos e pastas e backup de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="fc67b-193">Se você não vir os arquivos e pastas, clique em **filtro** botão na parte superior de saudação da página hello e selecione **arquivos e pastas** no menu de tipo de Item de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="fc67b-194">De saudação **configurações** folha, gerenciar trabalhos de backup selecionando **monitoramento e relatórios > trabalhos > trabalhos de Backup** e, em seguida, selecionando **pastas de arquivos** de descarte de saudação menu.</span><span class="sxs-lookup"><span data-stu-id="fc67b-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="fc67b-195">Monitorar o uso do Backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-195">Monitor Backup usage</span></span>
<span data-ttu-id="fc67b-196">Olá seção de Backup Olá painel, bloco de uso do Backup de saudação mostra armazenamento Olá consumido no Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="fc67b-197">O uso do armazenamento é fornecido para:</span><span class="sxs-lookup"><span data-stu-id="fc67b-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="fc67b-198">Uso de armazenamento LRS de nuvem associado Olá cofre</span><span class="sxs-lookup"><span data-stu-id="fc67b-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="fc67b-199">A utilização de armazenamento GRS associada Olá cofre em nuvem</span><span class="sxs-lookup"><span data-stu-id="fc67b-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="fc67b-200">Gerenciar seus servidores de produção</span><span class="sxs-lookup"><span data-stu-id="fc67b-200">Manage your production servers</span></span>
<span data-ttu-id="fc67b-201">clique de seus servidores de produção, toomanage **configurações**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="fc67b-202">Em Gerenciar, clique em **Infraestrutura do Backup > Servidores de Produção**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="fc67b-203">listas de folha de servidores de produção de Hello de todos os servidores de produção disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fc67b-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="fc67b-204">Clique em um servidor em detalhes do servidor de saudação lista tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="fc67b-204">Click on a server in hello list tooopen hello server details.</span></span>

![Itens protegidos](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="fc67b-206">Agente de Backup do Azure Olá aberto</span><span class="sxs-lookup"><span data-stu-id="fc67b-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="fc67b-207">Olá abrir **Microsoft Azure Backup agent** (seja pesquisando seu computador para *Backup do Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="fc67b-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="fc67b-209">De saudação **ações** disponíveis em Olá direita do console do agente de backup Olá executar Olá tarefas de gerenciamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc67b-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="fc67b-210">Registrar Servidor</span><span class="sxs-lookup"><span data-stu-id="fc67b-210">Register Server</span></span>
* <span data-ttu-id="fc67b-211">Agendar backup</span><span class="sxs-lookup"><span data-stu-id="fc67b-211">Schedule Backup</span></span>
* <span data-ttu-id="fc67b-212">Fazer backup agora</span><span class="sxs-lookup"><span data-stu-id="fc67b-212">Back Up now</span></span>
* <span data-ttu-id="fc67b-213">Alterar propriedades</span><span class="sxs-lookup"><span data-stu-id="fc67b-213">Change Properties</span></span>

![Ações do console do agente de Backup do Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="fc67b-215">muito**recuperar dados**, consulte [restaurar arquivos tooa Windows server ou o computador de cliente do Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="fc67b-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="fc67b-216">Modificar agendamento de backup Olá</span><span class="sxs-lookup"><span data-stu-id="fc67b-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="fc67b-217">No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="fc67b-219">Em Olá **Assistente de agendamento de Backup** deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="fc67b-221">Se você quiser tooadd ou alterar itens na Olá **selecionar itens tooBackup** tela clique **adicionar itens**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="fc67b-222">Você também pode definir **configurações de exclusão** desta página no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="fc67b-223">Se você quiser tooexclude arquivos ou tipos de arquivo de leitura procedimento Olá para adicionar [configurações de exclusão](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="fc67b-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="fc67b-224">Selecione arquivos hello e pastas que deseja tooback backup e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="fc67b-226">Especifique a saudação **agendamento de backup** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="fc67b-227">Você pode agendar backups diários (no máximo três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="fc67b-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Itens para o backup do Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="fc67b-229">Especificar o agendamento de backup Olá é explicado em detalhes nesta [artigo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="fc67b-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="fc67b-230">Selecione Olá **política de retenção** para cópia de backup hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Itens para o backup do Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="fc67b-232">Em Olá **confirmação** tela hello Revise as informações e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="fc67b-233">Depois que a conclusão do Assistente de saudação criando Olá **agendamento de backup**, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="fc67b-234">Depois de modificar a proteção, você pode confirmar que os backups provocarem corretamente pelo vai toohello **trabalhos** guia e confirmando que as alterações sejam refletidas no hello trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="fc67b-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="fc67b-235">Habilitar a limitação de rede</span><span class="sxs-lookup"><span data-stu-id="fc67b-235">Enable Network Throttling</span></span>

<span data-ttu-id="fc67b-236">Agente de Backup do Azure Olá fornece uma guia de limitação que permite que você toocontrol como largura de banda de rede é usada durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="fc67b-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="fc67b-237">Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de internet.</span><span class="sxs-lookup"><span data-stu-id="fc67b-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="fc67b-238">Transferência de limitação de dados aplica tooback backup e atividades de restauração.</span><span class="sxs-lookup"><span data-stu-id="fc67b-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="fc67b-239">tooenable limitação:</span><span class="sxs-lookup"><span data-stu-id="fc67b-239">tooenable throttling:</span></span>

1. <span data-ttu-id="fc67b-240">Em Olá **agente de Backup**, clique em **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="fc67b-241">Em hello * * limitação guia, selecione **habilitar limitação para operações de backup do uso de largura de banda de internet**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitação de rede](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="fc67b-243">Depois que você habilitou a limitação, especificar Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="fc67b-244">os valores de largura de banda Olá começam em 512 quilobytes por segundo (Kbps) e podem subir too1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="fc67b-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="fc67b-245">Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são considerados trabalho dias.</span><span class="sxs-lookup"><span data-stu-id="fc67b-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="fc67b-246">tempo de saudação fora Olá designado de horas de trabalho é considerado toobe horas de folga.</span><span class="sxs-lookup"><span data-stu-id="fc67b-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="fc67b-247">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="fc67b-248">Gerenciar configurações de exclusão</span><span class="sxs-lookup"><span data-stu-id="fc67b-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="fc67b-249">Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="fc67b-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="fc67b-251">No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="fc67b-253">No Assistente de agendamento de Backup de saudação deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="fc67b-255">Clique em **Configurações de Exclusões**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-255">Click **Exclusions Settings**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="fc67b-257">Clique em **Adicionar Exclusão**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-257">Click **Add Exclusion**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="fc67b-259">Selecione Olá e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-259">Select hello location and then, click **OK**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="fc67b-261">Adicionar extensão de arquivo hello em Olá **tipo de arquivo** campo.</span><span class="sxs-lookup"><span data-stu-id="fc67b-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="fc67b-263">Adição de uma extensão .mp3</span><span class="sxs-lookup"><span data-stu-id="fc67b-263">Adding an .mp3 extension</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="fc67b-265">tooadd outra extensão, clique em **Adicionar exclusão** e insira outra extensão de tipo de arquivo (Adicionar uma extensão. JPEG).</span><span class="sxs-lookup"><span data-stu-id="fc67b-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="fc67b-267">Quando você tiver adicionado todas as extensões de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="fc67b-268">Continuar por Olá Assistente de agendamento de Backup clicando em **próximo** até Olá **página de confirmação**, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="fc67b-270">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="fc67b-270">Frequently asked questions</span></span>
<span data-ttu-id="fc67b-271">**1º TRIMESTRE. status do trabalho de backup Olá mostra como concluída no hello agente de backup do Azure, porque não ele sejam refletido imediatamente no portal?**</span><span class="sxs-lookup"><span data-stu-id="fc67b-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="fc67b-272">R1.</span><span class="sxs-lookup"><span data-stu-id="fc67b-272">A1.</span></span> <span data-ttu-id="fc67b-273">Há é em atraso máximo de 15 minutos entre o status do trabalho de backup Olá refletido no hello agente de backup do Azure e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="fc67b-274">**Q.2 quando um trabalho de backup falhar, quanto tempo leva tooraise um alerta?**</span><span class="sxs-lookup"><span data-stu-id="fc67b-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="fc67b-275">A. 2 um alerta é gerado dentro de 20 minutos de saudação falha de backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="fc67b-276">**P3. Há um caso em que um email não será enviado se as notificações forem configuradas?**</span><span class="sxs-lookup"><span data-stu-id="fc67b-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="fc67b-277">R3.</span><span class="sxs-lookup"><span data-stu-id="fc67b-277">A3.</span></span> <span data-ttu-id="fc67b-278">Abaixo estão casos hello quando Olá notificação não será enviada em ruído de alerta tooreduce Olá ordem:</span><span class="sxs-lookup"><span data-stu-id="fc67b-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="fc67b-279">Se as notificações são configuradas por hora e um alerta é gerado e resolvido na hora de saudação</span><span class="sxs-lookup"><span data-stu-id="fc67b-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="fc67b-280">o Trabalho será cancelado.</span><span class="sxs-lookup"><span data-stu-id="fc67b-280">Job is canceled.</span></span>
* <span data-ttu-id="fc67b-281">O segundo trabalho de backup falhou porque o trabalho de backup original estava em andamento.</span><span class="sxs-lookup"><span data-stu-id="fc67b-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="fc67b-282">Solucionando problemas de monitoramento</span><span class="sxs-lookup"><span data-stu-id="fc67b-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="fc67b-283">**Problema:** trabalhos de e/ou alertas do agente de Backup do Azure Olá não aparecem no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc67b-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="fc67b-284">**Etapas de solução de problemas:** Olá processo, ```OBRecoveryServicesManagementAgent```, envia Olá toohello dados alerta e trabalho de serviço de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc67b-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="fc67b-285">Ocasionalmente, esse processo pode ficar travado ou ser interrompido.</span><span class="sxs-lookup"><span data-stu-id="fc67b-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="fc67b-286">processo de saudação tooverify não está em execução, abra **Gerenciador de tarefas** e verifique se hello ```OBRecoveryServicesManagementAgent``` processo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="fc67b-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="fc67b-287">Supondo que o processo de saudação não está em execução, abra **painel de controle** e navegue Olá lista de serviços.</span><span class="sxs-lookup"><span data-stu-id="fc67b-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="fc67b-288">Inicie ou reinicie o **agente de gerenciamento dos Serviços de Recuperação do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fc67b-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="fc67b-289">Para obter mais informações, procure logs de saudação em:</span><span class="sxs-lookup"><span data-stu-id="fc67b-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="fc67b-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fc67b-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="fc67b-291">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc67b-291">Next steps</span></span>
* [<span data-ttu-id="fc67b-292">Restaurar o Windows Server ou o Windows Client do Azure</span><span class="sxs-lookup"><span data-stu-id="fc67b-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="fc67b-293">toolearn mais sobre o Backup do Azure, consulte [visão geral do Backup do Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="fc67b-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="fc67b-294">Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="fc67b-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
