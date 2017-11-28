---
title: "backups de máquina de virtual implantada para o Gerenciador de recursos de aaaManage | Microsoft Docs"
description: "Saiba como toomanage e monitor de backups de máquina de virtual implantada para o Gerenciador de recursos"
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
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="7124f-103">Gerenciar backups de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="7124f-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7124f-104">Gerenciar backups da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="7124f-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="7124f-105">Gerenciar backups de VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="7124f-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="7124f-106">Este artigo fornece orientação sobre como gerenciar backups VM e explica as informações de alertas de backup Olá disponíveis no painel do portal hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="7124f-107">diretrizes de saudação neste artigo se aplicam a toousing VMs com os cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7124f-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="7124f-108">Este artigo não aborda a criação de saudação de máquinas virtuais, nem explicam como máquinas virtuais de tooprotect.</span><span class="sxs-lookup"><span data-stu-id="7124f-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="7124f-109">Para um livro de instruções sobre como proteger VMs do Azure Resource Manager implantados no Azure com um cofre de serviços de recuperação, consulte [primeiro olhar: fazer backup de máquinas virtuais tooa Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7124f-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="7124f-110">Gerenciar cofres e máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="7124f-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="7124f-111">Olá portal do Azure, painel de Cofre de serviços de recuperação de saudação fornece acesso tooinformation sobre Olá cofre, inclusive:</span><span class="sxs-lookup"><span data-stu-id="7124f-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="7124f-112">Olá mais recente backup de instantâneo, que também é o ponto de restauração mais recente hello < br\></span><span class="sxs-lookup"><span data-stu-id="7124f-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="7124f-113">Olá a política de backup < br\></span><span class="sxs-lookup"><span data-stu-id="7124f-113">hello backup policy <br\></span></span>
* <span data-ttu-id="7124f-114">tamanho total de todos os instantâneos do backup <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="7124f-115">número de máquinas virtuais que são protegidas com o cofre hello < br\></span><span class="sxs-lookup"><span data-stu-id="7124f-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="7124f-116">Muitas tarefas de gerenciamento com um backup de máquinas virtuais começam com abrindo Olá cofre no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="7124f-117">No entanto, como cofres podem ser usado tooprotect tooview detalhes sobre uma determinada VM, abrem vários itens (ou várias VMs), painel de item de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="7124f-118">Olá procedimento a seguir mostra como Olá tooopen *painel Cofre* e, em seguida, continue toohello *painel Cofre de item*.</span><span class="sxs-lookup"><span data-stu-id="7124f-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="7124f-119">Há "dicas" nos dois procedimentos que destacam como tooadd Olá cofre e cofre toohello de item do painel do Azure usando o comando de toodashboard Olá Pin.</span><span class="sxs-lookup"><span data-stu-id="7124f-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="7124f-120">Toodashboard de PIN é uma maneira de criar um cofre do atalho toohello ou item.</span><span class="sxs-lookup"><span data-stu-id="7124f-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="7124f-121">Você também pode executar comandos comuns do atalho hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="7124f-122">Se você tiver vários painéis e abrir folhas, use o controle deslizante de azul escuro Olá final Olá Olá Olá de tooslide da janela do painel do Azure e para trás.</span><span class="sxs-lookup"><span data-stu-id="7124f-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Exibição completa com controle deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="7124f-124">Abra um cofre de serviços de recuperação no painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="7124f-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="7124f-125">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7124f-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7124f-126">No menu de Hub hello, clique em **procurar** e, na lista de saudação de recursos, digite **dos serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="7124f-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="7124f-127">Como começar a digitar, Olá filtros de lista com base em sua entrada.</span><span class="sxs-lookup"><span data-stu-id="7124f-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="7124f-128">Clique em **Cofre dos Serviços de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="7124f-128">Click **Recovery Services vault**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="7124f-130">saudação de lista de cofres de serviços de recuperação é exibida.</span><span class="sxs-lookup"><span data-stu-id="7124f-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="7124f-131">Listar cofres de Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="7124f-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="7124f-132">Se você fixar um painel do Azure de toohello do cofre, esse cofre é imediatamente acessível quando você abre Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7124f-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="7124f-133">toopin um painel de toohello do cofre, na lista de cofre hello, cofre hello e selecione **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="7124f-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="7124f-134">Saudação de cofres, selecione lista Olá cofre tooopen seu painel.</span><span class="sxs-lookup"><span data-stu-id="7124f-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="7124f-135">Quando você seleciona o cofre hello, painel de cofre hello e Olá **configurações** folha aberta.</span><span class="sxs-lookup"><span data-stu-id="7124f-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="7124f-136">Em Olá a imagem a seguir, Olá **Contoso cofre** painel é realçado.</span><span class="sxs-lookup"><span data-stu-id="7124f-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Abrir o painel do cofre e a folha de Configurações](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="7124f-138">Abra o painel do item do cofre</span><span class="sxs-lookup"><span data-stu-id="7124f-138">Open a vault item dashboard</span></span>
<span data-ttu-id="7124f-139">No procedimento anterior Olá você abriu o painel Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="7124f-140">Painel de item do tooopen Olá cofre:</span><span class="sxs-lookup"><span data-stu-id="7124f-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="7124f-141">No painel do cofre hello, em Olá **itens de Backup** lado a lado, clique em **máquinas virtuais do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7124f-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Bloco Abrir itens de backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="7124f-143">Olá **itens de Backup** Olá último backup trabalho para cada item de lista de folha.</span><span class="sxs-lookup"><span data-stu-id="7124f-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="7124f-144">Neste exemplo, há uma máquina virtual, demovm-markgal, protegida por esse cofre.</span><span class="sxs-lookup"><span data-stu-id="7124f-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="7124f-146">Para facilidade de acesso, você pode fixar um item de cofre toohello painel do Azure.</span><span class="sxs-lookup"><span data-stu-id="7124f-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="7124f-147">toopin um item de cofre, na lista de itens de cofre hello, item de saudação do botão direito do mouse e selecione **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="7124f-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="7124f-148">Em Olá **itens de Backup** folha, clique em Painel de item Olá item tooopen Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="7124f-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="7124f-150">Painel de item de cofre Hello e sua **configurações** folha aberta.</span><span class="sxs-lookup"><span data-stu-id="7124f-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Painel dos itens de backup com a folha Configurações](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="7124f-152">No painel de item de cofre hello, você pode executar várias tarefas de gerenciamento de chaves, como:</span><span class="sxs-lookup"><span data-stu-id="7124f-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="7124f-153">alterar as políticas ou criar uma nova política de backup <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="7124f-154">exibir pontos de restauração e ver seu estado de consistência <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="7124f-155">Backup sob demanda de uma máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="7124f-156">interromper a proteção das máquinas virtuais <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="7124f-157">retomar a proteção de uma máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="7124f-158">excluir os dados do backup (ou ponto de recuperação) <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="7124f-159">[restaurar discos de backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="7124f-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="7124f-160">Olá procedimentos a seguir, Olá ponto de partida é painel de item de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="7124f-161">Gerenciar políticas de backup</span><span class="sxs-lookup"><span data-stu-id="7124f-161">Manage backup policies</span></span>
1. <span data-ttu-id="7124f-162">Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **todas as configurações** tooopen Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="7124f-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Folha Política de backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="7124f-164">Em Olá **configurações** folha, clique em **política de Backup** tooopen folha.</span><span class="sxs-lookup"><span data-stu-id="7124f-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="7124f-165">Na folha de Olá, Olá retenção e frequência de intervalo detalhes de backup são mostradas.</span><span class="sxs-lookup"><span data-stu-id="7124f-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Folha Política de backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="7124f-167">De saudação **escolha a política de backup** menu:</span><span class="sxs-lookup"><span data-stu-id="7124f-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="7124f-168">políticas de toochange, selecione outra política e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7124f-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="7124f-169">nova política de saudação é aplicada imediatamente toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="7124f-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="7124f-170"><br\></span><span class="sxs-lookup"><span data-stu-id="7124f-170"><br\></span></span>
   * <span data-ttu-id="7124f-171">toocreate uma política, selecione **criar novo**.</span><span class="sxs-lookup"><span data-stu-id="7124f-171">toocreate a policy, select **Create New**.</span></span>

     ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="7124f-173">Para obter instruções sobre como criar uma política de backup, consulte [Definindo uma política de backup](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="7124f-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="7124f-174">Ao gerenciar políticas de backup, verifique se Olá de toofollow [práticas recomendadas](backup-azure-vms-introduction.md#best-practices) para desempenho ideal de backup</span><span class="sxs-lookup"><span data-stu-id="7124f-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="7124f-175">Backup sob demanda de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7124f-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="7124f-176">Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção.</span><span class="sxs-lookup"><span data-stu-id="7124f-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="7124f-177">Se o backup de saudação inicial está pendente, o backup por demanda cria uma cópia completa da máquina virtual de saudação em Olá que Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7124f-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="7124f-178">Se o backup de saudação inicial for concluída, um backup sob demanda enviará apenas as alterações do instantâneo anterior hello, toohello Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7124f-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="7124f-179">Ou seja, os backups subsequentes serão sempre incrementais.</span><span class="sxs-lookup"><span data-stu-id="7124f-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="7124f-180">período de retenção de saudação para um backup sob demanda é o valor de retenção de saudação especificado para o ponto de backup diário Olá na política de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="7124f-181">Se nenhum ponto de backup diário é selecionado, o ponto de backup semanal Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="7124f-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="7124f-182">backup tootrigger uma demanda de uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7124f-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="7124f-183">Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="7124f-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="7124f-185">portal de saudação certifica-se de que você deseja toostart um trabalho de backup sob demanda.</span><span class="sxs-lookup"><span data-stu-id="7124f-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="7124f-186">Clique em **Sim** trabalho de backup toostart hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-186">Click **Yes** toostart hello backup job.</span></span>

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="7124f-188">trabalho de backup Olá cria um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7124f-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="7124f-189">período de retenção Olá Olá do ponto de recuperação é Olá mesmo que o período de retenção especificado na diretiva de saudação associada à máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="7124f-190">progresso de saudação tootrack para trabalho hello, no painel do cofre hello, clique em Olá **trabalhos de Backup** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="7124f-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="7124f-191">Interromper a proteção de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="7124f-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="7124f-192">Se você escolher toostop proteger uma máquina virtual, você será solicitado a se quiser que os pontos de recuperação tooretain hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="7124f-193">Há duas maneiras de máquinas virtuais da proteção toostop:</span><span class="sxs-lookup"><span data-stu-id="7124f-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="7124f-194">parar todos os trabalhos de backup futuros e excluir todos os pontos de recuperação ou</span><span class="sxs-lookup"><span data-stu-id="7124f-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="7124f-195">parar todos os trabalhos de backup futuros, mas deixar Olá pontos de recuperação</span><span class="sxs-lookup"><span data-stu-id="7124f-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="7124f-196">Há um custo associado deixando Olá pontos de recuperação no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7124f-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="7124f-197">No entanto, a vantagem de saudação do deixando Olá pontos de recuperação é que você pode restaurar a máquina virtual de hello mais tarde, se desejado.</span><span class="sxs-lookup"><span data-stu-id="7124f-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="7124f-198">Para obter informações sobre o custo de saudação de deixar Olá pontos de recuperação, consulte Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="7124f-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="7124f-199">Se você escolher toodelete todos os pontos de recuperação, é possível restaurar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="7124f-200">proteção de toostop para uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7124f-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="7124f-201">Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **parar backup**.</span><span class="sxs-lookup"><span data-stu-id="7124f-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Botão Interromper backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="7124f-203">Abre a folha de parar Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-203">hello Stop Backup blade opens.</span></span>

    ![Folha Interromper backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="7124f-205">Em Olá **parar Backup** folha, escolha se tooretain ou delete Olá dados de backup.</span><span class="sxs-lookup"><span data-stu-id="7124f-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="7124f-206">caixa de informações de saudação fornece detalhes sobre sua escolha.</span><span class="sxs-lookup"><span data-stu-id="7124f-206">hello information box provides details about your choice.</span></span>

    ![Parar a proteção](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="7124f-208">Se você escolher os dados de backup tooretain hello, ignore toostep 4.</span><span class="sxs-lookup"><span data-stu-id="7124f-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="7124f-209">Se você escolher os dados de backup toodelete, confirme que você deseja toostop trabalhos de backup hello e excluir pontos de recuperação Olá - nome de saudação do tipo de item de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="7124f-211">Se você não tiver certeza do nome do item hello, passe o mouse sobre o nome de Olá Olá exclamação tooview.</span><span class="sxs-lookup"><span data-stu-id="7124f-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="7124f-212">Além disso, o nome de saudação do item de saudação é em **parar Backup** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="7124f-213">Como opção, forneça um **Motivo** ou **Comentário**.</span><span class="sxs-lookup"><span data-stu-id="7124f-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="7124f-214">trabalho de backup toostop Olá para o item atual do hello, clique em ![botão backup parar](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="7124f-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="7124f-215">Uma mensagem de notificação permite que você saiba os trabalhos de backup Olá foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="7124f-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="7124f-217">Retomar a proteção de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7124f-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="7124f-218">Se hello **reter dados de Backup** opção foi escolhida quando a proteção para a máquina virtual de saudação foi interrompida, é possível tooresume proteção.</span><span class="sxs-lookup"><span data-stu-id="7124f-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="7124f-219">Se hello **excluir dados de Backup** opção foi escolhida, então não é possível retomar a proteção para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="7124f-220">tooresume proteção para a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="7124f-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="7124f-221">Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **retomar backup**.</span><span class="sxs-lookup"><span data-stu-id="7124f-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Retomar proteção](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="7124f-223">Abre a folha de política de Backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7124f-224">Ao proteger novamente a máquina virtual de hello, você pode escolher uma regra diferente que a política de saudação com a qual a máquina virtual foi inicialmente protegida.</span><span class="sxs-lookup"><span data-stu-id="7124f-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="7124f-225">Siga as etapas de saudação em [gerenciar políticas de backup](backup-azure-manage-vms.md#manage-backup-policies) tooassign política de saudação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="7124f-226">Após a política de backup Olá toohello aplicada virtual machine, você verá a seguinte mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![VM protegida com êxito](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="7124f-228">Excluir dados de backup</span><span class="sxs-lookup"><span data-stu-id="7124f-228">Delete Backup data</span></span>
<span data-ttu-id="7124f-229">Você pode excluir os dados de backup Olá associados a uma máquina virtual durante a saudação **parar backup** trabalho, ou a qualquer momento após Olá o trabalho de backup foi concluída.</span><span class="sxs-lookup"><span data-stu-id="7124f-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="7124f-230">Ainda pode ser benéfico toowait dias ou semanas antes da exclusão de pontos de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="7124f-231">Ao contrário de restaurar os pontos de recuperação, ao excluir dados de backup, você não pode escolher toodelete de pontos de recuperação específico.</span><span class="sxs-lookup"><span data-stu-id="7124f-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="7124f-232">Se você escolher toodelete os dados de backup, você pode excluir todos os pontos de recuperação associados ao item de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="7124f-233">Olá seguinte princípio de trabalho de Backup Olá para a máquina virtual de saudação foi interrompido ou desabilitado.</span><span class="sxs-lookup"><span data-stu-id="7124f-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="7124f-234">Depois que o trabalho de Backup Olá estiver desabilitado, Olá **retomar backup** e **excluir backup** opções estão disponíveis no painel de item de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Botões para retomar e excluir](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="7124f-236">dados de backup toodelete em uma máquina virtual com hello *Backup desabilitado*:</span><span class="sxs-lookup"><span data-stu-id="7124f-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="7124f-237">Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **excluir backup**.</span><span class="sxs-lookup"><span data-stu-id="7124f-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="7124f-239">Olá **excluir dados de Backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="7124f-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="7124f-241">Nome do tipo de saudação de Olá item tooconfirm você deseja que os pontos de recuperação toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="7124f-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="7124f-243">Se você não tiver certeza do nome do item hello, passe o mouse sobre o nome de Olá Olá exclamação tooview.</span><span class="sxs-lookup"><span data-stu-id="7124f-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="7124f-244">Além disso, o nome de saudação do item de saudação é em **excluir dados de Backup** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7124f-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="7124f-245">Como opção, forneça um **Motivo** ou **Comentário**.</span><span class="sxs-lookup"><span data-stu-id="7124f-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="7124f-246">os dados de backup toodelete Olá para o item atual do hello, clique em ![botão backup parar](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="7124f-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="7124f-247">Uma mensagem de notificação permite que você saiba os dados de backup Olá foi excluídos.</span><span class="sxs-lookup"><span data-stu-id="7124f-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7124f-248">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7124f-248">Next steps</span></span>
<span data-ttu-id="7124f-249">Para obter informações sobre como recriar uma máquina virtual a partir de um ponto de recuperação, verifique [Restaurar VMs do Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="7124f-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="7124f-250">Se você precisar obter informações sobre como proteger suas máquinas virtuais, consulte [primeiro olhar: fazer backup de máquinas virtuais tooa Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7124f-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="7124f-251">Para obter informações sobre o monitoramento de eventos, confira [Monitorar alertas para backups de máquina virtual do Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="7124f-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
