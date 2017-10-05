---
title: "Gerenciar backups de máquina virtual implantados pelo Resource Manager | Microsoft Docs"
description: "Saiba como gerenciar e monitorar os backups da máquina virtual implantados pelo Gerenciador de Recursos"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="b8949-103">Gerenciar backups de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="b8949-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8949-104">Gerenciar backups da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="b8949-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="b8949-105">Gerenciar backups da VM Clássica</span><span class="sxs-lookup"><span data-stu-id="b8949-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="b8949-106">Este artigo fornece orientações sobre como gerenciar backups de VM e explica as informações sobre alertas de backup disponíveis no painel do portal.</span><span class="sxs-lookup"><span data-stu-id="b8949-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="b8949-107">As diretrizes neste artigo se aplicam ao uso das VMs com cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="b8949-108">Este artigo não aborda a criação das máquinas virtuais, nem explica como protegê-las.</span><span class="sxs-lookup"><span data-stu-id="b8949-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="b8949-109">Para ter instruções elementares sobre como proteger as VMs implantadas pelo Azure Resource Manager no Azure com um cofre dos Serviços de Recuperação, consulte [Primeiro examinar: fazer backup das VMs em um cofre dos Serviços de Recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b8949-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="b8949-110">Gerenciar cofres e máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="b8949-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="b8949-111">No portal do Azure, o painel do cofre dos Serviços de Recuperação fornece acesso a informações sobre o cofre, inclusive:</span><span class="sxs-lookup"><span data-stu-id="b8949-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="b8949-112">o instantâneo de backup mais recente, que também é o ponto de restauração mais recente <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="b8949-113">política de backup <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-113">the backup policy <br\></span></span>
* <span data-ttu-id="b8949-114">tamanho total de todos os instantâneos do backup <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="b8949-115">número de máquinas virtuais que são protegidas com o cofre <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="b8949-116">Muitas tarefas de gerenciamento com um backup da máquina virtual começam abrindo o cofre no painel de controle.</span><span class="sxs-lookup"><span data-stu-id="b8949-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="b8949-117">No entanto, como os cofres podem ser usados para proteger vários itens (ou várias VMs), para exibir detalhes sobre uma determinada VM, abra o painel do item do cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="b8949-118">O procedimento a seguir mostra como abrir o *painel do cofre*, em seguida, ir para o *painel do item do cofre*.</span><span class="sxs-lookup"><span data-stu-id="b8949-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="b8949-119">Há "dicas" em ambos os procedimentos que mostram como adicionar o cofre e o item do cofre ao painel do Azure usando o Pin no comando do painel.</span><span class="sxs-lookup"><span data-stu-id="b8949-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="b8949-120">Fixar no painel é uma maneira de criar um atalho para o cofre ou o item.</span><span class="sxs-lookup"><span data-stu-id="b8949-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="b8949-121">Você também pode executar os comandos comuns a partir do atalho.</span><span class="sxs-lookup"><span data-stu-id="b8949-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="b8949-122">Se você tiver vários painéis e folhas abertos, use o controle azul escuro na parte inferior da janela para deslizar o painel do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8949-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Exibição completa com controle deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="b8949-124">Abra um cofre dos Serviços de Recuperação no painel:</span><span class="sxs-lookup"><span data-stu-id="b8949-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="b8949-125">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b8949-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b8949-126">No menu Hub, clique em **Procurar** e, na lista de recursos, digite **Serviços de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="b8949-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="b8949-127">Quando você começa a digitar, a lista é filtrada com base em sua entrada.</span><span class="sxs-lookup"><span data-stu-id="b8949-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="b8949-128">Clique em **Cofre de Serviços de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="b8949-128">Click **Recovery Services vault**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="b8949-130">A lista de cofres de Serviços de Recuperação será exibida.</span><span class="sxs-lookup"><span data-stu-id="b8949-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="b8949-131">Listar cofres de Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="b8949-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="b8949-132">Se você fixar um cofre no Painel do Azure, esse cofre ficará imediatamente acessível quando você abrir o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8949-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="b8949-133">Para fixar um cofre no painel, na lista de cofres, clique com o botão direito no cofre e selecione **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="b8949-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="b8949-134">Na lista de cofres, escolha o cofre para abrir seu painel.</span><span class="sxs-lookup"><span data-stu-id="b8949-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="b8949-135">Quando você seleciona o cofre, o painel do cofre e a folha **Configurações** são abertos.</span><span class="sxs-lookup"><span data-stu-id="b8949-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="b8949-136">Na imagem a seguir, o painel **Cofre Contoso** é destacado.</span><span class="sxs-lookup"><span data-stu-id="b8949-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Abrir o painel do cofre e a folha de Configurações](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="b8949-138">Abra o painel do item do cofre</span><span class="sxs-lookup"><span data-stu-id="b8949-138">Open a vault item dashboard</span></span>
<span data-ttu-id="b8949-139">No procedimento anterior, você abriu o painel do cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="b8949-140">Para abrir o painel do item do cofre:</span><span class="sxs-lookup"><span data-stu-id="b8949-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="b8949-141">No painel do cofre, no bloco **Itens de Backup**, clique em **Máquinas Virtuais do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b8949-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Bloco Abrir itens de backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="b8949-143">A folha **Itens de Backup** lista o último trabalho de backup de cada item.</span><span class="sxs-lookup"><span data-stu-id="b8949-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="b8949-144">Neste exemplo, há uma máquina virtual, demovm-markgal, protegida por esse cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="b8949-146">Para facilitar o acesso, você pode fixar um item do cofre no Painel do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8949-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="b8949-147">Para fixar um item do cofre, na lista de itens do cofre, clique com o botão direito no item e selecione **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="b8949-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="b8949-148">Na folha **Itens de Backup** , clique no item para abrir o painel do item do cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="b8949-150">O painel do item do cofre e sua folha **Configurações** são abertos.</span><span class="sxs-lookup"><span data-stu-id="b8949-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Painel dos itens de backup com a folha Configurações](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="b8949-152">No painel de itens do cofre, você pode executar muitas tarefas de gerenciamento principais, como:</span><span class="sxs-lookup"><span data-stu-id="b8949-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="b8949-153">alterar as políticas ou criar uma nova política de backup <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="b8949-154">exibir pontos de restauração e ver seu estado de consistência <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="b8949-155">Backup sob demanda de uma máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="b8949-156">interromper a proteção das máquinas virtuais <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="b8949-157">retomar a proteção de uma máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="b8949-158">excluir os dados do backup (ou ponto de recuperação) <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="b8949-159">[restaurar discos de backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="b8949-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="b8949-160">Para os procedimentos a seguir, o ponto de partida é o painel de itens do cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="b8949-161">Gerenciar políticas de backup</span><span class="sxs-lookup"><span data-stu-id="b8949-161">Manage backup policies</span></span>
1. <span data-ttu-id="b8949-162">No [painel de itens do cofre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Todas as Configurações** para abrir a folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b8949-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Folha Política de backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="b8949-164">Na folha **Configurações**, clique em **Política de backup** para abrir essa folha.</span><span class="sxs-lookup"><span data-stu-id="b8949-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="b8949-165">Na folha, são mostrados os detalhes do intervalo de retenção e da frequência dos backups.</span><span class="sxs-lookup"><span data-stu-id="b8949-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Folha Política de backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="b8949-167">No menu **Escolher política de backup** :</span><span class="sxs-lookup"><span data-stu-id="b8949-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="b8949-168">Para alterar as políticas, selecione uma política diferente e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b8949-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="b8949-169">A nova política será aplicada imediatamente no cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="b8949-170"><br\></span><span class="sxs-lookup"><span data-stu-id="b8949-170"><br\></span></span>
   * <span data-ttu-id="b8949-171">Para criar uma política, selecione **Criar Nova**.</span><span class="sxs-lookup"><span data-stu-id="b8949-171">To create a policy, select **Create New**.</span></span>

     ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="b8949-173">Para obter instruções sobre como criar uma política de backup, consulte [Definindo uma política de backup](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="b8949-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="b8949-174">Ao gerenciar políticas de backup, certifique-se de seguir as [práticas recomendadas](backup-azure-vms-introduction.md#best-practices) para um desempenho de backup ideal</span><span class="sxs-lookup"><span data-stu-id="b8949-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="b8949-175">Backup sob demanda de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b8949-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="b8949-176">Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção.</span><span class="sxs-lookup"><span data-stu-id="b8949-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="b8949-177">Se o backup inicial está pendente, o backup sob demanda cria uma cópia completa da máquina virtual no cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="b8949-178">Se o backup inicial for concluído, um backup sob demanda enviará apenas as alterações do instantâneo anterior para o cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="b8949-179">Ou seja, os backups subsequentes serão sempre incrementais.</span><span class="sxs-lookup"><span data-stu-id="b8949-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="b8949-180">O intervalo de retenção para um backup sob demanda é o valor de retenção especificado para o ponto de backup Diário na política.</span><span class="sxs-lookup"><span data-stu-id="b8949-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="b8949-181">Se nenhum ponto de backup Diário for selecionado, o ponto de backup Semanal será usado.</span><span class="sxs-lookup"><span data-stu-id="b8949-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="b8949-182">Para inicializar um backup sob demanda de uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b8949-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="b8949-183">No [painel de itens do cofre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Fazer backup agora**.</span><span class="sxs-lookup"><span data-stu-id="b8949-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="b8949-185">O portal verificará você deseja iniciar um trabalho de backup sob demanda.</span><span class="sxs-lookup"><span data-stu-id="b8949-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="b8949-186">Clique em **Sim** para iniciar o trabalho de backup.</span><span class="sxs-lookup"><span data-stu-id="b8949-186">Click **Yes** to start the backup job.</span></span>

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="b8949-188">O trabalho de backup cria um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="b8949-189">O intervalo de retenção do ponto de recuperação é o mesmo especificado na política associada à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8949-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="b8949-190">Para acompanhar o progresso do trabalho, no painel do cofre, clique no bloco **Trabalhos de Backup** .</span><span class="sxs-lookup"><span data-stu-id="b8949-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="b8949-191">Interromper a proteção de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="b8949-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="b8949-192">Se você optar por interromper a proteção de uma máquina virtual, será perguntado se deseja manter os pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="b8949-193">Há duas maneiras de interromper a proteção das máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="b8949-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="b8949-194">parar todos os trabalhos de backup futuros e excluir todos os pontos de recuperação ou</span><span class="sxs-lookup"><span data-stu-id="b8949-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="b8949-195">parar todos os trabalhos de backup futuros, mas deixar os pontos de recuperação </span><span class="sxs-lookup"><span data-stu-id="b8949-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="b8949-196">Há um custo associado a deixar os pontos de recuperação no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b8949-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="b8949-197">No entanto, a vantagem de deixar os pontos de recuperação é que você pode restaurar a máquina virtual mais tarde, se desejado.</span><span class="sxs-lookup"><span data-stu-id="b8949-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="b8949-198">Para obter informações sobre o custo de deixar os pontos de recuperação, confira os [detalhes de preços](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="b8949-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="b8949-199">Se você optar por excluir todos os pontos de recuperação, não poderá restaurar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8949-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="b8949-200">Para interromper a proteção para uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b8949-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="b8949-201">No [painel de itens do cofre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Interromper backup**.</span><span class="sxs-lookup"><span data-stu-id="b8949-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Botão Interromper backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="b8949-203">A folha Interromper Backup é aberta.</span><span class="sxs-lookup"><span data-stu-id="b8949-203">The Stop Backup blade opens.</span></span>

    ![Folha Interromper backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="b8949-205">Na folha **Interromper Backup** , escolha se deseja manter ou excluir os dados do backup.</span><span class="sxs-lookup"><span data-stu-id="b8949-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="b8949-206">A caixa de informações fornece detalhes sobre sua escolha.</span><span class="sxs-lookup"><span data-stu-id="b8949-206">The information box provides details about your choice.</span></span>

    ![Parar a proteção](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="b8949-208">Se você escolheu manter os dados do backup, vá para a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="b8949-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="b8949-209">Se escolheu excluir os dados do backup, confirme se deseja interromper os trabalhos de backup e excluir os pontos de recuperação - digite o nome do item.</span><span class="sxs-lookup"><span data-stu-id="b8949-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="b8949-211">Se você não tiver certeza do nome do item, passe o mouse sobre o ponto de exclamação para exibir o nome.</span><span class="sxs-lookup"><span data-stu-id="b8949-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="b8949-212">Além disso, o nome do item está sob **Interromper Backup** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="b8949-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="b8949-213">Como opção, forneça um **Motivo** ou **Comentário**.</span><span class="sxs-lookup"><span data-stu-id="b8949-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="b8949-214">Para interromper o trabalho de backup para o item atual, clique em ![botão backup parar](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="b8949-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="b8949-215">Uma mensagem de notificação permite que você conheça os trabalhos de backup que foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="b8949-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="b8949-217">Retomar a proteção de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b8949-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="b8949-218">Se a opção **Reter Dados do Backup** foi selecionada quando a proteção da máquina virtual foi interrompida, será possível retomar a proteção.</span><span class="sxs-lookup"><span data-stu-id="b8949-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="b8949-219">Se a opção **Excluir Dados do Backup** foi escolhida, então, a proteção da máquina virtual não poderá retomar.</span><span class="sxs-lookup"><span data-stu-id="b8949-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="b8949-220">Retomar a proteção da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b8949-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="b8949-221">No [painel de itens do cofre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Retomar backup**.</span><span class="sxs-lookup"><span data-stu-id="b8949-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Retomar proteção](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="b8949-223">A folha Política de Backup será aberta.</span><span class="sxs-lookup"><span data-stu-id="b8949-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b8949-224">Ao proteger novamente a máquina virtual, você pode escolher uma política diferente da política com a qual a máquina virtual foi inicialmente protegida.</span><span class="sxs-lookup"><span data-stu-id="b8949-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="b8949-225">Siga as etapas em [Gerenciar políticas de backup](backup-azure-manage-vms.md#manage-backup-policies), para atribuir a política da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8949-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="b8949-226">Depois da política de backup ser aplicada à máquina virtual, você vê a mensagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8949-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![VM protegida com êxito](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="b8949-228">Excluir Dados do Backup</span><span class="sxs-lookup"><span data-stu-id="b8949-228">Delete Backup data</span></span>
<span data-ttu-id="b8949-229">Você pode excluir os dados de backup associados a uma máquina virtual durante o trabalho **Interromper backup** a qualquer momento depois que o trabalho de backup é concluído.</span><span class="sxs-lookup"><span data-stu-id="b8949-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="b8949-230">Pode até mesmo ser benéfico aguardar dias ou semanas antes de excluir os pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="b8949-231">Ao contrário de restaurar os pontos de recuperação, ao excluir os dados do backup, você não pode escolher os pontos de recuperação específicos para excluir.</span><span class="sxs-lookup"><span data-stu-id="b8949-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="b8949-232">Se você escolher excluir os dados de backup, apagará todos os pontos de recuperação associados ao item.</span><span class="sxs-lookup"><span data-stu-id="b8949-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="b8949-233">O procedimento a seguir pressupõe que o trabalho de Backup da máquina virtual foi interrompido ou desabilitado.</span><span class="sxs-lookup"><span data-stu-id="b8949-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="b8949-234">Depois que o trabalho de Backup é desabilitado, as opções **Retomar backup** e **Excluir backup** ficam disponíveis no painel de itens do cofre.</span><span class="sxs-lookup"><span data-stu-id="b8949-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Botões para retomar e excluir](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="b8949-236">Para excluir os dados de backup em uma máquina virtual com o *Backup desabilitado*:</span><span class="sxs-lookup"><span data-stu-id="b8949-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="b8949-237">No [painel de itens do cofre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Excluir backup**.</span><span class="sxs-lookup"><span data-stu-id="b8949-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="b8949-239">A folha **Excluir Dados do Backup** será aberta.</span><span class="sxs-lookup"><span data-stu-id="b8949-239">The **Delete Backup Data** blade opens.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="b8949-241">Você deve digitar o nome do item para confirmar que deseja excluir os pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8949-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="b8949-243">Se você não tiver certeza do nome do item, passe o mouse sobre o ponto de exclamação para exibir o nome.</span><span class="sxs-lookup"><span data-stu-id="b8949-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="b8949-244">Além disso, o nome do item está sob **Excluir Dados do Backup** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="b8949-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="b8949-245">Como opção, forneça um **Motivo** ou **Comentário**.</span><span class="sxs-lookup"><span data-stu-id="b8949-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="b8949-246">Para excluir os dados de backup para o item atual, clique em ![botão backup parar](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="b8949-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="b8949-247">Uma mensagem de notificação permite que você conheça os dados do backup que foram excluídos.</span><span class="sxs-lookup"><span data-stu-id="b8949-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8949-248">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8949-248">Next steps</span></span>
<span data-ttu-id="b8949-249">Para obter informações sobre como recriar uma máquina virtual a partir de um ponto de recuperação, verifique [Restaurar VMs do Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b8949-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="b8949-250">Se você precisar de informações sobre como proteger suas máquinas virtuais, consulte [Primeira consideração: fazer backup das VMs em um cofre dos Serviços de Recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b8949-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="b8949-251">Para obter informações sobre o monitoramento de eventos, confira [Monitorar alertas para backups de máquina virtual do Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b8949-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
