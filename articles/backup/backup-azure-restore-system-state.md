---
title: 'O Backup do Azure: Tooa de restaurar o estado do sistema Windows Server | Microsoft Docs'
description: "Explicação passo a passo para restaurar o estado do sistema do Windows Server de um backup no Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="25ddd-103">Restaurar o estado do sistema tooWindows Server</span><span class="sxs-lookup"><span data-stu-id="25ddd-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="25ddd-104">Este artigo explica como os backups de estado do sistema do Windows Server toorestore dos serviços de recuperação de um Azure cofre.</span><span class="sxs-lookup"><span data-stu-id="25ddd-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="25ddd-105">toorestore estado do sistema, você deve ter um backup de estado do sistema (criados usando instruções Olá [backup de estado do sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e certifique-se de ter instalado o hello [versão mais recente de saudação do Microsoft Azure Recovery O agente de serviços (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="25ddd-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="25ddd-106">Recuperar dados de estado do sistema do Windows Server de um cofre de serviços de recuperação do Azure é um processo de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="25ddd-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="25ddd-107">Restaure o estado do sistema como arquivos de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="25ddd-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="25ddd-108">Ao restaurar o estado do sistema como arquivos de Backup do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="25ddd-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="25ddd-109">Restaurar o estado do sistema toohello mesmo servidor em que foram feitos backups hello, ou</span><span class="sxs-lookup"><span data-stu-id="25ddd-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="25ddd-110">Servidor alternativo do tooan do arquivo de restauração de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="25ddd-111">Aplica tooa arquivos de estado do sistema Olá restaurado do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="25ddd-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="25ddd-112">Recuperar o estado do sistema de arquivos toohello mesmo servidor</span><span class="sxs-lookup"><span data-stu-id="25ddd-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="25ddd-113">Olá etapas a seguir explica como fazer o seu estado anterior do Windows Server configuração tooa tooroll.</span><span class="sxs-lookup"><span data-stu-id="25ddd-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="25ddd-114">Reverter o servidor de configuração tooa back conhecido, o estado estável, pode ser extremamente valioso.</span><span class="sxs-lookup"><span data-stu-id="25ddd-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="25ddd-115">saudação do estado do sistema do servidor de saudação restauração etapas a seguir de um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="25ddd-116">Olá abrir **Backup do Microsoft Azure** snap-in.</span><span class="sxs-lookup"><span data-stu-id="25ddd-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="25ddd-117">Se você não souber onde Olá snap-in foi instalado, pesquisar Olá computador ou servidor para **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="25ddd-118">aplicativo de área de trabalho de saudação deve aparecer nos resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="25ddd-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="25ddd-119">Clique em **recuperar dados** toostart Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="25ddd-121">Em Olá **Introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha esse servidor opção toorestore Olá dados toohello mesmo computador](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="25ddd-123">Em Olá **Selecionar modo de recuperação** painel, escolha **o estado do sistema** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="25ddd-125">No calendário Olá em **selecionar Volume e data** ponto do painel, selecione uma recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="25ddd-126">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="25ddd-127">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="25ddd-128">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="25ddd-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="25ddd-130">Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="25ddd-131">O Backup do Azure monta o ponto de recuperação locais hello e utiliza como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="25ddd-132">No painel de Avançar hello, especifique o destino Olá Olá recuperar arquivos de estado do sistema e clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="25ddd-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="25ddd-133">Olá opção **criar cópias para ter ambas as versões**, cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia de saudação de todo o arquivo de estado do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="25ddd-135">Verifique os detalhes de saudação de recuperação em Olá **confirmação** painel e clique em **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Clique em recuperar tooacknowledge Olá recuperar ação](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="25ddd-137">Saudação de cópia *WindowsImageBackup* diretório no volume não críticos de tooa do destino de recuperação do servidor de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="25ddd-138">Geralmente, Olá volume do sistema operacional Windows é volume crítico hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="25ddd-139">Depois que a recuperação de saudação for bem-sucedida, execute as etapas de saudação na seção Olá, [aplicar restaurado toohello de arquivos de estado do sistema Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), Olá toocomplete processo de recuperação do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="25ddd-140">Recuperar o estado do sistema de arquivos de servidor alternativo tooan</span><span class="sxs-lookup"><span data-stu-id="25ddd-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="25ddd-141">Se seu servidor do Windows está corrompido ou inacessível, e você quiser toorestore-tooa o estado estável, recuperando Olá estado do sistema do Windows Server, você pode restaurar o estado do sistema do servidor de saudação corrompido de outro servidor.</span><span class="sxs-lookup"><span data-stu-id="25ddd-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="25ddd-142">Use Olá seguindo as etapas toohello restaurar estado do sistema em um servidor separado.</span><span class="sxs-lookup"><span data-stu-id="25ddd-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="25ddd-143">terminologia de saudação usada essas etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="25ddd-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="25ddd-144">*Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="25ddd-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="25ddd-145">*Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="25ddd-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="25ddd-146">*Cofre de exemplo* – Olá Olá de toowhich de Cofre de serviços de recuperação *máquina de origem* e *máquina destino* são registrados.</span><span class="sxs-lookup"><span data-stu-id="25ddd-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="25ddd-147">Os backups de um computador não podem ser restaurado tooa máquina executando uma versão anterior do sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="25ddd-148">Por exemplo, os backups de um Windows Server 2016 máquina não pode ser restaurado tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="25ddd-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="25ddd-149">No entanto, o inverso de saudação é possível.</span><span class="sxs-lookup"><span data-stu-id="25ddd-149">However, hello inverse is possible.</span></span> <span data-ttu-id="25ddd-150">Você pode usar os backups do Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="25ddd-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="25ddd-151">Olá abrir **Backup do Microsoft Azure** snap-in no hello *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="25ddd-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="25ddd-152">Certifique-se de que Olá *máquina destino* e hello *máquina de origem* são registrado toohello dos serviços de recuperação mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="25ddd-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="25ddd-153">Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="25ddd-155">Selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="25ddd-155">Select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="25ddd-157">Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*.</span><span class="sxs-lookup"><span data-stu-id="25ddd-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="25ddd-158">Se o arquivo de credencial de cofre Olá é inválido (ou expirado), baixe um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="25ddd-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="25ddd-159">Depois que o arquivo de credencial de cofre Olá for fornecido, Cofre de serviços de recuperação de saudação associado ao arquivo de credencial de cofre Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="25ddd-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="25ddd-160">No painel de selecionar servidor de Backup do hello, selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas.</span><span class="sxs-lookup"><span data-stu-id="25ddd-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="25ddd-162">No painel de selecionar modo de recuperação hello, escolha **o estado do sistema** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Pesquisar](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="25ddd-164">Em Olá calendário no hello **selecionar Volume e data** ponto do painel, selecione uma recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="25ddd-165">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="25ddd-166">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="25ddd-167">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="25ddd-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Pesquisar itens](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="25ddd-169">Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="25ddd-170">Em Olá **Selecionar modo de recuperação de estado do sistema** painel, especifique o destino Olá onde você deseja que o estado do sistema de arquivos toobe recuperado, e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Criptografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="25ddd-172">Olá opção **criar cópias para ter ambas as versões**, cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia de saudação de todo o arquivo de estado do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="25ddd-173">Verifique os detalhes de saudação de recuperação no painel de confirmação hello e, em seguida, clique em **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Clique em processo de recuperação de Olá Olá recuperar botão tooconfirm](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="25ddd-175">Saudação de cópia *WindowsImageBackup* volume não críticos do diretório tooa do servidor de saudação (por exemplo d:\).</span><span class="sxs-lookup"><span data-stu-id="25ddd-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="25ddd-176">Geralmente Olá volume do sistema operacional Windows é volume crítico hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="25ddd-177">processo de recuperação do toocomplete hello, uso a seguir Olá seção muito[aplicar arquivos de estado do sistema Olá restaurado em um servidor Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="25ddd-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="25ddd-178">Aplicar o estado do sistema restaurado em um Windows Server</span><span class="sxs-lookup"><span data-stu-id="25ddd-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="25ddd-179">Depois que você tiver recuperado o estado do sistema como arquivos usando o agente de serviços de recuperação do Azure, use Olá Backup do Windows Server utilitário tooapply Olá recuperado tooWindows de estado do sistema servidor.</span><span class="sxs-lookup"><span data-stu-id="25ddd-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="25ddd-180">Olá utilitário de Backup do Windows Server já está disponível no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="25ddd-181">Olá, as etapas a seguir explica como tooapply Olá recuperado o estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="25ddd-182">A seguir Olá use comandos tooreboot seu servidor *modo de reparo de serviços de diretório*.</span><span class="sxs-lookup"><span data-stu-id="25ddd-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="25ddd-183">Em um prompt de comandos com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="25ddd-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="25ddd-184">Após a reinicialização do hello, abra o snap-in de Backup do Windows Server de hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="25ddd-185">Se você não souber onde Olá snap-in foi instalado, pesquisar Olá computador ou servidor para **Backup do Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="25ddd-186">o aplicativo de área de trabalho Olá aparece nos resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="25ddd-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="25ddd-187">No snap-in hello, selecione **Backup Local**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Selecione o Backup Local toorestore lá](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="25ddd-189">No console de Backup Local hello, em Olá **painel Ações**, clique em **recuperar** tooopen Olá Assistente de recuperação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="25ddd-190">Selecione a opção hello, **um backup armazenado em outro local**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Escolha um servidor diferente do toorecover tooa](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="25ddd-192">Ao especificar o tipo de local de saudação, selecione **pasta compartilhada remota** se o backup do estado do sistema foi recuperado tooanother server.</span><span class="sxs-lookup"><span data-stu-id="25ddd-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="25ddd-193">Se o estado do sistema foi recuperado localmente, então, selecione **unidades locais**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selecione se toorecovery do servidor local ou outro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="25ddd-195">Digite hello caminho toohello *WindowsImageBackup* diretório, ou escolha Olá unidade local que contém esse diretório (por exemplo, D:\WindowsImageBackup) recuperado como parte da recuperação de arquivos de estado do sistema hello usando a recuperação do Azure Serviços de agente e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![arquivo compartilhado do caminho toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="25ddd-197">Versão de estado do sistema Olá selecione que você deseja toorestore e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="25ddd-198">No painel de selecionar tipo de recuperação hello, selecione **o estado do sistema** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="25ddd-199">Para obter local Olá Olá recuperação do estado do sistema, selecione **local Original**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25ddd-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="25ddd-200">Examine os detalhes da confirmação de saudação, verifique as configurações de reinicialização hello e clique em **recuperar** tooapplly Olá restaurado arquivos de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![saudação de inicialização restaurar arquivos de estado do sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="25ddd-202">Considerações especiais para recuperação de estado do sistema no servidor do Active Directory</span><span class="sxs-lookup"><span data-stu-id="25ddd-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="25ddd-203">O backup de estado do sistema inclui dados do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25ddd-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="25ddd-204">Use Olá seguir etapas toorestore serviço de domínio Active Directory (AD DS) de seu estado anterior do estado tooa atual.</span><span class="sxs-lookup"><span data-stu-id="25ddd-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="25ddd-205">Reinicie o controlador de domínio de saudação no modo de restauração dos serviços de diretório (DSRM).</span><span class="sxs-lookup"><span data-stu-id="25ddd-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="25ddd-206">Siga as etapas de saudação [aqui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover cmdlets de Backup do Windows Server toouse AD DS.</span><span class="sxs-lookup"><span data-stu-id="25ddd-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="25ddd-207">Solucionar problemas de restauração de estado do sistema com falha</span><span class="sxs-lookup"><span data-stu-id="25ddd-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="25ddd-208">Se o processo anterior de saudação da aplicação de estado do sistema não for concluída com êxito, use Olá toorecover de ambiente de recuperação do Windows (Windows RE) do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="25ddd-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="25ddd-209">Olá etapas a seguir explicam como toorecover usando o Windows RE.</span><span class="sxs-lookup"><span data-stu-id="25ddd-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="25ddd-210">Use esta opção somente se o Windows Server não inicia normalmente após uma restauração de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="25ddd-211">Olá processo a seguir apaga dados não são do sistema, tenha cuidado.</span><span class="sxs-lookup"><span data-stu-id="25ddd-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="25ddd-212">Inicialize o Windows Server Olá ambiente de recuperação do Windows (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="25ddd-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="25ddd-213">Selecione solucionar problemas de três opções disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="25ddd-213">Select Troubleshoot from hello three available options.</span></span>

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="25ddd-215">De saudação **opções avançadas de** tela, selecione **Prompt de comando** e forneça o nome de usuário de administrador de servidor hello e senha.</span><span class="sxs-lookup"><span data-stu-id="25ddd-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Abrir menu](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="25ddd-217">Forneça a senha e o nome de usuário de administrador de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-217">Provide hello server administrator username and password.</span></span>

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="25ddd-219">Quando você abrir o prompt de comando Olá no modo de administrador, execute o seguinte versões de backup do comando tooget Olá estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="25ddd-221">Execute Olá tooget de comando a seguir todos os volumes disponíveis no backup hello.</span><span class="sxs-lookup"><span data-stu-id="25ddd-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="25ddd-223">Olá seguinte comando recupera todos os volumes que fazem parte da saudação Backup de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="25ddd-224">Observe que essa etapa recupera somente Olá volumes críticos que fazem parte de saudação do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="25ddd-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="25ddd-225">Todos os dados que não são do sistema são apagados.</span><span class="sxs-lookup"><span data-stu-id="25ddd-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="25ddd-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25ddd-227">Next steps</span></span>
* <span data-ttu-id="25ddd-228">Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="25ddd-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
