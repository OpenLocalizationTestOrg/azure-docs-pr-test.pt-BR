---
title: 'Backup do Azure: Restaurar Estado do Sistema para um Windows Server | Microsoft Docs'
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="a3175-103">Restaurar o Estado do Sistema para Windows Server</span><span class="sxs-lookup"><span data-stu-id="a3175-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="a3175-104">Este artigo explica como restaurar backups de estado do sistema do Windows Server de um cofre de Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3175-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="a3175-105">Para restaurar o estado do sistema, você deve ter um backup de estado do sistema (criado usando as instruções em [Backup de estado do sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e certifique-se de ter instalado a [versão mais recente do agente do Serviços de Recuperação do Microsoft Azure (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="a3175-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="a3175-106">Recuperar dados de estado do sistema do Windows Server de um cofre de serviços de recuperação do Azure é um processo de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="a3175-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="a3175-107">Restaure o estado do sistema como arquivos de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3175-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="a3175-108">Ao restaurar o estado do sistema como arquivos de Backup do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="a3175-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="a3175-109">Restaurar o estado do sistema para o mesmo servidor em que os backups foram realizados, ou</span><span class="sxs-lookup"><span data-stu-id="a3175-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="a3175-110">Restaurar o arquivo de estado do sistema para um servidor alternativo.</span><span class="sxs-lookup"><span data-stu-id="a3175-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="a3175-111">Aplica os arquivos restaurados do estado do sistema para um Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3175-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="a3175-112">Recuperar arquivos de estado do sistema para o mesmo servidor</span><span class="sxs-lookup"><span data-stu-id="a3175-112">Recover System State files to the same server</span></span>
<span data-ttu-id="a3175-113">As etapas a seguir explicam como reverter a configuração do Windows Server para um estado anterior.</span><span class="sxs-lookup"><span data-stu-id="a3175-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="a3175-114">Reverter a configuração do servidor para um estado conhecido, estável, pode ser extremamente valioso.</span><span class="sxs-lookup"><span data-stu-id="a3175-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="a3175-115">As etapas a seguir restauram o estado do sistema do servidor de um cofre de Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="a3175-116">Abra o snap-in do **Backup do Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="a3175-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="a3175-117">Se você não souber onde o snap-in foi instalado, pesquise **Backup do Microsoft Azure** no computador ou servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="a3175-118">O aplicativo da área de trabalho deve aparecer nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a3175-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="a3175-119">Clique em **Recuperar Dados** para iniciar o assistente.</span><span class="sxs-lookup"><span data-stu-id="a3175-119">Click **Recover Data** to start the wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="a3175-121">No painel **Introdução**, para restaurar os dados para o mesmo computador ou servidor, selecione **Este servidor (`<server name>`)** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a3175-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha a opção Este servidor para restaurar os dados para o mesmo computador](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="a3175-123">No painel **Selecionar Modo de Recuperação**, escolha **Estado do Sistema** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="a3175-125">No calendário no painel **Selecionar Volume e Data**, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="a3175-126">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a3175-127">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a3175-128">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="a3175-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="a3175-130">Depois de ter escolhido o ponto de recuperação a ser restaurado, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="a3175-131">O Backup do Azure monta o ponto de recuperação local e o usa como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="a3175-132">No próximo painel, especifique o destino para os arquivos recuperados do estado do sistema e clique em **Procurar** para abrir o Windows Explorer e localize os arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="a3175-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="a3175-133">A opção **Criar cópias para ter ambas as versões** cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia do arquivo de estado do sistema inteiro.</span><span class="sxs-lookup"><span data-stu-id="a3175-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="a3175-135">Verifique os detalhes da recuperação no painel de **confirmação** e clique em **Recuperar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![Clique em Recuperar para confirmar a ação de recuperação](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="a3175-137">Copie o diretório *WindowsImageBackup* no destino de recuperação para um volume não crítico do servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="a3175-138">Geralmente, o volume do sistema operacional Windows é o volume crítico.</span><span class="sxs-lookup"><span data-stu-id="a3175-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="a3175-139">Quando a recuperação for bem-sucedida, siga as etapas na seção [Aplicar arquivos restaurados de estado do sistema para o Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) para concluir o processo de recuperação do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="a3175-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="a3175-140">Recuperar o arquivo de estado do sistema para um servidor alternativo</span><span class="sxs-lookup"><span data-stu-id="a3175-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="a3175-141">Se seu Windows Server estiver corrompido ou inacessível e você deseja restaurá-lo para um estado estável, recuperando o estado do sistema do Windows Server, você pode restaurar o estado do sistema do servidor corrompido de outro servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="a3175-142">Use as seguintes etapas para a restauração de estado do sistema em um servidor separado.</span><span class="sxs-lookup"><span data-stu-id="a3175-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="a3175-143">A terminologia usada nessas etapas inclui:</span><span class="sxs-lookup"><span data-stu-id="a3175-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="a3175-144">*Máquina de origem* : a máquina original da qual o backup foi feito e que está indisponível no momento.</span><span class="sxs-lookup"><span data-stu-id="a3175-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="a3175-145">*Computador de destino* – O computador para o qual os dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="a3175-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="a3175-146">*Cofre de exemplo* – o cofre Serviços de Recuperação no qual a *Máquina de origem* e a *Máquina de destino* estão registradas.</span><span class="sxs-lookup"><span data-stu-id="a3175-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="a3175-147">Os backups de um computador não podem ser restaurados em um computador que esteja executando uma versão anterior do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a3175-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="a3175-148">Por exemplo, os backups de um computador Windows Server 2016 não podem ser restaurados para o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a3175-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="a3175-149">No entanto, o inverso é possível.</span><span class="sxs-lookup"><span data-stu-id="a3175-149">However, the inverse is possible.</span></span> <span data-ttu-id="a3175-150">Você pode usar os backups do Windows Server 2012 R2 para restaurar o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a3175-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="a3175-151">Abra o snap-in do **Backup do Microsoft Azure** no *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="a3175-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="a3175-152">Verifique se a *Máquina de destino* e a *Máquina de origem* estão registradas no mesmo cofre Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="a3175-153">Clique em **Recuperar Dados** para iniciar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a3175-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="a3175-155">Selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="a3175-155">Select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="a3175-157">Forneça o arquivo de credencial de cofre que corresponde ao *Cofre de exemplo*.</span><span class="sxs-lookup"><span data-stu-id="a3175-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="a3175-158">Se o arquivo de credencial de cofre for inválido (ou tiver expirado), baixe um novo arquivo de credencial de cofre do *Cofre de exemplo* no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3175-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="a3175-159">Depois que o arquivo de credencial de cofre for fornecido, o cofre de Serviços de Recuperação associado ao arquivo de credencial de cofre é exibido.</span><span class="sxs-lookup"><span data-stu-id="a3175-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="a3175-160">No painel Selecionar Servidor de Backup, selecione o *Computador de origem* na lista de computadores exibidos.</span><span class="sxs-lookup"><span data-stu-id="a3175-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="a3175-162">No painel Selecionar Modo de Recuperação, escolha **Estado do Sistema** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Pesquisar](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="a3175-164">No Calendário no painel **Selecionar Volume e Data**, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="a3175-165">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a3175-166">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a3175-167">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="a3175-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![Pesquisar itens](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="a3175-169">Depois de ter escolhido o ponto de recuperação a ser restaurado, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="a3175-170">No painel **Selecionar modo de recuperação de estado do sistema**, especifique o destino onde você deseja que os arquivos de estado do sistema sejam recuperados, e em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![Criptografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="a3175-172">A opção **Criar cópias para ter ambas as versões** cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia do arquivo de estado do sistema inteiro.</span><span class="sxs-lookup"><span data-stu-id="a3175-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="a3175-173">Verifique os detalhes da recuperação no painel de Confirmação e clique em **Recuperar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![Clique no botão Recuperar para confirmar o processo de recuperação](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="a3175-175">Copie o diretório *WindowsImageBackup* para um volume não crítico do servidor (por exemplo D:\).</span><span class="sxs-lookup"><span data-stu-id="a3175-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="a3175-176">Geralmente, o volume do sistema operacional Windows é o volume crítico.</span><span class="sxs-lookup"><span data-stu-id="a3175-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="a3175-177">Para concluir o processo de recuperação, use a seguinte seção para [aplicar os arquivos restaurados do estado do sistema em um Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="a3175-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="a3175-178">Aplicar o estado do sistema restaurado em um Windows Server</span><span class="sxs-lookup"><span data-stu-id="a3175-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="a3175-179">Uma vez você tiver recuperado o estado do sistema como arquivos usando o agente de serviços de recuperação do Azure, use o utilitário de Backup do Windows Server para aplicar o estado do sistema recuperado para o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3175-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="a3175-180">O utilitário de Backup do Windows Server já está disponível no servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="a3175-181">As etapas a seguir explicam como aplicar o estado do sistema recuperado.</span><span class="sxs-lookup"><span data-stu-id="a3175-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="a3175-182">Use os seguintes comandos para reiniciar o servidor em *Modo de reparo de serviços de diretório*.</span><span class="sxs-lookup"><span data-stu-id="a3175-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="a3175-183">Em um prompt de comandos com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="a3175-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="a3175-184">Após a reinicialização, abra o snap-in Backup do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3175-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="a3175-185">Se você não souber onde o snap-in foi instalado, pesquise **Backup do Windows Server** no computador ou servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="a3175-186">O aplicativo da área de trabalho aparece nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a3175-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="a3175-187">No snap-in, selecione **Backup Local**.</span><span class="sxs-lookup"><span data-stu-id="a3175-187">In the snap-in, select **Local Backup**.</span></span>

    ![Selecionar Backup Local para restaurar a partir daí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="a3175-189">No console do Backup Local, no **Painel Ações**, clique em **Recuperar** para abrir o Assistente de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="a3175-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="a3175-190">Selecione a opção **um backup armazenado em outro local**e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Escolha recuperar para um servidor diferente](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="a3175-192">Ao especificar o tipo de local, selecione **Pasta compartilhada remota** se o backup do estado do sistema foi recuperado em outro servidor.</span><span class="sxs-lookup"><span data-stu-id="a3175-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="a3175-193">Se o estado do sistema foi recuperado localmente, então, selecione **unidades locais**.</span><span class="sxs-lookup"><span data-stu-id="a3175-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selecione se é recuperação de servidor local ou outro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="a3175-195">Insira o caminho para o diretório *WindowsImageBackup*, ou escolha a unidade local que contém esse diretório (por exemplo, D:\WindowsImageBackup) recuperado como parte da recuperação de arquivos de estado do sistema usando o agente de serviços de recuperação do Azure e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![Caminho para o arquivo compartilhado](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="a3175-197">Selecione a versão de estado do sistema que você deseja restaurar e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="a3175-198">No painel Selecionar Tipo de Recuperação, selecione **Estado do Sistema** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="a3175-199">Para o local da Recuperação do Estado do Sistema, selecione **Local Original**, e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3175-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="a3175-200">Examine os detalhes da confirmação, verifique as configurações de reinicialização e clique em **Recuperar** para aplicar os arquivos do estado do sistema restaurado.</span><span class="sxs-lookup"><span data-stu-id="a3175-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![Inicie a restauração de arquivos de estado do sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="a3175-202">Considerações especiais para recuperação de estado do sistema no servidor do Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3175-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="a3175-203">O backup de estado do sistema inclui dados do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3175-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="a3175-204">Use as etapas a seguir para restaurar o Serviço de Domínio do Active Directory (AD DS) de seu estado atual para um estado anterior.</span><span class="sxs-lookup"><span data-stu-id="a3175-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="a3175-205">Reinicie o controlador de domínio no Modo de Restauração dos Serviços de Diretório (DSRM).</span><span class="sxs-lookup"><span data-stu-id="a3175-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="a3175-206">Siga as etapas [aqui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) para usar cmdlets do Backup do Windows Server para recuperar o AD DS.</span><span class="sxs-lookup"><span data-stu-id="a3175-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="a3175-207">Solucionar problemas de restauração de estado do sistema com falha</span><span class="sxs-lookup"><span data-stu-id="a3175-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="a3175-208">Se o processo anterior de aplicação de estado do sistema não for concluído com êxito, use o ambiente de recuperação do Windows (Windows RE) para recuperar o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3175-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="a3175-209">As etapas a seguir explicam como recuperar usando o Win RE.</span><span class="sxs-lookup"><span data-stu-id="a3175-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="a3175-210">Use esta opção somente se o Windows Server não inicia normalmente após uma restauração de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="a3175-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="a3175-211">O processo a seguir apaga dados que não são do sistema, tenha cuidado.</span><span class="sxs-lookup"><span data-stu-id="a3175-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="a3175-212">Inicialização do Windows Server para o ambiente de recuperação do Windows (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="a3175-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="a3175-213">Selecione a solução de problemas entre as três opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a3175-213">Select Troubleshoot from the three available options.</span></span>

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="a3175-215">Na tela **Opções Avançadas**, selecione o **Prompt de comando** e forneça o nome de usuário de administrador do servidor e a senha.</span><span class="sxs-lookup"><span data-stu-id="a3175-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![Abrir menu](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="a3175-217">Forneça o nome de usuário de administrador do servidor e a senha.</span><span class="sxs-lookup"><span data-stu-id="a3175-217">Provide the server administrator username and password.</span></span>

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="a3175-219">Quando você abrir o prompt de comando no modo de administrador, execute o seguinte comando para obter as versões de backup de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="a3175-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="a3175-221">Execute o seguinte comando para obter todos os volumes disponíveis no backup.</span><span class="sxs-lookup"><span data-stu-id="a3175-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="a3175-223">O comando a seguir recupera todos os volumes que fazem parte do backup do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="a3175-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="a3175-224">Observe que essa etapa recupera somente os volumes críticos que fazem parte do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="a3175-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="a3175-225">Todos os dados que não são do sistema são apagados.</span><span class="sxs-lookup"><span data-stu-id="a3175-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="a3175-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3175-227">Next steps</span></span>
* <span data-ttu-id="a3175-228">Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="a3175-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
