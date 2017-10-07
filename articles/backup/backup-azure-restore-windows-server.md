---
title: aaaRestore dados no computador do Windows ou do Azure tooa Windows Server | Microsoft Docs
description: Saiba como toorestore dados armazenados no computador do Windows ou do Azure tooa do Windows Server.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="01c28-103">Restaurar arquivos tooa Windows server ou o computador de cliente do Windows usando o modelo de implantação do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="01c28-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01c28-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="01c28-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="01c28-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="01c28-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="01c28-106">Este artigo explica como toorestore dados de um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="01c28-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="01c28-107">toorestore dados, você usa o Assistente de recuperar dados de saudação no agente do Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="01c28-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="01c28-108">Ao restaurar dados, é possível:</span><span class="sxs-lookup"><span data-stu-id="01c28-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="01c28-109">Restaurar dados toohello mesmo computador do qual os backups Olá foram realizados.</span><span class="sxs-lookup"><span data-stu-id="01c28-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="01c28-110">Restaure a máquina alternativo de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="01c28-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="01c28-111">Em janeiro de 2017, a Microsoft lançou um agente de MARS toohello de atualização de visualização.</span><span class="sxs-lookup"><span data-stu-id="01c28-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="01c28-112">Juntamente com correções de bug, essa atualização permite restauração instantânea, que permite que você toomount um instantâneo de ponto de recuperação gravável como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="01c28-113">Em seguida, você pode explorar Olá recuperação volume e copiar arquivos tooa computador local restaurando assim seletivamente arquivos.</span><span class="sxs-lookup"><span data-stu-id="01c28-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="01c28-114">Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) é necessária se você quiser toouse restauração instantânea toorestore dados.</span><span class="sxs-lookup"><span data-stu-id="01c28-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="01c28-115">Também os dados de backup Olá devem ser protegidos no cofres em localidades listados no artigo de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="01c28-116">Consulte Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) para a lista mais recente Olá das localidades que oferecem suporte à restauração instantânea.</span><span class="sxs-lookup"><span data-stu-id="01c28-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="01c28-117">No momento, a Restauração Instantânea **não** está disponível em todas as localidades.</span><span class="sxs-lookup"><span data-stu-id="01c28-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="01c28-118">Restauração instantânea está disponível para uso em cofres de serviços de recuperação no hello portal do Azure e cofres de Backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="01c28-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="01c28-119">Se você quiser toouse restauração instantânea, baixe a atualização de MARS Olá e siga os procedimentos de saudação que mencionem restauração instantânea.</span><span class="sxs-lookup"><span data-stu-id="01c28-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="01c28-120">Use a restauração instantânea toohello de dados toorecover mesmo computador</span><span class="sxs-lookup"><span data-stu-id="01c28-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="01c28-121">Se você excluiu acidentalmente um arquivo e quiser toorestore-toohello mesma máquina (do qual Olá é feito backup), Olá seguindo as etapas ajudará você a recuperar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="01c28-122">Olá abrir **Backup do Microsoft Azure** encaixe em.</span><span class="sxs-lookup"><span data-stu-id="01c28-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="01c28-123">Se você não souber onde o snap-in de saudação foi instalado, pesquisar Olá computador ou servidor para **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="01c28-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="01c28-124">aplicativo de área de trabalho de saudação deve aparecer nos resultados da pesquisa Olá.</span><span class="sxs-lookup"><span data-stu-id="01c28-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="01c28-125">Clique em **recuperar dados** toostart Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="01c28-127">Em Olá **Introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="01c28-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha esse servidor opção toorestore Olá dados toohello mesmo computador](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="01c28-129">Em Olá **Selecionar modo de recuperação** painel, escolha **arquivos e pastas individuais** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="01c28-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="01c28-131">Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="01c28-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="01c28-132">No calendário hello, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="01c28-133">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="01c28-134">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="01c28-135">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="01c28-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="01c28-137">Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **montar**.</span><span class="sxs-lookup"><span data-stu-id="01c28-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="01c28-138">O Backup do Azure monta o ponto de recuperação locais hello e utiliza como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="01c28-139">Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="01c28-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="01c28-141">No Windows Explorer, Olá copiar os arquivos e/ou pastas você deseja toorestore e colá-los tooany local toohello local servidor ou computador.</span><span class="sxs-lookup"><span data-stu-id="01c28-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="01c28-142">Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="01c28-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copie e cole os arquivos e pastas do local do volume montado toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="01c28-144">Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**.</span><span class="sxs-lookup"><span data-stu-id="01c28-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="01c28-145">Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.</span><span class="sxs-lookup"><span data-stu-id="01c28-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Desmontar o volume de saudação e confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="01c28-147">Se você não clicar desmontagem, Olá recuperação Volume permanecerá montada por 6 horas de tempo de saudação quando ele foi montado.</span><span class="sxs-lookup"><span data-stu-id="01c28-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="01c28-148">No entanto, o tempo de montagem de saudação é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento.</span><span class="sxs-lookup"><span data-stu-id="01c28-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="01c28-149">Nenhuma operação de backup será executado enquanto Olá volume está montado.</span><span class="sxs-lookup"><span data-stu-id="01c28-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="01c28-150">Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.</span><span class="sxs-lookup"><span data-stu-id="01c28-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="01c28-151">Usar restauração instantânea toorestore dados tooan alternativa máquina</span><span class="sxs-lookup"><span data-stu-id="01c28-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="01c28-152">Se o servidor inteiro for perdido, você ainda poderá recuperar dados de máquina do Azure Backup tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="01c28-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="01c28-153">Olá etapas a seguir ilustra o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="01c28-154">terminologia de saudação usada essas etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="01c28-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="01c28-155">*Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="01c28-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="01c28-156">*Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="01c28-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="01c28-157">*Cofre de exemplo* – Olá Olá de toowhich de Cofre de serviços de recuperação *máquina de origem* e *máquina destino* são registrados.</span><span class="sxs-lookup"><span data-stu-id="01c28-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="01c28-158">Os backups não podem ser restaurado tooa máquina de destino executando uma versão anterior do sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="01c28-159">Por exemplo, um backup feito em um computador com Windows 7 pode ser restaurado em um computador com Windows 8 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="01c28-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="01c28-160">Um backup feito em um computador Windows 8 não pode ser o computador restaurado tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="01c28-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="01c28-161">Olá abrir **Backup do Microsoft Azure** encaixe em Olá *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="01c28-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="01c28-162">Certifique-se de saudação *máquina destino* e hello *máquina de origem* são registrado toohello dos serviços de recuperação mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="01c28-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="01c28-163">Clique em **recuperar dados** tooopen Olá **Assistente para recuperar dados**.</span><span class="sxs-lookup"><span data-stu-id="01c28-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="01c28-165">Em Olá **Introdução** painel, selecione **outro servidor**</span><span class="sxs-lookup"><span data-stu-id="01c28-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="01c28-167">Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="01c28-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="01c28-168">Se o arquivo de credencial de cofre Olá é inválido (ou expirado), baixe um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01c28-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="01c28-169">Depois que você forneça uma credencial de cofre válida, Olá nome da saudação que Cofre de Backup correspondente é exibida.</span><span class="sxs-lookup"><span data-stu-id="01c28-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="01c28-170">Em Olá **Selecionar servidor de Backup** painel, selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas e forneça a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="01c28-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="01c28-171">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="01c28-171">Then click **Next**.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="01c28-173">Em Olá **Selecionar modo de recuperação** painel, selecione **arquivos e pastas individuais** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="01c28-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="01c28-175">Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="01c28-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="01c28-176">No calendário hello, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="01c28-177">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="01c28-178">Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="01c28-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="01c28-179">Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="01c28-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="01c28-181">Clique em **montar** toolocally montagem Olá ponto de recuperação como um volume de recuperação em seu *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="01c28-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="01c28-182">Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.</span><span class="sxs-lookup"><span data-stu-id="01c28-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="01c28-184">No Windows Explorer, copie arquivos hello e/ou pastas do volume de recuperação hello e colá-los tooyour *máquina destino* local.</span><span class="sxs-lookup"><span data-stu-id="01c28-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="01c28-185">Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="01c28-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="01c28-187">Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**.</span><span class="sxs-lookup"><span data-stu-id="01c28-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="01c28-188">Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.</span><span class="sxs-lookup"><span data-stu-id="01c28-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="01c28-190">Se você não clicar desmontagem, Olá recuperação Volume permanecerá montada por 6 horas de tempo de saudação quando ele foi montado.</span><span class="sxs-lookup"><span data-stu-id="01c28-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="01c28-191">No entanto, o tempo de montagem de saudação é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento.</span><span class="sxs-lookup"><span data-stu-id="01c28-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="01c28-192">Nenhuma operação de backup será executado enquanto Olá volume está montado.</span><span class="sxs-lookup"><span data-stu-id="01c28-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="01c28-193">Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.</span><span class="sxs-lookup"><span data-stu-id="01c28-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="01c28-194">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="01c28-194">Troubleshooting</span></span>
<span data-ttu-id="01c28-195">Se Backup do Azure com êxito não montar o volume de recuperação Olá até mesmo após vários minutos clicando em **montar** ou falhar toomount Olá volume de recuperação com um ou mais erros, siga as etapas de saudação abaixo toobegin recuperando normalmente.</span><span class="sxs-lookup"><span data-stu-id="01c28-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="01c28-196">Cancele o processo de montagem em andamento de saudação caso esteve em execução por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="01c28-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="01c28-197">Certifique-se de que você está na versão mais recente de saudação do agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01c28-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="01c28-198">toofind informações de versão de saudação do agente de Backup do Azure, clique em **sobre o Microsoft Azure Recovery Services Agent** em Olá **ações** painel do Microsoft Azure Backup console e certifique-se de que Olá ** Versão** número é igual tooor superior à versão Olá mencionado na [neste artigo](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="01c28-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="01c28-199">Você pode baixar a versão mais recente de saudação do [aqui](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="01c28-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="01c28-200">Vá muito**Gerenciador de dispositivos** -> **controladores de armazenamento** e certifique-se de que você pode localizar **iniciador Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="01c28-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="01c28-201">Se você pode localizá-lo, vá diretamente toostep 7 abaixo.</span><span class="sxs-lookup"><span data-stu-id="01c28-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="01c28-202">Se você não puder localizar o serviço do iniciador Microsoft iSCSI conforme mencionado na etapa 3, verifique toosee se você pode encontrar uma entrada em **Gerenciador de dispositivos** -> **controladores de armazenamento** chamado ** Dispositivo desconhecido** com a ID de Hardware **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="01c28-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="01c28-203">Clique com o botão direito do mouse em **Dispositivo Desconhecido** e selecione **Atualizar Software de Driver**.</span><span class="sxs-lookup"><span data-stu-id="01c28-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="01c28-204">Atualizar o driver de hello, selecionando a opção de saudação muito **pesquisar automaticamente software de driver atualizado de**.</span><span class="sxs-lookup"><span data-stu-id="01c28-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="01c28-205">Conclusão da atualização Olá deve alterar **dispositivo desconhecido** muito**iniciador Microsoft iSCSI** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="01c28-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Criptografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="01c28-207">Vá muito**Gerenciador de tarefas** -> **serviços (Local)** -> **serviço iniciador Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="01c28-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Criptografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="01c28-209">Reinicie o serviço Olá Microsoft iSCSI Initiator clicando-se no serviço hello, clicando em **parar** e mais clique direito novamente e clicando em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="01c28-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="01c28-210">Repita a recuperação usando a Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="01c28-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="01c28-211">Se recuperação Olá ainda falhar, reinicialize o servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="01c28-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="01c28-212">Se uma reinicialização não é desejável ou recuperação Olá ainda falha mesmo após a reinicialização do servidor de saudação, tente recuperar de uma máquina alternativo e entre em contato com suporte do Azure indo muito[Portal do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e enviar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="01c28-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01c28-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01c28-213">Next steps</span></span>
* <span data-ttu-id="01c28-214">Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="01c28-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
