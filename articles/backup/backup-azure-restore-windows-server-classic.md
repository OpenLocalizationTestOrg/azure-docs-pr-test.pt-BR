---
title: "Olá de aaaRestore tooa de dados do Windows Server ou Windows Client do Azure usando o modelo de implantação clássico | Microsoft Docs"
description: Saiba como toorestore de um cliente do Windows ou Windows Server.
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
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="aab04-103">Restaurar arquivos tooa Windows server ou o computador de cliente do Windows usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="aab04-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aab04-104">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="aab04-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="aab04-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aab04-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="aab04-106">Este artigo explica como toorecover dados de um backup de cofre e restauração-lo tooa servidor ou computador.</span><span class="sxs-lookup"><span data-stu-id="aab04-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="aab04-107">A partir de março de 2017, você não pode mais criar cofres de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aab04-108">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="aab04-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="aab04-109">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="aab04-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="aab04-110">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="aab04-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="aab04-111">**15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="aab04-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="aab04-112">**A partir de 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="aab04-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="aab04-113">Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="aab04-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="aab04-114">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="aab04-115">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="aab04-116">toorestore dados, você usa o Assistente de recuperar dados de saudação no agente do Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="aab04-117">Ao restaurar dados, é possível:</span><span class="sxs-lookup"><span data-stu-id="aab04-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="aab04-118">Restaurar dados toohello mesmo computador do qual os backups Olá foram realizados.</span><span class="sxs-lookup"><span data-stu-id="aab04-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="aab04-119">Restaure a máquina alternativo de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="aab04-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="aab04-120">Em janeiro de 2017, a Microsoft lançou um agente de MARS toohello de atualização de visualização.</span><span class="sxs-lookup"><span data-stu-id="aab04-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="aab04-121">Juntamente com correções de bug, essa atualização permite restauração instantânea, que permite que você toomount um instantâneo de ponto de recuperação gravável como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="aab04-122">Em seguida, você pode explorar Olá recuperação volume e copiar arquivos tooa computador local restaurando assim seletivamente arquivos.</span><span class="sxs-lookup"><span data-stu-id="aab04-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="aab04-123">Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) é necessária se você quiser toouse restauração instantânea toorestore dados.</span><span class="sxs-lookup"><span data-stu-id="aab04-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="aab04-124">Também os dados de backup Olá devem ser protegidos no cofres em localidades listados no artigo de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="aab04-125">Consulte Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) para a lista mais recente Olá das localidades que oferecem suporte à restauração instantânea.</span><span class="sxs-lookup"><span data-stu-id="aab04-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="aab04-126">No momento, a Restauração Instantânea **não** está disponível em todas as localidades.</span><span class="sxs-lookup"><span data-stu-id="aab04-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="aab04-127">Restauração instantânea está disponível para uso em cofres de serviços de recuperação no hello portal do Azure e cofres de Backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="aab04-128">Se você quiser toouse restauração instantânea, baixe a atualização de MARS Olá e siga os procedimentos de saudação que mencionem restauração instantânea.</span><span class="sxs-lookup"><span data-stu-id="aab04-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="aab04-129">Use a restauração instantânea toohello de dados toorecover mesmo computador</span><span class="sxs-lookup"><span data-stu-id="aab04-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="aab04-130">Se você excluiu acidentalmente um arquivo e quiser toorestore-toohello mesma máquina (do qual Olá é feito backup), Olá seguindo as etapas ajudará você a recuperar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="aab04-131">Olá abrir **Backup do Microsoft Azure** encaixe em.</span><span class="sxs-lookup"><span data-stu-id="aab04-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="aab04-132">Se você não souber onde o snap-in de saudação foi instalado, pesquisar Olá computador ou servidor para **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="aab04-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="aab04-133">aplicativo de área de trabalho de saudação deve aparecer nos resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="aab04-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="aab04-134">Clique em **recuperar dados** toostart Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="aab04-136">Em Olá **Introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha esse servidor opção toorestore Olá dados toohello mesmo computador](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="aab04-138">Em Olá **Selecionar modo de recuperação** painel, escolha **arquivos e pastas individuais** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="aab04-140">Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="aab04-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="aab04-141">No calendário hello, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="aab04-142">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="aab04-143">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="aab04-144">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="aab04-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="aab04-146">Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **montar**.</span><span class="sxs-lookup"><span data-stu-id="aab04-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="aab04-147">O Backup do Azure monta o ponto de recuperação locais hello e utiliza como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="aab04-148">Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="aab04-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="aab04-150">No Windows Explorer, Olá copiar os arquivos e/ou pastas você deseja toorestore e colá-los tooany local toohello local servidor ou computador.</span><span class="sxs-lookup"><span data-stu-id="aab04-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="aab04-151">Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="aab04-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copie e cole os arquivos e pastas do local do volume montado toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="aab04-153">Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**.</span><span class="sxs-lookup"><span data-stu-id="aab04-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="aab04-154">Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.</span><span class="sxs-lookup"><span data-stu-id="aab04-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Desmontar o volume de saudação e confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="aab04-156">Se você não clicar desmontagem, Olá Volume de recuperação permanecerá montada por seis horas de tempo de saudação quando ele foi montado.</span><span class="sxs-lookup"><span data-stu-id="aab04-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="aab04-157">Nenhuma operação de backup será executado enquanto Olá volume está montado.</span><span class="sxs-lookup"><span data-stu-id="aab04-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="aab04-158">Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.</span><span class="sxs-lookup"><span data-stu-id="aab04-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="aab04-159">Recuperar dados toohello mesmo computador</span><span class="sxs-lookup"><span data-stu-id="aab04-159">Recover data toohello same machine</span></span>
<span data-ttu-id="aab04-160">Se você excluiu acidentalmente um arquivo e quiser toorestore-toohello mesma máquina (do qual Olá é feito backup), Olá seguindo as etapas ajudará você a recuperar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="aab04-161">Olá abrir **Backup do Microsoft Azure** encaixe em.</span><span class="sxs-lookup"><span data-stu-id="aab04-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="aab04-162">Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="aab04-164">Olá selecione  **neste servidor (*yourmachinename*) * * saudação de toorestore opção backup arquivo hello mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="aab04-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Mesmo computador](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="aab04-166">Escolha muito**procurar arquivos** ou **pesquisar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="aab04-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="aab04-167">Deixe saudação padrão opção se você planejar toorestore um ou mais arquivos cujo caminho é conhecido.</span><span class="sxs-lookup"><span data-stu-id="aab04-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="aab04-168">Se você não tiver certeza sobre a estrutura de pasta Olá, mas desejar toosearch para um arquivo, selecione Olá **pesquisar arquivos** opção.</span><span class="sxs-lookup"><span data-stu-id="aab04-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="aab04-169">Finalidade Olá nesta seção, vamos continuará com a opção padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="aab04-171">Selecione o volume de saudação do qual você deseja que o arquivo de saudação toorestore.</span><span class="sxs-lookup"><span data-stu-id="aab04-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="aab04-172">Você pode restaurar de qualquer momento anterior.</span><span class="sxs-lookup"><span data-stu-id="aab04-172">You can restore from any point in time.</span></span> <span data-ttu-id="aab04-173">Datas que aparecem no **negrito** no controle de calendário Olá indicar a disponibilidade de saudação de um ponto de restauração.</span><span class="sxs-lookup"><span data-stu-id="aab04-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="aab04-174">Quando uma data é selecionada, com base em seu agendamento de backup (e o sucesso de saudação de uma operação de backup), você pode selecionar um ponto no tempo de saudação **tempo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aab04-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="aab04-176">Selecione Olá toorecover de itens.</span><span class="sxs-lookup"><span data-stu-id="aab04-176">Select hello items toorecover.</span></span> <span data-ttu-id="aab04-177">Você pode selecionar várias pastas/arquivos que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="aab04-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Selecionar arquivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="aab04-179">Especifica parâmetros de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-179">Specify hello recovery parameters.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="aab04-181">Você tem a opção de restauração toohello local original (no qual Olá arquivo/pasta seria substituída) ou tooanother em Olá mesma máquina.</span><span class="sxs-lookup"><span data-stu-id="aab04-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="aab04-182">Se Olá arquivo/pasta toorestore existe no local de destino hello, você pode criar cópias (duas versões do hello mesmo arquivo), substituir arquivos Olá no local de destino hello ou ignorar a recuperação de saudação de arquivos de saudação que existe no destino hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="aab04-183">É altamente recomendável que você deixe a opção padrão de saudação da restauração de ACLs de saudação em arquivos de saudação que estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="aab04-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="aab04-184">Depois que essas entradas forem fornecidas, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="aab04-185">Olá recuperação fluxo de trabalho, que restaura Olá arquivos toothis máquina, será iniciado.</span><span class="sxs-lookup"><span data-stu-id="aab04-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="aab04-186">Recuperar máquina alternativo tooan</span><span class="sxs-lookup"><span data-stu-id="aab04-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="aab04-187">Se o servidor inteiro for perdido, você ainda poderá recuperar dados de máquina do Azure Backup tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="aab04-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="aab04-188">Olá etapas a seguir ilustra o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="aab04-189">terminologia de saudação usada essas etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="aab04-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="aab04-190">*Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="aab04-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="aab04-191">*Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="aab04-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="aab04-192">*Cofre de exemplo* – Olá Olá de toowhich de Cofre de Backup *máquina de origem* e *máquina destino* são registrados.</span><span class="sxs-lookup"><span data-stu-id="aab04-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="aab04-193">Os backups de uma máquina não podem ser restaurados em um computador que está executando uma versão anterior do sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="aab04-194">Por exemplo, se um backup for de um computador com Windows 7, ele poderá ser restaurado em um computador com Windows 8 ou superior.</span><span class="sxs-lookup"><span data-stu-id="aab04-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="aab04-195">No entanto, o contrário Olá não verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="aab04-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="aab04-196">Olá abrir **Backup do Microsoft Azure** encaixe em Olá *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="aab04-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="aab04-197">Certifique-se de que Olá *máquina destino* e hello *máquina de origem* são toohello registrado mesmo Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="aab04-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="aab04-198">Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="aab04-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="aab04-200">Selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="aab04-200">Select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="aab04-202">Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*.</span><span class="sxs-lookup"><span data-stu-id="aab04-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="aab04-203">Se o arquivo de credencial de cofre Olá é inválido (ou expirados) baixar um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab04-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="aab04-204">Depois que o arquivo de credencial de cofre Olá for fornecido, o Cofre de backup Olá no arquivo de credencial de cofre Olá é exibido.</span><span class="sxs-lookup"><span data-stu-id="aab04-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="aab04-205">Selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas.</span><span class="sxs-lookup"><span data-stu-id="aab04-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="aab04-207">Selecione qualquer Olá **pesquisar arquivos** ou **procurar arquivos** opção.</span><span class="sxs-lookup"><span data-stu-id="aab04-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="aab04-208">Para finalidade de saudação desta seção, usaremos Olá **pesquisar arquivos** opção.</span><span class="sxs-lookup"><span data-stu-id="aab04-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="aab04-210">Selecione Olá volume e data na próxima tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="aab04-211">Pesquisa de nome de pasta/arquivo hello deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="aab04-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="aab04-213">Selecione Olá local onde os arquivos de saudação necessário toobe restaurado.</span><span class="sxs-lookup"><span data-stu-id="aab04-213">Select hello location where hello files need toobe restored.</span></span>

    ![Restaurar local](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="aab04-215">Fornecer Olá senha de criptografia que foi fornecida durante a *máquina de origem* registro muito*cofre exemplo*.</span><span class="sxs-lookup"><span data-stu-id="aab04-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="aab04-217">Depois de entrada hello for fornecida, clique em **recuperar**, que gatilhos Olá restauração de saudação backup arquivos toohello destino fornecido.</span><span class="sxs-lookup"><span data-stu-id="aab04-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="aab04-218">Usar restauração instantânea toorestore dados tooan alternativa máquina</span><span class="sxs-lookup"><span data-stu-id="aab04-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="aab04-219">Se o servidor inteiro for perdido, você ainda poderá recuperar dados de máquina do Azure Backup tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="aab04-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="aab04-220">Olá etapas a seguir ilustra o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="aab04-221">terminologia de saudação usada essas etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="aab04-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="aab04-222">*Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="aab04-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="aab04-223">*Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="aab04-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="aab04-224">*Cofre de exemplo* – Olá Olá de toowhich de Cofre de serviços de recuperação *máquina de origem* e *máquina destino* são registrados.</span><span class="sxs-lookup"><span data-stu-id="aab04-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="aab04-225">Os backups não podem ser restaurado tooa máquina de destino executando uma versão anterior do sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="aab04-226">Por exemplo, um backup feito em um computador com Windows 7 pode ser restaurado em um computador com Windows 8 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="aab04-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="aab04-227">Um backup feito em um computador Windows 8 não pode ser o computador restaurado tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="aab04-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="aab04-228">Olá abrir **Backup do Microsoft Azure** encaixe em Olá *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="aab04-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="aab04-229">Certifique-se de saudação *máquina destino* e hello *máquina de origem* são registrado toohello dos serviços de recuperação mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="aab04-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="aab04-230">Clique em **recuperar dados** tooopen Olá **Assistente para recuperar dados**.</span><span class="sxs-lookup"><span data-stu-id="aab04-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="aab04-232">Em Olá **Introdução** painel, selecione **outro servidor**</span><span class="sxs-lookup"><span data-stu-id="aab04-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="aab04-234">Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="aab04-235">Se o arquivo de credencial de cofre Olá é inválido (ou expirado), baixe um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab04-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="aab04-236">Depois que você forneça uma credencial de cofre válida, Olá nome da saudação que Cofre de Backup correspondente é exibida.</span><span class="sxs-lookup"><span data-stu-id="aab04-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="aab04-237">Em Olá **Selecionar servidor de Backup** painel, selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas e forneça a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab04-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="aab04-238">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-238">Then click **Next**.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="aab04-240">Em Olá **Selecionar modo de recuperação** painel, selecione **arquivos e pastas individuais** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="aab04-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="aab04-242">Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="aab04-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="aab04-243">No calendário hello, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="aab04-244">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="aab04-245">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aab04-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="aab04-246">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="aab04-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="aab04-248">Clique em **montar** toolocally montagem Olá ponto de recuperação como um volume de recuperação em seu *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="aab04-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="aab04-249">Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="aab04-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="aab04-251">No Windows Explorer, copie arquivos hello e/ou pastas do volume de recuperação hello e colá-los tooyour *máquina destino* local.</span><span class="sxs-lookup"><span data-stu-id="aab04-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="aab04-252">Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="aab04-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="aab04-254">Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**.</span><span class="sxs-lookup"><span data-stu-id="aab04-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="aab04-255">Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.</span><span class="sxs-lookup"><span data-stu-id="aab04-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="aab04-257">Se você não clicar desmontagem, Olá Volume de recuperação permanecerá montada por seis horas de tempo de saudação quando ele foi montado.</span><span class="sxs-lookup"><span data-stu-id="aab04-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="aab04-258">Nenhuma operação de backup será executado enquanto Olá volume está montado.</span><span class="sxs-lookup"><span data-stu-id="aab04-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="aab04-259">Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.</span><span class="sxs-lookup"><span data-stu-id="aab04-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="aab04-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aab04-260">Next steps</span></span>
* [<span data-ttu-id="aab04-261">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="aab04-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="aab04-262">Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="aab04-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="aab04-263">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="aab04-263">Learn more</span></span>
* [<span data-ttu-id="aab04-264">Visão geral do backup do Azure</span><span class="sxs-lookup"><span data-stu-id="aab04-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="aab04-265">Fazer backup de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="aab04-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="aab04-266">Fazer backup de cargas de trabalho Microsoft</span><span class="sxs-lookup"><span data-stu-id="aab04-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
