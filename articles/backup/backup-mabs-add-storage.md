---
title: aaaUse modernos o armazenamento de Backup com o servidor de Backup do Azure v2 | Microsoft Docs
description: "Saiba mais sobre os novos recursos Olá no servidor de Backup do Azure v2. Este artigo descreve como tooupgrade a instalação do servidor de Backup."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="49908-104">Adicionar armazenamento tooAzure v2 do servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="49908-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="49908-105">Servidor de Backup do Azure v2 vem com o System Center 2016 Data Protection Manager armazenamento de backup moderno.</span><span class="sxs-lookup"><span data-stu-id="49908-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="49908-106">O armazenamento de Backup moderno oferece economia de armazenamento de 50%, backups de armazenamento três vezes mais rápido e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="49908-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="49908-107">Ele também oferece o armazenamento com reconhecimento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="49908-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="49908-108">toouse modernos o armazenamento de Backup, você deve executar v2 do servidor de Backup no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="49908-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="49908-109">Se você executar o servidor de Backup v2 em uma versão anterior do Windows Server, servidor de Backup do Azure não poderá tirar proveito do armazenamento de Backup moderno.</span><span class="sxs-lookup"><span data-stu-id="49908-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="49908-110">Em vez disso, ele protegerá as cargas de trabalho, como ocorre com o servidor de Backup v1.</span><span class="sxs-lookup"><span data-stu-id="49908-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="49908-111">Para obter mais informações, consulte a versão do servidor de Backup Olá [matriz proteção](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="49908-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="49908-112">Volumes no servidor de Backup v2</span><span class="sxs-lookup"><span data-stu-id="49908-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="49908-113">Servidor de Backup v2 aceita volumes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49908-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="49908-114">Quando você adicionar um volume, o servidor de Backup formata Olá volume tooResilient arquivo ReFS (sistema), que exige o armazenamento de Backup modernos.</span><span class="sxs-lookup"><span data-stu-id="49908-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="49908-115">tooadd um volume e tooexpand-lo mais tarde se necessário, sugerimos que você use esse fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="49908-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="49908-116">Configure o servidor Backup v2 em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49908-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="49908-117">Crie um volume em um disco virtual em um pool de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="49908-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="49908-118">Adicionar um pool de armazenamento do disco tooa e criar um disco virtual com o layout simples.</span><span class="sxs-lookup"><span data-stu-id="49908-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="49908-119">Adicionar discos adicionais e expandir disco virtual hello.</span><span class="sxs-lookup"><span data-stu-id="49908-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="49908-120">Crie volumes no disco virtual hello.</span><span class="sxs-lookup"><span data-stu-id="49908-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="49908-121">Adicione Olá volumes tooBackup Server.</span><span class="sxs-lookup"><span data-stu-id="49908-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="49908-122">Configure o armazenamento com reconhecimento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="49908-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="49908-123">Crie um volume para armazenamento de Backup moderno</span><span class="sxs-lookup"><span data-stu-id="49908-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="49908-124">Usar um Servidor de Backup v2 com volumes como armazenamento de disco pode ajudá-lo a manter o controle sobre o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49908-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="49908-125">Um volume pode ser um único disco.</span><span class="sxs-lookup"><span data-stu-id="49908-125">A volume can be a single disk.</span></span> <span data-ttu-id="49908-126">No entanto, se você quiser tooextend armazenamento Olá futuros, crie um volume fora de um disco criado usando espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49908-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="49908-127">Isso pode ajudar se você quiser tooexpand volume de saudação para armazenamento de backup.</span><span class="sxs-lookup"><span data-stu-id="49908-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="49908-128">Esta seção oferece as práticas recomendadas para a criação de um volume com esta instalação.</span><span class="sxs-lookup"><span data-stu-id="49908-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="49908-129">No Gerenciador do Servidor, selecione **Arquivo e Serviços de Armazenamento** > **Volumes** > **Pools de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="49908-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="49908-130">Em **DISCOS FÍSICOS**, selecione **novo Pool de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="49908-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Crie um novo pool de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="49908-132">Em Olá **tarefas** caixa de lista suspensa, selecione **novo disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="49908-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Adicione um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="49908-134">Selecione o pool de armazenamento hello e, em seguida, selecione **adicionar disco físico**.</span><span class="sxs-lookup"><span data-stu-id="49908-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Adicione um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="49908-136">Selecione o disco físico hello e, em seguida, selecione **Expandir Disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="49908-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Expandir disco virtual Olá](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="49908-138">Selecione o disco virtual hello e, em seguida, selecione **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="49908-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Criar um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="49908-140">Em Olá **Selecionar servidor de saudação e disco** caixa de diálogo, o servidor de saudação selecione e o novo disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="49908-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="49908-141">Em seguida, selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="49908-141">Then, select **Next**.</span></span>

    ![Selecione o disco e o servidor de saudação](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="49908-143">Adicione o armazenamento de disco do servidor de tooBackup volumes</span><span class="sxs-lookup"><span data-stu-id="49908-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="49908-144">tooadd tooBackup um volume no servidor, em Olá **gerenciamento** , examinar novamente armazenamento hello e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49908-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="49908-145">É exibida uma lista de todos os Olá volumes disponíveis toobe adicionado para o armazenamento de servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="49908-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="49908-146">Depois de volumes disponíveis são adicionados toohello lista dos volumes selecionados, você pode fornecer toohelp um nome amigável que você gerenciá-los.</span><span class="sxs-lookup"><span data-stu-id="49908-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="49908-147">tooformat tooReFS esses volumes para fazer Backup do servidor possa usar os benefícios de saudação do armazenamento de Backup moderna, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="49908-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Adicione Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="49908-149">Configure o armazenamento com reconhecimento de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="49908-149">Set up workload-aware storage</span></span>

<span data-ttu-id="49908-150">Com o armazenamento com reconhecimento de carga de trabalho, você pode selecionar os volumes de saudação que armazenam preferencialmente determinados tipos de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="49908-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="49908-151">Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) toostore somente Olá cargas de trabalho que exigem backups frequentes, de alto volume.</span><span class="sxs-lookup"><span data-stu-id="49908-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="49908-152">Um exemplo é o SQL Server com logs de transação.</span><span class="sxs-lookup"><span data-stu-id="49908-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="49908-153">Outras cargas de trabalho de backup com menos frequência, como VMs, podem fazer backup de volumes toolow custo.</span><span class="sxs-lookup"><span data-stu-id="49908-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="49908-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="49908-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="49908-155">Você pode configurar o armazenamento com reconhecimento de carga de trabalho usando o cmdlet do PowerShell Olá Update-DPMDiskStorage, que atualiza as propriedades de saudação de um volume no pool de armazenamento de saudação em um servidor do Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="49908-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="49908-156">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="49908-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="49908-157">Olá seguinte captura de tela mostra Olá atualização DPMDiskStorage cmdlet na janela do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="49908-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Olá DPMDiskStorage de atualização de comando na janela do PowerShell Olá](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="49908-159">Olá alterações usando o PowerShell são refletidas no hello Console do administrador do servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="49908-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Discos e volumes no hello Console do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="49908-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49908-161">Next steps</span></span>
<span data-ttu-id="49908-162">Depois de instalar o servidor de Backup, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="49908-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="49908-163">Preparar as cargas de trabalho do Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="49908-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="49908-164">Usar o servidor de Backup tooback um servidor VMware</span><span class="sxs-lookup"><span data-stu-id="49908-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="49908-165">Usar o servidor de Backup tooback o SQL Server</span><span class="sxs-lookup"><span data-stu-id="49908-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

