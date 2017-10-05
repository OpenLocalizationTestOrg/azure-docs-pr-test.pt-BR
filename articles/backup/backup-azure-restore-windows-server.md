---
title: Restaurar dados no Azure para um computador Windows ou Windows Server | Microsoft Docs
description: Saiba como restaurar os dados armazenados no Azure para um computador Windows ou Windows Server.
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
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="9fd39-103">Restaurar arquivos em um computador de cliente do Windows ou Windows Server usando o modelo de implantação do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="9fd39-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fd39-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9fd39-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="9fd39-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="9fd39-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="9fd39-106">Este artigo explica como restaurar dados de um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="9fd39-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="9fd39-107">Para restaurar dados, você pode usar o assistente recuperar dados do agente do Serviços de Recuperação do Microsoft Azure (MARS).</span><span class="sxs-lookup"><span data-stu-id="9fd39-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="9fd39-108">Ao restaurar dados, é possível:</span><span class="sxs-lookup"><span data-stu-id="9fd39-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="9fd39-109">Restaurar dados para o mesmo computador do qual os backups foram realizados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="9fd39-110">Restaurar dados para um computador alternativo.</span><span class="sxs-lookup"><span data-stu-id="9fd39-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="9fd39-111">Em janeiro de 2017, a Microsoft lançou uma atualização de Versão Prévia para o agente do MARS.</span><span class="sxs-lookup"><span data-stu-id="9fd39-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="9fd39-112">Juntamente com as correções de bug, essa atualização permite Restauração Instantânea, que permite que você monte um instantâneo de ponto de recuperação gravável como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="9fd39-113">Em seguida, é possível explorar os arquivos de volume de recuperação e de cópia em um computador local e, assim, restaurar arquivos de forma seletiva.</span><span class="sxs-lookup"><span data-stu-id="9fd39-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="9fd39-114">A [atualização do Backup do Azure de janeiro de 2017](https://support.microsoft.com/en-us/help/3216528?preview) será necessária se você desejar usar a Restauração Instantânea para restaurar dados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="9fd39-115">Além disso, os dados de backup devem ser protegidos em cofres nas localidades listadas no artigo de suporte.</span><span class="sxs-lookup"><span data-stu-id="9fd39-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="9fd39-116">Consulte a [atualização do Backup do Azure de janeiro de 2017](https://support.microsoft.com/en-us/help/3216528?preview) para obter a lista mais recente de localidades que oferecem suporte à Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="9fd39-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="9fd39-117">No momento, a Restauração Instantânea **não** está disponível em todas as localidades.</span><span class="sxs-lookup"><span data-stu-id="9fd39-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="9fd39-118">A Restauração Instantânea está disponível para uso em cofres dos Serviços de Recuperação no portal do Azure e em cofres de Backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9fd39-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="9fd39-119">Se desejar usar a Restauração Instantânea, baixe a atualização do MARS e siga os procedimentos que mencionam a Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="9fd39-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="9fd39-120">Use a Restauração Instantânea para recuperar dados no mesmo computador</span><span class="sxs-lookup"><span data-stu-id="9fd39-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="9fd39-121">Se você excluiu acidentalmente um arquivo e deseja restaurá-lo para o mesmo computador (do qual o backup foi feito), as etapas a seguir o ajudarão a recuperar os dados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="9fd39-122">Abra o snap-in do **Backup do Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="9fd39-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="9fd39-123">Se você não souber onde o snap-in foi instalado, pesquise **Backup do Microsoft Azure** no computador ou servidor.</span><span class="sxs-lookup"><span data-stu-id="9fd39-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="9fd39-124">O aplicativo da área de trabalho deve aparecer nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9fd39-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="9fd39-125">Clique em **Recuperar Dados** para iniciar o assistente.</span><span class="sxs-lookup"><span data-stu-id="9fd39-125">Click **Recover Data** to start the wizard.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="9fd39-127">No painel **Introdução**, para restaurar os dados para o mesmo computador ou servidor, selecione **Este servidor (`<server name>`)** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha a opção Este servidor para restaurar os dados para o mesmo computador](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="9fd39-129">No painel **Selecionar Modo de Recuperação**, escolha **Pastas e arquivos individuais** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Procurar arquivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="9fd39-131">No painel **Selecionar Volume e Data**, selecione o volume que contém os arquivos e/ou pastas que deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="9fd39-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="9fd39-132">No calendário, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="9fd39-133">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="9fd39-134">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="9fd39-135">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e data](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="9fd39-137">Depois de ter escolhido o ponto de recuperação a ser restaurado, clique em **Montar**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="9fd39-138">O Backup do Azure monta o ponto de recuperação local e o usa como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="9fd39-139">No painel **Procurar e Recuperar Arquivos**, clique em **Procurar** para abrir o Windows Explorer e localize os arquivos e pastas desejados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="9fd39-141">No Windows Explorer, copie os arquivos e/ou pastas que deseja restaurar e cole-os em qualquer localização local no servidor ou computador.</span><span class="sxs-lookup"><span data-stu-id="9fd39-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="9fd39-142">Você pode abrir ou transmitir os arquivos diretamente do volume de recuperação e verificar se as versões corretas são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="9fd39-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiar e colar arquivos e pastas do volume montado na localização local](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="9fd39-144">Quando você terminar de restaurar os arquivos e/ou pastas, no painel **Procurar e Recuperar Arquivos**, clique em **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="9fd39-145">Clique em **Sim** para confirmar que deseja desmontar o volume.</span><span class="sxs-lookup"><span data-stu-id="9fd39-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Desmontar o volume e confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="9fd39-147">Se você não clicar em Desmontar, o Volume de Recuperação permanecerá montado por seis horas a partir da hora em que foi montado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="9fd39-148">No entanto, o tempo de montagem é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento.</span><span class="sxs-lookup"><span data-stu-id="9fd39-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="9fd39-149">Não será executada nenhuma operação de backup enquanto o volume estiver montado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="9fd39-150">Qualquer operação de backup agendada para execução durante o tempo em que o volume estiver montado será executada após o volume de recuperação ser desmontado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="9fd39-151">Usar a Restauração Instantânea para restaurar dados em um computador alternativo</span><span class="sxs-lookup"><span data-stu-id="9fd39-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="9fd39-152">Se o servidor inteiro for perdido, você ainda pode recuperar dados do backup do Azure para um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="9fd39-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="9fd39-153">As etapas a seguir ilustram o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9fd39-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="9fd39-154">A terminologia usada nessas etapas inclui:</span><span class="sxs-lookup"><span data-stu-id="9fd39-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="9fd39-155">*Máquina de origem* : a máquina original da qual o backup foi feito e que está indisponível no momento.</span><span class="sxs-lookup"><span data-stu-id="9fd39-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="9fd39-156">*Computador de destino* – O computador para o qual os dados estão sendo recuperados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="9fd39-157">*Cofre de exemplo* – o cofre Serviços de Recuperação no qual a *Máquina de origem* e a *Máquina de destino* estão registradas.</span><span class="sxs-lookup"><span data-stu-id="9fd39-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="9fd39-158">Os backups não podem ser restaurados em um computador de destino executando uma versão anterior do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="9fd39-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="9fd39-159">Por exemplo, um backup feito em um computador com Windows 7 pode ser restaurado em um computador com Windows 8 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="9fd39-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="9fd39-160">Um backup feito em um computador com Windows 8 não pode ser restaurado em um computador com Windows 7.</span><span class="sxs-lookup"><span data-stu-id="9fd39-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="9fd39-161">Abra o snap-in do **Backup do Microsoft Azure** no *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="9fd39-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="9fd39-162">Verifique se o *Computador de destino* e o *Computador de origem* estão registrados no mesmo cofre de Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="9fd39-163">Clique em **Recuperar Dados** para abrir o **Assistente de Recuperação de Dados**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="9fd39-165">No painel **Introdução**, selecione **Outro servidor**</span><span class="sxs-lookup"><span data-stu-id="9fd39-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="9fd39-167">Forneça o arquivo de credencial de cofre que corresponde ao *Cofre de exemplo* e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="9fd39-168">Se o arquivo de credencial de cofre for inválido (ou tiver expirado), baixe um novo arquivo de credencial de cofre do *Cofre de exemplo* no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd39-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="9fd39-169">Depois de fornecer uma credencial de cofre válida, o nome do Cofre de Backup correspondente aparecerá.</span><span class="sxs-lookup"><span data-stu-id="9fd39-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="9fd39-170">No painel **Selecionar Servidor de Backup**, selecione o *Computador de origem* na lista de computadores exibidos e forneça a senha.</span><span class="sxs-lookup"><span data-stu-id="9fd39-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="9fd39-171">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-171">Then click **Next**.</span></span>

    ![Lista de computadores](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="9fd39-173">No painel **Selecionar Modo de Recuperação**, selecione **Pastas e arquivos individuais** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Pesquisar](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="9fd39-175">No painel **Selecionar Volume e Data**, selecione o volume que contém os arquivos e/ou pastas que deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="9fd39-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="9fd39-176">No calendário, selecione um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="9fd39-177">Você pode restaurar de qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="9fd39-178">As datas em **negrito** indicam a disponibilidade de pelo menos um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9fd39-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="9fd39-179">Depois de selecionar uma data, se houver vários pontos de recuperação disponíveis, escolha o ponto de recuperação específico no menu suspenso **Hora**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Pesquisar itens](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="9fd39-181">Clique em **Montar** para montar localmente o ponto de recuperação como um volume de recuperação em seu *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="9fd39-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="9fd39-182">No painel **Procurar e Recuperar Arquivos**, clique em **Procurar** para abrir o Windows Explorer e localize os arquivos e pastas desejados.</span><span class="sxs-lookup"><span data-stu-id="9fd39-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="9fd39-184">No Windows Explorer, copie os arquivos e/ou pastas do volume de recuperação e cole-os na localização de seu *Computador de destino*.</span><span class="sxs-lookup"><span data-stu-id="9fd39-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="9fd39-185">Você pode abrir ou transmitir os arquivos diretamente do volume de recuperação e verificar se as versões corretas são recuperadas.</span><span class="sxs-lookup"><span data-stu-id="9fd39-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="9fd39-187">Quando você terminar de restaurar os arquivos e/ou pastas, no painel **Procurar e Recuperar Arquivos**, clique em **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="9fd39-188">Clique em **Sim** para confirmar que deseja desmontar o volume.</span><span class="sxs-lookup"><span data-stu-id="9fd39-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="9fd39-190">Se você não clicar em Desmontar, o Volume de Recuperação permanecerá montado por seis horas a partir da hora em que foi montado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="9fd39-191">No entanto, o tempo de montagem é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento.</span><span class="sxs-lookup"><span data-stu-id="9fd39-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="9fd39-192">Não será executada nenhuma operação de backup enquanto o volume estiver montado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="9fd39-193">Qualquer operação de backup agendada para execução durante o tempo em que o volume estiver montado será executada após o volume de recuperação ser desmontado.</span><span class="sxs-lookup"><span data-stu-id="9fd39-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="9fd39-194">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9fd39-194">Troubleshooting</span></span>
<span data-ttu-id="9fd39-195">Se o Backup do Azure não tiver montado com êxito o volume de recuperação mesmo após os diversos minutos de clicar em **Montar** ou falha ao montar o volume de recuperação com um ou mais erros, siga as etapas abaixo para iniciar a recuperação normalmente.</span><span class="sxs-lookup"><span data-stu-id="9fd39-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="9fd39-196">Cancele o processo de montagem em andamento caso ele esteja sendo executado por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="9fd39-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="9fd39-197">Verifique se você está na versão mais recente do agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd39-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="9fd39-198">Para obter as informações de versão do agente de Backup do Azure, clique em **Sobre o Agente dos Serviços de Recuperação do Microsoft Azure** no painel **Ações** do console de Backup do Microsoft Azure e verifique se o número de **Versão** é igual a ou maior do que a versão mencionada [neste artigo](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="9fd39-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="9fd39-199">Você pode baixar a versão mais recente [aqui](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="9fd39-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="9fd39-200">Vá para **Gerenciador de Dispositivos** -> **Controladores de Armazenamento** e verifique se você pode localizar o **Iniciador do Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="9fd39-201">Se você puder localizá-lo, vá diretamente para a etapa 7 abaixo.</span><span class="sxs-lookup"><span data-stu-id="9fd39-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="9fd39-202">Se você não puder localizar o serviço Iniciador do Microsoft iSCSI conforme mencionado na etapa 3, verifique se você pode encontrar uma entrada em **Gerenciador de Dispositivos** -> **Controladores de Armazenamento** chamada **Dispositivo Desconhecido** com a ID de Hardware **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="9fd39-203">Clique com o botão direito do mouse em **Dispositivo Desconhecido** e selecione **Atualizar Software de Driver**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="9fd39-204">Atualize o driver ao selecionar a opção para **Pesquisar automaticamente software de driver atualizado**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="9fd39-205">A conclusão da atualização deve alterar o **Dispositivo Desconhecido** para o **Iniciador do Microsoft iSCSI** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9fd39-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Criptografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="9fd39-207">Vá para **Gerenciador de Tarefas** -> **Serviços (Local)** -> **Serviço Iniciador do Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Criptografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="9fd39-209">Reinicie o serviço Iniciador do Microsoft iSCSI ao clicar com o botão direito do mouse no serviço, clicar em **Parar** e continue clicando com o botão direito do mouse e clicando em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9fd39-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="9fd39-210">Repita a recuperação usando a Restauração Instantânea.</span><span class="sxs-lookup"><span data-stu-id="9fd39-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="9fd39-211">Se a recuperação ainda falhar, reinicialize o servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="9fd39-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="9fd39-212">Se uma reinicialização não for desejável ou se a recuperação ainda falhar mesmo após a reinicialização do servidor, tente recuperar de um Computador Alternativo e contate o Suporte do Azure no [Portal do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e envie uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="9fd39-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fd39-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fd39-213">Next steps</span></span>
* <span data-ttu-id="9fd39-214">Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9fd39-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
