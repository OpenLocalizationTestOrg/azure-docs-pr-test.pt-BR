---
title: "Restaurar dados para um Windows Server ou Client do Azure usando o modelo de implantação clássico | Microsoft Docs"
description: Saiba como restaurar de um Windows Server ou Windows Client.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="99ae6-103">Restaurar arquivos em um computador de cliente do Windows ou Windows Server usando o modelo de implantação do clásico</span><span class="sxs-lookup"><span data-stu-id="99ae6-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99ae6-104">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="99ae6-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="99ae6-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="99ae6-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="99ae6-106">Este artigo explica como recuperar dados de um cofre de backup e restaurá-lod para um computador ou servidor.</span><span class="sxs-lookup"><span data-stu-id="99ae6-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="99ae6-107">A partir de março de 2017, você não poderá mais usar o portal clássico para criar os cofres de backup.</span><span class="sxs-lookup"><span data-stu-id="99ae6-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99ae6-108">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="99ae6-109">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="99ae6-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="99ae6-110">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="99ae6-111">**15 de outubro de 2017**, você não poderá mais usar o PowerShell para criar cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="99ae6-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="99ae6-112">**A partir de 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="99ae6-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="99ae6-113">Nenhum cofre de Backup restante será atualizado automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="99ae6-114">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="99ae6-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="99ae6-115">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="99ae6-116">Para restaurar dados, você pode usar o assistente recuperar dados do agente do Serviços de Recuperação do Microsoft Azure (MARS).</span><span class="sxs-lookup"><span data-stu-id="99ae6-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="99ae6-117">Ao restaurar dados, é possível:</span><span class="sxs-lookup"><span data-stu-id="99ae6-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="99ae6-118">Restaurar dados para o mesmo computador do qual os backups foram realizados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="99ae6-119">Restaurar dados para um computador alternativo.</span><span class="sxs-lookup"><span data-stu-id="99ae6-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="99ae6-120">Em janeiro de 2017, a Microsoft lançou uma atualização de Versão Prévia para o agente do MARS.</span><span class="sxs-lookup"><span data-stu-id="99ae6-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="99ae6-121">Juntamente com as correções de bug, essa atualização permite Restauração Instantânea, que permite que você monte um instantâneo de ponto de recuperação gravável como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="99ae6-122">Em seguida, é possível explorar os arquivos de volume de recuperação e de cópia em um computador local e, assim, restaurar arquivos de forma seletiva.</span><span class="sxs-lookup"><span data-stu-id="99ae6-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="99ae6-123">A [atualização do Backup do Azure de janeiro de 2017](https://support.microsoft.com/en-us/help/3216528?preview) será necessária se você desejar usar a Restauração Instantânea para restaurar dados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="99ae6-124">Além disso, os dados de backup devem ser protegidos em cofres nas localidades listadas no artigo de suporte.</span><span class="sxs-lookup"><span data-stu-id="99ae6-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="99ae6-125">Consulte a [atualização do Backup do Azure de janeiro de 2017](https://support.microsoft.com/en-us/help/3216528?preview) para obter a lista mais recente de localidades que oferecem suporte à Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="99ae6-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="99ae6-126">No momento, a Restauração Instantânea **não** está disponível em todas as localidades.</span><span class="sxs-lookup"><span data-stu-id="99ae6-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="99ae6-127">A Restauração Instantânea está disponível para uso em cofres dos Serviços de Recuperação no portal do Azure e em cofres de Backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="99ae6-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="99ae6-128">Se desejar usar a Restauração Instantânea, baixe a atualização do MARS e siga os procedimentos que mencionam a Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="99ae6-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="99ae6-129">Use a Restauração Instantânea para recuperar dados no mesmo computador</span><span class="sxs-lookup"><span data-stu-id="99ae6-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="99ae6-130">Se você excluiu acidentalmente um arquivo e deseja restaurá-lo para o mesmo computador (do qual o backup foi feito), as etapas a seguir o ajudarão a recuperar os dados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="99ae6-131">Abra o snap-in do **Backup do Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="99ae6-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="99ae6-132">Se você não souber onde o snap-in foi instalado, pesquise **Backup do Microsoft Azure** no computador ou servidor.</span><span class="sxs-lookup"><span data-stu-id="99ae6-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="99ae6-133">O aplicativo da área de trabalho deve aparecer nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="99ae6-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="99ae6-134">Clique em **Recuperar Dados** para iniciar o assistente.</span><span class="sxs-lookup"><span data-stu-id="99ae6-134">Click **Recover Data** to start the wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="99ae6-136">No painel **Introdução**, para restaurar os dados para o mesmo computador ou servidor, selecione **Este servidor (`<server name>`)** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha a opção Este servidor para restaurar os dados para o mesmo computador](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="99ae6-138">No painel **Selecionar Modo de Recuperação**, escolha **Pastas e arquivos individuais** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="99ae6-140">No painel **Selecionar Volume e Data**, selecione o volume que contém os arquivos e/ou pastas que deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="99ae6-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="99ae6-141">No calendário, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="99ae6-142">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="99ae6-143">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="99ae6-144">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="99ae6-146">Depois de ter escolhido o ponto de recuperação a ser restaurado, clique em **Montar**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="99ae6-147">O Backup do Azure monta o ponto de recuperação local e o usa como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="99ae6-148">No painel **Procurar e Recuperar Arquivos**, clique em **Procurar** para abrir o Windows Explorer e localize os arquivos e pastas desejados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="99ae6-150">No Windows Explorer, copie os arquivos e/ou pastas que deseja restaurar e cole-os em qualquer localização local no servidor ou computador.</span><span class="sxs-lookup"><span data-stu-id="99ae6-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="99ae6-151">Você pode abrir ou transmitir os arquivos diretamente do volume de recuperação e verificar se as versões corretas são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="99ae6-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiar e colar arquivos e pastas do volume montado na localização local](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="99ae6-153">Quando você terminar de restaurar os arquivos e/ou pastas, no painel **Procurar e Recuperar Arquivos**, clique em **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="99ae6-154">Clique em **Sim** para confirmar que deseja desmontar o volume.</span><span class="sxs-lookup"><span data-stu-id="99ae6-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Desmontar o volume e confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="99ae6-156">Se você não clicar em Desmontar, o Volume de Recuperação permanecerá montado por seis horas a partir da hora em que foi montado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="99ae6-157">Não será executada nenhuma operação de backup enquanto o volume estiver montado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="99ae6-158">Qualquer operação de backup agendada para execução durante o tempo em que o volume estiver montado será executada após o volume de recuperação ser desmontado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="99ae6-159">Recuperar dados para o mesmo computador</span><span class="sxs-lookup"><span data-stu-id="99ae6-159">Recover data to the same machine</span></span>
<span data-ttu-id="99ae6-160">Se você excluiu acidentalmente um arquivo e deseja restaurá-lo para o mesmo computador (do qual o backup foi feito), as etapas a seguir o ajudarão a recuperar os dados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="99ae6-161">Abra o snap-in do **Backup do Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="99ae6-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="99ae6-162">Clique em **Recuperar Dados** para iniciar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99ae6-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="99ae6-164">Selecione a opção **Este servidor (*nomeseucomputador*)** para restaurar o backup do arquivo no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="99ae6-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![Mesmo computador](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="99ae6-166">Escolha **Procurar arquivos** ou **Pesquisar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="99ae6-167">Deixe a opção padrão se você planeja restaurar um ou mais arquivos cujo caminho é conhecido.</span><span class="sxs-lookup"><span data-stu-id="99ae6-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="99ae6-168">Se você não tiver certeza sobre a estrutura de pastas, mas gostaria de procurar por um arquivo, selecione a opção **Pesquisar arquivos** .</span><span class="sxs-lookup"><span data-stu-id="99ae6-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="99ae6-169">Para fins desta seção, prosseguiremos com a opção padrão.</span><span class="sxs-lookup"><span data-stu-id="99ae6-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="99ae6-171">Selecione o volume do qual você deseja restaurar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="99ae6-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="99ae6-172">Você pode restaurar de qualquer momento anterior.</span><span class="sxs-lookup"><span data-stu-id="99ae6-172">You can restore from any point in time.</span></span> <span data-ttu-id="99ae6-173">As datas que aparecem em **negrito** no controle de calendário indicam a disponibilidade de um ponto de restauração.</span><span class="sxs-lookup"><span data-stu-id="99ae6-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="99ae6-174">Quando uma data é selecionada, com base em seu agendamento de backup (e o sucesso de uma operação de backup), você pode selecionar um ponto no tempo no menu suspenso **Tempo** .</span><span class="sxs-lookup"><span data-stu-id="99ae6-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="99ae6-176">Selecione os itens que serão recuperados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-176">Select the items to recover.</span></span> <span data-ttu-id="99ae6-177">Você pode selecionar várias pastas/arquivos que deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="99ae6-177">You can multi-select folders/files you wish to restore.</span></span>

    ![Selecionar arquivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="99ae6-179">Especifique os parâmetros de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-179">Specify the recovery parameters.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="99ae6-181">Você tem uma opção de restaurar no local original (em que a pasta/o arquivo será substituído) ou em outro local no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="99ae6-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="99ae6-182">Se o arquivo/pasta que você deseja restaurar existir no local de destino, você tem a opção de criar cópias (duas versões do mesmo arquivo), substituir os arquivos no local de destino ou ignorar a recuperação dos arquivos que existem no destino.</span><span class="sxs-lookup"><span data-stu-id="99ae6-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="99ae6-183">É altamente recomendável que você deixe a opção padrão de restaurar as ACLs nos arquivos que estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="99ae6-184">Depois que essas entradas forem fornecidas, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="99ae6-185">O fluxo de trabalho de recuperação, que restaura os arquivos para essa máquina, será iniciado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="99ae6-186">Recuperar em um computador alternativo</span><span class="sxs-lookup"><span data-stu-id="99ae6-186">Recover to an alternate machine</span></span>
<span data-ttu-id="99ae6-187">Se o servidor inteiro for perdido, você ainda pode recuperar dados do backup do Azure para um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="99ae6-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="99ae6-188">As etapas a seguir ilustram o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99ae6-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="99ae6-189">A terminologia usada nessas etapas inclui:</span><span class="sxs-lookup"><span data-stu-id="99ae6-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="99ae6-190">*Máquina de origem* : a máquina original da qual o backup foi feito e que está indisponível no momento.</span><span class="sxs-lookup"><span data-stu-id="99ae6-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="99ae6-191">*Computador de destino* – O computador para o qual os dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="99ae6-192">*Cofre de exemplo* – Cofre de backup em que o *Computador de origem* e o *Computador de destino são registrados*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="99ae6-193">Os backups de um computador não podem ser restaurados em um computador que esteja executando uma versão anterior do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="99ae6-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="99ae6-194">Por exemplo, se um backup for de um computador com Windows 7, ele poderá ser restaurado em um computador com Windows 8 ou superior.</span><span class="sxs-lookup"><span data-stu-id="99ae6-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="99ae6-195">No entanto, o contrário não pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="99ae6-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="99ae6-196">Abra o snap-in do **Backup do Microsoft Azure** no *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="99ae6-197">Verifique se o *Computador de destino* e o *Computador de origem* serão restaurados no mesmo cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="99ae6-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="99ae6-198">Clique em **Recuperar Dados** para iniciar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99ae6-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="99ae6-200">Selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="99ae6-200">Select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="99ae6-202">Forneça o arquivo de credencial de cofre que corresponde ao *Cofre de exemplo*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="99ae6-203">Se o arquivo de credencial do cofre for inválido (ou tiver expirado), baixe um novo arquivo de credencial do *Cofre de exemplo* no Portal do Azure clássico.</span><span class="sxs-lookup"><span data-stu-id="99ae6-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="99ae6-204">Depois que o arquivo de credencial de cofre for fornecido, o cofre de backup relacionado ao arquivo de credencial de cofre será exibido.</span><span class="sxs-lookup"><span data-stu-id="99ae6-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="99ae6-205">Selecione o *Computador de origem* na lista de computadores exibidos.</span><span class="sxs-lookup"><span data-stu-id="99ae6-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="99ae6-207">Selecione a opção **Pesquisar arquivos** ou **Procurar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="99ae6-208">Para os fins desta seção, usaremos a opção **Pesquisar arquivos** .</span><span class="sxs-lookup"><span data-stu-id="99ae6-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="99ae6-210">Na próxima tela, selecione o volume e a data.</span><span class="sxs-lookup"><span data-stu-id="99ae6-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="99ae6-211">Procure o nome do arquivo/pasta que você deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="99ae6-211">Search for the folder/file name you want to restore.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="99ae6-213">Selecione o local no qual os arquivos precisam ser restaurados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-213">Select the location where the files need to be restored.</span></span>

    ![Restaurar local](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="99ae6-215">Forneça a senha de criptografia determinada durante o registro da *Máquina de origem* no *Cofre de exemplo*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="99ae6-217">Após a entrada ser fornecida, clique no botão **Recuperar**, o que inicia a restauração dos arquivos de backup no destino fornecido.</span><span class="sxs-lookup"><span data-stu-id="99ae6-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="99ae6-218">Usar a Restauração Instantânea para restaurar dados em um computador alternativo</span><span class="sxs-lookup"><span data-stu-id="99ae6-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="99ae6-219">Se o servidor inteiro for perdido, você ainda pode recuperar dados do backup do Azure para um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="99ae6-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="99ae6-220">As etapas a seguir ilustram o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99ae6-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="99ae6-221">A terminologia usada nessas etapas inclui:</span><span class="sxs-lookup"><span data-stu-id="99ae6-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="99ae6-222">*Máquina de origem* : a máquina original da qual o backup foi feito e que está indisponível no momento.</span><span class="sxs-lookup"><span data-stu-id="99ae6-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="99ae6-223">*Computador de destino* – O computador para o qual os dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="99ae6-224">*Cofre de exemplo* – o cofre Serviços de Recuperação no qual a *Máquina de origem* e a *Máquina de destino* estão registradas.</span><span class="sxs-lookup"><span data-stu-id="99ae6-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="99ae6-225">Os backups não podem ser restaurados em um computador de destino executando uma versão anterior do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="99ae6-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="99ae6-226">Por exemplo, um backup feito em um computador com Windows 7 pode ser restaurado em um computador com Windows 8 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="99ae6-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="99ae6-227">Um backup feito em um computador com Windows 8 não pode ser restaurado em um computador com Windows 7.</span><span class="sxs-lookup"><span data-stu-id="99ae6-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="99ae6-228">Abra o snap-in do **Backup do Microsoft Azure** no *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="99ae6-229">Verifique se o *Computador de destino* e o *Computador de origem* estão registrados no mesmo cofre de Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="99ae6-230">Clique em **Recuperar Dados** para abrir o **Assistente de Recuperação de Dados**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="99ae6-232">No painel **Introdução**, selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="99ae6-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="99ae6-234">Forneça o arquivo de credencial de cofre que corresponde ao *Cofre de exemplo* e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="99ae6-235">Se o arquivo de credencial de cofre for inválido (ou tiver expirado), baixe um novo arquivo de credencial de cofre do *Cofre de exemplo* no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="99ae6-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="99ae6-236">Depois de fornecer uma credencial de cofre válida, o nome do Cofre de Backup correspondente aparecerá.</span><span class="sxs-lookup"><span data-stu-id="99ae6-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="99ae6-237">No painel **Selecionar Servidor de Backup**, selecione o *Computador de origem* na lista de computadores exibidos e forneça a senha.</span><span class="sxs-lookup"><span data-stu-id="99ae6-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="99ae6-238">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-238">Then click **Next**.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="99ae6-240">No painel **Selecionar Modo de Recuperação**, selecione **Pastas e arquivos individuais** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="99ae6-242">No painel **Selecionar Volume e Data**, selecione o volume que contém os arquivos e/ou pastas que deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="99ae6-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="99ae6-243">No calendário, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="99ae6-244">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="99ae6-245">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99ae6-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="99ae6-246">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="99ae6-248">Clique em **Montar** para montar localmente o ponto de recuperação como um volume de recuperação em seu *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="99ae6-249">No painel **Procurar e Recuperar Arquivos**, clique em **Procurar** para abrir o Windows Explorer e localize os arquivos e pastas desejados.</span><span class="sxs-lookup"><span data-stu-id="99ae6-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="99ae6-251">No Windows Explorer, copie os arquivos e/ou pastas do volume de recuperação e cole-os na localização de seu *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="99ae6-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="99ae6-252">Você pode abrir ou transmitir os arquivos diretamente do volume de recuperação e verificar se as versões corretas são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="99ae6-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="99ae6-254">Quando você terminar de restaurar os arquivos e/ou pastas, no painel **Procurar e Recuperar Arquivos**, clique em **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="99ae6-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="99ae6-255">Clique em **Sim** para confirmar que deseja desmontar o volume.</span><span class="sxs-lookup"><span data-stu-id="99ae6-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="99ae6-257">Se você não clicar em Desmontar, o Volume de Recuperação permanecerá montado por seis horas a partir da hora em que foi montado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="99ae6-258">Não será executada nenhuma operação de backup enquanto o volume estiver montado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="99ae6-259">Qualquer operação de backup agendada para execução durante o tempo em que o volume estiver montado será executada após o volume de recuperação ser desmontado.</span><span class="sxs-lookup"><span data-stu-id="99ae6-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="99ae6-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99ae6-260">Next steps</span></span>
* [<span data-ttu-id="99ae6-261">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="99ae6-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="99ae6-262">Visite o [Fórum de backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="99ae6-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="99ae6-263">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="99ae6-263">Learn more</span></span>
* [<span data-ttu-id="99ae6-264">Visão geral do backup do Azure</span><span class="sxs-lookup"><span data-stu-id="99ae6-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="99ae6-265">Fazer backup de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="99ae6-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="99ae6-266">Fazer backup de cargas de trabalho Microsoft</span><span class="sxs-lookup"><span data-stu-id="99ae6-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
