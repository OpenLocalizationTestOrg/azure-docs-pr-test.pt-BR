---
title: Usar armazenamento de Backup moderno com Servidor de Backup do Azure v2 | Microsoft Docs
description: "Saiba mais sobre os novos recursos no Servidor de Backup do Azure v2. Este artigo descreve como atualizar sua instalação do servidor de Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="45e8b-104">Adicionar armazenamento ao Servidor de Backup do Azure v2</span><span class="sxs-lookup"><span data-stu-id="45e8b-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="45e8b-105">Servidor de Backup do Azure v2 vem com o System Center 2016 Data Protection Manager armazenamento de backup moderno.</span><span class="sxs-lookup"><span data-stu-id="45e8b-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="45e8b-106">O armazenamento de Backup moderno oferece economia de armazenamento de 50%, backups de armazenamento três vezes mais rápido e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="45e8b-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="45e8b-107">Ele também oferece o armazenamento com reconhecimento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45e8b-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="45e8b-108">Para usar o armazenamento de Backup modernos, você deve executar servidor de Backup v2 no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="45e8b-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="45e8b-109">Se você executar o servidor de Backup v2 em uma versão anterior do Windows Server, servidor de Backup do Azure não poderá tirar proveito do armazenamento de Backup moderno.</span><span class="sxs-lookup"><span data-stu-id="45e8b-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="45e8b-110">Em vez disso, ele protegerá as cargas de trabalho, como ocorre com o servidor de Backup v1.</span><span class="sxs-lookup"><span data-stu-id="45e8b-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="45e8b-111">Para obter mais informações, consulte a versão do servidor de Backup [matriz proteção](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="45e8b-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="45e8b-112">Volumes no servidor de Backup v2</span><span class="sxs-lookup"><span data-stu-id="45e8b-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="45e8b-113">Servidor de Backup v2 aceita volumes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45e8b-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="45e8b-114">Quando você adiciona um volume, o servidor de Backup formata o volume para o sistema de arquivos resiliente (ReFS), que exige o armazenamento de Backup modernos.</span><span class="sxs-lookup"><span data-stu-id="45e8b-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="45e8b-115">Para adicionar um volume e expandi-lo mais tarde, se você precisar, sugerimos que você use esse fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="45e8b-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="45e8b-116">Configure o servidor Backup v2 em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45e8b-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="45e8b-117">Crie um volume em um disco virtual em um pool de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="45e8b-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="45e8b-118">Adicione um disco para um pool de armazenamento e crie um disco virtual com o layout simples.</span><span class="sxs-lookup"><span data-stu-id="45e8b-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="45e8b-119">Adicione quaisquer discos adicionais e estenda o disco virtual.</span><span class="sxs-lookup"><span data-stu-id="45e8b-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="45e8b-120">Crie volumes no disco virtual.</span><span class="sxs-lookup"><span data-stu-id="45e8b-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="45e8b-121">Adicione volumes ao servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="45e8b-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="45e8b-122">Configure o armazenamento com reconhecimento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45e8b-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="45e8b-123">Crie um volume para armazenamento de Backup moderno</span><span class="sxs-lookup"><span data-stu-id="45e8b-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="45e8b-124">Usar um Servidor de Backup v2 com volumes como armazenamento de disco pode ajudá-lo a manter o controle sobre o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45e8b-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="45e8b-125">Um volume pode ser um único disco.</span><span class="sxs-lookup"><span data-stu-id="45e8b-125">A volume can be a single disk.</span></span> <span data-ttu-id="45e8b-126">No entanto, se você quiser estender o armazenamento no futuro, crie um volume fora de um disco criado usando espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45e8b-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="45e8b-127">Isso pode ajudar se você quiser expandir o volume de armazenamento de backup.</span><span class="sxs-lookup"><span data-stu-id="45e8b-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="45e8b-128">Esta seção oferece as práticas recomendadas para a criação de um volume com esta instalação.</span><span class="sxs-lookup"><span data-stu-id="45e8b-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="45e8b-129">No Gerenciador do Servidor, selecione **Arquivo e Serviços de Armazenamento** > **Volumes** > **Pools de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="45e8b-130">Em **DISCOS FÍSICOS**, selecione **novo Pool de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Crie um novo pool de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="45e8b-132">Em **TAREFAS** caixa suspensa, selecione **novo Disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Adicione um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="45e8b-134">Selecione o pool de armazenamento e, em seguida, selecione **Adicionar Disco Físico**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Adicione um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="45e8b-136">Selecione o disco físico e, em seguida, selecione **Expandir Disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Estender o disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="45e8b-138">Selecione o disco virtual e, em seguida, selecione **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Criar um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="45e8b-140">No diálogo **Selecione o servidor e disco**, selecione o servidor e o novo disco.</span><span class="sxs-lookup"><span data-stu-id="45e8b-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="45e8b-141">Em seguida, selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-141">Then, select **Next**.</span></span>

    ![Selecione o servidor e disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="45e8b-143">Adicione volumes de armazenamento do servidor de Backup em disco</span><span class="sxs-lookup"><span data-stu-id="45e8b-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="45e8b-144">Para adicionar um volume ao servidor de Backup, no painel **Gerenciamento**, examinar novamente o armazenamento e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="45e8b-145">É exibida uma lista de todos os volumes disponíveis para serem adicionados para o armazenamento de servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="45e8b-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="45e8b-146">Depois dos volumes disponíveis serem adicionados à lista de volumes selecionados, você pode dar-lhes um nome amigável para te ajudar a gerenciá-los.</span><span class="sxs-lookup"><span data-stu-id="45e8b-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="45e8b-147">Para formatar esses volumes para ReFS para que o servidor de Backup possa usar os benefícios do armazenamento de Backup moderna, selecione **Ok**.</span><span class="sxs-lookup"><span data-stu-id="45e8b-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Adicione Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="45e8b-149">Configure o armazenamento com reconhecimento de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="45e8b-149">Set up workload-aware storage</span></span>

<span data-ttu-id="45e8b-150">Com o armazenamento com reconhecimento de carga de trabalho, você pode selecionar os volumes que armazenam preferencialmente determinados tipos de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45e8b-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="45e8b-151">Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) para armazenar apenas as cargas de trabalho que exigem backups frequentes de alto volume.</span><span class="sxs-lookup"><span data-stu-id="45e8b-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="45e8b-152">Um exemplo é o SQL Server com logs de transação.</span><span class="sxs-lookup"><span data-stu-id="45e8b-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="45e8b-153">Outras cargas de trabalho de backup com menos frequência, como VMs, podem ser feitas o backup de volumes de baixo custo.</span><span class="sxs-lookup"><span data-stu-id="45e8b-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="45e8b-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="45e8b-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="45e8b-155">Você pode configurar o armazenamento com reconhecimento de carga de trabalho usando o cmdlet do PowerShell Update-DPMDiskStorage, que atualiza as propriedades de um volume no pool de armazenamento em um servidor do Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="45e8b-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="45e8b-156">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="45e8b-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="45e8b-157">A captura de tela a seguir mostra o cmdlet Update-DPMDiskStorage na janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45e8b-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![O comando Update-DPMDiskStorage na janela do PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="45e8b-159">As alterações feitas por meio do PowerShell são refletidas no Console do administrador do servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="45e8b-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Discos e volumes no Console do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="45e8b-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45e8b-161">Next steps</span></span>
<span data-ttu-id="45e8b-162">Depois de instalar o Servidor de Backup, saiba como preparar seu servidor, ou começar a proteger uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45e8b-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="45e8b-163">Preparar as cargas de trabalho do Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="45e8b-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="45e8b-164">Usar o Servidor de Backup para fazer backup de um Servidor do VMware</span><span class="sxs-lookup"><span data-stu-id="45e8b-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="45e8b-165">Usar o Servidor de Backup para fazer backup de um SQL Server</span><span class="sxs-lookup"><span data-stu-id="45e8b-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

